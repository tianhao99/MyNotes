# MySQL数据库学习笔记



## 一、数据库的相关概念

### 1、数据库的好处

- 可以持久化数据到本地
- 支持结构化查询

### 2、数据库的常见概念

- <font color='red'>**DB**</font>：数据库，存储数据的容器

- <font color='red'>**DBMS**</font>：数据库管理系统，又称为数据库软件或数据库产品，用于创建或管理数据库（DB）

- <font color='red'>**SQL**</font>：结构化查询语言，用于和数据库通信的语言，不是某个数据库所特有的，而是几乎所有主流的数据库软件通用语言

### 3、数据库存储数据的特点

- 数据存放到表中，然后表再放到库中

- 一个数据库中可以有多张表，每张表具有唯一的表名用来标识自己

- 表中有一个或多个列，列又称为“字段”，相当于Java中的“属性”

- 表中的每一行数据，相当于Java中的一个“对象”

### 4、常见的数据库管理系统

- MySQL

- Oracle

- DB2

- SqlServer



## 二、MySQL的产品介绍

### 1、MySQL的背景

- 前身属于瑞典的一家公司-----MySQL AB

- 2008年被SUN公司收购

- 2009年SUN公司被Oracle公司收购

### 2、MySQL的优点

- 开源、免费、成本低

- 性能高、移植性好

- 体积小、便于安装

### 3、MySQL服务的启动和停止

方式一：计算机--->右键管理--->服务

![image-20211007090250217](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211007124551034-16335819523551.png)

方式二：通过管理员身份运行

- net start 服务名（启动服务）
- net stop 服务名（停止服务）

### 4、MySQL服务的登录和退出

方式一：通过MySQL自带的客户端【仅限于root用户】

方式二：通过Windows自带的客户端

**登录**：mysql -h 主机名 -P端口号   -u用户名  -p 回车【MySQL -u root -p】

输入：密码

**退出**：

exit、ctrl + c



### 5、MySQL的常见命令

1. <font color='red'>查看当前所有数据库</font>

	```mysql
	show databases;
	```

2. <font color='red'>打开指定的库</font>

	```mysql
	use 库名;
	```

3. <font color='red'>查看当前数据可的所有表</font>

	```mysql
	show tables;
	```

4. <font color='red'>创建表</font>

	```mysql
	create table 表名(
		列名 列类型，
		列名 列类型，
		。。。。
	);
	```

5. <font color='red'>查看表结构</font>

	```mysql
	desc 表名;
	```

6. <font color='red'>查看其他库的所有表</font>

	```mysql
	show tables from 库名;
	```

7. <font color='red'>查看服务器的版本</font>

	```mysql
	方式一：登录到MySQL服务端
	select version
	或者
	MySQL --V
	```

	

### 6、MySQL的语法规范

一、不区分大小写，但是建议关键字大写，表名、列名小写；

二、每条命令最好用分号结尾

三、每条命令根据需要，可以进行缩进或者换行

四、注释

​		单行注释：#注释文字

​		单行注释：-- 注释文字【中间有个空格】

​		多行注释：/*注释文字*/

### 7、MySQL中的存储引擎

- **概念：**
	- 在MySQL中的数据用各种不同的技术存储在文件或内存中

- 通过show engines；来查看MySQL支持的存储引擎

- 在MySQL中用的最多的存储引擎有：
	- InnoDB：支持事务
	- MyISAM：不支持事务
	- MEMORY：不支持事务
	- 

## 三、DQL语言基础

### 1、基础查询

**语法：**
**<font color='red'>SELECT 查询列表 FROM 表名；</font>**

**特点：**
1、查询列表可以是：表中的字段、常量值、表达式、函数；
2、查询的结果可以是一个虚拟的表格



测试用表：city

![image-20211007124551034](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211007124703092-16335820244892.png)

- <font color='red'>查询表中的单个字段</font>

	> ```sql
	> SELECT `Name` FROM city;
	> -- ``这个是着重号，加上以后防止列名和关键字重名，加上后就不再识别为关键字
	> ```

![image-20211007124703092](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211007124716442-16335820389233.png)

- <font color='red'>查询表中的多个字段</font>

	> ```sql
	> SELECT name,population FROM city;
	> ```
	>
	> ![image-20211007124716442](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211007090250217-16335685717101.png)

	

- <font color='red'>查询表中的所有字段</font>

	```sql
	SELECT * FROM city;-- 缺点：不能改变表的顺序，只能按原列顺序
	```

	![image-20211007124733789](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211007124743640-16335820644735.png)

- <font color='red'>查询常量值</font>

	```sql
	SELECT 100;
	SELECT 'join';
	```

	![image-20211007124743640](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211007124809142-16335820916186.png)

	![image-20211007124809142](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211007124833279.png)

- <font color='red'>查询表达式</font>

	```sql
	SELECT 100%98;
	```

	![image-20211007124833279](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211007124843910-16335821257467.png)

- <font color='red'>查询函数</font>

	```sql
	SELECT VERSION();-- 版本信息
	```

	![image-20211007124843910](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211007124915496-16335821565648.png)

- <font color='red'>起别名</font>

	- 便于理解

	- 如果要查询的字段有重名的情况，使用别名可以区分开来

	- 方式一：使用 AS

		```sql
		SELECT 100%97 AS 结果;
		SELECT `name` AS 姓名, population AS 人口数 FROM city;
		```

		![image-20211007124915496](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211007124926397-16335821675709.png)

		![image-20211007124926397](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211007125021559-163358222271510.png)

	- 方式二：使用  空格即可

		```sql
		SELECT 100%97 结果;
		SELECT `name` 姓名, population AS 人口数 FROM city;
		```

- **注意：**当别名中有关键字、空格、特殊字符时，加双引号处理，防止歧义，造成语法错误。

- <font color='red'>去重</font>

	案例：查询参与评选的城市都有哪些
	直接查询城市代码[有好多重复的代码]

	```sql
	SELECT `countryCode` FROM city;
	-- 去重DISTINCT
	SELECT DISTINCT `countryCode` FROM city;
	```

	未用去重函数时：![image-20211007125021559](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211007125059657-163358226099411.png)

	使用去重函数DISTINCT后![image-20211007125059657](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211007124733789-16335820547614.png)

	

- <font color='red'> +号的作用</font>

	- MySQL中的+号，仅仅有一个功能：----->运算符

	- SELECT 100 + 90;【190】	 两个操作数都是数值型，则做加法运算。

	- SELECT "100" + 90;【190】	若一方为字符型，一方为数值型，则试图将字符型装换成数值型再进行运算。

	- SELECT "Pledge" + 90;【90】	转换失败：字符型无法转换成数值型，那么将字符型置为0，再继续运算

	- SELECT null + 90;【190】	  只要其中一个是null，则结果必定为Null；

		查询城市名和城市代码，并拼接在一起

		```sql
		SELECT CONCAT(countrycode,"9999",`name`) FROM city;-- 连接函数，具体参数个数不限
		```

		![image-20211007125123953](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211007125123953-163358228514912.png)





### 2、条件查询

**语法：**
	**<font color='red'>SELECT</font>**
				**<font color='red'>查询列表</font>**
	**<font color='red'>FROM</font>**
				**<font color='red'>表名</font>**
	**<font color='red'>WHERE</font>**
				**<font color='red'>筛选条件;</font>**
**分类：**

- <font color='red'> 按条件表达式筛选</font>

	- 条件运算符：>、<、 =、 !=、<>、>=、<=

		```sql
		-- 案例1：查询人口数大于100000的城市
		SELECT
					*
		FROM
					city
		WHERE
					population>100000;
		-- 案例2：查询城市代码不是AFG的城市名和人口数和城市编号
		SELECT
					`Name`,Population,CountryCode
		FROM
					city
		WHERE
					CountryCode<>"AFG";-- 不等于<>
		```

		

- <font color='red'> 按逻辑表达式筛选

	- 逻辑运算符：&&、||、！
		<font color='red'> 推荐用</font>：and or not

		```sql
		-- 案例1：城市人口数在1600000到2000000之间的城市的名字和人口数
		
		SELECT
					`Name`,Population
		FROM
					city
		WHERE
					-- 方式一使用AND
		 			Population<200000 AND Population>160000;			
		
					-- 方式二使用between and
					Population BETWEEN 160000 AND 200000;
		-- 案例2：城市ID不在2~999之间的城市的名字和人口数
		SELECT
					`Name`,Population
		FROM
					city
		WHERE
					ID<2 OR ID>999;
		```

		

- <font color='red'> 模糊查询</font>

	- <font color='red'> like</font>

		- 一般和通配符搭配使用
			通配符：
					<font color='red'>%</font> 	任意多个字符，也包含0个字符
					<font color='red'>_</font> 	  任一单个字符

	- <font color='red'> between and</font>
				①可以提高语句的整洁度
				②包含临界值，闭区间
				③and前后临界值不能颠倒
				

	- <font color='red'> in </font>:用于判断某字段的值是否属于in列表中的某一项
				①使用in提高语句整洁度
				②in列表的值类型必须一致或者兼容（123和"123"）

		```sql
		-- 案例4：查询城市代码为AFG、NLD的城市
		SELECT
				`Name`,CountryCode
		FROM
				city
		WHERE
		-- 		方式一：
				CountryCode = "AFG" OR CountryCode = "NLD";
		-- 		方式二：
				CountryCode IN("AFG","NLD");
		```

		​	

	- <font color='red'> is null</font>
				= 或者 <>不能用于判断null的值，
				有的数据为null，此时就用is  null来判断【其他数据不能用is判断】

		```sql
		-- 案例4：查询城市代码不等于null的城市
		SELECT
				`Name`,CountryCode
		FROM
				city
		WHERE
		-- 		方式一：
				CountryCode IS NOT NULL;-- 城市代码不等于null的值 
		```

		

	- <font color='red'> 补充</font>：

		- 1、IS NULL ：仅仅可以判断NULL值，可读性高建议使用；
		- 2、<font color='red'> 安全等于<=></font>：既可以判断NULL值，也可以判断普通的数值，可读性低；	

		```sql
		-- 案例1：查询城市名字中包含字符m的员工信息
		SELECT
					`Name`,ID
		FROM
					city
		WHERE
					`Name` LIKE '%m%';-- 百分号表示通配符，不区分大小写
		
		-- 案例2：查询城市名字中第三个字符为m，第五个字符为e的的员工信息
		
		SELECT
				`Name`,ID
		FROM
				city
		WHERE
				`Name` LIKE '__m_e%';
				
		-- 案例3：查询城市名字中第三个字符为_ 的员工信息
		SELECT
				`Name`,ID
		FROM
				city
		WHERE
				-- `Name` LIKE '__\_%';				-- 可以用\来做转义，也可以自定义转义符
				`Name` LIKE '__!_%' ESCAPE '!';		-- 使用ESCAPE自定义转义符
				
		```

