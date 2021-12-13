# Maven笔记

## Maven安装

### 1、官网下载

官网地址：https://maven.apache.org/download.cgi

![image-20211212164853953](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211212164853953.png)

### 2、压缩包解压	

下载下来都是压缩包，直接找地方解压就行了【跟Tomcat一样】，路径最好不要带中文

我的路径：/Users/tianhao/MyApp/apache-maven-3.8.4

![image-20211212165310858](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211212165310858.png)

### 3、环境配置

在用户/用户名 地址下：

- 按==option + command + .==

  - 打开隐藏文件显示

- 找到==.zshrc==打开更改内容如下

  - 务必要有JAVA_HOME的配置信息【就是jdk的环境配置】

  - ```dockerfile
    # JAVA_HOME配置
    export JAVA_HOME="/Users/tianhao/Library/Java/JavaVirtualMachines/jdk-17.0.1/Contents/Home"
    
    # Maven配置
    export MAVEN_HOME=/Users/tianhao/MyApp/apache-maven-3.8.4
    export PATH=$PATH:$MAVEN_HOME/bin
    ```

    ![image-20211212165812952](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211212165812952.png)

### 4、验证安装

终端输入==mvn -v==

显示如下效果，表示成功![image-20211212170339092](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211212170339092.png)

## 更改本地仓库位置

中央仓库存放所有需要的jar包等依赖文件，可以自己更改个位置，如D盘之类的



### 1、打开maven的解压目录

找到settings.xml文件![image-20211212170907055](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211212170907055.png)

### 2、更改settings.xml

```xml
找到此处
<!-- localRepository
   | The path to the local repository maven will use to store artifacts.
   |
   | Default: ${user.home}/.m2/repository
  <localRepository>/path/to/local/repo</localRepository>
-->

  <!-- 
      更改默认jar包的位置【默认是/Users/tianhao/.m2/repository】
      这里就先不改了，就放在默认位置
			直接修改下面的路径位置，就可以了
    -->
  <localRepository>/path/to/local/repo</localRepository>
```



## 更改中央仓库下载镜像

### 1、打开maven的解压目录

找到settings.xml文件![image-20211212170907055](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211212170907055.png)

### 2、更改settings.xml

```xml
<mirrors>
  
  
<!-- 中央仓库位置 -->
    <!-- <mirror>
      <id>maven-default-http-blocker</id>
      <mirrorOf>external:http:*</mirrorOf>
      <name>Pseudo repository to mirror external repositories initially using HTTP.</name>
      <url>http://0.0.0.0/</url>
      <blocked>true</blocked>
    </mirror>


<!-- 换成阿里巴巴的国内镜像 -->
    <mirror>
      <id>nexus-aliyun</id>
      <mirrorOf>central</mirrorOf>
      <name>Nexus aliyun</name>
      <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
      <!-- <blocked>true</blocked> -->
  	</mirror>
  
  
</mirrors>

  

```



![image-20211212171028394](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211212171028394.png)



## IDEA中集成Maven环境

### 1、设置

File -> New Projects Setup -> Perferences for New Projects...![image-20211212175113676](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211212175113676.png)

直接搜maven

- Maven home path：选择maven的解压目录

- User settings file ： 选择maven目录下，我们更改的settings文件【需要勾选Override】

![image-20211212180650937](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211212180650937.png)



### 2、Maven项目创建

#### Java项目的创建

![image-20211212175834412](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211212175834412.png)

下一步填写工程名称、路径、包名，继续finish即可。【期间可以看到配置Maven界面，已经保留了我们设置的内容】![image-20211212182308094](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211212182308094.png)

创建好的Java项目可能会没有resources目录，自己手动创建，再选择Mark Directory as Resources Root![image-20211212181700483](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211212181700483.png)

创建的时候，IDEA也会提醒，直接回车，文件类型都选好了![image-20211212181908581](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211212181908581.png)

创建Maven命令

![image-20211212191921147](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211212191921147.png)

