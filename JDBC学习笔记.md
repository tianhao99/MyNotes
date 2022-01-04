## 第 1 章 概述

在 Java 中， 数据库存取技术可分为如下几类：

-  JDBC 直接访问数据库
-  JDO 技术（Java Data Object）
-  第三方 O/R 工具， 如 Hibernate, Mybatis 等

JDBC 是 java 访问数据库的基石， JDO, Hibernate 等只是更好的封装了 JDBC。  

### 1、 什么是 JDBC

JDBC(Java Database Connectivity)是一个<font color='red'>独立于特定数据库管理系统（ DBMS） 、 通用的 SQL 数据库存取和操作的公共接口</font>（一组 API）,定义了用来访问数据库的标准 Java 类库， 使用这个类库可以以一种标准的方法、 方便地访问数据库资源

JDBC 为访问不同的数据库提供了一种<font color='red'>统一的途径</font>， 为开发者屏蔽了一些细节问题。

JDBC 的目标是使 Java 程序员使用 JDBC 可以连接任何<font color='red'>提供了 JDBC 驱动程序的数据库系统</font>， 这样就使得程序员无需对特定的数据库系统的特点有过多的了解， 从而大大简化和加快了开发过程。

如果没有 JDBC， 那么 Java 程序访问数据库时是这样的：  

**没有jbdc**

![image-20211019195228216](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211019195228216-16346443495641.png)

**改装后**

![image-20211019195235207](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211019195447471-16346444887483.png)

**实际上：**![image-20211019195447471](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211019195615124-16346445761784.png)



**<font color='red'>结论：</font>**

JDBC 是 SUN 公司（Oracle）提供一套用于数据库操作的接口 API， Java 程序员只需要面向这套接口编程即可。

不同的数据库厂商， 需要针对这套接口， 提供不同实现。 不同的实现的集合， 即为不同数据库的驱动。  



### 2、 JDBC API

JDBC API 是一系列的接口， 它统一和规范了应用程序与数据库的连接、 执行 SQL 语句， 并到得到返回结果等各类操作。 声明在 java.sql 与 javax.sql 包中。  

![image-20211019195615124](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211019195235207-16346443569982.png)

### 3、 JDBC 程序编写步骤  

![image-20211019195700989](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211019200030357-16346448324046.png)



## 第 2 章 获取数据库连接

### 1、 引入 JDBC 驱动程序

#### 1.1 如何获取 JDBC 驱动程序

驱动程序由数据库提供商提供下载。
MySQL 的驱动下载地址： http://dev.mysql.com/downloads/

MySQL8.0数据库驱动jar包下载地址：https://dev.mysql.com/downloads/file/?id=496589

#### 1.2 如何在 Java Project 项目应用中添加数据库驱动 jar  

![image-20211019200030357](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211019200220130-16346449418807.png)

idea中：方式一：

![image-20211019200220130](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211019200246534-16346449675468.png)

![image-20211019200246534](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211019195700989-16346446220905.png)

**方式二：也可以直接右键jar包，Add as Library。**

**注意：** 如果是 Dynamic Web Project（ 动态的 web 项目） 话， 则是把驱动 jar 放到 WebContent（ 有的开发工具叫WebRoot） 目录中的 WEB-INF 目录中的 lib 目录下即可  

![image-20211019200542053](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211019200542053-16346451431469.png)



### 2、 加载并注册驱动

加载并注册驱动：

- 加载驱动， 把驱动类加载到内存
- 注册驱动， 把驱动类的对象交给 DriverManager 管理， 用于后面创建连接等使用。

#### 2.1 Driver 接口

Java.sql.Driver 接口是所有 JDBC 驱动程序需要实现的接口。 这个接口是提供给数据库厂商使用的， 不同数据库
厂商提供不同的实现。

- MySQL： com.mysql.cj.jdbc.Driver
- SQLServer： com.microsoft.sqlserver.jdbc.SQLServerDriver
- Oracle： oracle.jdbc.driver.OracleDriver

#### 2.2 编写加载与注册驱动的代码

- **直接创建 Driver 接口的实现类对象**

```java
Driver driver = new com.mysql.cj.jdbc.Driver();
//因为与 mysql 驱动包中的类发生直接依赖， 所以这样可移植性不够好
```

- **DriverManager 类的 registerDriver()**

 - 在实际开发中， 程序中不直接去访问实现了 Driver 接口的类， 而是由驱动程序管理器类(java.sql.DriverManager)去调用这些 Driver 实现。

  - DriverManager 类是驱动程序管理器类， 负责管理驱动程序。  
  - 通常不用显式调用 DriverManager 类的 registerDriver() 方法来注册驱动程序类的实例。  

```java
//DriverManager.registerDriver()方式注册驱动， 还是依赖
DriverManager.registerDriver(new com.mysql.jdbc.Driver());
```

- **Class.forName()或 ClassLoader 对象.loadClass()**

	- 因 为 Driver 接 口 的 驱 动 程 序 类 都 包 含 了 静 态 代 码 块 ， 在 这 个 静 态 代 码 块 中 ， 会 调 用
		DriverManager.registerDriver() 方法来注册自身的一个实例， 所以可以换一种方式来加载驱动。 （ 即只要想办法让驱动类的这段静态代码块执行即可注册驱动类， 而要让这段静态代码块执行， 只要让该类被类加载器加载即可）  

![image-20211019213656046](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211019213656046-16346506175041.png)

调用 Class 类的静态方法 forName()， 向其传递要加载的 JDBC 驱动的类名

```java
//1、 通过反射， 加载与注册驱动类， 解耦合（不直接依赖）
Class.forName("com.mysql.jdbc.Driver");


//2、 通过类加载器加载驱动类， 解耦合（不直接依赖）
ClassLoader.getSystemClassLoader().loadClass("com.mysql.jdbc.Driver");
```

- **服务提供者框架（例如： JDBC 的驱动程序） 自动注册（有版本要求）**
	- 符合 JDBC 4.0 规范的驱动程序包含了一个文件 META-INF/services/java.sql.Driver， 在这个文件中提供了 JDBC 驱动实现的类名。
	-  例如： mysql-connector-java-5.1.40-bin.jar 文件中就可以找到 java.sql.Driver 文件， 用文本编辑器打开文件就可以看到： com.mysql.jdbc.Driver 类。  

![image-20211019213814751](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211019213842805-16346507241183.png)



JVM 的服务提供者框架在启动应用时就会注册服务， 例如： MySQL 的 JDBC 驱动就会被注册， 而原代码中的
Class.forName("com.mysql.jdbc.Driver")仍然可以存在， 但是不会起作用。  

**但是注意 mysql-connector-java-5.0.8-bin.jar 版本的 jar 中没有， 如下**  

![image-20211019213842805](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211019214110909-16346508721264.png)



### 3、获取数据库链接

可以通过 DriverManager 类建立到数据库的连接 Connection：

DriverManager 试图从已注册的 JDBC 驱动程序集中选择一个适当的驱动程序。  

- public static Connection getConnection(String url)
- public static Connection getConnection(String url,String user, String password)
- public static Connection getConnection(String url,Properties info)  

#### 3.1 JDBC URL

JDBC URL 用于标识一个被注册的驱动程序， 驱动程序管理器通过这个 URL 选择正确的驱动程序， 从而建立到数据库的连接。

JDBC URL 的标准由三部分组成， 各部分间用冒号分隔。

**jdbc:<子协议>:<子名称>**

- **协议：** JDBC URL 中的协议总是 jdbc
- **子协议：** 子协议用于标识一个数据库驱动程序
- **子名称：** 一种标识数据库的方法。 子名称可以依不同的子协议而变化， 用子名称的目的是为了定位数据库提供足够的信息
- 例如：![image-20211019214110909](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211019213814751-16346506958152.png)
- MySQL 的连接 URL 编写方式：
	- jdbc:mysql://主机名称:mysql 服务端口号/数据库名称?参数=值&参数=值
	- jdbc:mysql://localhost:3306/库名
	- <font color='red'>**jdbc:mysql://localhost:3306/city99?serverTimezone=GMT%2B8**</font>
	- MySQL8.0版本以上调整东八区可用【如上】
	- jdbc:mysql://localhost:3306/库名?useUnicode=true&characterEncoding=utf8
	- jdbc:mysql://localhost:3306/库名?user=root&password=123456
- Oracle9i:
	- jdbc:oracle:thin:@主机名称:oracle 服务端口号:数据库名称
	- jdbc:oracle:thin:@localhost:1521:testdb
- SQLServer
	- jdbc:sqlserver://主机名称:sqlserver 服务端口号:DatabaseName=数据库名称
	- jdbc:sqlserver://localhost:1433:DatabaseName=testdb  

```java
//1、 加载与注册驱动
Class.forName("com.mysql.jdbc.Driver");
//2、 获取数据库连接
String url = "jdbc:mysql://localhost:3306/test";
Connection conn = DriverManager.getConnection(url, "root", "root");
//硬编码
```

#### 3.2 jdbc.properties

在 src 下建立文件 jdbc.properties， 当然也可以是其他名字， 只不过这里为了见名知意取这个名通常至少应该包括 "user" 和 "password" 属性  

```properties
#key=value
driver=com.mysql.jdbc.Driver
url=jdbc:mysql://localhost:3306/test
user=root
password=root
```

#### 3.3 连接方式一

```java
//连接数据库方式一：
@Test
public void testConnection() throws SQLException {
    //1、获取driver的实现类对象
    Driver driver = new com.mysql.cj.jdbc.Driver();

    /*
    * url:"jdbc:mysql://localhost:3306/city99?serverTimezone=GMT%2B8"
    * jdbc:mysql:协议
    * localhost：ip地址
    * 3306：默认的mysql的端口号
    * city99：数据库名称
    * serverTimezone=GMT%2B8：修改时区为东八区
    * */
    //2、提供要连接的数据库
    String url = "jdbc:mysql://localhost:3306/city99?serverTimezone=GMT%2B8";
    //3、提供连接需要的用户名和密码
    Properties info = new Properties();
    info.setProperty("user","root");
    info.setProperty("password","123456");
    //4、获取连接
    Connection con = driver.connect(url,info);
    System.out.println(con);
}
```



#### 3.4 连接方式二

```java
//连接数据库方式二：迭代方式一【使用反射】
//在如下程序中不出现第三方的api，使得程序具有更好的可移植性
@Test
public void testConnection2() throws Exception {
    //1、获取driver的实现类对象
    Class clazz = Class.forName("com.mysql.cj.jdbc.Driver");
    Driver driver = (Driver) clazz.getDeclaredConstructor().newInstance();
    //2、提供要连接的数据库
    String url = "jdbc:mysql://localhost:3306/city99?serverTimezone=GMT%2B8";
    //3、提供连接需要的用户名和密码
    Properties info = new Properties();
    info.setProperty("user","root");
    info.setProperty("password","123456");
    //4、获取连接
    Connection con = driver.connect(url,info);
    System.out.println(con);
}
```

#### 3.5 连接方式三

```java
//连接数据库方式三：迭代方式二【使用DriverManager替换Driver】
    @Test
    public void testConnection3() throws Exception {
        //1、获取Driver实现类对象
        Class clazz = Class.forName("com.mysql.cj.jdbc.Driver");
        Driver driver = (Driver) clazz.getDeclaredConstructor().newInstance();
        //2、提供另外3个连接的基本信息
        String url = "jdbc:mysql://localhost:3306/city99?serverTimezone=GMT%2B8";
        String user = "root";//账号密码也可以还用properties封装，getConnection也提供了相应的构造器
        String password = "123456";
        //3、注册驱动
//        DriverManager.registerDriver(driver); //此步可以省略，
        //4、获取连接
        Connection con = DriverManager.getConnection(url,user,password);
        System.out.println(con);
    }
```

#### 3.6 连接方式四

```java
//连接数据库方式四：优化方式三
@Test
public void testConnection4() throws Exception {

    //1、提供另外3个连接的基本信息
    String url = "jdbc:mysql://localhost:3306/city99?serverTimezone=GMT%2B8";
    String user = "root";//账号密码也可以还用properties封装，getConnection也提供了相应的构造器
    String password = "123456";
    //2、获取Driver实现类对象
    Class.forName("com.mysql.cj.jdbc.Driver");

    //3、获取连接
    Connection con = DriverManager.getConnection(url,user,password);
    System.out.println(con);
}
```



此方法为什么可以不注册驱动呢？直接加载驱动就行，因为在MySQL的Driver实现类的源码替我们做了

源码如下：

```java
public class Driver extends NonRegisteringDriver implements java.sql.Driver {
    //
    // Register ourselves with the DriverManager
    //
    static {
        try {
            java.sql.DriverManager.registerDriver(new Driver());
        } catch (SQLException E) {
            throw new RuntimeException("Can't register driver!");
        }
    }

    /**
     * Construct a new driver and register it with DriverManager
     * 
     * @throws SQLException
     *             if a database error occurs.
     */
    public Driver() throws SQLException {
        // Required for Class.forName().newInstance()
    }
}
```



#### 3.7 连接方式五【最终版】

将需要连接的数据库的4个基本信息声明在配置文件中，通过读取配置文件的方式，获取连接信息

**好处：**

- 实现了<font color='red'>代码和数据的分离</font>，实现了<font color='red'>解耦</font>
- 如果需要修改配置文件信息，【如更改数据库名】，可以<font color='red'>避免程序重新打包。</font>

```java
public class ConnectionTest {
	//连接数据库方式五：最终版
    @Test
    public void testConnection5() throws Exception {//记得抛异常

        //1、读取配置文件中的4个信息
        InputStream is = ClassLoader.getSystemClassLoader().getResourceAsStream("jdbc.properties");
        Properties pro = new Properties();
        pro.load(is);

        String user = pro.getProperty("user");
        String password = pro.getProperty("password");
        String url = pro.getProperty("url");
        String driverClass = pro.getProperty("driverClass");

        //2、加载驱动
        Class.forName(driverClass);
        //3、获取连接
        Connection con = DriverManager.getConnection(url,user,password);
        System.out.println(con);
    }
}
```

**jbdc.properties文件**

```properties
user=root
password=123456
url=jdbc:mysql://localhost:3306/city99?serverTimezone=GMT%2B8
driverClass=com.mysql.cj.jdbc.Driver
```



## 第 3 章 使用PreparedStatement实现CRUD操作

### 1、操作和访问数据库

- 数据库连接被用于向数据库服务器发送命令和SQL语句，并接受数据库服务器的返回结果，其实一个数据库连接就是一个Socket连接
- 在java.sql 包中有3个接口分别定义了对数据库的调用的不同方式
	- Statement：用于执行静态SQL语句并返回它所生成结果的对象
	- PrepatedStatement：SQL语句被预编译并存储在此对象中，可以使用此对象多次高效地执行该语句
	- CallableStatement：用于执行SQL存储过程

### 2、使用Statement操作数据表的弊端

- 通过调用Connection对象的createStatement() 方法创建该对象。该对象用于执行静态的SQL语句，并返回执行结果

- Statement 接口中定义了以下方法用于执行SQL语句：

```java

int excuteUpdate(String sql);//执行更新操作insert、update、delete
ResultSet executeQuery(String sql);//执行查询操作select

```

- 但是使用Statement操作数据表存在弊端

	 - 问题一：存在拼串操作、繁琐
	- 问题二：存在SQL注入问题

- SQL 注入是利用某些系统没有对用户输入的数据进行充分检查，而在用户输入数据中注入非法的SQL语句段或命令，从而利用系统的SQL引擎完成恶意行为的做法，如：