### 3、排序查询

**语法：**

​	**<font color='red'>SELECT 	查询列表</font>**
​	**<font color='red'>FROM	 表名</font>**
​	**<font color='red'>WHERE 	筛选条件</font>**
​	**<font color='red'>ORDER BY 	排序列表 	ASC或者DESC</font>**

**总结：**

- ASC   升序【可以省略，默认升序】
- DESC  降序
- order by子句中可以支持单个字段、多个字段、表达式、函数、别名
- order by子句一般是放在查询语句的最后边，limit子句除外；

```sql
-- 查询城市人口数，要求人口数从高到低
SELECT * FROM city ORDER BY Population DESC;
SELECT * FROM city ORDER BY Population ASC;

-- 查询中国的城市----代码CHN，按人口数排序
SELECT *
FROM city
WHERE CountryCode = 'CHN'
ORDER BY Population DESC;
```

- 按表达式排序

```sql
-- 查询所有中国的城市,将人口数除以10000，命名为人口数
-- 【IFNULL(字段,default)----如果数据时null，则调用defaul值】
SELECT *, IFNULL(Population,0)/10000 AS 人口数
FROM city
WHERE CountryCode = 'CHN'
ORDER BY IFNULL(Population,0)/10000 DESC;
```

- 按别名排序

```sql
SELECT *, IFNULL(Population,0)/10000 AS 人口数
FROM city
WHERE CountryCode = 'CHN'
ORDER BY 人口数 DESC;
```

- 按函数排序

```sql
-- 按城市名长度和人口数排序
SELECT LENGTH(`Name`) 城市名长度,`Name`,Population
FROM city
WHERE CountryCode = 'CHN'
ORDER BY LENGTH(`Name`);
```

-  按多个字段排序

```sql
-- 查询先按城市名长度降序，再按人口数升序

SELECT LENGTH(`Name`) 城市名长度,`Name`,Population
FROM city
WHERE CountryCode = 'CHN'
ORDER BY LENGTH(`Name`) DESC,Population ASC;
```



### 4、常见函数

**概念：**类似于Java的方法，将一组逻辑语句封装在方法体中，对外暴露方法名

**好处：**1、隐藏了实现细节
			2、提高了代码的重用性

**调用：**SELECT 函数名（实参列表） FROM 表名；
**关注点：**
		①叫什么（函数名）
		②干什么（函数功能）
**分类：**

#### 字符函数

- **length  获取参数值的字节个数**

	```sql
	SELECT LENGTH('tianhao');
	SELECT LENGTH('张三丰')
	```

- **concat  拼接字符串**

	```sql
	SELECT CONCAT(Name,'__',CountryCode) 哈哈 FROM city;
	```

- **upper、lower  转换大小写**

	```sql
	SELECT CONCAT(UPPER(Name),'__',LOWER(CountryCode)) 哈哈 FROM city;
	```

- **substr、substring  截取字符**
	**注意：索引从1开始**

	```sql
	-- 开始索引到结束
	SELECT SUBSTR('张三丰打张无忌',5) 明教教主;-- 张无忌
	-- 开始索引 第二参数是截取长度
	SELECT SUBSTR('张三丰打张无忌',5,2) 明教教主;-- 张无
	```

- **instr  返回子串第一次出现的索引，如果找不到返回0；**

	```sql
	SELECT INSTR('乔峰会降龙十八掌','降龙');-- 4
	SELECT INSTR('乔峰会降龙十八掌','降大龙');-- 0
	```

- **trim 去除字符串首尾空给或指定字符** 

	```sql
	SELECT TRIM('   段誉  ');-- 段誉
	SELECT TRIM('乔峰' FROM '乔峰A 乔峰  段誉  a乔峰');-- A 乔峰  段誉  a
	```

- **lpad 用指定的字符实现左填充的长度，若超过，则右截断**

	```sql
	SELECT LPAD('小李飞刀',7,'鬼');-- 鬼鬼鬼小李飞刀
	SELECT LPAD('小李飞刀',2,'鬼');-- 小李
	```

- **rpad 用指定的字符实现右填充的长度，若超过，则右截断**

	```sql
	SELECT RPAD('小李飞刀',7,'鬼');-- 小李飞刀鬼鬼鬼
	SELECT RPAD('小李飞刀',2,'鬼');-- 小李
	```

- **replace 替换**

	```sql
	SELECT REPLACE('张无忌喜欢周芷若还是周芷若？？','周芷若','赵敏');-- 张无忌喜欢赵敏还是赵敏？？
	```

	

#### 数学函数

- **round  四舍五入**

	```sql
	SELECT ROUND(-1.5);
	SELECT ROUND(-1.5678,2);-- 保留两位小数
	```

- **ceil  向上取整  返回>=该参数的最小整数**

	```sql
	SELECT CEIL(-1.02); -- -1
	```

- **floor  向下取整  返回<=该参数的最大整数**

	```sql
	SELECT FLOOR(-1.02); -- -2
	```

- **truncate  截断**

	```sql
	SELECT TRUNCATE(1.9999,2);-- 1.99保留两位，直接截断
	```

- **mod 取余【源码操作：mod(a,b)就是a-a/b*b】**

	```sql
	SELECT MOD(-10,3);-- -1
	SELECT 10%3;-- 1
	```

#### 日期函数

- **Now()  返回当前系统日期+时间**

	```sql
	SELECT NOW();-- 2021-10-09 21:42:08
	```

- **curdate 返回当前系统的日期，不包含时间**

	```sql
	SELECT CURDATE();
	SELECT CURRENT_DATE;
	```

	

- **curtime 返回当前系统的时间，不包含日期**

	```sql
	SELECT CURRENT_TIME;
	SELECT CURTIME();
	```

	

- **获取指定的部分，年月日时分秒**

	```sql
	SELECT YEAR(NOW());
	SELECT YEAR('1998-9-9');
	SELECT MONTH(NOW());
	```

	

- **STR_TO_DATE(str,format);将字符串转换为指定格式的日期，format格式**

	```sql
	SELECT STR_TO_DATE('3-5-1995','%d-%c-%Y');-- 1995-05-03
	```

	

- **DATE_FORMAT(date,format);将日期转换成字符串**

	```sql
	SELECT DATE_FORMAT('2000/9/9','%Y年%m月%d日');-- 2000年09月09日
	```

- **DATEDIFF(NOW(),'2012-9-26');时间作差，计算天数**

	```sql
	SELECT DATEDIFF(NOW(),'2012-9-26');-- 计算现在到2012年9月26日过去了多少天
	```

- **monthname：以英文形式返回月**

	![image-20211011083429429](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211010111112796-16338354740351.png)

#### **其它函数**

```sql
SELECT VERSION();-- 当前版本号8.0.26
SELECT DATABASE();-- 当前数据库名称
SELECT USER();-- root@localhost当前用户
SELECT password('字符');-- 将字符加密输出
SELECT MD5('字符');-- 用MD5加密形式加密
```

#### 流程控制函数

- **IF(条件,true结果,false结果)函数**

	```sql
	SELECT IF(10>99,'对了，翠花','错了，黑土');-- 错了，黑土
	```

	

- **CASE函数的使用一：switch case的效果；**

	```sql
	case 要判断的字段或者表达式
	when 常量1 then 要显示的值1或者语句1
	when 常量2 then 要显示的值2或者语句2
	....
	else 要显示的值n或者语句n;
	end case;
	```

	

- **CASE函数的使用二：类似于多重if 的效果；**

	```sql
	case 
	when 条件1 then 要显示的值1或者语句1
	when 条件2 then 要显示的值2或者语句2
	...
	else 要显示的值n或者语句n;
	end;
	```

	

- **练习:**

	```sql
	-- 查询城市人口数，若是中国城市，人口数不变，AFG国家人口数/1000，其他国家人口数减100000,
		SELECT `Name`,CountryCode,Population,
		CASE CountryCode
		WHEN 'CHN' THEN	Population/10000
		WHEN 'NLD' THEN	Population-100000
		ELSE Population
		END  HAHA
		FROM city;
	
	-- 查询城市LifeExpectancy分数，大于90为A，大于80为B，大于70为C，其余为D
	SELECT `Name`,LifeExpectancy,
	CASE 
		WHEN LifeExpectancy>90 THEN	'A'
		WHEN LifeExpectancy>80 THEN	'B'
		WHEN LifeExpectancy>70 THEN	'C'
		ELSE 'D'
	END 等级排名
	FROM country;
	```

	

#### 分组函数

- 功能：做统计使用，又称为统计函数、聚合函数、组函数

**分类：**sum求和、avg 平均值、max 最大值、min 最小值、count 计算个数



### 5、分组函数

- **1、简单使用**

```sql
SELECT SUM(Population) FROM city;
SELECT AVG(Population) FROM city;
SELECT MIN(Population) FROM city;
SELECT MAX(Population) FROM city;
SELECT COUNT(Population) FROM city;
-- 一行显式
SELECT SUM(Population) 和,AVG(Population) 平均值,MIN(Population) 最小值, MAX(Population) 最大值,COUNT(Population) 数据个数
FROM city;
```

![image-20211010111112796](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211011083429429-16339124710521.png)

- **2、参数支持哪些类型**

	- sum avg 一般用于处理数值型
	- max min count可以处理任何类型数据

- **3、sum、avg、max、min、count全部忽略null值，进行计算或比较或统计**

- **4、可以和distinct【去重】搭配使用**

	```sql
	SELECT SUM(Population) 原始数据,SUM(DISTINCT Population) 去重数据 FROM city;
	SELECT COUNT(CountryCode) 原始数据,COUNT(DISTINCT CountryCode) 去重数据 FROM city;
	```

	![image-20211010112853573](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211012115955351-16340111970856.png)

- **5、count 函数单独介绍**
	**效率：**

	- MYISAM存储引擎下，count(\*)效率高，底层有一个计数器，直接返回了

	- INNODB存储引擎下，count(\*)和count(1)效率差不多，但是比count(字段)效率高

	- **<font color='red'>综上所述：一般使用count(\*)统计行数</font>**

		```sql
		-- 统计ID列总行数【非null数据】
		SELECT COUNT(ID) FROM city;
		
		-- 统计所有列总行数【就是看列表有多少行，N列只要有一列不null，都能被计算，除非有一列全为null，不统计】
		SELECT COUNT(*) FROM city;
		
		-- 自建一列元素全为1,再统计，1也可以是任何字符【就是统计行数】
		SELECT COUNT(1) FROM city;
		```

		

- **6、和分组函数一同查询的字段要求是group by后的字段**

	

### 6、分组查询

**语法：**

```sql
SELECT 分组函数,列（要求出现在group by的后面）
FROM 表名
WHERE 筛选语句
GROUP BY 分组的列表
ORDER BY 排序子句
```