运行Maven命令![image-20211212193641562](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211212193641562.png)

#### Web项目的创建

步骤同上，在选择模板时，选webapp，创建完成后需要修改部分配置![image-20211212194102716](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211212194102716.png)

==**直接在pom.xml文件中做如下修改：**==![image-20211212195047046](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211212195047046.png)

##### 1、修改jdk版本

- 默认是1.7，改成自己使用的jdk版本

```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>1.17</maven.compiler.source>
    <maven.compiler.target>1.17</maven.compiler.target>
  </properties>
```

##### 2、修改junit版本

- 可以到中央仓库中查看最新的版本是哪个，直接改名就行

- ![image-20211212195951761](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211212195951761.png)

  ```xml
  <dependencies>
      <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.13</version>
        <scope>test</scope>
      </dependency>
    </dependencies>
  ```

##### 3、	删除<plugins>标签里面的内容

<plugins>标签留下，下边还要在里面添加插件

```xml
		<pluginManagement>
      <plugins>
    		
<!-- lock down plugins versions to avoid using Maven defaults (may be moved to parent pom)-->
				都是些插件版本相关，直接删除
      </plugins>
    </pluginManagement>
```

##### 4、添加web部署的插件

在<plugins>标签内部添加，插件添加方法：

- ==Tomcat插件==

  打开maven官网，选择插件![image-20211212203242068](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211212203242068.png)

  下拉，并找到目标插件![image-20211212203410164](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211212203410164.png)

  点击插件名，跳转插件官网、选择目标版本点击![image-20211212203550915](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211212203550915.png)

  选择目标版本，复制代码，插入<plugins>标签![image-20211212203739778](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211212203739778.png)

```xml
<!-- Tomcat插件-->
<plugin>
  <groupId>org.apache.tomcat.maven</groupId>
  <artifactId>tomcat7-maven-plugin</artifactId>
  <version>2.2</version>

  <!-- 自己额外设置的 -->
  <configuration>
      <!-- 可指定当前项目的站点名 即对外访问路径-->
      <path>/MyMaven02</path>
      <port>8080</port> <!-- 设置启动的端口号 默认8080 -->
      <uriEncoding>UTF-8</uriEncoding> <!-- 设置字符集编码 -->
      <server>tomcat_MyMaven02</server> <!-- 服务器名称 -->
  </configuration>
</plugin>
```

- ==jetty插件==

  pom.xml文件的在<plugins>标签内部添加，插件添加方法：

  ```xml
  <!-- jetty插件-->
  <plugin>
    <groupId>org.eclipse.jetty</groupId>
    <artifactId>jetty-maven-plugin</artifactId>
    <version>9.2.11.v20150529</version>
  
    <!-- 自己额外设置的 -->
    <configuration>
        <!-- 热部署，每10秒扫描1次-->
        <scanIntervalSeconds>10</scanIntervalSeconds>
  
        <webApp>
            <!-- 可指定当前项目的站点名-->
            <contextPath>/MyMaven02</contextPath>
        </webApp>
  
        <httpConnector>
            <!-- 设置启动的端口号  -->
            <port>8888</port>
      	</httpConnector>
    </configuration>
  </plugin>
  ```

##### 5、运行插件

可以直接执行maven命令，也可以把maven命令添加到==运行按钮==处![image-20211212233422285](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211212233422285.png)

添加maven命令![image-20211212233535434](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211212233535434.png)

直接点击运行按钮即可~~~![image-20211212233639285](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211212233639285.png)

## Maven环境下构建多模块项目

### 1、创建模块

四个模块：

- maven_parent：总项目
  - 创建时选择maven
  - 不选择模板
- maven_dao：jdbc层
  - 创建时选择普通的Java模板【quickstart】
- maven_service：服务层
  - 创建时选择普通的Java模板【quickstart】
- maven_controller：控制模块
  - 创建时选择普通的web模板【webapp】![image-20211213000209165](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211213000209165.png)

### 2、修改模块配置

