# 一、HelloWorld

**需求：浏览发送/hello请求，响应 Hello，Spring Boot 2 **

## **1、创建Maven工程**

![image-20220604203850183](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220604203850183.png)

## 2、**引入依赖**

```xml
		1、导入SpringBoot依赖
		<parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.3.4.RELEASE</version>
    </parent>

		2、导入对应工程的依赖，如这里是web工程，他会自动导入一系列web工程所需要的包
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
    </dependencies>
```

## 3、**创建主程序**

```java
/**
 * 主程序类
 * @SpringBootApplication：这是一个SpringBoot应用
 */
@SpringBootApplication
public class MainApplication {
    public static void main(String[] args) {
        SpringApplication.run(MainApplication.class,args);
    }
}
```

## 4、编写业务

```java
@RestController
public class HelloController {
    @RequestMapping("/hello")
    public String handle01(){
        return "Hello, Spring Boot 2!";
    }
}
```

## 5、测试

直接运行main程序即可

## 6、简化配置

所有配置在这里直接修改即可，简单易读

可修改配置的官方文档https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html#appendix.application-properties

![image-20220604210836860](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220604210836860.png)

```properties
# 修改端口号
server.port=8888
```

## 7、简化部署

### 1、添加依赖插件

```xml
<!--    直接将程序打包成jar包，称fat jar-->
    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
```

### 2、maven直接打包成jar包

![image-20220604210347798](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220604210347798.png)

### 3、打包结果

可在命令行直接运行

![](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220604210922512.png)

![image-20220604210421016](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220604210421016.png)

# 二、自动配置原理

## 1、依赖管理

 

- 父项目做依赖管理

```xml
依赖管理    
<parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.3.4.RELEASE</version>
</parent>

他的父项目
 <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-dependencies</artifactId>
        <version>2.3.4.RELEASE</version>
  </parent>

几乎声明了所有开发中常用的依赖的版本号,自动版本仲裁机制
```

- 开发导入starter场景启动器
  - 1、见到很多 spring-boot-starter-* ：*就某种场景，如web工程就是web
    2、只要引入starter，这个场景的所有常规需要的依赖我们都自动引入
    3、SpringBoot所有支持的场景
    https://docs.spring.io/spring-boot/docs/current/reference/html/using-spring-boot.html#using-boot-starter
    4、见到的  *-spring-boot-starter： 第三方为我们提供的简化开发的场景启动器。
    5、所有场景启动器最底层的依赖

```xml

<dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter</artifactId>
      <version>2.3.4.RELEASE</version>
      <scope>compile</scope>
</dependency>
```

- 无需关注版本号，自动版本仲裁
  - 1、引入依赖默认都可以不写版本<font color="red">【因为是自动装配，他就默认把需要的包，自己决定版本导入】</font>
  - 2、引入非版本仲裁的jar，要写版本号。

- 可以修改默认版本号

  - 1、查看spring-boot-dependencies里面规定当前依赖的版本 用的 key。

  - 2、在当前项目里面重写配置

  - 3、直接写一个版本号就行了

  - ```xml
    <properties>
      	<mysql.version>5.1.43</mysql.version>
    </properties>
    ```

## 2、自动配置内容

 

- 自动配好Tomcat
  - 引入Tomcat依赖。
  - 配置Tomcat
- 自动配好SpringMVC
  - 引入SpringMVC全套组件
  - 自动配好SpringMVC常用组件（功能）
- 自动配好Web常见功能，如：字符编码问题
  - SpringBoot帮我们配置好了所有web开发的常见场景

- 默认的包结构

  - 主程序main所在包及其下面的所有子包里面的组件都会被默认扫描进

  - 无需以前的包扫描配置，如果要扫描主程序外边的程序需如下更改

  - 想要改变扫描路径，```@SpringBootApplication(scanBasePackages="com.atguigu")```
    - 或者```@ComponentScan 指定扫描路径```

```java
@SpringBootApplication
等同于
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan("com.atguigu.boot")
```



- ﻿各种配置拥有默认值
  - 默认配置最终都是映射到某个类上，如：MultipartProperties
  - 配置文件的值最终会绑定每个类上，这个类会在容器中创建对象
- 按需加载所有自动配置项
  - 非常多的starter
  - 引入了哪些场景这个场景的自动配置才会开启
  - SpringBoot所有的自动配置功能都在 spring-boot-autoconfigure 包里面



## 3、容器功能

### 3.1、组件添加

#### 1、Configuration

- 基本使用

  - 配置类里面使用@Bean标注在方法上给容器注册组件，默认也是单实例的
  - 配置类本身也是组件
  - proxyBeanMethods：代理bean的方法
    -  ==Full(proxyBeanMethods =true)==
      - 【保证每个@Bean方法被调用多少次返回的组件都是单实例的】
      - 但是每次要检查容器中有没有，费时间    
    -  ==Lite(proxyBeanMethods =false)==
      - 【每个@Bean方法被调用多少次返回的组件都是新创建的】
      - 啥都不管直接new，时间短，但是不能保证单例     
    - 组件依赖必须使用Full模式默认。其他默认是否Lite模式
  - @Import({User.class, DBHelper.class})
    - 给容器中自动创建出这两个类型的组件、默认组件的名字就是全类名
  - @ImportResource("classpath:beans.xml")导入Spring的配置文件
    - <font color='red'>默认SpringBoot不需要写xml的配置文件，但是若导入到老文件，是xml写到，这时候就要用import注解导入</font>

- ```java
  #############################Configuration使用示例######################################################
  // 【默认是true，用单例创建，改成false每次用就直接创建，不去容器中查是否存在】
  @Configuration(proxyBeanMethods = false) //告诉SpringBoot这是一个配置类 == 配置文件
  public class MyConfig {
  
      /**
       * Full:外部无论对配置类中的这个组件注册方法调用多少次获取的都是之前注册容器中的单实例对象
       */
  
      @Bean("tom")
      public Pet tomcatPet(){
          return new Pet("tomcat");
      }
  }
  
  ```

#### 2、**@Bean、@Component、@Controller、@Service、@Repository**

#### 3、**@ComponentScan、@Import**

```java
// @Import({User.class, DBHelper.class})
//      给容器中自动创建出这两个类型的组件、默认组件的名字就是全类名,


@Import({User.class, DBHelper.class})
@Configuration() //告诉SpringBoot这是一个配置类 == 配置文件
public class MyConfig {
}
```

#### 4、@Conditional

条件装配：Conditional指定一个条件，满足条件就进行对应的组件注入

