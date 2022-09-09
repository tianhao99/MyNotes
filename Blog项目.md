# Blog项目技术整理

## 一、技术亮点

### 1、JWT+Redis

- **jwt + redis 使用token令牌的登录，访问认证速度快，实现session共享，安全性较高。 redis做了token令牌和用户信息的对应管理。**
- 1. **访问接口token验证，进一步增加了安全性** 
  2. **登录用户做了缓存** 
  3. **灵活控制用户的过期时间（可以续期，踢掉线等）**

- jwt 可以生成 一个加密的token，做为用户登录的令牌，当用户登录成功之后，发放给客户端。 当请求需要登录的资源或者接口的时候，将token携带，后端验证token是否合法。
- 首先在登陆之前在redis数据库中对数据进行查询，看是否存在该条数据，如果不存在的话，就去数据库查找，然后在查找到之后，在正常登录的时候将数据存储到redis中，当然这个存储信息的键值对也就是在redis查询的那个数据，然后下次如果再次执行访问的时候，在redis中就有了此数据，进而提高了访问的效率。
- 细节：存储用户的登录信息，存储在redis中的时候使用的是hash数据结构，【hash数据结构其实就是，对应的键值对的值是一个字典类型。】此时就可以将用户携带的唯一标识作为值的键，将用户的其他某个信息作为该键的值存储起来。

### 2、ThreadLocal线程隔离

- 本地线程变量保存用户信息副本到每一个线程中【线程封闭，不会出现线程并发安全问题】。

  在请求的线程之内，可以随时获取登录的用户，在使用完ThreadLocal之后，**做了对value的删除，防止了内存泄漏**。

- 【内存泄露】

  【弱引用，jvm垃圾回收就会收走key，剩一个没有key的value造成泄露】

  > `ThreadLocalMap` 为 `ThreadLocal` 的一个静态内部类，里面定义了`Entry` 来保存数据。而且是继承的弱引用。在`Entry`内部使用`ThreadLocal`作为`key`，使用我们设置的`value`作为`value`。
  >
  > 如果 `key threadlocal` 为 `null` 了，这个 `entry` 就可以清除了。
  >
  > ThreadLocalMap中的key为ThreadLocal的弱引用，当key为`null`时，ThreadLocal会被当成垃圾回收 。
  >
  > ```Java
  >  //首先获取当前线程对象
  >  Thread t = Thread.currentThread();
  >  //获取线程中变量 ThreadLocal.ThreadLocalMap
  >  ThreadLocalMap map = getMap(t); //弱引用
  > ```
  >
  > **虽然ThreadLocalMap的key没了，但是value还在，这就造成了内存泄漏。**