**注意：**查询列表必须特殊要求是分组函数和group by后面出现的字段
**特点：**

- 分组查询中的筛选条件分为两类

|              | 数据源         | 位置             | 关键字 |
| ------------ | -------------- | ---------------- | ------ |
| 分组前筛选： | 原始表         | GROUP BY子句前面 | WHERE  |
| 分组后筛选： | 分组后的结果集 | GROUP BY子句后面 | HAVING |

- **分组函数做条件，肯定是放在having子句中**
- 能用分组前筛选的，就优先考虑使用分组前筛选
- group by子句支持：
	- 单个字段分组
	- 多个字段分组（多个字段之间用逗号隔开，前后顺序没有要求）
	- 表达式或者函数分组（用的较少）
- 也可以添加排序（排序语句放在整个分组查询的最后）



**练习：**

```sql
-- 案例1：查询每个国家的最热门的城市
SELECT `Name`,MAX(Population) 最热门的城市人口数,CountryCode
FROM city
GROUP BY CountryCode;

-- 案例2：查询每个国家有多少个城市上榜
SELECT COUNT(*) 城市个数,CountryCode
FROM city
GROUP BY CountryCode;

-- 案例3：查询城市首字母是a的，每个国家的平均人口数
SELECT CountryCode,AVG(Population) 平均人口数
FROM city
WHERE `Name` LIKE 'A%'
GROUP BY CountryCode;-- 按谁分组，就写谁

-- 案例4：查询那个国家的城市个数大于10
-- 1、查询每个国家的城市个数
-- 2、查询城市数大于10的
SELECT CountryCode,COUNT(*) 城市个数
FROM city
GROUP BY CountryCode
HAVING COUNT(*)>10;-- having表示在已查询表格后，继续操作

-- 案例5：查询每个国家中城市人口数最大值大于1000000的城市名称和人口数

SELECT `Name`,max(Population) 最高人口数,CountryCode
FROM city
GROUP BY CountryCode
HAVING 最高人口数>1000000;


-- 多个字段进行分组
-- 查询每个国家，每种语言的平均得分
SELECT CountryCode,IsOfficial,SUM(Percentage)
FROM countrylanguage
GROUP BY IsOfficial,CountryCode;

-- 添加排序
SELECT CountryCode,IsOfficial,SUM(Percentage) AS 百分比之和
FROM countrylanguage
GROUP BY IsOfficial,CountryCode
HAVING 百分比之和 !=0
ORDER BY 百分比之和 DESC;
```



### 7、连接查询

**含义：**又称多表查询，当查询的字段来自于多个表时，就会用到连接查询

**笛卡尔乘积现象：**表1有m行，表2有n行，查询结果= m*n行

**发生原因**：没有有效的连接条件
**如何避免**：添加有效的连接条件

**分类：**		

- 按年代分类：
	- sq192标准：仅仅支持内连接
	- sq199标准【推荐】：支持所有的内连接+外连接（左外和右外）+交叉连接		
- 按功能分类：				
	- 内连接：
		- 等值连接
		- 非等值连接
		- 自连接
	- 外连接：
		- 左外连接
		- 右外连接
		- 全外连接
	- 交叉连接

#### SQL92标准

##### 1、等值连接

###### **语法：**

```sql
SELECT 查询列表
FROM 表1 别名1,表2 别名2
WHERE 别名1.key = 别名2.key   -- key是字段名，
AND 筛选条件
GROUP BY 分组字段
HAVING 分组后的筛选
ORDER BY 排序字段
```

- **特点：**
	- 多表连接的结果为多表的交集部分
	- n张表连接，至少需要n-1个连接条件
	- 多表连接时，表的顺序是没有要求的
	- 一般需要为表起别名
	- 可以搭配前面介绍过的所有子句使用，比如：排序、分组、筛选

```sql
-- 查询城市名对应的国家
SELECT city.`Name`,country.`Name`
FROM city,country
WHERE city.CountryCode = country.`Code`-- 通过两个表的城市代码相同，去匹配数据
```

###### 一、**为表起别名**

- 提高语句的简洁度
- 区分多个重名的字段

**注意：**如果为表起了别名，那么就不能再使用原表名了。

```sql
SELECT c.`Name`,cy.`Name`
FROM city c,country cy    -- 在from处起名
WHERE c.CountryCode = cy.`Code`
```

###### 二、**表的前后顺序无所谓**

###### 三、**可以加筛选**

```sql
SELECT c.`Name`,cy.`Name`
FROM city c,country cy    -- 在from处起名
WHERE c.CountryCode = cy.`Code`
AND  cy.`Name` LIKE '_r%';-- 第二个字符是r
```

###### 四、**可以加分组**

```sql
-- 查询城市名对应的国家，按国家分组
SELECT c.`Name`,cy.`Name`,COUNT(*) 个数
FROM city c,country cy    -- 在from处起名
WHERE c.CountryCode = cy.`Code`
AND  cy.`Name` LIKE '_r%'-- 第二个字符是r
GROUP BY cy.`Name`;
```

###### 五、**可以加排序**

```sql
SELECT c.`Name`,cy.`Name`,COUNT(*) 个数
FROM city c,country cy    -- 在from处起名
WHERE c.CountryCode = cy.`Code`
AND  cy.`Name` LIKE '_r%'-- 第二个字符是r
GROUP BY cy.`Name`
ORDER BY 个数 DESC;

```

###### 六、**可以多个表连接，无限连接**



##### 2、非等值连接

```sql
-- 案例1 ：查询薪资对应的薪资水平，判断where 不一定是等值，可以是比较
SELECT salary,grade_level
FROM employees e,job_grades g
WHERE salary BETWEEN g.`lowest_sal` AND g.`highest_sal`-- 薪资在low和high之间，分ABCDEF六档
AND g.`grade_level` = 'A';-- 筛选仅要A级的
```



##### 3、自连接

就是第一次查询，使用表A获取信息，第二次查询仍然使用表A，用前边获取的信息，再获取最终信息
通过起别名，防止歧义问题

```sql
-- 同一个表，每个员工都有工号，员工的manager_id信息存放领导的工号，
-- 先找员工的领导工号，第二次查询找该工号的领导名字，输出
SELECT 员工表.employee_id,员工表.`name`,领导表.employee_id,领导表.`name`,
FROM employees 员工表,employees 领导表,
WHERE 员工表.`manager_id` = 领导表.`employee_id`;
```

#### SQL99标准

**语法：**

```sql
SELECT 查询列表
FROM 表1 别名1 
【连接类型】 JOIN 表2 别名2
ON 连接条件---别名1.key = 别名2.key   -- key是字段名，
WHERE 筛选条件
GROUP BY 分组字段
HAVING 分组后的筛选
ORDER BY 排序字段

-- 连接类型：
内连接：INNER
外连接：
		左外连接：LEFT
		右外连接：RIGHT
		全外连接：FULL
交叉连接：CROSS
```



##### 一、内连接【多表交集】

```sql
-- 语法：
SELECT 查询列表
FROM 表1 别名1 【连接类型】
JOIN 表2 别名2
ON 连接条件---别名1.key = 别名2.key   -- key是字段名，
```



**内连接分类：**

- 等值连接
- 非等值连接
- 自连接

**特点：**

- 1、可以添加筛选、分组、排序
- 2、INNER等连接类型可以省略
- 3、筛选条件放在where后边，连接条件放在on后边，提高了分离性，便于阅读
- 4、内连接的等值连接个sql92中的等值连接效果完全相同



###### 1、等值连接

```sql
-- 查询城市名对应的国家
SELECT city.`Name`,country.`Name`
FROM city
INNER JOIN country
ON city.CountryCode = country.`Code`-- 通过两个表的城市代码相同，去匹配数据

-- 查询第二个字符是r的城市名
SELECT c.`Name`,cy.`Name`
FROM city c
INNER JOIN country cy    -- 在from处起名
ON c.CountryCode = cy.`Code`
WHERE  cy.`Name` LIKE '_r%';-- 第二个字符是r

-- 查询城市个数对应的国家，按国家分组,城市数大于300的国家，降序排列
SELECT count(*) 个数,cy.`Name`
FROM city c
INNER JOIN country cy    -- 在from处起名
ON c.CountryCode = cy.`Code`
GROUP BY cy.`Name`
HAVING 个数 > 300
ORDER BY 个数 DESC;

-- 多表连接
SELECT c.`Name`,cy.`Name`,COUNT(*) 个数
FROM city c
INNER JOIN country cy ON c.CountryCode = cy.`Code`
INNER JOIN countrylanguage cl ON cl.CountryCode = c.CountryCode
WHERE  cy.`Name` LIKE '_r%'-- 第二个字符是r
GROUP BY cy.`Name`
ORDER BY 个数 DESC;
```



###### 2、非等值连接

```sql
-- 案例1 ：查询薪资对应的薪资水平，判断where 不一定是等值，可以是比较
SELECT salary,grade_level
FROM employees e
JOIN job_grades g
ON salary BETWEEN g.`lowest_sal` AND g.`highest_sal`-- 薪资在low和high之间，分ABCDEF六档
WHERE g.`grade_level` = 'A';-- 筛选仅要A级的
```



###### 3、自连接

```sql
-- 同一个表，每个员工都有工号，员工的manager_id信息存放领导的工号，
-- 先找员工的领导工号，第二次查询找该工号的领导名字，输出
SELECT 员工表.employee_id,员工表.`name`,领导表.employee_id,领导表.`name`,
FROM employees 员工表
JOIN employees 领导表
ON 员工表.`manager_id` = 领导表.`employee_id`;
```



##### 二、外连接【主表匹配从表，从表没有返回null】

**应用场景：**用于查询一个表中有，而另一个表中没有的记录

**特点：**

- 外链接的查询结果为：主表中的所有记录
	- 如果从表中有和他匹配的--->显示对应的匹配值
	- 如果从表中没有和他匹配的--->显式null
	- 外连接查询结果   =   内连接查询结果   +   主表中有而从表中没有的记录

- <font color='red'>**左外连接【left join】**</font>：left join左边的是主表，结果为主表所有内容，从表没有显式null

- <font color='red'>**右外连接【right join】**</font>：right join右边的是主表，同上

- <font color='red'>**全外连接【full join】**</font>：左右都是主表，结果为两个表的所有记录，没有的互相显式null【并集】

- <font color='red'>**交叉连接【cross join】**</font>：就是乘积，主表每个元素都对应从表所有元素，主表5行，从表3行，对应返回就是15行

- 左外连接和右外连接交换两个表的顺序，可以实现同样的效果

	![image-20211011083449119](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211012120107598-16340112692507.png)

![image-20211011083526080](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211010112853573-16338365347792.png)



