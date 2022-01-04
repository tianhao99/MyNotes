# Spring5框架

## 一、**IOC**(概念和原理)

1、什么是 IOC

- ==控制反转==，把对象创建和对象之间的调用过程，交给 Spring 进行管理 

- 使用 IOC 目的：为了耦合度降低

2、IOC 底层原理

- xml 解析、工厂模式、反射

## 二、<span id="jump">IOC创建对象的方式</span>

### 1、使用无参构造器

```xml
<bean id="user" class="com.tianhao.pojo.User">
  
    <!--  无参构造器  属性注入      -->
    <property name="name" value="嬴政"/>

</bean>
```

### 2、使用有参构造器【三种方式】

- 根据形参==索引==注入，有参构造器的形参数组

  ```xml
  <bean id="user" class="com.tianhao.pojo.User">
  
      <!--  通过形参个数，来用索引注入      -->
      <constructor-arg index="0" value="我是通过索引赋的值，我也是嬴政"/>
  
  </bean>
  ```

- 根据形参的==数据类型==注入

  ```xml
  <bean id="user" class="com.tianhao.pojo.User">
  
      <!--  通过形参类型，来注入      【不建议使用，多个同类型怎么办】 -->
      <constructor-arg type="java.lang.String" value="我是通过有参构造器，不同的数据类型传入的参数，我也叫嬴政"/>
  
  </bean>
  ```

- 根据形参==名字==，精准注入

  ```xml
  <bean id="user" class="com.tianhao.pojo.User">
  
      <!-- 通过形参名字   精准赋值 -->
      <constructor-arg name="name" value="我是通过有参构造器，形参名字赋的值，我也叫嬴政"/>
    
  </bean>
  ```

  

### **总结：**

在配置文件被加载的时候，容器中管理的对象就已经调用无参构造器完成了初始化操作



## 三、Spring配置

### 1、别名

配置文件：

```xml
<bean id="user" class="com.tianhao.pojo.User">
    <!--  无参构造器  属性注入      -->
    <property name="name" value="嬴政"/>
</bean>

<!-- 别名，如果添加了别名，除了本名外，别名也可以调用 -->
<alias name="user" alias="userNew"/>
```

调用程序：

```java
public class TestUser {
    public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
				// 使用原名
				// User user = (User)context.getBean("user");
        // 使用别名
        User user = (User)context.getBean("userNew");

        user.show();
    }
}
```

### 2、bean的配置

bean 标签中

- id  =  变量名
- class  =  new 的对象
- property  =  给对象的属性赋值【依赖set方法】
- name  =  也是别名，而且可以起多个，用逗号、分号或空格隔开

```xml
<!--  使用Spring来创建对象，在Spring这些都称为bean

原始创建对象：类型 变量名 = new 类型();
            Hello hello = new Hello();
此处的xml配置文件，就是让这个过程交给Spring
-->

<bean id="hello" class="com.tianhao.pojo.Hello" name="newHello,twoHello">
    <property name="str" value="秦始皇"/>
</bean>
```

### 3、import

一般用于团队开发使用，他可以将多个配置文件，导入合并为一个

团队中每个人负责不同的类，不同类需要注册不同的bean，最后利用import将多人的bean合并为一个总的

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <import resource="beans.xml"/>
    <import resource="beans2.xml"/>
    <import resource="beans3.xml"/>