![image-20220710175107187](https://gitee.com/yang-chuanwei/typora-img/raw/master/img/image-20220710175107187.png)

 

- **线程安全** 

  - 更新文章阅读数时，进行判断，是否等于原有的viewCount，如果不是，表明已经被更新了，算是乐观锁

  - update table set value = [newValue] where id=[xx] and value=[oldValue]

  - > **CAS**：CAS是Compare And Swap的简称，即：比较并交换。这是当前的处理器基本都支持的一种指令。每个CAS指令包括三个运算符，一个内存地址V，一个期望值A和一个新值B，CAS指令执行的时候是去判断这个地址V上的值和期望值A是否相等，相等则将地址V上的值修改为新值B，不等则不作任何操作。CAS操作实际实现是在一个循环中不断执行CAS指令，直到成功为止。

  - 

  - ```java
    查看完文章之后，本应该直接返回数据了，这时候做了一个更新操作，更新时加写锁，阻塞其他的读操作，性能就会比较低
    // 更新 增加了此次接口的 耗时 如果一旦更新出问题，不能影响 查看文章的操作
    //线程池  可以把更新操作 扔到线程池中去执行，和主线程就不相关了
    threadService.updateArticleViewCount(articleMapper,article);
    ```

    

- **线程池**

  - **@Async** 对当前的主业务流程无影响的操作，放入线程池执行。

  比如==加载文章详情==和==文章阅读数更新==，这两个业务流程需要分开执行，互不影响。

- 创线程池配置类

  - 起名为```taskExecutor```

  - ```java
    @Configuration
    @EnableAsync //开启多线程
    public class ThreadPoolConfig {
    
        @Bean("taskExecutor")
        public Executor asyncServiceExecutor() {
            ThreadPoolTaskExecutor executor = new ThreadPoolTaskExecutor();
            // 设置核心线程数
            executor.setCorePoolSize(5);
            // 设置最大线程数
            executor.setMaxPoolSize(20);
            //配置队列大小
            executor.setQueueCapacity(Integer.MAX_VALUE);
            // 设置线程活跃时间（秒）
            executor.setKeepAliveSeconds(60);
            // 设置默认线程名称
            executor.setThreadNamePrefix("博客项目");
            // 等待所有任务结束后再关闭线程池
            executor.setWaitForTasksToCompleteOnShutdown(true);
            //执行初始化
            executor.initialize();
            return executor;
        }
    }
    ```

  在需要多线程操作的部分直接注解

  ```java
  @Component
  public class ViewCountHandler {
  
      @Async("taskExecutor") //直接将这个方法-扔到线程池 执行
      public void scheduled(){
  
      }
  }
  ```

### 3、SpringSecurity 权限管理系统

- 引入依赖【完整的一套框架，包括登录页面】

- 创建UserDetailsService接口的实现类，-------实现去数据库查找账户密码操作。

- 修改SpringSecurity 配置类

  - 关闭csrf

    - 如果自定义登录 需要关闭

  - 修改登录页面【并放行登录页相关的静态文件】

  - 修改退出登录结果页面

  - 修改默认加密方式BCrypt

  - 自定义```@authService.auth(request,authentication) ```实现实时的权限检查

    - ```java
      //获取
      Object principal = authentication.getPrincipal();
      //若为空，表示未登录若不空直接强转为
      UserDetails userDetails = (UserDetails) principal;
      //然后获取userDetails的name或者id，通过name或者id去数据库的权限表中查询权限有权限，则返回true，无权限返回false
      ```

  ![image-20220901161433884](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220901161433884.png)

![image-20220901160805277](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220901160805277.png)

### 4、统一日志记录

- ==注解主要实现，对需要记录日志的Controller上增加注解，实现运行的方法名和具体操作输出，了解运行情况。==

1、自定义注解

```java
//Type 代表可以放在类上面 Method 代表可以放在方法上
@Target({ElementType.METHOD})
@Retention(RetentionPolicy.RUNTIME)
@Documented
public @interface LogAnnotation {

    String module() default "";

    String operator() default "";
}
```

2、定义了通知和切点的关系

```java
@Component
@Aspect //切面 定义了通知和切点的关系
@Slf4j
public class LogAspect {
		// 切点引用自定义的注解
    @Pointcut("@annotation(com.mszlu.blog.common.aop.LogAnnotation)")
    public void pt(){}

    //环绕通知
    @Around("pt()")
    public Object log(ProceedingJoinPoint joinPoint) throws Throwable {
        long beginTime = System.currentTimeMillis();
        //执行方法
        Object result = joinPoint.proceed();
        //执行时长(毫秒)
        long time = System.currentTimeMillis() - beginTime;
        //保存日志
        recordLog(joinPoint, time);
        return result;
    }

    private void recordLog(ProceedingJoinPoint joinPoint, long time) {
        MethodSignature signature = (MethodSignature) joinPoint.getSignature();
        Method method = signature.getMethod();
        LogAnnotation logAnnotation = method.getAnnotation(LogAnnotation.class);
        log.info("=====================log start================================");
        log.info("module:{}",logAnnotation.module());
        log.info("operation:{}",logAnnotation.operator());

        //请求的方法名
        String className = joinPoint.getTarget().getClass().getName();
        String methodName = signature.getName();
        log.info("request method:{}",className + "." + methodName + "()");

//        //请求的参数
        Object[] args = joinPoint.getArgs();
        String params = JSON.toJSONString(args[0]);
        log.info("params:{}",params);

        //获取request 设置IP地址
        HttpServletRequest request = HttpContextUtils.getHttpServletRequest();
        log.info("ip:{}", IpUtils.getIpAddr(request));


        log.info("excute time : {} ms",time);
        log.info("=====================log end================================");
    }
}
```

3、使用

直接对Controller进行注解，自己定义的注解

```java
    @PostMapping
    //加上此注解 代表要对此接口记录日志
    @LogAnnotation(module="文章",operator="获取文章列表")
    public Result listArticle(@RequestBody PageParams pageParams){
        return articleService.listArticle(pageParams);
    }
```

### 5、统一缓存处理

- 注解主要实现，对需要缓存的的Controller上增加注解，实现运行时先检查缓存，

  - 缓存中存在：从缓存取数据，更高效，

  - 缓存中不存在：去数据库中查找，然后存入缓存，下次调用直接从缓存读取，

原理同上，使用时也是直接在Controller上注解自己定义的缓存注解

```java
@Target({ElementType.METHOD})
@Retention(RetentionPolicy.RUNTIME)
@Documented
public @interface Cache {

    long expire() default 1 * 60 * 1000;
    //缓存标识 key
    String name() default "";

}
```

```java
//aop 定义一个切面，切面定义了切点和通知的关系
@Aspect
@Component
@Slf4j
public class CacheAspect {

    private static final ObjectMapper objectMapper = new ObjectMapper();


    @Autowired
    private RedisTemplate<String, String> redisTemplate;

    @Pointcut("@annotation(com.mszlu.blog.common.cache.Cache)")
    public void pt(){}

    @Around("pt()")
    public Object around(ProceedingJoinPoint pjp){
        try {
            Signature signature = pjp.getSignature();
            //类名
            String className = pjp.getTarget().getClass().getSimpleName();
            //调用的方法名
            String methodName = signature.getName();


            Class[] parameterTypes = new Class[pjp.getArgs().length];
            Object[] args = pjp.getArgs();
            //参数
            String params = "";
            for(int i=0; i<args.length; i++) {
                if(args[i] != null) {
                    params += JSON.toJSONString(args[i]);
                    parameterTypes[i] = args[i].getClass();
                }else {
                    parameterTypes[i] = null;
                }
            }
            if (StringUtils.isNotEmpty(params)) {
                //加密 以防出现key过长以及字符转义获取不到的情况
                params = DigestUtils.md5Hex(params);
            }
            Method method = pjp.getSignature().getDeclaringType().getMethod(methodName, parameterTypes);
            //获取Cache注解
            Cache annotation = method.getAnnotation(Cache.class);
            //缓存过期时间
            long expire = annotation.expire();
            //缓存名称
            String name = annotation.name();
            //先从redis获取
            String redisKey = name + "::" + className+"::"+methodName+"::"+params;
            String redisValue = redisTemplate.opsForValue().get(redisKey);
            if (StringUtils.isNotEmpty(redisValue)){
                log.info("走了缓存~~~,{}",redisKey);
                Result result = JSON.parseObject(redisValue, Result.class);
                return result;
            }
            Object proceed = pjp.proceed();
            redisTemplate.opsForValue().set(redisKey,JSON.toJSONString(proceed), Duration.ofMillis(expire));
            log.info("存入缓存~~~ {},{}",className,methodName);
            return proceed;
        } catch (Throwable throwable) {
            throwable.printStackTrace();
        }
        return Result.fail(-999,"系统错误");
    }

}
```

```java
    @PostMapping
    //加上此注解 代表要对此接口先走缓存
    @Cache(expire = 5 * 60 * 1000,name = "listArticle")
    public Result listArticle(@RequestBody PageParams pageParams){
        return articleService.listArticle(pageParams);
    }
```



### 6、统一异常拦截

任何异常，直接拦截，输出异常内容，返回Result格式JSON



**@ControllerAdvice   注解全局拦截**

```java
//对加了@Controller注解的方法进行拦截处理 AOP的实现
@ControllerAdvice //全局拦截
public class AllExceptionHandler {
    //进行异常处理，处理Exception.class的异常
    @ExceptionHandler(Exception.class)
    @ResponseBody //返回json数据
    public Result doException(Exception ex){
        ex.printStackTrace();
        return Result.fail(-999,"系统异常");
    }

}
```

### 7、登录拦截

- **实现HandlerInterceptor接口**

  - 重写preHandle方法，拦截，检查请求
    -  调用时间：Controller方法处理之前
    - 若返回false，则中断执行，注意：不会进入afterCompletion
    - 需要判断 请求的接口路径 是否为 HandlerMethod (controller方法)
    - 判断 token是否为空，如果为空 未登录
    - 如果token 不为空，登录验证 loginService checkToken
    - 如果认证成功 放行即可

  - **重写afterCompletion方法，释放资源**
    - 调用前提：preHandle返回true
    - 调用时间：DispatcherServlet进行视图的渲染之后
    - 多用于清理资源

- **重写WebMVCConfig配置类，标注拦截内容**

  - 将自己写的拦截器，注册到Interceptor中，要不然不生效，并设置拦截路径和放行路径

  - 一般全部拦截，放行登录和注册页面即可，但是博客文章，不用登录也能看，就不做拦截，仅拦截发布文章和发表评论

  - ```java
    @Configuration
    public class WebMVCConfig implements WebMvcConfigurer {
        @Autowired
        private LoginInterceptor loginInterceptor;
    
        @Override
        public void addCorsMappings(CorsRegistry registry) {
    //        //跨域配置
            registry.addMapping("/**").allowedOrigins("https://blog.mszlu.com","http://blog1.mszlu.com","http://localhost:8080");
        }
    
        // 将自己写的拦截器，注册到Interceptor中，要不然不生效，并设置拦截路径和放行路径
        // 一般全部拦截，放行登录和注册页面即可，但是博客文章，不用登录也能看，就不做拦截，仅拦截发布文章和发表评论
        @Override
        public void addInterceptors(InterceptorRegistry registry) {
            //拦截接口，后续实际遇到需要拦截的接口时，在配置为真正的拦截接口
            registry.addInterceptor(loginInterceptor)
                    .addPathPatterns("/comments/create/change")
                    .addPathPatterns("/articles/publish");
        }
    }
    ```

```java
@Component
@Slf4j
public class LoginInterceptor implements HandlerInterceptor {
    @Autowired
    private LoginService loginService;

    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {

        if (!(handler instanceof HandlerMethod)){
            //handler 可能是 RequestResourceHandler springboot 程序 访问静态资源 默认去classpath下的static目录去查询
            return true;
        }
        String token = request.getHeader("Authorization");

        log.info("=================request start===========================");
        String requestURI = request.getRequestURI();
        log.info("request uri:{}",requestURI);
        log.info("request method:{}",request.getMethod());
        log.info("token:{}", token);
        log.info("=================request end===========================");


        if (StringUtils.isBlank(token)){
            Result result = Result.fail(ErrorCode.NO_LOGIN.getCode(), "未登录");
            response.setContentType("application/json;charset=utf-8");
            response.getWriter().print(JSON.toJSONString(result));
            return false;
        }
        SysUser sysUser = loginService.checkToken(token);
        if (sysUser == null){
            Result result = Result.fail(ErrorCode.NO_LOGIN.getCode(), "未登录");
            response.setContentType("application/json;charset=utf-8");
            response.getWriter().print(JSON.toJSONString(result));
            return false;
        }
        //登录验证成功，放行
        //我希望在controller中 直接获取用户的信息 怎么获取?
        UserThreadLocal.put(sysUser);
        return true;
    }

    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
        //如果不删除 ThreadLocal中用完的信息 会有内存泄漏的风险
        UserThreadLocal.remove();
    }
}
```

### 8、事务处理

放止登录失败但写入账户密码到数据库，以及发表文章失败，却将数据写入数据库等操作，多这类操作的实现类加上事务注解，出现异常自动回滚

```java
@Service
@Transactional  // 事务注解
public class LoginServiceImpl implements LoginService {
		// 这是一个登录操作Service的实现类
}
```



### 9、定时执行

对于阅读量和评论来说，不能一成不变，设置定时任务，例每5秒刷新一次数据

- @EnableScheduling 在配置类上使用，开启计划任务的支持（类上）

- @Scheduled 来申明这是一个任务，包括cron,fixDelay,fixRate等类型（方法上，需先开启计划任务的支持）

```java
@Component
@Slf4j
@EnableScheduling
public class ViewCountHandler {

    @Scheduled(cron = "0/10 * * * * *")
    //@Scheduled(cron = "0 0 3 * * *") 生产环境 每天凌晨3点执行
    @Async("taskExecutor") //扔到线程池 执行
    public void scheduled(){
        // 这里执行刷新浏览量的具体操作
    }

}
```

## 二、优化方向

### 1、阅读数和评论数展示

现在在数据库中存储阅读数和评论数，每次写入要查库。

考虑把阅读数和评论数放到Redis 中，使用incr自增实现操作，然后再用定时任务，一段时间进行一次查库，将Redis中的数据写入到数据库中，这样减少了查库操作，提高了效率和用户体验

### 2、使用RocketMQ解决缓存一致性问题

因为在浏览文章等操作处加了缓存，提高速度，但是修改文章后，读取到的还是缓存中未修改的原文章。

导致浏览的数据无法及时更新。

通过RrcketMQ消息队列实现，在发布文章时，判断是否是修改操作，若是就发送一条消息给RocketMQ，告诉她可以修改缓存了。