```sql
-- 查询那个国家没有创建年限
-- 左外连接
SELECT city.CountryCode,country.IndepYear
FROM city
LEFT JOIN country
ON city.CountryCode = country.`Code`
WHERE country.IndepYear IS NULL;

-- 右外连接

SELECT city.CountryCode,country.IndepYear
FROM country
RIGHT JOIN city
ON city.CountryCode = country.`Code`
WHERE country.IndepYear IS NULL;

-- 全外连接

SELECT city.CountryCode,country.IndepYear
FROM country
FULL JOIN city
ON city.CountryCode = country.`Code`
WHERE country.IndepYear IS NULL;

-- 交叉连接   就是乘积。主表每个元素都对应从表所有元素

SELECT city.CountryCode,country.IndepYear
FROM country
CROSS JOIN city
ON city.CountryCode = country.`Code`
WHERE country.IndepYear IS NULL;


```



### 8、子查询

概念：

> 出现在其他语句中的select语句，称为子查询或者内查询
>
> 外部的查询语句，称为主查询或外查询

分类：

- 按子句出现的位置：
	- select后面：仅仅支持标量查询
	- from后面：支持表子查询
	- **where或者having后面：**
		- 支持标量子查询（单行）
		- 列子查询（多行）
		- 行子查询
	- exists后面：表子查询

- 按结果集的行列数不同：
	- 标量子查询：结果只有一行一列
	- 列子查询：结果只有一列多行
	- 行子查询：结果有一行多列，或者多行多列
	- 表子查询：结果一般为多行多列

#### 一、select后面：仅仅支持标量查询

就是select处的字段也可以用小括号括起来，进行查询套娃

```sql
-- SELECT后面
-- 查询每个国家的城市数量

SELECT city.*,(
		SELECT COUNT(*)
		FROM country
		WHERE country.`Code` = city.CountryCode
) 个数
FROM city;

```



#### 二、from后面：支持表子查询

from后面是放的表，子查询放到from后面，就是将查询出来的表作为目标表，不用每次都使用原表。

必须要起别名。

**语法：**

```sql
SELECT 查询字段
FROM (  SELECT COUNT(*)-- 子查询返回的表
		FROM country
		WHERE country.`Code` = city.CountryCode
) 个数
WHERE 筛选条件
```





#### 三、where或having后面

##### 1、支持标量子查询（单行）

```sql
-- 查询谁的人口数比上海高
SELECT `Name`,Population
FROM city
WHERE Population>(

	SELECT Population
	FROM city
	WHERE `Name` = 'Shanghai'
	
);

-- 查询与上海的国家编号相同，但是人口数比商丘多的城市
SELECT `Name`,Population,CountryCode
FROM city
WHERE CountryCode = (-- 上海国家编号
		SELECT CountryCode
		FROM city
		WHERE `Name` = 'Shanghai'
	) AND Population > (-- 商丘流行度
		SELECT Population
		FROM city
		WHERE `Name` = 'Shangqiu'
	);

-- 查询中国每个省份人口数最高的城市、流行度、省份、国家代码
SELECT CountryCode,District,`Name`,max(Population)
FROM city
WHERE CountryCode = 'CHN' 
GROUP BY district;

-- 查询人口数最高的城市所在国家的，所有城市的人口数、国家代码

SELECT CountryCode,`Name`,Population
FROM city
WHERE CountryCode = (-- 找到目标国家代码
		SELECT CountryCode
		FROM city
		WHERE Population = (-- 找到最高人口数
				SELECT max(Population)
				FROM city
		)
)


-- 查询每个国家的最高人口城市，并保留大于上海人口数的城市
SELECT CountryCode,`Name`,max(Population) 
FROM city
GROUP BY CountryCode
HAVING max(Population) > (
		SELECT Population
		FROM city
		WHERE `Name` = 'Shanghai'
);
```



##### 2、列子查询（多行）

![image-20211011095407130](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211011083449119-16339124907602.png)

```sql
-- 查询ID在50或55的国家代码，的国家人口最多的城市

SELECT CountryCode,`Name`,max(Population) 
FROM city
WHERE CountryCode IN(
		SELECT DISTINCT CountryCode
		FROM city
		WHERE ID IN(50,60)-- 切记IN表示或者，，，，50 或者60
)
```



##### 3、行子查询

结果集是：一行多列或多行多列

```SQL
-- 查询人口数最多且平均寿命最小的国家信息
SELECT *
FROM country
WHERE (Population,LifeExpectancy) = (
		SELECT MAX(Population),MIN(LifeExpectancy)
		FROM country
)
```



##### **注意：**

- 子查询放在小括号内

- 子查询一般放在条件的右侧

- 标量子查询一般搭配着单行操作符使用【> 、< 、>= 、<= 、= 、<>】

- 列子查询一般搭配着多行操作符使用【in、any/some、all】
- 子查询先执行，因为主查询要用到子查询的结果

#### 四、exists后面：表子查询（也叫相关子查询）

布尔类型

**语法：**

**exists（完整的查询语句）**

返回结果：1或0，有值为1，无值为0；

```sql
-- 查询有独立年份的国家【从city中找国家代号，去country中判断是否有独立年份】
SELECT CountryCode
FROM city
WHERE EXISTS(
		SELECT code
		FROM country
		WHERE city.CountryCode = counttry.Code AND IndepYear IS NULL 
    	-- 内部可以用到外边的表，city，所以叫相关子查询
)
就是一个判定条件
```

**使用 exists 和 in 对比**

```sql
-- 查询没有对应女朋友的男生名字
-- 使用IN()
SELECT boys.*
FROM boys
WHERE boys.id NOT IN(-- 不在下边的表中的id数据
		SELECT boyfriend_id--此处在女生表中查出所有女生对应的男生id，有女朋友才有对应id
		FROM beauty
)
-- 使用EXISTS()
SELECT boys.*
FROM boys
WHERE NOT EXISTS(-- 不在下边的表中的id数据
		SELECT boyfriend_id
		FROM beauty
		WHERE boys.id = beauty.boyfriend_id -- 查出所有 有女朋友对应id的男生id
)

```



### 9、分页查询

**应用场景：**当要显示的数据，一页显示不全，需要分页提交sql请求

**语法：**

```sql
SELECT 查询列表
FROM 表1 别名1 
【连接类型】 JOIN 表2 别名2
ON 连接条件---别名1.key = 别名2.key   -- key是字段名，
WHERE 筛选条件
GROUP BY 分组字段
HAVING 分组后的筛选
ORDER BY 排序字段
LIMIT OFFSET,size;

OFFSET ：要显示条目的起始索引（起始索引从0开始）【可选，不写默认0】
size：要显示的条目个数!!!!这是个数，不是索引结束，切记切记
```

size：要显示的条目个数！！！！**<font color = 'red'>这是个数</font>**，不是索引结束，<font color = 'red'>**切记切记**</font>

**特点：**

- limit语句放在查询语句的最后面
- 公式：
	- page：要显示的页数
	- size：每页要显示的条目数
- <font color = 'red'>**limit  （page-1）*size，size**；</font>【直接套用】

```sql
	页数		size          语句
	1		  10		limit 0,10
	2		  10		limit 10,10
	3         10		limit 20,10
```



### 10、union联合查询

**语法：**

```sql
查询语句1
union
查询语句2
union
查询语句3
...

```

**应用场景：**

要查询的结果来自于多个表，且多个表没有直接的连接关系，但查询的信息字段相同。

**注意：**

- 要被联合的多个查询语句，的列数必须一致

- 要求多条查询语句的，查询字段，顺序保持一致，本来就是没关系的表，联合在一起，顺序不一样数据类型都不同
- union关键字默认去重，不想去重可以使用union all



## 四、DML语言基础

### 1、插入：insert

**语法一：**

```sql
INSERT INTO 表名(列1，列2....)
VALUES(值1，值2....)
```

**语法二：**

```sql
INSERT INTO 表名
set 列名=值，列名=值....
```



**语法对比：**

- 语法一支持多行

	> ```sql
	> INSERT INTO city99.ci(cittt,ciii,diii)
	> VALUES(1,2,3),(4,6,5),(9,8,7);
	> ```

- 语法一支持子查询

	> ```sql
	> -- 直接用select查询的结果代替values
	> INSERT INTO city99.ci(cittt,ciii,diii)
	> SELECT SurfaceArea,IndepYear,LifeExpectancy
	> FROM country
	> WHERE code = 'CHN'
	> 
	> ```



**注意：**

- 插入的值的类型，必须要与原列的数据类型相同

- 表中不可以为空的位置，必须插入元素

- 表中允许为空的单元格，有两种不插入数据方式
	- 在字段处，不写该列，系统默认为null
	- 在字段处写上该列，values处数据填写null
- 字段顺序可以颠倒，但是values处值必须于上边字段对应
- 列数和值的个数必须一致
- 可以省略列名，默认所有列，而且列的顺序默认是原表的顺序，数据要与之对应

```sql
-- 语法一
INSERT INTO city99.ci(cittt,ciii,diii)
VALUES(1,2,3);
-- 语法二
INSERT INTO city99.ci
SET cittt=9,ciii=8,diii=7;
```



### 2、修改：update

**语法：**

一、修改单表的记录

```sql
-- 语法
UPDATE 表名
SET 列1=新值1，列2=新值2....
WHERE 筛选条件		-- 不写where筛选条件的话，所有行都改了
```

```sql
-- 实践
UPDATE city99.ci
SET cittt=888
WHERE diii>20;
```

二、修改多表的记录

```sql
-- SQL92语法
UPDATE 表1 别名1，表2 别名2
SET 列1=值1，列2=值2.....
WHERE 连接条件
AND 筛选条件

-- SQL99语法
UPDATE 表1 别名1
INNER/LEFT/RIGHT JOIN 表2 别名2
ON 连接条件
SET 列1=值1，列2=值2.....
WHERE 筛选条件
```



### 3、删除：delete

**语法：**

一、单表的删除

```sql
DELETE FROM 表名 WHERE 筛选条件   -- 不加筛选条件，就是删除整个表
```

二 、多表的删除

```sql
TRUNCATE TABLE 表名  -- 清空表
```

```sql
-- SQL92语法
DELETE 别名1  		-- 此处要删除那个表的 信息，就写那个表名或别名，也可写多个
FROM 表1 别名1，表2 别名2
SET 列1=值1，列2=值2.....
WHERE 连接条件
AND 筛选条件

-- SQL99语法
DELETE 表1 别名1 			-- 此处要删除那个表的 信息，就写那个表名或别名，也可写多个
FROM 表1 别名1
INNER/LEFT/RIGHT JOIN 表2 别名2
ON 连接条件
WHERE 筛选条件
```