~~~sql
```sql
-- 要求传入SQL语句字符串，正确版本
select user,password from user_table where user='a' and password='1234';

-- 转成字符串【一般用户密码需要用户输入，所以定义变量】【这时就要拼接字符串操作】
str = "select user,password from user_table where user='"+ user+"' and password='"+password+"';"

-- SQL注入问题
str = "select user,password from user_table where user='user'or1=' and password='or'1'='1';"
-- 输入用户名为：user'or 1=     密码为：or'1'='1【此时用户输入必须是scan.nextLine()录入整行数据】

-- 实际传入的SQL语句为
select user,password from user_table where user='user'or 1='and password=' or '1'='1';

变成user=user或者1='and password='或者'1'='1'，三个条件只要有一个成立，就能进入数据库，而此时第三个条件'1'='1'是必定成立的，所以存在SQL注入问题
```
~~~

- 对于java而言，要防范SQL注入，只要用PreparedStatement（从Statement扩展而来）取代Statement就可以了。

综上：![image-20211021202800277](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211026172011554-16352400129482.png)

### 3、PreparedStatement的使用

#### 3.1 PreparedStatement介绍

- 可以通过调用 Connection 对象的 **preparedStatement(String sql)** 方法获取 PreparedStatement 对象

- **PreparedStatement 接口是 Statement 的子接口，它表示一条预编译过的 SQL 语句**

- PreparedStatement 对象所代表的 SQL 语句中的参数用问号(?)来表示，调用 PreparedStatement 对象的 setXxx() 方法来设置这些参数. setXxx() 方法有两个参数，第一个参数是要设置的 SQL 语句中的参数的索引(从 1 开始)，第二个是设置的 SQL 语句中的参数的值

#### 3.2 PreparedStatement vs Statement

- 代码的可读性和可维护性。
- **PreparedStatement 能最大可能提高性能：**
	- DBServer会对**预编译**语句提供性能优化。<font color='red'>因为预编译语句有可能被重复调用，所以语句在被DBServer的编译器编译后的执行代码被缓存下来，那么下次调用时只要是相同的预编译语句就不需要编译，只要将参数直接传入编译过的语句执行代码中就会得到执行</font>。
	- 在statement语句中,即使是相同操作但因为数据内容不一样,所以整个语句本身不能匹配,没有缓存语句的意义.事实是没有数据库会对普通语句编译后的执行代码缓存。这样<u>每执行一次都要对传入的语句编译一次。</u>
	- (语法检查，语义检查，翻译成二进制命令，缓存)
- <font color='red'>**PreparedStatement 如何防止 SQL 注入** </font>
	- 因为预编译，已经将语法格式固定，占位符传入的只是参数值，不会引起SQL注入问题
	- 而Statement没有预编译，参数传入后，统一成一句SQL语句，进行编译，这样会引起歧义，导致SQL注入问题

#### 3.3 Java与SQL对应数据类型转换表

| Java类型           | SQL类型                  |
| ------------------ | ------------------------ |
| boolean            | BIT                      |
| byte               | TINYINT                  |
| short              | SMALLINT                 |
| int                | INTEGER                  |
| long               | BIGINT                   |
| String             | CHAR,VARCHAR,LONGVARCHAR |
| byte   array       | BINARY  ,    VAR BINARY  |
| java.sql.Date      | DATE                     |
| java.sql.Time      | TIME                     |
| java.sql.Timestamp | TIMESTAMP                |



#### 3.4封装成连接工具类

<font color='red'>**因为这一系列操作过于程序化，完全可以封装起来，做成一个工具类！！!**</font>

**工具类：**

```java
package utilTest;

import java.io.InputStream;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.Properties;

/**
 * @ClassName JDBCUtils
 * @Description TODO:工具类，实现获取数据库连接对象，关闭资源两个操作
 * @Author sth_199509@163.com
 * @Date 2021/10/25 22:14
 * @Version 1.0
 */
public class JDBCUtils {
    /**
     * 获取连接操作
     * @return 返回连接对象
     * @throws Exception
     */
    public static Connection getConnection() throws Exception {
        //1、读取配置文件中的4个信息
        InputStream is = ClassLoader.getSystemClassLoader().getResourceAsStream("jdbc.properties");
        Properties pro = new Properties();
        pro.load(is);
        String user = pro.getProperty("user");
        String password = pro.getProperty("password");
        String url = pro.getProperty("url");
        String driverClass = pro.getProperty("driverClass");
        //2、加载驱动
        Class.forName(driverClass);
        //3、获取连接
        Connection con = DriverManager.getConnection(url,user,password);
        //4、返回对象
        return con;
    }

    /**
     * 关闭资源操作
     * @param con 连接关闭
     * @param ps prepareStatement对象关闭
     */
    public static void closeResource(Connection con, Statement ps){
        try {
            ps.close();
        } catch (SQLException e) {
            e.printStackTrace();
        }
        try {
            con.close();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}

```



#### 3.5 使用PreparedStatement实现【增、删、改】操作

<font color='red'>**【普通的】插入操作**</font>

```java
public class UpdateTest {
    //向数据库city99的tulong表中插入数据
    @Test
    public void test() throws Exception {
        //1、读取配置文件中的4个信息
        InputStream is = ClassLoader.getSystemClassLoader().getResourceAsStream("jdbc.properties");
        Properties pro = new Properties();
        pro.load(is);
        String user = pro.getProperty("user");
        String password = pro.getProperty("password");
        String url = pro.getProperty("url");
        String driverClass = pro.getProperty("driverClass");
        //2、加载驱动
        Class.forName(driverClass);
        //3、获取连接
        Connection con = DriverManager.getConnection(url,user,password);

        

        //4、预编译sql语句，返回PreparedStatement的对象
        String sql = "insert into tulong(name,school)values(?,?)"; // ? 问号代表占位符
        PreparedStatement ps = con.prepareStatement(sql);
        //5、填充占位符
        ps.setString(1,"赵敏");//parameterIndex就是序号，切记MySQL是从1开始的
        ps.setString(2,"元朝");
        //如果需要插入日期
//        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
//        java.util.Date date = sdf.parse("1999-09-09");
//        ps.setDate(1,new java.sql.Date(date.getTime()));
        //6、执行操作
        ps.execute();
        //7、资源的关闭【应该用try-catch-finally，确保资源可以关闭】
        ps.close();
        con.close();
    }
}
```

<font color='red'>**【封装后的】修改操作**</font>

```java
public class UpdateTest {
    //修改数据库city99的tulong表中的数据
    @Test
    public void test1() throws Exception {
        //1、获取连接
        Connection con = JDBCUtils.getConnection();

        //2、预编译sql语句，返回PreparedStatement的对象
        String sql = "update tulong set name=?,school=? where name=?"; // ? 问号代表占位符
        PreparedStatement ps = con.prepareStatement(sql);

        //3、填充占位符
        ps.setString(1,"周芷若");//parameterIndex就是序号，切记MySQL是从1开始的
        ps.setString(2,"峨眉派");
        ps.setString(3,"张翠山");

        //4、执行
        ps.execute();

        //5、资源的关闭
        JDBCUtils.closeResource(con,ps);
    }
}
```



#### 3.6 【增、删、改通用方法】

##### **工具类：**



```java
package utilTest;

import java.io.InputStream;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.Properties;

/**
 * @ClassName JDBCUtils
 * @Description TODO:工具类，实现获取数据库连接对象，关闭资源两个操作
 * @Author sth_199509@163.com
 * @Date 2021/10/25 22:14
 * @Version 1.0
 */
public class JDBCUtils {
    /**
     * 获取连接操作
     * @return 返回连接对象
     * @throws Exception
     */
    public static Connection getConnection() throws Exception {
        //1、读取配置文件中的4个信息
        InputStream is = ClassLoader.getSystemClassLoader().getResourceAsStream("jdbc.properties");
        Properties pro = new Properties();
        pro.load(is);
        String user = pro.getProperty("user");
        String password = pro.getProperty("password");
        String url = pro.getProperty("url");
        String driverClass = pro.getProperty("driverClass");
        //2、加载驱动
        Class.forName(driverClass);
        //3、获取连接
        Connection con = DriverManager.getConnection(url,user,password);
        //4、返回对象
        return con;
    }

    /**
     * 关闭资源操作
     * @param con 连接关闭
     * @param ps prepareStatement对象关闭
     */
    public static void closeResource(Connection con, Statement ps){
        try {
            ps.close();
        } catch (SQLException e) {
            e.printStackTrace();
        }
        try {
            con.close();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}

```

##### **通用方法：**

```java
public class UpdateTest {

    //测试通用方法
    @Test
    public void test2(){
        //删
        String sql = "delete from tulong where name=?";
        //注意这个sql语句，【关键词要用``着重号】
        update(sql,"白眉鹰王");
    }
     /**
​	     * 通用方法实现数据库的【增删改】操作
​	     * @param sql sql语句，其中包含n个【问号？】占位符
​	     * @param args 传入不定形参，个数对应sql语句中的【问号？】个数n
​	     */
​	 public void update(String sql,Object ...args){
​	     Connection con = null;
​	     PreparedStatement ps = null;
​	     try {
​	         //1、获取连接
​	         con = JDBCUtils.getConnection();
​	         //2、预编译sql语句，返回PreparedStatement的对象
​	         ps = con.prepareStatement(sql);
​	
	         //3、填充占位符
	         for (int i = 0; i < args.length; i++) {
	             ps.setObject(i+1,args[i]);//切记数据库索引是从1开始，所以第一个parameterIndex要+1；
	         }
	    //4、执行
            ps.execute();
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            //5、资源的关闭
            JDBCUtils.closeResource(con,ps);
        }
    }
}
```


​	  



#### 3.7 使用PreparedStatement实现【查询】操作

**针对city99数据库中tulong表的通用查询操作**

> ```java
> import org.junit.jupiter.api.Test;
> import utilTest.JDBCUtils;
> import java.lang.reflect.Field;
> import java.sql.*;
> 
> /**
>  * @ClassName TuLongForQuery
>  * @Description TODO:针对tulong表的通用查询操作
>  * @Author sth_199509@163.com
>  * @Date 2021/10/25 23:32
>  * @Version 1.0
>  */
> public class TuLongForQuery {
>     @Test
>     public void test() throws Exception {
>         String sql = "select id,name,school from tulong where name=?";
>         TuLong tulong = queryForTuLong(sql,"周芷若");
>         System.out.println(tulong);
>         String sql1 = "select id,school from tulong where id=?";
>         TuLong tulong1 = queryForTuLong(sql1,"2");
>         System.out.println(tulong1);
> 
>     }
> 
>     public TuLong queryForTuLong(String sql,Object ...args) throws Exception {
>         //1、获取连接
>         Connection con = JDBCUtils.getConnection();
>         //2、获取实例
>         PreparedStatement ps = con.prepareStatement(sql);
>         //3、设置占位符
>         for (int i = 0; i < args.length; i++) {
>             ps.setObject(i+1,args[i]);
>         }
>         //4、获取结果集
>         ResultSet resultSet = ps.executeQuery();
>         //5、获取结果集的元数据
>         ResultSetMetaData metaData = resultSet.getMetaData();
>         //6、通过ResultSetMetaData获取结果集中的列数
>         int columnCount = metaData.getColumnCount();//结果集的列数
>         if(resultSet.next()){//假设就查一行数据，多行用while
>             TuLong tuLong = new TuLong();
>             //处理结果集一行数据中的每一个列
>             for (int i = 0; i < columnCount; i++) {
>                 //获取列的值
>                 Object value = resultSet.getObject(i + 1);
>                 //获取每个列的列名【然后赋值给相应的属性，不获取的话不知道给谁赋值】
>                 String columnName = metaData.getColumnName(i + 1);//返回第i+1列的列名，因为数据库从1开始
>                 //通过反射，给tulong对象指定的columnName属性，赋值为columValue
>                 Field field = TuLong.class.getDeclaredField(columnName);
>                 field.setAccessible(true);
>                 field.set(tuLong,value);
>             }
>             return tuLong;
>         }
>         JDBCUtils.closeResource(con,ps,resultSet);
>         return null;//没有查询到结果
>     }
> }
> ```



**针对city99数据库中author表的通用查询操作**

```java
import PreparedStatementTest.TestBean.Author;
import org.junit.jupiter.api.Test;
import utilTest.JDBCUtils;
import java.lang.reflect.Field;
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.ResultSetMetaData;

/**
 * @ClassName AuthorForQuery
 * @Description TODO:针对author表的通用查询操作
 * @Author sth_199509@163.com
 * @Date 2021/10/26 9:54
 * @Version 1.0
 */
public class AuthorForQuery {
    @Test
    public void test() throws Exception {
        //这里在sql语句中给字段名起了别名【别名是类属性的名字】
        //这样查询到的结果集的名字和类的名字一致，就可以正常使用反射了
        //
        String sql = "select id,au_Name `name`,nation from author where nation=?";
        Author result = queryForAuthor(sql, "中国");
        System.out.println(result);
    }

    //处理异常应该用try-catch-finally，确保资源可以关闭
    public Author queryForAuthor(String sql,Object ...args) throws Exception {
        //1、获取连接
        Connection con = JDBCUtils.getConnection();
        //2、获取实例
        PreparedStatement pstate = con.prepareStatement(sql);
        //3、设置占位符
        for (int i = 0; i < args.length; i++) {
            pstate.setObject(i+1,args[i]);
        }
        //4、执行、获取结果集
        ResultSet resultSet = pstate.executeQuery();
        //5、获取结果集元数据
        ResultSetMetaData metaData = pstate.getMetaData();
        //6、通过结果集的元数据获取列数
        int columnCount = metaData.getColumnCount();
        if (resultSet.next()){
            //7、创建结果集类
            Author author = new Author();
            for (int i = 0; i < columnCount; i++) {
                //8、通过结果集获取列值
                Object value = resultSet.getObject(i + 1);
                //9、通过元数据获取别名【getColumnLabel】列名【getColumnName】
//                String columnName = metaData.getColumnName(i + 1);
                String columnlabel = metaData.getColumnLabel(i + 1);
                Field field = Author.class.getDeclaredField(columnlabel);
                field.setAccessible(true);
                field.set(author,value);
            }
            return author;
        }
        //10、关闭资源
        JDBCUtils.closeResource(con,pstate,resultSet);
        return null;
    }
}
```



#### 3.8 【查询通用方法】

- 两种思想
	- <font color='red'>面向接口编程的思想</font>
	- <font color='red'>ORM编程思想（object relational mapping）</font>
		- 一个数据表对应一个java类
		- 表中的一条记录对应java类的一个对象
		- 表中的一个字段对应java类的一个属性
- 两种技术
	- JDBC结果集的元数据：ResultSetMetaData
		- 获取列名：getColumnName()
		- 获取列的别名：getColumnLabel()
	- 通过反射，创建指定类的对象，获取指定的属性并赋值
- <font color='red'>针对表的字段名和类的属性名不相同的情况：</font>
	- 1、必须在声明SQL语句时，使用类的属性名来命名字段的别名
	- 2、使用ResultSetMetaData时，需要使用getColumnLabel()来替换getColumnName()获取列的别名
	- 说明：如果sql中没有起别名，getColumnLabel()获取的就是列名
- 查询流程
	- ![微信图片_20211026104818](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211027230535660-16353471375711-16353968387211.png)

**工具类：