- 设置JDK版本

  ```xml
  <properties>
      <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
      <maven.compiler.source>17</maven.compiler.source>
      <maven.compiler.target>17</maven.compiler.target>
  </properties>
  ```

- 设置单元测试JUnit版本

  ```xml
  <dependencies>
      <dependency>
          <groupId>junit</groupId>
          <artifactId>junit</artifactId>
          <version>4.13</version>
          <scope>test</scope>
      </dependency>
  </dependencies>
  ```

- 删除多余的插件配置

```xml
<build>
    <pluginManagement>
        <plugins>


        </plugins>
    </pluginManagement>
</build>
```



### 3、设置模块之间的依赖

模块间的依赖就是相互导包（import），导包要提前在pom.xml中添加依赖，也可以让IDEA处理

比如：service层要用调用dao层的类

- **在maven_service模块的pom.xml文件中修改，添加依赖**

- ```xml
  <dependencies>
      <dependency>
          <groupId>junit</groupId>
          <artifactId>junit</artifactId>
          <version>4.13</version>
          <scope>test</scope>
      </dependency>
      <!--  引入maven_dao模块的依赖，引入后才能导包import      -->
      <dependency>
          <groupId>com.tianhao</groupId>
          <artifactId>maven_dao</artifactId>
          <version>1.0-SNAPSHOT</version>
          <scope>compile</scope>
      </dependency>
  </dependencies>
  ```

- **然后在service类中import**

![image-20211213104537389](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211213104537389.png)

同理，需要包或者模块之间，相互调用的，只要涉及到==import导包==操作的，对应的包都要在==当前模块的pom.xml文件中添加依赖==

如：servlet包

**依赖：**

```xml
<dependencies>
     <!--  添加单元测试依赖，引入后才能导包import      --> 
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.13</version>
        <scope>test</scope>
    </dependency>
  
  
    <!--  引入maven_service模块的依赖，引入后才能导包import      -->
    <dependency>
        <groupId>com.tianhao</groupId>
        <artifactId>maven_service</artifactId>
        <version>1.0-SNAPSHOT</version>
        <scope>compile</scope>
    </dependency>
  
  
    <!--  引入servlet的依赖     -->
    <!-- https://mvnrepository.com/artifact/javax.servlet/javax.servlet-api -->
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>javax.servlet-api</artifactId>
        <version>3.1.0</version>
        <scope>provided</scope>
    </dependency>
</dependencies>
```

**导包：**

![image-20211213105115273](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211213105115273.png)

### 4、如何寻找依赖

**在百度搜mvn**

![image-20211213123527545](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211213123527545.png)

进入网页https://mvnrepository.com

**直接搜自己要找的包就行了**

![image-20211213123706006](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211213123706006.png)

**选择一个版本，点进去**

![image-20211213123746965](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211213123746965.png)

**直接copy依赖就行了**

![image-20211213123820437](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211213123820437.png)

**复制到pom.xml文件**

```xml
<dependencies>
  	复制到这个标签下面
</dependencies>
```

## Maven打包项目

### 1、建立对应的目录结构

没有的目录自己创建，并修改目录类型

如资源目录，java目录，资源下边的【开发时资源】、【正式版资源】、【测试资源】

![image-20211213141913783](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211213141913783.png)

### 2、添加Profile配置【pom.xml文件中】

```xml
	<dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.13</version>
      <scope>test</scope>
    </dependency>
  </dependencies>

  <!-- 打包环境配置  开发环境dev、测试环境test、正式环境product -->
  <profiles>
    <!-- 开发环境dev -->
    <profile>
      <id>dev</id> <!-- 名字要和文件名对应 -->
      <properties>
              <env>dev</env> <!-- 名字要和文件名对应 -->
      </properties>

      <!--  未指定环境时，默认打包dev环境      -->
      <activation>
        <activeByDefault>true</activeByDefault>
      </activation>
    </profile>

    <!-- 测试环境test -->
    <profile>
      <id>test</id><!-- 名字要和文件名对应 -->
      <properties>
        <env>test</env><!-- 名字要和文件名对应 -->
      </properties>
    </profile>

    <!-- 正式环境product -->
    <profile>
      <id>product</id><!-- 名字要和文件名对应 -->
      <properties>
        <env>product</env><!-- 名字要和文件名对应 -->
      </properties>
    </profile>
  </profiles>
```