- **delete和truncate的区别和联系**
	- delete可以加where筛选条件，truncate不能加
	- truncate效率高，因为不用筛选
	- 假如要删除的表中有自增长列
		- 如果用delete删除后，再插入数据，自增长列的值从断点开始
		- 而truncate删除后，再插入数据，自增长列的值从1开始
	- delete删除有返回值，truncate删除没有返回值，【就是几行删除了，truncate全清，他也不知道删了几行】
	- truncate删除不能回滚，delete删除可以回滚

**【自增长列】：**就是你不用管他，类似序号，你添加其他数据后他会自动给你加一，假设原表有7个元素

- 当delete删除全表，此时数据为空，再插入数据，自增长列竟然从8开始

- 若使用truncate清空全表，此时数据为空，再插入数据，自增长列从1开始



## 五、DDL语言基础

数据定义语言

### 一、库的管理

#### 1、库的创建：create

**语法：**

```sql
CREATE DATABASE 库名    	-- 若存在，就报错

CREATE DATABASE IF NOT EXISTS 库名   -- 判断不存在，以后再创建
```

#### 2、库的修改：alter

```sql
ALTER DATABASE 库名 CHARACTER SET GBK; -- 修改库的字符集
```

#### 3、库的删除：drop

```sql
DROP DATABASE 库名    	-- 若不存在，就报错

DROP DATABASE IF EXISTS 库名   -- 判断存在，以后再删除
```



### 二、表的管理

#### 1、表的创建：create

**语法：**

```sql
CREATE TABLE 表名(
		列名 列的类型 【（长度）约束】-- 有需要约束长度的，就加个括号内部长度，不需要就不用写
		列名 列的类型 【（长度）约束】
		列名 列的类型 【（长度）约束】
		列名 列的类型 【（长度）约束】
		.....
)
-- 创建图书表
CREATE TABLE book(
		id INT,-- 编号
		bName VARCHAR(20), -- 图书名
		price DOUBLE, -- 价格
		authorId INT,  -- 作者编号
		publishDate DATETIME -- 出版日期  【最后一个不要加逗号】
);
DESC book;-- 显式表的结构

-- 创建作者表
CREATE TABLE author(
		id INT,-- 编号
		au_Name VARCHAR(20), -- 作者名
		nation VARCHAR(10) -- 国籍
);

DESC author;-- 显式表的结构

```

#### 2、表的修改：alter

##### 一、修改列名

```sql
ALTER TABLE book CHANGE COLUMN publishdate pubDate DATETIME;
```



##### 二、修改列的类型或者约束

```sql
ALTER TABLE book MODIFY COLUMN pubdate TIMESTAMP;
```



##### 三、添加新列

```sql
ALTER TABLE author ADD COLUMN annual DOUBLE;
```



##### 四、删除列

```sql
ALTER TABLE author DROP COLUMN annual;
```



##### 五、修改表名

```sql
ALTER TABLE author RENAME TO book_author;
```



#### 3、表的删除：drop

```sql
DROP TABLE IF EXISTS book; -- 判断存在再删除
SHOW TABLES;-- 显示当前库下所有表
```



#### 4、表的复制：

##### 一、仅复制表的结构

```sql
CREATE TABLE copy_author LIKE book_author;
```

##### 二、复制表的结构和数据内容

```sql
-- 其实就是下边用了个子查询，想复制一部分内容的话，加个where筛选就行了
CREATE TABLE copy2_author
SELECT * FROM book_author;
```

##### 三、仅仅复制某些字段

```sql
-- 仅复制了其中两列，而且内容不复制，仅复制了两列的结构
CREATE TABLE copy3_author
SELECT id,au_name 
FROM book_author
WHERE 0;		-- 就是随便写了一个不成立的筛选条件，除了列名内容都不成立，就没复制，写1=2也行，

```



### 三、常见的数据类型

#### 数值型：

- **<font color='red'>整型</font>**

	> - **分类：**
	>
	> tinyint：1字节
	>
	> smallint：2字节
	>
	> mediumint：3字节
	>
	> int/integer：4字节
	>
	> bigint：8字节

	- **特点：**

		- 如果不设置无符号还是有符号，默认是有符号，如果想设置无符号，需要用unsigned关键字

		- 如果插入的数值超出了整型的范围，会报错out of range异常，

		- 如果不设置长度，会有默认的长度

		- 长度代表了显示的最大宽度，如果数据长度不够，会用0在左边填充，但必须使用zerofull关键字

		- ```sql
			CREATE TABLE tab_int(
					t1 INT(6) ZEROFILL,
			-- t1用了关键字zerofull，不够长度就用0填充，t2没用，虽然不够长度6，但也不会填充
					t2 INT(6) UNSIGNED
			-- t2用了关键字unsigned，表示为无符号类型，如果填充负数会报异常
			);
			
			
			SELECT * FROM tab_int;
			INSERT INTO tab_int VALUES(33,123124244);
			INSERT INTO tab_int VALUES(123424,333);
			```

			![image-20211012115955351](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211011095407130-16339172491295.png)

			![image-20211012120107598](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211011083526080-16339125288664.png)



- **<font color='red'>小数</font>**
	- 定点型：
		- dec(M,D)
		- decimal(M,D)
	- 浮点型
		- float(M,D)
		- double(M,D)
	- **特点：**
	- <font color='blue'>M和D的意思</font>：
		- <font color='red'>**M**</font>：整数部位 + 小数部位   的总个数
		- <font color='red'>**D**</font>：小数部位     的个数
		- 如果超过范围，插入临界值
		- （6,3）---->就是只允许111.222这样，
			- 小数位不够【填0补齐】，小数位超了【四舍五入】
			- 整数位不够【允许】，整数位超了【报错】
	- <font color='blue'>M和D都可以省略</font>：
		- 如果是<font color='red'>decimal类型</font>，省略后<font color='red'>默认是(M,D)===（10,0）</font>【不允许有小数】
		- 如果是float/double，省略后随便添加，不限定MD的值
	- <font color='blue'>定点型的精度较高，如果要求插入数据的精度较高或者货币运算等，可以使用定点型</font>
	- **选择原则：**所选择的类型越简单越好，能保存的数值的类型越小越好。

#### 字符型

- **<font color='red'>较短的文本：char、varcahr</font>**

	- |         | 写法       | M的意思                         | 特点           | 空间耗费情况 | 效率 |
		| ------- | ---------- | ------------------------------- | -------------- | ------------ | ---- |
		| char    | char(M)    | 最大的字符数，可以省略，默认为1 | 固定长度的字符 | 比较耗费     | 高   |
		| varchar | varchar(M) | 最大字符，不可以省略            | 可变长度的字符 | 比较节省     | 低   |

		**char每次开辟固定M大小的空间，对于性别，手机号这种固定的可以使用char，变化的建议用varchar**

	- <font color='red'>binary和varbinary用于保存较短的二进制</font>

	- <font color='red'>enum用于保存枚举</font>

	- <font color='red'>set用于保存集合</font>

- **<font color='red'>较长的文本：text、blob（较长的二进制数据）</font>**

#### 日期型

**分类：**

- <font color='blue'>date</font>：只保存日期

- <font color='blue'>time</font>：只保存时间

- <font color='blue'>year</font>：只保存年

- <font color='blue'>datetime</font>：保存日期 + 时间

- <font color='blue'>timestamp</font>：保存日期 + 时间

**特点：**

|           | 字节 | 范围      | 时区影响 |
| --------- | ---- | --------- | -------- |
| datetime  | 8    | 1000~9999 | 不受     |
| timestamp | 4    | 1970~2038 | 受       |



### 四、常见的约束

**概念：**一种限制，用于限制表中的数据，为了保证表中的数据的准确和可靠性

**位置：**

> ```sql
> CREATE TABLE 表名(
> 		字段名 字段类型 列级约束,
> 		字段名 字段类型 列级约束,
> 		表级约束
> )
> ```

- **<font color='red'>NOT NULL---></font> <font color='blue'>非空</font>**：用于保证该字段的值不能为空
	- 比如：姓名、学号；
- **<font color='red'>DEFAULT---></font> <font color='blue'>默认</font>**：用于保证该字段有默认值
	- 比如：同一班级下，学生的班级代码；
- **<font color='red'>PRIMARY KEY---></font> <font color='blue'>主键</font>**：用于保证该字段的值具有唯一性，并且非空
	- 比如学号；
- **<font color='red'>UNIQUE---></font> <font color='blue'>唯一</font>**：用于保证该字段的值具有唯一性，可以为空
	- 比如座位号；
- **<font color='red'>CHECK---></font> <font color='blue'>检查约束</font>**：用于检查是否为某值；
- **<font color='red'>FOREIGN KEY---></font> <font color='blue'>外键</font>**：用于限制两个表的关系，保证该字段的值必须来自主表的关联列的值 

#### 1、**添加约束的时机：**

- 1、创建表时
- 2、修改表时

#### 2、**约束的添加分类：**

- <font color='red'>列级约束</font>：六大约束语法上都支持，但是外键约束没有效果

	> ```sql
	> 语法：
	> CREATE TABLE 表名(
	> 		字段名 字段类型 列级约束,
	> 		字段名 字段类型 列级约束,
	> )
	> ```
	>
	> ```sql
	> 
	> CREATE TABLE students(
	> 		id INT PRIMARY KEY,-- 主键
	> 		stuName VARCHAR(10) NOT NULL,-- 非空
	> 		gender CHAR(1) CHECK(gender='男' OR gender='女'),-- 检查
	> 		seatId INT UNIQUE,-- 唯一
	> 		age INT DEFAULT 18,-- 默认
	> 
	> );
	> 
	> CREATE TABLE major(
	> 		id INT PRIMARY KEY,
	> 		majorName VARCHAR(20)
	> );
	> ```
	>
	> 

- <font color='red'>表级约束</font>：除了非空、默认约束，其他约束都支持

	> ```sql
	> 语法：
	> 一、完整版
	> CREATE TABLE 表名(
	> 		字段名 字段类型,
	> 		字段名 字段类型,
	> 		constraint 约束名 约束类型(字段名)
	> )
	> 二、简略版
	> CREATE TABLE 表名(
	> 		字段名 字段类型,
	> 		字段名 字段类型,
	> 		约束类型(字段名)
	> )
	> 
	> ```
	>
	> ```sql
	> 一、完整版
	> CREATE TABLE students(
	> 		id INT,
	> 		stuName VARCHAR(10),
	> 		gender CHAR(1),
	> 		seatId INT,
	> 		age INT,
	> 		majorId INT,
	> 		CONSTRAINT pk PRIMARY KEY(id),-- 主键
	> 		CONSTRAINT uq UNIQUE(seatId),-- 唯一键
	> 		CONSTRAINT ch CHECK(gender='男' OR gender='女'),-- 检查
	> 		CONSTRAINT fk_students_major FOREIGN KEY(majorId) REFERENCES major(id)-- 外键
	> );
	> ---------------------------------------------------------------------------------
	> 二、省略版
	> CREATE TABLE students(
	> 		id INT,
	> 		stuName VARCHAR(10),
	> 		gender CHAR(1),
	> 		seatId INT,
	> 		age INT,
	> 		majorId INT,
	> 		PRIMARY KEY(id),-- 主键
	> 		UNIQUE(seatId),-- 唯一键
	> 		CHECK(gender='男' OR gender='女'),-- 检查
	> 		FOREIGN KEY(majorId) REFERENCES major(id)-- 外键
	> );
	> 
	> 
	> CREATE TABLE major(
	> 		id INT PRIMARY KEY,
	> 		majorName VARCHAR(20)
	> );
	> ```
	>
	