</beans>
```

![image-20211214172643302](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211214172643302.png)

## 四、DI依赖注入

### 1、构造器注入

见第二章[IOC创建对象的方式](#jump)

### 2、Set方式注入【重点】

依赖注入：Set注入

- 依赖：bean对象的创建依赖于容器
- 注入：bean对象中的所有属性，由容器来注入

环境搭建：

- 复杂类型

  ```java
  public class Address {
      // Feilds
      private String address;
      // Constructors
  
      // Methods
      public String getAddress() {
          return address;
      }
  
      public void setAddress(String address) {
          this.address = address;
      }
  
      @Override
      public String toString() {
          return "Address{" +
                  "address='" + address + '\'' +
                  '}';
      }
  }
  ```

- 真实测试对象

  ```java
  public class Student {
      // Fields
      private String name;
      private Address address;
      private String[] books;
      private List<String> hobbys;
      private Map<String,String> card;
      private Set<String> games;
      private String wife;
      private Properties info;
  ```

- applicationContext.xml

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:util="http://www.springframework.org/schema/util"
         xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/util https://www.springframework.org/schema/util/spring-util.xsd">
  
      <bean id="address" class="com.tianhao.pojo.Address">
          <property name="address" value="咸阳"/>
      </bean>
  
      <bean id="student" class="com.tianhao.pojo.Student">
          <!--  第一种，普通值注入，value  -->
          <property name="name" value="嬴政"/>
        
          <!--  第二种，bean注入，ref引用  -->
          <property name="address" ref="address"/>
        
          <!--  数组注入  -->
          <property name="books">
              <array>
                  <value>西游记</value>
                  <value>红楼梦</value>
                  <value>水浒传</value>
                  <value>三国演义</value>
              </array>
          </property>
        
          <!--  List注入  -->
          <property name="hobbys">
              <list>
                  <value>篮球</value>
                  <value>羽毛球</value>
                  <value>台球</value>
              </list>
          </property>
          <!--  Map注入  -->
          <property name="card">
              <map>
                  <entry key="身份证" value="15042199999"/>
                  <entry key="银行卡" value="12345678"/>
              </map>
          </property>
          <!--  Set注入  -->
          <property name="games">
              <set>
                  <value>英雄联盟</value>
                  <value>刺客信条</value>
              </set>
          </property>
        
          <!--  Null值注入  -->
          <property name="wife">
              <null/>
          </property>
        
          <!--  Properties注入  -->
          <property name="info">
              <props>
                  <prop key="姓名">张无忌</prop>
                  <prop key="妻子">赵敏</prop>
                  <prop key="邮箱">zhaomin@163.com</prop>
              </props>
          </property>
      </bean>
  </beans>
  
  ```

- 测试类

  ```java
  public class TestStu {
      public static void main(String[] args) {
          ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
          Student student = (Student) context.getBean("student");
          
          System.out.println(student);
      }
  }
  ```

  运行结果：![image-20211214204334468](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211214204334468.png)

### 3、拓展方式注入

我们可以使用==p命令空间==和==c命令空间==

**需要导入如下约束：**

```xml
<!-- 调用p命令空间需要在beans标签中添加这个属性 -->
xmlns:p="http://www.springframework.org/schema/p"
<!-- 调用c命令空间需要在beans标签中添加这个属性 -->
xmlns:c="http://www.springframework.org/schema/c"
```

- beans.xml

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns:p="http://www.springframework.org/schema/p"
         xmlns:c="http://www.springframework.org/schema/c"
         xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
  
      <!-- p命名空间注入，可以直接注入 property-->
      <bean id="user" class="com.tianhao.pojo.User" p:name="汉武帝" p:age="19" />
  
      <!-- c命名空间注入，通过构造器注入；constructor-org -->
      <bean id="user2" class="com.tianhao.pojo.User" c:name="汉武帝" c:age="19" />
  </beans>
  ```

- 测试类

  ```java
  @Test
  public void test(){
    ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
    User user = context.getBean("user2",User.class);// 加一个User.class形参，就不用强转了
  
    System.out.println(user);
  }
  ```



### 4、bean的作用域

在Spring中，那些组成应用程序的主体及由Spring IoC容器所管理的对象，被称之为bean。

简单地讲，bean就是由IoC容器初始化、装配及管理的对象 .

![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7K5cyS8ZRTpajtSInicNHbMYfmmAQF8hrnicY49FRXEkR5xkxD5A4H5pVUia3mFhrDdh4gBt183EiaFaQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

几种作用域中，request、session作用域仅在基于web的应用中使用（不必关心你所采用的是什么web应用框架），只能用在基于web的Spring ApplicationContext环境。

#### Singleton

当一个bean的作用域为Singleton，那么Spring IoC容器中只会存在一个共享的bean实例，并且所有对bean的请求，只要id与该bean定义相匹配，则只会返回bean的同一实例。Singleton是单例类型，就是在创建起容器时就同时自动创建了一个bean的对象，不管你是否使用，他都存在了，每次获取到的对象都是同一个对象。注意，Singleton作用域是Spring中的缺省作用域。要在XML中将bean定义成singleton，可以这样配置：

```xml
 <bean id="ServiceImpl" class="cn.csdn.service.ServiceImpl" scope="singleton">
```

测试：

```java
 @Test
 public void test03(){
     ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
     User user = (User) context.getBean("user");
     User user2 = (User) context.getBean("user");
     System.out.println(user==user2);// true
 }
```

#### Prototype

当一个bean的作用域为Prototype，表示一个bean定义对应多个对象实例。==Prototype作用域的bean会导致在每次对该bean请求（将其注入到另一个bean中，或者以程序的方式调用容器的getBean()方法）时都会创建一个新的bean实例==。Prototype是原型类型，它在我们创建容器的时候并没有实例化，而是当我们获取bean的时候才会去创建一个对象，而且我们每次获取到的对象都不是同一个对象。根据经验，对有状态的bean应该使用prototype作用域，而对无状态的bean则应该使用singleton作用域。在XML中将bean定义成prototype，可以这样配置：

```xml
 <bean id="account" class="com.foo.DefaultAccount" scope="prototype"/>  
  或者
 <bean id="account" class="com.foo.DefaultAccount" singleton="false"/>
```

#### Request

当一个bean的作用域为Request，表示在一次HTTP请求中，一个bean定义对应一个实例；即每个HTTP请求都会有各自的bean实例，它们依据某个bean定义创建而成。该作用域仅在基于web的Spring ApplicationContext情形下有效。考虑下面bean定义：

```xml
 <bean id="loginAction" class="cn.csdn.LoginAction" scope="request"/>
```

针对每次HTTP请求，Spring容器会根据loginAction bean的定义创建一个全新的LoginAction bean实例，且该loginAction bean实例仅在当前HTTP request内有效，因此可以根据需要放心的更改所建实例的内部状态，而其他请求中根据loginAction bean定义创建的实例，将不会看到这些特定于某个请求的状态变化。当处理请求结束，request作用域的bean实例将被销毁。

#### Session

当一个bean的作用域为Session，表示在一个HTTP Session中，一个bean定义对应一个实例。该作用域仅在基于web的Spring ApplicationContext情形下有效。考虑下面bean定义：

```xml
 <bean id="userPreferences" class="com.foo.UserPreferences" scope="session"/>
```

针对某个HTTP Session，Spring容器会根据userPreferences bean定义创建一个全新的userPreferences bean实例，且该userPreferences bean仅在当前HTTP Session内有效。与request作用域一样，可以根据需要放心的更改所创建实例的内部状态，而别的HTTP Session中根据userPreferences创建的实例，将不会看到这些特定于某个HTTP Session的状态变化。当HTTP Session最终被废弃的时候，在该HTTP Session作用域内的bean也会被废弃掉。



## 五、自动装配

> 自动装配说明

- 自动装配是使用spring满足bean依赖的一种方法
- spring会在应用上下文中为某个bean寻找其依赖的bean。

Spring中bean有三种装配机制，分别是：

1. 在xml中显式配置；
2. 在java中显式配置；
3. 隐式的bean发现机制和自动装配。



这里我们主要讲第三种：自动化的装配bean。

Spring的自动装配需要从两个角度来实现，或者说是两个操作：

1. 组件扫描(component scanning)：spring会自动发现应用上下文中所创建的bean；
2. 自动装配(autowiring)：spring自动满足bean之间的依赖，也就是我们说的IoC/DI；

组件扫描和自动装配组合发挥巨大威力，使得显示的配置降低到最少。

**推荐不使用自动装配xml配置 , 而使用注解 .**



> 测试环境搭建

1、新建一个项目

2、新建两个实体类，Cat  Dog  都有一个叫的方法

```java
public class Cat {
   public void shout() {
       System.out.println("miao~");
  }
}
public class Dog {
   public void shout() {
       System.out.println("wang~");
  }
}
```

3、新建一个用户类 User

```java
public class User {
   private Cat cat;
   private Dog dog;
   private String str;
}
```

4、编写Spring配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd">

   <bean id="dog" class="com.kuang.pojo.Dog"/>
   <bean id="cat" class="com.kuang.pojo.Cat"/>

   <bean id="user" class="com.kuang.pojo.User">
       <property name="cat" ref="cat"/>
       <property name="dog" ref="dog"/>
       <property name="str" value="qinjiang"/>
   </bean>
</beans>
```

5、测试

```java
public class MyTest {
   @Test
   public void testMethodAutowire() {
       ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
       User user = (User) context.getBean("user");
       user.getCat().shout();
       user.getDog().shout();
  }
}
```

结果正常输出，环境OK



### byName

**autowire byName (按名称自动装配)**

由于在手动配置xml过程中，常常发生字母缺漏和大小写等错误，而无法对其进行检查，使得开发效率降低。

采用自动装配将避免这些错误，并且使配置简单化。

测试：

1、修改bean配置，增加一个属性  autowire="byName"

```xml
<bean id="dog" class="com.kuang.pojo.Dog"/>
<bean id="cat" class="com.kuang.pojo.Cat"/>

<bean id="user" class="com.kuang.pojo.User" autowire="byName">
   <!-- 
   这User类的，cat和dog属性，就不注入值了，让他自动装配
   但是！！！上边cat和dog类的bean 的id名必须和类名一致
   <property name="cat" ref="cat"/>
   <property name="dog" ref="dog"/>
   -->
   <property name="str" value="qinjiang"/>
</bean>
```

2、再次测试，结果依旧成功输出！

3、<font color="red">我们将 cat 的bean id修改为 catXXX</font>

4、<font color="red">再次测试， 执行时报空指针java.lang.NullPointerException。</font>因为按byName规则找不对应set方法，真正的setCat就没执行，对象就没有初始化，所以调用时就会报空指针错误。

**小结：**

当一个bean节点带有 autowire byName的属性时。

1. 将查找其类中所有的set方法名，例如setCat，获得将set去掉并且首字母小写的字符串，即cat。

2. 去spring容器中寻找是否有此字符串名称id的对象。

3. 如果有，就取出注入；如果没有，就报空指针异常。

   

### byType

**autowire byType (按类型自动装配)**

使用autowire byType首先需要保证：同一类型的对象，在spring容器中唯一。如果不唯一，会报不唯一的异常。

```java
NoUniqueBeanDefinitionException
```

测试：

1、将user的bean配置修改一下 ： autowire="byType"

2、测试，正常输出

3、在注册一个cat 的bean对象！

```xml
<bean id="dog" class="com.kuang.pojo.Dog"/>
<bean id="cat" class="com.kuang.pojo.Cat"/>
<bean id="cat2" class="com.kuang.pojo.Cat"/><!--根据这个包地址，但是只能有一个，两个就报错了-->

<bean id="user" class="com.kuang.pojo.User" autowire="byType">
   <property name="str" value="qinjiang"/>
</bean>
```

4、测试，报错：NoUniqueBeanDefinitionException

5、删掉cat2，将cat的bean名称改掉！测试！因为是按类型装配，所以并不会报异常，也不影响最后的结果。甚至将id属性去掉，也不影响结果。

这就是按照类型自动装配！

### 使用注解

jdk1.5开始支持注解，spring2.5开始全面支持注解。

准备工作：利用注解的方式注入属性。



1、在spring配置文件中引入context文件头

```xml
xmlns:context="http://www.springframework.org/schema/context"
http://www.springframework.org/schema/context
http://www.springframework.org/schema/context/spring-context.xsd
```

2、开启属性注解支持！

```xml
<context:annotation-config/>
```

#### @Autowired

- @Autowired是按类型自动转配的，不支持id匹配。
- 需要导入 spring-aop的包！

测试：

1、将User类中的set方法去掉，使用@Autowired注解

```java
public class User {
   @Autowired
   private Cat cat;
   @Autowired
   private Dog dog;
   private String str;

   public Cat getCat() {
       return cat;
  }
   public Dog getDog() {
       return dog;
  }
   public String getStr() {
       return str;
  }
}
```

2、此时配置文件内容

```xml
<context:annotation-config/>

<bean id="dog" class="com.kuang.pojo.Dog"/>
<bean id="cat" class="com.kuang.pojo.Cat"/>
<bean id="user" class="com.kuang.pojo.User"/>
```

3、测试，成功输出结果！



==@Autowired(required=false)  说明：false，对象可以为null；true，对象必须存对象，不能为null。==

```java
//如果允许对象为null，设置required = false,默认为true
@Autowired(required = false)
private Cat cat;
```

#### @Qualifier

- @Autowired是根据类型自动装配的，加上@Qualifier则可以根据byName的方式自动装配
- @Qualifier不能单独使用。

测试实验步骤：

1、配置文件修改内容，保证类型存在对象。且名字不为类的默认名字！

```xml
<bean id="dog1" class="com.kuang.pojo.Dog"/>
<bean id="dog2" class="com.kuang.pojo.Dog"/>
<bean id="cat1" class="com.kuang.pojo.Cat"/>
<bean id="cat2" class="com.kuang.pojo.Cat"/>
```

2、没有加Qualifier测试，直接报错

3、在属性上添加Qualifier注解

```java
@Autowired
@Qualifier(value = "cat2")
private Cat cat;
@Autowired
@Qualifier(value = "dog2")
private Dog dog;
```

测试，成功输出！

#### @Resource

- @Resource如有指定的name属性，先按该属性进行byName方式查找装配；
- 其次再进行默认的byName方式进行装配；
- 如果以上都不成功，则按byType的方式自动装配。
- 都不成功，则报异常。

实体类：

```java
public class User {
   //如果允许对象为null，设置required = false,默认为true
   @Resource(name = "cat2")
   private Cat cat;
   @Resource
   private Dog dog;
   private String str;
}
```

beans.xml

```xml
<bean id="dog" class="com.kuang.pojo.Dog"/>
<bean id="cat1" class="com.kuang.pojo.Cat"/>
<bean id="cat2" class="com.kuang.pojo.Cat"/>

<bean id="user" class="com.kuang.pojo.User"/>
```

测试：结果OK

配置文件2：beans.xml ， 删掉cat2

```xml
<bean id="dog" class="com.kuang.pojo.Dog"/>
<bean id="cat1" class="com.kuang.pojo.Cat"/>
```

实体类上只保留注解

```java
@Resource
private Cat cat;
@Resource
private Dog dog;
```

结果：OK

结论：先进行byName查找，失败；再进行byType查找，成功。

### 小结

==@Autowired与@Resource异同：==

1、@Autowired与@Resource都可以用来装配bean。都可以写在字段上，或写在setter方法上。

2、@Autowired默认按类型装配（属于spring规范），默认情况下必须要求依赖对象必须存在，如果要允许null 值，可以设置它的required属性为false

- 如：@Autowired(required=false) ，如果我们想使用名称装配可以结合@Qualifier注解进行使用

3、@Resource（属于J2EE复返），默认按照名称进行装配，名称可以通过name属性进行指定。如果没有指定name属性，当注解写在字段上时，默认取字段名进行按照名称查找，如果注解写在setter方法上默认取属性名进行装配。当找不到与名称匹配的bean时才按照类型进行装配。但是需要注意的是，如果name属性一旦指定，就只会按照名称进行装配。

它们的作用相同都是用注解方式注入对象，但执行顺序不同。@Autowired先byType，@Resource先byName。



## 六、使用注解开发

### 1、说明

在spring4之后，想要使用注解形式，必须得要引入aop的包

![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7IzypAUHDfDEujP4ry6cHxWTvAS6qRS0qrmMCic3QqF9icGNcPj8IZwNo3R9VEgpAgWHrStBN1ya6Tg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

在配置文件当中，还得要引入一个context约束

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xmlns:context="http://www.springframework.org/schema/context"
      xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/context
       http://www.springframework.org/schema/context/spring-context.xsd">
<context:annotation-config/>
</beans>
```



### 2、Bean的实现

我们之前都是使用 bean 的标签进行bean注入，但是实际开发中，我们一般都会使用注解！

1、配置扫描哪些包下的注解

```xml
<!--指定注解扫描包-->
<context:component-scan base-package="com.tianhao.pojo"/>
```

2、在指定包下编写类，增加注解

```java
@Component("user")
// 相当于配置文件中 <bean id="user" class="当前注解的类"/>
public class User {
   public String name = "秦始皇";
}
```

3、测试

```java
@Test
public void test(){
   ApplicationContext applicationContext =
       new ClassPathXmlApplicationContext("applicationContext.xml");
   User user = (User) applicationContext.getBean("user");
   System.out.println(user.name);
}
```



### 3、属性注入

使用注解注入属性

1、可以不用提供set方法，直接在直接名上添加@value("值")

```java
@Component("user")
// 相当于配置文件中 <bean id="user" class="当前注解的类"/>
public class User {
   @Value("秦疆")
   // 相当于配置文件中 <property name="name" value="秦疆"/>
   public String name;
}
```

2、如果提供了set方法，在set方法上添加@value("值");

```java
@Component("user")
public class User {

   public String name;

   @Value("秦疆")
   public void setName(String name) {
       this.name = name;
  }
}
```



### 4、衍生注解

我们这些注解，就是替代了在配置文件当中配置步骤而已！更加的方便快捷！

**@Component三个衍生注解**

为了更好的进行分层，Spring可以使用其它三个注解，==功能一样==，目前使用哪一个功能都一样。

- ==@Component==：组件，放在类名之上，表示该类被Spring管理了，就是bean

- ==@Controller==：web层
- ==@Service==：service层
- ==@Repository==：dao层

写上这些注解，就相当于将这个类交给Spring管理装配了！【记得把扫描的配置放大，能包住所写注解的包】

```xml
<!--指定注解扫描包-->
<context:component-scan base-package="com.tianhao.pojo"/>
放大！！！！如下
<context:component-scan base-package="com.tianhao"/>
```

### 5、自动装配注解

- @Autowired：自动装配，先类型，后名字
  - @Qualifier(value="xxx")：当@Autowired不能唯一自动装配上属性时，用此注解。
- @Nullable：字段标记了这个注解之后，说明这个字段可以为null
- @Resource：自动装备先名字，后类型

### 6、作用域

==@Scope==

- singleton：默认的，Spring会采用单例模式创建这个对象。关闭工厂 ，所有的对象都会销毁。
- prototype：多例模式。关闭工厂 ，所有的对象不会销毁。内部的垃圾回收机制会回收

```java
@Controller("user")
@Scope("prototype")
public class User {
   @Value("秦疆")
   public String name;
}
```



### 7、小结

**XML与注解比较**

- XML可以适用任何场景 ，结构清晰，维护方便
- 注解不是自己提供的类使用不了，开发简单方便

**xml与注解整合开发** ：推荐最佳实践

- xml管理Bean
- 注解完成属性注入
- 使用过程中， 可以不用扫描，扫描是为了类上的注解生效

```xml
<context:annotation-config/>  
<!--指定注解扫描包， 也可以不扫描，  但是类上有自己写的注解，就必须扫描-->
<context:component-scan base-package="com.tianhao"/>
```

**作用：**

- 进行注解驱动注册，从而使注解生效

- 用于激活那些已经在spring容器里注册过的bean上面的注解，也就是显示的向Spring注册

- 如果不扫描包，就需要手动配置bean

- 如果不加注解驱动，则注入的值为null！

  

### 8、基于Java类进行配置

JavaConfig 原来是 Spring 的一个子项目，它通过 Java 类的方式提供 Bean 的定义信息，

在 Spring4 的版本， JavaConfig 已正式成为 Spring4 的核心功能 。

测试：

1、编写一个实体类，Dog

```java
@Component  //将这个类标注为Spring的一个组件，放到容器中！
public class Dog {
   public String name = "dog";
}
```

2、新建一个config配置包，编写一个MyConfig配置类

```java
@Configuration  //代表这是一个配置类
public class MyConfig {

   @Bean //通过方法注册一个bean，这里的返回值就Bean的类型，方法名就是bean的id！
   public Dog dog(){
       return new Dog();
  }

}
```

3、测试

```java
@Test
public void test2(){
   ApplicationContext applicationContext =
           new AnnotationConfigApplicationContext(MyConfig.class);
   Dog dog = (Dog) applicationContext.getBean("dog");
   System.out.println(dog.name);
}
```

4、成功输出结果！

**导入其他配置如何做呢？**

1、我们再编写一个配置类！

```java
@Configuration  //代表这是一个配置类
public class MyConfig2 {
}
```

2、在之前的配置类中我们来选择导入这个配置类

```java
@Configuration
@Import(MyConfig2.class)  //导入合并其他配置类，类似于配置文件中的 inculde 标签
public class MyConfig {

   @Bean
   public Dog dog(){
       return new Dog();
  }

}
```

关于这种Java类的配置方式，我们在之后的SpringBoot 和 SpringCloud中还会大量看到，我们需要知道这些注解的作用即可！

## 七、AOP

### 1、什么是AOP

AOP（Aspect Oriented Programming）意为：面向切面编程，通过预编译方式和运行期动态代理实现程序功能的统一维护的一种技术。

AOP是OOP的延续，是软件开发中的一个热点，也是Spring框架中的一个重要内容，是函数式编程的一种衍生范型。利用AOP可以对业务逻辑的各个部分进行隔离，从而使得业务逻辑各部分之间的耦合度降低，提高程序的可重用性，同时提高了开发的效率。



![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7JAeTYOaaH6rZ6WmLLgwQLHf5pmH30gj6mZm81PC7iauicFu55sicJtspU7K3vTCVdZCDTSHq7D5XHlw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

### 2、Aop在Spring中的作用

提供声明式事务；允许用户自定义切面

以下名词需要了解下：

- 横切关注点：跨越应用程序多个模块的方法或功能。即是，与我们业务逻辑无关的，但是我们需要关注的部分，就是横切关注点。如日志 , 安全 , 缓存 , 事务等等 ....
- 切面（ASPECT）：横切关注点 被模块化 的特殊对象。即，它是一个类。
- 通知（Advice）：切面必须要完成的工作。即，它是类中的一个方法。
- 目标（Target）：被通知对象。
- 代理（Proxy）：向目标对象应用通知之后创建的对象。
- 切入点（PointCut）：切面通知 执行的 “地点”的定义。
- 连接点（JointPoint）：与切入点匹配的执行点。



![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7JAeTYOaaH6rZ6WmLLgwQLHVOZ1JpRb7ViaprZCRXsUbH0bZpibiaTjqib68LQHOWZicSvuU8Y1dquUVGw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

SpringAOP中，通过Advice定义横切逻辑，Spring中支持5种类型的Advice:



![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7JAeTYOaaH6rZ6WmLLgwQLHbAWH8haUQeJ0LVBxxX0icC5TZlBkEBGibibey7jFrCbibPzQcRhkNFcGAA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

即 Aop 在 不改变原有代码的情况下 , 去增加新的功能 .



### 3、使用Spring实现Aop

【重点】使用AOP织入，需要导入一个依赖包！

```xml
<!-- https://mvnrepository.com/artifact/org.aspectj/aspectjweaver -->
<dependency>
   <groupId>org.aspectj</groupId>
   <artifactId>aspectjweaver</artifactId>
   <version>1.9.4</version>
</dependency>
```

#### 一：通过 Spring API 实现

首先编写我们的业务接口和实现类

```java
public interface UserService {

   public void add();

   public void delete();

   public void update();

   public void search();

}
public class UserServiceImpl implements UserService{

   @Override
   public void add() {
       System.out.println("增加用户");
  }

   @Override
   public void delete() {
       System.out.println("删除用户");
  }

   @Override
   public void update() {
       System.out.println("更新用户");
  }

   @Override
   public void search() {
       System.out.println("查询用户");
  }
}
```

然后去写我们的增强类 , 我们编写两个 , 一个前置增强 一个后置增强

```java
public class Log implements MethodBeforeAdvice {
		 /**
     *
     * @param method ：要执行的目标对象的方法
     * @param args ：参数数组
     * @param target ：目标对象
     * @throws Throwable
     */
    @Override
    public void before(Method method, Object[] args, Object target) throws Throwable {
        System.out.println(target.getClass().getName() + "类的" + method.getName() + "方法被执行了");
    }
}
public class AfterLog implements AfterReturningAdvice {
    /**
     *
     * @param returnValue ：多了一个返回值【相比于MethodBeforeAdvice】
     * @param method
     * @param args
     * @param target
     * @throws Throwable
     */
    @Override
    public void afterReturning(Object returnValue, Method method, Object[] args, Object target) throws Throwable {
        System.out.println("执行了" + method.getName() + "方法，返回结果是" + returnValue);
    }
}
```

最后去spring的文件中注册 , 并实现aop切入实现 , 注意导入约束 .

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xmlns:aop="http://www.springframework.org/schema/aop"
      xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/aop
       http://www.springframework.org/schema/aop/spring-aop.xsd">

   <!--注册bean-->
   <bean id="userService" class="com.kuang.service.UserServiceImpl"/>
   <bean id="log" class="com.kuang.log.Log"/>
   <bean id="afterLog" class="com.kuang.log.AfterLog"/>

   <!--aop的配置-->
   <aop:config>
       <!--切入点 expression:表达式匹配要执行的方法-->
       <aop:pointcut id="pointcut" expression="execution(* com.kuang.service.UserServiceImpl.*(..))"/>
       <!--执行环绕; advice-ref执行方法 . pointcut-ref切入点-->
       <aop:advisor advice-ref="log" pointcut-ref="pointcut"/>
       <aop:advisor advice-ref="afterLog" pointcut-ref="pointcut"/>
   </aop:config>

</beans>
```

测试

```java
public class MyTest {
   @Test
   public void test(){
       ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
       UserService userService = (UserService) context.getBean("userService");
       userService.add();
  }
}
```

Aop的重要性 : 很重要 . 一定要理解其中的思路 , 主要是思想的理解这一块 .

Spring的Aop就是将公共的业务 (日志 , 安全等) 和领域业务结合起来 , 当执行领域业务时 , 将会把公共业务加进来 . 实现公共业务的重复利用 . 领域业务更纯粹 , 程序猿专注领域业务 , 其本质还是动态代理 . 



#### 二：自定义类来实现Aop

目标业务类不变依旧是userServiceImpl

第一步 : 写我们自己的一个切入类

```java
public class DiyPointcut {

   public void before(){
       System.out.println("---------方法执行前---------");
  }
   public void after(){
       System.out.println("---------方法执行后---------");
  }
   
}
```

去spring中配置

```xml
<!--第二种方式自定义实现-->
<!--注册bean-->
<bean id="diyPointCut" class="com.tianhao.diy.DiyPointCut"/>

<!--AOP配置-->
<aop:config>
  <!--自定义切面位置 ,ref表示要引用的类【用上边bean标签中的id】-->
  <aop:aspect ref="diyPointCut">
    <!--切入点-->
    <aop:pointcut id="point" expression="execution(* com.tianhao.service.UserServiceImpl.*(..))"/>
    <!--通知 具体在哪里执行，方法前后等-->
    <aop:before method="myBefore" pointcut-ref="point"/>
    <aop:after method="myAfter" pointcut-ref="point"/>
  </aop:aspect>
</aop:config>
```

测试：

```java
public class MyTest {
   @Test
   public void test(){
       ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
       UserService userService = (UserService) context.getBean("userService");
       userService.add();
  }
}
```



**第三种方式**

**使用注解实现**

第一步：编写一个注解实现的增强类

```java
@Aspect //这个注解标注后，表示这个类是一个切面
public class AnnocationPointCut {
  
    @Before("execution(* com.tianhao.service.UserServiceImpl.*(..))")
    public void myBefore(){
        System.out.println("=======方法执行====前=====");
    }
  
    @After("execution(* com.tianhao.service.UserServiceImpl.*(..))")
    public void myAfter(){
        System.out.println("=======方法执行====后=====");
    }
  
    @Around("execution(* com.tianhao.service.UserServiceImpl.*(..))")
    public void myAround(ProceedingJoinPoint jp) throws Throwable{
        /**
         * 这个方法就是：
         *     能够控制目标方法的开始时间
         *     通过控制开始开关，在前后输入代码，形成环绕效果
         *     还能读取目标方法的数据
         */

        System.out.println("环绕前");
        Signature signature = jp.getSignature();// 获取目标方法的签名
        System.out.println("签名：" + signature);
        // 执行方法
        Object proceed = jp.proceed();// 有返回值就接收一下，无值不接受也行

        System.out.println("环绕后");

    }
}

```

第二步：在Spring配置文件中，注册bean，并增加支持注解的配置

```xml
<!-- 方式三：使用注解-->
<bean id="annotionPointCut" class="com.tianhao.diy.AnnocationPointCut"/>
<!--开启注解支持-->
<aop:aspectj-autoproxy/>
```

aop:aspectj-autoproxy：说明

```xml
通过aop命名空间的<aop:aspectj-autoproxy />声明自动为spring容器中那些配置@aspectJ切面的bean创建代理，织入切面。当然，spring 在内部依旧采用AnnotationAwareAspectJAutoProxyCreator进行自动代理的创建工作，但具体实现的细节已经被<aop:aspectj-autoproxy />隐藏起来了

<aop:aspectj-autoproxy />有一个proxy-target-class属性，默认为false，表示使用jdk动态代理织入增强，当配为<aop:aspectj-autoproxy  poxy-target-class="true"/>时，表示使用CGLib动态代理技术织入增强。不过即使proxy-target-class设置为false，如果目标类没有声明接口，则spring将自动使用CGLib动态代理。
```

## 八、声明式事务

声明式事务

### 1、回顾事务

- 事务在项目开发过程非常重要，涉及到数据的一致性的问题，不容马虎！
- 事务管理是企业级应用程序开发中必备技术，用来确保数据的完整性和一致性。

事务就是把一系列的动作当成一个独立的工作单元，这些动作要么全部完成，要么全部不起作用。

**事务四个属性ACID**

1. ==原子性（atomicity）==

2. - 事务是原子性操作，由一系列动作组成，事务的原子性确保动作要么全部完成，要么完全不起作用

3. ==一致性（consistency）==

4. - 一旦所有事务动作完成，事务就要被提交。数据和资源处于一种满足业务规则的一致性状态中

5. ==隔离性（isolation）==

6. - 可能多个事务会同时处理相同的数据，因此每个事务都应该与其他事务隔离开来，防止数据损坏

7. ==持久性（durability）==

   - 事务一旦完成，无论系统发生什么错误，结果都不会受到影响。通常情况下，事务的结果被写到持久化存储器中

### 2、测试

将上面的代码拷贝到一个新项目中

在之前的案例中，我们给userDao接口新增两个方法，删除和增加用户；

```java
//添加一个用户
int addUser(User user);

//根据id删除用户
int deleteUser(int id);
```

mapper文件，我们故意把 deletes 写错，测试！

```xml
<insert id="addUser" parameterType="com.kuang.pojo.User">
insert into user (id,name,pwd) values (#{id},#{name},#{pwd})
</insert>

<delete id="deleteUser" parameterType="int">
deletes from user where id = #{id}
</delete>
```

编写接口的实现类，在实现类中，我们去操作一波

```java
public class UserDaoImpl extends SqlSessionDaoSupport implements UserMapper {

   //增加一些操作
   public List<User> selectUser() {
       User user = new User(4,"小明","123456");
       UserMapper mapper = getSqlSession().getMapper(UserMapper.class);
       mapper.addUser(user);
       mapper.deleteUser(4);
       return mapper.selectUser();
  }

   //新增
   public int addUser(User user) {
       UserMapper mapper = getSqlSession().getMapper(UserMapper.class);
       return mapper.addUser(user);
  }
   //删除
   public int deleteUser(int id) {
       UserMapper mapper = getSqlSession().getMapper(UserMapper.class);
       return mapper.deleteUser(id);
  }

}
```

测试

```java
@Test
public void test2(){
   ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
   UserMapper mapper = (UserMapper) context.getBean("userDao");
   List<User> user = mapper.selectUser();
   System.out.println(user);
}
```

报错：sql异常，delete写错了

结果 ：插入成功！

没有进行事务的管理；我们想让他们都成功才成功，有一个失败，就都失败，我们就应该需要**事务！**

以前我们都需要自己手动管理事务，十分麻烦！

但是Spring给我们提供了事务管理，我们只需要配置即可；



### 3、Spring中的事务管理

Spring在不同的事务管理API之上定义了一个抽象层，使得开发人员不必了解底层的事务管理API就可以使用Spring的事务管理机制。Spring支持编程式事务管理和声明式的事务管理。

#### **编程式事务管理**

- 将事务管理代码嵌到业务方法中来控制事务的提交和回滚
- 缺点：必须在每个事务操作业务逻辑中包含额外的事务管理代码

#### **声明式事务管理**

- 一般情况下比编程式事务好用。
- 将事务管理代码从业务方法中分离出来，以声明的方式来实现事务管理。
- 将事务管理作为横切关注点，通过aop方法模块化。Spring中通过Spring AOP框架支持声明式事务管理。

**使用Spring管理事务，注意头文件的约束导入 : tx**

```xml
xmlns:tx="http://www.springframework.org/schema/tx"

http://www.springframework.org/schema/tx
http://www.springframework.org/schema/tx/spring-tx.xsd">
```

**事务管理器**

- 无论使用Spring的哪种事务管理策略（编程式或者声明式）事务管理器都是必须的。
- 就是 Spring的核心事务管理抽象，管理封装了一组独立于技术的方法。

**JDBC事务**

```xml
<bean id="transactionManager"class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
       <property name="dataSource" ref="dataSource" />
</bean>
```

**配置好事务管理器后我们需要去配置事务的通知**

```xml
<!--配置事务通知-->
<tx:advice id="txAdvice" transaction-manager="transactionManager">
   <tx:attributes>
       <!--配置哪些方法使用什么样的事务,配置事务的传播特性-->
       <tx:method name="add" propagation="REQUIRED"/>
       <tx:method name="delete" propagation="REQUIRED"/>
       <tx:method name="update" propagation="REQUIRED"/>
       <tx:method name="search*" propagation="REQUIRED"/>
       <tx:method name="get" read-only="true"/>
       <tx:method name="*" propagation="REQUIRED"/>
   </tx:attributes>
</tx:advice>
```

#### **spring事务传播特性：**

事务传播行为就是多个事务方法相互调用时，事务如何在这些方法间传播。spring支持7种事务传播行为：

- propagation_requierd：如果当前没有事务，就新建一个事务，如果已存在一个事务中，加入到这个事务中，这是最常见的选择。
- propagation_supports：支持当前事务，如果没有当前事务，就以非事务方法执行。
- propagation_mandatory：使用当前事务，如果没有当前事务，就抛出异常。
- propagation_required_new：新建事务，如果当前存在事务，把当前事务挂起。
- propagation_not_supported：以非事务方式执行操作，如果当前存在事务，就把当前事务挂起。
- propagation_never：以非事务方式执行操作，如果当前事务存在则抛出异常。
- propagation_nested：如果当前存在事务，则在嵌套事务内执行。如果当前没有事务，则执行与propagation_required类似的操作

**Spring 默认的事务传播行为是 PROPAGATION_REQUIRED，它适合于绝大多数的情况。**

假设 ServiveX#methodX() 都工作在事务环境下（即都被 Spring 事务增强了），假设程序中存在如下的调用链：Service1#method1()->Service2#method2()->Service3#method3()，那么这 3 个服务类的 3 个方法通过 Spring 的事务传播机制都工作在同一个事务中。

就好比，我们刚才的几个方法存在调用，所以会被放在一组事务当中！

**配置AOP**

导入aop的头文件！

```xml
<!--配置aop织入事务-->
<aop:config>
   <aop:pointcut id="txPointcut" expression="execution(* com.kuang.dao.*.*(..))"/>
   <aop:advisor advice-ref="txAdvice" pointcut-ref="txPointcut"/>
</aop:config>
```

**进行测试**

删掉刚才插入的数据，再次测试！

```java
@Test
public void test2(){
   ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
   UserMapper mapper = (UserMapper) context.getBean("userDao");
   List<User> user = mapper.selectUser();
   System.out.println(user);
}
```

> 思考问题？

为什么需要配置事务？

- 如果不配置，就需要我们手动提交控制事务；
- 事务在项目开发过程非常重要，涉及到数据的一致性的问题，不容马虎！
