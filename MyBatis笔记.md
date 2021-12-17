# MyBatis

## 1. 简介

- MyBatis 是一款优秀的**持久层框架**
- MyBatis 避免了几乎所有的 JDBC 代码和手动设置参数以及获取结果集的过程
- MyBatis 可以使用简单的 XML 或注解来配置和映射原生信息，将接口和 Java 的 实体类 【Plain Old Java Objects,普通的 Java对象】映射成数据库中的记录。
- MyBatis 本是apache的一个开源项目ibatis, 2010年这个项目由apache 迁移到了google code，并且改名为MyBatis
- 2013年11月迁移到**Github** .
- Mybatis官方文档 : http://www.mybatis.org/mybatis-3/zh/index.html
- GitHub : https://github.com/mybatis/mybatis-3

### 1.1 持久化

**持久化是将程序数据在持久状态和瞬时状态间转换的机制。**

- 即把数据（如内存中的对象）保存到可永久保存的存储设备中（如磁盘）。持久化的主要应用是将内存中的对象存储在数据库中，或者存储在磁盘文件中、XML数据文件中等等。
- JDBC就是一种持久化机制。文件IO也是一种持久化机制。
- 在生活中 : 将鲜肉冷藏，吃的时候再解冻的方法也是。将水果做成罐头的方法也是。

**为什么需要持久化服务呢？那是由于内存本身的缺陷引起的**

- ==内存断电后数据会丢失==，但有一些对象是无论如何都不能丢失的，比如银行账号等，遗憾的是，人们还无法保证内存永不掉电。
- 内存过于昂贵，与硬盘、光盘等外存相比，内存的价格要高2~3个数量级，而且维持成本也高，至少需要一直供电吧。所以即使对象不需要永久保存，也会因为内存的容量限制不能一直呆在内存中，需要持久化来缓存到外存。

### 1.2 持久层

**什么是持久层？**

- 完成持久化工作的代码块 .  ---->  dao层 【DAO (Data Access Object)  数据访问对象】
- 大多数情况下特别是企业级应用，数据持久化往往也就意味着将内存中的数据保存到磁盘上加以固化，而持久化的实现过程则大多通过各种**关系数据库**来完成。
- 不过这里有一个字需要特别强调，也就是所谓的“层”。对于应用系统而言，数据持久功能大多是必不可少的组成部分。也就是说，我们的系统中，已经天然的具备了“持久层”概念？也许是，但也许实际情况并非如此。之所以要独立出一个“持久层”的概念,而不是“持久模块”，“持久单元”，也就意味着，我们的系统架构中，应该有一个相对独立的逻辑层面，专注于数据持久化逻辑的实现.
- 与系统其他部分相对而言，这个层面应该具有一个较为清晰和严格的逻辑边界。【说白了就是用来操作数据库存在的！】

### 1.3 为什么需要Mybatis

- Mybatis就是帮助程序猿将数据存入数据库中 , 和从数据库中取数据 .

- 传统的jdbc操作 , 有很多重复代码块 .比如 : 数据取出时的封装 , 数据库的建立连接等等... , 通过框架可以减少重复代码,提高开发效率 .

- MyBatis 是一个半自动化的**ORM框架 (Object Relationship Mapping) -->对象关系映射**

- 所有的事情，不用Mybatis依旧可以做到，只是用了它，所有实现会更加简单！**技术没有高低之分，只有使用这个技术的人有高低之别**

- MyBatis的优点

- - 简单易学：本身就很小且简单。没有任何第三方依赖，最简单安装只要两个jar文件+配置几个sql映射文件就可以了，易于学习，易于使用，通过文档和源代码，可以比较完全的掌握它的设计思路和实现。
  - 灵活：mybatis不会对应用程序或者数据库的现有设计强加任何影响。sql写在xml里，便于统一管理和优化。通过sql语句可以满足操作数据库的所有需求。
  - 解除sql与程序代码的耦合：通过提供DAO层，将业务逻辑和数据访问逻辑分离，使系统的设计更清晰，更易维护，更易单元测试。sql和代码的分离，提高了可维护性。
  - 提供xml标签，支持编写动态sql。
  - .......

- 最重要的一点，使用的人多！公司需要！

## 2.第一个MyBatis程序

思路：搭建环境----导入MyBatis----编写代码----测试

### 2.1 搭建环境

#### 1、创建数据库

```mysql
create database `mybatis`;

use `mybatis`;

create table `user`(
		`id` int(20) not null primary key,
		`name` varchar(30) default null,
		`pwd` varchar(30) default null
)engine=INNODB default charset=utf8;

insert into `user`(`id`,`name`,`pwd`)values
(1,'张无忌','zhaomin'),
(2,'张三丰','guoxiang'),
(3,'杨过','xiaolongnv')

select * from `user`;
```

#### 2、新建项目

1、新建一个普通的Maven项目

2、删除src【所有子项目通过木块来实现，这个就单纯是个父项目，不用具体代码，所以删了src就行】

3、导入Maven依赖

- MySQL依赖
- MyBatis依赖
- junit依赖

```xml
<!--导入依赖-->
<dependencies>
    <!--MySQL驱动-->
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>8.0.27</version>
    </dependency>
    <!--MyBatis-->
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis</artifactId>
        <version>3.5.7</version>
    </dependency>
    <!--junit-->
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.13.1</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```

### 2.2 创建一个模块

#### 1、编写MyBatis的核心配置文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<!--configuration核心配置文件-->
<configuration>
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.cj.jdbc.driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/mybatis?useSSL=true&amp;useUnicode=true&amp;characterEncoding=UTF-8&amp;serverTimezone=GMT%2B8"/>
                <property name="username" value="root"/>
                <property name="password" value="123456"/>
            </dataSource>
        </environment>
    </environments>
    <mappers>
        <mapper resource="org/mybatis/example/BlogMapper.xml"/>
    </mappers>