- **列级约束和表级约束的区别**

	|          | 位置           | 支持的约束类型               | 是否可以起约束名       |
	| -------- | -------------- | ---------------------------- | ---------------------- |
	| 列级约束 | 列的后面       | 语法都支持，但外键没有效果   | 不可以                 |
	| 表级约束 | 所有列的最下面 | 默认和非空不支持，其他均支持 | 可以（但主键没有效果） |

	

#### 3、**<font color='red'>通用的写法：</font>**

一般的写列级约束，外键写表级约束，这样命名更规范，也能见名知意，知道关联表是哪个。

```sql
CREATE TABLE students(
		id INT PRIMARY KEY,-- 主键
		stuName VARCHAR(10) NOT NULL,-- 非空
		gender CHAR(1) CHECK(gender='男' OR gender='女'),-- 检查
		seatId INT UNIQUE,-- 唯一
		age INT DEFAULT 18,-- 默认
		majorId INT,
		CONSTRAINT fk_students_major FOREIGN KEY(majorId) REFERENCES major(id)
);
```



#### 4、修改表时添加约束

- 添加列级约束

```sql
ALTER TABLE 表名 MODIFY COLUMN 字段名 字段类型 新约束;
```

- 添加表级约束

```sql
ALTER TABLE 表名 ADD 【constrain 约束名】 约束类型(字段名) 【外键的引用】;
-- 【】中的内容表示可以省略，或者根据外键需要添加
```



```sql
-- 添加非空约束
ALTER TABLE students MODIFY COLUMN stuName VARCHAR(20) NOT NULL;


-- 添加默认约束
ALTER TABLE students MODIFY COLUMN age INT DELETE 18;


-- 添加主键约束[主键约束支持表级约束和列级约束]
-- ①通过列级约束添加
ALTER TABLE students MODIFY COLUMN id INT PRIMARY KEY;
-- ②通过表级约束添加
ALTER TABLE students ADD PRIMARY KEY(id);


-- 添加唯一约束[唯一约束支持表级约束和列级约束]
-- ①通过列级约束添加
ALTER TABLE students MODIFY COLUMN seatId INT UNIQUE;
-- ②通过表级约束添加
ALTER TABLE students ADD UNIQUE(seatId);


-- 添加外键
ALTER TABLE students ADD FOREIGN KEY(majorId) REFERENCES major(id);
```



#### 5、修改表时删除约束

```sql
-- 删除非空约束
ALTER TABLE students MODIFY COLUMN stuName NULL;


-- 删除默认约束
ALTER TABLE students MODIFY COLUMN age INT;


-- 删除主键约束
ALTER TABLE students DROP PRIMARY KEY;


-- 删除唯一约束
ALTER TABLE students DROP INDEX seatId;


-- 删除外键
ALTER TABLE students DROP FOREIGN KEY fk_students_major;
```



### 五、标识列【自增长列】

**概念：**可以不用手动的插入值，系统提供默认的序列值

**注意：**

- 标识列必须和主键搭配吗？？？？不一定，但<font color='red'>必须是一个key</font>，可以直接主键、唯一键、外键、自定义键
- 一个表可以有<font color='red'>至多一个标识列</font>
- 标识列的类型只能是<font color='red'>数值型</font>
- 标识列可以通过【SET auto_increment_increment = 3;】-- 更改步长
- 标识列可以通过手动插入的形式更改起始值【INSERT INTO tab_identify(id,Name) VALUES(9,'456');】

#### 1、创建时设置标识列

设置方式：在列字段后面增加【<font color='red'>AUTO_INCREMENT</font>】

```sql
CREATE TABLE tab_identify(
		id INT PRIMARY KEY AUTO_INCREMENT,
		Name VARCHAR(20)
);
INSERT INTO tab_identify VALUES(9,'123');-- 自增长列也可以设置值，就可以实现改变起始值的想法
INSERT INTO tab_identify VALUES(NULL,'123');-- 省略版
INSERT INTO tab_identify(id,Name) VALUES(NULL,'456');-- 完整版
INSERT INTO tab_identify(Name) VALUES('789');-- 自增长列不写

SELECT * FROM tab_identify;

SHOW VARIABLES LIKE '%auto_increment%';--  查看步长和起始值（偏移量）
SET auto_increment_increment = 3;-- 更改步长为3
```

#### 2、修改表时设置标识列

```sql
ALTER TABLE tab_identify MODIFY COLUMN id INT PRIMARY KEY AUTO_INCREMENT;
```

#### 3、修改表时删除表示列

```sql
ALTER TABLE tab_identify MODIFY COLUMN id INT;
```





## 六、TCL语言基础（Transaction Control Language）

Transaction Control Language：事务控制语言

### **1、事务概念**

- <font color='red'>事务右单独单元的一个或者多个SQL语句组成在这个事务单元中，每条MySQL语句是相互依赖的。</font>而整个单独单元作为一个不可分割的整体，如果单元中某条SQL语句一旦执行失败或产生错误，整个单元将会回滚。所受到影响的数据将返回到事务开始以前的状态；如果单元中的所有SQL语句均执行成功，则事务被顺利执行。
- 例如：转账，若发生故障必须退回转账金额，回滚到未转账状态。

### 2、事务的特性（ACID属性） <font color='red'>**【高频考点】**</font>

-  <font color='red'>**原子性（Atomicity）**</font>
	- 原子性是指事务是一个不可分割的工作单位，事务中的操作要么都发生，要么都不发生。
- <font color='red'>**一致性（Consistency）**</font>
	- 事务必须使数据库从一个一致性状态变换到另外一个一致性状态。
- <font color='red'>**隔离性（Isolation）**</font>
	- 事务的隔离性是指一个事务的执行不能被其他事物干扰，即一个事务的内部操作及使用的数据对并发的其他事务是隔离的，并发执行的各个事务之间不能相互干扰。
- <font color='red'>**持久性（Durability）**</font>
	- 持久性是指一个事务一旦被提交他对数据库中数据的改变就是永久性的，接下来的其他操作和数据库故障不应该对其有任何的影响。

### 3、事务的创建

#### 一、隐式事务

事务没有明显的开启和结束的标记

比如insert、update、delete语句

#### 二、显式事务

事务具有明显的开启和结束标记

前提：必须先设置自动提交功能为禁用。

```sql
set autocommit = 0;-- 禁用事务的自动提交功能【仅针对当前对话】
```

#### 三、创建步骤

```sql
-- 步骤1：开启事务
set autocommit = 0;
start transaction;
-- 步骤2：编写事务中的SQL语句（select、insert、update、delete）
语句1；
语句2；
...
-- 步骤3：结束事务
commit;-- 提交事务
rollback;-- 回滚事务
```

```sql
-- 创建表
CREATE TABLE tulong(
		id INT PRIMARY KEY AUTO_INCREMENT,
		name VARCHAR(5),
		balance INT
)
-- 查看表
SELECT * FROM TULONG;
-- 插入数据
INSERT INTO tulong VALUES(null,'张无忌',1000);
INSERT INTO tulong VALUES(null,'赵敏',1000);


-- 开启事务
SET autocommit = 0;
START TRANSACTION;
-- 编写一组事务语句【张无忌给赵敏转账500元】
UPDATE tulong SET balance = 500 WHERE `name` = '张无忌';
UPDATE tulong SET balance = 1500 WHERE `name` = '赵敏';
-- 结束事务
COMMIT;


-- 【假设失败，提前设置回滚】
-- 开启事务
SET autocommit = 0;
START TRANSACTION;
-- 编写一组事务语句
UPDATE tulong SET balance = 1000 WHERE `name` = '张无忌';
UPDATE tulong SET balance = 1000 WHERE `name` = '赵敏';
-- 回滚事务
ROLLBACK;
-- 运行后结果仍是张无忌500，赵敏1500；

```

- **delete和truncate在事务使用时的区别**
	- delete支持回滚操作
	- truncate不支持回滚操作

```sql
-- delete和truncate在事务使用时的区别
-- 演示delete
SET autocommit = 0;
START TRANSACTION;
DELETE FROM tulong;
ROLLBACK;-- 回滚     原数据保留
-- 演示truncate
SET autocommit = 0;
START TRANSACTION;
TRUNCATE TABLE tulong;
ROLLBACK;-- 回滚      表空了
```

- **savepoint的使用**

	- 保存节点，搭配回滚使用

		```sql
		
		SET autocommit = 0;
		START TRANSACTION;
		DELETE FROM tulong where id = 1;
		DELETE FROM tulong where id = 2;
		savepoint hao;-- 设置保存节点，并起别名
		DELETE FROM tulong where id = 3;
		ROLLBACK TO hao;-- 回滚到hao节点处
		
		-- 最终tulong表中，id为1、2的已经被删除，id=3的元素因为回滚，未删除。
		```

		

### 4、数据库的隔离级别

- 对于同时运行的多个事务，当这些事务访问数据库中相同的数据时，如果没有采取必要的隔离机制，就会导致各种并发问题：
	- <font color='red'>脏读</font>：对于两个事务甲、乙，当甲读取了已经被乙更新但还<font color='blue'>没有提交</font>的字段，之后若乙发生了回滚，甲读取的内容就是临时的，且无效的。
	- <font color='red'>不可重复读</font>：对于两个事务甲、乙，甲读取了一个字段，然后乙<font color='blue'>更新</font>了该字段，之后甲再次读取同一个字段时，字段的值就不同了。
	- <font color='red'>幻读</font>：对于两个事务甲、乙，甲从表中读取了一个字段，然后乙在该表中<font color='blue'>插入</font>了一些新的行，如果甲再次读取同一个表，就会多出几行。

- **数据库事务的隔离性：**数据库系统必须具有隔离并发运行各个事务的能力，使他们不会互相影响，避免各种并发问题

- 一个事务与其他事务隔离的程度称为隔离级别，数据库规定了多种事务隔离级别，不同隔离级别对应不同的干扰程度，<font color='blue'>**隔离级别越高，数据的一致性就越好，但并发性越弱**</font>。

- 数据库提供了4种隔离级别：