### 3、设置资源文件配置

在build标签下

```xml
<build>
    <finalName>maven_package</finalName>
    

  <!--  对于项目资源文件的配置放在build中  -->
    <resources>
      <resource>
        	<directory>src/main/resources/${env}</directory>
      </resource>
      <resource>
          <directory>src/main/java</directory>
          <includes>
              <include>**/*.xml</include>
              <include>**/*.properties</include>
              <include>**/*.tld</include>
          </includes>
          <filtering>false</filtering>
      </resource>
    </resources>
  </build>
```

### 4、添加打包插件

```xml
<!-- 这个是web程序的插件、打包jar包需要单独插件 -->
<pluginManagement>
      <plugins>
          <plugin>
              <groupId>org.apache.maven.plugins</groupId>
              <artifactId>maven-war-plugin</artifactId>
              <version>3.2.2</version>
          </plugin>
      </plugins>
</pluginManagement>
```

### 5、执行打包操作

**maven命令**

- ==clean compile package -Pdev -Dmaven.test.skip=true==

  打包默认环境（dev开发环境）并且跳过maven的测试操作

- ==clean compile package -Ptest -Dmaven.test.skip=true==

  打包测试环境，并且跳过maven的测试操作

- ==clean compile package -Pproduct -Dmaven.test.skip=true==

  打包生产环境，并且跳过maven的测试操作

![image-20211213143454526](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211213143454526.png)

**打包成功**

![image-20211213143421710](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211213143421710.png)

## Maven命令

**1） mvn clean: 清理命令， **

- 作用：删除以前生成的数据， 删除target目录。

- 插件： maven-clean-plugin   ， 版本是 2.5


**2）mvn compile:编译命令，执行的代码编译， 把src/main/java目录中的java代码编译为class文件。**

​     同时把class文件拷贝到 target/classes目录。 这个目录classes是存放类文件的根目录（也叫做类路径，classpath）



​    插件： maven-compiler-plugin 版本3.1。  编译代码的插件

​                maven-resources-plugin 版本2.6 。 资源插件， 处理文件的。 作用是把src/main/resources目录中的                

​                                                             文件拷贝target/classes目录中。

3）mvn test-compile: 编译命令， 编译src/test/java目录中的源文件， 把生成的class拷贝到target/test-classes目录。同时把src/test/resources目录中的文件拷贝到 test-clasess目录

​    插件： maven-compiler-plugin 版本3.1。  编译代码的插件

​                maven-resources-plugin 版本2.6 。 资源插件， 处理文件的



4）mvn test:测试命令， 作用执行 test-classes目录的程序， 测试src/main/java目录中的主程序代码是否符合要求。

​     插件： maven-surefire-plugin 版本 2.12.4



5）mvn package:打包，作用是把项目中的资源class文件和配置文件都放到一个压缩文件中， 默认压缩文件是jar类型的。 web应用是war类型， 扩展是jar，war的。

​    插件：maven-jar-plugin 版本 2.4。 执行打包处理。 生成一个jar扩展的文件， 放在target目录下.

​               打包的文件包含的是 src/main目录中的所有的生成的class和配置文件和test无关。



​    生成的是 ch01-maven-1.0-SNAPSHOT.jar

```xml
  <groupId>com.bjpowernode</groupId>
  <artifactId>ch01-maven</artifactId>
  <version>1.0-SNAPSHOT</version>
  <packaging>jar</packaging>
打包的文件名： artifactId-version.packaging
```

6）mvn install : 把生成的打包的文件 ，安装到maven仓库。

​     插件： maven-install-plugin 版本 2.4 。 把生成的jar文件安装到本地仓库。 

​    查看查看中的jar文件：