</configuration>
```

#### 2、编写MyBatis工具类

```java
// sqlSessionFactory ---->sqlSession
public class MyBatisUtils {
    private static SqlSessionFactory sqlSessionFactory;
    private static InputStream inputStream;
    // 在静态代码块中，随着类的加载而加载
    static{
        try {
            // 使用MyBatis获取sqlSessionFactory对象
            String resource = "mybatis-config.xml";
            inputStream = Resources.getResourceAsStream(resource);
            sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    //既然有了 SqlSessionFactory，顾名思义，我们可以从中获得 SqlSession 的实例。
    //SqlSession 提供了在数据库执行 SQL 命令所需的所有方法。你可以通过 SqlSession 实例来直接执行已映射的 SQL 语句。
    public static SqlSession getSqlSession(){
        return sqlSessionFactory.openSession();
    }
}
```

#### 3、编写代码

实体类

![image-20211229164921909](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211229164921909.png)

Dao接口

```java
public interface UserDao {
    List<User> getUserList();
}
```

接口实现类【由原来的UserDaoImpl接口实现类，换成一个xml配置文件】

![image-20211229170057249](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211229170057249.png)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!--namespace = 绑定一个对应的Dao/Mapper接口-->
<mapper namespace="com.pledge.dao.UserDao">
    <select id="getUserList" resultType="com.pledge.pojo.User">
        select * from mybatis.user;
    </select>
</mapper>
```

#### 4、测试

Junit测试

```java
public class UserDaoTest {
    @Test
    public void getUserList() {
        // 1、获得sqlSession 对象
        SqlSession sqlSession = MyBatisUtils.getSqlSession();
        // 2、执行sql语句
            // 方式一：使用getMapper
        UserDao userDao = sqlSession.getMapper(UserDao.class);
        for (User user : userDao.getUserList()) {
            System.out.println(user);
        }
        // 3、关闭资源
        sqlSession.close();
    }
}
```



#### 5、问题说明

##### 1、配置文件没有注册

![image-20211229172738838](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211229172738838.png)

##### 2、绑定接口错误

![image-20211229172850091](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211229172850091.png)

##### 3、方法名不对

这里调用反射，id=“接口的方法名”，方法名错了，就没办法反射了

![image-20211229172910823](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211229172910823.png)

##### 4、返回类型不对

如果返回值是list，那么写他泛型内部的。

如下返回值类型是List<User>，此处直接写User

![image-20211229173205520](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211229173205520.png)

##### 5、Maven静态资源过滤问题

资源过滤，要开开，要不然会报错，找不到java目录下面的文件，只能找到src目录下边



```xml
<resources>
   <resource>
       <directory>src/main/java</directory>
       <includes>
           <include>**/*.properties</include>
           <include>**/*.xml</include>
       </includes>
       <filtering>false</filtering>
   </resource>
  
   <resource>
       <directory>src/main/resources</directory>
       <includes>
           <include>**/*.properties</include>
           <include>**/*.xml</include>
       </includes>
       <filtering>false</filtering>
   </resource>
</resources>
```

## 3. 增删改查(CRUD)

### 1、namespace

namespace中的包名要和Dao/Mapper 接口的包名一致

![image-20211229230848036](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211229230848036.png)

### 2、增删改查【步骤】

#### 1、编写接口，制定接口方法

![image-20211229231752058](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211229231752058.png)

#### 2、编写对应的mapper.xml配置文件中的sql语句

![image-20211229231915664](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211229231915664.png)

#### 3、测试

![image-20211229231957967](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211229231957967.png)

#### 注意：

==增删改，要在关闭流之前提交事务，否则事务无效==

```java
@Test
public void delUserById(){
    // 1、获取sqlSession对象，并通过try保证流的关闭
    try(SqlSession sqlSession = MyBatisUtils.getSqlSession()){
        // 2、获取UserMapper对象，并调用目标方法
        UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
        userMapper.delUserById(2);
        // 3、提交事务
        sqlSession.commit();
    }
}
```

配置文件的resource后面不能用com.pledge.dao.UserMapper.xml

这里后面放的是路径，要用斜杠

```xml
<!--每一个Mapper.xml都需要在MyBatis核心配置文件中注册    -->
<mappers>
    <mapper resource="com/pledge/dao/UserMapper.xml"/>
</mappers>
```

### 3、查询select

- id：就是对应UserMapper接口中的方法名
- resultType：SQL语句执行的返回值
- parameterType：要传参数的类型（int，String。。。）

1、编写接口，制定接口方法

```java
public interface UserMapper {

    /**
     * 查询表中所有信息
     * @return User对象列表
     */
    List<User> getUserList();

    /**
     * 根据ID查询数据
     * @param id 要查询数据的id
     * @return 返回User对象
     */
    User getUserById(int id);

}
```

2、编写对应的mapper.xml配置文件中的sql语句

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

<!--namespace = 绑定一个对应的Dao/Mapper接口-->
<mapper namespace="com.pledge.dao.UserMapper">
    <!--查询操作-->
    <select id="getUserList" resultType="com.pledge.pojo.User">
        select * from mybatis.user;
    </select>
    <select id="getUserById" resultType="com.pledge.pojo.User" parameterType="int">
        select * from mybatis.user where id = #{id};
    </select>
</mapper>
```

3、测试

```java
public class UserMapperTest {
    @Test
    public void getUserList() {
        // 1、获得sqlSession 对象,并确保流的关闭
        try (SqlSession sqlSession = MyBatisUtils.getSqlSession()){
            // 2、执行sql语句
            // 方式一：使用getMapper
            UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
            for (User user : userMapper.getUserList()) {
                System.out.println(user);
            }
        }
    }

    @Test
    public void getUserById() {
        // 1、获得sqlSession 对象,并确保流的关闭
        try (SqlSession sqlSession = MyBatisUtils.getSqlSession()){
            // 2、执行sql语句
            UserMapper userMapper = sqlSession.getMapper(UserMapper.class);

            User user = userMapper.getUserById(1);
            System.out.println(user);
        }
    }
}
```

### 4、插入insert

- id：就是对应UserMapper接口中的方法名
- resultType：SQL语句执行的返回值
- parameterType：要传参数的类型（int，String。。。）

1、编写接口，制定接口方法

```java
public interface UserMapper {
    /**
     * 插入个用户信息
     * @param user 待插入的新用户
     */
    void addUser(User user);
}
```

2、编写对应的mapper.xml配置文件中的sql语句

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

<!--namespace = 绑定一个对应的Dao/Mapper接口-->
<mapper namespace="com.pledge.dao.UserMapper">
    <!--插入操作-->
    <!--对象中的属性，可以直接取出来，甚至不用User.getName(),直接下name就行    -->
    <insert id="addUser" parameterType="com.pledge.pojo.User">
        insert into mybatis.user(`id`,`name`,`pwd`) values (#{id},#{name},#{pwd});
    </insert>
</mapper>
```

3、测试

```java
public class UserMapperTest {
    @Test
    public void addUser(){
        // 1、获得sqlSession对象，并确保流关闭
        try(SqlSession sqlSession = MyBatisUtils.getSqlSession()){
            // 2、执行sql语句
            UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
            User user = new User(9,"金毛狮王","wujihaier");
            userMapper.addUser(user);

            // 提交事务！！！
            sqlSession.commit();
        }
    }
}
```

### 5、更新update

- id：就是对应UserMapper接口中的方法名
- resultType：SQL语句执行的返回值
- parameterType：要传参数的类型（int，String。。。）

1、编写接口，制定接口方法

```java
public interface UserMapper {
    /**
     * 根据id更新用户信息
     * @param user 要更新的用户
     */
    void updateUser(User user);
}
```

2、编写对应的mapper.xml配置文件中的sql语句

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

<!--namespace = 绑定一个对应的Dao/Mapper接口-->
<mapper namespace="com.pledge.dao.UserMapper">
    <!--更新操作-->
    <update id="updateUser" parameterType="com.pledge.pojo.User">
        update mybatis.user set name=#{name},pwd=#{pwd} where id=#{id};
    </update>
</mapper>
```

3、测试

```java
public class UserMapperTest {
    @Test
    public void updateUser(){
        // 1、获取sqlSession对象，并确保流关闭
        try(SqlSession sqlSession = MyBatisUtils.getSqlSession()){
            // 2、获取userMapper对象，调用对应方法
            UserMapper mapper = sqlSession.getMapper(UserMapper.class);
            mapper.updateUser(new User(9,"乔峰","azhu"));
            // 3、提交事务
            sqlSession.commit();
        }
    }
}
```

### 6、删除delete

- id：就是对应UserMapper接口中的方法名
- resultType：SQL语句执行的返回值
- parameterType：要传参数的类型（int，String。。。）

1、编写接口，制定接口方法

```java
public interface UserMapper {
    /**
     * 根据id删除一个用户
     * @param id 要删除用户的id
     */
    void delUserById(int id);
}
```

2、编写对应的mapper.xml配置文件中的sql语句

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

<!--namespace = 绑定一个对应的Dao/Mapper接口-->
<mapper namespace="com.pledge.dao.UserMapper">
    <!--删除操作-->
    <delete id="delUserById" parameterType="int">
        delete
        from mybatis.user
        where id=#{id};
    </delete>
</mapper>
```

3、测试

```java
public class UserMapperTest {
    @Test
    public void delUserById(){
        // 1、获取sqlSession对象，并通过try保证流的关闭
        try(SqlSession sqlSession = MyBatisUtils.getSqlSession()){
            // 2、获取UserMapper对象，并调用目标方法
            UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
            userMapper.delUserById(2);
            // 3、提交事务
            sqlSession.commit();
        }
    }
}
```

### 7、万能的Map

==**不管三七二十一！！！只要传参，就可以用Map传**==

假设，我们的实体类，或者数据库中的表，字段或者参数过多，我们应当考虑使用Map。

就是--如果你传实体类对象，那么要通过构造器new对象，有可能只用几个参数，new的时候却只能用全参构造器，而且使用时名字只能是属性名，Map就不一样了，直接key-value，new一个HashMap，想存几个put几个，名字随便起

```java
// 正常方法
/**
     * 插入个用户信息
     * @param user 待插入的新用户
     */
//    void addUser(User user);

// Map方法
    /**
     * 使用Map插入新对象
     * @param map key-value用来存储相应的属性和名称，需要几个put几个
     */
    void addUser(Map<String,Object> map);
```

```xml
<!--插入操作-->
    <!--对象中的属性，可以直接取出来，甚至不用User.getName(),直接下name就行    -->
<!--    <insert id="addUser" parameterType="com.pledge.pojo.User">-->
<!--        insert into mybatis.user(`id`,`name`,`pwd`) values (#{id},#{name},#{pwd});-->
<!--    </insert>-->


    <!--使用Map传参，map对象中的属性，可以随意赋值，在这里调用时使用自己赋值的key就行    -->
    <insert id="addUser" parameterType="map">
        insert into mybatis.user (`id`,`name`,`pwd`) values (#{myId},#{myName},#{myPwd});
    </insert>
```

**这里注意，参数类型还是parameterType，不是parameterMap**

```java
@Test
    public void addUser(){
        // 1、获得sqlSession对象，并确保流关闭
        try(SqlSession sqlSession = MyBatisUtils.getSqlSession()){
            // 2、执行sql语句
            UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
            
          // 方式一：使用对象传参
//            User user = new User(9,"金毛狮王","wujihaier");
//            userMapper.addUser(user);
            
          // 方式二：使用map传参
            HashMap<String, Object> map = new HashMap<>();
            map.put("myId","5");
            map.put("myName","沉香");
            map.put("myPwd","xiaoyu");
            userMapper.addUser(map);
            // 提交事务！！！
            sqlSession.commit();
        }
    }
```

### 8、模糊查询like语句该怎么写?

第1种：在Java代码中添加sql通配符。【传参，把这个通配符放到参数上】

```xml
string wildcardname = “%smi%”;
list<name> names = mapper.selectlike(wildcardname);

<select id=”selectlike”>
select * from foo where bar like #{value}
</select>
```

第2种：在sql语句中拼接通配符，会引起sql注入【传参，把这个通配符放在sql语句上，参数就仅仅传参数】

```xml
string wildcardname = “smi”;
list<name> names = mapper.selectlike(wildcardname);

<select id=”selectlike”>
    select * from foo where bar like "%"#{value}"%"
</select>
```

## 4、配置解析

#### 1、核心配置文件

- mybatis-config.xml 系统核心配置文件
- MyBatis 的配置文件包含了会深深影响 MyBatis 行为的设置和属性信息。
- 能配置的内容如下：

```xml
configuration（配置）
properties（属性）
settings（设置）
typeAliases（类型别名）
typeHandlers（类型处理器）
objectFactory（对象工厂）
plugins（插件）
environments（环境配置）
environment（环境变量）
transactionManager（事务管理器）
dataSource（数据源）
databaseIdProvider（数据库厂商标识）
mappers（映射器）
<!-- 注意元素节点的顺序！顺序不对会报错 -->
```

我们可以阅读 mybatis-config.xml 上面的dtd的头文件！

#### 2、环境配置

environments元素

**里面可以有多个配置环境，但是被使用的只有一个，就是在default那个更改，换上自己要用的环境，**

**为什么需要多个环境？？**

- 比如测试环境，

- 换了数据库测试

- 换了连接方式

- 换了数据库其他用户名和密码等

  ![image-20211230131859884](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211230131859884.png)

```xml
<environments default="development">
   <environment id="development">
       <transactionManager type="JDBC">
         	<property name="..." value="..."/>
       </transactionManager>
       <dataSource type="POOLED">
           <property name="driver" value="${driver}"/>
           <property name="url" value="${url}"/>
           <property name="username" value="${username}"/>
           <property name="password" value="${password}"/>
       </dataSource>
   </environment>
</environments>
```

- 配置MyBatis的多套运行环境，将SQL映射到多个不同的数据库上，必须指定其中一个为默认运行环境（通过default指定）

- 子元素节点：**environment**

- - dataSource 元素使用标准的 JDBC 数据源接口来配置 JDBC 连接对象的资源。

  - 数据源是必须配置的。

  - 有三种内建的数据源类型

    ```xml
    type="[UNPOOLED|POOLED|JNDI]"）
    ```

  - unpooled：这个数据源的实现只是每次被请求时打开和关闭连接。

  - **pooled**：这种数据源的实现利用“池”的概念将 JDBC 连接对象组织起来 , 这是一种使得并发 Web 应用快速响应请求的流行处理方式。

  - jndi：这个数据源的实现是为了能在如 Spring 或应用服务器这类容器中使用，容器可以集中或在外部配置数据源，然后放置一个 JNDI 上下文的引用。

  - 数据源也有很多第三方的实现，比如dbcp，c3p0，druid等等....

  - 这两种事务管理器类型都不需要设置任何属性。

  - 具体的一套环境，通过设置id进行区别，id保证唯一！

  - 子元素节点：transactionManager - [ 事务管理器 ]

    ```xml
    <!-- 语法 -->
    <transactionManager type="[ JDBC | MANAGED ]"/>
    ```

  - 子元素节点：**数据源（dataSource）**

#### 3、Properties优化

数据库这些属性都是可外部配置且可动态替换的，既可以在典型的 Java 属性文件中配置，亦可通过 properties 元素的子元素来传递。

![image-20211230135906523](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211230135906523.png)

我们来优化我们的配置文件

第一步 ：在资源目录下新建一个db.properties

```properties
driver=com.mysql.cj.jdbc.Driver
url=jdbc:mysql://localhost:3306/mybatis?useSSL=true&useUnicode=true&characterEncoding=UTF-8&serverTimezone=GMT%2B8
username=root
password=123456
```

第二步 : 将文件导入properties 配置文件==【注意，properties标签要写在顶端，最上边！！！！】==

```xml
<configuration>
   <!--导入properties文件-->
   <properties resource="db.properties"/>

   <environments default="development">
       <environment id="development">
           <transactionManager type="JDBC"/>
           <dataSource type="POOLED">
               <property name="driver" value="${driver}"/>
               <property name="url" value="${url}"/>
               <property name="username" value="${username}"/>
               <property name="password" value="${password}"/>
           </dataSource>
       </environment>
   </environments>
   <mappers>
       <mapper resource="mapper/UserMapper.xml"/>
   </mappers>
</configuration>
```

除了直接引入，还可以在其中增加配置

就是properties文件中写一部分，在xml配置文件中写一部分

```xml
<configuration>
<!--    引入外部配置文件-->
    <properties resource="db.properties">
        <property name="pwd" value="1234"/>
    </properties>
```

如果有重名的属性，那么xml文件中的属性会覆盖properties文件的属性

#### 4、typeAliases优化

![](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211230135906523.png)

##### 4.1 类起别名

类型别名是为 Java 类型设置一个短的名字。它只和 XML 配置有关，存在的意义仅在于用来减少类完全限定名的冗余。

```xml
<!--配置别名,注意顺序-->
<typeAliases>
   <typeAlias type="com.pledge.pojo.User" alias="hello"/>
</typeAliases>
```

当这样配置时，`User`可以用在任何使用`com.pledge.pojo.User`的地方。

![image-20211230140139748](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211230140139748.png)

##### 4.2 指定包名

也可以指定一个包名，MyBatis 会在包名下面搜索需要的 Java Bean，比如:

```xml
<typeAliases>
   <package name="com.pledge.pojo"/>
</typeAliases>
```

每一个在包 `com.pledge.pojo` 中的 Java Bean，在没有注解的情况下，会使用 Bean 的首字母小写的非限定类名来作为它的别名。

<font color='red'>指定包名之后，这个包下的所有类，都有了别名，别名就是这个类名开头字母小写</font>

![image-20211230140626293](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211230140626293.png)

若有注解，则别名为其注解值。见下面的例子：

```java
@Alias("丫蛋")
public class User {
  // 这样后边调用的时候，写丫蛋，就能找到这个类
}
```

#### 5、设置

- 设置（settings）相关 => 查看帮助文档

- - 懒加载
  - 日志实现
  - 缓存开启关闭

- 一个配置完整的 settings 元素的示例如下：

  ```xml
  <settings>
   <setting name="cacheEnabled" value="true"/>
   <setting name="lazyLoadingEnabled" value="true"/>
   <setting name="multipleResultSetsEnabled" value="true"/>
   <setting name="useColumnLabel" value="true"/>
   <setting name="useGeneratedKeys" value="false"/>
   <setting name="autoMappingBehavior" value="PARTIAL"/>
   <setting name="autoMappingUnknownColumnBehavior" value="WARNING"/>
   <setting name="defaultExecutorType" value="SIMPLE"/>
   <setting name="defaultStatementTimeout" value="25"/>
   <setting name="defaultFetchSize" value="100"/>
   <setting name="safeRowBoundsEnabled" value="false"/>
   <setting name="mapUnderscoreToCamelCase" value="false"/>
   <setting name="localCacheScope" value="SESSION"/>
   <setting name="jdbcTypeForNull" value="OTHER"/>
   <setting name="lazyLoadTriggerMethods" value="equals,clone,hashCode,toString"/>
  </settings>
  ```

**类型处理器**

- 无论是 MyBatis 在预处理语句（PreparedStatement）中设置一个参数时，还是从结果集中取出一个值时， 都会用类型处理器将获取的值以合适的方式转换成 Java 类型。
- 你可以重写类型处理器或创建你自己的类型处理器来处理不支持的或非标准的类型。【了解即可】

**对象工厂**

- MyBatis 每次创建结果对象的新实例时，它都会使用一个对象工厂（ObjectFactory）实例来完成。
- 默认的对象工厂需要做的仅仅是实例化目标类，要么通过默认构造方法，要么在参数映射存在的时候通过有参构造方法来实例化。
- 如果想覆盖对象工厂的默认行为，则可以通过创建自己的对象工厂来实现。

#### 6、映射器（mappers）

MapperRegistry：注册绑定我们的Mapper文件

方式一：

```xml
<!-- 使用相对于类路径的资源引用 -->
<mappers>
  <mapper resource="org/mybatis/builder/AuthorMapper.xml"/>
  <mapper resource="org/mybatis/builder/BlogMapper.xml"/>
  <mapper resource="org/mybatis/builder/PostMapper.xml"/>
</mappers>
```

方式二：

注意：【否则会报错】

- 接口和他的Mapper配置文件必须同名
- 接口和他的Mapper配置文件必须在同一个包下

```xml
<!-- 使用完全限定资源定位符（URL） -->
<mappers>
  <mapper url="file:///var/mappers/AuthorMapper.xml"/>
  <mapper url="file:///var/mappers/BlogMapper.xml"/>
  <mapper url="file:///var/mappers/PostMapper.xml"/>
</mappers>
```

方式三：

注意：【否则会报错】

- 接口和他的Mapper配置文件必须同名
- 接口和他的Mapper配置文件必须在同一个包下

```xml
<!-- 使用映射器接口实现类的完全限定类名 -->
<mappers>
  <mapper class="org.mybatis.builder.AuthorMapper"/>
  <mapper class="org.mybatis.builder.BlogMapper"/>
  <mapper class="org.mybatis.builder.PostMapper"/>
</mappers>
```

方式四：

```xml
<!-- 将包内的映射器接口实现全部注册为映射器 -->
<mappers>
  <package name="org.mybatis.builder"/>
</mappers>
```

这些配置会告诉 MyBatis 去哪里找映射文件



#### 7、作用域和生命周期

理解我们目前已经讨论过的不同作用域和生命周期类是至关重要的，因为错误的使用会导致非常严重的并发问题。

我们可以先画一个流程图，分析一下Mybatis的执行过程！



![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7JdnS939HH5TayIhQo5s0aJbReBExSQO1U23XeLAXlhTWUeL87mJZL0lDzPstpY3CSIwvW0dN9ccA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**作用域理解**

- SqlSessionFactoryBuilder==【创建完工厂，他就没用了】==

  - SqlSessionFactoryBuilder 的作用在于创建 SqlSessionFactory，创建成功后【创建完工厂，他就没用了】SqlSessionFactoryBuilder 就失去了作用，所以它只能存在于创建 SqlSessionFactory 的方法中，而不要让其长期存在。因此 **SqlSessionFactoryBuilder 实例的最佳作用域是方法作用域**（也就是局部方法变量）。

- SqlSessionFactory ==【相当于一个数据库连接池，除非MyBatis不用了】==

  - SqlSessionFactory 可以被认为是一个数据库连接池，它的作用是创建 SqlSession 接口对象。因为 MyBatis 的本质就是 Java 对数据库的操作，所以 ==SqlSessionFactory 的生命周期存在于整个 MyBatis 的应用之中，所以一旦创建了 SqlSessionFactory，就要长期保存它，直至不再使用 MyBatis 应用，所以可以认为 SqlSessionFactory 的生命周期就等同于 MyBatis 的应用周期。==

  - 由于 SqlSessionFactory 是一个对数据库的连接池，所以它占据着数据库的连接资源。如果创建多个 SqlSessionFactory，那么就存在多个数据库连接池，这样不利于对数据库资源的控制，也会导致数据库连接资源被消耗光，出现系统宕机等情况，所以尽量避免发生这样的情况。

  - 因此在一般的应用中我们往往希望 SqlSessionFactory 作为一个单例，让它在应用中被共享。所以说 **SqlSessionFactory 的最佳作用域是应用作用域。**

- SqlSession ==数据库连接池里的对象，用完了还回去，需要时再创建==

  - 如果说 SqlSessionFactory 相当于数据库连接池，那么 SqlSession 就相当于一个数据库连接（Connection 对象），你可以在一个事务里面执行多条 SQL，然后通过它的 commit、rollback 等方法，提交或者回滚事务。所以它应该存活在一个业务请求中，处理完整个请求后，应该关闭这条连接，让它归还给 SqlSessionFactory，否则数据库资源就很快被耗费精光，系统就会瘫痪，所以用 try...catch...finally... 语句来保证其正确关闭。

  - **所以 SqlSession 的最佳的作用域是请求或方法作用域。**



![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7JdnS939HH5TayIhQo5s0aJJq1YuJCr3e9PsTBpBgc1tbicoshHB3qLkwgn3Jp2q8qI1dY9vGhIia3w/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



## 5、解决属性名和字段名不一致的问题

环境：新建一个项目，将之前的项目拷贝过来

1、查看之前的数据库的字段名

![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7KdXPq6whFkfHe43CtgZMJrr62lCnbfxl25aQ4ZDwlU4JiaMZHs3nqAoNxFsJYZRC4Cm11uSH0USNQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

2、Java中的实体类设计

```java
public class User {

   private int id;  //id
   private String name;   //姓名
   private String password;   //密码和数据库不一样！
   
   //构造
   //set/get
   //toString()
}
```

3、接口

```java
//根据id查询用户
User selectUserById(int id);
```

4、mapper映射文件

```java
<select id="selectUserById" resultType="user">
  select * from user where id = #{id}
</select>
```

5、测试

```java
@Test
public void testSelectUserById() {
   SqlSession session = MybatisUtils.getSession();  //获取SqlSession连接
   UserMapper mapper = session.getMapper(UserMapper.class);
   User user = mapper.selectUserById(1);
   System.out.println(user);
   session.close();
}
```

**结果:**

- User{id=1, name='狂神', password='null'}
- 查询出来发现 password 为空 . 说明出现了问题！

**分析：**

- select * from user where id = #{id} 可以看做

  select  id,name,pwd  from user where id = #{id}

- mybatis会根据这些查询的列名(会将列名转化为小写,数据库不区分大小写) , 去对应的实体类中查找相应列名的set方法设值 , 由于找不到setPwd() , 所以password返回null ; 【自动映射】



### 1、解决方案

方案一：为列名指定别名 , 别名和java实体类的属性名一致 .

```xml
<select id="selectUserById" resultType="User">
  select id , name , pwd as password from user where id = #{id}
</select>
```

**方案二：使用结果集映射->ResultMap** 【推荐】

简单说，就是找一个中介，通过key-value

- key：数据库字段名
- value：对应类的属性名

原本对不上，现在用中介找到key，返回value，就对上了

==这里不需要写所有属性，那个字段和属性名不一样，就写他，一样的就不用写==

```xml
<resultMap id="UserMap" type="User">
   <id column="id" property="id"/>
   <!-- column是数据库表的列名 , property是对应实体类的属性名 -->
   <result column="name" property="name"/>
   <result column="pwd" property="password"/>
</resultMap>

<select id="selectUserById" resultMap="UserMap">
  select * from user where id = #{id}
</select>
```



### 2、ResultMap

**自动映射**

- `resultMap` 元素是 MyBatis 中最重要最强大的元素。它可以让你从 90% 的 JDBC `ResultSets` 数据提取代码中解放出来。
- 实际上，在为一些比如连接的复杂语句编写映射代码的时候，一份 `resultMap` 能够代替实现同等功能的长达数千行的代码。
- ResultMap 的设计思想是，对于简单的语句根本不需要配置显式的结果映射，而对于复杂一点的语句只需要描述它们的关系就行了。

你已经见过简单映射语句的示例了，但并没有显式指定 `resultMap`。比如：

```xml
<select id="selectUserById" resultType="map">
select id , name , pwd
  from user
  where id = #{id}
</select>
```

上述语句只是简单地将所有的列映射到 `HashMap` 的键上，这由 `resultType` 属性指定。虽然在大部分情况下都够用，但是 HashMap 不是一个很好的模型。你的程序更可能会使用 JavaBean 或 POJO（Plain Old Java Objects，普通老式 Java 对象）作为模型。

`ResultMap` 最优秀的地方在于，虽然你已经对它相当了解了，但是根本就不需要显式地用到他们。

**手动映射**

1、返回值类型为resultMap

```xml
<select id="selectUserById" resultMap="UserMap">
  select id , name , pwd from user where id = #{id}
</select>
```

2、编写resultMap，实现手动映射！

```xml
<resultMap id="UserMap" type="User">
   <!-- id为主键 -->
   <id column="id" property="id"/>
   <!-- column是数据库表的列名 , property是对应实体类的属性名 -->
   <result column="name" property="name"/>
   <result column="pwd" property="password"/>
</resultMap>
```

如果世界总是这么简单就好了。但是肯定不是的，数据库中，存在一对多，多对一的情况，我们之后会使用到一些高级的结果集映射，association，collection这些，我们将在之后讲解，今天你们需要把这些知识都消化掉才是最重要的！理解结果集映射的这个概念！

## 6、日志

### 1、日志工厂

思考：我们在测试SQL的时候，要是能够在控制台输出 SQL 的话，是不是就能够有更快的排错效率？

如果一个 数据库相关的操作出现了问题，我们可以根据输出的SQL语句快速排查问题。

对于以往的开发过程，我们会经常使用到debug模式来调节，跟踪我们的代码执行过程。但是现在使用Mybatis是基于接口，配置文件的源代码执行过程。因此，我们必须选择日志工具来作为我们开发，调节程序的工具。

Mybatis内置的日志工厂提供日志功能，具体的日志实现有以下几种工具：

- SLF4J
- Apache Commons Logging
- Log4j 2
- ==Log4j==
- JDK logging

具体选择哪个日志实现工具由MyBatis的内置日志工厂确定。它会使用最先找到的（按上文列举的顺序查找）。如果一个都未找到，日志功能就会被禁用。

**标准日志实现**

指定 MyBatis 应该使用哪个日志记录实现。如果此设置不存在，则会自动发现日志记录实现。

```xml
<settings>
       <setting name="logImpl" value="STDOUT_LOGGING"/>
</settings>
```

测试，可以看到控制台有大量的输出！我们可以通过这些输出来判断程序到底哪里出了Bug

### 2、Log4j

**简介：**

- Log4j是Apache的一个开源项目
- 通过使用Log4j，我们可以控制日志信息输送的目的地：控制台，文本，GUI组件....
- 我们也可以控制每一条日志的输出格式；
- 通过定义每一条日志信息的级别，我们能够更加细致地控制日志的生成过程。最令人感兴趣的就是，这些可以通过一个配置文件来灵活地进行配置，而不需要修改应用的代码。

**使用步骤：**

1、导入log4j的包

```xml
<dependency>
   <groupId>log4j</groupId>
   <artifactId>log4j</artifactId>
   <version>1.2.17</version>
</dependency>
```

2、配置文件编写

```properties
#将等级为DEBUG的日志信息输出到console和file这两个目的地，console和file的定义在下面的代码
log4j.rootLogger=DEBUG,console,file

#控制台输出的相关设置
log4j.appender.console = org.apache.log4j.ConsoleAppender
log4j.appender.console.Target = System.out
log4j.appender.console.Threshold=DEBUG
log4j.appender.console.layout = org.apache.log4j.PatternLayout
log4j.appender.console.layout.ConversionPattern=[%c]-%m%n

#文件输出的相关设置
log4j.appender.file = org.apache.log4j.RollingFileAppender
log4j.appender.file.File=./log/pledge.log
log4j.appender.file.MaxFileSize=10mb
log4j.appender.file.Threshold=DEBUG
log4j.appender.file.layout=org.apache.log4j.PatternLayout
log4j.appender.file.layout.ConversionPattern=[%p][%d{yy-MM-dd}][%c]%m%n

#日志输出级别
log4j.logger.org.mybatis=DEBUG
log4j.logger.java.sql=DEBUG
log4j.logger.java.sql.Statement=DEBUG
log4j.logger.java.sql.ResultSet=DEBUG
log4j.logger.java.sql.PreparedStatement=DEBUG
```

3、setting设置日志实现

```xml
<!--日志-->
<settings>
    <setting name="logImpl" value="LOG4J"/>
    <!--开启驼峰命名转换，就是数据库字段如果是create_id,字段使用驼峰命名createId
          这样就不用别名处理，开启这个配置后就能自动识别，仅限驼峰命名-->
    <setting name="mapUnderscoreToCamelCase" value="true"/>
    <!--开起全局缓存，默认是开启的，这里显式开启一下-->
    <setting name="cacheEnabled" value="true"/>
</settings>
```

4、在程序中使用Log4j进行输出！

```java
//注意导包：org.apache.log4j.Logger
static Logger logger = Logger.getLogger(MyTest.class);

@Test
public void selectUser() {
   logger.info("info：进入selectUser方法");
   logger.debug("debug：进入selectUser方法");
   logger.error("error: 进入selectUser方法");
   SqlSession session = MybatisUtils.getSession();
   UserMapper mapper = session.getMapper(UserMapper.class);
   List<User> users = mapper.selectUser();
   for (User user: users){
       System.out.println(user);
  }
   session.close();
}
```

5、测试，看控制台输出！

- 使用Log4j 输出日志
- 可以看到还生成了一个日志的文件 【需要修改file的日志级别】

![image-20211231115717420](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211231115717420.png)

## 7、分页

### 1、limit实现分页

**思考：为什么需要分页？**

在学习mybatis等持久层框架的时候，会经常对数据进行增删改查操作，使用最多的是对数据库进行查询操作，如果查询大量数据的时候，我们往往使用分页进行查询，也就是每次处理小部分数据，这样对数据库压力就在可控范围内。

**使用Limit实现分页**

```mysql
#语法
SELECT * FROM table LIMIT stratIndex，pageSize

SELECT * FROM table LIMIT 5,10; // 检索记录行 6-15  

#为了检索从某一个偏移量到记录集的结束所有的记录行，可以指定第二个参数为 -1：
# 这个bug已经被修复了，不能用-1了
SELECT * FROM table LIMIT 95,-1; // 检索记录行 96-last.  

#如果只给定一个参数，它表示返回最大的记录行数目：   
SELECT * FROM table LIMIT 5; //检索前 5 个记录行  

#换句话说，LIMIT n 等价于 LIMIT 0,n。 
```

**步骤：**

1、修改Mapper文件

```xml
<resultMap id="myMap" type="user">
        <result column="pwd" property="password"/>
</resultMap>
<!-- 因为字段名和类属性名不一致，这里用了个中介myMap-->
<select id="selectUser" parameterType="map" resultType="myMap">
  select * from user limit #{startIndex},#{pageSize}
</select>
```

2、Mapper接口，参数为map

```java
//选择全部用户实现分页
List<User> selectUser(Map<String,Integer> map);
```

3、在测试类中传入参数测试

- 推断：起始位置 =  （当前页面 - 1 ） * 页面大小

```java
//分页查询 , 两个参数startIndex , pageSize
@Test
public void testSelectUser() {
   SqlSession session = MybatisUtils.getSession();
   UserMapper mapper = session.getMapper(UserMapper.class);

   int currentPage = 1;  //第几页
   int pageSize = 2;  //每页显示几个
   Map<String,Integer> map = new HashMap<String,Integer>();
   map.put("startIndex",(currentPage-1)*pageSize);
   map.put("pageSize",pageSize);

   List<User> users = mapper.selectUser(map);

   for (User user: users){
       System.out.println(user);
  }

   session.close();
}
```



### 2、RowBounds分页【不推荐，太老了】

我们除了使用Limit在SQL层面实现分页，也可以使用RowBounds在Java代码层面实现分页，当然此种方式作为了解即可。我们来看下如何实现的！

**步骤：**

1、mapper接口

```java
//选择全部用户RowBounds实现分页
List<User> getUserByRowBounds();
```

2、mapper文件

```xml
<select id="getUserByRowBounds" resultType="user">
select * from user
</select>
```

3、测试类

在这里，我们需要使用RowBounds类

```java
@Test
public void testUserByRowBounds() {
   SqlSession session = MybatisUtils.getSession();

   int currentPage = 2;  //第几页
   int pageSize = 2;  //每页显示几个
   RowBounds rowBounds = new RowBounds((currentPage-1)*pageSize,pageSize);

   //通过session.**方法进行传递rowBounds，[此种方式现在已经不推荐使用了]
   List<User> users =session.selectList("com.kuang.mapper.UserMapper.getUserByRowBounds", null, rowBounds);

   for (User user: users){
       System.out.println(user);
  }
   session.close();
}
```





### 3、分页插件

#### MyBatis 分页插件 PageHelper

官方使用文档：https://pagehelper.github.io/docs/

![image-20211231132331216](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211231132331216.png)



## 8、使用注解开发

### 1、面向接口编程

- 大家之前都学过面向对象编程，也学习过接口，但在真正的开发中，很多时候我们会选择面向接口编程
- **根本原因 :  解耦 , 可拓展 , 提高复用 , 分层开发中 , 上层不用管具体的实现 , 大家都遵守共同的标准 , 使得开发变得容易 , 规范性更好**
- 在一个面向对象的系统中，系统的各种功能是由许许多多的不同对象协作完成的。在这种情况下，各个对象内部是如何实现自己的,对系统设计人员来讲就不那么重要了；
- 而各个对象之间的协作关系则成为系统设计的关键。小到不同类之间的通信，大到各模块之间的交互，在系统设计之初都是要着重考虑的，这也是系统设计的主要工作内容。面向接口编程就是指按照这种思想来编程。



**关于接口的理解**

- 接口从更深层次的理解，应是定义（规范，约束）与实现（名实分离的原则）的分离。

- 接口的本身反映了系统设计人员对系统的抽象理解。

- 接口应有两类：

- - 第一类是对一个个体的抽象，它可对应为一个抽象体(abstract class)；
  - 第二类是对一个个体某一方面的抽象，即形成一个抽象面（interface）；

- 一个体有可能有多个抽象面。抽象体与抽象面是有区别的。



**三个面向区别**

- 面向对象是指，我们考虑问题时，以对象为单位，考虑它的属性及方法 .

- 面向过程是指，我们考虑问题时，以一个具体的流程（事务过程）为单位，考虑它的实现 .

- 接口设计与非接口设计是针对复用技术而言的，与面向对象（过程）不是一个问题.更多的体现就是对系统整体的架构

  

### 2、利用注解开发

- **mybatis最初配置信息是基于 XML ,映射语句(SQL)也是定义在 XML 中的。而到MyBatis 3提供了新的基于注解的配置。不幸的是，Java 注解的的表达力和灵活性十分有限。最强大的 MyBatis 映射并不能用注解来构建**

- sql 类型主要分成 :

- - @select ()
  - @update ()
  - @Insert ()
  - @delete ()



**注意：**利用注解开发就不需要mapper.xml映射文件了 .

1、我们在我们的接口中添加注解

```java
//查询全部用户
@Select("select * from mybatis.user")
public List<User> getAllUser();
```

2、在mybatis的核心配置文件中注入

```xml
<!--使用class绑定接口-->
<mappers>
   <mapper class="com.kuang.mapper.UserMapper"/>
</mappers>
```

3、测试

```java
@Test
public void getUserList() {
    // 1、获取sqlSession对象，保证流关闭
    try(SqlSession sqlSession = MyBatisUtils.getSqlSession()){
        // 使用getMapper()方法，获取接口对象，调用目标方法
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
      
        for (User user : mapper.getUserList()) {
          	System.out.println(user);
        }
    }
}
```

4、利用Debug查看本质

![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7LZwwtchlelS8kzAAyVia5uNnMiahVkdvictXZkDDWHQCwob9rMlKtxnhiaQee5Kxa6K0BCbHH2ibRERibQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

5、本质上利用了jvm的动态代理机制

![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7LZwwtchlelS8kzAAyVia5uNeukjWMleICg2Jsm8hTI63hvVLiarGmD7zT1CmgXlUXSUbmdhialeIjpA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

6、Mybatis详细的执行流程

![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7LZwwtchlelS8kzAAyVia5uNvhic22X8ahJy5BdOfjy1LlDRfo8Nf3GOAzwALgvriau4SzmXZIhUUd2A/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

### 3、注解增删改

改造MybatisUtils工具类的getSession( ) 方法，增加true参数，实现事务的自动提交

```java
public class MyBatisUtils {
    private static SqlSessionFactory sqlSessionFactory;
    private static InputStream inputStream;
    // 在静态代码块中，随着类的加载而加载
    static{
        try {
            // 使用MyBatis获取sqlSessionFactory对象
            String resource = "mybatis-config.xml";
            inputStream = Resources.getResourceAsStream(resource);
            sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    //既然有了 SqlSessionFactory，顾名思义，我们可以从中获得 SqlSession 的实例。
    //SqlSession 提供了在数据库执行 SQL 命令所需的所有方法。你可以通过 SqlSession 实例来直接执行已映射的 SQL 语句。
    public static SqlSession getSqlSession(){
        // 参数true表示，开启自动提交
        return sqlSessionFactory.openSession(true);
    }
}
```

【注意】确保实体类和数据库字段对应

#### **查询：**

1、编写接口方法注解

这里values值一定是user类的属性，不能是数据库的字段

```java
/**
 * 查询表中所有信息
 * @return User对象列表
 */
@Select("select * from mybatis.user")
List<User> getUserList();
```

2、测试

```java
@Test
public void getUserList() {
    // 1、获取sqlSession对象，保证流关闭
    try(SqlSession sqlSession = MyBatisUtils.getSqlSession()){
        // 使用getMapper()方法，获取接口对象，调用目标方法
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        for (User user : mapper.getUserList()) {
            System.out.println(user);
        }
    }
}
```

#### **新增：**

1、编写接口方法注解

```java
//添加一个用户
@Insert("insert into mybatis.user(`id`,`name`,`pwd`) values(#{id},#{name},#{password})")
void addUser(User user);
```

2、测试

```java
@Test
public void addUser() {
    try(SqlSession sqlSession = MyBatisUtils.getSqlSession()){
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        mapper.addUser(new User(99,"天山童姥","tonglao"));
    }
}
```

#### **修改：**

1、编写接口方法注解

```java
/**
 * 修改一个用户
 * @param user 待更新目标
 */
@Update("update user set `name`=#{name},`pwd`=#{password} where `id`=#{id}")
void updateUser(User user);
```

2、测试

```java
@Test
public void updateUser(){
    try(SqlSession sqlSession = MyBatisUtils.getSqlSession()){
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        mapper.updateUser(new User(8,"如来佛祖","rulai"));
    }
}
```

#### **删除：**

1、编写接口方法注解

```java
/**
 * 根据id和姓名删除数据
 * @param id 待删除的id
 * @param name 待删除数据的姓名
 */
@Delete("delete from mybatis.user where `id`=#{id} and `name`=#{哈哈}")
void deleteUser(@Param("id")int id,@Param("哈哈") String name);
// @Param这种获取参数的方式，只能用在基本数据类型，引用数据类型不需要
```

2、测试

```java
@Test
public void deleteUser(){
    try(SqlSession sqlSession = MyBatisUtils.getSqlSession()){
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        mapper.deleteUser(11,"白眉鹰王");
    }
}
```

【注意点：增删改一定记得对事务的处理，此处没有处理是因为在MyBatisUtils工具类中增加了，自动提交事务】



### 4、关于@Param

@Param注解用于给方法参数起一个名字。以下是总结的使用原则：

- 在方法只接受一个参数的情况下，可以不使用@Param。

- 在方法接受多个参数的情况下，建议一定要使用@Param注解给参数命名。

- 如果参数是 JavaBean【==引用数据类型==】 ， 则不能使用@Param。

- 不使用@Param注解时，参数只能有一个，并且是Javabean。

  ```java
  @Delete("delete from mybatis.user where `id`=#{id} and `name`=#{哈哈}")
  void deleteUser(@Param("id")int id,@Param("哈哈") String name);
  ```

  

### 5、#与$的区别

- \#{} 的作用主要是替换预编译语句(PrepareStatement)中的占位符? 【推荐使用】

  ```mysql
  INSERT INTO user (name) VALUES (#{name});
  INSERT INTO user (name) VALUES (?);
  ```

- ${} 的作用是直接进行字符串替换【==存在SQL注入风险==】

  ```mysql
  INSERT INTO user (name) VALUES ('${name}');
  INSERT INTO user (name) VALUES ('kuangshen');
  ```

> 使用注解和配置文件协同开发，才是MyBatis的最佳实践！

### 6、Lombok插件

#### 1、Lombok是什么

Lombok官网：https://projectlombok.org

Lombok项目是一种自动接通你的编辑器和构建工具的一个Java库。不用再一次写额外的getter或者equals方法。由此可以看出，lombok会帮我们自动生成getter和euqals方法,但是更有意思的是,当我们的变量发生改变时,我们不再需要修改对的getter、setter方法,lombok帮我们在运行的过程中自动生成上述方法,编码更灵活.

使用lombok的优点: 

- 1、简化long冗余的javabean代码;

- 2、提高执行效率

#### 2、如何使用Lombok

##### 1、IDEA中添加Lombok插件

![image-20211231173843448](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211231173843448.png)

##### 2、引入依赖【mvn仓库】：

```xml
<!--Lombok插件-->
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.20</version>
<!--  <scope>provided</scope>  -->
</dependency>

<!--scope作用域可以删掉，直接全局生效-->
```

##### 3、lombok中的常用注解

最常用：

- ==@Data==：get、set、equals、hashCode、toString

  ![image-20211231174202128](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211231174202128.png)

- ==@AllArgsConstructor==：全参构造器；

- ==@NoArgsConstructor==：无参构造器；

@Setter ：在JavaBean或类JavaBean中使用，使用此注解会生成对应的setter方法；
@Getter：在JavaBean或类JavaBean中使用，使用此注解会生成对应的getter方法；
==@ToString==：在JavaBean或类JavaBean中使用，使用此注解会自动重写对应的toStirng方法；
@NoArgsConstructor：在JavaBean或类JavaBean中使用，使用此注解会生成对应的无参构造方法；
@HashCode：
@Equals：
@CanEqual：
@Data：在JavaBean或类JavaBean中使用，这个注解包含范围最广，它包含上述注解，即当使用当前注解时，会自动生成包含的所有方法；
@AllArgsConstructor：在JavaBean或类JavaBean中使用，使用此注解会生成对应的有参构造方法；
@Log(这是一个泛型注解，具体有很多种形式)
@EqualsAndHashCode：在JavaBean或类JavaBean中使用，使用此注解会自动重写对应的equals方法和hashCode方法；

##### 4、使用

- 可以放在属性上
  - @Getter，就会生产该属性单独的get方法
- 可以配合使用
  - 自己写部分参数的构造器，无参和全参用注解

## 9、多对一的处理

数据库表如下：

![image-20211231204427647](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211231204427647.png)

需求：获取所有学生信息，并获取对应的老师，将学生表最后一个老师id换成老师名字输出

正常的语句和结果应该如下：

```sql
select s.id,s.name,t.name
from student s,teacher t
where s.tid=t.id;
```

![image-20211231204246027](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211231204246027.png)

方式一：在StudentMapper.xml中的语句如下：

```xml
1、直接查学生表所有信息
<select id="getStudent" resultMap="student_teacher">
    select * from mybatis.student
</select>
2、调用一个中介，返回学生信息。中介的第三个元素为teacher类，并调用select再附加查询
<resultMap id="student_teacher" type="student">
    <result property="id" column="id"/>
    <result property="name" column="name"/>
    <!--
        一一对应的直接result就行了，但是要形成复杂的，id列，name列，老师列
        如果是返回对象：用association
        如果是返回集合：用collection
    -->
    <association property="teacher" column="tid" javaType="teacher" select="getTeacher"/>
</resultMap>

3、association中调用下边这个查询，根据id返回teacher类
<select id="getTeacher" resultType="teacher">
    select * from mybatis.teacher where id=#{id}
</select>
```



### 1、数据库设计



![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7LPbib5To6slfFhMArq5QvCjofjccx37cuQgKsWEHibax0bDiaicU6ojNfEzWrj3TibFsX3MJju4sAp5Pg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

```mysql
#创建教师表
CREATE TABLE `teacher` (
`id` INT(10) NOT NULL,
`name` VARCHAR(30) DEFAULT NULL,
PRIMARY KEY (`id`)
) ENGINE=INNODB DEFAULT CHARSET=utf8

INSERT INTO teacher(`id`, `name`) VALUES (1, '秦老师');

#创建学生表
CREATE TABLE `student` (
`id` INT(10) NOT NULL,
`name` VARCHAR(30) DEFAULT NULL,
`tid` INT(10) DEFAULT NULL,
PRIMARY KEY (`id`),
KEY `fktid` (`tid`),
CONSTRAINT `fktid` FOREIGN KEY (`tid`) REFERENCES `teacher` (`id`)
) ENGINE=INNODB DEFAULT CHARSET=utf8


INSERT INTO `student` (`id`, `name`, `tid`) VALUES ('1', '小明', '1');
INSERT INTO `student` (`id`, `name`, `tid`) VALUES ('2', '小红', '1');
INSERT INTO `student` (`id`, `name`, `tid`) VALUES ('3', '小张', '1');
INSERT INTO `student` (`id`, `name`, `tid`) VALUES ('4', '小李', '1');
INSERT INTO `student` (`id`, `name`, `tid`) VALUES ('5', '小王', '1');
```

### 2、搭建测试环境

#### 1、IDEA安装Lombok插件

#### 2、引入Maven依赖

```xml
<!-- https://mvnrepository.com/artifact/org.projectlombok/lombok -->
<dependency>
   <groupId>org.projectlombok</groupId>
   <artifactId>lombok</artifactId>
   <version>1.16.10</version>
</dependency>
```

#### 3、创建对应数据库的实体类

```java
@Data
@NoArgsConstructor
@AllArgsConstructor
public class Student {
    private int id;
    private String name;
    private Teacher teacher;
}
@Data
@NoArgsConstructor
@AllArgsConstructor
public class Teacher {
    private int id;
    private String name;
}
```

#### 4、编写实体类对应的Mapper接口 【两个】

- **无论有没有需求，都应该写上，以备后来之需！**

```java
public interface StudentMapper {
}
public interface TeacherMapper {
}
```

#### 5、编写Mapper接口对应的 mapper.xml配置文件 【两个】

- **无论有没有需求，都应该写上，以备后来之需！**

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
       PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
       "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.kuang.mapper.StudentMapper">

</mapper>
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
       PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
       "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.pledge.mapper.TeacherMapper">

</mapper>
```



### 3、按查询嵌套处理

#### 1、给StudentMapper接口增加方法

```java
//获取所有学生及对应老师的信息
public List<Student> getStudents();
```

#### 2、编写对应的Mapper文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
       PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
       "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.kuang.mapper.StudentMapper">

   <!--
   需求：获取所有学生及对应老师的信息
   思路：
       1. 获取所有学生的信息
       2. 根据获取的学生信息的老师ID->获取该老师的信息
       3. 思考问题，这样学生的结果集中应该包含老师，该如何处理呢，数据库中我们一般使用关联查询？
           1. 做一个结果集映射：StudentTeacher
           2. StudentTeacher结果集的类型为 Student
           3. 学生中老师的属性为teacher，对应数据库中为tid。
              多个 [1,...）学生关联一个老师=> 一对一，一对多
           4. 查看官网找到：association – 一个复杂类型的关联；使用它来处理关联查询
   -->
   <select id="getStudents" resultMap="StudentTeacher">
    		select * from student
   </select>
   <resultMap id="StudentTeacher" type="Student">
       <!--association关联属性 property属性名 javaType属性类型 column在多的一方的表中的列名-->
       <association property="teacher"  column="tid" javaType="Teacher"select="getTeacher"/>
   </resultMap>
   <!--
   这里传递过来的id，只有一个属性的时候，下面可以写任何值
   association中column多参数配置：
       column="{key=value,key=value}"
       其实就是键值对的形式，key是传给下个sql的取值名称，value是片段一中sql查询的字段名。
   -->
   <select id="getTeacher" resultType="teacher">
      select * from teacher where id = #{id}
   </select>

</mapper>
```

#### 3、编写完毕去Mybatis配置文件中，注册Mapper！

#### 4、注意点说明：

```xml
<resultMap id="StudentTeacher" type="Student">
   <!--association关联属性 property属性名 javaType属性类型 column在多的一方的表中的列名-->
   <association property="teacher"  column="{id=tid,name=tid}" javaType="Teacher"select="getTeacher"/>
</resultMap>
<!--
这里传递过来的id，只有一个属性的时候，下面可以写任何值
association中column多参数配置：
   column="{key=value,key=value}"
   其实就是键值对的形式，key是传给下个sql的取值名称，value是片段一中sql查询的字段名。
-->
<select id="getTeacher" resultType="teacher">
  select * from teacher where id = #{id} and name = #{name}
</select>
```

#### 5、测试

```java
@Test
    public void getStudent() {
        try(SqlSession sqlSession = MyBatisUtils.getSqlSession()){
            StudentMapper mapper = sqlSession.getMapper(StudentMapper.class);
            List<Student> students = mapper.getStudent();
            for(Student student : students){
                System.out.println(student.getId() +"\t"+ student.getName() +"\t"+ student.getTeacher().getName());
            }

        }
    }
```

### 4、按结果嵌套处理

除了上面这种方式，还有其他思路吗？

我们还可以按照结果进行嵌套处理；

#### 1、接口方法编写

```java
public List<Student> getStudents2();
```

#### 2、编写对应的mapper文件

```xml
<!--
按查询结果嵌套处理
思路：
   1. 直接查询出结果，进行结果集的映射
-->
<select id="getStudents2" resultMap="StudentTeacher2" >
  select s.id sid, s.name sname , t.name tname
  from student s,teacher t
  where s.tid = t.id
</select>

<resultMap id="StudentTeacher2" type="Student">
   <id property="id" column="sid"/>
   <result property="name" column="sname"/>
   <!--关联对象property 关联对象在Student实体类中的属性-->
   <association property="teacher" javaType="Teacher">
       <result property="name" column="tname"/>
   </association>
</resultMap>
```

#### 3、去mybatis-config文件中注入【此处应该处理过了】

#### 4、测试

```java
@Test
public void testGetStudents2(){
   SqlSession session = MybatisUtils.getSession();
   StudentMapper mapper = session.getMapper(StudentMapper.class);

   List<Student> students = mapper.getStudents2();

   for (Student student : students){
       System.out.println(
               "学生名:"+ student.getName()
                       +"\t老师:"+student.getTeacher().getName());
  }
}
```

### 5、小结

按照查询进行嵌套处理就像SQL中的子查询

按照结果进行嵌套处理就像SQL中的联表查询

## 10、一对多的处理

一对多的理解：

- 一个老师拥有多个学生
- 如果对于老师这边，就是一个一对多的现象，即从一个老师下面拥有一群学生（集合）！

### 1、实体类编写

```java
@Data
public class Student {
   private int id;
   private String name;
   private int tid;
}
@Data 
public class Teacher {
   private int id;
   private String name;
   //一个老师多个学生
   private List<Student> students;
}
```

..... 和之前一样，搭建测试的环境！



### 2、按结果嵌套处理

#### 1、TeacherMapper接口编写方法

```java
//获取指定老师，及老师下的所有学生
public Teacher getTeacher(int id);
```

#### 2、编写接口对应的Mapper配置文件

```xml
<mapper namespace="com.kuang.mapper.TeacherMapper">

   <!--
   思路:
       1. 从学生表和老师表中查出学生id，学生姓名，老师姓名
       2. 对查询出来的操作做结果集映射
           1. 集合的话，使用collection！
               JavaType和ofType都是用来指定对象类型的
               JavaType是用来指定pojo中属性的类型
               ofType指定的是映射到list集合属性中pojo的类型。
   -->
   <select id="getTeacher" resultMap="TeacherStudent">
      select s.id sid, s.name sname , t.name tname, t.id tid
      from student s,teacher t
      where s.tid = t.id and t.id=#{id}
   </select>

   <resultMap id="TeacherStudent" type="Teacher">
       <result  property="name" column="tname"/>
       <collection property="students" ofType="Student">
           <result property="id" column="sid" />
           <result property="name" column="sname" />
           <result property="tid" column="tid" />
       </collection>
   </resultMap>
</mapper>
```

#### 3、将Mapper文件注册到MyBatis-config文件中

```xml
<mappers>
   <mapper resource="mapper/TeacherMapper.xml"/>
</mappers>
```

#### 4、测试

```java
@Test
public void testGetTeacher(){
   SqlSession session = MybatisUtils.getSession();
   TeacherMapper mapper = session.getMapper(TeacherMapper.class);
   Teacher teacher = mapper.getTeacher(1);
   System.out.println(teacher.getName());
   System.out.println(teacher.getStudents());
}
```



### 3、按查询嵌套处理

#### 1、TeacherMapper接口编写方法

```java
public Teacher getTeacher2(int id);
```

#### 2、编写接口对应的Mapper配置文件

```xml
<select id="getTeacher2" resultMap="TeacherStudent2">
select * from teacher where id = #{id}
</select>
<resultMap id="TeacherStudent2" type="Teacher">
   <!--column是一对多的外键 , 写的是一的主键的列名-->
   <collection property="students" javaType="ArrayList" ofType="Student" column="id"select="getStudentByTeacherId"/>
</resultMap>
<select id="getStudentByTeacherId" resultType="Student">
  select * from student where tid = #{id}
</select>
```

#### 3、将Mapper文件注册到MyBatis-config文件中

#### 4、测试

```java
@Test
public void testGetTeacher2(){
   SqlSession session = MybatisUtils.getSession();
   TeacherMapper mapper = session.getMapper(TeacherMapper.class);
   Teacher teacher = mapper.getTeacher2(1);
   System.out.println(teacher.getName());
   System.out.println(teacher.getStudents());
}
```

### 4、小结

1、关联-association

2、集合-collection

3、所以association是用于一对一和多对一，而collection是用于一对多的关系

4、JavaType和ofType都是用来指定对象类型的

- JavaType是用来指定pojo中属性的类型
- ofType指定的是映射到list集合属性中pojo的类型。

**注意说明：**

1、保证SQL的可读性，尽量通俗易懂

2、根据实际要求，尽量编写性能更高的SQL语句

3、注意属性名和字段不一致的问题

4、注意一对多和多对一 中：字段和属性对应的问题

5、尽量使用Log4j，通过日志来查看自己的错误



## 11、一对多、多对一总结

### 一对多实体类：

```java
public class Teacher {
    private int id;
    private String name;
    // 一个老师  对应多个学生，所以是集合
    private List<Student> students;
}

public class Student {
    private int id;
    private String name;
    private int tid;// 老师的id
}
```

需求：查询每个老师信息，并查出门下的弟子信息

![image-20220101113509548](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220101113509548.png)

### 方式一：处理结果集的对应问题

**直接SQL该怎么写怎么写，返回结果对应处理**

**这里查询后，返回id、name都是能对应的，只有List<Student> students没办法对应，所以用一个==中介Map==**

- id 普通属性
  - property----类中的属性名   
  - column----查询结果伪表的字段名【配套对应==赋值给==property】

- collection 是集合   ofType 是集合中具体数据的（泛型）类型
  - property----类中的属性名
  - column----查询结果伪表的字段名【配套对应==赋值给==property】

```xml
<select id="getTeacherStu" resultMap="stuTeaMap">
    select t.`id` tid,t.`name` tname,s.`name` sname,s.`id` sid
    from student s,teacher t
    where s.tid=t.id and t.id=#{tid};
</select>

<resultMap id="stuTeaMap" type="teacher">
    <id property="id" column="tid"/>
    <id property="name" column="tname"/>
    <collection property="students" ofType="student">
        <result property="id" column="sid"/>
        <result property="name" column="sname"/>
    </collection>
</resultMap>
```

### 方式二：处理SQL语句，拆成能一一对应的

拆分成两个表的单独查询，设置==中介Map==

先查询主要目标teacher，id、name属性正常赋值

List<Student> students这个属性通过中介Map 单独调用另一个查询

- Property     类中属性名
- javaType     类的返回值类型
- ofType         集合中元素的数据类型（泛型）
- select           调用另一个查询
- column        另一个查询需要的参数，这里是当前map中的id信息，根据t老师的d查询学生

```xml
<select id="getTeacherStu" resultMap="myMap">
    select *
    from mybatis.teacher
    where id=#{tid}
</select>

<resultMap id="myMap" type="teacher">
    <id property="id" column="id"/>
    <collection property="students"  javaType="ArrayList" ofType="student" select="order" column="id"/>
</resultMap>

<select id="order" resultType="student">
    select *
    from mybatis.student
    where tid=#{id};
</select>
```

### 多对一实体类：

道理同上，不再赘述

```java
public class Student {
    private int id;
    private String name;
    //多个学生对应同一个老师
    private Teacher teacher;
}

public class Teacher {
    private int id;
    private String name;
}
```

需求：查询每个学生信息，并查出对应的老师信息

![image-20220101114207918](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220101114207918.png)

### 方式一：处理结果集的一一对应问题

官话：【按结果嵌套处理】

```xml
<select id="getStudents2" resultMap="调用哈哈" >
  select s.id sid, s.name sname , t.name tname
  from student s,teacher t
  where s.tid = t.id
</select>

<resultMap id="调用哈哈" type="Student">
   <id property="id" column="sid"/>
   <result property="name" column="sname"/>
   <!--关联对象property 关联对象在Student实体类中的属性-->
   <association property="teacher" javaType="Teacher">
       <result property="name" column="tname"/>
   </association>
</resultMap>
```



### 方式二：处理SQL语句，拆成能一一对应的

官话：【按查询嵌套处理】

```xml
<select id="getStudent" resultMap="student_teacher">
    select * from mybatis.student
</select>

<resultMap id="student_teacher" type="student">
    <result property="id" column="id"/>
    <result property="name" column="name"/>
    <!--
        一一对应的直接result就行了，但是要形成复杂的，id列，name列，老师列
        如果是返回对象：用association
        如果是返回集合：用collection
    -->
    <association property="teacher" column="tid" javaType="teacher" select="getTeacher"/>
</resultMap>

<select id="getTeacher" resultType="teacher">
    select * from mybatis.teacher where id=#{id}
</select>
```

## 12、动态SQL

### 1、介绍

什么是动态SQL：**动态SQL指的是根据不同的查询条件 , 生成不同的Sql语句.**

```properties
官网描述：
MyBatis 的强大特性之一便是它的动态 SQL。如果你有使用 JDBC 或其它类似框架的经验，你就能体会到根据不同条件拼接 SQL 语句的痛苦。例如拼接时要确保不能忘记添加必要的空格，还要注意去掉列表最后一个列名的逗号。利用动态 SQL 这一特性可以彻底摆脱这种痛苦。
虽然在以前使用动态 SQL 并非一件易事，但正是 MyBatis 提供了可以被用在任意 SQL 映射语句中的强大的动态 SQL 语言得以改进这种情形。
动态 SQL 元素和 JSTL 或基于类似 XML 的文本处理器相似。在 MyBatis 之前的版本中，有很多元素需要花时间了解。MyBatis 3 大大精简了元素种类，现在只需学习原来一半的元素便可。MyBatis 采用功能强大的基于 OGNL 的表达式来淘汰其它大部分元素。

  -------------------------------
  - if
  - choose (when, otherwise)
  - trim (where, set)
  - foreach
  -------------------------------
```

我们之前写的 SQL 语句都比较简单，如果有比较复杂的业务，我们需要写复杂的 SQL 语句，往往需要拼接，而拼接 SQL ，稍微不注意，由于引号，空格等缺失可能都会导致错误。

那么怎么去解决这个问题呢？这就要使用 mybatis 动态SQL，通过 if, choose, when, otherwise, trim, where, set, foreach等标签，可组合成非常灵活的SQL语句，从而在提高 SQL 语句的准确性的同时，也大大提高了开发人员的效率。

### 2、搭建环境

**新建一个数据库表：blog**

字段：id，title，author，create_time，views

```
CREATE TABLE `blog` (
`id` varchar(50) NOT NULL COMMENT '博客id',
`title` varchar(100) NOT NULL COMMENT '博客标题',
`author` varchar(30) NOT NULL COMMENT '博客作者',
`create_time` datetime NOT NULL COMMENT '创建时间',
`views` int(30) NOT NULL COMMENT '浏览量'
) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

1、创建Mybatis基础工程



![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7JISvrLfLvE3e9Wv1kpFL9qzPPOq4EuoibKKLvGve4vEicLpXeEHfz1flqX3ribyzpbjDlOGzziapTsIw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

2、IDutil工具类

```java
public class IDUtil {

   public static String genId(){
       return UUID.randomUUID().toString().replaceAll("-","");
  }
}
```

3、实体类编写  【注意set方法作用】

```java
import java.util.Date;

public class Blog {

   private String id;
   private String title;
   private String author;
   private Date createTime;
   private int views;
   //set，get....
}
```

4、编写Mapper接口及xml文件

```xml
public interface BlogMapper {
}
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
       PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
       "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.kuang.mapper.BlogMapper">

</mapper>
```

5、mybatis核心配置文件，下划线驼峰自动转换

```xml
<settings>
        <setting name="logImpl" value="LOG4J"/>
        <!--开启驼峰命名转换，就是数据库字段如果是create_id,字段使用驼峰命名createId
        这样就不用别名处理，开启这个配置后就能自动识别，仅限驼峰命名-->
        <setting name="mapUnderscoreToCamelCase" value="true"/>
    </settings>
<mappers>
 		<mapper resource="com/pledge/mapper/BlogMapper.xml"/>
</mappers>
```

6、插入初始数据

编写接口

```java
//新增一个博客
int addBlog(Blog blog);
```

sql配置文件

```java
<insert id="addBlog" parameterType="blog">
  insert into blog (id, title, author, create_time, views)
  values (#{id},#{title},#{author},#{createTime},#{views});
</insert>
```

初始化博客方法

```java
@Test
public void addInitBlog(){
   SqlSession session = MybatisUtils.getSession();
   BlogMapper mapper = session.getMapper(BlogMapper.class);

   Blog blog = new Blog();
   blog.setId(IDUtil.genId());
   blog.setTitle("Mybatis如此简单");
   blog.setAuthor("狂神说");
   blog.setCreateTime(new Date());
   blog.setViews(9999);

   mapper.addBlog(blog);

   blog.setId(IDUtil.genId());
   blog.setTitle("Java如此简单");
   mapper.addBlog(blog);

   blog.setId(IDUtil.genId());
   blog.setTitle("Spring如此简单");
   mapper.addBlog(blog);

   blog.setId(IDUtil.genId());
   blog.setTitle("微服务如此简单");
   mapper.addBlog(blog);

   session.close();
}
```

初始化数据完毕！



### 3、if 语句

<font color='red'>就是查询表信息，在where后面的筛选条件前后加if，如果传进来的参数有就加上，没有就不写，实现动态SQL。</font>

<font color='red'>参数全部通过Map来传，有几个传几个，没有传空Map相当于不写where语句</font>

**需求：根据作者名字和博客名字来查询博客！如果作者名字为空，那么只根据博客名字查询，反之，则根据作者名来查询**

1、编写接口类

```java
//需求1
List<Blog> queryBlogIf(Map map);
```

2、编写SQL语句

```xml
<!--需求1：
根据作者名字和博客名字来查询博客！
如果作者名字为空，那么只根据博客名字查询，反之，则根据作者名来查询
select * from blog where title = #{title} and author = #{author}
-->
<select id="queryBlogIf" parameterType="map" resultType="blog">
  select * from blog where
   <if test="title != null">
      title = #{title}
   </if>
   <if test="author != null">
      and author = #{author}
   </if>
</select>
```

3、测试

```java
@Test
public void testQueryBlogIf(){
   SqlSession session = MybatisUtils.getSession();
   BlogMapper mapper = session.getMapper(BlogMapper.class);

   HashMap<String, String> map = new HashMap<String, String>();
   map.put("title","Mybatis如此简单");
   map.put("author","狂神说");
   List<Blog> blogs = mapper.queryBlogIf(map);

   System.out.println(blogs);

   session.close();
}
```

这样写我们可以看到，如果 author 等于 null，那么查询语句为 select * from user where title=#{title},但是如果title为空呢？那么查询语句为 select * from user where and author=#{author}，这是错误的 SQL 语句，如何解决呢？请看下面的 where 语句！



### 4、Where

<font color='blue'>SQL语句中的where标签，相当于where关键字，这样SQL语句就不用写where</font>

- <font color='blue'>如果where内部的条件成立了他自动拼接一个where关键字</font>

- <font color='blue'>而且多个条件前边都加上and或者or，如果他是第一个，那么MyBatis会自己判断，如果and开头就默认给去掉and或者or</font>

修改上面的SQL语句；

```xml
<select id="queryBlogIf" parameterType="map" resultType="blog">
  select * from blog
   <where>
       <if test="title != null">
          and title = #{title}
       </if>
       <if test="author != null">
          and author = #{author}
       </if>
   </where>
</select>
```

这个“where”标签会知道如果它包含的标签中有返回值的话，它就插入一个‘where’。此外，如果标签返回的内容是以AND 或OR 开头的，则它会剔除掉。



### 5、Set

<font color='red'>set标签也是一样，直接在SQL语句写set关键字的时候引用set标签，后边全加上逗号，他会自己识别，多余的自动去掉了</font>

1、编写接口方法

```java
int updateBlog(Map map);
```

2、sql配置文件

```xml
<!--注意set是用的逗号隔开-->
<update id="updateBlog" parameterType="map">
  update blog
     <set>
         <if test="title != null">
            title = #{title},
         </if>
         <if test="author != null">
            author = #{author}
         </if>
     </set>
  where id = #{id};
</update>
```

3、测试

```java
@Test
public void testUpdateBlog(){
   SqlSession session = MybatisUtils.getSession();
   BlogMapper mapper = session.getMapper(BlogMapper.class);

   HashMap<String, String> map = new HashMap<String, String>();
   map.put("title","动态SQL");
   map.put("author","秦疆");
   map.put("id","9d6a763f5e1347cebda43e2a32687a77");

   mapper.updateBlog(map);


   session.close();
}
```



### 6、choose语句

有时候，我们不想用到所有的查询条件，只想选择其中的一个，查询条件有一个满足即可，使用 choose 标签可以解决此类问题，==类似于 Java 的 switch 语句==

1、编写接口方法

```java
List<Blog> queryBlogChoose(Map map);
```

2、sql配置文件

```xml
<select id="queryBlogChoose" parameterType="map" resultType="blog">
  select * from blog
   <where>
       <choose>
           <when test="title != null">
              and title = #{title}
           </when>
           <when test="author != null">
              and author = #{author}
           </when>
           <otherwise>
              and views = #{views}
           </otherwise>
       </choose>
   </where>
</select>
```

3、测试类

```java
@Test
public void testQueryBlogChoose(){
   SqlSession session = MybatisUtils.getSession();
   BlogMapper mapper = session.getMapper(BlogMapper.class);

   HashMap<String, Object> map = new HashMap<String, Object>();
   map.put("title","Java如此简单");
   map.put("author","狂神说");
   map.put("views",9999);
   List<Blog> blogs = mapper.queryBlogChoose(map);

   System.out.println(blogs);

   session.close();
}
```



### 7、SQL片段

有时候可能某个 sql 语句我们用的特别多，为了增加代码的重用性，简化代码，我们需要将这些代码抽取出来，然后使用时直接调用。

**提取SQL片段：**

```xml
<sql id="if-title-author">
   <if test="title != null">
      title = #{title}
   </if>
   <if test="author != null">
      and author = #{author}
   </if>
</sql>
```

**引用SQL片段：**

```xml
<select id="queryBlogIf" parameterType="map" resultType="blog">
  select * from blog
   <where>
       <!-- 引用 sql 片段，如果refid 指定的不在本文件中，那么需要在前面加上 namespace -->
       <include refid="if-title-author"></include>
       <!-- 在这里还可以引用其他的 sql 片段 -->
   </where>
</select>
```

注意：

①、最好基于 单表来定义 sql 片段，提高片段的可重用性

②、==在 sql 片段中不要包括 where==



### 8、Foreach

将数据库中前三个数据的id修改为1,2,3；

需求：我们需要查询 blog 表中 id 分别为1,2,3的博客信息

1、编写接口

```java
List<Blog> queryBlogForeach(Map map);
```

2、编写SQL语句

```xml
<select id="queryBlogForeach" parameterType="map" resultType="blog">
  select * from blog
   <where>
       <!--
       collection:指定输入对象中的集合属性
       item:每次遍历生成的对象
       open:开始遍历时的拼接字符串
       close:结束时拼接的字符串
       separator:遍历对象之间需要拼接的字符串
       select * from blog where 1=1 and (id=1 or id=2 or id=3)
     -->
       <foreach collection="ids"  item="id" open="(" close=")" separator="or">
          id=#{id}
       </foreach>
   </where>
</select>
```

3、测试

```java
@Test
public void queryByForeach(){
    try(SqlSession sqlSession = MytBatisUtils.getSqlSession()){
        BlogMapper mapper = sqlSession.getMapper(BlogMapper.class);
        HashMap<String, Object> map = new HashMap<>();
        ArrayList<Integer> list = new ArrayList<>();
        list.add(1);
        list.add(4);
        list.add(3);
        map.put("ids",list);

        List<Blog> blogs = mapper.queryByForeach(map);
        blogs.forEach(System.out::println);
    }
}
```

小结：其实动态 sql 语句的编写往往就是一个拼接的问题，为了保证拼接准确

我们最好首先要写原生的 sql 语句出来，然后在通过 mybatis 动态sql 对照着改，防止出错。多在实践中使用才是熟练掌握它的技巧。



> 简介

1、什么是缓存 [ Cache ]？

- 存在内存中的临时数据。
- 将用户经常查询的数据放在缓存（内存）中，用户去查询数据就不用从磁盘上(关系型数据库数据文件)查询，从缓存中查询，从而提高查询效率，解决了高并发系统的性能问题。

2、为什么使用缓存？

- 减少和数据库的交互次数，减少系统开销，提高系统效率。

3、什么样的数据能使用缓存？

- 经常查询并且不经常改变的数据。



## 13、Mybatis缓存

- MyBatis包含一个非常强大的查询缓存特性，它可以非常方便地定制和配置缓存。缓存可以极大的提升查询效率。

- MyBatis系统中默认定义了两级缓存：**一级缓存**和**二级缓存**

- - 默认情况下，只有一级缓存开启。（SqlSession级别的缓存，也称为本地缓存）
  - 二级缓存需要手动开启和配置，他是基于namespace级别的缓存。
  - 为了提高扩展性，MyBatis定义了缓存接口Cache。我们可以通过实现Cache接口来自定义二级缓存



### 1、一级缓存

一级缓存也叫本地缓存：

- 与数据库同一次会话期间查询到的数据会放在本地缓存中。
- 以后如果需要获取相同的数据，直接从缓存中拿，没必须再去查询数据库；



> 测试

1、在mybatis中加入日志，方便测试结果

2、编写接口方法

```java
//根据id查询用户
User queryUserById(@Param("id") int id);
```

3、接口对应的Mapper文件

```xml
<select id="queryUserById" resultType="user">
  select * from user where id = #{id}
</select>
```

4、测试

```java
@Test
public void getUserById() {
    try(SqlSession sqlSession = MyBatisUtils.getSqlSession()){
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
      	// 第一次，查询id=3
        System.out.println(mapper.getUserById(3));
      	// 第二次，查询id=3
        System.out.println(mapper.getUserById(3));
    }
}
```

5、结果分析

SQL语句只执行了一次，直接在缓存中查出来的

![image-20220101192219572](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220101192219572.png)



### 2、一级缓存失效的四种情况

一级缓存是SqlSession级别的缓存，是一直开启的，我们关闭不了它；

一级缓存失效情况：没有使用到当前的一级缓存，效果就是，还需要再向数据库中发起一次查询请求！

#### 1、sqlSession不同

```java
@Test
public void testQueryUserById(){
   SqlSession session = MybatisUtils.getSession();
   SqlSession session2 = MybatisUtils.getSession();
   UserMapper mapper = session.getMapper(UserMapper.class);
   UserMapper mapper2 = session2.getMapper(UserMapper.class);

   User user = mapper.queryUserById(1);
   System.out.println(user);
   User user2 = mapper2.queryUserById(1);
   System.out.println(user2);
   System.out.println(user==user2);

   session.close();
   session2.close();
}
```

观察结果：发现发送了两条SQL语句！

结论：**每个sqlSession中的缓存相互独立**

#### 2、sqlSession相同，查询条件不同

```java
@Test
public void getUserById() {
    try(SqlSession sqlSession = MyBatisUtils.getSqlSession()){
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        System.out.println(mapper.getUserById(1));
        System.out.println(mapper.getUserById(3));
    }
}
```

观察结果：发现发送了两条SQL语句！很正常的理解

结论：**当前缓存中，不存在这个数据**

![image-20220101192711395](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220101192711395.png)

#### 3、sqlSession相同，两次查询之间执行了增删改操作！

增加方法

```java
//修改用户
int updateUser(Map map);
```

编写SQL

```xml
<update id="updateUser" parameterType="map">
  update user set name = #{name} where id = #{id}
</update>
```

测试

```java
@Test
public void testQueryUserById(){
   SqlSession session = MybatisUtils.getSession();
   UserMapper mapper = session.getMapper(UserMapper.class);

   User user = mapper.queryUserById(1);
   System.out.println(user);

   HashMap map = new HashMap();
   map.put("name","kuangshen");
   map.put("id",4);
   mapper.updateUser(map);

   User user2 = mapper.queryUserById(1);
   System.out.println(user2);

   System.out.println(user==user2);

   session.close();
}
```

观察结果：查询在中间执行了增删改操作后，重新执行了

结论：**因为增删改操作可能会对当前数据产生影响**

#### 4、sqlSession相同，手动清除一级缓存

```java
@Test
public void getUserById() {
    try(SqlSession sqlSession = MyBatisUtils.getSqlSession()){
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        System.out.println(mapper.getUserById(3));
        // 手动清理缓存
        sqlSession.clearCache();
        System.out.println(mapper.getUserById(3));
    }
}
```

一级缓存就是一个map

![image-20220101192847698](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220101192847698.png)

### 3、二级缓存

- 二级缓存也叫全局缓存，一级缓存作用域太低了，所以诞生了二级缓存

- 基于namespace级别的缓存，一个名称空间，对应一个二级缓存；

- 工作机制

- - ==一个会话查询一条数据，这个数据就会被放在当前会话的一级缓存中；==
  - 如果当前会话关闭了，这个会话对应的一级缓存就没了；但是我们想要的是，==会话关闭了，一级缓存中的数据被保存到二级缓存中；==
  - 新的会话查询信息，就可以从二级缓存中获取内容；
  - 不同的mapper查出的数据会放在自己对应的缓存（map）中；



> 使用步骤

1、开启全局缓存 【mybatis-config.xml】

```xml
<setting name="cacheEnabled" value="true"/>
```

2、去每个mapper.xml中配置使用二级缓存，这个配置非常简单；【xxxMapper.xml】

- eviction               	 创建了一个 FIFO 缓存
- flushInterval  	      每隔 60 秒刷新
- size                          最多可以存储结果对象或列表的 512 个引用
- readOnly                 返回的对象被认为是只读的

因此对它们进行修改可能会在不同线程中的调用者产生冲突。

==注意：==使用空标签时，因为没有了缓存策略FIFO，所以要实体类实现序列化接口

否则会报错：```Cause: java.io.NotSerializableException: com.pledge.pojo.User```

![image-20220101221010686](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220101221010686.png)

```xml
<mapper namespace = “com.pledge.mapper.UserMapper” > 
   	可以啥也不写，直接空标签就行【空标签要先序列化实体类】
    <cache/>
</mapper>

<mapper namespace = “com.pledge.mapper.UserMapper” > 
    也可以设置部分属性
    	<cache
         eviction="FIFO"
         flushInterval="60000"
         size="512"
         readOnly="true"/> 
</mapper>

```

3、代码测试

- 所有的实体类先实现序列化接口，否则会报错

  ```java
  Cause: java.io.NotSerializableException: com.pledge.pojo.User
  ```

  

- 测试代码

```java
@Test
public void testQueryUserById(){
   SqlSession session = MybatisUtils.getSession();
   SqlSession session2 = MybatisUtils.getSession();

   UserMapper mapper = session.getMapper(UserMapper.class);
   UserMapper mapper2 = session2.getMapper(UserMapper.class);

   User user = mapper.queryUserById(1);
   System.out.println(user);
   session.close();

   User user2 = mapper2.queryUserById(1);
   System.out.println(user2);
   System.out.println(user==user2);

   session2.close();
}
```

> 结论

- 只要开启了二级缓存，我们在同一个Mapper中的查询，可以在二级缓存中拿到数据
- 查出的数据都会被默认先放在一级缓存中
- 只有会话提交或者关闭以后，一级缓存中的数据才会转到二级缓存中



### 4、缓存原理图

先检查二级缓存，然后到一级缓存，再找不到就去数据库

![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7KickRVspms8t4ZU0jXovPT2egdNicaJuVnzMYxibyYFvB0COWW4sgDhHPqvFbG9F9KS1vX7ibIMNqefg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

### 5、EhCache



![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7KickRVspms8t4ZU0jXovPT29RfsqgE50IOicMbHPzceX3r2BWn2U9MZ29rpQAy3gtQBnWpveiaRr2lw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

第三方缓存实现--EhCache: 查看百度百科

Ehcache是一种广泛使用的java分布式缓存，用于通用缓存；

要在应用程序中使用Ehcache，需要引入依赖的jar包

```xml
<!-- https://mvnrepository.com/artifact/org.mybatis.caches/mybatis-ehcache -->
<dependency>
   <groupId>org.mybatis.caches</groupId>
   <artifactId>mybatis-ehcache</artifactId>
   <version>1.1.0</version>
</dependency>
```

在mapper.xml中使用对应的缓存即可

```xml
<mapper namespace = “org.acme.FooMapper” > 
   <cache type = “org.mybatis.caches.ehcache.EhcacheCache” /> 
</mapper>
```

编写ehcache.xml文件放在resources目录下，如果在加载时未找到/ehcache.xml资源或出现问题，则将使用默认配置。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<ehcache xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="http://ehcache.org/ehcache.xsd"
        updateCheck="false">
   <!--
      diskStore：为缓存路径，ehcache分为内存和磁盘两级，此属性定义磁盘的缓存位置。参数解释如下：
      user.home – 用户主目录
      user.dir – 用户当前工作目录
      java.io.tmpdir – 默认临时文件路径
    -->
   <diskStore path="./tmpdir/Tmp_EhCache"/>
   
   <defaultCache
           eternal="false"
           maxElementsInMemory="10000"
           overflowToDisk="false"
           diskPersistent="false"
           timeToIdleSeconds="1800"
           timeToLiveSeconds="259200"
           memoryStoreEvictionPolicy="LRU"/>

   <cache
           name="cloud_user"
           eternal="false"
           maxElementsInMemory="5000"
           overflowToDisk="false"
           diskPersistent="false"
           timeToIdleSeconds="1800"
           timeToLiveSeconds="1800"
           memoryStoreEvictionPolicy="LRU"/>
   <!--
      defaultCache：默认缓存策略，当ehcache找不到定义的缓存时，则使用这个缓存策略。只能定义一个。
    -->
   <!--
     name:缓存名称。
     maxElementsInMemory:缓存最大数目
     maxElementsOnDisk：硬盘最大缓存个数。
     eternal:对象是否永久有效，一但设置了，timeout将不起作用。
     overflowToDisk:是否保存到磁盘，当系统当机时
     timeToIdleSeconds:设置对象在失效前的允许闲置时间（单位：秒）。仅当eternal=false对象不是永久有效时使用，可选属性，默认值是0，也就是可闲置时间无穷大。
     timeToLiveSeconds:设置对象在失效前允许存活时间（单位：秒）。最大时间介于创建时间和失效时间之间。仅当eternal=false对象不是永久有效时使用，默认是0.，也就是对象存活时间无穷大。
     diskPersistent：是否缓存虚拟机重启期数据 Whether the disk store persists between restarts of the Virtual Machine. The default value is false.
     diskSpoolBufferSizeMB：这个参数设置DiskStore（磁盘缓存）的缓存区大小。默认是30MB。每个Cache都应该有自己的一个缓冲区。
     diskExpiryThreadIntervalSeconds：磁盘失效线程运行时间间隔，默认是120秒。
     memoryStoreEvictionPolicy：当达到maxElementsInMemory限制时，Ehcache将会根据指定的策略去清理内存。默认策略是LRU（最近最少使用）。你可以设置为FIFO（先进先出）或是LFU（较少使用）。
     clearOnFlush：内存数量最大时是否清除。
     memoryStoreEvictionPolicy:可选策略有：LRU（最近最少使用，默认策略）、FIFO（先进先出）、LFU（最少访问次数）。
     FIFO，first in first out，这个是大家最熟的，先进先出。
     LFU， Less Frequently Used，就是上面例子中使用的策略，直白一点就是讲一直以来最少被使用的。如上面所讲，缓存的元素有一个hit属性，hit值最小的将会被清出缓存。
     LRU，Least Recently Used，最近最少使用的，缓存的元素有一个时间戳，当缓存容量满了，而又需要腾出地方来缓存新的元素的时候，那么现有缓存元素中时间戳离当前时间最远的元素将被清出缓存。
  -->

</ehcache>
```



合理的使用缓存，可以让我们程序的性能大大提升！



