- | 隔离强度 | 支持         | 隔离级别                             | 描述                                                         |
	| -------- | ------------ | ------------------------------------ | ------------------------------------------------------------ |
	| 最低     | MySQL        | READ UNCOMMITTED<br />(读未提交数据) | 允许事务读取未被其他事物提交的表更、脏读、不可重复读和幻读的问题都会出现 |
	|          | Oracle/MySQL | READ COMMITED<BR />(读已提交数据)    | 只允许事务读取已经被其他事物提交的变更、可以避免脏读、但但但不可重复读和幻读问题仍可能会出现 |
	|          | MySQL        | REPEATABLE READ<br/>(可重复读)       | 确保事务可以多次从一个字段中读取相同的值，但这个事务持续期间，禁止其他事物对这个字段进行更新，可以避免脏读和不可重复读，但但但幻读问题仍然存在 |
	| 最高     | Oracle/MySQL | SERIALIZABLE(串行化)                 | 确保事务可以从一个表中读取相同的行，在这个事务持续期间，禁止其他事务对该表执行插入、更新和删除操作，所有并发问题都可以避免，但性能十分低下 |

	|                  | 脏读     | 不可重复读 | 幻读     |
	| ---------------- | -------- | ---------- | -------- |
	| read uncommitted | 会出现   | 会出现     | 会出现   |
	| read committed   | 不会出现 | 会出现     | 会出现   |
	| repeatable read  | 不会出现 | 不会出现   | 会出现   |
	| serializable     | 不会出现 | 不会出现   | 不会出现 |
	
- <font color='red'>MySQL</font>中默认是 第三个隔离级别 <font color='red'>repeatable read</font>

- <font color='red'>Oracle</font>中默认是 第二个隔离级别 <font color='red'>read committed</font>

- **常用命令**

	- 查看隔离级别

		<font color='red'>select @@tx_isolation;</font>

	- 设置隔离级别

		<font color='red'>set session/global transaction isolation level 隔离级别;</font>









## 七、视图

- **概念**：MySQL从5.0.1版本开始提供视图功能。一种虚拟存在的表，行和列的数据来自自定义视图的查询中使用的表，并且是在使用视图时动态生成的，只保存了SQL逻辑，不保存查询结果
- **应用场景：**
	- 多个地方用到同样的查询结果
	- 该查询结果使用的SQL语句较复杂
- **好处：**
	- 重复利用SQL语句
	- 简化了复杂的SQL操作，不必知道它的查询细节
	- 保护数据，提高安全性

### 1、创建视图

```sql
-- 语法
CREATE VIEW 视图名
AS
一系列要被封装的查询语句;
```

就是封装了一系列SQL语句，下次调用这个视图，直接就是这一些列语句。不用每次都写那么多重复语句

```sql
CREATE VIEW wudangV1 -- 将武当派所有人的信息封装成视图
AS
SELECT * 
FROM tulong 
WHERE school = '武当派';


-- 查看视图的内容
SELECT * FROM wudangV1;

-- 运用视图查看武当中名字结尾是山的人员
SELECT *
FROM wudangV1
WHERE `name` LIKE '%山';
```



### 2、修改视图

**方式一：**其实就是创建或者修改，存在就修改，不存在就创建

```sql
-- 语法
CREATE OR REPLACE VIEW 视图名
AS
一系列要被封装的查询语句;
```

**方式二：**

```sql
-- 语法
ALTER VIEW 视图名
AS
一系列要被封装的查询语句;
```



### 3、删除视图

```sql
-- 语法
DROP VIEW 视图名1,视图名2,视图名3,视图名4.....;   -- 可以删除多个视图
```



### 4、查看视图

```sql
-- 语法一
DESC 视图名;

-- 语法二
SHOW CREATE VIEW 视图名;
```



### 5、更新视图

就是：假设原表有10列，视图1中可能筛选了，只有2列，然后可以对视图1使用表的增删改功能，完全一致，将表名换成视图名就可以了，但是这个增删改同时也改变了原表的数据，对于视图中没有的列，原表数据会自动填充null。

**以下类型的视图是不支持更新的：**

- 包含以下关键字的SQL语句：
	- 分组函数
	- distinct
	- group by
	- having
	- union
	- union all
- 常量视图
- select中包含子查询
- join
- from一个不能更新的视图【套娃，视图1不能更新，你再from它，创建视图2，视图2必然不能更新】
- where子句的子查询引用了from子句中的表



## 八、变量

### 1、系统变量

使用语法：

**查看所有的系统变量：**

```sql
-- 1、查看搜有的系统变量
show global / session  variables;

-- 2、查看满足条件的部分系统变量
show global / session  variables like '%haha%';

-- 3、查看指定的某个系统变量的值
select @@global/session.系统变量名;

-- 4、为某个系统变量赋值
-- 方式一：
set global/session 系统变量名 = 值;
-- 方式二：
set @@global/session.系统变量名 = 值;
```

**注意：**

- 如果是全局变量，则需要加上global
- 如果是会话级别，则需要加session
- 如果什么都不加，默认是session



- **全局变量：**
	- 作用域：服务器每次启动，将为所有的全局变量赋初始值，针对于所有的会话（连接有效），但不能跨重启。

- **会话变量：**
	- 作用域：仅仅针对当前会话（连接有效）
- **用户变量：**
	- 作用域：仅仅针对当前会话（连接有效）
- **局部变量：**
	- 作用域：仅仅在定义它的begin end 中有效



### 2、自定义变量

- 用户变量：
	- 作用域：仅仅针对当前会话（连接有效）

- **用户变量使用语法：**

	```sql
	-- 1、声明并初始化【3种方式】
	set @用户变量名=值;
	set @用户变量名:=值;
	select @用户变量名:=值;
	
	
	-- 2、赋值（更新用户变量的值）
	-- 方式一    通过set或者select
	set @用户变量名=值;
	set @用户变量名:=值;
	select @用户变量名:=值;
	-- 方式二     通过select into
	select 字段 into 变量名
	from 表;-- 查询出来一个值，赋给变量，必须是一个值
	
	
	-- 3、查看用户变量值
	select @用户变量名;
	```

- **局部变量使用语法：**

	```sql
	-- 1、声明并初始化【2种方式】            -- 声明时 声明类型
	declare 变量名 类型;
	declare 变量名 类型 default 值;-- 赋默认值
	
	
	-- 2、赋值（更新用户变量的值）
	-- 方式一    通过set或者select
	set 局部变量名=值;
	set 局部变量名:=值;
	select @局部变量名:=值;
	-- 方式二     通过select into
	select 字段 into 局部变量名
	from 表;-- 查询出来一个值，赋给变量，必须是一个值
	
	
	-- 3、查看用户变量值
	select 局部变量名;
	```

	

- **对比用户变量和局部变量**

	|          | 作用域      | 定义和使用的位置                | 语法                          |
	| -------- | ----------- | ------------------------------- | ----------------------------- |
	| 用户变量 | 当前会话    | 会话中的任何地方                | 必须加@符号，不需要限定类型   |
	| 局部变量 | begin end中 | 只能在begin end中，且为第一句话 | 一般不用加@符号，需要限定类型 |

	```sql
	-- 用户变量
	SET @a = 1;
	SET @b = 2;
	SET @sum = @a+@b;
	SELECT @sum; -- 3
	
	-- 局部变量【直接运行报错，因为必须放在begin end中】
	DECLARE a INT DEFAULT 1;
	DECLARE b INT DEFAULT 2;
	DECLARE sum INT;
	SET sum = a+b;
	SELECT sum;
	```

	







## 九、存储过程和函数

### 1、存储过程

**定义：**一组预先编译好的SQL语句的集合，理解成批处理语句

- 提高了代码的重用性
- 简化了操作
- 减少了编译次数
- 减少了和数据库服务器的连接次数提高了效率

#### 一、创建及调用存储过程

```sql
-- 语法
CREATE PROCEDURE 存储过程名(参数列表)
BEGIN
			存储过程体（就是一组合法的SQL语句）
END

注意：
1、参数列表包含三部分
参数模式	参数名	  参数类型

eg： IN stuName VARCHAR(10)


-- 调用
CALL 存储过程名（实参列表）;

```

**注意：**

- **<font color='red'>参数列表包含三部分</font>**
- <font color='red'>**参数模式	参数名	  参数类型**</font>

- 参数模式包含：IN/OUT/INOUT三种
	- IN：该参数可以作为输入，也就是该参数需要调用者传入值【正常形参】
	- OUT：该参数可以作为输出，也就是该参数可以作为返回值【return】
	- INOUT：该参数既可以输入也可以输出，也就是该参数既需要传入值，也可以返回值

- 如果存储过程体仅仅只有一句话，BEGIN END可以省略
- 存储过程体中的每条SQL语句的结尾要求必须加分号
- 存储过程的结尾可以使用 DELIMITER 重新设置
- 语法：DELIMITER 结束标记【结束标记随便定义，啥都行】

##### **1、不带参数的结构：**

```sql
案例1
向my表中插入数据

DELIMITER !-- 将叹号设置成结束标记
CREATE PROCEDURE myP99999()
BEGIN
		INSERT INTO my(`named`)
		VALUES('丫蛋'),('张无忌'),('杨过'),('殷素素'),('赵敏'),('周芷若');
END !

-- 调用存储过程
CALL myp99() !
-- 因为设置了结束标记，每个语句结束必须用设定的标记，否则默认未输入完成，不执行操作
```

**注意：因为设置了结束标记，<font color='red'>每个语句结束必须用设定的标记</font>，否则默认未输入完成，不执行操作**



##### 2、带参数in的结构

<font color='red'>本例可以用于判断用户登录成功与否，传入账号密码，返回存在不存在</font>

```sql
-- 查询中国人口数大于100000的城市的个数
DELIMITER !
CREATE procedure myPopu(in countryCode varchar(5),in population int)
begin
			declare result int default 0;-- 声明变量，并初始化
			
			select count(*) into result -- 查询结果赋值给刚定义的变量
			from city
			where city.CountryCode = countryCode
			and city.Population > population;
			-- 城市个数大于100返回成功，小于100返回失败
			select if(result > 100,'成功','失败');-- 使用变量
end！

call myPopu('CHN',100000)!
```

##### 3、带参数out的结构

```sql
-- 根据给出的编号，在my表中找到对应的名字，根据名字在tulong表中找到门派，返回
DELIMITER !
CREATE procedure mySch(in id int,out school varchar(10))
begin
			
			select t.school into school
			-- 假如有两个out，select A,B into out1，out2
			from tulong t
			inner join my m on m.named = t.`name` -- 通过名字连接
			where m.id = id;-- 找到my表中id对应的行

end!

-- 调用
set @bschool varchar(10)!   -- 调用用户变量【此处也可以省略】
call mySch(2,@bschool)!				-- 直接这里也算是定义了@bschool
select @bschool!

```