![image.png](https://pledge99.oss-cn-beijing.aliyuncs.com/img/1602835786727-28b6f936-62f5-4fd6-a6c5-ae690bd1e31d.png)

例如：

- **@ConditionalOnBean(name = "tom")**：当容器中有tom这个bean时，才可以注入下边的内容
- **@ConditionalOnMissingBean(name = "tom")**：容器中没有tom这个bean时，才能注入下边的bean

```java
=====================测试条件装配==========================
@Configuration() //告诉SpringBoot这是一个配置类 == 配置文件
//@ConditionalOnBean(name = "tom")
@ConditionalOnMissingBean(name = "tom")
public class MyConfig {
    @Bean("tom22")
    public Pet tomcatPet(){
        return new Pet("tomcat");
    }
}

public static void main(String[] args) {
        //1、返回我们IOC容器
        ConfigurableApplicationContext run = SpringApplication.run(MainApplication.class, args);

        //2、查看容器里面的组件
        String[] names = run.getBeanDefinitionNames();
        for (String name : names) {
            System.out.println(name);
        }

        boolean tom = run.containsBean("tom");
        System.out.println("容器中Tom组件："+tom);

        boolean user01 = run.containsBean("user01");
        System.out.println("容器中user01组件："+user01);

        boolean tom22 = run.containsBean("tom22");
        System.out.println("容器中tom22组件："+tom22);
    }
```

 

###  3.2、原生配置文件引入

#### 1、@ImportResource

假设原文件有如下xml配置文件，需要将haha和hehe类注入容器

```xml
======================beans.xml=========================
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">

    <bean id="haha" class="com.atguigu.boot.bean.User">
        <property name="name" value="zhangsan"></property>
        <property name="age" value="18"></property>
    </bean>

    <bean id="hehe" class="com.atguigu.boot.bean.Pet">
        <property name="name" value="tomcat"></property>
    </bean>
</beans>
```

通过注解实现

```java
@ImportResource("classpath:beans.xml")
public class MyConfig {}
======================测试=================
        boolean haha = run.containsBean("haha");
        boolean hehe = run.containsBean("hehe");
        System.out.println("haha："+haha);//true
        System.out.println("hehe："+hehe);//true
```

### 3.3、配置绑定

如何使用Java读取到properties文件中的内容，并且把它封装到JavaBean中，以供随时使用；

```java
// 以前的方式，单独有一个properties文件，然后顺序读取
public class getProperties {
     public static void main(String[] args) throws FileNotFoundException, IOException {
         Properties pps = new Properties();
         pps.load(new FileInputStream("a.properties"));
         Enumeration enum1 = pps.propertyNames();//得到配置文件的名字
         while(enum1.hasMoreElements()) {
             String strKey = (String) enum1.nextElement();
             String strValue = pps.getProperty(strKey);
             System.out.println(strKey + "=" + strValue);
             //封装到JavaBean。
         }
     }
 }
```

SpringBoot方式：

首先在application.properties中填写信息

![image-20220610192941074](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220610192941074.png)

#### 前提注解@ConfigurationProperties(prefix = "==key==")

- 在==对应类==上进行注解<font color='red'>@ConfigurationProperties(prefix = "key")</font>

- 需要有Component注解伴随，表示把类放到容器中

- key表示自定义的抬头，不能有大写字母

- ```java
  @Component
  @ConfigurationProperties(prefix = "mycar")
  public class Car {
      private String brand;
      private Integer price;
      public String getBrand() {
          return brand;
      }
      public void setBrand(String brand) {
          this.brand = brand;
      }
      public Integer getPrice() {
          return price;
      }
      public void setPrice(Integer price) {
          this.price = price;
      }
      @Override
      public String toString() {
          return "Car{" +
                  "brand='" + brand + '\'' +
                  ", price=" + price +
                  '}';
      }
  }
  
  ```

#### 方式1：@EnableConfigurationProperties + @ConfigurationProperties

不需要在某类上放Component注解了

- 在==配置类MyConfig==上注解

- @EnableConfigurationProperties表示开启==某类==的配置绑定功能

- 把==某类==这个组件自动注册到容器中

- ![image-20220610194716835](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220610194716835.png)

- ![image-20220610194758048](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220610194758048.png)

- ```java
  @EnableConfigurationProperties(Car.class)
  @Configuration()  
  public class MyConfig {
  	换言之：就是MyConfig里面没写Car的bean注册
      		通过注解标注想注册的类，然后注册MyConfig的时候，把他顺道也注册了
  }
  ```

#### 方法2：**@Component + @ConfigurationProperties**

![image-20220610194449117](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220610194449117.png)

- 然后就可以再controller中使用了

- ```java
  @RestController
  public class HelloController {
      @Autowired
      Car car;
  
      @RequestMapping("/car")
      public Car car(){
          return car;
      }
      @RequestMapping("/hello")
      public String handle01(){
          return "Hello SpringBoot 2 !";
      }
  }
  ```

## 4、引导加载自动配置类

```java
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan(excludeFilters = { @Filter(type = FilterType.CUSTOM, classes = TypeExcludeFilter.class),
		@Filter(type = FilterType.CUSTOM, classes = AutoConfigurationExcludeFilter.class) })
public @interface SpringBootApplication{}
```

-   @SpringBootConfiguration 

@Configuration。代表当前是一个配置类

-   @ComponentScan 

指定扫描哪些，Spring注解；

- @EnableAutoConfiguration

```java
@AutoConfigurationPackage
@Import(AutoConfigurationImportSelector.class)
public @interface EnableAutoConfiguration {}
```

- **@AutoConfigurationPackage**

  - 自动配置包？指定了默认的包规则

  - ```java
    @Import(AutoConfigurationPackages.Registrar.class)  //给容器中导入一个组件
    public @interface AutoConfigurationPackage {}
    
    //利用Registrar给容器中导入一系列组件
    //将指定的一个包下的所有组件导入进来？MainApplication 所在包下。
    ```

- **@Import(AutoConfigurationImportSelector.class)**

  - ```java
    1、利用getAutoConfigurationEntry(annotationMetadata);给容器中批量导入一些组件
    2、调用List<String> configurations = getCandidateConfigurations(annotationMetadata, attributes)获取到所有需要导入到容器中的配置类
    3、利用工厂加载 Map<String, List<String>> loadSpringFactories(@Nullable ClassLoader classLoader)；得到所有的组件
    4、从META-INF/spring.factories位置来加载一个文件。
    	默认扫描我们当前系统里面所有META-INF/spring.factories位置的文件
        spring-boot-autoconfigure-2.3.4.RELEASE.jar包里面也有META-INF/spring.factories
        
    ```

![image.png](https://pledge99.oss-cn-beijing.aliyuncs.com/img/1602845382065-5c41abf5-ee10-4c93-89e4-2a9b831c3ceb.png)

```xml
文件里面写死了spring-boot一启动就要给容器中加载的所有配置类
spring-boot-autoconfigure-2.3.4.RELEASE.jar/META-INF/spring.factories
# Auto Configure
org.springframework.boot.autoconfigure.EnableAutoConfiguration=\
org.springframework.boot.autoconfigure.admin.SpringApplicationAdminJmxAutoConfiguration,\
org.springframework.boot.autoconfigure.aop.AopAutoConfiguration,\
org.springframework.boot.autoconfigure.amqp.RabbitAutoConfiguration,\
org.springframework.boot.autoconfigure.batch.BatchAutoConfiguration,\
org.springframework.boot.autoconfigure.cache.CacheAutoConfiguration,\
org.springframework.boot.autoconfigure.cassandra.CassandraAutoConfiguration,\
org.springframework.boot.autoconfigure.context.ConfigurationPropertiesAutoConfiguration,\
org.springframework.boot.autoconfigure.context.LifecycleAutoConfiguration,\
org.springframework.boot.autoconfigure.context.MessageSourceAutoConfiguration,\
org.springframework.boot.autoconfigure.context.PropertyPlaceholderAutoConfiguration,\
org.springframework.boot.autoconfigure.couchbase.CouchbaseAutoConfiguration,\
org.springframework.boot.autoconfigure.dao.PersistenceExceptionTranslationAutoConfiguration,\
org.springframework.boot.autoconfigure.data.cassandra.CassandraDataAutoConfiguration,\
org.springframework.boot.autoconfigure.data.cassandra.CassandraReactiveDataAutoConfiguration,\
org.springframework.boot.autoconfigure.data.cassandra.CassandraReactiveRepositoriesAutoConfiguration,\
org.springframework.boot.autoconfigure.data.cassandra.CassandraRepositoriesAutoConfiguration,\
org.springframework.boot.autoconfigure.data.couchbase.CouchbaseDataAutoConfiguration,\
org.springframework.boot.autoconfigure.data.couchbase.CouchbaseReactiveDataAutoConfiguration,\
org.springframework.boot.autoconfigure.data.couchbase.CouchbaseReactiveRepositoriesAutoConfiguration,\
org.springframework.boot.autoconfigure.data.couchbase.CouchbaseRepositoriesAutoConfiguration,\
org.springframework.boot.autoconfigure.data.elasticsearch.ElasticsearchDataAutoConfiguration,\
org.springframework.boot.autoconfigure.data.elasticsearch.ElasticsearchRepositoriesAutoConfiguration,\
org.springframework.boot.autoconfigure.data.elasticsearch.ReactiveElasticsearchRepositoriesAutoConfiguration,\
org.springframework.boot.autoconfigure.data.elasticsearch.ReactiveElasticsearchRestClientAutoConfiguration,\
org.springframework.boot.autoconfigure.data.jdbc.JdbcRepositoriesAutoConfiguration,\
org.springframework.boot.autoconfigure.data.jpa.JpaRepositoriesAutoConfiguration,\
org.springframework.boot.autoconfigure.data.ldap.LdapRepositoriesAutoConfiguration,\
org.springframework.boot.autoconfigure.data.mongo.MongoDataAutoConfiguration,\
org.springframework.boot.autoconfigure.data.mongo.MongoReactiveDataAutoConfiguration,\
org.springframework.boot.autoconfigure.data.mongo.MongoReactiveRepositoriesAutoConfiguration,\
org.springframework.boot.autoconfigure.data.mongo.MongoRepositoriesAutoConfiguration,\
org.springframework.boot.autoconfigure.data.neo4j.Neo4jDataAutoConfiguration,\
org.springframework.boot.autoconfigure.data.neo4j.Neo4jRepositoriesAutoConfiguration,\
org.springframework.boot.autoconfigure.data.solr.SolrRepositoriesAutoConfiguration,\
org.springframework.boot.autoconfigure.data.r2dbc.R2dbcDataAutoConfiguration,\
org.springframework.boot.autoconfigure.data.r2dbc.R2dbcRepositoriesAutoConfiguration,\
org.springframework.boot.autoconfigure.data.r2dbc.R2dbcTransactionManagerAutoConfiguration,\
org.springframework.boot.autoconfigure.data.redis.RedisAutoConfiguration,\
org.springframework.boot.autoconfigure.data.redis.RedisReactiveAutoConfiguration,\
org.springframework.boot.autoconfigure.data.redis.RedisRepositoriesAutoConfiguration,\
org.springframework.boot.autoconfigure.data.rest.RepositoryRestMvcAutoConfiguration,\
org.springframework.boot.autoconfigure.data.web.SpringDataWebAutoConfiguration,\
org.springframework.boot.autoconfigure.elasticsearch.ElasticsearchRestClientAutoConfiguration,\
org.springframework.boot.autoconfigure.flyway.FlywayAutoConfiguration,\
org.springframework.boot.autoconfigure.freemarker.FreeMarkerAutoConfiguration,\
org.springframework.boot.autoconfigure.groovy.template.GroovyTemplateAutoConfiguration,\
org.springframework.boot.autoconfigure.gson.GsonAutoConfiguration,\
org.springframework.boot.autoconfigure.h2.H2ConsoleAutoConfiguration,\
org.springframework.boot.autoconfigure.hateoas.HypermediaAutoConfiguration,\
org.springframework.boot.autoconfigure.hazelcast.HazelcastAutoConfiguration,\
org.springframework.boot.autoconfigure.hazelcast.HazelcastJpaDependencyAutoConfiguration,\
org.springframework.boot.autoconfigure.http.HttpMessageConvertersAutoConfiguration,\
org.springframework.boot.autoconfigure.http.codec.CodecsAutoConfiguration,\
org.springframework.boot.autoconfigure.influx.InfluxDbAutoConfiguration,\
org.springframework.boot.autoconfigure.info.ProjectInfoAutoConfiguration,\
org.springframework.boot.autoconfigure.integration.IntegrationAutoConfiguration,\
org.springframework.boot.autoconfigure.jackson.JacksonAutoConfiguration,\
org.springframework.boot.autoconfigure.jdbc.DataSourceAutoConfiguration,\
org.springframework.boot.autoconfigure.jdbc.JdbcTemplateAutoConfiguration,\
org.springframework.boot.autoconfigure.jdbc.JndiDataSourceAutoConfiguration,\
org.springframework.boot.autoconfigure.jdbc.XADataSourceAutoConfiguration,\
org.springframework.boot.autoconfigure.jdbc.DataSourceTransactionManagerAutoConfiguration,\
org.springframework.boot.autoconfigure.jms.JmsAutoConfiguration,\
org.springframework.boot.autoconfigure.jmx.JmxAutoConfiguration,\
org.springframework.boot.autoconfigure.jms.JndiConnectionFactoryAutoConfiguration,\
org.springframework.boot.autoconfigure.jms.activemq.ActiveMQAutoConfiguration,\
org.springframework.boot.autoconfigure.jms.artemis.ArtemisAutoConfiguration,\
org.springframework.boot.autoconfigure.jersey.JerseyAutoConfiguration,\
org.springframework.boot.autoconfigure.jooq.JooqAutoConfiguration,\
org.springframework.boot.autoconfigure.jsonb.JsonbAutoConfiguration,\
org.springframework.boot.autoconfigure.kafka.KafkaAutoConfiguration,\
org.springframework.boot.autoconfigure.availability.ApplicationAvailabilityAutoConfiguration,\
org.springframework.boot.autoconfigure.ldap.embedded.EmbeddedLdapAutoConfiguration,\
org.springframework.boot.autoconfigure.ldap.LdapAutoConfiguration,\
org.springframework.boot.autoconfigure.liquibase.LiquibaseAutoConfiguration,\
org.springframework.boot.autoconfigure.mail.MailSenderAutoConfiguration,\
org.springframework.boot.autoconfigure.mail.MailSenderValidatorAutoConfiguration,\
org.springframework.boot.autoconfigure.mongo.embedded.EmbeddedMongoAutoConfiguration,\
org.springframework.boot.autoconfigure.mongo.MongoAutoConfiguration,\
org.springframework.boot.autoconfigure.mongo.MongoReactiveAutoConfiguration,\
org.springframework.boot.autoconfigure.mustache.MustacheAutoConfiguration,\
org.springframework.boot.autoconfigure.orm.jpa.HibernateJpaAutoConfiguration,\
org.springframework.boot.autoconfigure.quartz.QuartzAutoConfiguration,\
org.springframework.boot.autoconfigure.r2dbc.R2dbcAutoConfiguration,\
org.springframework.boot.autoconfigure.rsocket.RSocketMessagingAutoConfiguration,\
org.springframework.boot.autoconfigure.rsocket.RSocketRequesterAutoConfiguration,\
org.springframework.boot.autoconfigure.rsocket.RSocketServerAutoConfiguration,\
org.springframework.boot.autoconfigure.rsocket.RSocketStrategiesAutoConfiguration,\
org.springframework.boot.autoconfigure.security.servlet.SecurityAutoConfiguration,\
org.springframework.boot.autoconfigure.security.servlet.UserDetailsServiceAutoConfiguration,\
org.springframework.boot.autoconfigure.security.servlet.SecurityFilterAutoConfiguration,\
org.springframework.boot.autoconfigure.security.reactive.ReactiveSecurityAutoConfiguration,\
org.springframework.boot.autoconfigure.security.reactive.ReactiveUserDetailsServiceAutoConfiguration,\
org.springframework.boot.autoconfigure.security.rsocket.RSocketSecurityAutoConfiguration,\
org.springframework.boot.autoconfigure.security.saml2.Saml2RelyingPartyAutoConfiguration,\
org.springframework.boot.autoconfigure.sendgrid.SendGridAutoConfiguration,\
org.springframework.boot.autoconfigure.session.SessionAutoConfiguration,\
org.springframework.boot.autoconfigure.security.oauth2.client.servlet.OAuth2ClientAutoConfiguration,\
org.springframework.boot.autoconfigure.security.oauth2.client.reactive.ReactiveOAuth2ClientAutoConfiguration,\
org.springframework.boot.autoconfigure.security.oauth2.resource.servlet.OAuth2ResourceServerAutoConfiguration,\
org.springframework.boot.autoconfigure.security.oauth2.resource.reactive.ReactiveOAuth2ResourceServerAutoConfiguration,\
org.springframework.boot.autoconfigure.solr.SolrAutoConfiguration,\
org.springframework.boot.autoconfigure.task.TaskExecutionAutoConfiguration,\
org.springframework.boot.autoconfigure.task.TaskSchedulingAutoConfiguration,\
org.springframework.boot.autoconfigure.thymeleaf.ThymeleafAutoConfiguration,\
org.springframework.boot.autoconfigure.transaction.TransactionAutoConfiguration,\
org.springframework.boot.autoconfigure.transaction.jta.JtaAutoConfiguration,\
org.springframework.boot.autoconfigure.validation.ValidationAutoConfiguration,\
org.springframework.boot.autoconfigure.web.client.RestTemplateAutoConfiguration,\
org.springframework.boot.autoconfigure.web.embedded.EmbeddedWebServerFactoryCustomizerAutoConfiguration,\
org.springframework.boot.autoconfigure.web.reactive.HttpHandlerAutoConfiguration,\
org.springframework.boot.autoconfigure.web.reactive.ReactiveWebServerFactoryAutoConfiguration,\
org.springframework.boot.autoconfigure.web.reactive.WebFluxAutoConfiguration,\
org.springframework.boot.autoconfigure.web.reactive.error.ErrorWebFluxAutoConfiguration,\
org.springframework.boot.autoconfigure.web.reactive.function.client.ClientHttpConnectorAutoConfiguration,\
org.springframework.boot.autoconfigure.web.reactive.function.client.WebClientAutoConfiguration,\
org.springframework.boot.autoconfigure.web.servlet.DispatcherServletAutoConfiguration,\
org.springframework.boot.autoconfigure.web.servlet.ServletWebServerFactoryAutoConfiguration,\
org.springframework.boot.autoconfigure.web.servlet.error.ErrorMvcAutoConfiguration,\
org.springframework.boot.autoconfigure.web.servlet.HttpEncodingAutoConfiguration,\
org.springframework.boot.autoconfigure.web.servlet.MultipartAutoConfiguration,\
org.springframework.boot.autoconfigure.web.servlet.WebMvcAutoConfiguration,\
org.springframework.boot.autoconfigure.websocket.reactive.WebSocketReactiveAutoConfiguration,\
org.springframework.boot.autoconfigure.websocket.servlet.WebSocketServletAutoConfiguration,\
org.springframework.boot.autoconfigure.websocket.servlet.WebSocketMessagingAutoConfiguration,\
org.springframework.boot.autoconfigure.webservices.WebServicesAutoConfiguration,\
org.springframework.boot.autoconfigure.webservices.client.WebServiceTemplateAutoConfiguration
```

## **5、按需开启自动配置项**

虽然我们127个场景的所有自动配置启动的时候默认全部加载。xxxxAutoConfiguration 按照条件装配规则（@Conditional），最终会按需配置。

## **6、修改默认配置**

```java
@Bean
@ConditionalOnBean(MultipartResolver.class)  //容器中有这个类型组件
@ConditionalOnMissingBean(name = DispatcherServlet.MULTIPART_RESOLVER_BEAN_NAME) //容器中没有这个名字 multipartResolver 的组件
public MultipartResolver multipartResolver(MultipartResolver resolver) {
    //给@Bean标注的方法传入了对象参数，这个参数的值就会从容器中找。
    //SpringMVC multipartResolver。防止有些用户配置的文件上传解析器不符合规范
    // Detect if the user has created a MultipartResolver but named it incorrectly
    return resolver;
}
给容器中加入了文件上传解析器；
```

**SpringBoot默认会在底层配好所有的组件。但是如果用户自己配置了以用户的优先**

```java
@Bean
@ConditionalOnMissingBean
public CharacterEncodingFilter characterEncodingFilter() {

}
```

## 7、总结

●SpringBoot先加载所有的自动配置类  xxxxxAutoConfiguration
●每个自动配置类按照条件进行生效，默认都会绑定配置文件指定的值。xxxxProperties里面拿。xxxProperties和配置文件进行了绑定
●生效的配置类就会给容器中装配很多组件
●只要容器中有这些组件，相当于这些功能就有了
●定制化配置
○用户直接自己@Bean替换底层的组件
○用户去看这个组件是获取的配置文件什么值就去修改。
==xxxxxAutoConfiguration ---> 组件  ---> xxxxProperties里面拿值  ----> application.properties==



## 8、最佳实践

- 引入场景依赖
  - https://docs.spring.io/spring-boot/docs/current/reference/html/using-spring-boot.html#using-boot-starter
  - ![image-20220707154428042](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220707154428042.png)
- 查看自动配置了哪些（选做）
  - 自己分析，引入场景对应的自动配置一般都生效了
  - 配置文件中debug=true开启自动配置报告。Negative（不生效）\Positive（生效）
  - ![image-20220707154502430](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220707154502430.png)
  - ![image-20220707154558536](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220707154558536.png)
  - ![image-20220707154706210](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220707154706210.png)
- 是否需要修改
  - 参照文档修改配置项
  - https://docs.spring.io/spring-boot/docs/current/reference/html/appendix-application-properties.html#common-application-properties
  - 自己分析。xxxxProperties绑定了配置文件的哪些。
  - 自定义加入或者替换组件
  - @Bean、@Component。。。
  - 自定义器  XXXXXCustomizer；

## 9、更换抬头

将图片文件放在主程序的resources目录下

![image-20220707155743013](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220707155743013.png)

方式一：将图片命名为==banner.xxx==

![image-20220707160006557](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220707160006557.png)

方式二：在application.properties中填写相应配置

![image-20220707155937411](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220707155937411.png)





![image-20220707155714122](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220707155714122.png)



# 三、开发小技巧

## 一、Lombok

### 添加依赖

```xml
<!--    引入lombok插件-->
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.24</version>
    <scope>provided</scope>
</dependency>
```

通过注解简化JavaBean的开发，除了属性其他都不需要写，在编译的时候会自动生成

### 安装插件

![image-20220707171319025](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220707171319025.png)

### ==JavaBean类：==

- @ToString          						// toString()方法
- @Data                                   // get、set方法
- @AllArgsConstructor            // 有参构造器
- @NoArgsConstructor            // 无参构造器
- @EqualsAndHashCode        // 重写HashCode和equals方法

- ```java
  @ToString    // toString()方法
  @Data       // get、set方法
  @AllArgsConstructor  // 有参构造器
  @NoArgsConstructor   // 无参构造器
  @EqualsAndHashCode   // 重写HashCode和equals方法
  @Component
  @ConfigurationProperties(prefix = "mycar")
  public class Car {
  
      private String brand;
      private Integer price;
  
  }
  ```

### ==日志开发：==

在controller类中，使用日志注解，会形成一个log对象，直接调用相应方法即可

```java
@Slf4j
@RestController
public class HelloController {
    @RequestMapping("/hello")
    public String handle01(){
      
        log.info("请求进入、hello内部了"); // ！！！！！！！！！
        return "Hello SpringBoot 2 !";
    }
}
```

![image-20220707171102047](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220707171102047.png)

## 二、dev-tools

### 添加依赖

```xml
<dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-devtools</artifactId>
        <optional>true</optional>
</dependency>
```

修改后，重新编译：Ctrl + F9快捷键

Java文件修改，会重新启动【和手动关闭重启服务器一样】

静态页面修改，会快些

```真正的热部署插件:JRebel```,但是收费；



## 三、Spring Initailizr【创建项目必备】

项目初始化向导，创建时选择这个向导，选择使用的功能及版本，会自动为你添加项目依赖，及全部框架；

1、新建工程：

- ![image-20220707174040545](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220707174040545.png)

2、选择创建项目类型and需要的插件等

- ![image-20220707174300182](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220707174300182.png)

3、创建完成，文件结构都写好了

- ![image-20220707174510944](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220707174510944.png)

- 依赖也自动添加了
- ![image-20220707174529234](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220707174529234.png)



# 四、SpringBoot核心功能

## 1、配置文件

### 1.1、properties

跟以前一样，一个用法

### 1.2、yaml

#### 简介

YAML 是 "YAML Ain't Markup Language"（YAML 不是一种标记语言）的递归缩写。在开发的这种语言时，YAML 的意思其实是："Yet Another Markup Language"（仍是一种标记语言）。 

非常适合用来做以数据为中心的配置文件

#### 基本语法

- key: value；kv之间有空格
- 大小写敏感
- 使用缩进表示层级关系
- 缩进==不允许==使用tab，只允许空格【idea将tab换成4个空格了，所以可以使用】
- 缩进的空格数不重要，只要相同层级的元素左对齐即可
- '#'表示注释
- 字符串无需加引号，如果要加，''与""表示字符串内容 会被 转义/不转义

#### 数据类型

**字面量**：单个的、不可再分的值。date、boolean、string、number、null

```properties
userName: "小明\n小李"
#  userName: '小明\n小李'
# 这里单引号双引号都可以作为字符串，唯一区别就是单引号\n之类的转义字符，就直接输出了，如果用双引号就会换行
boss: true
birth: 2022/03/22
age: 28
```



**对象**：键值对的集合。map、hash、set、object 

```properties
pet:
    name: 狗蛋儿
    weight: 99



animal: [龙,凤凰]

score: {english:88,math:99}

salarys:
  - 998
  - 9999
```



**数组**：一组按次序排列的值。array、list、queue

```properties
#  interests: [篮球,足球]
interests:
  - 篮球
  - 足球
salarys:
  - 998
  - 9999
```

bean类：

```java
@ConfigurationProperties(prefix = "person")
@Component
@Data
public class Person {
    private String userName;
    private Boolean boss;
    private Date birth;
    private Integer age;
    private Pet pet;
    private String[] interests;
    private List<String> animal;
    private Map<String, Object> score;
    private Set<Double> salarys;
    private Map<String, List<Pet>> allPets;
}
```

```java
@Data
public class Pet {
    private String name;
    private Double weight;
}
```

```properties
person:
  userName: "小明\n小李"
#  userName: '小明\n小李'
  # 这里单引号双引号都可以作为字符串，唯一区别就是单引号\n之类的转义字符，就直接输出了，如果用双引号就会换行
  boss: true
  birth: 2022/03/22
  age: 28
  
#   Pet pet;
  pet:
    name: 狗蛋儿
    weight: 99
#   String[] interests;
    #  interests: [篮球,足球]
    interests:
      - 篮球
      - 足球
#   List<String> animal;
  animal: [龙,凤凰]
#   Map<String, Object> score;
  score: {english:88,math:99}
#   Set<Double> salarys;
  salarys:
    - 998
    - 9999
#   Map<String, List<Pet>> allPets;
  allPets:
    sick:
      - {name: 胖胖,weight: 88}
      - name: 丫丫
        weight: 99
      - name: 企鹅
        weight: 8
    health:
      - {name: 狗蛋儿,weight: 888}
      - name: 元宝儿
        weight: 777
```

#### 语法提醒

在yaml中填写配置信息，默认没有提示：

![image-20220717111452812](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220717111452812.png)



影响效率，添加注释依赖后就有提示了

```properties
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-configuration-processor</artifactId>
    <optional>true</optional>
</dependency>
```

![image-20220717112224985](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220717112224985.png)

## 2、Web开发

### 1、简单功能分析

#### 2.1、静态资源访问

- 1、静态资源目录
- 只要静态资源放在类路径下： 
  - ```static```
  - ```public ```
  - ```resources```
  - ```META-INF/resources```
  - 默认创建的是static，这几个名字都可以，同时存在也行
- 访问 ： 当前项目根路径/ + 静态资源名 
- ![image-20220717155421740](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220717155421740.png)
- ![image-20220717155437462](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220717155437462.png)

原理： 静态映射/**。
请求进来，先去找Controller看能不能处理。不能处理的所有请求又都交给静态资源处理器。静态资源也找不到则响应404页面

也就是说，**如果有Controller和静态资源同名，会先访问controller**



改变默认的静态资源路径

```properties
# 对静态资源统一加一个前缀，这样后期设置拦截器之类的好操作，但是目前有个bug就是加了前缀不显示index首页了
spring:
  mvc:
    static-path-pattern: /res/**
    
    
# 修改后，就不去resources下寻找了
  resources:
    static-locations: [classpath:/haha/]
```



#### 2.2、webjar

自动映射 /[webjars](http://localhost:8080/webjars/jquery/3.5.1/jquery.js)/**

这个网址https://www.webjars.org/，将一些jar包，转换成依赖，拿过去直接添加就行了



![image-20220717160031318](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220717160031318.png)

添加依赖后，SpringBoot自动就映射了，当做静态资源处理，也可以直接在网页访问到

先查看静态页面结构：**可以看到这里用的静态页面是==META-INF/resources==**

所以访问里面的静态结构，直接从webjars开始就可以了

![image-20220717161631411](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220717161631411.png)

按文件结构访问

![image-20220717161550297](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220717161550297.png)





### 2、==普通参数与基本注解==

#### @PathVariable：

将 **URL** 中占位符参数绑定到控制器处理方法的入参中

- URL 中的 {**xxx**} 占位符可以通过@PathVariable(“**xxx**“) 绑定到操作方法的入参中。

- 把URL地址中的参数，取出来

- ```java
  //@PathVariable可以用来映射URL中的占位符到目标方法的参数中
  		@RequestMapping("/testPathVariable/{id}")
      public String testPathVariable(@PathVariable("id") Integer id)
      {
          System.out.println("testPathVariable:"+id);
          return SUCCESS;
      }
  ```

  

#### @RequestHeader：

获取请求头中的数据，通过指定参数 value 的值来获取请求头中指定的参数值。其他参数用法和 @RequestParam 完全一样

- 请求头中参数都是```key:value```形式存储的，可以全部取出来，也可以按照key提取

- ![image-20220717190422040](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220717190422040.png)

- ```java
  @Controller
  public class handleHeader {
  
  	@GetMapping("/getHeader")
  	public String getRequestHeader(@RequestHeader("User-Agent") String agent) {
  		  System.out.println(agent);
  		  return "success";
  	}
  }
  ```

#### @RequestParam：

将请求参数绑定到你控制器的方法参数上（是springmvc中接收普通参数的注解）

- 就是获取传过来的参数
- 语法：```@RequestParam(value=”参数名”,required=”true/false”,defaultValue=””)```
  - value：参数名
  - required：是否包含该参数，默认为true，表示该请求路径中必须包含该参数，如果不包含就报错。
  - defaultValue：默认参数值，如果设置了该值，required=true将失效，自动为false,如果没有传该参数，就使用默认值

- ```java
     @PostMapping("/hello")
      public void aliReceive(@RequestParam("message") String message) {
          System.out.println(message);
        	return "success";
      }
  ```

#### @RequestBody：

主要用来接收前端传递给后端的```json字符串```中的数据的(请求体中的数据的)；而最常用的使用请求体传参的无疑是```POST请求```了，所以使用@RequestBody接收数据时，一般都用POST方式进行提交。

- 

- ```java
  //直接把json 读成字符串
  @PostMapping("/save")
  public Map postMethod(@RequestBody String content){
      System.out.println(content);
      return "success";
  }
  // 假设有个类eamil 有user、password两个属性
  // 传来的json是{user:tom,password:123456}
  // requestBody会自动匹配key值，赋值到email对象中
  @PostMapping("/save")
  public Map postMethod(@RequestBody email email){
      System.out.println(email.toString());
      return "success";
  }
  ```



#### @ModelAttribute:

- <font color="blue">**应用在方法上**</font>

  - 使用`@ModelAttribute`注解无返回值的方法

    ```java
    @Controller
    @RequestMapping(value = "/modelattribute")
    public class ModelAttributeController {
    
        @ModelAttribute
        public void myModel(@RequestParam(required = false) String abc, Model model) {
            model.addAttribute("attributeName", abc);
        }
    
        @RequestMapping(value = "/method")
        public String method() {
            return "method";
        }
    }
    ```

    这个例子，在请求`/modelattribute/method?abc=aaa`后，会先执行`myModel`方法，然后接着执行`method`方法，参数`abc`的值被放到`Model`中后，接着被带到`method`方法中。

    当返回视图`/modelattribute/method`时，`Model`会被带到页面上，当然你在使用`@RequestParam`的时候可以使用`required`来指定参数是否是必须的。

    如果把`myModel`和`method`合二为一，代码如下，这也是我们最常用的方法：

    

    ```java
    @RequestMapping(value = "/method")
    public String method(@RequestParam(required = false) String abc, Model model) {
        model.addAttribute("attributeName", abc);
        return "method";
    }
    ```

    使用`@ModelAttribute`注解带有返回值的方法

    

    ```java
    @ModelAttribute
    public String myModel(@RequestParam(required = false) String abc) {
        return abc;
    }
    
    @ModelAttribute
    public Student myModel(@RequestParam(required = false) String abc) {
        Student student = new Student(abc);
        return student;
    }
    
    @ModelAttribute
    public int myModel(@RequestParam(required = false) int number) {
        return number;
    }
    ```

    对于这种情况，返回值对象会被默认放到隐含的`Model`中，在`Model`中的`key`为**`返回值首字母小写`**，`value`为返回的值。

    上面3种情况等同于：

    ```tsx
    model.addAttribute("string", abc);
    model.addAttribute("int", number);
    model.addAttribute("student", student);
    ```

    > 在jsp页面使用`${int}`表达式时会报错：`javax.el.ELException: Failed to parse the expression [${int}]`。
    > 解决办法：
    > 在tomcat的配置文件`conf/catalina.properties`添加配置`org.apache.el.parser.SKIP_IDENTIFIER_CHECK=true`

    如果只能这样，未免太局限了，我们很难接受`key`为`string`、`int`、`float`等等这样的。

    想自定义其实很简单，只需要给`@ModelAttribute`添加`value`属性即可，如下：

    ```java
    @ModelAttribute(value = "num")
    public int myModel(@RequestParam(required = false) int number) {
        return number;
    }
    ```

    这样就相当于`model.addAttribute("num", number);`

- <font color="blue">**应用在方法的参数上**</font>

  ```java
  @Controller
  @RequestMapping(value = "/modelattribute")
  public class ModelAttributeParamController {
  
      @ModelAttribute(value = "attributeName")
      public String myModel(@RequestParam(required = false) String abc) {
          return abc;
      }
  
      @ModelAttribute
      public void myModel3(Model model) {
          model.addAttribute("name", "zong");
          model.addAttribute("age", 20);
      }
  
      @RequestMapping(value = "/param")
      public String param(@ModelAttribute("attributeName") String str,
                         @ModelAttribute("name") String str2,
                         @ModelAttribute("age") int str3) {
          return "param";
      }
  }
  ```

  从代码中可以看出，使用`@ModelAttribute`注解的参数，意思是从前面的`Model`中提取对应名称的属性。

  这里提及一下`@SessionAttributes`的使用：

  > - 如果在类上面使用了`@SessionAttributes("attributeName")`注解，而本类中恰巧存在`attributeName`，则会将`attributeName`放入到`session`作用域。
  > - 如果在类上面使用了`@SessionAttributes("attributeName")`注解，SpringMVC会在执行方法之前，自动从`session`中读取`key`为`attributeName`的值，并注入到`Model`中。所以我们在方法的参数中使用`ModelAttribute("attributeName")`就会正常的从`Model`读取这个值，也就相当于获取了`session`中的值。
  > - 使用了`@SessionAttributes`之后，Spring无法知道什么时候要清掉`@SessionAttributes`存进去的数据，如果要明确告知，也就是在方法中传入`SessionStatus`对象参数，并调用`status.setComplete`就可以了。

- <font color="blue">**应用在方法上，并且方法也使用了`@RequestMapping`**</font>

  ```java
  @Controller
  @RequestMapping(value = "/modelattribute")
  public class ModelAttributeController {
  
      @RequestMapping(value = "/test")
      @ModelAttribute("name")
      public String test(@RequestParam(required = false) String name) {
          return name;
      }
  }
  ```

  这种情况下，返回值String（或者其他对象）就不再是视图了，而是放入到`Model`中的值，此时对应的页面就是`@RequestMapping`的值`test`。
  如果类上有`@RequestMapping`，则视图路径还要加上类的`@RequestMapping`的值，本例中视图路径为`modelattribute/test.jsp`。



#### @MatrixVariable

- `value` 和属性`pathVar`的别名;
- `pathVar` 用于指定name-value参数所在的路径片段名称
- `name` 用于指定name-value参数的参数名
- `required` 是否为必填值，默认为false
- `defaultValue` 设置默认值

##### 1. 背景

**@MatrixVariable注解与矩阵变量有关**

一般我们会定义这样的url：`/cars/{path}/?a=xxx&b=XXX`，这是使用查询字符串的方式提交参数，在后台方法我们使用@RequestParam注解来获取参数。另外，我们考虑这样的url：`/cars/sell;a=xxx;b=xxx,XXX`，这就是使用矩阵变量的方式提交参数，那么我们就使用@MatrixVariable注解

一般，矩阵变量会应用到这样的场景。

<font color="blue">在页面开发中，如果Cookie被禁用了，该如何获得Session中的数据？</font>

- 如果使用Cookie，通过获取Cookie中的JSessionID，找到Session对象，从而获取该Session中的数据。

- 而Cookie被禁用了，就无法获取JSessionID，也就不能用这种方法获取Session的数据。

- 这时，我们可以使用`url重写`的方式解决这一问题，比如这样的url：`/abc;jsessionid=xxxxx`，也就是将Cookie的值使用矩阵变量的方式传递



##### 2. 矩阵变量的格式

一般以矩阵变量的方式传递参数，则url有多种格式

- `/cars/sell;low=34;brand=bmw;brand=audi;brand=benz` 这是在;后面以key=value形式加上参数，之间用;分开
- `/cars/sell;low=34;brand=bmw,audi,benz` 这是将相同key的value值以,分开
- `/boss/1;age=20/2;age=18` 这是以/boss/{bossId}/{empId}的形式，并且在bossId和empId中分别带上了参数

矩阵变量是绑定在路径变量中的。比如，对于`/cars/sell;low=34;brand=bmw,audi,benz`这个url，在Controller方法上的`@RequestMapping`中的url为`/cars/{path}`



##### 3. 开启SpringBoot对矩阵变量的支持

在SpringBoot中，需要手动开启对矩阵变量的支持。在url路径的处理上，SpringMVC使用`UrlPathHelper`进行解析，这个类中有个变量`removeSemicolonContent`默认为true，表示默认移除url中的分号内容。所以为了支持矩阵变量，需要自定义SpringMVC，有两种解决方法

方法一：

我们在配置类中放入一个`WebMvcConfigurer`，标注@bean注解，将这个类放入容器中，在这个类中覆盖configurePathMatch方法

```java
@Configuration(proxyBeanMethods = false)
public class MyConfig{

    @Bean
    public WebMvcConfigurer webMvcConfigurer() {
        return new WebMvcConfigurer() {
            @Override
            public void configurePathMatch(PathMatchConfigurer configurer) {
                UrlPathHelper urlPathHelper = new UrlPathHelper();
                urlPathHelper.setRemoveSemicolonContent(false);
                configurer.setUrlPathHelper(urlPathHelper);
            }
        };
    }
}
```

方法二：

直接将配置类实现`WebMvcConfigurer`，且在配置类中实现configurePathMatch方法

```java
@Configuration(proxyBeanMethods = false)
public class MyConfig implements WebMvcConfigurer {

    @Override
    public void configurePathMatch(PathMatchConfigurer configurer) {
        UrlPathHelper urlPathHelper = new UrlPathHelper();
        urlPathHelper.setRemoveSemicolonContent(false);
        configurer.setUrlPathHelper(urlPathHelper);
    }
}
```

这样就开启了SpringBoot对于矩阵变量的支持



##### 4. @MatrixVariable的使用



那么，对于相应的Controller方法，我们可以这样写

```java
/**
 * /cars/sell;low=34;brand=bmw,audi,benz
 * 或者/cars/sell;low=34;brand=bmw;brand=audi;brand=benz
 */
@GetMapping("/cars/{path}")
public Map<String, Object> test3(@MatrixVariable("low") Integer low,
                                 @MatrixVariable("brand") List<String> brand,
                                 @PathVariable("path") String path) {
    Map<String, Object> map = new HashMap<>();
    map.put("low", low);
    map.put("brand", brand);
    map.put("path", path);
    return map;
}
```

当我们发起这样的请求时`/cars/sell;low=34;brand=bmw,audi,benz`或者`/cars/sell;low=34;brand=bmw;brand=audi;brand=benz`，页面显示的结果为`{"path":"sell","low":34,"brand":["bmw","audi","benz"]}`

另外，对于这样的url：`/boss/1;age=20/2;age=18`，在url中有两个名称相同的矩阵变量，相应的处理方法为

```java
/**
 * /boss/1;age=20/2;age=18
 */
@GetMapping("/boss/{bossId}/{empId}")
public Map<String, Object> test4(@MatrixVariable(value = "age", pathVar = "bossId") Integer bossAge,
                                 @MatrixVariable(value = "age", pathVar = "empId") Integer empAge) {
    Map<String, Object> map = new HashMap<>();
    map.put("bossAge", bossAge);
    map.put("empAge", empAge);
    return map;
}
```

在`@MatrixVariable`注解中有`pathVar`属性，这个属性来区分是哪个路径下的变量

这样当我们发起这样的请求时 `/boss/1;age=20/2;age=18`，显示的结果为`{"bossAge":20,"empAge":18}`

##### 5. 总结

1. SpringBoot默认不支持矩阵变量，需要自定义SpringMVC的`WebMvcConfigurer`中的`UrlPathHelper`来开启
2. 矩阵变量必须要有url路径变量才能被解析



#### @CookieValue

##### 1、@CookieValue的作用

　　用来获取Cookie中的值

##### 2、@CookieValue参数

　　1、value：参数名称

　　2、required：是否必须

　　3、defaultValue：默认值

##### 3、@CookieValue使用案例

```java
@Controller
public class HelloWorldController {
	@RequestMapping("/cookieValueTest")
	public void cookieValueTest(@CookieValue(value="JSESSIONID")String sessionId) {
		System.out.println("通过@CookieValue获得JSESSIONID:"+sessionId);
	}
}
```

#### 重定向传参

**==RedirectAttributes==** 是Spring mvc 3.1版本之后出来的一个功能，专门用于重定向之后还能带参数跳转的的工具类
他有两种带参的方式：

```java
@GetMapping("/city/delete/{id}")
public String deleteCity(@PathVariable("id") Integer id,
                         @RequestParam(value = "pn",defaultValue = "1") Integer pn,
                         RedirectAttributes ra){
    // 删除id数据
    cityServiceImpl.removeById(id);
    ra.addAttribute("pn",pn);
    // 重定向到当前页码
    return "redirect:/dynamic_table";
}
```



**第一种：**

redirectAttributes.addAttributie("prama",value); 这种方法相当于在重定向链接地址追加传递的参数，例如:

```java
redirectAttributes.addAttributie("prama1",value1);

redirectAttributes.addAttributie("prama2",value2);

return:"redirect：/path/list" 
```

以上重定向的方法等同于 ```return:"redirect：/path/list？prama1=value1**&**prama2=value2 " ```，注意这种方法直接将传递的参数暴露在链接地址上，非常的不安全，慎用。

**第二种：**

```redirectAttributes.addFlashAttributie("prama",value); ```这种方法是隐藏了参数，链接地址上不直接暴露，但是能且只能在重定向的 **“*****\\*页面\\**”** 获取prama参数值。其原理就是放到session中，session在跳到页面后马上移除对象。如果是重定向一个controller中是获取不到该prama属性值的。除非在controller中用(@RequestPrama(value = "prama")String prama)注解，采用传参的方式。页面获值例如：

```java
redirectAttributes.addFlashAttributie("prama1",value1);

redirectAttributes.addFlashAttributie("prama2",value2);

return:"redirect：/path/list.jsp" 
```

在以上参数均可在list.jsp页面使用EL表达式获取到参数值${prama*}

controller获得redirectAttributes重定向的值例如：

```java
redirectAttributes.addFlashAttributie("prama1",value1);

redirectAttributes.addFlashAttributie("prama2",value2);

return:"redirect：/path/list/"

@RequestMapping("list")
public List<Student> list(@RequestPrama(value = "prama1")String  prama1,
   @RequestPrama(value = "prama2")String  prama2,...
){
    //TODO
    //your code

}
```

通过在controller中的list方法体中可以获取到参数值。



### 3、==模板引擎-Thymeleaf==

#### 1、thymeleaf简介

Thymeleaf is a modern server-side Java template engine for both web and standalone environments, capable of processing HTML, XML, JavaScript, CSS and even plain text.
现代化、服务端Java模板引擎

#### 2、基本语法

##### 1、表达式

##### ![image-20220718113139667](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220718113139667.png)2、字面量

- 文本值: 'one text' , 'Another one!' ,…

- 数字: 0 , 34 , 3.0 , 12.3 ,…

- 布尔值: true , false
- 空值: null
- 变量： one，two，.... 变量不能有空格

##### 3、文本操作

- 字符串拼接: +
- 变量替换: |The name is ${name}| 

##### 4、数学运算

- 运算符: + , - , * , / , %

##### 5、布尔运算

- 运算符:  and , or
- 一元运算: ! , not 

##### 6、比较运算

- 比较: > , < , >= , <= ( gt , lt , ge , le )等式: == , != ( eq , ne ) 

##### 7、条件运算

- If-then: (if) ? (then)
- If-then-else: (if) ? (then) : (else)
- Default: (value) ?: (defaultvalue) 

#### 3、设置属性值-th:attr

- 设置单个值

- ```html
  <form action="subscribe.html" th:attr="action=@{/subscribe}">
    <fieldset>
      <input type="text" name="email" />
      <input type="submit" value="Subscribe!" th:attr="value=#{subscribe.submit}"/>
    </fieldset>
  </form>
  ```

- 设置多个值

- ```html
  <img src="../../images/gtvglogo.png"  th:attr="src=@{/images/gtvglogo.png},title=#{logo},alt=#{logo}" />
  ```

- 以上两个的代替写法 th:xxxx

- ```html
  <input type="submit" value="Subscribe!" th:value="#{subscribe.submit}"/>
  <form action="subscribe.html" th:action="@{/subscribe}">
  ```

#### **4、迭代**

```html
<tr th:each="prod : ${prods}">
        <td th:text="${prod.name}">Onions</td>
        <td th:text="${prod.price}">2.41</td>
        <td th:text="${prod.inStock}? #{true} : #{false}">yes</td>
</tr>
```

```html
<tr th:each="prod,iterStat : ${prods}" th:class="${iterStat.odd}? 'odd'">
  <td th:text="${prod.name}">Onions</td>
  <td th:text="${prod.price}">2.41</td>
  <td th:text="${prod.inStock}? #{true} : #{false}">yes</td>
</tr>
```

#### 5、条件运算

```html
<a href="comments.html"
th:href="@{/product/comments(prodId=${prod.id})}"
th:if="${not #lists.isEmpty(prod.comments)}">view</a>
```

```html
<div th:switch="${user.role}">
  <p th:case="'admin'">User is an administrator</p>
  <p th:case="#{roles.manager}">User is a manager</p>
  <p th:case="*">User is some other thing</p>
</div>
```

#### 6、属性优先级

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/1605498132699-4fae6085-a207-456c-89fa-e571ff1663da.png)



### 4、==thymeleaf使用==

**1、引入Starter**

```xml
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-thymeleaf</artifactId>
        </dependency>
```

**2、自动配置好了thymeleaf,不用管了**

 ```java
 @Configuration(proxyBeanMethods = false)
 @EnableConfigurationProperties(ThymeleafProperties.class)
 @ConditionalOnClass({ TemplateMode.class, SpringTemplateEngine.class })
 @AutoConfigureAfter({ WebMvcAutoConfiguration.class, WebFluxAutoConfiguration.class })
 public class ThymeleafAutoConfiguration { }
 ```

自动配好的策略
1、所有thymeleaf的配置值都在 ThymeleafProperties
2、配置好了 SpringTemplateEngine 
3、配好了 ThymeleafViewResolver 
4、我们只需要直接开发页面

默认路径：【所以在跳转的时候，直接写文件名就行了，后缀和路径都不用写

假设为haha.html 直接return "haha"即可】

- 文件夹：==/templates/==
- 文件后缀：==".html"==

```java
	public static final String DEFAULT_PREFIX = "classpath:/templates/";

	public static final String DEFAULT_SUFFIX = ".html";  //xxx.html
```

**3、页面开发**

不经过后端渲染，数据显示为==哎呦我去==，后端渲染后为==我是新来的==

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <h1 th:text="${msg}">哎呦我去</h1>
    <h2>
        <a href="www.bushi.com" th:href="${link}" >打开百度</a>
        <a href="www.bushi.com" th:href="@{link}">打开百度222</a>
    </h2>
</body>
</html>
```

```java

@Controller
public class thymeleafTest {
    @RequestMapping("/thy")
    public String test(Model model){
        model.addAttribute("msg","我是新来的");
        model.addAttribute("link","www.baidu.com");
        // thymeleaf默认路径和结尾给了，所以就直接写文件名就能跳转了
        // 默认路径是templates文件夹下.html文件
        return "hello";
    }
}
```

### 5、==构建后台管理系统==

#### 1、项目创建

thymeleaf、web-starter、devtools、lombok

#### 2、静态资源处理

自动配置好，我们只需要把所有静态资源放到 static 文件夹下

![image-20220719020104233](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220719020104233.png)

#### 3、路径构建

th:action="@{/login}"

```java
@Controller
public class IndexController {

    /**
     * 跳转登录页，/或者/login都是跳转登录页
     * @return
     */
    @GetMapping(value = {"/","/login"})
    public String loginPage(){
        return "login";
    }

    @PostMapping("/login")
    public String toMain(User user, HttpSession session, Model model){

        if (!StringUtils.isEmpty(user.getUserName())&& !StringUtils.isEmpty(user.getPassword())){
            // 登录成功的user保存到session中，后边展示相关信息使用
            session.setAttribute("loginUser",user);
            // 重定向，放止表单重复提交
            return "redirect:/main.html";
        }else{
            // 提示账号密码错误
            model.addAttribute("msg","账号密码错误，请重新输入");
            // 回到登录页面
            return "login";
        }
    }
    // 多写一个是为了放止表单重复提交，在toMain中直接转main.html里面后，url地址来还是在localhost:8080/login下
    // 如果重复刷新，那就会不断提交post请求，经过这养一个媒介以后，刷新只是刷新main.html页面
    // 这里不能直接写main，因为请求只能访问static文件，必须经过处理才能访问到templates下文件
    @GetMapping("/main.html")
    public String mainPage(HttpSession session,Model model){
        //如果不判断，就只要拿到这个连接http://localhost:8080/main.html，任何地方敲进去都能进去
        if(session.getAttribute("loginUser") == null){
            // 说明不是正常途径进来的，要不然肯定又登录用户的信息
            model.addAttribute("msg","请先登录账号");
            return "login";
        }else{

            return "main";
        }
    }
}
```

- 没有在登录界面直接跳转main，而是多写一个方法做中介是为了放止表单重复提交，在toMain中直接转main.html里面后，url地址来还是在localhost:8080/login下
- 如果重复刷新，那就会不断提交post请求，经过这养一个媒介以后，刷新只是刷新main.html页面
- 这里不能直接写main，因为请求只能访问static文件，必须经过处理才能访问到templates下文件

#### 4、模板抽取

将前端模板**公共区域全部提取**出来，放到common.html中，统一管理，便于修改配置。然后将配置回插到原页面，主要有三个方法：

==主要逻辑：==

- 1、将公共部分的一个标签拿出来，存到common.html中，不论是h、p、a、head、div等哪个标签都可以
- 2、第一种方式：在标签中添加```th:fragment="别名"```
  - 调用时：在目标位置标签内用```th:insert="~{common::别名}"```
- 3、第二种方式：在确保标签有个id属性，没有就添加一个
  - 调用时：在目标位置标签内用```th:replace="common::#id"```,他会去common页面找这个id，然后加进去



在`Thymeleaf`中，可以使用`th:insert`，`th:replace`，`th:include`三种方式插入模板片段，下面通过例子对三种方式进行比较：

准备片段页面`footer.html`：其内容就是span标签及其内容

```html
<span th:fragment="copy">Footer Text</span>

<span id="第二种方式">Footer Text</span>

```

在页面中使用三种方式插入模板片段：

```html
<div th:insert="~{footer::copy}"></div>
<div th:replace="~{footer::copy}"></div>
<div th:include="~{footer::copy}"></div>

<div th:replace="footer :: #第二种方式"></div>  insert/replace/include通用
```

结果：

```html
<div><span>Footer Text</span></div>  insert：直接插入，包括标签也插进去【插入】
<span>Footer Text</span>							replace：替换，将目标标签，换成自带标签【带格式粘贴】
<div>Footer Text</div>							 include：只取内容，不携带原标签【粘贴为纯文本】
```

因此：
`th:insert`会将选择到的`span`节点插入到`div`中；
`th:replace`会将原来的`div`节点替换为`span`节点；
`th:include`会将`span`节点的内容（包括子节点）插入到`div`中。

#### 5、页面跳转

下面页面跳转逻辑还是一样，只能读到templates文件，里面的路径就要写上，table/basic_table，但是不用写.html

完整路径是templates/table/basic_table.html

```java
@Controller
public class TablelController {
    @GetMapping("/basic_table")
    public String basic_table(){
        return "table/basic_table";
    }

    @GetMapping("/dynamic_table")
    public String dynamic_table(Model model){

        List<User> users = Arrays.asList(new User("zhagnsan", "1234"),
                                         new User("lisi", "234"),
                                         new User("wanger", "3456"));
        model.addAttribute("users",users);
        return "table/dynamic_table";

    }

    @GetMapping("/responsive_table")
    public String responsive_table(){
        return "table/responsive_table";
    }

    @GetMapping("/editable_table")
    public String editable_table(){
        return "table/editable_table";
    }
}

```

#### 6、数据渲染

```java
    @GetMapping("/dynamic_table")
    public String dynamic_table(Model model){
        //表格内容的遍历
        List<User> users = Arrays.asList(new User("zhangsan", "123456"),
                new User("lisi", "123444"),
                new User("haha", "aaaaa"),
                new User("hehe ", "aaddd"));
        model.addAttribute("users",users);

        return "table/dynamic_table";
    }
```

```html
        <table class="display table table-bordered" id="hidden-table-info">
        <thead>
        <tr>
            <th>#</th>
            <th>用户名</th>
            <th>密码</th>
        </tr>
        </thead>
        <tbody>
          stats表示遍历次序，类似i，从1开始
        <tr class="gradeX" th:each="user,stats:${users}">
            <td th:text="${stats.count}">Trident</td>
            <td th:text="${user.userName}">Internet</td>
            <td >[[${user.password}]]</td>
        </tr>
        </tbody>
        </table>
```

### 6、==拦截器==

#### 1、拦截器流程

- <font color="red">1、编写一个拦截器</font>：实现 HandlerInterceptor 接口，根据拦截位置需要
  - <font color="blue">重写preHandle()方法：</font>在业务处理器处理请求之前被调用。预处理，可以进行编码、安全控制、权限校验等处理；
  - <font color="blue">重写postHandle()方法：</font>在业务处理器处理请求执行完成后，生成视图之前执行。后处理（调用了Service并返回ModelAndView，但未进行页面渲染），有机会修改ModelAndView ；
  - <font color="blue">重写afterCompletion()方法：</font>在DispatcherServlet完全处理完请求后被调用，可用于清理资源等。返回处理（已经渲染了页面）；
  - ![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/1104426-20180407232200147-2079803025.png)
- <font color="red">2、拦截器注册到容器中</font>：实现 WebMvcConfigurer 接口，重写 addInterceptors 方法【添加add拦截器】
- <font color="red">3、指定拦截规则</font>：【使用哪个拦截器】【拦截哪些路径】【放行哪些路径】
- <font color="red">注意</font>：如果是全部拦截，那么静态资源也会被拦截，这里要单独处理
- ![image-20220719124537265](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220719124537265.png)
- 配置文件设置前缀：```spring.mvc.static-path-pattern=/static/**```



#### 2、拦截器原理

- 1、根据当前请求，找到HandlerExecutionChain【可以处理请求的handler以及handler的所有 拦截器】
- 2、先来顺序执行 所有拦截器的 preHandle方法
  - 1、如果当前拦截器prehandler返回为true。则执行下一个拦截器的preHandle
  - 2、如果当前拦截器返回为false。直接    倒序执行所有已经执行了的拦截器的  afterCompletion；
- 3、如果任何一个拦截器返回false。直接跳出不执行目标方法
- 4、所有拦截器都返回True。执行目标方法
- 5、倒序执行所有拦截器的postHandle方法。
- 6、前面的步骤有任何异常都会直接倒序触发 afterCompletion
- 7、页面成功渲染完成以后，也会倒序触发 afterCompletion
- ![image.png](https://pledge99.oss-cn-beijing.aliyuncs.com/img/1605765121071-64cfc649-4892-49a3-ac08-88b52fb4286f.png)

#### 3、创建拦截器

![image-20220719123521415](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220719123521415.png)

实现HandlerInterceptor接口

```java
@Slf4j
public class LoginInterceptor implements HandlerInterceptor {
    // 目标方法执行之前
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        String requestURI = request.getRequestURI();
        log.info("拦截的请求路径是{}",requestURI);

        HttpSession session = request.getSession();
        // 因为在登录处，只要登陆了，session中就有loginUser对象，没有就是没登录
        Object loginUser = session.getAttribute("loginUser");

        // 登录了，直接true放行即可
        if(loginUser != null) return true;
        // 未登录，要重定向到首页或者登录页，可以设置一个msg，让有个提示。恰好密码错误哪里可以获取一个msg，这里直接给赋一个
        request.setAttribute("msg","请登录后操作！");
        // 重定向到根目录，就是首页了【but，重定向拿不到session，这里用请求转发】
        request.getRequestDispatcher("/").forward(request,response); // 请求抓发
//        response.sendRedirect("/");// 请求重定向
        return false;
    }

    // 目标方法执行后
    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
        HandlerInterceptor.super.postHandle(request, response, handler, modelAndView);
    }

    // 目标方法执行之后，视图渲染完成以后
    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
        HandlerInterceptor.super.afterCompletion(request, response, handler, ex);
    }
}
```

#### 4、添加拦截器到容器中

![image-20220719124425083](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220719124425083.png)

```java
@Configuration
public class AdminWebConfig implements WebMvcConfigurer {
    // 添加拦截器
    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        // 添加一个拦截器，到容器
        // 添加拦截的路径
        // 选择不拦截的路径
        registry.addInterceptor(new LoginInterceptor())  // new一个拦截器对象，添加进去
                .addPathPatterns("/**") // 所有都拦截【包含静态资源】
                // 放行：登录页、静态资源【因为资源路径是static/下，所以不能直接给static】
                .excludePathPatterns("/","/login","/css/**","/fonts/**","/images/**","/js/**");
                // 还有一种方式，就是给静态资源在application.yaml中加统一前缀，
                // 但是所有html页面就要对应增加，前缀，不能直接写css/xxx了
                // 这里因为用的模板，改起来复杂，自己写的时候可以提前考虑到这层，写页面的时候就写进去如：/hhh/css/xxx
    }
}
```

#### 5、拦截器Interceptor和过滤器Filter区别

- Filter需要在web.xml中配置，依赖于Servlet
- Interceptor需要在SpringMVC中配置，依赖于框架
- Filter的执行顺序在Interceptor之前，具体的流程见下图

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/2494062-20211025163030484-1296381714.png)

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/2494062-20211025163333011-1880329915.png)

 

**两者的本质区别：**拦截器（Interceptor）是基于Java的反射机制，而过滤器（Filter）是基于函数回调。

从灵活性上说拦截器功能更强大些，Filter能做的事情，都能做，而且可以在请求前，请求后执行，比较灵活。

Filter主要是针对URL地址做一个编码的事情、过滤掉没用的参数、安全校验（比较泛的，比如登录不登录之类），太细的话，还是建议用interceptor。不过还是根据不同情况选择合适的。





### 7、==文件上传==

#### 1、前端页面编辑

- 表头

  - post请求

  - 编码：```enctype="multipart/form-data"```

- 单文件上传

  - ```<input type="file" name="headerImg" id="exampleInputFile">```

- 多文件上传

  - ```<input type="file" name="photos" multiple>```
  - 就是结尾加一个**multiple**

```html
<form role="form" th:action="@{/upload}" method="post" enctype="multipart/form-data">
    <div class="form-group">
        <label for="exampleInputEmail1">邮箱</label>
        <input type="email" name="email" class="form-control" id="exampleInputEmail1" placeholder="Enter email">
    </div>
    <div class="form-group">
        <label for="exampleInputPassword1">名字</label>
        <input type="text" name="username" class="form-control" id="exampleInputPassword1" placeholder="Password">
    </div>
    <div class="form-group">
        <label for="exampleInputFile">头像</label>
        <input type="file" name="headerImg" id="exampleInputFile">
    </div>
    <div class="form-group">
        <label for="exampleInputFile">生活照</label>
        <input type="file" name="photos" multiple>
    </div>
    <div class="checkbox">
        <label>
            <input type="checkbox"> Check me out
        </label>
    </div>
    <button type="submit" class="btn btn-primary">提交</button>
</form>
```

#### 2、后端页面编辑

- 1、修改上传文件大小限制

  - ```properties
    # 单个文件上传大小限制
    spring.servlet.multipart.max-file-size=10MB
    # 一个请求最大上传文件的限制
    spring.servlet.multipart.max-request-size=100MB
    ```

- 2、编写对应的Controller

  - 单个文件下载：

  - ```java
    @Controller
    public class FormController {
    		// 收到form请求，跳转form页面
        @GetMapping("/form_layouts")
        public String toForm_layouts(){
            return "/form/form_layouts";
        }
    		// 处理下载需求
        @PostMapping("/upload")
        public String upload(@RequestParam("email") String email,
                             @RequestParam("username") String username,
                             @RequestPart("headerImg") MultipartFile headerImg,
                             @RequestPart("photos") MultipartFile[] photos) throws IOException {
    
            if(!headerImg.isEmpty()){
                // 上传的问价那不是空的，把他上传到服务器，这里暂时保存到本地
                // 获取文件原来的名字
                String originalFilename = headerImg.getOriginalFilename();
                headerImg.transferTo(new File("路径" + originalFilename));
            }
            // 上传完成，让它回到主页
            return "main";
        }
    }
    ```

  - 多个文件下载，就是用列表接收，然后遍历逐一下载

  - ```java
    @Controller
    public class FormController {
    
        @GetMapping("/form_layouts")
        public String toForm_layouts(){
            return "/form/form_layouts";
        }
    
        @PostMapping("/upload")
        public String upload(@RequestParam("email") String email,
                             @RequestParam("username") String username,
                             @RequestPart("headerImg") MultipartFile headerImg,
                             @RequestPart("photos") MultipartFile[] photos) throws IOException {
    
            // 遍历下载多个文件
            for(MultipartFile photo : photos){
                if(!photo.isEmpty()){
                    // 上传的问价那不是空的，把他上传到服务器，这里暂时保存到本地
                    // 获取文件原来的名字
                    String originalFilename = photo.getOriginalFilename();
                    photo.transferTo(new File("路径" + originalFilename));
                }
            }
            // 上传完成，让它回到主页
            return "main";
        }
    }
    ```
  
  


#### 3、自动配置原理

文件上传自动配置类-MultipartAutoConfiguration-MultipartProperties

自动配置好了 StandardServletMultipartResolver   【文件上传解析器】

原理步骤

- 1、请求进来使用文件上传解析器判断（isMultipart）并封装（resolveMultipart，返回MultipartHttpServletRequest）文件上传请求
- 2、参数解析器来解析请求中的文件内容封装成MultipartFile
- 3、将request中文件信息封装为一个Map；MultiValueMap<String, MultipartFile>FileCopyUtils。实现文件流的拷贝



### 8、==异常错误处理==

#### 1、默认规则

默认情况下，Spring Boot提供/error处理所有错误的映射

- 对于机器客户端，它将生成JSON响应，其中包含错误，HTTP状态和异常消息的详细信息。
  - ![image.png](https://pledge99.oss-cn-beijing.aliyuncs.com/img/1606024421363-77083c34-0b0e-4698-bb72-42da351d3944.png)

- 对于浏览器客户端，响应一个“ whitelabel”错误视图，以HTML格式呈现相同的数据
  - ![image.png](https://pledge99.oss-cn-beijing.aliyuncs.com/img/1606024616835-bc491bf0-c3b1-4ac3-b886-d4ff3c9874ce.png)

**浏览器端这个页面太丑了，跟原网页帅气风格不符，立即推：改！**

![image-20220720225419825](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220720225419825.png)

#### 2、自定义漂亮的错误页面

##### **1、静态资源中，创建error文件夹及对应错误的页面**

- 保存对应错误的html页面，400、404可以单独创建两个不同的html页面，也可以写4xx.html，系统遇到错误，会根据错误的status自动去找
- 如404错误，就会去找404.html，找不到就会找4xx.html。其他也同理，看自己需不需要写多个页面了，一般两个页面分别表示4xx 和 5xx错误就可以了
- 如果都找不到，那就会生成一个白页，包含错误信息

![image-20220720231802271](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220720231802271.png)



##### 2、html页面

主要是展示错误信息，具体信息可以直接读取json字符串的内容

- timestamp

- status

- error

- message

- path

![image-20220720232852345](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220720232852345.png)

#### 3、自定义处理异常

![image-20220720232528361](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220720232528361.png)

自定义一个异常类，然后选择处理那些异常，类中可以自己添加想要的处理结果

下例中，遇到运算异常和空指针异常，就会返回登录页。

```java
/**
 * @ClassName GlobalExceptionHandler
 * @Description TODO:自定义处理异常，全局接收，这里暂时只判断了运算符和空指针的两个异常
 */

@Slf4j
@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler({ArithmeticException.class,NullPointerException.class}) // 处理的异常添加进去，哪些类型自定义
    public String handleArithException(Exception e){

        log.error("异常是：{}",e);
        return "login";
    }
}
```



### 9、==Web三大组件注入==

#### 1、使用Servlet API

- 第一步，在==启动类==中，添加扫描位置注解
- @ServletComponentScan(basePackages = "com.atguigu.admin") :指定原生Servlet组件都放在那里
- ![image-20220721011356596](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220721011356596.png)

##### @WebServlet

- @WebServlet(urlPatterns = "/my")：
- 效果：直接响应，没有经过Spring的拦截器
- ![image-20220721191459765](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220721191459765.png)

##### @WebFilter

- @WebFilter(urlPatterns={"/css/*","/images/*"})，过滤器

- ![image-20220721192826636](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220721192826636.png)

##### @WebListener

- ![image-20220721192904803](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220721192904803.png)

推荐可以这种方式；

==/*是servlet的所有文件的意思，双**是Spring的所有文件的意思==

扩展：DispatchServlet 如何注册进来？

容器中自动配置了  DispatcherServlet  属性绑定到 WebMvcProperties；对应的配置文件配置项是 spring.mvc。
通过 ServletRegistrationBean<DispatcherServlet> 把 DispatcherServlet  配置进来。
默认映射的是 / 路径。



#### 2、使用RegistrationBean

ServletRegistrationBean, FilterRegistrationBean, and ServletListenerRegistrationBean

```java
@Configuration
public class MyRegistConfig {

    @Bean
    public ServletRegistrationBean myServlet(){
        MyServlet myServlet = new MyServlet();

        return new ServletRegistrationBean(myServlet,"/my","/my02");
    }


    @Bean
    public FilterRegistrationBean myFilter(){

        MyFilter myFilter = new MyFilter();
//        return new FilterRegistrationBean(myFilter,myServlet());
        FilterRegistrationBean filterRegistrationBean = new FilterRegistrationBean(myFilter);
        filterRegistrationBean.setUrlPatterns(Arrays.asList("/my","/css/*"));
        return filterRegistrationBean;
    }

    @Bean
    public ServletListenerRegistrationBean myListener(){
        MySwervletContextListener mySwervletContextListener = new MySwervletContextListener();
        return new ServletListenerRegistrationBean(mySwervletContextListener);
    }
}
```





### 10、嵌入式Servlet容器

#### 1、切换嵌入式Servlet容器

==就是tomcat等几个不同的服务器，内嵌到SpringBoot里了，不用单独配置==

- 默认支持的webServer

  - Tomcat, Jetty, or Undertow
  - ServletWebServerApplicationContext 容器启动寻找ServletWebServerFactory 并引导创建服务器

- 切换服务器

  - ![image.png](https://pledge99.oss-cn-beijing.aliyuncs.com/img/1606280937533-504d0889-b893-4a01-af68-2fc31ffce9fc.png)

  - ```xml
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
        <exclusions>
            <exclusion>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-tomcat</artifactId>
            </exclusion>
        </exclusions>
    </dependency>
    ```

- 原理

  - SpringBoot应用启动发现当前是Web应用。web场景包-导入tomcat
  - web应用会创建一个web版的ioc容器 ServletWebServerApplicationContext 
  - ServletWebServerApplicationContext 启动的时候寻找 ServletWebServerFactory（Servlet 的web服务器工厂--> Servlet 的web服务器） 
  - SpringBoot底层默认有很多的WebServer工厂；TomcatServletWebServerFactory,JettyServletWebServerFactory, or UndertowServletWebServerFactory
  - 底层直接会有一个自动配置类。ServletWebServerFactoryAutoConfiguration
  - ServletWebServerFactoryAutoConfiguration导入了ServletWebServerFactoryConfiguration（配置类）
  - ServletWebServerFactoryConfiguration 配置类 根据动态判断系统中到底导入了那个Web服务器的包。（默认是web-starter导入tomcat包），容器中就有 TomcatServletWebServerFactory
  - TomcatServletWebServerFactory 创建出Tomcat服务器并启动；TomcatWebServer 的构造器拥有初始化方法initialize---this.tomcat.start();
  - 内嵌服务器，就是手动把启动服务器的代码调用（tomcat核心jar包存在）



#### 2、定制Servlet容器

- 实现  WebServerFactoryCustomizer<ConfigurableServletWebServerFactory> 
  - 把配置文件的值和ServletWebServerFactory 进行绑定
- 修改配置文件 server.xxx
- 直接自定义 ConfigurableServletWebServerFactory 

xxxxxCustomizer：定制化器，可以改变xxxx的默认规则

```java
import org.springframework.boot.web.server.WebServerFactoryCustomizer;
import org.springframework.boot.web.servlet.server.ConfigurableServletWebServerFactory;
import org.springframework.stereotype.Component;

@Component
public class CustomizationBean implements WebServerFactoryCustomizer<ConfigurableServletWebServerFactory> {

    @Override
    public void customize(ConfigurableServletWebServerFactory server) {
        server.setPort(9000);
    }

}
```

### 11、定制化原理

#### 1、定制化的常见方式 

- 修改配置文件；

- xxxxxCustomizer；

- 编写自定义的配置类   xxxConfiguration；+ @Bean替换、增加容器中默认组件；视图解析器 

- Web应用 编写一个配置类实现 WebMvcConfigurer 即可定制化web功能；+ @Bean给容器中再扩展一些组件

- ```java
  @Configuration
  public class AdminWebConfig implements WebMvcConfigurer
  ```

- @EnableWebMvc + WebMvcConfigurer —— @Bean  可以全面接管SpringMVC，所有规则全部自己重新配置； 实现定制和扩展功能

- 原理

- 1、WebMvcAutoConfiguration  默认的SpringMVC的自动配置功能类。静态资源、欢迎页.....

- 2、一旦使用 @EnableWebMvc 、。会 @Import(DelegatingWebMvcConfiguration.class)

- 3、DelegatingWebMvcConfiguration 的 作用，只保证SpringMVC最基本的使用

  - 把所有系统中的 WebMvcConfigurer 拿过来。所有功能的定制都是这些 WebMvcConfigurer  合起来一起生效
  - 自动配置了一些非常底层的组件。RequestMappingHandlerMapping、这些组件依赖的组件都是从容器中获取
  - public class DelegatingWebMvcConfiguration extends WebMvcConfigurationSupport

- 4、WebMvcAutoConfiguration 里面的配置要能生效必须@ConditionalOnMissingBean(WebMvcConfigurationSupport.class)

- 5、@EnableWebMvc  导致了 WebMvcAutoConfiguration  没有生效。

- 

#### 2、原理分析套路

场景starter - xxxxAutoConfiguration - 导入xxx组件 - 绑定xxxProperties -- 绑定配置文件项 



## 3、==访问数据库==

### 1、默认数据源---**HikariDataSource**

##### 1、引入jdbc依赖

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jdbc</artifactId>
</dependency>
```

##### 2、引入MySQL依赖

不写版本也行，SpringBoot会自动进行版本仲裁，八成是最新版

```xml
<dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
<!--            <version>8.0.28</version>-->
        </dependency>
```

还可以在顶部单独配置版本

```xml
<properties>
    <java.version>1.8</java.version>
    <mysql.version>5.1.49</mysql.version>
</properties>
```

##### 3、修改配置文件

yaml文件，属性后边记得==空格==

```yaml
spring:
  datasource:
#    url: jdbc:mysql://localhost:3306/Pledge?useSSL=true&useUnicode=true&characterEncoding=UTF-8&serverTimezone=GMT%2B8
    url: jdbc:mysql://localhost:3306/mybatis?serverTimezone=GMT%2B8
    username: root
    password: 123456
    driver-class-name: com.mysql.cj.jdbc.Driver

```

还可以修改一些jdbc的其他属性，例如超时提醒等

```yaml
 spring:
 		jdbc:
  		  template:
    	  		# 超时提醒，超过3秒就提醒
      			query-timeout: 3
```

##### 4、测试数据库

创建接收类

```java
@Data
@NoArgsConstructor
@AllArgsConstructor
public class sqlTestUser {
    private int id;
    private String name;
    private String pwd;
}
```

待查表单

![image-20220722124532585](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220722124532585.png)

测试类中查询

![image-20220722124748016](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220722124748016.png)

这个JdbcTemplate的query操作比较不正常，需要研究后使用

比如。forList只能查一行数据。

```java
@Slf4j
@SpringBootTest
class Springboot05WebAdminApplicationTests {

    @Autowired
    JdbcTemplate jdbcTemplate;

    @Test
    void contextLoads() {
        String sql = "select * from user";
        List<sqlTestUser> user = jdbcTemplate.query(sql, new BeanPropertyRowMapper<>(sqlTestUser.class));

        for (sqlTestUser s : user){
            log.info("第{}号用户为：{}，密码是{}",s.getId(),s.getName(),s.getPwd());
        }
    }
}
```

运行结果

![image-20220722124715620](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220722124715620.png)



##### 5、自动配置原理

1、自动配置的类

- DataSourceAutoConfiguration ： 数据源的自动配置

  - 修改数据源相关的配置：spring.datasource

  - 数据库连接池的配置，是自己容器中没有DataSource才自动配置的

  - 底层配置好的连接池是：==HikariDataSource==

```java
	@Configuration(proxyBeanMethods = false)
	@Conditional(PooledDataSourceCondition.class)
	@ConditionalOnMissingBean({ DataSource.class, XADataSource.class })
	@Import({ DataSourceConfiguration.Hikari.class, DataSourceConfiguration.Tomcat.class,
			DataSourceConfiguration.Dbcp2.class, DataSourceConfiguration.OracleUcp.class,
			DataSourceConfiguration.Generic.class, DataSourceJmxConfiguration.class })
	protected static class PooledDataSourceConfiguration
```

- DataSourceTransactionManagerAutoConfiguration： 事务管理器的自动配置

- JdbcTemplateAutoConfiguration： JdbcTemplate的自动配置，可以来对数据库进行crud

  - 可以修改这个配置项@ConfigurationProperties(prefix = "spring.jdbc") 来修改JdbcTemplate

  - @Bean@Primary    JdbcTemplate；容器中有这个组件

- JndiDataSourceAutoConfiguration： jndi的自动配置
- XADataSourceAutoConfiguration： 分布式事务相关的



### 2、使用Druid数据源

##### 1、druid官方github地址

https://github.com/alibaba/druid

整合第三方技术的两种方式【主要介绍starter自动配置】

- 自定义
- 找starter

##### 2、引入druid-starter

```xml
<dependency>
  	<groupId>com.alibaba</groupId>
  	<artifactId>druid-spring-boot-starter</artifactId>
  	<version>1.1.17</version>
</dependency>
```

##### 3、修改配置文件

所有配置项的内容如下：

https://github.com/alibaba/druid/wiki/DruidDataSource%E9%85%8D%E7%BD%AE%E5%B1%9E%E6%80%A7%E5%88%97%E8%A1%A8

```yaml
spring:
  datasource:
		# url: jdbc:mysql://localhost:3306/Pledge?useSSL=true&useUnicode=true&characterEncoding=UTF-8&serverTimezone=GMT%2B8
    url: jdbc:mysql://localhost:3306/mybatis?serverTimezone=GMT%2B8
    username: root
    password: 123456
    driver-class-name: com.mysql.cj.jdbc.Driver

    druid:
      aop-patterns: com.pledge.admin.*  #监控SpringBean 选择监控位置
      filters: stat,wall     # 底层开启功能，stat（sql监控），wall（防火墙）

      stat-view-servlet:   # 配置监控页功能
        enabled: true
        login-username: admin
        login-password: admin
        resetEnable: false  # 关闭重置按钮

      web-stat-filter:  # 监控web
        enabled: true
        urlPattern: /*
        exclusions: '*.js,*.gif,*.jpg,*.png,*.css,*.ico,/druid/*'


      filter:
        stat:    # 对上面filters里面的stat的详细配置
          slow-sql-millis: 1000   # 慢查询超过1000毫秒就记录
          logSlowSql: true
          enabled: true
        wall:
          enabled: true
          config:
            drop-table-allow: false
```

##### 4、查看监控器

在项目网址后面直接加```/druid```访问即可，如有设置账号密码，会弹出登录页面

![image-20220722143249971](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220722143249971.png)

监控页面

![image-20220722143439776](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220722143439776.png)





##### 5、自动配置原理

- 扩展配置项 spring.datasource.druid
- DruidSpringAopConfiguration.class,   监控SpringBean的；
  - 配置项：spring.datasource.druid.aop-patterns
- DruidStatViewServletConfiguration.class, 监控页的配置：
  - spring.datasource.druid.stat-view-servlet；默认开启
- DruidWebStatFilterConfiguration.class, web监控配置；
  - spring.datasource.druid.web-stat-filter；默认开启
- DruidFilterConfiguration.class}) 所有Druid自己filter的配置

```java
    private static final String FILTER_STAT_PREFIX = "spring.datasource.druid.filter.stat";
    private static final String FILTER_CONFIG_PREFIX = "spring.datasource.druid.filter.config";
    private static final String FILTER_ENCODING_PREFIX = "spring.datasource.druid.filter.encoding";
    private static final String FILTER_SLF4J_PREFIX = "spring.datasource.druid.filter.slf4j";
    private static final String FILTER_LOG4J_PREFIX = "spring.datasource.druid.filter.log4j";
    private static final String FILTER_LOG4J2_PREFIX = "spring.datasource.druid.filter.log4j2";
    private static final String FILTER_COMMONS_LOG_PREFIX = "spring.datasource.druid.filter.commons-log";
    private static final String FILTER_WALL_PREFIX = "spring.datasource.druid.filter.wall";
```

### 3、整合MyBatis

官方GitHub地址：https://github.com/mybatis

下面介绍混合使用方式，```注解```和```配置文件```同时存在

- 注解：实现简单sql语句的操作
- 配置文件：当SQL语句较为复杂时，使用比较方便

##### 1、导入依赖

```xml
<dependency>
    <groupId>org.mybatis.spring.boot</groupId>
    <artifactId>mybatis-spring-boot-starter</artifactId>
    <version>2.2.2</version>
</dependency>
```

或者在创建项目的时候，初始化选择MyBatis

![image-20220722223355917](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220722223355917.png)

##### 2、调整配置

==切记！！！mybatis顶行写，跟spring平级==

主要是指出配置文件位置```mapper-locations:```

```yaml
# 配置mybatis规则
mybatis:
  #  config-location: classpath:mybatis/mybatis-config.xml
  mapper-locations: classpath:mybatis/mapper/*.xml
  configuration:
    map-underscore-to-camel-case: true #开启驼峰命名规则，自动调整数据库和Java类的对应关系stu_name  == stuName
```

<img src="https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220723000210846.png" alt="image-20220723000210846" style="zoom:50%;" />

##### 3、编写Mapper接口

- ```java
  @Mapper
  public interface sqlUserMapper {
      // 注解的方式实现查询操作
      @Select("select * from user where id=#{id}")
      public sqlTestUser getById(Long id);
  
  
      // 注解方式实现插入操作，并开启自增主键，插入后返回到Java对象
      @Insert("insert into user(`id`,`name`,`pwd`) values (#{id},#{name},#{pwd})")
      @Options(useGeneratedKeys = true, keyProperty = "id")
      void insert(sqlTestUser user);
  
  
      // 配置文件实现插入操作
      public void insert(sqlTestUser user);
      
  }
  ```

使用配置文件的方式，还要编写对应的配置文件

配置文件存储位置，要在yaml文件中指出，要不然找不到

![image-20220723001849250](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220723001849250.png)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

<mapper namespace="com.pledge.admin.mapper.sqlUserMapper">
  
<!--    id是该sqlUserMapper接口中的方法名-->
    <insert id="insert" useGeneratedKeys="true" keyProperty="id">
        insert into user(`id`,`name`,`pwd`) values (#{id},#{name},#{pwd})
    </insert>
</mapper>
```

- **useGeneratedKeys="true"：**
  - 数据库中自增主键，执行插入方法后，如果属性为true，那么会把新增的主键id返回
- **keyProperty="id" ：** 
  - user类中可以接收自增主键id的属性名称，会自动赋值给user对象
- ==举例：==controller执行插入操作，插入user对象包含【id，name，password】三个属性
  - 因为id列是自增长列，所以插入时仅提供name和password属性即可
  - 要求controller同时展示插入的user对象，到html页面
  - 但是因为没有id列，最后展示结果就是【id=null，name=小花，password=123456】
  - 这显然不符合要求，所以在插入操作时，useGeneratedKeys="true" 并用id属性接收这个自增IDkeyProperty="id" 
  - 开启了insert这两个属性后，展示结果为【id=55，name=小花，password=123456】





##### 4、编写Service接口和实现类

<img src="https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220723115824265.png" alt="image-20220723115824265" style="zoom:50%;" />

先编写接口

```java
public interface userService {

    public sqlTestUser getById(Long id);

    public void saveUser(sqlTestUser user) ;
}
```

再编写接口对应实现类

自动注入mapper接口，实现其方法

```java

@Slf4j
@Service
public class userServiceImpl implements userService {

    @Autowired
    sqlUserMapper sqlUserMapper;

    @Override
    public sqlTestUser getById(Long id){
        return  sqlUserMapper.getById(id);
    }

    @Override
    public void saveUser(sqlTestUser user) {
        sqlUserMapper.insert(user);
    }
}
```



##### 5、编写Controller类

接收前端请求，处理数据，返回数据

```java
@Slf4j
@Controller
public class MyBatisController {

    @Autowired
    userServiceImpl userServiceImpl;

    @ResponseBody
    @PostMapping("/user")
    public sqlTestUser saveUser(sqlTestUser user){
        userServiceImpl.saveUser(user);
        return user;
    }


    @ResponseBody
    @GetMapping("/user")
    public  sqlTestUser queryuser(@RequestParam("id") Long id){
        return userServiceImpl.getById(id);
    }
}
```



### 4、整合MyBatis Plus

##### 1、什么是MyBatis-Plus

- MyBatis-Plus（简称 MP）是一个 MyBatis 的增强工具，在 MyBatis 的基础上只做增强不做改变，为简化开发、提高效率而生。

  - MyBatis-Plus 官网：https://baomidou.com/

  - MyBatis-Plus GItHub：https://github.com/baomidou/mybatis-plus

建议在Idea中安装 MybatisX 插件 

==优点：==

-  只需要我们的Mapper继承 BaseMapper 就可以拥有crud能力

##### 2、导入依赖及配置

```xml
<!--    MyBatis Plus依赖-->
        <dependency>
            <groupId>com.baomidou</groupId>
            <artifactId>mybatis-plus-boot-starter</artifactId>
            <version>3.5.2</version>
        </dependency>
```

自动配置原理：

- MybatisPlusAutoConfiguration 配置类，MybatisPlusProperties 配置项绑定。
  - mybatis-plus：xxx 就是对mybatis-plus的定制
- SqlSessionFactory 自动配置好。底层是容器中默认的数据源
- mapperLocations 自动配置好的。有默认值。classpath*:/mapper/**/*.xml；
  - 任意包的类路径下的所有mapper文件夹下任意路径下的所有xml都是sql映射文件。  建议以后sql映射文件，放在 mapper下，
- 容器中也自动配置好了 SqlSessionTemplate
- @Mapper 标注的接口也会被自动扫描；建议直接 @MapperScan("com.atguigu.admin.mapper") 批量扫描就行
  - 就是直接在启动类，增加mapper扫描地点，不用每个mapper类都添加@mapper注解了

==简言之：==

- 直接用系统的数据源就可以，yaml配置信息不用额外添加

  - ```yaml
    spring:
      datasource:
    #    url: jdbc:mysql://localhost:3306/Pledge?useSSL=true&useUnicode=true&characterEncoding=UTF-8&serverTimezone=GMT%2B8
        url: jdbc:mysql://localhost:3306/mybatis?serverTimezone=GMT%2B8
        username: root
        password: 123456
        driver-class-name: com.mysql.cj.jdbc.Driver
    
    # druid这里不配也行，用系统默认的
        druid:
          aop-patterns: com.pledge.admin.*  #监控SpringBean
          filters: stat,wall     # 底层开启功能，stat（sql监控），wall（防火墙）
    
          stat-view-servlet: # 配置监控页功能
            enabled: true
            login-username: admin
            login-password: admin
            resetEnable: false
    
          web-stat-filter: # 监控web
            enabled: true
            urlPattern: /*
            exclusions: '*.js,*.gif,*.jpg,*.png,*.css,*.ico,/druid/*'
    
    
          filter:
            stat: # 对上面filters里面的stat的详细配置
              slow-sql-millis: 1000
              logSlowSql: true
              enabled: true
            wall:
              enabled: true
              config:
                drop-table-allow: false
    ```

- 建议在启动类增加mapper文件夹注解，这样这个文件夹里面都是mapper，就不用单独注解了

  - ![image-20220723121844648](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220723121844648.png)
  - ![image-20220723122011556](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220723122011556.png)

- 自动配置了mapper路径，不用单独写配置，直接创建个mapper文件下面放就行了

  - <img src="https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220723122136728.png" alt="image-20220723122136728" style="zoom:50%;" />
  - <img src="https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220723122228089.png" alt="image-20220723122228089" style="zoom:50%;" />





##### 3、创建实体类

- 数据库表cities如下：
  - ![image-20220723125923404](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220723125923404.png)

- 实体类City

  - @TableName("cities")

    - 数据库表名和实体类名称不一致时，用该注解表示映射关系

  - @TableField(exist = false) 

    - 当前属性，在表中不存在，默认是true表示存在

  - ```java
    @TableName("cities")// 数据库表名和实体类名称不一致时，用该注解表示映射关系
    @Data
    @NoArgsConstructor
    @AllArgsConstructor
    public class City {
        // 数据库中的对应字段
        private  Integer id;
        private String cityid;
        private String city;
        private String provinceid;
    
        // 假设这个类，还有一个数据库中没有的字段
        // 这时候要加一个注解，告诉MyBatis Plus，这个字段没在数据库中，要不然自动对应，就该显示查不到了
        @TableField(exist = false) // 当前属性，在表中不存在，默认是true表示存在
        private String noSQl;
    }
    ```

##### 4、创建Mapper接口

<font color="red">MyBatis Plus最大优势！！！！直接继承BaseMapper<实体类>，其中直接包含了若干方法，不用写增删改查了</font>

除非你的操作比较复杂，那么自己单独写xml即可

![image-20220723130143632](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220723130143632.png)

![image-20220723130346806](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220723130346806.png)

**若需自己写时，和MyBatis一样，直接写一个方法，然后xml文件id=方法名，写上SQL语句，后续直接调用方法即可**

![image-20220723130558472](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220723130558472.png)

![image-20220723130620958](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220723130620958.png)



##### 5、编写Service接口及实现类

**Service接口：**

- Service 继承IService这个顶级Service接口
- 泛型：<City>     是指要返回的实现类

- 这个```IService```中包含了超多的CRUD操作，不用写了

- ```java
  public interface CityService extends IService<City> {
  }
  ```

**Service实现类：**

- 同时，实现类也不用全部重写IService中的方法，继承ServiceImpl类即可

- 泛型：<CityMapper, City>

  - CityMapper：要操作哪个mapper接口
  - City：这个mapper接口返回的实体类类型

- ```java
  @Service
  public class CityServiceImpl extends ServiceImpl<CityMapper, City> implements CityService {
  }
  ```

这就结束了，后面直接调用ServiceImpl的方法用即可



##### 6、编写CityController

此处因为在html页面展示效果，就放在TablelController中，不再单独编写Controller

**主要是分页处理：**

首先配置分页插件

```java
@Configuration
public class MyBatisPlusConfig {
    @Bean
    public MybatisPlusInterceptor mybatisPlusInterceptor(){
        //1 创建MybatisPlusInterceptor拦截器对象
        MybatisPlusInterceptor mpInterceptor=new MybatisPlusInterceptor();
        //2 添加分页拦截器
        mpInterceptor.addInnerInterceptor(new PaginationInnerInterceptor());
        return mpInterceptor;
    }
}
```

![image-20220723151432378](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220723151432378.png)

###### ==分页查询==

- ```java
  @Controller
  public class TablelController {
  		// 注入方法
      @Autowired
      CityServiceImpl cityServiceImpl;
  
      @GetMapping("/dynamic_table")
      public String dynamic_table(@RequestParam(value = "pn",defaultValue = "1") Integer pn, Model model){//默认第一页
  
          // 分页查询的数据，从pn页开始，每页20行数据
          Page<City> cityPage = new Page<>(pn, 20);
          // 分页查询的结果,查询条件null。暂时不设条件
          Page<City> page = cityServiceImpl.page(cityPage,null);
          model.addAttribute("page",page);
          return "table/dynamic_table";
      }
  }
  ```

- 在html页面中，利用page的一些属性，实现分页数据展示

- ![Page源码](https://pledge99.oss-cn-beijing.aliyuncs.com/img/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2J1bGluc3Rhcg==,size_16,color_FFFFFF,t_70.png)

  - records 
    - 用来存放查询出来的数据
  - total 
    - 返回记录的总数
  - size 
    - 每页显示条数，默认 10
  - current 
    - 当前页,默认1
  - orders 
    - 排序字段信息
  - optimizeCountSql 
    - 自动优化 COUNT SQL,默认true
  - isSearchCount 
    - 是否进行 count 查询,默认true
  - hitCount 
    - 是否命中count缓存,默认false

- ![image-20220723203350239](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220723203350239.png)



###### ==删除操作==

主要涉及到删除后，页面重定向，不能返回第一页

要保证第10页数据删除一个，返回页面还是第10页，不能重定向跑到第一页了

```java
@Slf4j
@Controller
public class TablelController {

    @Autowired
    CityServiceImpl cityServiceImpl;

    @GetMapping("/city/delete/{id}")
    public String deleteCity(@PathVariable("id") Integer id,
                             @RequestParam(value = "pn",defaultValue = "1") Integer pn,
                             RedirectAttributes ra){
        // 删除id数据
        cityServiceImpl.removeById(id);
        ra.addAttribute("pn",pn);
        // 重定向到当前页码
        return "redirect:/dynamic_table";
    }
  
  @GetMapping("/dynamic_table")
    public String dynamic_table(@RequestParam(value = "pn",defaultValue = "1") Integer pn, Model model){//默认第一页

        // 分页查询的数据，从pn也开始，每页20行数据
        Page<City> cityPage = new Page<>(pn, 20);
        // 分页查询的结果,查询条件null。暂时不设条件
        Page<City> page = cityServiceImpl.page(cityPage,null);
        model.addAttribute("page",page);
        return "table/dynamic_table";

    }
}
```

**RedirectAttributes：重定向携带参数，**

重定向到/dynamic_table后，又获取到该参数，利用该参数查询分页数据。



### 5、整合Redis

Redis 是一个开源（BSD许可）的，内存中的数据结构存储系统，它可以用作数据库、缓存和消息中间件。 它支持多种类型的数据结构，如 字符串（strings）， 散列（hashes）， 列表（lists）， 集合（sets）， 有序集合（sorted sets） 与范围查询， bitmaps， hyperloglogs 和 地理空间（geospatial） 索引半径查询。 Redis 内置了 复制（replication），LUA脚本（Lua scripting）， LRU驱动事件（LRU eviction），事务（transactions） 和不同级别的 磁盘持久化（persistence）， 并通过 Redis哨兵（Sentinel）和自动 分区（Cluster）提供高可用性（high availability）。

##### 1、导入依赖

```xml
<dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

如果想导入jedis，还可以导入jedis依赖，然后修改配置文件client-type: jedis

```xml
<!--        导入jedis-->
        <dependency>
            <groupId>redis.clients</groupId>
            <artifactId>jedis</artifactId>
        </dependency>
```





**自动配置原理：**

- RedisAutoConfiguration 自动配置类。
  - RedisProperties 属性类 --> spring.redis.xxx是对redis的配置
- 连接工厂是准备好的。LettuceConnectionConfiguration、JedisConnectionConfiguration
- 自动注入了RedisTemplate<Object, Object> ： xxxTemplate；
- 自动注入了StringRedisTemplate；k：v都是String
  - key：value
- 底层只要我们使用 StringRedisTemplate、RedisTemplate就可以操作redis



##### 2、redis环境搭建

1、阿里云按量付费redis。经典网络
2、申请redis的公网连接地址
3、修改白名单  允许0.0.0.0/0 访问



##### 3、修改配置文件

```yaml
spring
  redis:
    host: r-bp1iq3z3avbg361zg6pd.redis.rds.aliyuncs.com
    port: 6379
    # 阿里云的密码是    【账户名：密码】
    password: pledge:Pledge99
    client-type: jedis
    jedis:
      pool:
        max-active: 10
```



##### 4、测试

```java
@Test
void testRedis(){
  	// 获取数据
	  ValueOperations<String, String> operations = redisTemplate.opsForValue();
		// 增加新的key:value
    operations.set("hello","world");
		// 根据key 查询value
    String hello = operations.get("hello");
  	// 输出value
    System.out.println(hello);
}
```

##### 5、实操

需求：在页面展示某某网页的访问次数

![image-20220724121256892](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220724121256892.png)

思路：

1. 设置拦截器：拦截所有请求
2. 拦截后，获取uri，存入Redis
   - key：uri
   - value：次数++
3. Controller获取Redis，传给前端



###### **1、创建拦截器**

```java
@Component
public class RedisUrlCountInterceptor implements HandlerInterceptor {

    @Autowired
    StringRedisTemplate redisTemplate;

    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
      
        String uri = request.getRequestURI();
      
        // 默认每次访问当前uri的时候，就会计数+1
        redisTemplate.opsForValue().increment(uri);

        // 全部放行，不拦截，拦下来只是为了统计访问次数
        return true;
    }
}
```

###### **2、添加拦截器**

之前拦截器，可以在添加时，直接new一个，这里不行，因为拦截器类中有自动注入的类，不光只有一个重写的方法，当拦截器只有重写的方法时，可以new拦截器添加，否则就要先注入拦截器，再调用

```java
@Configuration
public class AdminWebConfig implements WebMvcConfigurer {

    @Autowired
    RedisUrlCountInterceptor redisUrlCountInterceptor;

    // 添加拦截器
    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        // 拦截所有网页
        registry.addInterceptor(redisUrlCountInterceptor)
                .addPathPatterns("/**")
                .excludePathPatterns("/","/login","/css/**","/fonts/**","/images/**","/js/**","/user");
    }
}
```

![image-20220724122322463](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220724122322463.png)

###### 3、编写Controller

```java
@Controller
public class IndexController {
    @Autowired
    StringRedisTemplate redisTemplate;

    @GetMapping("/main.html")
    public String mainPage(HttpSession session,Model model){
        // 获取到Redis数据
        ValueOperations<String, String> opsForValue = redisTemplate.opsForValue();
        
        // 读取对应key的value值，在拦截器中用uri做key，次数做value存到Redis中了
        String numMain = opsForValue.get("/main.html");
        String numSql = opsForValue.get("/sql");
        
        // 传给前端
        model.addAttribute("mainCount",numMain);
        model.addAttribute("sqlCount",numSql);
        return "main";
    }
}
```

###### 4、前端获取数据

![image-20220724122542386](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220724122542386.png)



## 4、单元测试

### 1、JUnit5 的变化

Spring Boot 2.2.0 版本开始引入 JUnit 5 作为单元测试默认库
作为最新版本的JUnit框架，JUnit5与之前版本的Junit框架有很大的不同。由三个不同子项目的几个不同模块组成。

- JUnit 5 = JUnit Platform + JUnit Jupiter + JUnit Vintage
  - JUnit Platform: Junit Platform是在JVM上启动测试框架的基础，不仅支持Junit自制的测试引擎，其他测试引擎也都可以接入。
  - JUnit Jupiter: JUnit Jupiter提供了JUnit5的新的编程模型，是JUnit5新特性的核心。内部 包含了一个测试引擎，用于在Junit Platform上运行。
  - JUnit Vintage: 由于JUint已经发展多年，为了照顾老的项目，JUnit Vintage提供了兼容JUnit4.x,Junit3.x的测试引擎。
  - ![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/1606796395719-eb57ab48-ae44-45e5-8d2e-c4d507aff49a.png)

注意：
SpringBoot 2.4 以上版本移除了默认对 Vintage 的依赖。如果需要兼容junit4需要自行引入（不能使用junit4的功能 @Test）

JUnit 5’s Vintage Engine Removed from spring-boot-starter-test,如果需要继续兼容junit4需要自行引入vintage

- ```xml
  #手动引入vintage依赖，去兼容junit4
  <dependency>
      <groupId>org.junit.vintage</groupId>
      <artifactId>junit-vintage-engine</artifactId>
      <scope>test</scope>
      <exclusions>
          <exclusion>
              <groupId>org.hamcrest</groupId>
              <artifactId>hamcrest-core</artifactId>
          </exclusion>
      </exclusions>
  </dependency>
  ```



**Junit5 依赖引入：**默认工程创建的时候就引入了

- ```xml
  <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-test</artifactId>
      <scope>test</scope>
  </dependency>
  ```

**测试类注解：**一个@SpringBootTest就够了

- ```java
  @SpringBootTest
  class Boot05WebAdminApplicationTests {
      @Test
      void contextLoads() {
  
      }
  }
  ```



以前：
@SpringBootTest + @RunWith(SpringTest.class)


SpringBoot整合Junit以后。

- 编写测试方法：@Test标注（注意需要使用junit5版本的注解）
- Junit类具有Spring的功能，@Autowired、比如 **@Transactional 标注测试方法，测试完成后自动回滚**



### 2、JUnit5常用注解

JUnit5的注解与JUnit4的注解有所变化
https://junit.org/junit5/docs/current/user-guide/#writing-tests-annotations

- @Test :表示方法是测试方法。但是与JUnit4的@Test不同，他的职责非常单一不能声明任何属性，拓展的测试将会由Jupiter提供额外测试
- @ParameterizedTest :表示方法是参数化测试，下方会有详细介绍
- @RepeatedTest :表示方法可重复执行，下方会有详细介绍

- @DisplayName :为测试类或者测试方法设置展示名称

- @BeforeEach :表示在每个单元测试之前执行


- @AfterEach :表示在每个单元测试之后执行


- @BeforeAll :表示在所有单元测试之前执行

- @AfterAll :表示在所有单元测试之后执行

- @Tag :表示单元测试类别，类似于JUnit4中的@Categories

- @Disabled :表示测试类或测试方法不执行，类似于JUnit4中的@Ignore

- @Timeout :表示测试方法运行如果超过了指定时间将会返回错误

- @ExtendWith :为测试类或测试方法提供扩展类引用



```java
public class TestDemo {

    @Test
    @DisplayName("第一次测试")  // 为测试方法起名字，便于理解
    public void firstTest() {
        System.out.println("hello world");
    }
}
```

![image-20220724185800932](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220724185800932.png)

### 3、断言（assertions）

断言（assertions）是测试方法中的核心部分，用来对测试需要满足的条件进行验证。这些断言方法都是 org.junit.jupiter.api.Assertions 的静态方法。

JUnit 5 内置的断言可以分成如下几个类别：

- 检查业务逻辑返回的数据是否合理。
- 所有的测试运行结束以后，会有一个详细的测试报告；

#### 1、简单断言

用来对单个值进行简单的验证。如：

**就是给两个值，判断是否相等，或者是true和false，就是简单一步就能判断的相关操作**

- | 方法            | 说明                                 |
  | --------------- | ------------------------------------ |
  | assertEquals    | 判断两个对象或两个原始类型是否相等   |
  | assertNotEquals | 判断两个对象或两个原始类型是否不相等 |
  | assertSame      | 判断两个对象引用是否指向同一个对象   |
  | assertNotSame   | 判断两个对象引用是否指向不同的对象   |
  | assertTrue      | 判断给定的布尔值是否为 true          |
  | assertFalse     | 判断给定的布尔值是否为 false         |
  | assertNull      | 判断给定的对象引用是否为 null        |
  | assertNotNull   | 判断给定的对象引用是否不为 null      |

```java
@Test
@DisplayName("simple assertion")
public void simple() {
     assertEquals(3, 1 + 2, "simple math");
     assertNotEquals(3, 1 + 1);

     assertNotSame(new Object(), new Object());
     Object obj = new Object();
     assertSame(obj, obj);

     assertFalse(1 > 2);
     assertTrue(1 < 2);

     assertNull(null);
     assertNotNull(new Object());
}
```

![image-20220724190155079](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220724190155079.png)

#### 2、数组断言

通过 assertArrayEquals 方法来判断两个对象或原始类型的数组是否相等，数组内容颠倒也不行

```java
@Test
@DisplayName("array assertion")
public void array() {

  		assertArrayEquals(new int[]{2, 1}, new int[] {1, 2});
}
```

![image-20220724190535190](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220724190535190.png)

#### 3、组合断言

assertAll 方法接受多个 org.junit.jupiter.api.Executable 函数式接口的实例作为要验证的断言，可以通过 lambda 表达式很容易的提供这些断言

```java
@Test
@DisplayName("assert all")
public void all() {
    assertAll("Math",
            () -> assertEquals(2, 1 + 1),
            () -> assertTrue(1 > 0)
    );
}
```

#### 4、异常断言

在JUnit4时期，想要测试方法的异常情况时，需要用@Rule注解的ExpectedException变量还是比较麻烦的。

而JUnit5提供了一种新的断言方式Assertions.assertThrows() ,配合函数式编程就可以进行使用。

```java
@Test
@DisplayName("异常测试")
public void exceptionTest() {
    ArithmeticException exception = Assertions.assertThrows(
           //扔出断言异常
            ArithmeticException.class, () -> System.out.println(1 % 0));

}
```

#### 5、超时断言

Junit5还提供了Assertions.assertTimeout() 为测试方法设置了超时时间

```java
@Test
@DisplayName("超时测试")
public void timeoutTest() {
    //如果测试方法时间超过1s将会异常
    Assertions.assertTimeout(Duration.ofMillis(1000), () -> Thread.sleep(500));
}
```

#### 6、快速失败

通过 fail 方法直接使得测试失败【就是类似循环中的break，函数中的return】

有时测试类是统一执行的，方法很多，可以利用fail退出一个方法，或者中断操作

```java
@Test
@DisplayName("fail")
public void shouldFail() {
 			fail("This should fail");
}
```

### 4、前置条件（assumptions）

JUnit 5 中的前置条件（assumptions【假设】）类似于断言，不同之处在于**不满足的断言会使得测试方法失败，而不满足的前置条件只会使得测试方法的执行终止。**

前置条件可以看成是测试方法执行的前提，当该前提不满足时，就没有继续执行的必要。

```java
@DisplayName("前置条件")
public class AssumptionsTest {
   private final String environment = "DEV";

   @Test
   @DisplayName("simple")
   public void simpleAssume() {
        assumeTrue(Objects.equals(this.environment, "DEV"));
        assumeFalse(() -> Objects.equals(this.environment, "PROD"));
   }

   @Test
   @DisplayName("assume then do")
   public void assumeThenDo() {
        assumingThat(
           Objects.equals(this.environment, "DEV"),
           () -> System.out.println("In DEV")
        );
   }
}
```

assumeTrue 和 assumFalse 确保给定的条件为 true 或 false，不满足条件会使得测试执行终止。

assumingThat 的参数是表示条件的布尔值和对应的 Executable 接口的实现对象。

只有条件满足时，Executable 对象才会被执行；当条件不满足时，测试执行并不会终止。



### 5、嵌套测试

JUnit 5 可以通过 Java 中的内部类和@Nested 注解实现嵌套测试，从而可以更好的把相关的测试方法组织在一起。在内部类中可以使用@BeforeEach 和@AfterEach 注解，而且嵌套的层次没有限制。

**说明：**类中还有类，如果单独测子类的一个方法，若是用到父类中的参数，他也能获取

但是运行父类的方法，不能获取子类中的参数

```java
@DisplayName("A stack")
class TestingAStackDemo {

    Stack<Object> stack;

    @Test
    @DisplayName("is instantiated with new Stack()")
    void isInstantiatedWithNew() {
        new Stack<>();
    }

    @Nested
    @DisplayName("when new")
    class WhenNew {

        @BeforeEach
        void createNewStack() {
            stack = new Stack<>();
        }

        @Test
        @DisplayName("is empty")
        void isEmpty() {
            assertTrue(stack.isEmpty());
        }

        @Test
        @DisplayName("throws EmptyStackException when popped")
        void throwsExceptionWhenPopped() {
            assertThrows(EmptyStackException.class, stack::pop);
        }

        @Test
        @DisplayName("throws EmptyStackException when peeked")
        void throwsExceptionWhenPeeked() {
            assertThrows(EmptyStackException.class, stack::peek);
        }

        @Nested
        @DisplayName("after pushing an element")
        class AfterPushing {

            String anElement = "an element";

            @BeforeEach
            void pushAnElement() {
                stack.push(anElement);
            }

            @Test
            @DisplayName("it is no longer empty")
            void isNotEmpty() {
                assertFalse(stack.isEmpty());
            }

            @Test
            @DisplayName("returns the element when popped and is empty")
            void returnElementWhenPopped() {
                assertEquals(anElement, stack.pop());
                assertTrue(stack.isEmpty());
            }

            @Test
            @DisplayName("returns the element when peeked but remains not empty")
            void returnElementWhenPeeked() {
                assertEquals(anElement, stack.peek());
                assertFalse(stack.isEmpty());
            }
        }
    }
}
```



### 6、参数化测试

参数化测试是JUnit5很重要的一个新特性，它使得用不同的参数多次运行测试成为了可能，也为我们的单元测试带来许多便利。

利用@ValueSource等注解，指定入参，我们将可以使用不同的参数进行多次单元测试，而不需要每新增一个参数就新增一个单元测试，省去了很多冗余代码。

- @ValueSource: 为参数化测试指定入参来源，支持八大基础类以及String类型,Class类型

- @NullSource: 表示为参数化测试提供一个null的入参
- @EnumSource: 表示为参数化测试提供一个枚举入参
- @CsvFileSource：表示读取指定CSV文件内容作为参数化测试入参
- @MethodSource：表示读取指定方法的返回值作为参数化测试入参(注意方法返回需要是一个流)

当然如果参数化测试仅仅只能做到指定普通的入参还达不到让我觉得惊艳的地步。让我真正感到他的强大之处的地方在于他可以支持外部的各类入参。如:CSV,YML,JSON 文件甚至方法的返回值也可以作为入参。只需要去实现ArgumentsProvider接口，任何外部文件都可以作为它的入参。

```java
@ParameterizedTest
@ValueSource(strings = {"one", "two", "three"})
@DisplayName("参数化测试1")
public void parameterizedTest1(String string) {
    System.out.println(string);
    Assertions.assertTrue(StringUtils.isNotBlank(string));
}


@ParameterizedTest
@MethodSource("method")    //指定方法名
@DisplayName("方法来源参数")
public void testWithExplicitLocalMethodSource(String name) {
    System.out.println(name);
    Assertions.assertNotNull(name);
}

static Stream<String> method() {
    return Stream.of("apple", "banana");
}
```



### 7、迁移指南

在进行迁移的时候需要注意如下的变化：

- 注解在 org.junit.jupiter.api 包中，断言在 org.junit.jupiter.api.Assertions 类中，前置条件在org.junit.jupiter.api.Assumptions 类中。

- 把@Before 和@After 替换成@BeforeEach 和@AfterEach。
- 把@BeforeClass 和@AfterClass 替换成@BeforeAll 和@AfterAll。
- 把@Ignore 替换成@Disabled。
- 把@Category 替换成@Tag。
- 把@RunWith、@Rule 和@ClassRule 替换成@ExtendWith。



## 5、指标监控

### 1、SpringBoot Actuator

#### 1、简介

未来每一个微服务在云上部署以后，我们都需要对其进行监控、追踪、审计、控制等。SpringBoot就抽取了Actuator场景，使得我们每个微服务快速引用即可获得生产级别的应用监控、审计等功能。



#### 2、1.x与2.x的不同

![image.png](https://pledge99.oss-cn-beijing.aliyuncs.com/img/1606884394162-ac7f2d8e-7abb-44df-9998-fb0f2705f238.png)



#### 3、如何使用

##### 1、引入依赖

```xml
<!--        监控依赖-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
```

##### 2、配置文件打开端口，并暴露为web方式

```yaml
management:
  endpoints:
    enabled-by-default: false  # 关闭所有监控端点
    web:
      exposure:
        include: '*'  # 以web方式暴露所有端点
  endpoint:
    health:
      show-details: always
    # 放止全开有问题，把所有端点全部关闭，然后单独打开需要的端点
    info:
      enabled: true
    beans:
      enabled: true
    threaddump:
      enabled: true
```

##### 3、访问 http://localhost:8080/actuator/**

![image-20220725144054030](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220725144054030.png)

#### 4、测试

http://localhost:8080/actuator/beans
http://localhost:8080/actuator/configprops
http://localhost:8080/actuator/metrics
http://localhost:8080/actuator/metrics/jvm.gc.pause
http://localhost:8080/actuator/指标/指标详细路径

![image-20220725145547526](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220725145547526.png)

#### 5、可视化

官方GitHub网址：https://github.com/codecentric/spring-boot-admin

详细介绍页面：https://codecentric.github.io/spring-boot-admin/2.5.1/#set-up-admin-server

**总流程：**

1、创建一个新的SpringBoot项目，当做服务器，持续运行状态

- 添加server依赖
- 启动类添加`@EnableAdminServer`注解

2、将要监控的项目，当做一个客户端













##### 1、设置 Spring Boot 管理服务器

==就是创建一个项目，作为服务器，保持运行状态，用来检测其他正在运行的项目。==

首先，您需要设置您的服务器。为此，只需设置一个简单的引导项目（使用[start.spring.io](http://start.spring.io/)）。由于 Spring Boot Admin Server 能够作为 servlet 或 webflux 应用程序运行，因此您需要对此做出决定并添加相应的 Spring Boot Starter。在这个例子中，我们使用了 servlet web starter。



为防止端口冲突，可以在配置文件中修改端口

![image-20220725214252236](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220725214252236.png)

**1、将 Spring Boot Admin Server starter 添加到您的依赖项中：**

pom.xml

```xml
<dependency>
    <groupId>de.codecentric</groupId>
    <artifactId>spring-boot-admin-starter-server</artifactId>
    <version>2.5.1</version>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

**2、`@EnableAdminServer`通过添加到您的配置中拉入 Spring Boot Admin Server配置：**

添加这个注解到启动类上

```java
@EnableAdminServer
@SpringBootApplication
public class AdminServiceApplication {

    public static void main(String[] args) {
        SpringApplication.run(AdminServiceApplication.class, args);
    }

}
```



##### 2、Spring Boot 管理客户端

每个想要注册的应用程序都必须包含 Spring Boot Admin Client。为了保护端点，还要添加spring-boot-starter-security.

- 将 spring-boot-admin-starter-client 添加到您的依赖项中：


pom.xml

```xml
<dependency>
    <groupId>de.codecentric</groupId>
    <artifactId>spring-boot-admin-starter-client</artifactId>
    <version>2.5.1</version>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```

- 通过配置 Spring Boot Admin Server 的 URL 来启用 SBA Client：
  - 客户端还有一个instance.prefer-ip属性，改外true后，就把url当做网址来访问，不拆解
  - 因为本地测试时，服务器和客户端地址都一样，就端口号不一样，有时候容易出错

application.properties【yaml文件也一样】

```properties
# 这个url是服务器的url，意思是：把本客户端交给哪个服务器监管
# 要注册的 Spring Boot 管理服务器的 URL。
spring.boot.admin.client.url=http://localhost:8080 


# 打开所有监控端点
# 与 Spring Boot 2 一样，大多数端点默认情况下都不会通过 http 公开，我们会公开所有端点。对于生产，您应该仔细选择要公开的端点。
management.endpoints.web.exposure.include=*  
```

或者

```yaml
spring:  
  boot:
    admin:
      client:
        url: http://localhost:9999
        instance:
          prefer-ip: true    # 不做解析，使用ip注册
  application:      # 设置这个客户端的别名
    name: springboot-05-web-admin
```



3、运行服务器程序，和客户端程序

运行服务器程序：会出现如下界面

![image-20220725214835159](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220725214835159.png)

可以显示有几个被监控的客户端，每个客户端可以查看各项指标，针对需要的信息，添加标签，实现监控操作

![image-20220725214954954](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220725214954954.png)







### 2、Actuator Endpoint

#### 1、最常使用的端点

最常用的Endpoint

- **Health：**监控状况
- **Metrics：**运行时指标
- **Loggers：**日志记录

其余端点：

| ID               | 描述                                                         |
| ---------------- | ------------------------------------------------------------ |
| auditevents      | 暴露当前应用程序的审核事件信息。需要一个AuditEventRepository组件。 |
| beans            | 显示应用程序中所有Spring Bean的完整列表。                    |
| caches           | 暴露可用的缓存。                                             |
| conditions       | 显示自动配置的所有条件信息，包括匹配或不匹配的原因。         |
| configprops      | 显示所有@ConfigurationProperties。                           |
| env              | 暴露Spring的属性ConfigurableEnvironment                      |
| flyway           | 显示已应用的所有Flyway数据库迁移。 需要一个或多个Flyway组件。 |
| health           | 显示应用程序运行状况信息。                                   |
| httptrace        | 显示HTTP跟踪信息（默认情况下，最近100个HTTP请求-响应）。需要一个HttpTraceRepository组件。 |
| info             | 显示应用程序信息。                                           |
| integrationgraph | 显示Spring integrationgraph 。需要依赖spring-integration-core。 |
| loggers          | 显示和修改应用程序中日志的配置。                             |
| liquibase        | 显示已应用的所有Liquibase数据库迁移。需要一个或多个Liquibase组件。 |
| metrics          | 显示当前应用程序的“指标”信息。                               |
| mappings         | 显示所有@RequestMapping路径列表。                            |
| scheduledtasks   | 显示应用程序中的计划任务。                                   |
| sessions         | 允许从Spring Session支持的会话存储中检索和删除用户会话。需要使用Spring Session的基于Servlet的Web应用程序。 |
| shutdown         | 使应用程序正常关闭。默认禁用。                               |
| startup          | 显示由ApplicationStartup收集的启动步骤数据。需要使用SpringApplication进行配置BufferingApplicationStartup。 |
| threaddump       | 执行线程转储。                                               |



如果应用程序是Web应用程序（Spring MVC，Spring WebFlux或Jersey），则可以使用以下附加端点：

| ID         | 描述                                                         |
| ---------- | ------------------------------------------------------------ |
| heapdump   | 返回hprof堆转储文件。                                        |
| jolokia    | 通过HTTP暴露JMX bean（需要引入Jolokia，不适用于WebFlux）。需要引入依赖jolokia-core。 |
| logfile    | 返回日志文件的内容（如果已设置logging.file.name或logging.file.path属性）。支持使用HTTPRange标头来检索部分日志文件的内容。 |
| prometheus | 以Prometheus服务器可以抓取的格式公开指标。需要依赖micrometer-registry-prometheus。 |



#### 2、Health Endpoint

健康检查端点，我们一般用于在云平台，平台会定时的检查应用的健康状况，我们就需要Health Endpoint可以为平台返回当前应用的一系列组件健康状况的集合。

重要的几点：

- health endpoint返回的结果，应该是一系列健康检查后的一个汇总报告
- 很多的健康检查默认已经自动配置好了，比如：数据库、redis等
- 可以很容易的添加自定义的健康检查机制

<img src="https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220725150821028.png" alt="image-20220725150821028" style="zoom:50%;" />

#### 3、Metrics Endpoint

- 提供详细的、层级的、空间指标信息，这些信息可以被pull（主动推送）或者push（被动获取）方式得到；
- 通过Metrics对接多种监控系统
- 简化核心Metrics开发
- 添加自定义Metrics或者扩展已有Metrics

![image-20220725150944300](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220725150944300.png)



#### 4、管理Endpoints

##### 1、开启与禁用Endpoints

- 默认所有的Endpoint除过shutdown都是开启的。
- 需要开启或者禁用某个Endpoint。
  - 配置模式为  management.endpoint.<endpointName>.enabled = true

```yaml
management:
  endpoints:
    enabled-by-default: false  # 关闭所有监控端点
    web:
      exposure:
        include: '*'  # 以web方式暴露所有端点
  endpoint:
    health:
      show-details: always  # 显示详细信息
      enabled: true
    # 放止全开有问题，把所有端点全部关闭，然后单独打开需要的端点
    info:
      enabled: true
    beans:
      enabled: true
    threaddump:
      enabled: true
    metrics:
      enabled: true
```



##### 2、暴露Endpoints

支持的暴露方式

- HTTP：默认只暴露health和info Endpoint
- JMX：默认暴露所有Endpoint
- 除过health和info，剩下的Endpoint都应该进行保护访问。如果引入SpringSecurity，则会默认配置安全访问规则

两种模式默认暴露情况

| ID               | JMX  | Web  |
| ---------------- | ---- | ---- |
| auditevents      | Yes  | No   |
| beans            | Yes  | No   |
| caches           | Yes  | No   |
| conditions       | Yes  | No   |
| configprops      | Yes  | No   |
| env              | Yes  | No   |
| flyway           | Yes  | No   |
| health           | Yes  | Yes  |
| heapdump         | N/A  | No   |
| httptrace        | Yes  | No   |
| info             | Yes  | Yes  |
| integrationgraph | Yes  | No   |
| jolokia          | N/A  | No   |
| logfile          | N/A  | No   |
| loggers          | Yes  | No   |
| liquibase        | Yes  | No   |
| metrics          | Yes  | No   |
| mappings         | Yes  | No   |
| prometheus       | N/A  | No   |
| scheduledtasks   | Yes  | No   |
| sessions         | Yes  | No   |
| shutdown         | Yes  | No   |
| startup          | Yes  | No   |
| threaddump       | Yes  | No   |



### 3、定制 Endpoint

#### 1、定制 Health 信息

<font color="red">注意这个类名，必须是xxxHealthIndicator</font>

目录结构

<img src="https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220725154324226.png" alt="image-20220725154324226" style="zoom:50%;" />

代码

```java
@Component
public class MyComHealthIndicator extends AbstractHealthIndicator {

    /**
     * 真实的检查方法
     * @param builder
     * @throws Exception
     */
    @Override
    protected void doHealthCheck(Health.Builder builder) throws Exception {
        //mongodb。  获取连接进行测试
        Map<String,Object> map = new HashMap<>();
        // 检查完成
        if(1 == 2){
//            builder.up(); //健康
            builder.status(Status.UP);
            map.put("count",1);
            map.put("ms",100);
        }else {
//            builder.down();
            builder.status(Status.OUT_OF_SERVICE);
            map.put("err","连接超时");
            map.put("ms",3000);
        }


        builder.withDetail("code",100)
                .withDetails(map);

    }
}
```



```java
import org.springframework.boot.actuate.health.Health;
import org.springframework.boot.actuate.health.HealthIndicator;
import org.springframework.stereotype.Component;

@Component
public class MyHealthIndicator implements HealthIndicator {

    @Override
    public Health health() {
        int errorCode = check(); // perform some specific health check
        if (errorCode != 0) {
            return Health.down().withDetail("Error Code", errorCode).build();
        }
        return Health.up().build();
    }

}

构建Health
Health build = Health.down()
                .withDetail("msg", "error service")
                .withDetail("code", "500")
                .withException(new RuntimeException())
                .build();
```



![image-20220725152355298](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220725152355298.png)



#### 2、定制info信息

两种方式：

1、编写配置文件【不起作用，不知为啥】

```yaml
info:
  appName: boot-admin
  version: 2.0.1
  mavenProjectName: @project.artifactId@  #使用@@可以获取maven的pom文件值
  mavenProjectVersion: @project.version@
```

2、编写InfoContributor

```java
import java.util.Collections;

import org.springframework.boot.actuate.info.Info;
import org.springframework.boot.actuate.info.InfoContributor;
import org.springframework.stereotype.Component;

@Component
public class ExampleInfoContributor implements InfoContributor {

    @Override
    public void contribute(Info.Builder builder) {
        builder.withDetail("example",
                Collections.singletonMap("key", "value"));
    }
}
```

http://localhost:8080/actuator/info 会输出以上方式返回的所有info信息



#### 3、定制Metrics信息

##### 1、SpringBoot支持自动适配的Metrics

- JVM metrics, report utilization of:
  - Various memory and buffer pools
  - Statistics related to garbage collection
  - Threads utilization
  - Number of classes loaded/unloaded
- CPU metrics
- File descriptor metrics
- Kafka consumer and producer metrics
- Log4j2 metrics: record the number of events logged to Log4j2 at each level
- Logback metrics: record the number of events logged to Logback at each level
- Uptime metrics: report a gauge for uptime and a fixed gauge representing the application’s absolute start time
- Tomcat metrics (server.tomcat.mbeanregistry.enabled must be set to true for all Tomcat metrics to be registered)
- Spring Integration metrics



##### 2、增加定制Metrics



```java
@Component
class MyService{
    Counter counter;
    public MyService(MeterRegistry meterRegistry){
         counter = meterRegistry.counter("myservice.method.running.counter");
    }

    public void hello() {
        counter.increment();
    }
}
```

或者

```java
//也可以使用下面的方式
@Bean
MeterBinder queueSize(Queue queue) {
    return (registry) -> Gauge.builder("queueSize", queue::size).register(registry);
}
```

![image-20220725155831112](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220725155831112.png)

![image-20220725155907783](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220725155907783.png)



#### 4、定制Endpoint



```java
@Component
@Endpoint(id = "container")  // 给端点起个名，也可以在配置文件中修改属性
public class DockerEndpoint {

    @ReadOperation
    public Map getDockerInfo(){
        return Collections.singletonMap("info","docker started...");
    }

    @WriteOperation
    private void restartDocker(){
        System.out.println("docker restarted....");
    }

}
```

![image-20220725160156655](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220725160156655.png)



![image-20220725160235839](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220725160235839.png)

场景：开发ReadinessEndpoint来管理程序是否就绪，或者LivenessEndpoint来管理程序是否存活；
当然，这个也可以直接使用 https://docs.spring.io/spring-boot/docs/current/reference/html/production-ready-features.html#production-ready-kubernetes-probes



## 6、Profile功能

为了方便多环境适配，springboot简化了profile功能。

<font color="red">**大白话：**就是一个项目可能有开发环境、生产环境、测试环境多种环境，不同的测试环境可能会有不同的配置文件需要，于是就有了Profile功能，在最基础的application文件中，配置Profile属性，指出计划使用哪个环境，**但是基础的配置文件内容和目标配置文件都会生效！！**如果存在重名的属性，以目标配置文件为主</font>

关键是这个属性，可以在打成jar包以后修改，命令行修改属性



### 1、application-profile功能

- 默认配置文件  application.yaml；任何时候都会加载

  - 为什么任何时候都会加载，如果不加载，那怎么保证profile属性生效呢？不就成悖论了么
  - ![image-20220726164034488](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220726164034488.png)

- 指定环境配置文件  application-{env}.yaml

  - 命名必须是application-xxx.yaml这种格式，要不然识别不到

  - ```properties
    spring.profiles.active=prod
    ```

- 激活指定环境

  - 配置文件激活【方法如上】
  - 命令行激活：java -jar 包名.jar
  - <img src="https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220726165047630.png" alt="image-20220726165047630" style="zoom:50%;" />
  - 命令行修改属性
    -  --spring.profiles.active=prod  --person.name=haha
    - ![image-20220726165400228](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220726165400228.png)
    - <img src="https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220726165418089.png" alt="image-20220726165418089" style="zoom:50%;" />
  - 修改配置文件的任意值，命令行优先

- 默认配置与环境配置同时生效

- 同名配置项，profile配置优先



### 2、@Profile条件装配功能

**注解@Profile写在类上，或者方法上，可以根据当前配置文件，选择对应的类或者方法**

- ```就是说被@Profile注解的内容，启动或者装配时，是有前提条件的：那就是他注解的环境被启动```

如Person接口，有两个实现类，分别是Worker和Boss。

对他俩进行不同的注解，在自动装配Person时，就会根据配置不同，注入不同的实现类

![image-20220727123311841](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220727123311841.png)

配置文件启动prod环境

```properties
spring.profiles.active=prod   
```

  那么person的name和age就是application-prod.yaml文件的内容

![image-20220727123531443](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220727123531443.png)

同时查看person的getClass方法，会发现也是Boss类



### 3、profile分组

还可以同时启动多个配置文件，内容可以互补

比如:

- prod配置文件提供了
  - person的name=pledge
- prod22配置文件提供了
  - person的age=99

同时启动两个配置文件，就会有一个完整的person

```properties
# 启动我的小组
spring.profiles.active=myGroup

# 给我的配置文件起个名字，myGroup，分组添加配置文件
spring.profiles.group.myGroup[0]=prod
spring.profiles.group.myGroup[1]=prod22
```

![image-20220727124216292](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220727124216292.png)



## 7、外部化配置

https://docs.spring.io/spring-boot/docs/current/reference/html/spring-boot-features.html#boot-features-external-config

**与代码本身分离，抽取出来可以再外部调整的配置，称之为外部配置**

**外部配置可以获取以下14条位置及相关属性信息，并按照1---14先后检查，若有相同属性，则后检查的覆盖之前的。**

1. Default properties (specified by setting SpringApplication.setDefaultProperties).
2. @PropertySource annotations on your @Configuration classes. Please note that such property sources are not added to the Environment until the application context is being refreshed. This is too late to configure certain properties such as logging.* and spring.main.* which are read before refresh begins.
3. Config data (such as application.properties files)
4. A RandomValuePropertySource that has properties only in random.*.
5. OS environment variables.
6. Java System properties (System.getProperties()).
7. JNDI attributes from java:comp/env.
8. ServletContext init parameters.
9. ServletConfig init parameters.
10. Properties from SPRING_APPLICATION_JSON (inline JSON embedded in an environment variable or system property).
11. Command line arguments.
12. properties attribute on your tests. Available on @SpringBootTest and the test annotations for testing a particular slice of your application.
13. @TestPropertySource annotations on your tests.
14. Devtools global settings properties in the $HOME/.config/spring-boot directory when devtools is active.



### 1、外部配置源

常用：Java属性文件、YAML文件、环境变量、命令行参数；

### 2、配置文件查找位置

同样：后检查的会覆盖前面的，属性相同的话

- (1) classpath 根路径
- (2) classpath 根路径下config目录
- (3) jar包当前目录
- (4) jar包当前目录的config目录
- (5) /config子目录的直接子目录

### 3、配置文件加载顺序：

1. 当前jar包内部的application.properties和application.yml
2. 当前jar包内部的application-{profile}.properties 和 application-{profile}.yml
3. 引用的外部jar包的application.properties和application.yml
4. 引用的外部jar包的application-{profile}.properties 和 application-{profile}.yml

### 注意：指定环境优先，外部优先，后面的可以覆盖前面的同名配置项



## 8、自定义starter

### 1、starter启动原理

- starter-pom引入 autoconfigurer 包
- <img src="https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220727171758892.png" alt="image-20220727171758892" style="zoom:50%;" />
- autoconfigure包中配置使用 META-INF/spring.factories 中 EnableAutoConfiguration 的值，使得项目启动加载指定的自动配置类
- 编写自动配置类 xxxAutoConfiguration -> xxxxProperties
  - @Configuration
  - @Conditional
  - @EnableConfigurationProperties
  - @Bean
  - ......

<font color="green">**引入starter --- xxxAutoConfiguration --- 容器中放入组件 ---- 绑定xxxProperties ---- 配置项**</font>



### 2、自定义starter

#### 1、实现需求

假设我有一个starter，，，它有一个HelloService接口，

接口中有一个sayHello方法，只要调用这个方法，传给他一个参数name

他会从配置文件中找到prefix和suffix两个属性值，返回prefix   name   suffix，一套完整操作

<img src="https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220729181814885.png" alt="image-20220729181814885" style="zoom:50%;" />

#### 2、编写自定义starter

##### 1、创建空项目

用来存储starter包和autoconfigurantion两个包

##### 2、创建starter模块

maven项目就行，啥都没有，全删掉就行

**只要在pom中引入自动配置包的依赖就行了**，这个依赖就是模块的名称，到模块的pom文件中复制过来就行了

![image-20220729182802702](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220729182802702.png)

##### 3、创建自动配置模块

- 一个自动注册类，注册业务逻辑，

- 一个业务逻辑，需要属性bean

- 一个bean类

初始化创建SpringBoot项目，只选择Spring-web就行了

<img src="https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220729183016460.png" alt="image-20220729183016460" style="zoom:50%;" />

**HelloService逻辑层**

```java
/**
 * 默认不放到容器中，在HelloServiceAutoConfiguration自动注册的时候，需要，则把HelloServic New一个，然后注册到容器中
 */

public class HelloService {

    @Autowired
    HelloPropertires helloPropertires;

    public String sayHello(String userName){
        return helloPropertires.getPrefix() + ":" + userName + ":" + helloPropertires.getSuffix();
    }
}
```

**HelloPropertires**

bean获取配置文件参数类，获取配置文件中名字为pledge.hello的属性值

```java
@ConfigurationProperties("pledge.hello")   // 从配置文件中取出pledge.hello对应的属性值
public class HelloPropertires {

    private String prefix;
    private String suffix;
  
    public String getPrefix() {
        return prefix;
    }

    public void setPrefix(String prefix) {
        this.prefix = prefix;
    }

    public String getSuffix() {
        return suffix;
    }

    public void setSuffix(String suffix) {
        this.suffix = suffix;
    }


}
```

**HelloServiceAutoConfiguration**注册类，

```java
@Configuration
@EnableConfigurationProperties({HelloPropertires.class}) // 跟配置类进行了绑定，并且还会把HelloPropertires放到容器中
public class HelloServiceAutoConfiguration {

    @ConditionalOnMissingBean({HelloService.class})  // 当容器中没有HelloService时，才会注册到容器中，否则不执行
    @Bean
    public HelloService helloService(){
        return new HelloService();
    }

}
```

**spring.factories**

指定项目启动以后，加载哪些自动配置包；目前就一个，也可能有多个自动配置包，所以要设置是否项目启动就自动注册

![image-20220729183818550](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220729183818550.png)

```protertires
org.springframework.boot.autoconfigure.EnableAutoConfiguration=\
com/pledge/hello/auto/HelloServiceAutoConfiguration
```



#### 3、添加Maven工程

自动装配类添加到Maven

<img src="https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220729184026260.png" alt="image-20220729184026260" style="zoom:50%;" />

Starter类添加到Maven

![image-20220729184056093](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220729184056093.png)

#### 4、引用自定义的starter

到别的项目添加依赖就行了，依赖就是starter类的名称，在他的pom文件中复制出来就行了

![image-20220729184511745](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220729184511745.png)

新建项目，添加依赖

![image-20220729184554242](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220729184554242.png)

编写业务：\hello请求，返回sayHello（）方法

```java
@RestController
public class HelloController {
    
    // 自动装配HelloService
    @Autowired
    HelloService helloService;

    @GetMapping("/hello")
    public String hello(){
        
        // 直接调用方法，方法会完成他的逻辑，去配置文件中找参数
        String s = helloService.sayHello("小单");
        return s;

    }
}
```

配置文件提供参数

```properties
pledge.hello.prefix=start
pledge.hello.suffix=end
```

运行即可！



如果自己也写了一个同名方法，那么引用的starter就不会被调用了，因为写了注解，有就不会注册

容器中没有组件时就才会注册

```java
@ConditionalOnMissingBean({HelloService.class})  // 当容器中没有HelloService时，才会注册到容器中，否则不执行
```

## 9、SpringBoot原理



Spring原理【Spring注解】、SpringMVC原理、自动配置原理、SpringBoot原理

### 1、SpringBoot启动过程

- 创建 SpringApplication
  - 保存一些信息。
  - 判定当前应用的类型。ClassUtils。Servlet
  - bootstrappers：初始启动引导器（List<Bootstrapper>）：去spring.factories文件中找 org.springframework.boot.Bootstrapper
  - 找 ApplicationContextInitializer；去spring.factories找 ApplicationContextInitializer
    - List<ApplicationContextInitializer<?>> initializers
  - 找 ApplicationListener  ；应用监听器。去spring.factories找 ApplicationListener
    - List<ApplicationListener<?>> listeners
- 运行 SpringApplication
  - StopWatch
  - 记录应用的启动时间
  - 创建引导上下文（Context环境）createBootstrapContext()
    - 获取到所有之前的 bootstrappers 挨个执行 intitialize() 来完成对引导启动器上下文环境设置
  - 让当前应用进入headless模式。java.awt.headless
  - 获取所有 RunListener（运行监听器）【为了方便所有Listener进行事件感知】
    - getSpringFactoriesInstances 去spring.factories找 SpringApplicationRunListener. 
  - 遍历 SpringApplicationRunListener 调用 starting 方法；
    - 相当于通知所有感兴趣系统正在启动过程的人，项目正在 starting。
  - 保存命令行参数；ApplicationArguments
  - 准备环境 prepareEnvironment（）;
    - 返回或者创建基础环境信息对象。StandardServletEnvironment
    - 配置环境信息对象。
      - 读取所有的配置源的配置属性值。
    - 绑定环境信息
    - 监听器调用 listener.environmentPrepared()；通知所有的监听器当前环境准备完成
  - 创建IOC容器（createApplicationContext（））
    - 根据项目类型（Servlet）创建容器，
    - 当前会创建 AnnotationConfigServletWebServerApplicationContext
  - 准备ApplicationContext IOC容器的基本信息   prepareContext()
    - 保存环境信息
    - IOC容器的后置处理流程。
    - 应用初始化器；applyInitializers；
      - 遍历所有的 ApplicationContextInitializer 。调用 initialize.。来对ioc容器进行初始化扩展功能
      - 遍历所有的 listener 调用 contextPrepared。EventPublishRunListenr；通知所有的监听器contextPrepared
    - 所有的监听器 调用 contextLoaded。通知所有的监听器 contextLoaded；
  - 刷新IOC容器。refreshContext
    - 创建容器中的所有组件（Spring注解）
  - 容器刷新完成后工作？afterRefresh
  - 所有监听 器 调用 listeners.started(context); 通知所有的监听器 started
  - 调用所有runners；callRunners()
  - 获取容器中的 ApplicationRunner 
    - 获取容器中的  CommandLineRunner
    - 合并所有runner并且按照@Order进行排序
    - 遍历所有的runner。调用 run 方法
  - 如果以上有异常，
    - 调用Listener 的 failed
  - 调用所有监听器的 running 方法  listeners.running(context); 通知所有的监听器 running 
  - running如果有问题。继续通知 failed 。调用所有 Listener 的 failed；通知所有的监听器 failed



```java
public interface Bootstrapper {

	/**
	 * Initialize the given {@link BootstrapRegistry} with any required registrations.
	 * @param registry the registry to initialize
	 */
	void intitialize(BootstrapRegistry registry);

}
```