```java
import java.io.InputStream;
import java.sql.*;
import java.util.Properties;

/**
 * @ClassName JDBCUtils
 * @Description TODO:
 * @Author sth_199509@163.com
 * @Date 2021/10/25 22:14
 * @Version 1.0
 */
public class JDBCUtils {
    /**
     * 获取连接操作
     * @return 返回连接对象
     * @throws Exception
     */
    public static Connection getConnection() throws Exception {
        //1、读取配置文件中的4个信息
        InputStream is = ClassLoader.getSystemClassLoader().getResourceAsStream("jdbc.properties");
        Properties pro = new Properties();
        pro.load(is);
        String user = pro.getProperty("user");
        String password = pro.getProperty("password");
        String url = pro.getProperty("url");
        String driverClass = pro.getProperty("driverClass");
        //2、加载驱动
        Class.forName(driverClass);
        //3、获取连接
        Connection con = DriverManager.getConnection(url,user,password);
        //4、返回对象
        return con;
    }

    /**
     * 关闭资源操作
     * @param con 关闭连接
     * @param ps prepareStatement对象关闭
     * @param rs 关闭结果集
     */
    public static void closeResource(Connection con, Statement ps, ResultSet rs){
        try {
            ps.close();
        } catch (SQLException e) {
            e.printStackTrace();
        }
        try {
            con.close();
        } catch (SQLException e) {
            e.printStackTrace();
        }
        try {
            rs.close();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

**通用方法：**

##### 查询一条数据时



```java
    @Test
    public void test() throws Exception {
        String sql = "select id,au_Name `name`,nation from author where nation=?";
        Author instance = getInstance(Author.class, sql, "日本");
        System.out.println(instance);

        String sql2 = "select id,name,school from tulong where name=?";
        TuLong instance1 = getInstance(TuLong.class, sql2, "周芷若");
        System.out.println(instance1);
    }
    /**
     * 针对不同的表的【通用查询操作】，返回表中的一条数据
     * @param clazz 结果集类
     * @param sql 查询sql语句【名字不同时，记得起别名】
     * @param args 设置占位符
     * @param <T>
     * @return
     * @throws Exception
     */
    public <T> T getInstance(Class<T> clazz,String sql,Object ...args) {
        Connection con = null;
        PreparedStatement pstate = null;
        ResultSet resultSet = null;
        try {
            //1、获取连接
            con = JDBCUtils.getConnection();
            //2、获取实例
            pstate = con.prepareStatement(sql);
            //3、设置占位符
            for (int i = 0; i < args.length; i++) {
                pstate.setObject(i+1,args[i]);
            }
            //4、执行、获取结果集
            resultSet = pstate.executeQuery();
            //5、获取结果集元数据
            ResultSetMetaData metaData = pstate.getMetaData();
            //6、通过结果集的元数据获取列数
            int columnCount = metaData.getColumnCount();
            if (resultSet.next()){
                //7、创建结果集类
                T t = clazz.getDeclaredConstructor().newInstance();
                for (int i = 0; i < columnCount; i++) {
                    //8、通过结果集获取列值
                    Object value = resultSet.getObject(i + 1);
                    //9、通过元数据获取别名【getColumnLabel】
                    String columnlabel = metaData.getColumnLabel(i + 1);
                    Field field = clazz.getDeclaredField(columnlabel);
                    field.setAccessible(true);
                    field.set(t,value);
                }
                return t;
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            //10、关闭资源
            JDBCUtils.closeResource(con,pstate,resultSet);
        }
        return null;
    }

```


​	

##### 查询多条语句时

```java
import PreparedStatementTest.TestBean.Author;
import PreparedStatementTest.TestBean.TuLong;
import org.junit.jupiter.api.Test;
import utilTest.JDBCUtils;

import java.lang.reflect.Field;
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.ResultSetMetaData;
import java.util.ArrayList;
import java.util.List;

/**
 * @ClassName PreparedStatementQuery
 * @Description TODO:使用PreparedStatement实现针对不同表的【通用查询】操作
 * @Author sth_199509@163.com
 * @Date 2021/10/26 10:53
 * @Version 1.0
 */
public class PreparedStatementQuery {
    @Test
    public void testForList() throws Exception {
        String sql = "select id,au_Name `name`,nation from author where nation=?";
        List<Author> forList = getInstanceForList(Author.class, sql, "中国");
        forList.forEach(System.out::println);
        System.out.println("---------------------");

        String sql3 = "select * from tulong";
        List<TuLong> forList1 = getInstanceForList(TuLong.class, sql3);
        forList1.forEach(System.out::println);
        System.out.println("---------------------");

        String sql2 = "select id,name,school from tulong where name=?";
        TuLong instance1 = getInstance(TuLong.class, sql2, "周芷若");
        System.out.println(instance1);
    }

    public <T> List<T> getInstanceForList(Class<T> clazz, String sql, Object ...args) {
        Connection con = null;
        PreparedStatement pstate = null;
        ResultSet resultSet = null;
        try {
            //1、获取连接
            con = JDBCUtils.getConnection();
            //2、获取实例
            pstate = con.prepareStatement(sql);
            //3、设置占位符
            for (int i = 0; i < args.length; i++) {
                pstate.setObject(i+1,args[i]);
            }
            //4、执行、获取结果集
            resultSet = pstate.executeQuery();
            //5、获取结果集元数据
            ResultSetMetaData metaData = pstate.getMetaData();
            //6、通过结果集的元数据获取列数
            int columnCount = metaData.getColumnCount();
            ArrayList<T> list = new ArrayList<>();
            while (resultSet.next()){
                //7、创建结果集类
                T t = clazz.getDeclaredConstructor().newInstance();
                //处理结果集的每一行，给t对象属性赋值
                for (int i = 0; i < columnCount; i++) {
                    //8、通过结果集获取列值
                    Object value = resultSet.getObject(i + 1);
                    //9、通过元数据获取别名【getColumnLabel】
                    String columnlabel = metaData.getColumnLabel(i + 1);
                    Field field = clazz.getDeclaredField(columnlabel);
                    field.setAccessible(true);
                    field.set(t,value);
                }
                list.add(t);
            }
            return list;
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            //10、关闭资源
            JDBCUtils.closeResource(con,pstate,resultSet);
        }
        return null;
    }
}

```



### 4、练习

增删改操作可以有返回值，返回受影响行数

> ```java
> package PreparedStatementTest.Practice;
> 
> import PreparedStatementTest.*;
> import PreparedStatementTest.TestBean.TuLong;
> import utilTest.JDBCUpdateUtil;
> import utilTest.JDBCUtils;
> 
> import java.sql.Connection;
> import java.sql.PreparedStatement;
> import java.util.List;
> import java.util.Scanner;
> 
> /**
>  * @ClassName one
>  * @Description TODO:通过控制台像tulong表中插入一条数据
>  * @Author sth_199509@163.com
>  * @Date 2021/10/26 11:39
>  * @Version 1.0
>  */
> public class one {
>     public static void main(String[] args) {
>         one one = new one();
>         Scanner scan = new Scanner(System.in);
>         System.out.println("请输入姓名：");
>         String name = scan.next();
>         System.out.println("请输入门派：");
>         String school = scan.next();
>         //修改id为1 的数据
>         String sql = "update tulong set name=?,school=? where id = 1";
>         int updatelines = one.update(sql, name, school);
>         System.out.println("受影响行数为：" + updatelines);
> 
>         //删除id大于2的数据
>         String sqlDel = "delete from tulong where id > ?";
>         updatelines = one.update(sqlDel,2);
>         System.out.println("受影响行数为：" + updatelines);
> 
>         //插入新的数据
>         String sqlIns = "insert into tulong(name,school)values(?,?)";
>         one.update(sqlIns,"张无忌","明教");
>         one.update(sqlIns,"张三丰","武当派");
>         one.update(sqlIns,"殷素素","天鹰教");
>         one.update(sqlIns,"赵敏","元朝");
> 
>         //查询所有数据
>         String sqlQuery = "select * from tulong";//因为属性名和数据库名相同，所以这里可以用*号，否则要起别名
>         PreparedStatementQuery pq = new PreparedStatementQuery();
>         List<TuLong> list = pq.getInstanceForList(TuLong.class,sqlQuery);
>         list.forEach(System.out::println);
>     }
> 
>     public int update(String sql,Object ...args){
>         Connection con = null;
>         PreparedStatement ps = null;
>         try {
>             //1、获取连接
>             con = JDBCUtils.getConnection();
> 
>             //2、预编译sql语句，返回PreparedStatement的对象
>             ps = con.prepareStatement(sql);
> 
>             //3、填充占位符
>             for (int i = 0; i < args.length; i++) {
>                 ps.setObject(i+1,args[i]);//切记数据库索引是从1开始，所以第一个parameterIndex要+1；
>             }
> 
>             //4、执行
>             /**
>              * 这个execute()是有返回值的
>              * 如果执行的是查询操作，有返回结果，则返回true
>              * 如果执行的是增删改操作，没有返回结果，则此方法返回false
>              */
> //            ps.execute();
> 
> 
>             //如果想看增删改操作影响几行，可以用如下方法
>             return ps.executeUpdate();//返回受影响行数
>         } catch (Exception e) {
>             e.printStackTrace();
>         } finally {
>             //5、资源的关闭
>             JDBCUpdateUtil.closeResource(con,ps);
>         }
>         return 0;
>     }
> }
> ```



## 第4章 操作BLOB类型字段

### 4.1 MySQL BLOB类型

- MySQL中，BLOB是一个二进制大型对象，是一个可以存储大量数据的容器，它能容纳不同大小的数据。
- 插入BLOB类型的数据必须使用PreparedStatement，因为BLOB类型的数据无法使用字符串拼接写的。

- MySQL的四种BLOB类型(除了在存储的最大信息量上不同外，他们是等同的)

| 类型       | 大小（单位：字节） |
| ---------- | ------------------ |
| TinyBlob   | 最大 255           |
| Blob       | 最大 65k           |
| MediumBlob | 最大 16M           |
| LongBlob   | 最大 4G            |



- 实际使用中根据需要存入的数据大小定义不同的BLOB类型。
- 需要注意的是：如果存储的文件过大，数据库的性能会下降。
- <font color='red'>如果在指定了相关的Blob类型以后，还报错：xxx too large，那么在mysql的安装目录下，找my.ini文件加上如下的配置参数： **max_allowed_packet=16M**。同时注意：修改了my.ini文件之后，需要重新启动mysql服务。</font>
- 【MySQL8.0，在ProgramData文件夹找MySQL8.0里面，先打开隐藏文件夹】

### 4.2 向数据表中插入大数据类型

```java
//获取连接
Connection conn = JDBCUtils.getConnection();
		
String sql = "insert into customers(name,email,birth,photo)values(?,?,?,?)";
PreparedStatement ps = conn.prepareStatement(sql);

// 填充占位符
ps.setString(1, "徐海强");
ps.setString(2, "xhq@126.com");
ps.setDate(3, new Date(new java.util.Date().getTime()));
// 操作Blob类型的变量
FileInputStream fis = new FileInputStream("xhq.png");
ps.setBlob(4, fis);
//执行
ps.execute();
		
fis.close();
JDBCUtils.closeResource(conn, ps);

```



### 4.3 修改数据表中的Blob类型字段

```java
Connection conn = JDBCUtils.getConnection();
String sql = "update customers set photo = ? where id = ?";
PreparedStatement ps = conn.prepareStatement(sql);

// 填充占位符
// 操作Blob类型的变量
FileInputStream fis = new FileInputStream("coffee.png");
ps.setBlob(1, fis);
ps.setInt(2, 25);

ps.execute();

fis.close();
JDBCUtils.closeResource(conn, ps);
```



### 4.4 从数据表中读取大数据类型

```java
String sql = "SELECT id, name, email, birth, photo FROM customer WHERE id = ?";
conn = getConnection();
ps = conn.prepareStatement(sql);
ps.setInt(1, 8);
rs = ps.executeQuery();
if(rs.next()){
	Integer id = rs.getInt(1);
    String name = rs.getString(2);
	String email = rs.getString(3);
    Date birth = rs.getDate(4);
	Customer cust = new Customer(id, name, email, birth);
    System.out.println(cust); 
    //读取Blob类型的字段
	Blob photo = rs.getBlob(5);
	InputStream is = photo.getBinaryStream();
	OutputStream os = new FileOutputStream("c.jpg");
	byte [] buffer = new byte[1024];
	int len = 0;
	while((len = is.read(buffer)) != -1){
		os.write(buffer, 0, len);
	}
    JDBCUtils.closeResource(conn, ps, rs);
		
	if(is != null){
		is.close();
	}
		
	if(os !=  null){
		os.close();
	}
    
}

```

```java
@Test
public void testQuery() {
    Connection con = null;
    PreparedStatement ps = null;
    ResultSet resultSet = null;
    InputStream bs = null;
    FileOutputStream fout = null;

    try {
        con = JDBCUtils.getConnection();
        String sql = "select id,bName `name`,bschool school,Date `date`,photo from yitian where `bName`=?";
        ps = con.prepareStatement(sql);
        ps.setObject(1,"段誉");

        resultSet = ps.executeQuery();
        if(resultSet.next()){
            //方式一
//            int id = resultSet.getInt(1);
//            String name = resultSet.getString(2);
//            String school = resultSet.getString(3);
//            Date date = resultSet.getDate(4);
//            Blob blob = resultSet.getBlob(5);
            //方式二：用别名获取字段值，不受上边的顺序影响
            int id = resultSet.getInt("id");
            String name = resultSet.getString("name");
            String school = resultSet.getString("school");
            Date date = resultSet.getDate("date");
            Blob photo = resultSet.getBlob("photo");

            //将Blob类型的字段下载下来，以文件的方式保存在本地
            bs = photo.getBinaryStream();
            fout = new FileOutputStream("duanyu.jpg");
            byte[] bytes = new byte[1024];
            int len;
            while ((len = bs.read(bytes)) != -1){
                fout.write(bytes,0,len);
            }

            Yitian yitian = new Yitian(id,name,school,date);
            //【要有一个不包含Blob文件的构造器】
            System.out.println(yitian);

        }
    } catch (Exception e) {
        e.printStackTrace();
    } finally {
        JDBCUtils.closeResource(con,ps,resultSet);
        try {
            if (bs != null){
                bs.close();
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
        try {
            if (fout != null){
                fout.close();
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

## 第5章 批量插入

### 5.1 批量执行SQL语句

当需要成批插入或者更新记录时，可以采用Java的批量**更新**机制，这一机制允许多条语句一次性提交给数据库批量处理。通常情况下比单独提交处理更有效率

JDBC的批量处理语句包括下面三个方法：

- **addBatch(String)：添加需要批量处理的SQL语句或是参数；**
- **executeBatch()：执行批量处理语句；**
- **clearBatch():清空缓存的数据**

通常我们会遇到两种批量执行SQL语句的情况：

- 多条SQL语句的批量处理；
- 一个SQL语句的批量传参；



### 5.2 高效的批量插入

举例：向数据表中插入20000条数据

- 数据库中提供一个goods表。创建如下：

```sql
CREATE TABLE goods(
id INT PRIMARY KEY AUTO_INCREMENT,
NAME VARCHAR(20)
);
```



#### 5.2.1 实现层次一：使用Statement

```java
Connection conn = JDBCUtils.getConnection();
Statement st = conn.createStatement();
for(int i = 1;i <= 20000;i++){
	String sql = "insert into goods(name) values('name_' + "+ i +")";
	st.executeUpdate(sql);
}
```



#### 5.2.2 实现层次二：使用PreparedStatement

```java
long start = System.currentTimeMillis();
		
Connection conn = JDBCUtils.getConnection();
		
String sql = "insert into goods(name)values(?)";
PreparedStatement ps = conn.prepareStatement(sql);
for(int i = 1;i <= 20000;i++){
	ps.setString(1, "name_" + i);
	ps.executeUpdate();
}
		
long end = System.currentTimeMillis();
System.out.println("花费的时间为：" + (end - start));//2万条预计2173000毫秒
		
		
JDBCUpdateUtil.closeResource(conn, ps);
```

#### 5.2.3 实现层次三

- **mysql服务器默认是关闭批处理的，我们需要通过一个参数，让mysql开启批处理的支持。**
	- ?rewriteBatchedStatements=true 写在配置文件的url后面
 - ![image-20211026172011554](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211021202800277-16348192815141.png)
 - <font color='red'>MySQL8.0里面要默认更改东八区，所以这个批处理开启操作就要用&连接在后边。</font>

```java
/*
 * 修改1： 使用 addBatch() / executeBatch() / clearBatch()
 * 修改2：mysql服务器默认是关闭批处理的，我们需要通过一个参数，让mysql开启批处理的支持。
 * 		 ?rewriteBatchedStatements=true 写在配置文件的url后面
 * 
 */
@Test
public void testInsert1() throws Exception{
	long start = System.currentTimeMillis();
		
	Connection conn = JDBCUtils.getConnection();
		
	String sql = "insert into goods(name)values(?)";
	PreparedStatement ps = conn.prepareStatement(sql);
		
	for(int i = 1;i <= 1000000;i++){
		ps.setString(1, "name_" + i);
			
		//1.“攒”sql
		ps.addBatch();
		if(i % 500 == 0){
			//2.执行
			ps.executeBatch();
			//3.清空
			ps.clearBatch();
		}
	}
		
	long end = System.currentTimeMillis();
	System.out.println("花费的时间为：" + (end - start));//1百万条:507652毫秒
		
	JDBCUpdateUtil.closeResource(conn, ps);
}
```

#### 5.2.4 实现层次四

- 不允许自动提交，所有数据全部攒完，一次性提交
- 方式三是，攒500条提交一次

```java
/*
* 层次四：在层次三的基础上操作
* 使用Connection 的 setAutoCommit(false)  /  commit()
*/
@Test
public void testInsert2() throws Exception{
	long start = System.currentTimeMillis();
		
	Connection conn = JDBCUtils.getConnection();
		
	//1.设置为不自动提交数据
	conn.setAutoCommit(false);
		
	String sql = "insert into goods(name)values(?)";
	PreparedStatement ps = conn.prepareStatement(sql);
		
	for(int i = 1;i <= 1000000;i++){
		ps.setString(1, "name_" + i);
			
		//1.“攒”sql
		ps.addBatch();
			
		if(i % 500 == 0){
			//2.执行
			ps.executeBatch();
			//3.清空
			ps.clearBatch();
		}
	}
		
	//2.提交数据
	conn.commit();
		
	long end = System.currentTimeMillis();
	System.out.println("花费的时间为：" + (end - start));//1百万条:105246毫秒
		
	JDBCUpdateUtil.closeResource(conn, ps);
}
```



## 第6章： 数据库事务

### 6.1 数据库事务介绍

- **事务：一组逻辑操作单元,使数据从一种状态变换到另一种状态。**

- **事务处理（事务操作）：**保证所有事务都作为一个工作单元来执行，即使出现了故障，都不能改变这种执行方式。当在一个事务中执行多个操作时，要么所有的事务都**被提交(commit)**，那么这些修改就永久地保存下来；要么数据库管理系统将放弃所作的所有修改，整个事务**回滚(rollback)**到最初状态。

- 为确保数据库中数据的**一致性**，数据的操纵应当是离散的成组的逻辑单元：当它全部完成时，数据的一致性可以保持，而当这个单元中的一部分操作失败，整个事务应全部视为错误，所有从起始点以后的操作应全部回退到开始状态。 

### 6.2 JDBC事务处理

- <font color='blue'>数据一旦提交，就不可回滚。</font>

- 数据什么时候意味着提交？

	- <font color='blue'>**当一个连接对象被创建时，默认情况下是自动提交事务**</font>：每次执行一个 SQL 语句时，如果执行成功，就会向数据库自动提交，而不能回滚。
	- <font color='blue'>**关闭数据库连接，数据就会自动的提交。**</font>如果多个操作，每个操作使用的是自己单独的连接，则无法保证事务。即同一个事务的多个操作必须在同一个连接下。

- 哪些操作会导致数据的自动提交？？

	- DDL操作一旦执行，都会自动提交
		- set autocommit = false 对DDL操作无效
	- DML操作默认情况下，一旦执行，就会自动提交
		- 但是可以通过set autocommit = false 的方式取消DML操作的自动提交
	- 关闭数据库连接，数据就会自动的提交。

- **JDBC程序中为了让多个 SQL 语句作为一个事务执行：**

	- 调用 Connection 对象的 **setAutoCommit(false);** 以取消自动提交事务
	- 在所有的 SQL 语句都成功执行后，调用 **commit();** 方法提交事务
	- 在出现异常时，调用 **rollback();** 方法回滚事务

	> 若此时 Connection 没有被关闭，还可能被重复使用，则需要恢复其自动提交状态 setAutoCommit(true)。尤其是在使用数据库连接池技术时，执行close()方法前，建议恢复自动提交状态。

- 考虑到事务后，处理方式

	- 原本在增删改通用操作里面，获取连接，关闭连接
	- 现在将获取连接操作摘出来【因为关闭连接会自动提交数据，拿出来控制他不关闭】
	- 再设置conn.setAutoCommit(false);，不允许自动提交，【改成手动】
	- 语句执行完成后手动conn.commit();提交
	- 在catch中放置rollback，有异常，就回滚
	- 在finally中放置关闭连接和conn.setAutoCommit(true);，恢复人家的自动提交。

【案例：用户AA向用户BB转账100】

```java
public void testJDBCTransaction() {
	Connection conn = null;
	try {
		// 1.获取数据库连接
		conn = JDBCUtils.getConnection();
		// 2.开启事务
		conn.setAutoCommit(false);
		// 3.进行数据库操作
		String sql1 = "update user_table set balance = balance - 100 where user = ?";
		update(conn, sql1, "AA");

		// 模拟网络异常----出现异常，跳到catch，运行里面的rollback回滚
		//System.out.println(10 / 0);

		String sql2 = "update user_table set balance = balance + 100 where user = ?";
		update(conn, sql2, "BB");
		// 4.若没有异常，则提交事务
		conn.commit();
	} catch (Exception e) {
		e.printStackTrace();
		// 5.若有异常，则回滚事务
		try {
			conn.rollback();
		} catch (SQLException e1) {
			e1.printStackTrace();
		}
    } finally {
        try {
			//6.恢复每次DML操作的自动提交功能
			conn.setAutoCommit(true);
		} catch (SQLException e) {
			e.printStackTrace();
		}
        //7.关闭连接
		JDBCUtils.closeResource(conn, null, null); 
    }  
}

```

其中，对数据库操作的方法为：

```java
//使用事务以后的通用的增删改操作（version 2.0）
public void update(Connection conn ,String sql, Object... args) {
	PreparedStatement ps = null;
	try {
		// 1.获取PreparedStatement的实例 (或：预编译sql语句)
		ps = conn.prepareStatement(sql);
		// 2.填充占位符
		for (int i = 0; i < args.length; i++) {
			ps.setObject(i + 1, args[i]);
		}
		// 3.执行sql语句
		ps.execute();
	} catch (Exception e) {
		e.printStackTrace();
	} finally {
		// 4.关闭资源
		JDBCUtils.closeResource(null, ps);

	}
}
```



### 6.3 事务的ACID属性    

1. **原子性（Atomicity）**
	原子性是指事务是一个不可分割的工作单位，事务中的操作要么都发生，要么都不发生。 

2. **一致性（Consistency）**
	事务必须使数据库从一个一致性状态变换到另外一个一致性状态。

3. **隔离性（Isolation）**
	事务的隔离性是指一个事务的执行不能被其他事务干扰，即一个事务内部的操作及使用的数据对并发的其他事务是隔离的，并发执行的各个事务之间不能互相干扰。

4. **持久性（Durability）**
	持久性是指一个事务一旦被提交，它对数据库中数据的改变就是永久性的，接下来的其他操作和数据库故障不应该对其有任何影响。

#### 6.3.1 数据库的并发问题

- 对于同时运行的多个事务, 当这些事务访问数据库中相同的数据时, 如果没有采取必要的隔离机制, 就会导致各种并发问题:
 - <font color='red'>**脏读**</font>：对于两个事务甲、乙，当甲读取了已经被乙更新但还<font color='blue'>没有提交</font>的字段，之后若乙发生了回滚，甲读取的内容就是临时的，且无效的。
- <font color='red'>**不可重复读**</font>：对于两个事务甲、乙，甲读取了一个字段，然后乙<font color='blue'>更新</font>了该字段，之后甲再次读取同一个字段时，字段的值就不同了。
- <font color='red'>**幻读**</font>：对于两个事务甲、乙，甲从表中读取了一个字段，然后乙在该表中<font color='blue'>插入</font>了一些新的行，如果甲再次读取同一个表，就会多出几行。
- **数据库事务的隔离性**: 数据库系统必须具有隔离并发运行各个事务的能力, 使它们不会相互影响, 避免各种并发问题。

- 一个事务与其他事务隔离的程度称为隔离级别。数据库规定了多种事务隔离级别, 不同隔离级别对应不同的干扰程度, **隔离级别越高, 数据一致性就越好, 但并发性越弱。**

#### 6.3.2 四种隔离级别

- 数据库提供的4种事务隔离级别：

| 隔离强度 | 支持         | 隔离级别                             | 描述                                                         |
| -------- | ------------ | ------------------------------------ | ------------------------------------------------------------ |
| 最低     | MySQL        | READ UNCOMMITTED<br />(读未提交数据) | 允许事务读取未被其他事物提交的表更、脏读、不可重复读和幻读的问题都会出现 |
|          | Oracle/MySQL | READ COMMITED<BR />(读已提交数据)    | 只允许事务读取已经被其他事物提交的变更、可以避免脏读、但但但不可重复读和幻读问题仍可能会出现 |
|          | MySQL        | REPEATABLE READ<br/>(可重复读)       | 确保事务可以多次从一个字段中读取相同的值，但这个事务持续期间，禁止其他事物对这个字段进行更新，可以避免脏读和不可重复读，但但但幻读问题仍然存在 |
| 最高     | Oracle/MySQL | SERIALIZABLE(串行化)                 | 确保事务可以从一个表中读取相同的行，在这个事务持续期间，禁止其他事务对该表执行插入、更新和删除操作，所有并发问题都可以避免，但性能十分低下 |



- Oracle 支持的 2 种事务隔离级别：**READ COMMITED**, SERIALIZABLE。 Oracle 默认的事务隔离级别为: **READ COMMITED** 。


- Mysql 支持 4 种事务隔离级别。Mysql 默认的事务隔离级别为: **REPEATABLE READ。**


#### 6.3.3 在MySql中设置隔离级别

- 每启动一个 mysql 程序, 就会获得一个单独的数据库连接. 每个数据库连接都有一个全局变量 @@transaction_isolation, 表示当前的事务隔离级别。

- 查看当前的隔离级别: 

```mysql
SELECT @@transaction_isolation;-- 适配MySQL8.0
```

- 设置当前 mySQL 连接的隔离级别:  

```mysql
set transaction isolation level read committed;-- 适配MySQL8.0
```

- 设置数据库系统的全局的隔离级别:

```mysql
set global transaction isolation level read committed;-- 适配MySQL8.0
```

- 补充操作：
 - 创建mysql数据库用户：

```mysql
create user tom identified by 'abc123';-- 适配MySQL8.0
```

- 授予权限

```mysql
#授予通过网络方式登录的tom用户，对所有库所有表的全部权限.
grant all privileges on *.* to tom@'%'; 【未验证】

 #给tom用户使用本地命令行方式，授予atguigudb这个库下的所有表的插删改查的权限。
grant select,insert,delete,update on city99.* to 'tom'@'%';
【已验证可行，适用于MySQL8.0】

```


## 第7章：DAO及相关实现类

- DAO：Data Access Object访问数据信息的类和接口，包括了对数据的CRUD（Create、Retrival、Update、Delete），而不包含任何业务相关的信息。有时也称作：BaseDAO
- 作用：为了实现功能的模块化，更有利于代码的维护和升级。

![image-20211027230535660](https://pledge99.oss-cn-beijing.aliyuncs.com/img/微信图片_20211026104818.jpg)



### 【BaseDAO.java】

```java
package com.atguigu.bookstore.dao;

import java.lang.reflect.ParameterizedType;
import java.lang.reflect.Type;
import java.sql.Connection;
import java.sql.SQLException;
import java.util.List;

import org.apache.commons.dbutils.QueryRunner;
import org.apache.commons.dbutils.handlers.BeanHandler;
import org.apache.commons.dbutils.handlers.BeanListHandler;
import org.apache.commons.dbutils.handlers.ScalarHandler;


/**
 * 定义一个用来被继承的对数据库进行基本操作的Dao
 * 
 * @author HanYanBing
 *
 * @param <T>
 */
public abstract class BaseDao<T> {
	private QueryRunner queryRunner = new QueryRunner();
	// 定义一个变量来接收泛型的类型
	private Class<T> type;

	// 获取T的Class对象，获取泛型的类型，泛型是在被子类继承时才确定
	public BaseDao() {
		// 获取子类的类型
		Class clazz = this.getClass();
		// 获取父类的类型
		// getGenericSuperclass()用来获取当前类的父类的类型
		// ParameterizedType表示的是带泛型的类型
		ParameterizedType parameterizedType = (ParameterizedType) clazz.getGenericSuperclass();
		// 获取具体的泛型类型 getActualTypeArguments获取具体的泛型的类型
		// 这个方法会返回一个Type的数组
		Type[] types = parameterizedType.getActualTypeArguments();
		// 获取具体的泛型的类型·
		this.type = (Class<T>) types[0];
	}

	/**
	 * 通用的增删改操作
	 * 
	 * @param sql
	 * @param params
	 * @return
	 */
	public int update(Connection conn,String sql, Object... params) {
		int count = 0;
		try {
			count = queryRunner.update(conn, sql, params);
		} catch (SQLException e) {
			e.printStackTrace();
		} 
		return count;
	}

	/**
	 * 获取一个对象
	 * 
	 * @param sql
	 * @param params
	 * @return
	 */
	public T getBean(Connection conn,String sql, Object... params) {
		T t = null;
		try {
			t = queryRunner.query(conn, sql, new BeanHandler<T>(type), params);
		} catch (SQLException e) {
			e.printStackTrace();
		} 
		return t;
	}

	/**
	 * 获取所有对象
	 * 
	 * @param sql
	 * @param params
	 * @return
	 */
	public List<T> getBeanList(Connection conn,String sql, Object... params) {
		List<T> list = null;
		try {
			list = queryRunner.query(conn, sql, new BeanListHandler<T>(type), params);
		} catch (SQLException e) {
			e.printStackTrace();
		} 
		return list;
	}

	/**
	 * 获取一个但一值得方法，专门用来执行像 select count(*)...这样的sql语句
	 * 
	 * @param sql
	 * @param params
	 * @return
	 */
	public Object getValue(Connection conn,String sql, Object... params) {
		Object count = null;
		try {
			// 调用queryRunner的query方法获取一个单一的值
			count = queryRunner.query(conn, sql, new ScalarHandler<>(), params);
		} catch (SQLException e) {
			e.printStackTrace();
		} 
		return count;
	}
}
```

### 【BookDAO.java】

```java
package com.atguigu.bookstore.dao;

import java.sql.Connection;
import java.util.List;

import com.atguigu.bookstore.beans.Book;
import com.atguigu.bookstore.beans.Page;

public interface BookDao {

	/**
	 * 从数据库中查询出所有的记录
	 * 
	 * @return
	 */
	List<Book> getBooks(Connection conn);

	/**
	 * 向数据库中插入一条记录
	 * 
	 * @param book
	 */
	void saveBook(Connection conn,Book book);

	/**
	 * 从数据库中根据图书的id删除一条记录
	 * 
	 * @param bookId
	 */
	void deleteBookById(Connection conn,String bookId);

	/**
	 * 根据图书的id从数据库中查询出一条记录
	 * 
	 * @param bookId
	 * @return
	 */
	Book getBookById(Connection conn,String bookId);

	/**
	 * 根据图书的id从数据库中更新一条记录
	 * 
	 * @param book
	 */
	void updateBook(Connection conn,Book book);

	/**
	 * 获取带分页的图书信息
	 * 
	 * @param page：是只包含了用户输入的pageNo属性的page对象
	 * @return 返回的Page对象是包含了所有属性的Page对象
	 */
	Page<Book> getPageBooks(Connection conn,Page<Book> page);

	/**
	 * 获取带分页和价格范围的图书信息
	 * 
	 * @param page：是只包含了用户输入的pageNo属性的page对象
	 * @return 返回的Page对象是包含了所有属性的Page对象
	 */
	Page<Book> getPageBooksByPrice(Connection conn,Page<Book> page, double minPrice, double maxPrice);

}
```

### 【UserDAO.java】

```java
package com.atguigu.bookstore.dao;

import java.sql.Connection;

import com.atguigu.bookstore.beans.User;

public interface UserDao {

	/**
	 * 根据User对象中的用户名和密码从数据库中获取一条记录
	 * 
	 * @param user
	 * @return User 数据库中有记录 null 数据库中无此记录
	 */
	User getUser(Connection conn,User user);

	/**
	 * 根据User对象中的用户名从数据库中获取一条记录
	 * 
	 * @param user
	 * @return true 数据库中有记录 false 数据库中无此记录
	 */
	boolean checkUsername(Connection conn,User user);

	/**
	 * 向数据库中插入User对象
	 * 
	 * @param user
	 */
	void saveUser(Connection conn,User user);
}
```

### 【BookDaoImpl.java】

```java
package com.atguigu.bookstore.dao.impl;

import java.sql.Connection;
import java.util.List;

import com.atguigu.bookstore.beans.Book;
import com.atguigu.bookstore.beans.Page;
import com.atguigu.bookstore.dao.BaseDao;
import com.atguigu.bookstore.dao.BookDao;

public class BookDaoImpl extends BaseDao<Book> implements BookDao {

	@Override
	public List<Book> getBooks(Connection conn) {
		// 调用BaseDao中得到一个List的方法
		List<Book> beanList = null;
		// 写sql语句
		String sql = "select id,title,author,price,sales,stock,img_path imgPath from books";
		beanList = getBeanList(conn,sql);
		return beanList;
	}

	@Override
	public void saveBook(Connection conn,Book book) {
		// 写sql语句
		String sql = "insert into books(title,author,price,sales,stock,img_path) values(?,?,?,?,?,?)";
		// 调用BaseDao中通用的增删改的方法
		update(conn,sql, book.getTitle(), book.getAuthor(), book.getPrice(), book.getSales(), book.getStock(),book.getImgPath());
	}

	@Override
	public void deleteBookById(Connection conn,String bookId) {
		// 写sql语句
		String sql = "DELETE FROM books WHERE id = ?";
		// 调用BaseDao中通用增删改的方法
		update(conn,sql, bookId);
			
	}

	@Override
	public Book getBookById(Connection conn,String bookId) {
		// 调用BaseDao中获取一个对象的方法
		Book book = null;
		// 写sql语句
		String sql = "select id,title,author,price,sales,stock,img_path imgPath from books where id = ?";
		book = getBean(conn,sql, bookId);
		return book;
	}

	@Override
	public void updateBook(Connection conn,Book book) {
		// 写sql语句
		String sql = "update books set title = ? , author = ? , price = ? , sales = ? , stock = ? where id = ?";
		// 调用BaseDao中通用的增删改的方法
		update(conn,sql, book.getTitle(), book.getAuthor(), book.getPrice(), book.getSales(), book.getStock(), book.getId());
	}

	@Override
	public Page<Book> getPageBooks(Connection conn,Page<Book> page) {
		// 获取数据库中图书的总记录数
		String sql = "select count(*) from books";
		// 调用BaseDao中获取一个单一值的方法
		long totalRecord = (long) getValue(conn,sql);
		// 将总记录数设置都page对象中
		page.setTotalRecord((int) totalRecord);

		// 获取当前页中的记录存放的List
		String sql2 = "select id,title,author,price,sales,stock,img_path imgPath from books limit ?,?";
		// 调用BaseDao中获取一个集合的方法
		List<Book> beanList = getBeanList(conn,sql2, (page.getPageNo() - 1) * Page.PAGE_SIZE, Page.PAGE_SIZE);
		// 将这个List设置到page对象中
		page.setList(beanList);
		return page;
	}

	@Override
	public Page<Book> getPageBooksByPrice(Connection conn,Page<Book> page, double minPrice, double maxPrice) {
		// 获取数据库中图书的总记录数
		String sql = "select count(*) from books where price between ? and ?";
		// 调用BaseDao中获取一个单一值的方法
		long totalRecord = (long) getValue(conn,sql,minPrice,maxPrice);
		// 将总记录数设置都page对象中
		page.setTotalRecord((int) totalRecord);

		// 获取当前页中的记录存放的List
		String sql2 = "select id,title,author,price,sales,stock,img_path imgPath from books where price between ? and ? limit ?,?";
		// 调用BaseDao中获取一个集合的方法
		List<Book> beanList = getBeanList(conn,sql2, minPrice , maxPrice , (page.getPageNo() - 1) * Page.PAGE_SIZE, Page.PAGE_SIZE);
		// 将这个List设置到page对象中
		page.setList(beanList);
		
		return page;
	}

}
```

### 【UserDaoImpl.java】

```java
package com.atguigu.bookstore.dao.impl;

import java.sql.Connection;

import com.atguigu.bookstore.beans.User;
import com.atguigu.bookstore.dao.BaseDao;
import com.atguigu.bookstore.dao.UserDao;

public class UserDaoImpl extends BaseDao<User> implements UserDao {

	@Override
	public User getUser(Connection conn,User user) {
		// 调用BaseDao中获取一个对象的方法
		User bean = null;
		// 写sql语句
		String sql = "select id,username,password,email from users where username = ? and password = ?";
		bean = getBean(conn,sql, user.getUsername(), user.getPassword());
		return bean;
	}

	@Override
	public boolean checkUsername(Connection conn,User user) {
		// 调用BaseDao中获取一个对象的方法
		User bean = null;
		// 写sql语句
		String sql = "select id,username,password,email from users where username = ?";
		bean = getBean(conn,sql, user.getUsername());
		return bean != null;
	}

	@Override
	public void saveUser(Connection conn,User user) {
		//写sql语句
		String sql = "insert into users(username,password,email) values(?,?,?)";
		//调用BaseDao中通用的增删改的方法
		update(conn,sql, user.getUsername(),user.getPassword(),user.getEmail());
	}

}
```

### 【Book.java】

```java
package com.atguigu.bookstore.beans;
/**
 * 图书类
 * @author songhongkang
 *
 */
public class Book {

	private Integer id;
	private String title; // 书名
	private String author; // 作者
	private double price; // 价格
	private Integer sales; // 销量
	private Integer stock; // 库存
	private String imgPath = "static/img/default.jpg"; // 封面图片的路径
	//构造器，get()，set()，toString()方法略
}
```

### 【Page.java】

```java
package com.atguigu.bookstore.beans;

import java.util.List;
/**
 * 页码类
 * @author songhongkang
 *
 */
public class Page<T> {

	private List<T> list; // 每页查到的记录存放的集合
	public static final int PAGE_SIZE = 4; // 每页显示的记录数
	private int pageNo; // 当前页
//	private int totalPageNo; // 总页数，通过计算得到
	private int totalRecord; // 总记录数，通过查询数据库得到

```

### 【User.java】

```java
package com.atguigu.bookstore.beans;
/**
 * 用户类
 * @author songhongkang
 *
 */
public class User {

	private Integer id;
	private String username;
	private String password;
	private String email;

```



## 第8章：数据库连接池

### 8.1 JDBC数据库连接池的必要性

- 在使用开发基于数据库的web程序时，传统的模式基本是按以下步骤：　　
	- **在主程序（如servlet、beans）中建立数据库连接**
	- **进行sql操作**
	- **断开数据库连接**

- 这种模式开发，存在的问题:
	- 普通的JDBC数据库连接使用 DriverManager 来获取，每次向数据库建立连接的时候都要将 Connection 加载到内存中，再验证用户名和密码(得花费0.05s～1s的时间)。需要数据库连接的时候，就向数据库要求一个，执行完成后再断开连接。这样的方式将会消耗大量的资源和时间。**数据库的连接资源并没有得到很好的重复利用。**若同时有几百人甚至几千人在线，频繁的进行数据库连接操作将占用很多的系统资源，严重的甚至会造成服务器的崩溃。
	- **对于每一次数据库连接，使用完后都得断开。**否则，如果程序出现异常而未能关闭，将会导致数据库系统中的内存泄漏，最终将导致重启数据库。（回忆：何为Java的内存泄漏？）
	- **这种开发不能控制被创建的连接对象数**，系统资源会被毫无顾及的分配出去，如连接过多，也可能导致内存泄漏，服务器崩溃。 

### 8.2 数据库连接池技术

- 为解决传统开发中的数据库连接问题，可以采用数据库连接池技术。
- **数据库连接池的基本思想**：就是为数据库连接建立一个“缓冲池”。预先在缓冲池中放入一定数量的连接，当需要建立数据库连接时，只需从“缓冲池”中取出一个，使用完毕之后再放回去。

- **数据库连接池**负责分配、管理和释放数据库连接，它**允许应用程序重复使用一个现有的数据库连接，而不是重新建立一个**。
- 数据库连接池在初始化时将创建一定数量的数据库连接放到连接池中，这些数据库连接的数量是由**最小数据库连接数来设定**的。无论这些数据库连接是否被使用，连接池都将一直保证至少拥有这么多的连接数量。连接池的**最大数据库连接数量**限定了这个连接池能占有的最大连接数，当应用程序向连接池请求的连接数超过最大连接数量时，这些请求将被加入到等待队列中。

![微信图片_20211027231347](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211028103849069-16353887307761.png)

- **工作原理：**

![微信图片_20211027231358](https://pledge99.oss-cn-beijing.aliyuncs.com/img/微信图片_20211027231358-16353476738653.jpg)

- **数据库连接池技术的优点**

**1. 资源重用**

由于数据库连接得以重用，避免了频繁创建，释放连接引起的大量性能开销。在减少系统消耗的基础上，另一方面也增加了系统运行环境的平稳性。

**2. 更快的系统反应速度**

数据库连接池在初始化过程中，往往已经创建了若干数据库连接置于连接池中备用。此时连接的初始化工作均已完成。对于业务请求处理而言，直接利用现有可用连接，避免了数据库连接初始化和释放过程的时间开销，从而减少了系统的响应时间

**3. 新的资源分配手段**

对于多应用共享同一数据库的系统而言，可在应用层通过数据库连接池的配置，实现某一应用最大可用数据库连接数的限制，避免某一应用独占所有的数据库资源

**4. 统一的连接管理，避免数据库连接泄漏**

在较为完善的数据库连接池实现中，可根据预先的占用超时设定，强制回收被占用连接，从而避免了常规数据库连接操作中可能出现的资源泄露


### 8.3 多种开源的数据库连接池

- JDBC 的数据库连接池使用 javax.sql.DataSource 来表示，DataSource 只是一个接口，该接口通常由服务器(Weblogic, WebSphere, Tomcat)提供实现，也有一些开源组织提供实现：
	- **DBCP** 是Apache提供的数据库连接池。tomcat 服务器自带dbcp数据库连接池。**速度相对c3p0较快**，但因自身存在BUG，Hibernate3已不再提供支持。
	- **C3P0** 是一个开源组织提供的一个数据库连接池，**速度相对较慢，稳定性还可以。**hibernate官方推荐使用
	- **Proxool** 是sourceforge下的一个开源项目数据库连接池，有监控连接池状态的功能，**稳定性较c3p0差一点**
	- **BoneCP** 是一个开源组织提供的数据库连接池，速度快
	- **Druid** 是阿里提供的数据库连接池，据说是集DBCP 、C3P0 、Proxool 优点于一身的数据库连接池，但是速度不确定是否有BoneCP快
- DataSource 通常被称为数据源，它包含连接池和连接池管理两个部分，习惯上也经常把 DataSource 称为连接池
- **DataSource用来取代DriverManager来获取Connection，获取速度快，同时可以大幅度提高数据库访问速度。**
- 特别注意：
	- 数据源和数据库连接不同，数据源无需创建多个，它是产生数据库连接的工厂，因此**整个应用只需要一个数据源即可。**
	- 当数据库访问结束后，程序还是像以前一样关闭数据库连接：conn.close(); 但conn.close()并没有关闭数据库的物理连接，它仅仅把数据库连接释放，归还给了数据库连接池。

#### 8.3.1 C3P0数据库连接池

- 获取连接方式一

```java
//使用C3P0数据库连接池的方式，获取数据库的连接：不推荐
@Test
    public void testOne() throws Exception {
        //方式一：直接写在代码中
        ComboPooledDataSource cpds = new ComboPooledDataSource();
        cpds.setDriverClass("com.mysql.cj.jdbc.Driver");
        //加载jdbc驱动
        cpds.setJdbcUrl("jdbc:mysql://localhost:3306/city99?serverTimezone=GMT%2B8&rewriteBatchedStatements=true");
        cpds.setUser("root");
        cpds.setPassword("123456");
        //通过设置相关参数，对数据库连接池进行管理
        //设置初始时数据库连接池中的连接数
        cpds.setInitialPoolSize(10);
        Connection con = cpds.getConnection();

        //销毁C3P0连接池
//        DataSources.destroy(cpds);
    }
```



- 获取连接方式二【推荐】

```java
//使用C3P0数据库连接池的配置文件方式，获取数据库的连接：推荐

public class JDBCUtils_c3p0 {
    //创建池子放在方法外边，要不然每次调用方法，创建一个池子，调用n次，创建n个池子，完蛋了
    private static ComboPooledDataSource cpds = new ComboPooledDataSource("helloc3p0");

    public static Connection getConnection() throws SQLException {
        Connection con = cpds.getConnection();
        return  con;
    }
}
```

其中，src下的配置文件为：【c3p0-config.xml】

```xml
<c3p0-config>

    <named-config name="helloc3p0">
        <!-- 提供获取连接的4个基本信息 -->
        <!-- 注意小写开头字母-->
        <property name="driverClass">com.mysql.cj.jdbc.Driver</property>
        <property name="jdbcUrl">jdbc:mysql://localhost:3306/city99?serverTimezone=GMT%2B8&amp;rewriteBatchedStatements=true</property>
        <property name="user">root</property>
        <property name="password">*******</property>

        <!-- 进行数据库连接池管理的基本信息 -->
        <!-- 当数据库连接池中的连接数不够时，c3p0一次性想数据库服务器申请的连接数5       -->
        <property name="acquireIncrement">5</property>
        <!-- c3p0数据库连接池中初始化的连接数       -->
        <property name="initialPoolSize">10</property>
        <!-- c3p0数据库连接池中维护的最少的连接数       -->
        <property name="minPoolSize">10</property>
        <!-- c3p0数据库连接池中维护的最大的的连接数       -->
        <property name="maxPoolSize">100</property>
        <!-- c3p0数据库连接池中最多维护的Statement的个数       -->
        <property name="maxStatements">50</property>
        <!-- 每个连接中可以最多使用的Statement的个数       -->
        <property name="maxStatementsPerConnection">2</property>


    </named-config>
</c3p0-config>
```



#### 8.3.2 DBCP数据库连接池

- DBCP 是 Apache 软件基金组织下的开源连接池实现，该连接池依赖该组织下的另一个开源系统：Common-pool。如需使用该连接池实现，应在系统中增加如下两个 jar 文件：
	- Commons-dbcp.jar：连接池的实现
	- Commons-pool.jar：连接池实现的依赖库
- **Tomcat 的连接池正是采用该连接池来实现的。**该数据库连接池既可以与应用服务器整合使用，也可由应用程序独立使用。
- 数据源和数据库连接不同，数据源无需创建多个，它是产生数据库连接的工厂，因此整个应用只需要一个数据源即可。
- 当数据库访问结束后，程序还是像以前一样关闭数据库连接：conn.close(); 但上面的代码并没有关闭数据库的物理连接，它仅仅把数据库连接释放，归还给了数据库连接池。
- 配置属性说明

| 属性                       | 默认值 | 说明                                                         |
| -------------------------- | ------ | ------------------------------------------------------------ |
| initialSize                | 0      | 连接池启动时创建的初始化连接数量                             |
| maxActive                  | 8      | 连接池中可同时连接的最大的连接数                             |
| maxIdle                    | 8      | 连接池中最大的空闲的连接数，超过的空闲连接将被释放，如果设置为负数表示不限制 |
| minIdle                    | 0      | 连接池中最小的空闲的连接数，低于这个数量会被创建新的连接。该参数越接近maxIdle，性能越好，因为连接的创建和销毁，都是需要消耗资源的；但是不能太大。 |
| maxWait                    | 无限制 | 最大等待时间，当没有可用连接时，连接池等待连接释放的最大时间，超过该时间限制会抛出异常，如果设置-1表示无限等待 |
| poolPreparedStatements     | false  | 开启池的Statement是否prepared                                |
| maxOpenPreparedStatements  | 无限制 | 开启池的prepared 后的同时最大连接数                          |
| minEvictableIdleTimeMillis |        | 连接池中连接，在时间段内一直空闲， 被逐出连接池的时间        |
| removeAbandonedTimeout     | 300    | 超过时间限制，回收没有用(废弃)的连接                         |
| removeAbandoned            | false  | 超过removeAbandonedTimeout时间后，是否进 行没用连接（废弃）的回收 |



- 获取连接方式一：

```java
public void testOne() throws SQLException {
    //创建了DBCP的数据库连接池
    BasicDataSource source = new BasicDataSource();
    //设置基本信息
    source.setDriverClassName("com.mysql.cj.jdbc.Driver");
    source.setUrl("jdbc:mysql://localhost:3306/city99?serverTimezone=GMT%2B8&rewriteBatchedStatements=true");
    source.setUsername("root");
    source.setPassword("123456");

    //可以设置其他设计数据库连接池管理的相关属性
    source.setInitialSize(10);
    source.setMaxActive(10);

    Connection con = source.getConnection();
    System.out.println(con);
}
```

- 获取连接方式二【推荐】：

```java
//使用dbcp数据库连接池的配置文件方式，获取数据库的连接：推荐
private static DataSource source;
//同理，将数据库连接池的创建放到外边，要不然创建n个池子干啥
//因为涉及到流加载，不能直接声明，通过声明静态代码块，随着类的加载而加载
static{
    try {
        Properties pros = new Properties();
        FileInputStream is = new FileInputStream("src\\dbcp.properties");
        pros.load(is);
        //创建一个数据库连接池
        source = BasicDataSourceFactory.createDataSource(pros);
    } catch (Exception e) {
        e.printStackTrace();
    }
}

public static Connection getConnection_dbcp() throws SQLException {
    Connection con = source.getConnection();
    return con;
}
```

其中，src下的配置文件为：【dbcp.properties】

```properties
driverClassName=com.mysql.cj.jdbc.Driver
url=jdbc:mysql://localhost:3306/city99?serverTimezone=GMT%2B8&rewriteBatchedStatements=true
username=root
password=123456
initialSize=10
#...
```



#### 8.3.3 Druid（德鲁伊）数据库连接池

Druid是阿里巴巴开源平台上一个数据库连接池实现，它结合了C3P0、DBCP、Proxool等DB池的优点，同时加入了日志监控，可以很好的监控DB池连接和SQL的执行情况，可以说是针对监控而生的DB连接池，**可以说是目前最好的连接池之一。**

```java
/**
     * 使用druid数据库连接池技术
     * @return
     */
    private static DataSource sourceDruid;
    //同理，将数据库连接池的创建放到外边，要不然创建n个池子干啥
    //因为涉及到流加载，不能直接声明，通过声明静态代码块，随着类的加载而加载
    static{
        try {
            Properties pros = new Properties();
            // 读取jdbc.properties 属性配置文件
            InputStream is = ClassLoader.getSystemClassLoader().getResourceAsStream("jdbc.properties");
            // 从流中加载数据
            pros.load(is);
            // 创建数据库连接池
            sourceDruid = DruidDataSourceFactory.createDataSource(pros);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    public static Connection getConnection_druid(){
        Connection connection = null;
        try {
            connection = sourceDruid.getConnection();
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return connection;
    }

	/**
     * 关闭连接，放回数据库连接池
     * @param conn 要关闭的连接
     */
    public static void close(Connection conn){
        if (conn != null){
            try {
                conn.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
```

其中，src下的配置文件为：【druid.properties】【web工程放在main->resources下，调用时直接写名就行】

```java
driverClassName=com.mysql.cj.jdbc.Driver
url=jdbc:mysql://localhost:3306/city99?serverTimezone=GMT%2B8&rewriteBatchedStatements=true
username=root
password=123456

initialSize=10
maxActive=20
maxWait=1000
filters=wall
```

- 详细配置参数：

| **配置**                      | **缺省** | **说明**                                                     |
| ----------------------------- | -------- | ------------------------------------------------------------ |
| name                          |          | 配置这个属性的意义在于，如果存在多个数据源，监控的时候可以通过名字来区分开来。   如果没有配置，将会生成一个名字，格式是：”DataSource-” +   System.identityHashCode(this) |
| url                           |          | 连接数据库的url，不同数据库不一样。例如：mysql :   jdbc:mysql://10.20.153.104:3306/druid2      oracle :   jdbc:oracle:thin:@10.20.149.85:1521:ocnauto |
| username                      |          | 连接数据库的用户名                                           |
| password                      |          | 连接数据库的密码。如果你不希望密码直接写在配置文件中，可以使用ConfigFilter。详细看这里：<https://github.com/alibaba/druid/wiki/%E4%BD%BF%E7%94%A8ConfigFilter> |
| driverClassName               |          | 根据url自动识别   这一项可配可不配，如果不配置druid会根据url自动识别dbType，然后选择相应的driverClassName(建议配置下) |
| initialSize                   | 0        | 初始化时建立物理连接的个数。初始化发生在显示调用init方法，或者第一次getConnection时 |
| maxActive                     | 8        | 最大连接池数量                                               |
| maxIdle                       | 8        | 已经不再使用，配置了也没效果                                 |
| minIdle                       |          | 最小连接池数量                                               |
| maxWait                       |          | 获取连接时最大等待时间，单位毫秒。配置了maxWait之后，缺省启用公平锁，并发效率会有所下降，如果需要可以通过配置useUnfairLock属性为true使用非公平锁。 |
| poolPreparedStatements        | false    | 是否缓存preparedStatement，也就是PSCache。PSCache对支持游标的数据库性能提升巨大，比如说oracle。在mysql下建议关闭。 |
| maxOpenPreparedStatements     | -1       | 要启用PSCache，必须配置大于0，当大于0时，poolPreparedStatements自动触发修改为true。在Druid中，不会存在Oracle下PSCache占用内存过多的问题，可以把这个数值配置大一些，比如说100 |
| validationQuery               |          | 用来检测连接是否有效的sql，要求是一个查询语句。如果validationQuery为null，testOnBorrow、testOnReturn、testWhileIdle都不会其作用。 |
| testOnBorrow                  | true     | 申请连接时执行validationQuery检测连接是否有效，做了这个配置会降低性能。 |
| testOnReturn                  | false    | 归还连接时执行validationQuery检测连接是否有效，做了这个配置会降低性能 |
| testWhileIdle                 | false    | 建议配置为true，不影响性能，并且保证安全性。申请连接的时候检测，如果空闲时间大于timeBetweenEvictionRunsMillis，执行validationQuery检测连接是否有效。 |
| timeBetweenEvictionRunsMillis |          | 有两个含义： 1)Destroy线程会检测连接的间隔时间2)testWhileIdle的判断依据，详细看testWhileIdle属性的说明 |
| numTestsPerEvictionRun        |          | 不再使用，一个DruidDataSource只支持一个EvictionRun           |
| minEvictableIdleTimeMillis    |          |                                                              |
| connectionInitSqls            |          | 物理连接初始化的时候执行的sql                                |
| exceptionSorter               |          | 根据dbType自动识别   当数据库抛出一些不可恢复的异常时，抛弃连接 |
| filters                       |          | 属性类型是字符串，通过别名的方式配置扩展插件，常用的插件有：   监控统计用的filter:stat日志用的filter:log4j防御sql注入的filter:wall |
| proxyFilters                  |          | 类型是List，如果同时配置了filters和proxyFilters，是组合关系，并非替换关系 |



## 第9章：Apache-DBUtils实现CRUD操作

### 9.1 Apache-DBUtils简介

- commons-dbutils 是 Apache 组织提供的一个开源 JDBC工具类库，它是对JDBC的简单封装，学习成本极低，并且使用dbutils能极大简化jdbc编码的工作量，同时也不会影响程序的性能。

- API介绍：
	- org.apache.commons.dbutils.QueryRunner
	- org.apache.commons.dbutils.ResultSetHandler
	- 工具类：org.apache.commons.dbutils.DbUtils   
	
	





### 9.2 主要API的使用

#### 9.2.1 DbUtils

- DbUtils ：提供如关闭连接、装载JDBC驱动程序等常规工作的工具类，里面的所有方法都是静态的。主要方法如下：
	- **public static void close(…) throws java.sql.SQLException**：　DbUtils类提供了三个重载的关闭方法。这些方法检查所提供的参数是不是NULL，如果不是的话，它们就关闭Connection、Statement和ResultSet。
	- <font color='blue'>public static void closeQuietly(…):</font> 这一类方法不仅能在Connection、Statement和ResultSet为NULL情况下避免关闭，还能隐藏一些在程序中抛出的SQLEeception。
	- <font color='blue'>public static void commitAndClose(Connection conn)throws SQLException：</font> 用来提交连接的事务，然后关闭连接
	- <font color='blue'>public static void commitAndCloseQuietly(Connection conn)：</font> 用来提交连接，然后关闭连接，并且在关闭连接时不抛出SQL异常。 
	- <font color='blue'>public static void rollback(Connection conn)throws SQLException：</font>允许conn为null，因为方法内部做了判断
	- <font color='blue'>public static void rollbackAndClose(Connection conn)throws SQLException</font>
	- <font color='blue'>rollbackAndCloseQuietly(Connection)</font>
	- <font color='blue'>public static boolean loadDriver(java.lang.String driverClassName)：</font>这一方装载并注册JDBC驱动程序，如果成功就返回true。使用该方法，你不需要捕捉这个异常ClassNotFoundException。

#### 9.2.2 QueryRunner类

- **该类简单化了SQL查询，它与ResultSetHandler组合在一起使用可以完成大部分的数据库操作，能够大大减少编码量。**

- QueryRunner类提供了两个构造器：
	- 默认的构造器
	- 需要一个 javax.sql.DataSource 来作参数的构造器

- QueryRunner类的主要方法：
	- **更新**
		- public int update(Connection conn, String sql, Object... params) throws SQLException:用来执行一个更新（插入、更新或删除）操作。
		- ......
	- **插入**
		- public <T> T insert(Connection conn,String sql,ResultSetHandler<T> rsh, Object... params) throws SQLException：只支持INSERT语句，其中 rsh - The handler used to create the result object from the ResultSet of auto-generated keys.  返回值: An object generated by the handler.即自动生成的键值
		- ....
	- **批处理**
		- public int[] batch(Connection conn,String sql,Object[][] params)throws SQLException： INSERT, UPDATE, or DELETE语句
		- public <T> T insertBatch(Connection conn,String sql,ResultSetHandler<T> rsh,Object[][] params)throws SQLException：只支持INSERT语句
		- .....
	- **查询**
		- public Object query(Connection conn, String sql, ResultSetHandler rsh,Object... params) throws SQLException：执行一个查询操作，在这个查询中，对象数组中的每个元素值被用来作为查询语句的置换参数。该方法会自行处理 PreparedStatement 和 ResultSet 的创建和关闭。
		- ...... 

- 测试

```java
// 测试添加
@Test
public void testInsert() throws Exception {
	QueryRunner runner = new QueryRunner();
	Connection conn = JDBCUtils.getConnection3();
	String sql = "insert into customers(name,email,birth)values(?,?,?)";
	int count = runner.update(conn, sql, "何成飞", "he@qq.com", "1992-09-08");

	System.out.println("添加了" + count + "条记录");
		
	JDBCUtils.closeResource(conn, null);

}
```

```java
// 测试删除
@Test
public void testDelete() throws Exception {
	QueryRunner runner = new QueryRunner();
	Connection conn = JDBCUtils.getConnection3();
	String sql = "delete from customers where id < ?";
	int count = runner.update(conn, sql,3);

	System.out.println("删除了" + count + "条记录");
		
	JDBCUtils.closeResource(conn, null);

}
```



#### 9.2.3 ResultSetHandler接口及实现类

- 该接口用于处理 java.sql.ResultSet，将数据按要求转换为另一种形式。

- ResultSetHandler 接口提供了一个单独的方法：Object handle (java.sql.ResultSet .rs)。

- 接口的主要实现类：

	- ArrayHandler：把结果集中的第一行数据转成对象数组。

	- ArrayListHandler：把结果集中的每一行数据都转成一个数组，再存放到List中。

	- **BeanHandler：**将结果集中的第一行数据封装到一个对应的JavaBean实例中。

	- **BeanListHandler：**将结果集中的每一行数据都封装到一个对应的JavaBean实例中，存放到List里。

	- ColumnListHandler：将结果集中某一列的数据存放到List中。

	- KeyedHandler(name)：将结果集中的每一行数据都封装到一个Map里，再把这些map再存到一个map里，其key为指定的key。

	- **MapHandler：**将结果集中的第一行数据封装到一个Map里，key是列名，value就是对应的值。

	- **MapListHandler：**将结果集中的每一行数据都封装到一个Map里，然后再存放到List

	- **ScalarHandler：**查询单个值对象

	​	

- 测试

```java
/*
 * 测试查询:查询一条记录
 * 
 * 使用ResultSetHandler的实现类：BeanHandler
 */
@Test
public void testQueryInstance() throws Exception{
	QueryRunner runner = new QueryRunner();

	Connection conn = JDBCUtils.getConnection3();
		
	String sql = "select id,name,email,birth from customers where id = ?";
		
	//
	BeanHandler<Customer> handler = new BeanHandler<>(Customer.class);
	Customer customer = runner.query(conn, sql, handler, 23);
	System.out.println(customer);	
	JDBCUtils.closeResource(conn, null);
}
```

```java
/*
 * 测试查询:查询多条记录构成的集合
 * 
 * 使用ResultSetHandler的实现类：BeanListHandler
 */
@Test
public void testQueryList() throws Exception{
	QueryRunner runner = new QueryRunner();

	Connection conn = JDBCUtils.getConnection3();
		
	String sql = "select id,name,email,birth from customers where id < ?";
		
	//
	BeanListHandler<Customer> handler = new BeanListHandler<>(Customer.class);
	List<Customer> list = runner.query(conn, sql, handler, 23);
	list.forEach(System.out::println);
		
	JDBCUtils.closeResource(conn, null);
}
```

```java
/*
 * 自定义ResultSetHandler的实现类
 */
@Test
public void testQueryInstance1() throws Exception{
	QueryRunner runner = new QueryRunner();

	Connection conn = JDBCUtils.getConnection3();
		
	String sql = "select id,name,email,birth from customers where id = ?";
		
	ResultSetHandler<Customer> handler = new ResultSetHandler<Customer>() {

		@Override
		public Customer handle(ResultSet rs) throws SQLException {
			System.out.println("handle");
//			return new Customer(1,"Tom","tom@126.com",new Date(123323432L));
				
			if(rs.next()){
				int id = rs.getInt("id");
				String name = rs.getString("name");
				String email = rs.getString("email");
				Date birth = rs.getDate("birth");
					
				return new Customer(id, name, email, birth);
			}
			return null;
				
		}
	};
		
	Customer customer = runner.query(conn, sql, handler, 23);
		
	System.out.println(customer);
		
	JDBCUtils.closeResource(conn, null);
}
```

```java
/*
 * 如何查询类似于最大的，最小的，平均的，总和，个数相关的数据，
 * 使用ScalarHandler
 * 
 */
@Test
public void testQueryValue() throws Exception{
	QueryRunner runner = new QueryRunner();

	Connection conn = JDBCUtils.getConnection3();
		
	//测试一：
//	String sql = "select count(*) from customers where id < ?";
//	ScalarHandler handler = new ScalarHandler();
//	long count = (long) runner.query(conn, sql, handler, 20);
//	System.out.println(count);
		
	//测试二：
	String sql = "select max(birth) from customers";
	ScalarHandler handler = new ScalarHandler();
	Date birth = (Date) runner.query(conn, sql, handler);
	System.out.println(birth);
		
	JDBCUtils.closeResource(conn, null);
}
```

## JDBC总结

```java
总结
@Test
public void testUpdateWithTx() {
		
	Connection conn = null;
	try {
		//1.获取连接的操作（
		//① 手写的连接：JDBCUtils.getConnection();
		//② 使用数据库连接池：C3P0;DBCP;Druid
		//2.对数据表进行一系列CRUD操作
		//① 使用PreparedStatement实现通用的增删改、查询操作（version 1.0 \ version 2.0)
//version2.0的增删改public void update(Connection conn,String sql,Object ... args){}
//version2.0的查询 public <T> T getInstance(Connection conn,Class<T> clazz,String sql,Object ... args){}
		//② 使用dbutils提供的jar包中提供的QueryRunner类
			
		//提交数据
		conn.commit();
			
	
	} catch (Exception e) {
		e.printStackTrace();
			
			
		try {
			//回滚数据
			conn.rollback();
		} catch (SQLException e1) {
			e1.printStackTrace();
		}
			
	}finally{
		//3.关闭连接等操作
		//① JDBCUtils.closeResource();
		//② 使用dbutils提供的jar包中提供的DbUtils类提供了关闭的相关操作
			
	}
}
```



#### 相应代码：

##### 一、工具类【JDBCUtils】

静态方法作用：

- ①返回一个连接，或连接池提供
- ②关闭连接操作

```java
package util;

import com.alibaba.druid.pool.DruidDataSourceFactory;
import com.mchange.v2.c3p0.ComboPooledDataSource;
import org.apache.commons.dbcp.BasicDataSourceFactory;
import org.apache.commons.dbutils.DbUtils;

import javax.sql.DataSource;
import java.io.FileInputStream;
import java.io.InputStream;
import java.sql.*;
import java.util.Properties;

/**
 * @ClassName JDBCUtils
 * @Description TODO:
 * @Author sth_199509@163.com
 * @Date 2021/10/25 22:14
 * @Version 1.0
 */
public class JDBCUtils {
    /**
     * 获取连接操作【自己创建连接】
     * @return 返回连接对象
     * @throws Exception
     */
    public static Connection getConnection() throws Exception {
        //1、读取配置文件中的4个信息
        InputStream is = ClassLoader.getSystemClassLoader().getResourceAsStream("jdbc.properties");
        Properties pro = new Properties();
        pro.load(is);
        String user = pro.getProperty("user");
        String password = pro.getProperty("password");
        String url = pro.getProperty("url");
        String driverClass = pro.getProperty("driverClass");
        //2、加载驱动
        Class.forName(driverClass);
        //3、获取连接
        Connection con = DriverManager.getConnection(url,user,password);
        //4、返回对象
        return con;
    }

    /**
     * 使用c3p0连接池技术返回，连接
     */
    //创建池子放在方法外边，要不然每次调用方法，创建一个池子，调用n次，创建n个池子，完蛋了
    private static ComboPooledDataSource cpds = new ComboPooledDataSource("helloc3p0");
    public static Connection getConnection_c3p0() throws SQLException {
        Connection con = cpds.getConnection();
        return  con;
    }


    /**
     * 使用dbcp数据库连接池技术
     * @return
     */
    private static DataSource source;
    //同理，将数据库连接池的创建放到外边，要不然创建n个池子干啥
    //因为涉及到流加载，不能直接声明，通过声明静态代码块，随着类的加载而加载
    static{
        try {
            Properties pros = new Properties();
            FileInputStream is = new FileInputStream("src\\dbcp.properties");
            pros.load(is);
            //创建一个数据库连接池
            source = BasicDataSourceFactory.createDataSource(pros);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    public static Connection getConnection_dbcp() throws SQLException {
        Connection con = source.getConnection();
        return con;
    }


    /**
     * 使用druid数据库连接池技术
     * @return
     */
    private static DataSource sourceDruid;
    //同理，将数据库连接池的创建放到外边，要不然创建n个池子干啥
    //因为涉及到流加载，不能直接声明，通过声明静态代码块，随着类的加载而加载
    static{
        try {
            Properties pros = new Properties();
            InputStream is = ClassLoader.getSystemClassLoader().getResourceAsStream("druid.properties");
            pros.load(is);
            sourceDruid = DruidDataSourceFactory.createDataSource(pros);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    public static Connection getConnection_druid() throws SQLException {
        Connection con = sourceDruid.getConnection();
        return con;
    }

    /**
     * 关闭资源操作
     * @param con 关闭连接
     * @param ps prepareStatement对象关闭
     * @param rs 关闭结果集
     */
    public static void closeResource(Connection con, Statement ps, ResultSet rs){
        //方式一：使用使用dbutils提供的jar包中提供的DbUtils类提供了关闭的相关操作
        try {
            DbUtils.close(con);
        } catch (SQLException e) {
            e.printStackTrace();
        }
        try {
            DbUtils.close(ps);
        } catch (SQLException e) {
            e.printStackTrace();
        }
        try {
            DbUtils.close(rs);
        } catch (SQLException e) {
            e.printStackTrace();
        }

        //方式二：自己手动关闭
//        try {
//            if (ps != null)
//                ps.close();
//        } catch (SQLException e) {
//            e.printStackTrace();
//        }
//        try {
//            if (con != null)
//                con.close();
//        } catch (SQLException e) {
//            e.printStackTrace();
//        }
//        try {
//            if (rs != null)
//                rs.close();
//        } catch (SQLException e) {
//            e.printStackTrace();
//        }
    }
}
```



##### 二、通用查询

- 【使用PreparedStatement实现，不同表的操作】

```java
package util;
import java.lang.reflect.Field;
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.ResultSetMetaData;
import java.util.ArrayList;
import java.util.List;

/**
 * @ClassName PreparedStatementQuery
 * @Description TODO:使用PreparedStatement实现针对不同表的【通用查询】操作
 * @Author sth_199509@163.com
 * @Date 2021/10/26 10:53
 * @Version 1.0
 */
public class PreparedStatementQuery {
//    @Test
//    public void testForList() throws Exception {
//        String sql = "select id,au_Name `name`,nation from author where nation=?";
//        List<Author> forList = getInstanceForList(Author.class, sql, "中国");
//        forList.forEach(System.out::println);
//        System.out.println("---------------------");
//
//        String sql3 = "select * from tulong";
//        List<TuLong> forList1 = getInstanceForList(TuLong.class, sql3);
//        forList1.forEach(System.out::println);
//        System.out.println("---------------------");
//
//        String sql2 = "select id,name,school from tulong where name=?";
//        TuLong instance1 = getInstance(TuLong.class, sql2, "周芷若");
//        System.out.println(instance1);
//    }

    /**
     * 针对不同的表的【通用查询操作】，返回表中的多条数据
     * @param clazz 结果集类
     * @param sql 查询sql语句【名字不同时，记得起别名】
     * @param args 设置占位符
     * @param <T>
     * @return
     * @throws Exception
     */
    public <T> List<T> getInstanceForList(Class<T> clazz, String sql, Object ...args) {
        Connection con = null;
        PreparedStatement pstate = null;
        ResultSet resultSet = null;
        try {
            //1、获取连接
            con = JDBCUtils.getConnection();
            //2、获取实例
            pstate = con.prepareStatement(sql);
            //3、设置占位符
            for (int i = 0; i < args.length; i++) {
                pstate.setObject(i+1,args[i]);
            }
            //4、执行、获取结果集
            resultSet = pstate.executeQuery();
            //5、获取结果集元数据
            ResultSetMetaData metaData = pstate.getMetaData();
            //6、通过结果集的元数据获取列数
            int columnCount = metaData.getColumnCount();
            ArrayList<T> list = new ArrayList<>();
            while (resultSet.next()){
                //7、创建结果集类
                T t = clazz.getDeclaredConstructor().newInstance();
                //处理结果集的每一行，给t对象属性赋值
                for (int i = 0; i < columnCount; i++) {
                    //8、通过结果集获取列值
                    Object value = resultSet.getObject(i + 1);
                    //9、通过元数据获取别名【getColumnLabel】
                    String columnlabel = metaData.getColumnLabel(i + 1);
                    Field field = clazz.getDeclaredField(columnlabel);
                    field.setAccessible(true);
                    field.set(t,value);
                }
                list.add(t);
            }
            return list;
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            //10、关闭资源
            JDBCUtils.closeResource(con,pstate,resultSet);
        }
        return null;
    }
```


​	
```java
//    @Test
//    public void test() throws Exception {
//        String sql = "select id,au_Name `name`,nation from author where nation=?";
//        Author instance = getInstance(Author.class, sql, "日本");
//        System.out.println(instance);
//
//        String sql2 = "select id,name,school from tulong where name=?";
//        TuLong instance1 = getInstance(TuLong.class, sql2, "周芷若");
//        System.out.println(instance1);
//    }
    /**
     * 针对不同的表的【通用查询操作】，返回表中的一条数据
     * @param clazz 结果集类
     * @param sql 查询sql语句【名字不同时，记得起别名】
     * @param args 设置占位符
     * @param <T>
     * @return
     * @throws Exception
     */
    public <T> T getInstance(Class<T> clazz,String sql,Object ...args) {
        Connection con = null;
        PreparedStatement pstate = null;
        ResultSet resultSet = null;
        try {
            //1、获取连接
            con = JDBCUtils.getConnection();
            //2、获取实例
            pstate = con.prepareStatement(sql);
            //3、设置占位符
            for (int i = 0; i < args.length; i++) {
                pstate.setObject(i+1,args[i]);
            }
            //4、执行、获取结果集
            resultSet = pstate.executeQuery();
            //5、获取结果集元数据
            ResultSetMetaData metaData = pstate.getMetaData();
            //6、通过结果集的元数据获取列数
            int columnCount = metaData.getColumnCount();
            if (resultSet.next()){
                //7、创建结果集类
                T t = clazz.getDeclaredConstructor().newInstance();
                for (int i = 0; i < columnCount; i++) {
                    //8、通过结果集获取列值
                    Object value = resultSet.getObject(i + 1);
                    //9、通过元数据获取别名【getColumnLabel】
                    String columnlabel = metaData.getColumnLabel(i + 1);
                    Field field = clazz.getDeclaredField(columnlabel);
                    field.setAccessible(true);
                    field.set(t,value);
                }
                return t;
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            //10、关闭资源
            JDBCUtils.closeResource(con,pstate,resultSet);
        }
        return null;
    }
}
```



##### 三、通用增删改

- 【使用PreparedStatement实现，不同表的操作】


```java
package util;

import org.junit.jupiter.api.Test;
import java.sql.Connection;
import java.sql.PreparedStatement;

/**
 * @ClassName UpdateTest
 * @Description TODO:通用增删改操作
 * @Author sth_199509@163.com
 * @Date 2021/10/25 21:08
 * @Version 1.0
 */
public class UpdateTest {
    @Test
    public void test2(){//测试通用方法
        //删
//        String sql = "delete from tulong where name=?";//注意这个sql语句，【关键词要用``着重号】
//        update(sql,"白眉鹰王");

        //插入元素
        String sql1 = "insert into yitian(bName,bschool,Date)values(?,?,?)";
        update(sql1, "张无忌","明教","1995-09-09");
        update(sql1, "赵敏","元朝","1996-07-10");
        update(sql1, "周芷若","峨眉派","1996-09-08");
        update(sql1, "杨逍","明教","1990-08-04");
        update(sql1, "宋青书","武当派","1998-04-23");
        update(sql1, "乔峰","丐帮","1888-09-13");
    }

```


​	
​	
```java

    /**
     * 通用方法实现数据库的【增删改】操作
     * @param sql sql语句，其中包含n个【问号？】占位符
     * @param args 传入不定形参，个数对应sql语句中的【问号？】个数n
     */
    public void update(String sql,Object ...args){
        Connection con = null;
        PreparedStatement ps = null;
        try {
            //1、获取连接
            con = JDBCUtils.getConnection();

            //2、预编译sql语句，返回PreparedStatement的对象
            ps = con.prepareStatement(sql);

            //3、填充占位符
            for (int i = 0; i < args.length; i++) {
                ps.setObject(i+1,args[i]);//切记数据库索引是从1开始，所以第一个parameterIndex要+1；
            }

            //4、执行
            ps.execute();
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            //5、资源的关闭
            JDBCUpdateUtil.closeResource(con,ps);
        }
    }
}
```



##### 四、第三方jar包【实现增删改查】

- commons-dbutils 是Apache 组织提供的一个开源的JDBC工具类库，封装了针对于数据库的【增删改查】操作

```java
package dbutils;

import bean.YiTian;
import org.apache.commons.dbutils.QueryRunner;
import org.apache.commons.dbutils.ResultSetHandler;
import org.apache.commons.dbutils.handlers.*;
import org.junit.jupiter.api.Test;
import util.JDBCUtils;

import java.sql.Connection;
import java.sql.Date;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.List;
import java.util.Map;

/**
 * @ClassName QueryRunnerTest
 * @Description TODO:commons-dbutils 是Apache 组织提供的一个开源的JDBC工具类库，封装了针对于数据库的【增删改查】操作
 * @Author sth_199509@163.com
 * @Date 2021/10/28 9:23
 * @Version 1.0
 */
public class QueryRunnerTest {

// 本例测试插入，增删改一样，不再测试
    @Test
    public void testUpdate(){
        Connection con = null;
        try {
            QueryRunner runner = new QueryRunner();
            con = JDBCUtils.getConnection_druid();
            String sql = "insert into yitian(bName,bschool,Date)values(?,?,?)";
            int insertCount = runner.update(con, sql, "成昆", "明教", "1994-02-03");
            System.out.println("插入了" + insertCount + "行数据");
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            JDBCUtils.closeResource(con,null,null);
        }
    }

    
    
//测试查询
    /**
     * BeanHandler:是ResultSetHandler接口的实现类，用于封装一条记录
     */
    @Test
    public void testQuery() {
        Connection con = null;
        try {
            QueryRunner runner = new QueryRunner();
            con = JDBCUtils.getConnection_druid();
            String sql = "select id,bName name,bschool school,Date date from yitian where bName=?";
            BeanHandler<YiTian> handler = new BeanHandler<>(YiTian.class);
            YiTian tian = runner.query(con, sql, handler, "周芷若");
            System.out.println(tian);
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            JDBCUtils.closeResource(con,null,null);
        }
    }

    /**
     * BeanHandler:是ResultSetHandler接口的实现类，用于封装多条记录，返回集合
     */
    @Test
    public void testQuerys(){
        Connection con = null;
        try {
            QueryRunner runner = new QueryRunner();
            con = JDBCUtils.getConnection_druid();
            String sql = "select id,bName name,bschool school,Date date from yitian where id<?";
            BeanListHandler<YiTian> handler = new BeanListHandler<>(YiTian.class);
            List<YiTian> tians = runner.query(con, sql, handler, 10);
            tians.forEach(System.out::println);
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            JDBCUtils.closeResource(con,null,null);
        }
    }


    /**
     * MapHandler:是ResultSetHandler接口的实现类，用于封装一条记录
     * 将字段及相应字段的值，作为map中的key和value
     */
    @Test
    public void testMapQuery(){
        Connection con = null;
        try {
            QueryRunner runner = new QueryRunner();
            con = JDBCUtils.getConnection_druid();
            String sql = "select id,bName name,bschool school,Date date from yitian where id=?";
            MapHandler handler = new MapHandler();
            Map<String, Object> query = runner.query(con, sql, handler, 10);
            System.out.println(query);
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            JDBCUtils.closeResource(con,null,null);
        }
    }

    /**
     * MapListHandler:是ResultSetHandler接口的实现类，用于封装多条记录
     * 将字段及相应字段的值，作为map中的key和value，将每个map添加到list中
     */
    @Test
    public void testListMapQuerys(){
        Connection con = null;
        try {
            QueryRunner runner = new QueryRunner();
            con = JDBCUtils.getConnection_druid();
            String sql = "select id,bName name,bschool school,Date date from yitian where id<?";
            MapListHandler handler = new MapListHandler();
            List<Map<String, Object>> mapList = runner.query(con, sql, handler, 10);
            mapList.forEach(System.out::println);
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            JDBCUtils.closeResource(con,null,null);
        }
    }

    /**
     * ScalarHandler:是ResultSetHandler接口的实现类，用于查询特殊值，记录数？最大值？之类的
     *
     */
    @Test
    public void testQuerysValue(){
        Connection con = null;
        try {
            QueryRunner runner = new QueryRunner();
            con = JDBCUtils.getConnection_druid();
            String sql = "select count(*) from yitian";
            ScalarHandler handler = new ScalarHandler();
            Long query = (Long)runner.query(con, sql, handler);
            System.out.println("表中一共有" + query + "条数据");
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            JDBCUtils.closeResource(con,null,null);
        }
    }


    /**
     * 自定义BeanHandler类
     *
     */
    @Test
    public void testQuerys_self(){
        Connection con = null;
        try {
            QueryRunner runner = new QueryRunner();
            con = JDBCUtils.getConnection_druid();
            String sql = "select id,bName name,bschool school,Date date from yitian where id=?";
            //自定义
            ResultSetHandler<YiTian> handler = new ResultSetHandler<>(){

                @Override
                public YiTian handle(ResultSet resultSet) throws SQLException {
                    if (resultSet.next()){
                        int id = resultSet.getInt("id");//查询标签
                        String name = resultSet.getString("name");
                        String school = resultSet.getString("school");
                        Date date = resultSet.getDate("date");
                        return new YiTian(id,name,school,date);
                    }
                    return null;
                }
            };
            YiTian yiTian = runner.query(con, sql, handler, 2);
            System.out.println(yiTian);
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            JDBCUtils.closeResource(con,null,null);
        }
    }

}
```



##### 五、DAO全套文件

- BaseDAO:封装了对数据表的一系列通用操作
- YiTianDAO：接口，封装了一些列想要实现的操作，用抽象方法

- YiTianDAOImpl：具体实现类，继承BaseDAO类，实现YiTianDAO接口
- YiTianDAOImplTest：测试类
- 每个表要有一个相应的Bean类，字段对应属性





- 每个表，对应建一个【BaseDAO类】和 【类名DAO接口】，然后由实现类实现相应操作

![image-20211028103849069](https://pledge99.oss-cn-beijing.aliyuncs.com/img/微信图片_20211027231347-16353476600582.jpg)

- BaseDAO:封装了对数据表的一系列通用操作

```java
package baseDAOPro;

import util.JDBCUpdateUtil;
import util.JDBCUtils;

import java.lang.reflect.Field;
import java.lang.reflect.ParameterizedType;
import java.lang.reflect.Type;
import java.sql.*;
import java.util.ArrayList;
import java.util.List;

/**
 * @ClassName BaseDAO
 * @Description TODO:封装了对数据表的一系列通用操作
 * @Author sth_199509@163.com
 * @Date 2021/10/27 17:13
 * @Version 1.0
 */
public abstract class BaseDAO<T> {//设置成抽象类，不允许造对象
    private Class<T> clazz = null;
    {
        //获取带泛型的父类
        Type genericSuperclass = this.getClass().getGenericSuperclass();//this是子类的对象，继承！
        ParameterizedType paramType = (ParameterizedType) genericSuperclass;
        Type[] arguments = paramType.getActualTypeArguments();//获取了父类的泛型【可能有多个泛型，所以是数组】
        clazz = (Class<T>)arguments[0];//泛型的第一个参数
    }
    /**
     * 针对不同的表的【通用查询操作】，返回表中的多条数据【支持事务版本】
     * @param sql 查询sql语句【名字不同时，记得起别名】
     * @param args 设置占位符
     * @return
     * @throws Exception
     */
    public List<T> getInstanceForList(Connection con, String sql, Object ...args) {
        PreparedStatement pstate = null;
        ResultSet resultSet = null;
        try {
            //1、获取实例
            pstate = con.prepareStatement(sql);
            //2、设置占位符
            for (int i = 0; i < args.length; i++) {
                pstate.setObject(i+1,args[i]);
            }
            //3、执行、获取结果集
            resultSet = pstate.executeQuery();
            //4、获取结果集元数据
            ResultSetMetaData metaData = pstate.getMetaData();
            //5、通过结果集的元数据获取列数
            int columnCount = metaData.getColumnCount();
            ArrayList<T> list = new ArrayList<>();
            while (resultSet.next()){
                //6、创建结果集类
                T t = clazz.getDeclaredConstructor().newInstance();
                //处理结果集的每一行，给t对象属性赋值
                for (int i = 0; i < columnCount; i++) {
                    //7、通过结果集获取列值
                    Object value = resultSet.getObject(i + 1);
                    //8、通过元数据获取别名【getColumnLabel】
                    String columnlabel = metaData.getColumnLabel(i + 1);
                    Field field = clazz.getDeclaredField(columnlabel);
                    field.setAccessible(true);
                    field.set(t,value);
                }
                list.add(t);
            }
            return list;
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            //9、关闭资源
            JDBCUtils.closeResource(null,pstate,resultSet);//连接在外边创建，在外边关闭，此处不作处理
        }
        return null;
    }

    /**
     * 针对不同的表的【通用查询操作】，返回表中的一条数据【支持事务版本】
     * @param clazz 结果集类
     * @param sql 查询sql语句【名字不同时，记得起别名】
     * @param args 设置占位符
     * @param <T>
     * @return
     * @throws Exception
     */
    public T getInstance(Connection con,String sql,Object ...args) {
        PreparedStatement pstate = null;
        ResultSet resultSet = null;
        try {
            //1、获取实例
            pstate = con.prepareStatement(sql);
            //2、设置占位符
            for (int i = 0; i < args.length; i++) {
                pstate.setObject(i+1,args[i]);
            }
            //3、执行、获取结果集
            resultSet = pstate.executeQuery();
            //4、获取结果集元数据
            ResultSetMetaData metaData = pstate.getMetaData();
            //5、通过结果集的元数据获取列数
            int columnCount = metaData.getColumnCount();
            if (resultSet.next()){
                //6、创建结果集类
                T t = clazz.getDeclaredConstructor().newInstance();
                for (int i = 0; i < columnCount; i++) {
                    //7、通过结果集获取列值
                    Object value = resultSet.getObject(i + 1);
                    //8、通过元数据获取别名【getColumnLabel】
                    String columnlabel = metaData.getColumnLabel(i + 1);
                    Field field = clazz.getDeclaredField(columnlabel);
                    field.setAccessible(true);
                    field.set(t,value);
                }
                return t;
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            //9、关闭资源
            JDBCUtils.closeResource(null,pstate,resultSet);//连接在外边创建，在外边关闭，此处不作处理
        }
        return null;
    }

    /**
     * 【支持事务版本】
     * 通用方法实现数据库的【增删改】操作
     * @param sql sql语句，其中包含n个【问号？】占位符
     * @param args 传入不定形参，个数对应sql语句中的【问号？】个数n
     */
    public void update(Connection con,String sql,Object ...args){
        PreparedStatement ps = null;
        try {
            //1、预编译sql语句，返回PreparedStatement的对象
            ps = con.prepareStatement(sql);

            //2、填充占位符
            for (int i = 0; i < args.length; i++) {
                ps.setObject(i+1,args[i]);//切记数据库索引是从1开始，所以第一个parameterIndex要+1；
            }

            //3、执行
            ps.execute();
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            //4、资源的关闭
            JDBCUpdateUtil.closeResource(null,ps);//连接在外边创建，在外边关闭，此处不作处理
        }
    }

    /**
     * 用于查询特殊值的通用方法，如count()
     * @param con
     * @param sql
     * @param args
     * @param <E>
     * @return
     */
    public <E> E getValue(Connection con,String sql,Object ...args){
        PreparedStatement ps = null;
        ResultSet resultSet = null;
        try {
            ps = con.prepareStatement(sql);
            for (int i = 0; i < args.length; i++) {
                ps.setObject(i+1,args[i]);//MySQL数据库索引从1开始
            }
            resultSet = ps.executeQuery();
            if (resultSet.next()){//仅一条查询结果
                return (E)resultSet.getObject(1);
            }
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            JDBCUtils.closeResource(null,ps,resultSet);
        }
        return null;
    }
}
```


​	

- YiTianDAO：接口，封装了一些列想要实现的操作，用抽象方法

~~~java
```java
package baseDAOPro;

import bean.YiTian;

import java.sql.Connection;
import java.sql.Date;
import java.util.List;

/**
 * @ClassName UsersDAO
 * @Description TODO:
 * @Author sth_199509@163.com
 * @Date 2021/10/27 17:31
 * @Version 1.0
 */
public interface YiTianDAO {
    /**
     * 将user对象添加到数据库中
     * @param con
     * @param yitian
     */
    void insert(Connection con, YiTian yitian);

    /**
     * 针对指定id删除表中的一条数据
     * @param con
     * @param id
     */
    void deleteById(Connection con,int id);

    /**
     * 针对user对象，去修改数据表中的指定数据
     * @param con
     * @param yitian
     */
    void update(Connection con, YiTian yitian);

    /**
     * 针对指定id，查询得到对应的Users对象
     * @param con
     * @param id
     */
    YiTian getUsersById(Connection con, int id);

    /**
     * 查询表中所有的记录，返回集合
     * @param con
     * @return
     */
    List<YiTian> getAll(Connection con);

    /**
     * 返回数据表的记录条数
     * @param con
     * @return
     */
    Long getCount(Connection con);

    /**
     * 返回记录中的最大生日
     * @param con
     * @return
     */
    Date getMaxBirth(Connection con);
}
```
~~~



- YiTianDAOImpl：具体实现类，继承BaseDAO类，实现YiTianDAO接口

~~~java
```java
package baseDAOPro;

import bean.YiTian;

import java.sql.Connection;
import java.sql.Date;
import java.util.List;

/**
 * @ClassName YiTianDAOImpl
 * @Description TODO:
 * @Author sth_199509@163.com
 * @Date 2021/10/27 17:46
 * @Version 1.0
 */
public class YiTianDAOImpl extends BaseDAO<YiTian> implements YiTianDAO {
@Override
    public void insert(Connection con, YiTian yitian) {
        String sql = "insert into yitian(bName,bschool,`Date`)values(?,?,?)";
        update(con,sql,yitian.getName(),yitian.getSchool(),yitian.getDate());
    }

    @Override
    public void deleteById(Connection con, int id) {
        String sql = "delete from yitian where id = ?";
        update(con,sql,id);
    }

    @Override
    public void update(Connection con, YiTian yitian) {
        String sql = "update yitian set bName=?,bschool=?,Date=? where id=?";
        update(con,sql,yitian.getName(),yitian.getSchool(),yitian.getDate(),yitian.getId());
    }

    @Override
    public YiTian getUsersById(Connection con, int id) {
        String sql = "select id,bName name,bschool school,Date date from yitian where id=?";
        YiTian yiTian = getInstance(con, sql, id);
        return yiTian;
    }

    @Override
    public List<YiTian> getAll(Connection con) {
        String sql = "select id,bName name,bschool school,Date date from yitian";
        List<YiTian> list = getInstanceForList(con, sql);
        return list;
    }

    @Override
    public Long getCount(Connection con) {
        String sql = "select count(*) from yitian";
        return getValue(con,sql);
    }

    @Override
    public Date getMaxBirth(Connection con) {
        String sql = "select max(Date) from yitian";
        return getValue(con,sql);
    }
}
~~~


​	



- YiTianDAOImplTest：测试类



```java
package baseDAOPro;

import bean.YiTian;

import org.junit.jupiter.api.Test;
import util.JDBCUpdateUtil;
import util.JDBCUtils;

import java.sql.Connection;
import java.sql.Date;
import java.text.SimpleDateFormat;
import java.util.List;

/**
 * @ClassName YiTianDAOImplTest
 * @Description TODO:
 * @Author sth_199509@163.com
 * @Date 2021/10/27 18:11
 * @Version 1.0
 */
class YiTianDAOImplTest {

    private baseDAOPro.YiTianDAOImpl dao = new YiTianDAOImpl();

    @Test
    void insert() {
        Connection con = null;
        try {
            con = JDBCUpdateUtil.getConnection();

            SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
            long time = sdf.parse("1900-01-02").getTime();
            Date date = new Date(time);

            YiTian xz = new YiTian(1, "谢逊", "明教", date);
            dao.insert(con,xz);
            System.out.println("添加成功！");
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            JDBCUpdateUtil.closeResource(con,null);
        }
    }

    @Test
    void deleteById() {
        Connection con = null;
        try {
            con = JDBCUpdateUtil.getConnection();

            dao.deleteById(con,11);

            System.out.println("删除成功！");
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            JDBCUpdateUtil.closeResource(con,null);
        }
    }

    @Test
    void update() {
        Connection con = null;
        try {
            con = JDBCUpdateUtil.getConnection();

            String sql = "update yitian set bName=?,bschool=? where id=?";
            dao.update(con,sql,"阿离","天鹰教",5);

            System.out.println("修改成功！");
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            JDBCUpdateUtil.closeResource(con,null);
        }
    }

    @Test
    void getUsersById() {
        Connection con = null;
        try {
//            con = JDBCUpdateUtil.getConnection();
//            con = JDBCUtils.getConnection_c3p0();//测试c3p0连接池
            con = JDBCUtils.getConnection_dbcp();//测试dbcp连接池
//            con = JDBCUtils.getConnection_druid();//测试dbcp连接池
			YiTian user = dao.getUsersById(con, 1);
            System.out.println(user);

            System.out.println("查询成功！");
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            JDBCUpdateUtil.closeResource(con,null);
        }
    }

    @Test
    void getAll() {
        Connection con = null;
        try {
            con = JDBCUpdateUtil.getConnection();

            List<YiTian> all = dao.getAll(con);
            all.forEach(System.out::println);

            System.out.println("查询成功！");
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            JDBCUpdateUtil.closeResource(con,null);
        }
    }

    @Test
    void getCount() {
        Connection con = null;
        try {
            con = JDBCUpdateUtil.getConnection();

            Long count = dao.getCount(con);
            System.out.println("记录总条数为：" + count);

            System.out.println("查询成功！");
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            JDBCUpdateUtil.closeResource(con,null);
        }
    }

    @Test
    void getMaxBirth() {
        Connection con = null;
        try {
            con = JDBCUpdateUtil.getConnection();

            Date maxBirth = dao.getMaxBirth(con);
            System.out.println("最大生日为：" + maxBirth);

            System.out.println("查询成功！");
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            JDBCUpdateUtil.closeResource(con,null);
        }
    }
}
```


​	

## 面试题



### Statement与PreparedStatement的区别？？

- Preparedstatement是预处理过的，对于批量处理可以大大提高效率
- 数据库只进行一次处理时，用Statement对象进行处理，Preparedstatement开销比Statement大，对于一次性操作无好处
- Statement每次执行SQL语句时，相关数据库都要执行SQL的编译，PrepareStatement是预编译的，支持批处理
- Preparedstatement对象可以防止SQL注入更加安全。



