##### 4、带参数inout的结构

```sql
delimiter !
create procedure myDouble(inout a int,inout b int)
begin
		set a=a*2;
		set b=b*2;
end!

-- 调用
set @m=10!
set @n=5!
call myDouble(@m,@n)!
select @m!   -- 20
select @n!   -- 10


```



#### 二、删除存储过程



```sql
-- 语法：
drop procedure myP;

drop procedure myP11,myP99;-- 错误！！！！只能一个一个删

```

#### 三、查看存储过程

```sql
-- 语法：
show create procedure myP11;

desc myP11; -- 不支持！！！！
-- desc 只能查看【表】或者【视图】的结构
```

**注意：**存储过程中的<font color='red'>begin end之间的语句不允许修改</font>



练习：创建存储过程，实现传入一个日期，格式化成xxxx年xx月xx日并返回

```sql
delimiter ! -- 结束符
create procedure dateToStr(in mydate datetime,out strDate varchar(20))
begin
		select date_format(mydate,'%Y年%m月%d日') into strDate;
end !

-- 调用
call dateToStr(now(),@str)!
select @str!

```



### 2、函数

**返回值区别：**

- 函数：有且仅有一个返回值【<font color='blue'>必须有一个，没有都不行</font>】

- 存储过程：可以有0个、1个、多个返回值

**适用场景：**

- 函数：适合用来处理数据，并返回一个结果
- 存储过程：适合做批量的插入、批量的更新操作

#### 一、创建及调用函数

```sql
-- 创建
create function 函数名(参数列表) returns 返回类型
begin
			函数体
end

-- 调用
select 函数名(参数列表)
```

**注意：**

- 参数列表包含<font color='red'>两部分</font>
	- <font color='red'>参数名   参数类型</font>
- 函数体肯定会有return语句，没有就会报错
- 当函数体只有一句话时，end可以省略
- 使用delimiter语句设置结束标记

##### 1、无参数函数

```sql
-- 查询统计表中，中国城市的个数
set global log_bin_trust_function_creators=1;
-- 开启修改设置函数的权限，否则报错，下次服务器重启会失效

delimiter !
create function countCity() returns int
begin
		declare c int default 0;-- 定义一个变量
		select COUNT(*) into c  -- 赋值
		from city
		where city.CountryCode = 'CHN';
		return c;
end!
select countCity()!
```

##### 2、带参数的函数

```sql
-- 查询统计表中，某个国家城市的个数
set global log_bin_trust_function_creators=1;
-- 开启修改设置函数的权限，否则报错，下次服务器重启会失效

delimiter !
create function countCity8(countrycode varchar(5)) returns int
begin
		declare c int default 0;-- 定义一个变量
		select COUNT(*) into c  -- 赋值
		from city
		where city.CountryCode = countrycode;
		return c;
end!
select countCity8('CHN')!
```



#### 二、删除函数

```sql
drop function countCity8;   -- 直接写函数名，不用加小括号！！！
```



#### 三、查看函数

```sql
show create function countCity8;   -- 直接写函数名，不用加小括号！！！
```





## 十、流程控制结构

**简介：**

- 顺序结构：程序从上往下依次执行
- 分支结构：程序从两条或多条路径中选择一条去执行
- 循环结构：程序在满足一定条件的基础上，重复执行一段代码

### 1、分支结构

#### 1、if函数

```sql
if(判断式,成立返回值,失败返回值)【就跟简单的return a>b? yes:no】
```

#### 2、if结构

功能：实现多重分支

```sql
if 条件1 then 语句1;
elseif 条件2 then 语句2;
elseif 条件3 then 语句3;
...
else 语句n;    -- 最后的else语句也可以省略
end if;
```

**注意：**只能用在begin end语句中

**练习：**创建函数，根据传入成绩判断等级并返回sdf 

```sql
create function test_if(score int) returns char
begin
		if score>=90 and score<=100 then return 'A';
		elseif score>=80 then return 'B';
		elseif score>=60 then return 'C';
		else return 'D';
		end if;
end!

call test_if(96)!

```



#### 3、case结构

情况1：类似java中的switch语句，一般用于<font color='red'>等值判断</font>

```sql
-- 返回值
case 变量/表达式/字段
when 要判断的值 then 返回的值1  -- 也可以返回语句，但是返回语句时，最后的end要改成end case;
when 要判断的值 then 返回的值2
when 要判断的值 then 返回的值3
....
else 要返回的值n
end;


-- 返回语句
case 变量/表达式/字段
when 要判断的值 then 返回的语句1;  -- 也可以返回语句，但是返回语句时，最后的end要改成end case;
when 要判断的值 then 返回的语句2;  -- 独立语句时，每条语句后面要加分号
when 要判断的值 then 返回的语句3;
....
else 要返回的语句n;
end case;
```

情况2：泪滴java中的多重if语句，一般用于<font color='red'>区间判断</font>

```sql
case 变量/表达式/字段
when 要判断的条件1 then 返回的值1
when 要判断的条件2 then 返回的值2
when 要判断的条件3 then 返回的值3
....
else 要返回的值n
end;
```

**特点：**

- <font color='red'>可以作为**表达式**，嵌套在其他语句中使用，可以放在任何地方，begin end中或者begin end外面</font>
- <font color='red'>可以作为**独立的语句**去使用，只能放在begin end中</font>
- 如果when中的值或者条件成立，则执行对应的then后面的语句，并结束case
- 如果都不满足，则执行else中的语句或值
- 如果else省略了，但是所有when中条件都不成立，则返回null
- **作为独立语句时，后面每条语句都要加分号**



**练习：**创建存储过程，根据传入成绩判断等级

```sql
create procedure test_case(in score int)
begin
		case
		when score>=90 and score<=100 then select 'A';
		when score>=80 then select 'B';
		when score>=60 then select 'C';
		ELSE SELECT 'D';
		END CASE;
end!

call test_case(96)!

```



### 2、循环结构

- 分类：
	- while
	- loop
	- repeat
- 循环控制
	- iterate【类似continue】，结束本次循环，继续下一次
	- leave【类似break】，结束当前循环，跳出循环

#### 1、while

```sql
标签:while 循环条件 do
	循环体;
end while 标签;
```



- **使用leave**

```sql
-- 向my表中插入数据，当插入20行时，停止
create procedure test_while(in insertcount int)
begin
		declare i int default 1;
		a:while i<=insertcount do
				insert into my(named)values(concat('张无忌',i));
				if i>20 then leave a;
				end if;
				set i = i+1;
		end while;
end!

-- 调用
call test_while(100)!
```

- **使用iterate**

	```sql
	-- 向my表中插入数据，只插入奇数i
	delimiter !
	create procedure test_while(in insertcount int)
	begin
			declare j int default 0;
			a:while j<=insertcount do
					set j=j+1;
					if MOD(j,2)=0 then iterate a;
					-- 如果不是奇数，继续下一层循环，不执行下边的插入语句
					end if;
					insert into my(named)values(concat('张无忌',j));
			end while a;
	end!
	
	-- 调用
	call test_while(100)!
	```

	



#### 2、loop

这个因为没有【循环条件】，如果不加iterate或者leave等控制结构，就是【死循环】

```sql
标签:loop
	循环体;
end loop 标签;
```



#### 3、repeat

类似do while 先执行后判断，也就是肯定会执行一次。

```sql
标签:repeat
	循环体;
until 结束循环的条件
end repeat 标签;
```



## 十一、大练习

已知表stringcontent其中字段：【运用函数、存储过程】

- id int 自增长
- content varchar(30)
- 向该表插入指定个数的随机字符串

```sql
-- 1、创建表
create table stringcontent(
	id int primary key auto_increment,
	content varchar(27)
);
-- 2、查看表
select * from stringcontent;

-- 3、创建函数【实现产生随机字符串】
set global log_bin_trust_function_creators=1; -- 开启函数设置、修改权限
delimiter $-- 设置结束标记
create function randStr() returns varchar(27)-- 定义函数，用于产生随机字符串
begin
		declare strs varchar(26) default('abcdefghijklmnopqrstuvwxyz');
		declare startIndex int default 1;
		declare len int default 1;
		set startIndex = floor(rand()*26+1);-- 产生一个1~26的随机整数
		set len = floor(rand()*(26+1-startIndex)+1); -- 26+1 再减去start保证1~26
		return substr(strs,startIndex,len);
end $

-- 4、创建存储过程【实现插入操作，其中调用函数】
delimiter $ -- 设置结束标记
create procedure myString(in nums int)
begin
			declare str varchar(27);
			while nums>0 do
			select randStr() into str;-- 调用函数，并赋值给str
			insert into stringcontent(content) values(str);-- 插入数据
			set nums = nums-1;
			end while;
end $

-- 5、调用存储过程
call myString(20)$  -- 调用存储过程



-- 6、工具
truncate table stringcontent;-- 清空表中数据
drop procedure myString; 	 -- 删除存储过程
drop function randStr;       -- 删除函数
```



## 面试题

### 一、执行结果是什么？并说明理由

#### 1、试问：下面两段代码输出结果一样吗？

> ```sql
> -- 代码一
> SELECT
> 	*
> FROM
> 	city;
> ```
>
> ```sql
> -- 代码二
> SELECT
> 	* 
> FROM
> 	city
> WHERE
> 	id LIKE '%%' AND Population LIKE '%%';
> ```
>
> 

**答：不一定相同；**

> 代码一：输出city表中所有的字段
>
> 代码二：对city表中的两个字段进行了模糊搜索，通配符%%全部匹配，正常来说，应该返回的也是所有数据，<font color='red'>但是：如果其中一个字段中包含null，那么就不能匹配，导致数据丢失</font>
>
> <font color='red'>若把AND 改成 OR，并把所有字段名全写上</font>，则会输出所有数据，除非有一行数据全部为null，因为使用OR 只要有一个不是null，就不影响数据输出







### 二、谈一谈数据库中主键约束和唯一约束的区别和联系？？

|          | 能否保证唯一性 | 是否允许为空 | 一个表中可以有多少列使用 | 是否允许组合     |
| -------- | -------------- | ------------ | ------------------------ | ---------------- |
| 主键约束 | 能             | 不允许       | 至多有一列               | 允许，但是不推荐 |
| 唯一约束 | 能             | 允许         | 可以有多列               | 允许，但是不推荐 |



### 三、谈谈数据库外键的使用及优缺点？？？？

外键：

- 要求在从表中设置外键关系
- 从表的外键列的类型和主表的关联列的类型要求一致或兼容，名称无要求
- 主表的关联列必须是一个key（一般是主键约束或唯一约束）
- 插入数据时，必须先插入主表，再插入从表【因为从表引用主表数据】
- 删除数据时，必须先删除从表，再删除主表【同上】

n
