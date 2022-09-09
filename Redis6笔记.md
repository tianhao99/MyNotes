#  一、NoSQL数据库简介

## 1、技术发展

### 1.1、技术的分类

1、解决功能性的问题：Java、Jsp、RDBMS、Tomcat、HTML、Linux、JDBC、SVN

2、解决扩展性的问题：Struts、Spring、SpringMVC、Hibernate、Mybatis

3、解决性能的问题：NoSQL、Java线程、Hadoop、Nginx、MQ、ElasticSearch



### 1.2、Web1.0时代

Web1.0的时代，数据访问量很有限，用一夫当关的高性能的单点服务器可以解决大部分问题。

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps1.jpg) 

 

### 1.3、Web2.0时代

随着Web2.0的时代的到来，用户访问量大幅度提升，同时产生了大量的用户数据。加上后来的智能移动设备的普及，所有的互联网平台都面临了巨大的性能挑战。

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps2.jpg) 

### 1.4、解决CPU及内存压力

负载均衡后，怎么保证每次同一用户的session一致问题

- 方案一：session存储在cookie中
  - 不安全、网络负担效率低
- 方案二：存在文件服务器或者数据库里
  - 大量的IO效率问题
- 方案三：session复制
  - session数据冗余
  - 节点越多浪费越大
- 方案四：缓存数据库
  - 完全在内存中，速度快，数据结构简单

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps3.png) 

 

### 1.5、解决IO压力

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps4.png)

## 2、NoSQL数据库

### 1、NoSQL数据库概述

NoSQL(NoSQL = <font color="red">Not Only SQL</font> )，意即“不仅仅是SQL”，泛指**<font color="red">非关系型的数据库</font>**。 

NoSQL 不依赖业务逻辑方式存储，而以简单的key-value模式存储。因此大大的增加了数据库的扩展能力。

- 不遵循SQL标准。

- 不支持ACID。【支持事务，但不支持这四大特性】

- 远超于SQL的性能。

### 2、NoSQL适用场景

- 对数据高并发的读写

- 海量数据的读写

- 对数据高可扩展性的

### 3、NoSQL不适用场景

- 需要事务支持

- 基于sql的结构化查询存储，处理复杂的关系,需要即席查询。

* 用不着sql的和用了sql也不行的情况，请考虑用NoSql

### 4、Memcache

| <img src="https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps5.png" alt="img" style="zoom: 25%;" /> | 很早出现的NoSql数据库<br />数据都在内存中，一般不持久化<br />支持简单的key-value模式，支持类型单一<br /> 一般是作为缓存数据库辅助持久化的数据库 |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
|                                                              |                                                              |

### 5、Redis

| <img src="https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps6.png" alt="img" style="zoom:33%;" /> | 几乎覆盖了Memcached的绝大部分功能<br />数据都在内存中，支持持久化，主要用作备份恢复<br />除了支持简单的key-value模式，还支持多种数据结构的存储，比如 list、set、hash、zset等。<br />一般是作为缓存数据库辅助持久化的数据库 |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
|                                                              |                                                              |

### 6、MongoDB

| <img src="https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps7.png" alt="img" style="zoom:33%;" /> | 高性能、开源、模式自由(schema  free)的文档型数据库**<br />数据都在内存中， 如果内存不足，把不常用的数据保存到硬盘<br /> 虽然是key-value模式，但是对value（尤其是**json**）提供了丰富的查询功能<br />支持二进制数据及大型对象ü 可以根据数据的特点**替代RDBMS** ，成为独立的数据库。或者配合RDBMS，存储特定的数据。 |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
|                                                              |                                                              |

## 3、行式存储数据库（大数据时代）

### 1、行式数据库

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps8.png) 

### 2、列式数据库

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps9.png) 

- **Hbase**

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps10.png) 

HBase是**Hadoop**项目中的数据库。它用于需要对大量的数据进行随机、实时的读写操作的场景中。

HBase的目标就是处理数据量**非常庞大 **的表，可以用**普通的计算机 **处理超过**10亿行数据 **，还可处理有数百万**列 **元素的数据表。

- **Cassandra**

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps11.png) 

Apache Cassandra是一款免费的开源NoSQL数据库，其设计目的在于管理由大量商用服务器构建起来的庞大集群上的**海量数据集(数据量通常达到PB级别) **。在众多显著特性当中，Cassandra最为卓越的长处是对写入及读取操作进行规模调整，而且其不强调主集群的设计思路能够以相对直观的方式简化各集群的创建与扩展流程。

计算机存储单位 计算机存储单位一般用B，KB，MB，GB，TB，EB，ZB，YB，BB来表示

它们之间的关系是：位 bit (比特)(Binary Digits)：存放一位二进制数，即 0 或 1，最小的存储单位。

字节 byte：8个二进制位为一个字节(B)，最常用的单位。

1KB (Kilobyte 千字节)=1024B

1MB (Megabyte 兆字节 简称“兆”)=1024KB

1GB (Gigabyte 吉字节 又称“千兆”)=1024MB

1TB (Trillionbyte 万亿字节 太字节)=1024GB，其中1024=2^10 ( 2 的10次方)

1PB（Petabyte 千万亿字节 拍字节）=1024TB

1EB（Exabyte 百亿亿字节 艾字节）=1024PB

1ZB (Zettabyte 十万亿亿字节 泽字节)= 1024 EB

1YB (Jottabyte 一亿亿亿字节 尧字节)= 1024 ZB

1BB (Brontobyte 一千亿亿亿字节)= 1024 YB

注：“兆”为百万级数量单位。

### 3、图关系型数据库

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps12.png) 

主要应用：社会关系，公共交通网络，地图及网络拓谱(n*(n-1)/2)

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps13.png) 

### 4、DB-Engines数据库排名

http://db-engines.com/en/ranking

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps14.jpg)














# 二、Redis6 概述和安装

## 1、Redis 概述

- Redis是一个开源的**key-value**存储系统。
- 和Memcached类似，它支持存储的value类型相对更多，包括string(字符串)、list(链表)、set(集合)、zset(sorted set --有序集合)和hash（哈希类型）。
- 这些数据类型都支持push/pop、add/remove及取交集并集和差集及更丰富的操作，而且这些操作都是原子性的。
- 在此基础上，Redis支持各种不同方式的排序。
- 与memcached一样，为了保证效率，数据都是缓存在内存中。
- 区别的是Redis会周期性的把更新的数据写入磁盘或者把修改操作写入追加的记录文件。
- 并且在此基础上实现了master-slave(主从)同步。

应用场景

- 配合关系型数据库做高速缓存
  - 高频次，热门访问的数据，降低数据库IO
  - 分布式架构，做session共享
  - ![image-20220731162853611](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220731162853611.png)

- 多样的数据结构存储持久化数据
  - ![image-20220731162903993](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220731162903993.png)

## 2、Redis安装

Redis官方网站	Redis中文官方网站
http://redis.io	



### 1、安装版本

- 7.0.4
- ![image-20220731164247913](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220731164247913.png)
- 不用考虑在windows环境下对Redis的支持

### 2、安装步骤

- 下载redis-7.0.4.tar.gz放/opt目录

- 进入文件目录，查看文件列表

  - ```bash
    cd /opt
    ls
    ```

  - ![image-20220801095902105](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220801095902105.png)

- 准备工作：下载安装最新版的gcc编译器【有gcc就不用再装了】

- 安装C 语言的编译环境

  ```bash
  yum install centos-release-scl scl-utils-build
  yum install -y devtoolset-8-toolchain
  scl enable devtoolset-8 bash
  # 测试 gcc版本 
  gcc --version
  ```

- 解压命令：```tar -zxvf redis-7.0.4.tar.gz```

- 解压完成后进入目录：```cd redis-7.0.4```

- 在redis-7.0.4目录下执行make命令（只是编译好）```make```开始编译

- 编译完成后，对编译好的文件进行安装```make install```

- 安装完成后到默认目录查看安装文件

  - ```bash
    cd /usr/local/bin
    ls
    # 展示如下：
    redis-benchmark  redis-check-rdb  redis-sentinel
    redis-check-aof  redis-cli        redis-server
    ```

  - 



- 如果没有准备好C语言编译环境，make 会报错—Jemalloc/jemalloc.h：没有那个文件
  - ![image-20220731163357108](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220731163357108.png)

- 解决方案：运行make distclean
  - ![image-20220731163404751](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220731163404751.png)

- 在redis-6.2.1目录下再次执行make命令（只是编译好）




### 3、安装目录：/usr/local/bin

查看默认安装目录：

- redis-benchmark:性能测试工具，可以在自己本子运行，看看自己本子性能如何
- redis-check-aof：修复有问题的AOF文件，rdb和aof后面讲
- redis-check-dump：修复有问题的dump.rdb文件
- redis-sentinel：Redis集群使用
- redis-server：Redis服务器启动命令
- redis-cli：客户端，操作入口

### 4、前台启动（不推荐）

```bash
# 启动命令，在usr/local/bin目录下
redis-server
```



- 前台启动，终端窗口不能关闭，否则服务器停止
- ![image-20220731163503593](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220731163503593.png)

### 5、后台启动（推荐）

- 备份redis.conf

  - 拷贝一份redis.conf到其他目录/etc/myredis.conf

  - ```bash
    # 当前在redis-7.0.4目录下 所以直接写文件名就行了，否则要写全路径
    # 文件不在安装目录下，在/opt/redis-7.0.4下面
    [root@CentOS7-01 redis-7.0.4]# cp redis.conf /etc/myredis.conf
    ```

    

- 到/etc/myredis.conf，修改配置文件内容

- 后台启动设置==daemonize no==改成==yes==

  - 修改redis.conf(128行)文件将里面的daemonize no 改成 yes，让服务在后台启动

  - ```bash
    vim myredis.conf
    # 找到内容，默认显示一页，继续翻页寻找，修改内容
    daemonize yes
    
    # 退出vim编辑器
    Esc :wq!   Enter
    ```

  - 

- Redis启动【指定自己写的配置文件，作为启动的配置文件】

  - ```bash
    [root@CentOS7-01 etc]# cd /usr/local/bin
    [root@CentOS7-01 bin]# ls
    # 目录文件列表
    redis-benchmark  redis-check-rdb  redis-sentinel
    redis-check-aof  redis-cli        redis-server
    # 启动redis，指定刚改的配置文件【不指定文件的话，还是默认前台启动】
    [root@CentOS7-01 bin]# redis-server /etc/myredis.conf
    
    # 查看状态
    [root@CentOS7-01 bin]# ps -ef | grep redis
    # 显示内容 
    root     11557     1 99 20:21 ?        00:17:38 redis-benchmark redis-check-rdb redis-sentinel
    root     11636     1  0 20:38 ?        00:00:00 redis-server 127.0.0.1:6379
    root     11643 11571  0 20:38 pts/1    00:00:00 grep --color=auto redis
    ```

  - 

- 用客户端访问：```redis-cli```


- 多个端口可以：```redis-cli -p6379```

- 测试验证： ```ping```

- Redis关闭 可以在redis内部时用exit关闭或者shutdown
  - ![image-20220801154553569](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220801154553569.png)
- 单实例关闭：```redis-cli shutdown```
  - ![image-20220801154530976](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220801154530976.png)
- 多实例关闭，指定端口关闭：```redis-cli -p 6379 shutdown```

## 3、Redis介绍相关知识

### 1、端口6379从何而来

Alessia  Merz名字在手机9键按键merz就是6379

- 默认16个数据库，类似数组下标从0开始，初始默认使用0号库
- <img src="https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220801105644424.png" alt="image-20220801105644424" style="zoom:50%;" />
- 使用命令 select   <dbid>来切换数据库。如: select 8 
- 统一密码管理，所有库同样密码。
- dbsize查看当前数据库的key的数量
- flushdb清空当前库
- flushall通杀全部库

### 2、Redis是单线程+多路IO复用技术

- 多路复用是指使用一个线程来检查多个文件描述符（Socket）的就绪状态，比如调用select和poll函数，传入多个文件描述符，如果有一个文件描述符就绪，则返回，否则阻塞直到超时。得到就绪状态后进行真正的操作可以在同一个线程里执行，也可以启动线程执行（比如使用线程池）
- memcached ：多线程+锁
- Redis： 单线程+多路IO复用
  - 一个进程/线程虽然任一时刻只能处理一个请求，但是处理每个请求的事件时，耗时控制在 1 毫秒以内，这样 1 秒内就可以处理上千个请求，把时间拉长来看，多个请求复用了一个进程/线程，这就是多路复用，这种思想很类似一个 CPU 并发多个进程，所以也叫做时分多路复用。
- （与Memcache三点不同: 支持多数据类型，支持持久化，单线程+多路IO复用）  
- ![image-20220731163732670](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220731163732670.png)



# 三、常用的五大数据类型

操作指令查询：http://www.redis.cn/commands.html

## 1、Redis  键key

- keys *          查看当前库所有key    (匹配：keys *1)

- exists key      判断某个key是否存在
- type key        查看你的key是什么类型
- del key           删除指定的key数据
- unlink key       根据value选择非阻塞删除
  - 仅将keys从keyspace元数据中删除，真正的删除会在后续异步操作。
- expire key 10         10秒钟：为给定的key设置过期时间
- ttl key                   查看还有多少秒过期，-1表示永不过期，-2表示已过期

- select                  命令切换数据库
- dbsize                 查看当前数据库的key的数量
- flushdb               清空当前库
- flushall                通杀全部库



## 2、Redis字符串(String)

### 1、简介

String是Redis最基本的类型，你可以理解成与Memcached一模一样的类型，一个key对应一个value。

String类型是二进制安全的。意味着Redis的string可以包含任何数据。比如jpg图片或者序列化的对象。

String类型是Redis最基本的数据类型，一个Redis中字符串value最多可以是512M

### 2、常用命令

- set   <key><value>添加键值对
  - ![image-20220801155012117](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220801155012117.png)

- setnx：当数据库中key不存在时，可以将key-value添加数据库
- setxx：当数据库中key存在时，可以将key-value添加数据库，与NX参数互斥
- setex：key的超时秒数
- setpx：key的超时毫秒数，与EX互斥

- get   <key>查询对应键值
- append  <key><value>将给定的<value> 追加到原值的末尾
- strlen  <key>获得值的长度
- setnx  <key><value>只有在 key 不存在时    设置 key 的值

- incr  <key>   将 key 中储存的数字值增1
  - 只能对数字值操作，如果为空，新增值为1

- decr  <key>  将 key 中储存的数字值减1
  - 只能对数字值操作，如果为空，新增值为-1
- incrby / decrby  <key><步长>      将 key 中储存的数字值增减。自定义步长。

![image-20220801155119986](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220801155119986.png)

- mget  <key1><key2><key3> .....

  - 同时获取一个或多个 value  
- msetnx <key1><value1><key2><value2>  ..... 
  - 同时设置一个或多个 key-value 对，当且仅当所有给定 key 都不存在。
  - **<font color='red'>原子性，有一个失败则都失败</font>**

- getrange  <key><起始位置><结束位置>
  - 全部展示的话范围就写【0,-1】
  - 获得值的范围，类似java中的substring，前包，后包
- setrange  <key><起始位置><value>
- 用 <value>  覆写<key>所储存的字符串值，从<起始位置>开始(索引从0开始)。

- setex  <key><过期时间><value>
- 设置键值的同时，设置过期时间，单位秒。
- getset <key><value>
- 以新换旧，设置了新值同时获得旧值。

### 3、数据结构

String的数据结构为简单动态字符串(Simple Dynamic String,缩写SDS)。是可以修改的字符串，内部结构实现上类似于Java的ArrayList，采用预分配冗余空间的方式来减少内存的频繁分配.

![image-20220801155201304](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220801155201304.png)

如图中所示，内部为当前字符串实际分配的空间capacity一般要高于实际字符串长度len。当字符串长度小于1M时，扩容都是加倍现有的空间，如果超过1M，扩容时一次只会多扩1M的空间。需要注意的是字符串最大长度为512M。



## 3、Redis列表(List)

### 1、简介

单键多值
Redis 列表是简单的字符串列表，按照插入顺序排序。你可以添加一个元素到列表的头部（左边）或者尾部（右边）。
它的底层实际是个双向链表，对两端的操作性能很高，通过索引下标的操作中间的节点性能会较差。

### 2、常用命令

- lpush/rpush  <key><value1><value2><value3> .... 从左边/右边插入一个或多个值。
- lpop/rpop  <key>从左边/右边吐出一个值。值在键在，值光键亡。

- rpoplpush  <key1><key2>从<key1>列表右边吐出一个值，插到<key2>列表左边。


- lrange <key><start><stop>  按照索引下标获得元素(从左到右)


- lrange mylist 0 -1   0左边第一个，-1右边第一个，（0-1表示获取所有）
- lindex <key><index>按照索引下标获得元素(从左到右)
- llen <key>获得列表长度 

- linsert <key>  before <value><newvalue>在<value>的后面插入<newvalue>插入值
- lrem <key><n><value>从左边删除n个value(从左到右)
- lset<key><index><value>将列表key下标为index的值替换成value

### 3、数据结构

List的数据结构为快速链表quickList。

首先在列表元素较少的情况下会使用一块连续的内存存储，这个结构是ziplist，也即是压缩列表。

它将所有的元素紧挨着一起存储，分配的是一块连续的内存。

当数据量比较多的时候才会改成quicklist。

因为普通的链表需要的附加指针空间太大，会比较浪费空间。比如这个列表里存的只是int类型的数据，结构上还需要两个额外的指针prev和next。

![image-20220801161402356](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220801161402356.png)

Redis将链表和ziplist结合起来组成了quicklist。也就是将多个ziplist使用双向指针串起来使用。这样既满足了快速的插入删除性能，又不会出现太大的空间冗余。



## 4、Redis集合(Set)

### 1、简介

Redis set对外提供的功能与list类似是一个列表的功能，特殊之处在于set是可以自动排重的，当你需要存储一个列表数据，又不希望出现重复数据时，set是一个很好的选择，并且set提供了判断某个成员是否在一个set集合内的重要接口，这个也是list所不能提供的。
Redis的Set是string类型的无序集合。它底层其实是一个value为null的hash表，所以添加，删除，查找的复杂度都是O(1)。
一个算法，随着数据的增加，执行时间的长短，如果是O(1)，数据增加，查找数据的时间不变

### 2、常用命令

- sadd <key><value1><value2> ..... 
  - 将一个或多个 member 元素加入到集合 key 中，已经存在的 member 元素将被忽略
- smembers <key>取出该集合的所有值。
- sismember <key><value>判断集合<key>是否为含有该<value>值，有1，没有0
- scard<key>返回该集合的元素个数。
- srem <key><value1><value2> .... 删除集合中的某个元素。
- spop <key>随机从该集合中吐出一个值。
- srandmember <key><n>随机从该集合中取出n个值。不会从集合中删除 。
- smove <source><destination>value把集合中一个值从一个集合移动到另一个集合
- sinter <key1><key2>返回两个集合的交集元素。
- sunion <key1><key2>返回两个集合的并集元素。
- sdiff <key1><key2>返回两个集合的差集元素(key1中的，不包含key2中的)

### 3、数据结构

Set数据结构是dict字典，字典是用哈希表实现的。
Java中HashSet的内部实现使用的是HashMap，只不过所有的value都指向同一个对象。Redis的set结构也是一样，它的内部也使用hash结构，所有的value都指向同一个内部值。



## 5、Redis哈希(Hash)

### 1、简介

Redis hash 是一个键值对集合。
Redis hash是一个string类型的field和value的映射表，hash特别适合用于存储对象。
类似Java里面的Map<String,Object>
用户ID为查找的key，存储的value用户对象包含姓名，年龄，生日等信息，如果用普通的key/value结构来存储

主要有以下2种存储方式：

![image-20220801161655729](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220801161655729.png)

### 2、常用命令

- hset <key><field><value>给<key>集合中的  <field>键赋值<value>

- hget <key1><field>从<key1>集合<field>取出 value 
- hmset <key1><field1><value1><field2><value2>... 批量设置hash的值
- hexists<key1><field>查看哈希表 key 中，给定域 field 是否存在。 
- hkeys <key>列出该hash集合的所有field
- hvals <key>列出该hash集合的所有value
- hincrby <key><field><increment>为哈希表 key 中的域 field 的值加上增量 1   -1
- hsetnx <key><field><value>将哈希表 key 中的域 field 的值设置为 value ，当且仅当域 field 不存在 .

### 3、数据结构

Hash类型对应的数据结构是两种：ziplist（压缩列表），hashtable（哈希表）。当field-value长度较短且个数较少时，使用ziplist，否则使用hashtable。

## 6、Redis有序集合Zset(sorted set) 

### 1、简介

Redis有序集合zset与普通集合set非常相似，是一个没有重复元素的字符串集合。
不同之处是有序集合的每个成员都关联了一个评分（score）,这个评分（score）被用来按照从最低分到最高分的方式排序集合中的成员。集合的成员是唯一的，但是评分可以是重复了 。
因为元素是有序的, 所以你也可以很快的根据评分（score）或者次序（position）来获取一个范围的元素。
访问有序集合的中间元素也是非常快的,因此你能够使用有序集合作为一个没有重复成员的智能列表。

### 2、常用命令

- zadd  <key><score1><value1><score2><value2>…
  - 将一个或多个 member 元素及其 score 值加入到有序集 key 当中。
- zrange <key><start><stop>  [WITHSCORES]   
  - 返回有序集 key 中，下标在<start><stop>之间的元素
- 带WITHSCORES，可以让分数一起和值返回到结果集。
- zrangebyscore key minmax [withscores] [limit offset count]
  - 返回有序集 key 中，所有 score 值介于 min 和 max 之间(包括等于 min 或 max )的成员。有序集成员按 score 值递增(从小到大)次序排列。 
- zrevrangebyscore key maxmin [withscores] [limit offset count]               
  - 同上，改为从大到小排列。 
- zincrby <key><increment><value>      为元素的score加上增量
- zrem  <key><value>删除该集合下，指定值的元素 
- zcount <key><min><max>统计该集合，分数区间内的元素个数 
- zrank <key><value>返回该值在集合中的排名，从0开始。
- 案例：如何利用zset实现一个文章访问量的排行榜？

![image-20220801161716796](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220801161716796.png)

### 3、数据结构

SortedSet(zset)是Redis提供的一个非常特别的数据结构，一方面它等价于Java的数据结构Map<String, Double>，可以给每一个元素value赋予一个权重score，另一方面它又类似于TreeSet，内部的元素会按照权重score进行排序，可以得到每个元素的名次，还可以通过score的范围来获取元素的列表。
zset底层使用了两个数据结构
（1）hash，hash的作用就是关联元素value和权重score，保障元素value的唯一性，可以通过元素value找到相应的score值。
（2）跳跃表，跳跃表的目的在于给元素value排序，根据score的范围获取元素列表。

### 4、跳跃表（跳表）

1、简介
	有序集合在生活中比较常见，例如根据成绩对学生排名，根据得分对玩家排名等。对于有序集合的底层实现，可以用数组、平衡树、链表等。数组不便元素的插入、删除；平衡树或红黑树虽然效率高但结构复杂；链表查询需要遍历所有效率低。Redis采用的是跳跃表。跳跃表效率堪比红黑树，实现远比红黑树简单。
2、实例
	对比有序链表和跳跃表，从链表中查询出51

（1）有序链表

![image-20220801161904343](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220801161904343.png)

要查找值为51的元素，需要从第一个元素开始依次查找、比较才能找到。共需要6次比较。
（2）跳跃表

![image-20220801161919621](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220801161919621.png)

从第2层开始，1节点比51节点小，向后比较。
21节点比51节点小，继续向后比较，后面就是NULL了，所以从21节点向下到第1层
在第1层，41节点比51节点小，继续向后，61节点比51节点大，所以从41向下
在第0层，51节点为要查找的节点，节点被找到，共查找4次。

从此可以看出跳跃表比有序链表效率要高



# 四、Redis6 配置文件详解

部分配置文件注释

配置文件英文注释很详细了，可以对应查看配置文件的每个英文注释

```bash
# 类似导入，可以包含其他配置文件，就和前端提取公共部分一样
# include /path/to/local.conf
# include /path/to/other.conf
# include /path/to/fragments/*.conf


# 这个代码意思是支持持本地连接，不能被其他电脑连接
bind 127.0.0.1 -::1
# 将他注销掉，就支持远程访问了，下边再改一个protected-mode为no就可以远程访问了
# bind 127.0.0.1 -::1

# 保护模式，yes后不能被远程访问，改成no就能远程访问了
protected-mode no

# 默认端口号
port 6379

# 设置tcp的backlog，backlog其实是一个连接队列，backlog队列总和=未完成三次握手队列 + 已经完成三次握手队列。
# 在高并发环境下你需要一个高backlog值来避免慢客户端连接问题。

tcp-backlog 511

# 秒为单位，设置客户端连接超时时间，
# 如timeout 4，表示客户端连接后，4秒内无操作，就断开连接， 想操作就得重新连接
# timeout 0.表示永不超时
timeout 0

# 检测心跳，   秒为单位，如果300秒内没有操作，那么释放连接
tcp-keepalive 300

# no 表示前台启动，yes表示以后台启动
daemonize no


# 进程号，存放pid文件的位置，每个实例会产生一个不同的pid文件
pidfile /var/run/redis_6379.pid

# 指定日志记录级别，Redis总共支持四个级别：debug、verbose、notice、warning，默认为notice
# 四个级别根据使用阶段来选择，生产环境选择notice 或者warning
loglevel notice

# 日志名称
logfile ""

# 设定库的数量 默认16，默认数据库为0，可以使用SELECT <dbid>命令在连接上指定数据库id
databases 16
```



设置密码

![image-20220801165738033](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220801165738033.png)

访问密码的查看、设置和取消
在命令中设置密码，只是临时的。重启redis服务器，密码就还原了。
永久设置，需要再配置文件中进行设置。

![image-20220801165747735](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220801165747735.png)

LIMITS限制

maxclients

- 设置redis同时可以与多少个客户端进行连接。
- 默认情况下为10000个客户端。
- 如果达到了此限制，redis则会拒绝新的连接请求，并且向这些连接请求方发出“max number of clients reached”以作回应。
- ![image-20220801165823352](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220801165823352.png)

maxmemory 

- **建议必须设置**，否则，将内存占满，造成服务器宕机
- 设置redis可以使用的内存量。一旦到达内存使用上限，redis将会试图移除内部数据，移除规则可以通过maxmemory-policy来指定。
- 如果redis无法根据移除规则来移除内存中的数据，或者设置了“不允许移除”，那么redis则会针对那些需要申请内存的指令返回错误信息，比如SET、LPUSH等。
- 但是对于无内存申请的指令，仍然会正常响应，比如GET等。如果你的redis是主redis（说明你的redis有从redis），那么在设置内存使用上限时，需要在系统中留出一些内存空间给同步队列缓存，只有在你设置的是“不移除”的情况下，才不用考虑这个因素。
- ![image-20220801165852174](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220801165852174.png)



maxmemory-policy

- volatile-lru：使用LRU算法移除key，只对设置了过期时间的键；（最近最少使用）
- allkeys-lru：在所有集合key中，使用LRU算法移除key
- volatile-random：在过期集合中移除随机的key，只对设置了过期时间的键
- allkeys-random：在所有集合key中，移除随机的key
- volatile-ttl：移除那些TTL值最小的key，即那些最近要过期的key
- noeviction：不进行移除。针对写操作，只是返回错误信息
- ![image-20220801165925790](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220801165925790.png)

maxmemory-samples

- 设置样本数量，LRU算法和最小TTL算法都并非是精确的算法，而是估算值，所以你可以设置样本的大小，redis默认会检查这么多个key并选择其中LRU的那个。
- 一般设置3到7的数字，数值越小样本越不准确，但性能消耗越小。
- ![image-20220801165932904](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220801165932904.png)



# 五、Redis6 的发布和订阅

## 1、简介

客户端可以订阅频道，也可以发布频道信息

![image-20220801171415524](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220801171415524.png)

当频道有新消息发布之后，就会通知所有订阅他的客户端

![image-20220801172232602](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220801172232602.png)

## 2、操作命令

1、订阅频道

```bash
# 订阅频道channel1
SUBSCRIBE channel1
```

2、发布消息

```bash
# 发送消息
publish channel1 hello我是新消息
```

3、已订阅的客户端就会收到即使的消息推送

![image-20220801173002551](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220801173002551.png)

注：发布的消息没有持久化，如果在订阅的客户端收不到hello，只能收到订阅后发布的消息



# 六、Redis6 新数据类型

## 1、Bitmaps

<font color="red">用**<font color="green">位运算</font>**存储数据，适合统计活跃用户的登录次数之类的，但是僵尸用户就不适合，白白的占地方</font>

### 1、简介

现代计算机用二进制（位） 作为信息的基础单位， 1个字节等于8位， 例如“abc”字符串是由3个字节组成， 但实际在计算机存储时将其用二进制表示， “abc”分别对应的ASCII码分别是97、 98、 99， 对应的二进制分别是01100001、 01100010和01100011，如下图

![image-20220801180745628](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220801180745628.png)

合理地使用操作位能够有效地提高内存使用率和开发效率。

Redis提供了Bitmaps这个“数据类型”可以实现对位的操作：
（1）Bitmaps本身不是一种数据类型， 实际上它就是字符串（key-value） ， 但是它可以对字符串的位进行操作。
（2）Bitmaps单独提供了一套命令， 所以在Redis中使用Bitmaps和使用字符串的方法不太相同。 

<font color = "red">可以把Bitmaps想象成一个以位为单位的数组， 数组的每个单元只能存储0和1， 数组的下标在Bitmaps中叫做偏移量。</font>

![image-20220801181221423](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220801181221423.png)

### 2、命令

#### 1、setbit

（1）语法

setbit<key><offset><value>     设置Bitmaps中某个偏移量的值（0或1）

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps56.jpg) 

*offset:偏移量从0开始

 

（2）实例

每个独立用户是否访问过网站存放在Bitmaps中， 将访问的用户记做1， 没有访问的用户记做0， 用偏移量作为用户的id。

设置键的第offset个位的值（从0算起） ， 假设现在有20个用户，userid=1， 6， 11， 15， 19的用户对网站进行了访问， 那么当前Bitmaps初始化结果如图

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps57.jpg)

unique:users:20201106代表2020-11-06这天的独立访问用户的Bitmaps 

unique:users:20201106【这一串就是一个key】key offset  value

![image-20220801181605914](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220801181605914.png)

注：

<font color="red">很多应用的用户id以一个指定数字（例如10000） 开头， 直接将用户id和Bitmaps的偏移量对应势必会造成一定的浪费， 通常的做法是每次做setbit操作时将用户id减去这个指定数字。</font>

在第一次初始化Bitmaps时， 假如偏移量非常大， 那么整个初始化过程执行会比较慢， 可能会造成Redis的阻塞。

#### 2、getbit

（1）格式

getbit<key><offset>获取Bitmaps中某个偏移量的值

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps58.jpg) 

获取键的第offset位的值（从0开始算）

 

（2）实例

获取id=8的用户是否在2020-11-06这天访问过， 返回0说明没有访问过：

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps59.jpg) 

 

注：因为100根本不存在，所以也是返回0

 

#### 3、bitcount

统计**字符串 **被设置为1的bit数。一般情况下，给定的整个字符串都会被进行计数，通过指定额外的 start 或 end 参数，可以让计数只在特定的位上进行。start 和 end 参数的设置，都可以使用负数值：比如 -1 表示最后一个位，而 -2 表示倒数第二个位，start、end 是指bit组的字节的下标数，二者皆包含。

（1）格式

bitcount<key>[start end] 统计字符串从start字节到end字节比特值为1的数量

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps60.jpg) 

 

（2）实例

计算2022-11-06这天的独立访问用户数量

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps61.jpg) 

 

start和end代表起始和结束字节数， 下面操作计算用户id在第1个字节到第3个字节之间的独立访问用户数， 对应的用户id是11， 15， 19。

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps62.jpg) 

 

举例： K1 【01000001 01000000  00000000 00100001】，对应【0，1，2，3】

bitcount K1 1 2  ： 统计下标1、2字节组中bit=1的个数，即01000000  00000000

```bash
bitcount K1 1 2 　　
# 结果
1
```

bitcount K1 1 3  ： 统计下标1、2、3字节组中bit=1的个数，即01000000  00000000 00100001

```bash
bitcount K1 1 3　　
# 结果
3
```

bitcount K1 0 -2  ： 统计下标0到下标倒数第2，字节组中bit=1的个数，即01000001  01000000  00000000

```bash
bitcount K1 0 -2　
# 结果
3 
```

 注意：redis的setbit设置或清除的是bit位置，而bitcount计算的是byte位置。

 

#### 4、bitop

(1)格式

bitop and(or/not/xor) <destkey> [key…]

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps63.jpg) 

bitop是一个复合操作， 它可以做多个Bitmaps的and（交集） 、 or（并集） 、 not（非） 、 xor（异或） 操作并将结果保存在destkey中。

 

(2)实例

2020-11-04 日访问网站的userid=1,2,5,9。

<font color="red">注： 【unique:users:20201104】  这就是个key，别误会</font>

- setbit unique:users:20201104 1 1
- setbit unique:users:20201104 2 1
- setbit unique:users:20201104 5 1
- setbit unique:users:20201104 9 1

2020-11-03 日访问网站的userid=0,1,4,9。

- setbit unique:users:20201103 0 1
- setbit unique:users:20201103 1 1
- setbit unique:users:20201103 4 1
- setbit unique:users:20201103 9 1

 

计算出两天都访问过网站的用户数量

bitop and unique:users:and:20201104_03

 unique:users:20201103unique:users:20201104

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps64.jpg) 

 

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps65.jpg) 

计算出任意一天都访问过网站的用户数量（例如月活跃就是类似这种） ， 可以使用or求并集

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps66.jpg) 

 

### 3、Bitmaps与set对比

假设网站有1亿用户， 每天独立访问的用户有5千万， 如果每天用集合类型和Bitmaps分别存储活跃用户可以得到表

 ![image-20220801184121418](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220801184121418.png)

很明显， 这种情况下使用Bitmaps能节省很多的内存空间， 尤其是随着时间推移节省的内存还是非常可观的

![image-20220801184109475](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220801184109475.png) 

但Bitmaps并不是万金油， 假如该网站每天的独立访问用户很少， 例如只有10万（大量的僵尸用户） ， 那么两者的对比如下表所示， 很显然， 这时候使用Bitmaps就不太合适了， 因为基本上大部分位都是0。

<font color="red">Bitmaps存储活跃用户更合适，要不然大部分僵尸用户反而占据了大部分内存</font>

![image-20220801184054249](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220801184054249.png)

## 2、HyperLogLog

<font color="red">统计**<font color="green">基数</font>**个数，其实普通的set或者mysql也能实现查找不重复元素个数的操作。但是数据量级上去以后，就不如单独设置一个类型，只用来统计，不用遍历操作了</font>

### 1、简介

在工作当中，我们经常会遇到与统计相关的功能需求，比如统计网站PV（PageView页面访问量）,可以使用Redis的incr、incrby轻松实现。

但像UV（UniqueVisitor，独立访客）、独立IP数、搜索记录数等需要去重和计数的问题如何解决？这种求集合中不重复元素个数的问题称为基数问题。

解决基数问题有很多种方案：

（1）数据存储在MySQL表中，使用distinct count计算不重复个数

（2）使用Redis提供的hash、set、bitmaps等数据结构来处理

以上的方案结果精确，但随着数据不断增加，导致占用空间越来越大，对于非常大的数据集是不切实际的。

能否能够降低一定的精度来平衡存储空间？Redis推出了HyperLogLog

Redis HyperLogLog 是用来做基数统计的算法，HyperLogLog 的优点是，在输入元素的数量或者体积非常非常大时，计算基数所需的空间总是固定的、并且是很小的。

在 Redis 里面，每个 HyperLogLog 键只需要花费 12 KB 内存，就可以计算接近 2^64 个不同元素的基数。这和计算基数时，元素越多耗费内存就越多的集合形成鲜明对比。

但是，因为 HyperLogLog 只会根据输入元素来计算基数，而不会储存输入元素本身，所以 HyperLogLog 不能像集合那样，返回输入的各个元素。

 

什么是基数?

比如数据集 {1, 3, 5, 7, 5, 7, 8}， 那么这个数据集的基数集为 {1, 3, 5 ,7, 8}, 基数(不重复元素)为5。 基数估计就是在误差可接受的范围内，快速计算基数。

 

### 2、命令

#### 1、pfadd 

（1）格式

pfadd <key>< element> [element ...]  添加指定元素到 HyperLogLog 中

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps67.jpg) 

 

（2）实例

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps68.jpg) 

​	将所有元素添加到指定HyperLogLog数据结构中。如果执行命令后HLL估计的近似基数发生变化，则返回1，否则返回0。

 

#### 2、pfcount

（1）格式

pfcount<key> [key ...] 计算HLL的近似基数，可以计算多个HLL，比如用HLL存储每天的UV，计算一周的UV可以使用7天的UV合并计算即可

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps69.jpg) 

 

（2）实例

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps70.jpg) 

 

#### 3、pfmerge

（1）格式

pfmerge<destkey><sourcekey> [sourcekey ...]  将一个或多个HLL合并后的结果存储在另一个HLL中，比如每月活跃用户可以使用每天的活跃用户来合并计算可得

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps71.jpg) 

 

 

（2）实例

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps72.jpg) 

 

 

## 3、Geospatial

<font color="red">根据**<font color="green">经纬度</font>**存储数据，可以筛选范围，求直线距离等操作</font>

### 1、简介

Redis 3.2 中增加了对GEO类型的支持。GEO，Geographic，地理信息的缩写。该类型，就是元素的2维坐标，在地图上就是经纬度。redis基于该类型，提供了经纬度设置，查询，范围查询，距离查询，经纬度Hash等常见操作。

 

### 2、命令

#### 1、geoadd

（1）格式

geoadd<key>< longitude><latitude><member> [longitude latitude member...]  添加地理位置（经度，纬度，名称）

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps73.jpg) 

 

（2）实例

geoadd china:city 121.47 31.23 shanghai

geoadd china:city 106.50 29.53 chongqing 114.05 22.52 shenzhen 116.38 39.90 beijing

 

 

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps74.jpg) 

两极无法直接添加，一般会下载城市数据，直接通过 Java 程序一次性导入。

有效的经度从 -180 度到 180 度。有效的纬度从 -85.05112878 度到 85.05112878 度。

当坐标位置超出指定范围时，该命令将会返回一个错误。

已经添加的数据，是无法再次往里面添加的。

#### 2、geopos  

（1）格式

geopos  <key><member> [member...]  获得指定地区的坐标值

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps75.jpg) 

  

（2）实例

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps76.jpg) 

 

#### 3、geodist

（1）格式

geodist<key><member1><member2>  [m|km|ft|mi ]  获取两个位置之间的直线距离

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps77.jpg) 

 

（2）实例

获取两个位置之间的直线距离

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps78.jpg) 

单位：

m 表示单位为米[默认值]。

km 表示单位为千米。

mi 表示单位为英里。

ft 表示单位为英尺。

如果用户没有显式地指定单位参数， 那么 GEODIST 默认使用米作为单位

#### 4、georadius

（1）格式

georadius<key>< longitude><latitude>radius m|km|ft|mi  以给定的经纬度为中心，找出某一半径内的元素

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps79.jpg) 

经度 纬度 距离 单位



（2）实例

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps80.jpg) 



# 七、Jedis操作Redis6

## 1、导入Jedis所需要的jar包

```xml
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
    <version>3.2.0</version>
</dependency>
```

## 2、连接Redis注意事项

禁用Linux的防火墙：Linux(CentOS7)里执行命令

```bash
systemctl stop/disable firewalld.service
```

修改redis配置信息【允许外部访问】

redis.conf中注释掉bind 127.0.0.1 ,然后 protected-mode no

## 3、Jedis常用操作

3.1、创建动态的工程

3.2、创建测试程序

```java
import redis.clients.jedis.Jedis;
public class Demo01 {
public static void main(String[] args) {
  	Jedis jedis = new Jedis("192.168.137.3",6379);
        String pong = jedis.ping();
        System.out.println("连接成功："+pong);
        jedis.close();
  	}
}
```

## 4、测试相关数据类型

### 1、Jedis-API:    Key

```java
jedis.set("k1", "v1");
jedis.set("k2", "v2");
jedis.set("k3", "v3");
Set<String> keys = jedis.keys("*");
System.out.println(keys.size());
for (String key : keys) {
		System.out.println(key);
}
System.out.println(jedis.exists("k1"));
System.out.println(jedis.ttl("k1"));                
System.out.println(jedis.get("k1"));

```

### 2、Jedis-API:    String

```java
jedis.mset("str1","v1","str2","v2","str3","v3");
System.out.println(jedis.mget("str1","str2","str3"));
```



### 3、Jedis-API:    List

```java
List<String> list = jedis.lrange("mylist",0,-1);
for (String element : list) {
		System.out.println(element);
}
```



### 4、Jedis-API:    set

```java
jedis.sadd("orders", "order01");
jedis.sadd("orders", "order02");
jedis.sadd("orders", "order03");
jedis.sadd("orders", "order04");
Set<String> smembers = jedis.smembers("orders");
for (String order : smembers) {
		System.out.println(order);
}
jedis.srem("orders", "order02");
```



### 5、Jedis-API:    hash

```java
jedis.hset("hash1","userName","lisi");
System.out.println(jedis.hget("hash1","userName"));
Map<String,String> map = new HashMap<String,String>();
map.put("telphone","13810169999");
map.put("address","atguigu");
map.put("email","abc@163.com");
jedis.hmset("hash2",map);
List<String> result = jedis.hmget("hash2", "telphone","email");
for (String element : result) {
		System.out.println(element);
}
```



### 6、Jedis-API:    zset

```java
jedis.zadd("zset01", 100d, "z3");
jedis.zadd("zset01", 90d, "l4");
jedis.zadd("zset01", 80d, "w5");
jedis.zadd("zset01", 70d, "z6");

List<String> zrange = jedis.zrange("zset01", 0, -1);
for (String e : zrange) {
		System.out.println(e);
}
```

# 八、Redis_Jedis_实例

需求：完成一个手机验证码功能

要求：

1、输入手机号，点击发送后随机生成6位数字码，2分钟有效

2、输入验证码，点击验证，返回成功或失败

3、每个手机号每天只能输入3次

![image-20220801191433986](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220801191433986.png)



## 1、代码分析

一、Java生成6位随机数

二、Redis中存入，并设置过期时间120秒

三、Redis中读取数据，验证操作

四、Redis设置每天3次

```java
package com.pledge.controller;

import redis.clients.jedis.Jedis;

import java.util.Random;

/**
 * @ClassName PhoneCode
 * @Description TODO:
 * @Author sth_199509@163.com
 * @Date 2022/8/2 11:03
 * @Version 1.0
 */
public class PhoneCode {

    // 获取连接
    static Jedis jedis = new Jedis("192.168.31.190",6379);

		// 测试
    public static void main(String[] args) {
        // 131 申请验证码，获取申请到的验证码，或者已达上限的提示
        String code = applyCode("132");
        // 判断申请 成功与否，
        if (code.length() == 6) System.out.println("验证码申请成功，120秒有效,验证码是：" + code);
        else System.out.println("您今日申请次数已达上限，请明天再来继续申请!");



        // 131 填充验证码,获取验证结果
        boolean verify131 = verifyCode("132", code);

        // 判断，验证成功了
        if (verify131) System.out.println("验证成功,验证码是：" + code);
        else System.out.println("验证失败，请核对验证码后输入，并在120秒内使用");

        // 关闭客户端连接
        jedis.close();


    }


    /**
     * 申请验证码
     * @param phone
     * @return
     */
    public static String applyCode(String phone){
        // 单独存储，两个key，一个存验证码，一个存当天次数
        String countKey = "VerifyCode" + phone + ":count";
        String codeKey = "VerifyCode" + phone + ":code";
        String count = jedis.get(countKey);
        if(count == null){
            // 当天没有申请过验证码，允许申请
            jedis.setex(countKey,24*60*60,"1");   // 当天申请次数为1，有效期为1天   24*60*60秒
            String code = RandomCode();
            jedis.setex(codeKey,120,code);    // 存储验证码,120秒有效
            return code;
        }else if(Integer.parseInt(count) == 3){
            return "您当天申请次数已达到3次，请明日再来申请!";
        }else{
            // 当允许申请
            jedis.incr(countKey); // 值加一
            String code = RandomCode();
            jedis.setex(codeKey,120,code);    // 存储验证码,120秒有效
            return code;
        }
    }

    /**
     * 核对验证码
     * @param phone
     * @param code
     * @return
     */
    public static boolean verifyCode(String phone,String code){

        // 单独存储，两个key，一个存验证码，一个存当天次数
        String countKey = "VerifyCode" + phone + ":count";
        String codeKey = "VerifyCode" + phone + ":code";

        String count = jedis.get(countKey);
        if(count == null){
            return false;
        }else{
            return code.equals(jedis.get(codeKey));
        }
    }



    /**
     * 生成6位随机验证码
     * @return
     */
    public static String RandomCode(){
        Random random = new Random();
        String res = "";
        for (int j = 0; j < 6; j++) {
            int i = random.nextInt(10);
            res += String.valueOf(i);
        }
        return res;
    }
}
```

<img src="https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220802120709781.png" alt="image-20220802120709781" style="zoom:50%;" />

# 九、Redis6 和SpringBoot整合

##### 1、导入依赖

```xml
<dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

如果想使用jedis，还可以导入jedis依赖，然后修改配置文件client-type: jedis

```xml
<!--        导入jedis-->
        <dependency>
            <groupId>redis.clients</groupId>
            <artifactId>jedis</artifactId>
        </dependency>
```



##### 3、修改配置文件

```properties
#Redis服务器地址
spring.redis.host=192.168.140.136
#Redis服务器连接端口
spring.redis.port=6379

# 除了上边的，底下的参数会有默认值，不是必须配置

#Redis数据库索引（默认为0）
spring.redis.database= 0
#连接超时时间（毫秒）
spring.redis.timeout=1800000
#连接池最大连接数（使用负值表示没有限制）
spring.redis.lettuce.pool.max-active=20
#最大阻塞等待时间(负数表示没限制)
spring.redis.lettuce.pool.max-wait=-1
#连接池中的最大空闲连接
spring.redis.lettuce.pool.max-idle=5
#连接池中的最小空闲连接
spring.redis.lettuce.pool.min-idle=0
```



```yaml
# yaml格式
spring
  redis:
    host: 192.168.31.190
    port: 6379
    
    # 下面如果使用jedis客户端，就需要配置，否则不用配置
    client-type: jedis
    jedis:
      pool:
        max-active: 10
```



##### 4、测试

```java
@RestController
//@RequestMapping("/redis")
public class RedisTestController {
    @Autowired
    StringRedisTemplate redisTemplate;
    @ResponseBody
    @GetMapping("/redis")
    public String mainPage(Model model){
        // 保存数据到Redis
        redisTemplate.opsForValue().set("1","我是SpringBoot1");
        redisTemplate.opsForValue().set("2","我是SpringBoot2");
        redisTemplate.opsForValue().set("3","我是SpringBoot3");
        redisTemplate.opsForValue().set("4","我是SpringBoot4");

        // 获取到Redis数据
        ValueOperations<String, String> opsForValue = redisTemplate.opsForValue();
        // 读取对应key的value值，在拦截器中用uri做key，次数做value存到Redis中了
        String s1 = opsForValue.get("1");
        String s2 = opsForValue.get("2");
        String s3 = opsForValue.get("3");
        String s4 = opsForValue.get("4");

        return s1 + s2 + s3 + s4;
    }

}
```

![image-20220802124157172](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220802124157172.png)



# 十、Redis6 的事务操作

## 一、事务的定义

Redis事务是一个单独的隔离操作：事务中的所有命令都会序列化、按顺序地执行。事务在执行的过程中，不会被其他客户端发送来的命令请求所打断。

Redis事务的主要作用就是串联多个命令防止别的命令插队。

**Multi、Exec、discard**

从输入Multi命令开始，输入的命令都会依次进入命令队列中，但不会执行，直到输入Exec后，Redis会将之前的命令队列中的命令依次执行。

组队的过程中可以通过discard来放弃组队。  

![image-20220802161620258](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220802161620258.png)

<img src="https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220802161649399.png" alt="image-20220802161649399" style="zoom:33%;" />

若组队阶段，提交失败，则所有指令都不会执行【就是编译阶段出错，全停】

<img src="https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220802161750040.png" alt="image-20220802161750040" style="zoom:50%;" />

若组队成功，提交后有错误，则没错误的指令正常运行【运行阶段，有错的指令报错，没错的指令执行，不会有回滚，也不会全停】

<img src="https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220802161921027.png" alt="image-20220802161921027" style="zoom:50%;" />

## 二、事务的错误处理

组队中某个命令出现了报告错误，执行时整个的所有队列都会被取消。

![image-20220802161953344](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220802161953344.png)

如果执行阶段某个命令报出了错误，则只有报错的命令不会被执行，而其他的命令都会执行，不会回滚。

![image-20220802162002479](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220802162002479.png)

## 三、事务冲突之----悲观锁、乐观锁

**例子**

一个请求想给金额减8000

一个请求想给金额减5000

一个请求想给金额减1000

![image-20220802162131013](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220802162131013.png)

**悲观锁(Pessimistic Lock)**, 顾名思义，就是很悲观，每次去拿数据的时候都认为别人会修改，所以每次在拿数据的时候都会上锁，这样别人想拿这个数据就会block直到它拿到锁。**传统的关系型数据库里边就用到了很多这种锁机制**，比如**行锁**，**表锁**等，**读锁**，**写锁**等，都是在做操作之前先上锁。

![image-20220802162521362](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220802162521362.png)

**乐观锁(Optimistic Lock)** ，顾名思义，就是很乐观，每次去拿数据的时候都认为别人不会修改，所以不会上锁，但是在更新的时候会判断一下在此期间别人有没有去更新这个数据，可以使用<font color="red">版本号</font>等机制。**乐观锁适用于多读的应用类型，这样可以提高吞吐量**。<font color="red">Redis就是利用这种check-and-set机制实现事务的。</font>

![image-20220802162654455](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220802162654455.png)

## 四、开启锁监控

```watch key[key....]```

watch可以监控多个key

在执行multi之前，先执行watch key1 [key2],可以监视一个(或多个) key ，如果在事务**执行之前这个(或这些) key 被其他命令所改动，那么事务将被打断。**

![image-20220802164131841](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220802164131841.png)

## 五、关闭锁监控

**unwatch**

取消 WATCH 命令对所有 key 的监视。

如果在执行 WATCH 命令之后，EXEC 命令或DISCARD 命令先被执行了的话，那么就不需要再执行UNWATCH 了。



## 六、Redis事务的三大特性

Redis的事务，就是一个指令队列。

- 把要执行的指令按顺序入队queue，如果不执行就discard原地散伙

- 执行的话exec就指令出队，按顺序执行，有报错的也不影响后边指令继续出队。

- 但是如果在入队的时候指令就报错了，那最后exec就不会执行任何指令。

<font color="red">单独的隔离操作 </font>

事务中的所有命令都会序列化、按顺序地执行。事务在执行的过程中，不会被其他客户端发送来的命令请求所打断。 

<font color="red">没有隔离级别的概念 </font>

队列中的命令没有提交之前都不会实际被执行，因为事务提交前任何指令都不会被实际执行

<font color="red">不保证原子性 </font>

事务中如果有一条命令执行失败，其后的命令仍然会被执行，没有回滚 

# 十一、Redis事务—秒杀案例

## 1、解决计数器和人员记录的事务操作

![image-20220803170743871](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220803170743871.png)

## 2、Redis 事务--秒杀并发模拟

### 1、安装ab模拟测试工具

CentOS 安装指令

```bash
yum install httpd-tools
```

M1芯片要改镜像源，直接将目前CentOS中```etc/yum.repos.d```文件夹中文件复制过去，然后运行

```bash
# 清理缓存
yum clean all
# 重新生成缓存
yum makecache
```

即可。

### 2、开始测试

可以创建一个文件，用来存储要提交的信息

如：创建postfile 文件，用来存储post请求的参数

<img src="https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220803171409606.png" alt="image-20220803171409606" style="zoom:50%;" />

#### 测试指令

- ```bash
  ab -n 2000 -c 200 -p ~/postfile -T application/x-www-form-urlencoded http://192.168.31.123:8080/doseckill
  
  ab -n 2000 -c 200 http://192.168.31.123:8080/doseckill
  http://192.168.31.123:8080/redisLock
  ```
  
- -n 2000：请求数量 2000个请求

- -c 200：并发请求数量  有200个并发请求

- -p ~/postfile：要提交的参数文件

- -T multipart/form-data：要提交的参数类型，

  - ![image-20220803171742579](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220803171742579.png)

- 最后加请求地址

造成超卖问题

![image-20220803171922752](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220803171922752.png)

### 3、通过乐观锁和事务，解决超卖问题

未解决，用jedis可以

```java
@Component
public class secKillService {

    @Autowired
    RedisTemplate<String,String> redisTemplate;

    private String msg;

    public String getMsg(){
        return msg;
    }

    public boolean doKill(String userId,String prodId){
        // 1、uid和prodid非空判断
        if(userId == null || prodId == null){
            msg = "用户未登录，用户名为空！";
            return false;
        }
        // 2、连接redis
//        JedisPool jedisPool = new JedisPool("192.168.31.190",6379);
//        Jedis jedis = jedisPool.getResource();
        Jedis jedis = new Jedis("192.168.31.190",6379);


        // 3、拼接key【针对成功后要入库操作】
        // prodid号商品秒杀成功的用户集合key   对应的value是set用户集合
        String uidSetKey = "sk:" + prodId + ":user";    // sk:秒杀，prodId，哪个产品，每个产品有一个set集合，用来存储购买他的用户清单
        // 秒杀成功的商品id  对应的value是库存信息
        String pidKey = "sk:" + prodId + ":qt";



//         监视库存
        redisTemplate.watch(pidKey);
//        jedis.watch(pidKey);
        // 4、获取库存，如果库存为null，表示秒杀还没开始

        String kcValue = redisTemplate.opsForValue().get(pidKey);
        if (kcValue == null) {
            msg = "秒杀还没有开始";
            return false;
        }
        // 5、判断用户是否重复秒杀，限购1件【查看产品的购买用户列表，看看有没有当前用户】
        Boolean isMember = redisTemplate.opsForSet().isMember(uidSetKey, userId);
        if (isMember){
            msg = "本产品每人限购1件，您已购买，请无重复下单！";
            return false;
        }
        // 6、判断商品数量，库存数量小于1，秒杀结束
        if(Integer.parseInt(kcValue) < 1){
            msg = "商品已经售罄，请等待下一轮购买";
            return false;
        }
        // 7、秒杀成功，库存-1，商品用户+1
//        redisTemplate.opsForValue().decrement(pidKey);
//        redisTemplate.opsForSet().add(uidSetKey,userId);
//        System.out.print(redisTemplate.opsForValue().get(pidKey));
//        msg = "您已经抢到商品，请尽快付款！";



//        execute a transaction
        List<Object> txResults = redisTemplate.execute(new SessionCallback<List<Object>>() {
            @Override
            public List<Object> execute(RedisOperations operations) throws DataAccessException {

                operations.multi();
                redisTemplate.opsForValue().decrement(pidKey);
                redisTemplate.opsForSet().add(uidSetKey, userId);

                // This will contain the results of all operations in the transaction
                return operations.exec();

            }
        });

        if (txResults == null || txResults.isEmpty()){
            msg = "秒杀结束了";
            return false;
        }else {
            System.out.print(Integer.parseInt(txResults.get(0).toString()) + 1);
            msg = "您已经抢到商品，请尽快付款！";
        }


        /*Jedis 操作事务*/
//        Transaction multi= jedis.multi();//开启事务
//        List<Object> exec = new ArrayList<>();
//        try{
//            multi.decr(pidKey);
//            multi.sadd(uidSetKey,userId);
//            //int i = 1/0;//代码抛出异常，执行失败,输出为null
//
//            exec = multi.exec();//执行事务
//        } catch (Exception e){
//            multi.discard();
//            System.out.println("-------------------取消事务");
//        } finally {
//            jedis.close();//关闭连接
//        }
//        if (exec == null || exec.isEmpty()){
//            msg = "秒杀结束了";
//            return false;
//        }else {
//            System.out.print(Integer.parseInt(exec.get(0).toString()) + 1);
//            msg = "您已经抢到商品，请尽快付款！";
//        }

        return true;

    }
}
```

### 4、通过Redis连接池，解决超时问题



### 5、通过LUA脚本，解决库存遗留问题

Lua 是一个小巧的[脚本语言](http://baike.baidu.com/item/脚本语言)，Lua脚本可以很容易的被C/C++ 代码调用，也可以反过来调用C/C++的函数，Lua并没有提供强大的库，一个完整的Lua解释器不过200k，所以Lua不适合作为开发独立应用程序的语言，而是作为嵌入式脚本语言。

很多应用程序、游戏使用LUA作为自己的嵌入式脚本语言，以此来实现可配置性、可扩展性。

这其中包括魔兽争霸地图、魔兽世界、博德之门、愤怒的小鸟等众多游戏插件或外挂。

https://www.w3cschool.cn/lua/

**LUA脚本在Redis中的优势**

将复杂的或者多步的redis操作，写为一个脚本，一次提交给redis执行，减少反复连接redis的次数。提升性能。

LUA脚本是类似redis事务，有一定的原子性，不会被其他命令插队，可以完成一些redis事务性的操作。

但是注意redis的lua脚本功能，只有在Redis 2.6以上的版本才可以使用。

利用lua脚本淘汰用户，解决超卖问题。

redis 2.6版本以后，通过lua脚本解决**争抢问题**，实际上是**redis 利用其单线程的特性，用任务队列的方式解决多任务并发问题**。

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps81.png)

#### 整合脚本

![image-20220804124900425](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220804124900425.png)

##### 1、编写脚本内容

脚本文件存放在和application.yaml同级目录下

```lua
local userid=KEYS[1];
local prodid=KEYS[2];
local qtkey='sk:'..prodid..":qt";
local usersKey='sk:'..prodid..":usr";
local userExists=redis.call("sismember",usersKey,userid); -- 查看已购用户id
-- 如果已购用户存在，则返回2，表示限购1件
if tonumber(userExists)==1 then
    return "2";
end
    local num= redis.call("get" ,qtkey);  -- 获取库存
    -- 库存小于等于0，返回0，表示卖光了，没库存了
    if tonumber(num)<=0 then
       return "0";
    else
    -- 有库存，那么执行
       redis.call("decr",qtkey);  -- 库存-1
       redis.call("sadd",usersKey,userid);  -- 已购用户入库
    end
        -- 返回1，表示抢购成功
        return "1";
```

##### 2、编写配置信息

```java
@Configuration
public class RedisConfig {
    @Bean
    public DefaultRedisScript<String> script(){
        DefaultRedisScript<String> redisScript = new DefaultRedisScript<>();
        // 脚本位置，和application.yaml同级目录
        redisScript.setLocation(new ClassPathResource("checkandset.lua"));
        // 脚本返回类型，可以自定义，Boolean也行，对应泛型里的都改了就行了
        redisScript.setResultType(String.class);
        return redisScript;
    }
}
```

##### 3、调用脚本

这里还不是很严谨，删除锁的 时候没有进行判断，可能会误删别人的锁

如果运行中出现异常，导致操作没完成锁就过期了，这时候别人获取了新锁，等你执行到删除锁操作时，删掉的就是别人的锁

```java
@Component
public class secKillService {
    // 注入Redis和lua脚本
    @Autowired
    RedisTemplate<String,String> redisTemplate;
    @Autowired
    RedisScript<String> script;
  
    private String msg;
    public String getMsg(){
        return msg;
    }

		// 此处运行脚本的同时，为Redis增加了锁，用一个key来做锁，有值就有人用，用完了删除。没值可以申请
    public boolean doSecKill(String uid,String prodid) throws IOException {
        String randValue = UUID.randomUUID().toString();// 生成一个随机数
        // 设置过期时间，放止应用在运行过程中抛出异常，导致锁无法正常释放
        // setIfAbsent,如果key不存在，就设置，和普通的set不一样，普通set存在就覆盖了
        Boolean lock = redisTemplate.opsForValue().setIfAbsent("lock", randValue,5, TimeUnit.SECONDS);
        if (lock){
            List<String> list = new ArrayList<>();
            list.add(uid);
            list.add(prodid);
            String result = redisTemplate.execute(script,list);
          
            if ("1".equals(result)) {
                msg = "您已经抢到商品，请尽快付款！";
                // 返回之前，释放锁
                redisTemplate.delete("lock");
                return true;
            }else if("0".equals(result))  { msg = "商品已经售罄，请等待下一轮购买";
            }else if("2".equals(result))  { msg = "本产品每人限购1件，您已购买，请无重复下单！";
            }else{ msg = "网络繁忙，请刷新后重试！";}
            
            // 没抢到，那也得释放锁
            redisTemplate.delete("lock");
            return false;

        }else{
            System.out.println("有线程在使用，请稍后操作！");
        }
        return true;
    }
}

```

![image-20220804125752009](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220804125752009.png)

# 十一、Redis6 持久化之RDB

http://www.redis.io

Redis 提供了2个不同形式的持久化方式。

- RDB（Redis DataBase）

- AOF（Append Of File）



## **1、RDB是什么**

在指定的时间间隔内将内存中的数据集快照写入磁盘， 也就是Snapshot快照，它恢复时是将快照文件直接读到内存里

**备份是如何执行的**

Redis会单独创建（fork）一个子进程来进行持久化，会先将数据写入到 一个临时文件中，待持久化过程都结束了，再用这个临时文件替换上次持久化好的文件。 整个过程中，主进程是不进行任何IO操作的，这就确保了极高的性能 如果需要进行大规模数据的恢复，且对于数据恢复的完整性不是非常敏感，那RDB方式要比AOF方式更加的高效。**<font color="red">RDB的缺点是</font>**最后一次持久化后的数据可能丢失。

**Fork**

Fork的作用是复制一个与当前进程一样的进程。新进程的所有数据（变量、环境变量、程序计数器等） 数值都和原进程一致，但是是一个全新的进程，并作为原进程的子进程

在Linux程序中，fork()会产生一个和父进程完全相同的子进程，但子进程在此后多会exec系统调用，出于效率考虑，Linux中引入了“**写时复制技术**”

**一般情况父进程和子进程会共用同一段物理内存**，只有进程空间的各段的内容要发生变化时，才会将父进程的内容复制一份给子进程。

 

## **2、RDB持久化流程**

 

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps82.jpg) 

**dump.rdb文件**

在redis.conf中配置文件名称，默认为dump.rdb

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps83.jpg) 

**配置位置**

rdb文件的保存路径，也可以修改。默认为Redis启动时命令行所在的目录下

dir "/myredis/"

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps84.jpg) 

**如何触发RDB快照；保持策略**

## 3、**配置文件中默认的快照配置**

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps85.jpg) 

- **命令save VS bgsave**

  - **save ：**save时只管保存，其它不管，全部阻塞。手动保存。不建议。

  - **bgsave：**Redis会在后台异步进行快照操作， 快照同时还可以响应客户端请求。

  - 可以通过lastsave 命令获取最后一次成功执行快照的时间

- **flushall命令**
  - 执行flushall命令，也会产生dump.rdb文件，但里面是空的，无意义

**###SNAPSHOTTING快照###**

- Save

  - 格式：save 秒钟 写操作次数

  - RDB是整个内存的压缩过的Snapshot，RDB的数据结构，可以配置复合的快照触发条件，

  - **默认是1分钟内改了1万次，或5分钟内改了10次，或15分钟内改了1次。**
  - 禁用
  - 不设置save指令，或者给save传入空字符串

- **stop-writes-on-bgsave-error**

  - ![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps86.jpg) 

  - 当Redis无法写入磁盘的话，直接关掉Redis的写操作。推荐yes.

- **rdbcompression压缩文件**

  - ![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps87.jpg) 

  - 对于存储到磁盘中的快照，可以设置是否进行压缩存储。如果是的话，redis会采用LZF算法进行压缩。

  - 如果你不想消耗CPU来进行压缩的话，可以设置为关闭此功能。推荐yes.

- **rdbchecksum检查完整性**

  - ![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps88.jpg) 

  - 在存储快照后，还可以让redis使用CRC64算法来进行数据校验，

  - 但是这样做会增加大约10%的性能消耗，如果希望获取到最大的性能提升，可以关闭此功能

  - 推荐yes.

- **rdb的备份**

  - 先通过config get dir  查询rdb文件的目录 

  - 将*.rdb的文件拷贝到别的地方

- **rdb的恢复**
  - 关闭Redis
  - 先把备份的文件拷贝到工作目录下 cp dump2.rdb dump.rdb
  - 启动Redis, 备份数据会直接加载

## 4、**优势**

- 适合大规模的数据恢复
- 对数据完整性和一致性要求不高更适合使用
- 节省磁盘空间
- 恢复速度快

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps89.png) 

## **5、劣势**

Fork的时候，内存中的数据被克隆了一份，大致2倍的膨胀性需要考虑

虽然Redis在fork时使用了**写时拷贝技术**,但是如果数据庞大时还是比较消耗性能。

在备份周期在一定间隔时间做一次备份，所以如果Redis意外down掉的话，就会<font color="red">丢失最后一次快照后的所有修改。</font>

**如何停止**

动态停止RDB：redis-cli config set save ""#save后给空值，表示禁用保存策略

## **6、小总结**

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps90.png) 



# 十二、Redis6 持久化之AOF

**AOF（Append Only File）**

## **1、AOF是什么**

以**日志**的形式来记录每个写操作（增量保存），将Redis执行过的所有写指令记录下来( **读操作不记录 **)，  **只许追加文件但不可以改写文件 **，redis启动之初会读取该文件重新构建数据，换言之，redis 重启的话就根据日志文件的内容将写指令从前到后执行一次以完成数据的恢复工作

## **2、AOF持久化流程**

（1）客户端的请求写命令会被append追加到AOF缓冲区内；

（2）AOF缓冲区根据AOF持久化策略[always,everysec,no]将操作sync同步到磁盘的AOF文件中；

（3）AOF文件大小超过重写策略或手动重写时，会对AOF文件rewrite重写，压缩AOF文件容量；

（4）Redis服务重启时，会重新load加载AOF文件中的写操作达到数据恢复的目的；

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps91.jpg) 

 

**AOF默认不开启**

- 可以在redis.conf中配置文件名称，默认为 appendonly.aof
- AOF文件的保存路径，同RDB的路径一致。
- **AOF和RDB**同时开启，**redis**听谁的？
- AOF和RDB同时开启，系统默认取AOF的数据（数据不会存在丢失）

**AOF启动修复恢复**

- AOF的备份机制和性能虽然和RDB不同, 但是备份和恢复的操作同RDB一样，都是拷贝备份文件，需要恢复时再拷贝到Redis工作目录下，启动系统即加载。

- 正常恢复

- 修改默认的appendonly no，改为yes

- 将有数据的aof文件复制一份保存到对应目录(查看目录：config get dir)

- 恢复：重启redis然后重新加载

 

**异常恢复**

- 修改默认的appendonly no，改为yes

- 如遇到 **AOF文件损坏 **，通过/usr/local/bin/ **redis-check-aof--fix appendonly.aof **进行恢复

- 备份被写坏的AOF文件

- 恢复：重启redis，然后重新加载

**AOF同步频率设置**

- appendfsync always
  - 始终同步，每次Redis的写入都会立刻记入日志；性能较差但数据完整性比较好

- appendfsync everysec
  - 每秒同步，每秒记入日志一次，如果宕机，本秒的数据可能丢失。
- appendfsync no
  - redis不主动进行同步，把同步时机交给操作系统。



## **3、Rewrite压缩**

AOF采用文件追加方式，文件会越来越大为避免出现此种情况，新增了重写机制, 当AOF文件的大小超过所设定的阈值时，Redis就会启动AOF文件的内容压缩， 只保留可以恢复数据的最小指令集.可以使用命令bgrewriteaof

**重写原理，如何实现重写**

AOF文件持续增长而过大时，会fork出一条新进程来将文件重写(也是先写临时文件最后再rename)，redis4.0版本后的重写，是指上就是把rdb 的快照，以二级制的形式附在新的aof头部，作为已有的历史数据，替换掉原来的流水账操作。

```no-appendfsync-on-rewrite：```

- 如果 no-appendfsync-on-rewrite=yes ,不写入aof文件只写入缓存，用户请求不会阻塞，但是在这段时间如果宕机会丢失这段时间的缓存数据。（降低数据安全性，提高性能）

- 如果 no-appendfsync-on-rewrite=no,  还是会把数据往磁盘里刷，但是遇到重写操作，可能会发生阻塞。（数据安全，但是性能降低）

**触发机制，何时重写**

Redis会记录上次重写时的AOF大小，默认配置是当AOF文件大小是上次rewrite后大小的一倍且文件大于64M时触发

重写虽然可以节约大量磁盘空间，减少恢复时间。但是每次重写还是有一定的负担的，因此设定Redis要满足一定条件才会进行重写。 

- auto-aof-rewrite-percentage：设置重写的基准值，文件达到100%时开始重写（文件是原来重写后文件的2倍时触发）
- auto-aof-rewrite-min-size：设置重写的基准值，最小文件64MB。达到这个值开始重写。

例如：文件达到70MB开始重写，降到50MB，下次什么时候开始重写？100MB

系统载入时或者上次重写完毕时，Redis会记录此时AOF大小，设为base_size,

如果Redis的AOF当前大小>= base_size +base_size*100% (默认)且当前大小>=64mb(默认)的情况下，Redis会对AOF进行重写。 

**重写流程**

（1）bgrewriteaof触发重写，判断是否当前有bgsave或bgrewriteaof在运行，如果有，则等待该命令结束后再继续执行。

（2）主进程fork出子进程执行重写操作，保证主进程不会阻塞。

（3）子进程遍历redis内存中数据到临时文件，客户端的写请求同时写入aof_buf缓冲区和aof_rewrite_buf重写缓冲区保证原AOF文件完整以及新AOF文件生成期间的新的数据修改动作不会丢失。

（4）1).子进程写完新的AOF文件后，向主进程发信号，父进程更新统计信息。2).主进程把aof_rewrite_buf中的数据写入到新的AOF文件。

（5）使用新的AOF文件覆盖旧的AOF文件，完成AOF重写。

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps92.jpg) 

 

## 4、优势

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps93.png) 

- 备份机制更稳健，丢失数据概率更低。
- 可读的日志文本，通过操作AOF稳健，可以处理误操作。

## 5、劣势

- 比起RDB占用更多的磁盘空间。
- 恢复备份速度要慢。
- 每次读写都同步的话，有一定的性能压力。
- 存在个别Bug，造成恢复不能。

##  6、小总结

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps94.png) 

**总结(Which one)用哪个好**

官方推荐两个都启用。

如果对数据不敏感，可以选单独用RDB。

不建议单独用 AOF，因为可能会出现Bug。

如果只是做纯内存缓存，可以都不用。

**官网建议** 

RDB持久化方式能够在指定的时间间隔能对你的数据进行快照存储

AOF持久化方式记录每次对服务器写的操作,当服务器重启的时候会重新执行这些命令来恢复原始的数据,AOF命令以redis协议追加保存每次写的操作到文件末尾. 

Redis还能对AOF文件进行后台重写,使得AOF文件的体积不至于过大

只做缓存：如果你只希望你的数据在服务器运行的时候存在,你也可以不使用任何持久化方式.

同时开启两种持久化方式

在这种情况下,当redis重启的时候会优先载入AOF文件来恢复原始的数据, 因为在通常情况下AOF文件保存的数据集要比RDB文件保存的数据集要完整.

RDB的数据不实时，同时使用两者时服务器重启也只会找AOF文件。那要不要只使用AOF呢？ 

建议不要，因为RDB更适合用于备份数据库(AOF在不断变化不好备份)， 快速重启，而且不会有AOF可能潜在的bug，留着作为一个万一的手段。

性能建议

因为RDB文件只用作后备用途，建议只在Slave上持久化RDB文件，而且只要15分钟备份一次就够了，只保留save 900 1这条规则。 如果使用AOF，好处是在最恶劣情况下也只会丢失不超过两秒数据，启动脚本较简单只load自己的AOF文件就可以了。代价,一是带来了持续的IO，二是AOF rewrite的最后将rewrite过程中产生的新数据写到新文件造成的阻塞几乎是不可避免的。只要硬盘许可，应该尽量减少AOF rewrite的频率，AOF重写的基础大小默认值64M太小了，可以设到5G以上。默认超过原大小100%大小时重写可以改到适当的数值。



# 十三、Redis6 的主从复制

## 1、简介

服务器集群，多个服务器组合到一起，分主服务器和从服务器

- <font color="red">主服务器【master】</font>：读写权限，完整的服务器功能
  - 主要是写操作
- <font color="red">从服务器【slaver】</font>：读权限，复制主服务器的内容
  - 提供读操作，实现读写分离，缓解服务器压力
- <font color="red">主要优势</font>：
  - 读写分离，性能扩展
  - 容灾快速恢复
- ![image-20220804165918931](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220804165918931.png)

**1、Redis复制原理：**

![image-20220804185000615](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220804185000615.png)

- Slave启动成功连接到master后会发送一个sync命令
- Master接到命令启动后台的存盘进程，同时收集所有接收到的用于修改数据集命令， 在后台进程执行完毕之后，master将传送整个数据文件到slave,以完成一次完全同步
- 全量复制：而slave服务在接收到数据库文件数据后，将其存盘并加载到内存中。
- 增量复制：Master继续将新的所有收集到的修改命令依次传给slave,完成同步
- 但是只要是重新连接master,一次完全同步（全量复制)将被自动执行



**2、MySQL主从复制的原理**

![img](https://pics7.baidu.com/feed/908fa0ec08fa513d164b929b50889cfdb0fbd9fa.jpeg?token=fbd31ddde4a27c833a62fca0c97d5f9f)

主库将变更写入binlog日志，然后从库连接到主库之后，从库有一个 IO 线程，将主库的 binlog 日志拷贝到自己本地，写入一个 relay中继日志(relay log)中。接着从库中有一个SQL线程会从中继日志读取binlog，然后执行binlog日志中的内容，也就是在自己本地再次执行一遍SQL语句，从而使从服务器和主服务器的数据保持一致。

## 2、手动搭建---一主二从

多个服务器最好，目前只有一个系统，可以设定不一样的端口号，实现模拟服务器的效果。

多台服务器启动以后，不需要对主服务器进行任何设置

在**从服务器**输入命令，实现认主操作

- ```bash
   # slaveof 主服务器地址 主服务器端口
   slaveof 127.0.0.1 6379
  ```

查看服务器状态指令：

- ```bash
  info replication
  ```

### 1、创建配置文件

搭建服务器，只需要将配置文件创建多份即可，启动时用不一样的配置文件启动，就会有多个服务器的效果

每个配置文件需要修改内容如下

```bash
pidfile /var/run/redis_6388.pid
port 6388   
dbfilename dump6388.rdb
```

创建一个文件夹

```bash
# 创建文件夹
mkdir /myredis
cd /myredis

# 从原位置，拷贝出来一份配置文件
cp /opt/redis-7.0.4/redis.conf /myredis

# 创建新的文件，这里不采用复制的方式，使用【引用】
vi redis6388.conf
ls
#  redis.conf  reids6388.conf

# 再拷贝一份，做3个服务器
cp redis6388.conf redis6399.conf

# 修改配置文件内容【i插入，esc  :wq! 退出并保存】
vim redis6399.conf
```

文件内容：

- redis6399.conf

  - ```bash
    # 导入原配置文件，就不用完整复制了，导过来然后增加自己要修改的部分即可
    include /myredis/redis.conf
    # 插入要更新的部分内容
    pidfile /var/run/redis_6399.pid
    port 6399
    dbfilename dump6399.rdb
    
    ```
    
  - 



### 2、启动服务器

```bash
# 到安装目录
cd /usr/local/bin

# 启动服务器，根据自己写到配置文件
redis-server /myredis/redis.conf
redis-server /myredis/redis6388.conf
redis-server /myredis/redis6399.conf

# 查看服务器进程
ps -ef |grep redis
```

![image-20220804175130508](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220804175130508.png)

### 3、连接服务器

打开三个shell，分别连接不同的端口

```bash
# 到安装目录
cd /usr/local/bin

# 根据端口启动客户端
redis-cli -p 6388
```

![image-20220804175530170](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220804175530170.png)

### 4、认主--查看状态

原则：配从不配主



查看状态：```info replication```

- 默认都是master主服务器

- ![image-20220804175840878](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220804175840878.png)

认主:```slaveof 127.0.0.1 6379```

再次查看状态

![image-20220804180227294](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220804180227294.png)

### 5、注意

1、在主机上写，在从机上可以读取数据

2、从服务器没有写权限

- ![image-20220804180449738](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220804180449738.png)

3、主机挂掉，重启就行，一切如初

4、从机重启需重设：slaveof 127.0.0.1 6379

- 从机重启后，默认自己是老大，要让他认主。认主时会一次性复制主服务器所有内容， 不会因为他重启或者宕机丢失数据的。

- 可以将配置增加到文件中。永久生效。

5、薪火相传

- 可以无限套娃，从服务器，也能做其他服务器的主服务器
- 上一个Slave可以是下一个slave的Master，Slave同样可以接收其他 slaves的连接和同步请求，那么该slave作为了链条中下一个的master, 可以有效减轻master的写压力,去中心化降低风险。

6、反客为主

- 主服务器挂掉以后，从服务器可以升为主服务器

  - ```bash
    # 执行下面命令，提升从服务器 称为主服务器【可以通过哨兵自动提升】
    slaveof  no one
    ```

7、复制延迟

- 由于所有的写操作都是先在Master上操作，然后同步更新到Slave上，所以从Master同步到Slave机器有一定的延迟，当系统很繁忙的时候，延迟问题会更加严重，Slave机器数量的增加也会使这个问题更加严重。

## 3、哨兵模式

反客为主的自动版，能够后台监控主机是否故障，如果故障了根据投票数自动将从库转换为主库，不用人工执行切换主服务器的操作

### **1、创建哨兵**

自定义sentinel.conf文件，内容为

```bash
sentinel monitor mymaster 127.0.0.1 6379 1
# 其中mymaster为监控对象起的服务器名称,
		# 在java中，只要这个名字就行，不用管是不是切换了服务器，只要我拿到这个名字，就只当前的主服务器
# 1 为至少有多少个哨兵同意迁移的数量。 
```

### 2、启动哨兵

```bash
cd /usr/local/bin
# 使用自己写到配置文件，因为里面指定了监控对象
redis-sentinel  /myredis/sentinel.conf 

# redis做压测可以用自带的redis-benchmark工具
```

### 3、哨兵的抉择

哨兵如何选择哪台从服务器作为主服务呢？？

按如下顺序筛选：

1、选择优先级靠前的

- 优先级：配置文件中的replica-priority 100属性，100为最大，0为用不切换为主

2、选择偏移量最大的

- 偏移量：获得原主机数据最安全的

3、选择runid最小的从服务器

- runid：每个redis实例启动后都会随机生成一个40位的runid



## 4、故障恢复

<font color="red">主服务器宕机后，会推选出新的主服务器，当原主服务器恢复正常以后，只能作为从服务器加入集群</font>

![image-20220805081759310](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220805081759310.png)

Java代码

```java
private static JedisSentinelPool jedisSentinelPool=null;

public static  Jedis getJedisFromSentinel(){
			if(jedisSentinelPool==null){
            Set<String> sentinelSet=new HashSet<>();
            sentinelSet.add("192.168.11.103:26379");

            JedisPoolConfig jedisPoolConfig =new JedisPoolConfig();
            jedisPoolConfig.setMaxTotal(10); //最大可用连接数
            jedisPoolConfig.setMaxIdle(5); //最大闲置连接数
            jedisPoolConfig.setMinIdle(5); //最小闲置连接数
            jedisPoolConfig.setBlockWhenExhausted(true); //连接耗尽是否等待
            jedisPoolConfig.setMaxWaitMillis(2000); //等待时间
            jedisPoolConfig.setTestOnBorrow(true); //取连接的时候进行一下测试 ping pong

            jedisSentinelPool=new JedisSentinelPool("mymaster",sentinelSet,jedisPoolConfig);
            return jedisSentinelPool.getResource();
      }else{
        		return jedisSentinelPool.getResource();
      }
}
```



# 十四、Redis6 集群

## 1、简介

- 容量不够，redis如何进行扩容？
- 并发写操作， redis如何分摊？
- 另外，主从模式，薪火相传模式，主机宕机，导致ip地址发生变化，应用程序中配置需要修改对应的主机地址、端口等信息。

之前通过代理主机来解决，但是redis3.0中提供了解决方案。就是<font color="red">无中心化集群配置</font>。

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA77-h57696b6Z,size_20,color_FFFFFF,t_70,g_se,x_16.png)

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA77-h57696b6Z,size_20,color_FFFFFF,t_70,g_se,x_16-20220805111540767.png)



- Redis 集群实现了对Redis的水平扩容，即启动**N**个redis节点，将整个数据库分布存储在这N个节点中，<font color="red">每个节点存储总数据的</font><font color="green">**1/N**</font>。
- Redis 集群通过分区（partition）来提供一定程度的可用性（availability）： 即使集群中有一部分节点失效或者无法进行通讯， 集群也可以继续处理命令请求。

## 2、创建集群

### 1、删除持久化数据

将rdb,aof文件都删除掉。

<img src="https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220805095430008.png" alt="image-20220805095430008" style="zoom:50%;" />

### 2、制作6个实例

此处使用不同端口表示不同的服务器6379,6389,6399,6378,6388,6398
**1、配置基本信息**

- 开启daemonize yes
- Pid文件名字
- 指定端口
- Log文件名字
- Dump.rdb名字
- Appendonly 关掉或者换名字

**2、redis cluster配置修改**

- cluster-enabled yes    打开集群模式
- cluster-config-file nodes-6379.conf  设定节点配置文件名
- cluster-node-timeout 15000   设定节点失联时间，超过该时间（毫秒），集群自动进行主从切换。

- ```bash
  # 导入原配置文件信息，要写全路径
  include /myredis/redis.conf
  # 添加其他配置
  port 6379
  pidfile "/var/run/redis_6379.pid"
  dbfilename "dump6379.rdb"
  # 指出集群文件夹
  dir "/myredis/redis_cluster"
  logfile "/myredis/redis_cluster/redis_err_6379.log"
  # 打开集群模式
  cluster-enabled yes
  cluster-config-file nodes-6379.conf
  cluster-node-timeout 15000
  ```

- 修改其他5个文件内容，可以使用```%/6379/6380```实现替换操作，替换6379为6380

## 3、启动集群

### **1、启动6个Redis，使用对应的配置文件**

- <img src="https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220805100606691.png" alt="image-20220805100606691" style="zoom:75%;" />

### **2、将实例合并为一个集群**

组合之前，请确保所有redis实例启动后，nodes-xxxx.conf文件都生成正常。

1、到安装目录下【就是redis压缩包解压位置】

```bash
# 到安装目录，因为只有安装目录才有集群的操作指令
cd  /opt/redis-7.0.4/src

# 将多个实例合并
redis-cli --cluster create --cluster-replicas 1 192.168.11.101:6379 192.168.11.101:6380 192.168.11.101:6381 192.168.11.101:6389 192.168.11.101:6390 192.168.11.101:6391
```

此处不要用127.0.0.1， 用真实IP地址

- --replicas 1 ：一台主机配一台从机模式，正好三组。

## 4、操作集群

### 1、普通方式登录

可能直接进入读主机，存储数据时，会出现MOVED重定向操作。所以，应该以集群方式登录。

```bash
redis-cli -p 6379
```

<img src="https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220805101219196.png" alt="image-20220805101219196" style="zoom:75%;" />

### 2、采用集群策略连接

- -c ：设置数据会自动切换到相应的写主机

```bash
redis-cli -c -p 6379
```

<img src="https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220805101359266.png" alt="image-20220805101359266" style="zoom:75%;" />

### 3、查看集群信息

```bash
cluster nodes
```

![image-20220805101453545](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220805101453545.png)

### 4、redis cluster 如何分配这六个节点?

一个集群至少要有三个主节点。

选项 --cluster-replicas 1 表示我们希望为集群中的每个主节点创建一个从节点。

分配原则尽量保证每个主数据库运行在不同的IP地址，每个从库和主库不在一个IP地址上。

![image-20220805111629040](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220805111629040.png)

### 5、什么是slots【插槽】



![image-20220805102038087](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220805102038087.png)
一个 Redis 集群包含 16384 个插槽（hash slot）， 数据库中的每个键都属于这 16384 个插槽的其中一个， 
集群使用公式 CRC16(key) % 16384 来计算键 key 属于哪个槽， 其中 CRC16(key) 语句用于计算键 key 的 CRC16 校验和 。
集群中的每个节点负责处理一部分插槽。 

举个例子， 如果一个集群可以有主节点， 其中：

- 节点 A 负责处理 0 号至 5460 号插槽。
- 节点 B 负责处理 5461 号至 10922 号插槽。
- 节点 C 负责处理 10923 号至 16383 号插槽。

### 6、在集群中录入值

**因为多个主服务器分了不同的插槽，默认登录方式插入属于别的服务器的key，就会报错**

**使用-c的方式登录，不管插入的key是不是属于当前服务器，都能成功，他会自动分配服务器**



在redis-cli每次录入、查询键值，redis都会计算出该key应该送往的插槽，如果不是该客户端对应服务器的插槽，redis会报错，并告知应前往的redis实例地址和端口。

**redis-cli客户端提供了 –c 参数实现自动重定向。**
如 ```redis-cli  -c –p 6379 ```登入后，再录入、查询键值对可以自动重定向。

==注意：==

不在一个slot下的键值，是不能使用mget,mset等多键操作。

![image-20220805102305040](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220805102305040.png)

可以通过{}来定义组的概念，从而使key中{}内相同内容的键值对放到一个slot中去。

![image-20220805102322537](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220805102322537.png)

### 7、查询集群中的值

```bash
cluster keyslot cust             #   返回cust在槽中的位置
cluster countkeysinslot 4847		 #   返回4847槽中的值的个数
cluster getkeysinslot 4847 10		 #   返回4847槽中的10个值
```

![image-20220805104904419](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220805104904419.png)

## 5、故障恢复

如果主节点下线？从节点能否自动升为主节点？注意：15秒超时

![image-20220805105051589](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220805105051589.png)

主节点恢复后，主从关系会如何？**主节点回来变成从机。**

![image-20220805105100650](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220805105100650.png)

如果所有某一段插槽的主从节点都宕掉，redis服务是否还能继续?

- 如果某一段插槽的主从都挂掉，而cluster-require-full-coverage 为yes ，那么 ，整个集群都挂掉
- 如果某一段插槽的主从都挂掉，而cluster-require-full-coverage 为no ，那么，该插槽数据全都不能使用，也无法存储，但是其他服务器的插槽还能用
  - 例如管理0-999插槽的服务器A挂掉了，但是1000-1999的插槽还能用
- redis.conf中的参数  cluster-require-full-coverage

## 6、集群的Jedis开发

- 即使连接的不是主机，**集群会自动切换主机存储**。主机写，从机读。
- **无中心化主从集群**。无论从哪台主机写的数据，其他主机上都能读到数据。

```c
@Test
    public void JedisClusterTest(){
        Set<HostAndPort> set =new HashSet<HostAndPort>();
        set.add(new HostAndPort("192.168.126.129",6379));
        JedisCluster jedisCluster=new JedisCluster(set);
        jedisCluster.set("k2", "v2");
        System.out.println(jedisCluster.get("k2"));
    }
12345678
```

## 7、集群的优势

- 实现扩容
- 分摊压力
- 无中心配置相对简单

## 8、集群的不足

- 多键操作是不被支持的
- 多键的Redis事务是不被支持的。lua脚本不被支持
- 由于集群方案出现较晚，很多公司已经采用了其他的集群方案，而代理或者客户端分片的方案想要迁移至redis cluster，需要整体迁移而不是逐步过渡，复杂度较大。

# 十五、==Redis6 应用问题解决==

##  **1、缓存穿透**

###  **1、问题描述**

key对应的数据在数据源并不存在，每次针对此key的请求从缓存获取不到，请求都会压到数据源，从而可能压垮数据源。比如用一个不存在的用户id获取用户信息，不论缓存还是数据库都没有，若黑客利用此漏洞进行攻击可能压垮数据库。

![image-20220805120524707](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220805120524707.png)



### **2、解决方案**

一个一定不存在缓存及查询不到的数据，由于缓存是不命中时被动写的，并且出于容错考虑，如果从存储层查不到数据则不写入缓存，这将导致这个不存在的数据每次请求都要到存储层去查询，失去了缓存的意义。

（1）**对空值缓存：**如果一个查询返回的数据为空（不管是数据是否不存在），我们仍然把这个空结果（null）进行缓存，设置空结果的过期时间会很短，最长不超过五分钟

（2）**设置可访问的名单（白名单）：**

使用bitmaps类型定义一个可以访问的名单，名单id作为bitmaps的偏移量，每次访问和bitmap里面的id进行比较，如果访问id不在bitmaps里面，进行拦截，不允许访问。

（3）**采用布隆过滤器**：(布隆过滤器（Bloom Filter）是1970年由布隆提出的。它实际上是一个很长的二进制向量(位图)和一系列随机映射函数（哈希函数）。

布隆过滤器可以用于检索一个元素是否在一个集合中。它的优点是空间效率和查询时间都远远超过一般的算法，缺点是有一定的误识别率和删除困难。)

将所有可能存在的数据哈希到一个足够大的bitmaps中，一个一定不存在的数据会被这个bitmaps拦截掉，从而避免了对底层存储系统的查询压力。

（4）**进行实时监控：**当发现Redis的命中率开始急速降低，需要排查访问对象和访问的数据，和运维人员配合，可以设置黑名单限制服务



## **2、缓存击穿**

### **1、问题描述**

key对应的数据存在，但在redis中过期，此时若有大量并发请求过来，这些请求发现缓存过期一般都会从后端DB加载数据并回设到缓存，这个时候大并发的请求可能会瞬间把后端DB压垮。

![image-20220805120618437](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220805120618437.png)



### 2、**解决方案**

key可能会在某些时间点被超高并发地访问，是一种非常“热点”的数据。这个时候，需要考虑一个问题：缓存被“击穿”的问题。

解决问题：

1. **预先设置热门数据：**在redis高峰访问之前，把一些热门数据提前存入到redis里面，加大这些热门数据key的时长

2. **实时调整：**现场监控哪些数据热门，实时调整key的过期时长

3. **使用锁：**

   1. 就是在缓存失效的时候（判断拿出来的值为空），不是立即去load db。

   1. 先使用缓存工具的某些带成功操作返回值的操作（比如Redis的SETNX）去set一个mutex key

   1. 当操作返回成功时，再进行load db的操作，并回设缓存,最后删除mutex key；

   1. 当操作返回失败，证明有线程在load db，当前线程睡眠一段时间再重试整个get缓存的方法。



![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps100.jpg)



## **3、缓存雪崩**

### **1、问题描述 **

key对应的数据存在，但在redis中过期，此时若有大量并发请求过来，这些请求发现缓存过期一般都会从后端DB加载数据并回设到缓存，这个时候大并发的请求可能会瞬间把后端DB压垮。

缓存雪崩与缓存击穿的区别在于这里针对很多key缓存，前者则是某一个key



正常访问

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps101.jpg)

缓存失效瞬间

![image-20220805120704898](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220805120704898.png)



### **2、解决方案**

缓存失效时的雪崩效应对底层系统的冲击非常可怕！

解决方案：

（1）**构建多级缓存架构：**nginx缓存+ redis缓存+其他缓存（ehcache等）

（2）**使用锁或队列**：

- 用加锁或者队列的方式保证来保证不会有大量的线程对数据库一次性进行读写，从而避免失效时大量的并发请求落到底层存储系统上。不适用高并发情况

（3）**设置过期标志更新缓存：**

- 记录缓存数据是否过期（设置提前量），如果过期会触发通知另外的线程在后台去更新实际key的缓存。

（4）**将缓存失效时间分散开：**

- 比如我们可以在原有的失效时间基础上增加一个随机值，比如1-5分钟随机，这样每一个缓存的过期时间的重复率就会降低，就很难引发集体失效的事件。



## 4、分布式锁

### 1、问题描述

随着业务发展的需要，原单体单机部署的系统被演化成分布式集群系统后，由于分布式系统多线程、多进程并且分布在不同机器上，这将使原单机部署情况下的并发控制锁策略失效，单纯的Java API并不能提供分布式锁的能力。为了解决这个问题就需要一种跨JVM的互斥机制来控制共享资源的访问，这就是分布式锁要解决的问题！

**分布式锁主流的实现方案：**

1. 基于数据库实现分布式锁
2. 基于缓存（Redis等）
3. 基于Zookeeper

**每一种分布式锁解决方案都有各自的优缺点：**

1. 性能：redis最高
2. 可靠性：zookeeper最高
这里，我们就基于redis实现分布式锁。

### 2、业务逻辑

- A要执行操作
- 先设置锁
- 开始执行
- 删除锁

### 3、存在问题--优化

- 操作出现异常， 没有到释放锁环节，造成死锁

  - 解决方案：设置锁的过期时间，到时间自动释放

- 多个客户端同时获得锁

  - 解决方案：使用setnx，存在才可以设置

- 通过expire设置过期时间（缺乏原子性：如果在setnx和expire之间出现异常，锁也无法释放）

  - 解决方案：在setnx处直接设置，合并为一条语句

  - ```bash
    setnx key value EX 5
    
    EX second ：设置键的过期时间为 second 秒。 
    PX millisecond ：设置键的过期时间为 millisecond 毫秒。 
    NX ：只在键不存在时，才对键进行设置操作。 
    XX ：只在键已经存在时，才对键进行设置操作。
    ```

- 若因故操作没完成，但是锁过期了，等执行删除操作时，就会删了别人的锁
  - 解决方案：设置一个uuid，删除之前判断一下，是自己设置的锁就删除，否则就不用删除了，因为已经过期了
- 判断是不是自己的锁时，判断返回true，准备删除时，锁过期了，然后还是会把别人的锁删除【判断和删除不是原子操作】
  - 解决方案：通过LUA脚本，把判断和删除封装为一个原子操作

### 4、最终版本

#### 流程图：

- ![image-20220805180420388](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220805180420388.png)

#### 文件夹结构：

- 统一管理所有脚本，将所有LUA脚本放到static/redis/文件夹下
- 添加配置类
- 自动注入
  - 自动注入时同名方法，确保每个对应的名字完全匹配，否则就得需要使用name等方法做标注

![image-20220806094007990](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220806094007990.png)

#### Java代码：

**LUA脚本**

- 保证删除操作的原子性

- 这里就是一个判断删除操作，是自己设的锁，就删除，不是就证明释放了，不用删了

- ```lua
  if redis.call('get', KEYS[1]) == ARGV[1] then
      return redis.call('del', KEYS[1])
  else
      return 0
  end
  ```

**配置类**

- ```java
  @Configuration
  public class RedisConfig {
      // 这个是判断库存状况的LUA脚本
      @Bean()
      public DefaultRedisScript<String> script(){
          DefaultRedisScript<String> redisScript = new DefaultRedisScript<>();
          redisScript.setLocation(new ClassPathResource("static/redis/checkandset.lua"));
          redisScript.setResultType(String.class);
          return redisScript;
      }
  
      // 这个是删除锁操作的LUA脚本
      @Bean()
      public DefaultRedisScript<String> delScript(){
          DefaultRedisScript<String> redisScript = new DefaultRedisScript<>();
          // 脚本位置
          redisScript.setLocation(new ClassPathResource("static/redis/dellock.lua"));
          // 设置一下返回值类型 为Long
          // 因为删除判断的时候，返回的0,给其封装为数据类型。如果不封装那么默认返回String 类型，
          // 那么返回字符串与0 会有发生错误。
          redisScript.setResultType(String.class);
          return redisScript;
      }
  }
  
  ```

**调用**

- ```java
  @Component
  public class DistributeLockService {
  
      @Autowired
      RedisTemplate<String,String> redisTemplate;
  
      @Autowired
  //    @Qualifier(value = "delScript")
      RedisScript<String> delScript;
  
      public void testRedisLock() {
          //1 声明一个uuid ,将做为一个value 放入我们的key所对应的值中
          String uuid = UUID.randomUUID().toString();
          //2 定义一个锁：lua 脚本可以使用同一把锁，来实现删除！
          String skuId = "25"; // 访问skuId 为25号的商品
          String locKey = "lock:" + skuId; // 锁住的是每个商品的数据【不能所有商品全是一个锁，没必要，只要同一个商品互不干扰就行了】
  
          // 3 获取锁   过期时间3秒
          Boolean lock = redisTemplate.opsForValue().setIfAbsent(locKey, uuid, 3, TimeUnit.SECONDS);
  
          // 如果true，设置成功，获取到锁
          if (lock) {
              // 执行的业务逻辑开始
              // 获取缓存中的num 数据
              Object value = redisTemplate.opsForValue().get("num");
              // 如果是空直接返回
              if (StringUtils.isEmpty(value)) {return;}
              // 不是空 如果说在这出现了异常！ 那么delete 就删除失败！ 也就是说锁永远存在！
              int num = Integer.parseInt(value + "");
              // 使num 每次+1 放入缓存
              redisTemplate.opsForValue().set("num", String.valueOf(++num));
              /*使用lua脚本来锁*/
              redisTemplate.execute(delScript, Arrays.asList(locKey), uuid);
          } else {
              // 其他线程等待
              try {
                  // 睡眠
                  Thread.sleep(1000);
                  // 睡醒了之后，调用方法。
                  testRedisLock();
              } catch (InterruptedException e) {
                  e.printStackTrace();
              }
          }
      }
  }
  
  ```

  



# 十六、Redis6 新功能

## **1、简介**

Redis ACL是Access Control List（访问控制列表）的缩写，该功能允许根据可以执行的命令和可以访问的键来限制某些连接。

在Redis 5版本之前，Redis 安全规则只有密码控制 还有通过rename 来调整高危命令比如 flushdb ， KEYS* ，shutdown 等。Redis 6 则提供ACL的功能对用户进行更细粒度的权限控制 ：

（1）接入权限：用户名和密码 

（2）可以执行的命令 

（3）可以操作的 KEY

参考官网：https://redis.io/topics/acl

 

## **2、命令**

### 1、使用acl list命令展现用户权限列表

（1）数据说明

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps1.jpg) 

### 2、使用acl cat命令

（1）查看添加权限指令类别

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps2.jpg) 

（2）加参数类型名可以查看类型下具体命令

<img src="https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps3.jpg" alt="img" style="zoom:50%;" /> 

 

3、使用acl whoami命令查看当前用户

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps4.jpg) 

 

4、使用aclsetuser命令创建和编辑用户ACL

（1）ACL规则

下面是有效ACL规则的列表。某些规则只是用于激活或删除标志，或对用户ACL执行给定更改的单个单词。其他规则是字符前缀，它们与命令或类别名称、键模式等连接在一起。

![image-20220807124058770](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220807124058770.png)

（2）通过命令创建新用户默认权限

```bash
acl setuser user1
```



![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps5.jpg) 

在上面的示例中，我根本没有指定任何规则。如果用户不存在，这将使用just created的默认属性来创建用户。如果用户已经存在，则上面的命令将不执行任何操作。

 

（3）设置有用户名、密码、ACL权限、并启用的用户

```bash
acl setuser user2 on >password ~cached:* +get
```



![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps6.jpg) 

 

(4)切换用户，验证权限

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps7.jpg) 

 

## **3、IO多线程**

**简介**

Redis6终于支撑多线程了，告别单线程了吗？

IO多线程其实指***客户端交互部分***的***网络IO***交互处理模块***多线程***，而非***执行命令多线程***。```Redis6执行命令依然是单线程。```

 

***原理架构***

Redis 6 加入多线程,但跟 Memcached 这种从 IO处理到数据访问多线程的实现模式有些差异。Redis 的多线程部分只是用来处理网络数据的读写和协议解析，执行命令仍然是单线程。之所以这么设计是不想因为多线程而变得复杂，需要去控制 key、lua、事务，LPUSH/LPOP 等等的并发问题。整体的设计大体如下:

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps8.jpg) 

 

==另外==，多线程IO默认也是不开启的，需要再配置文件中配置

```bash
io-threads-do-reads  yes 

io-threads 4
```



 

## **4、工具支持 Cluster**

之前老版Redis想要搭集群需要单独安装ruby环境，Redis 5 将 redis-trib.rb 的功能集成到 redis-cli 。另外官方 redis-benchmark 工具开始支持 cluster 模式了，通过多线程的方式对多个分片进行压测。

![img](https://pledge99.oss-cn-beijing.aliyuncs.com/img/wps9.jpg) 

 

## 5、Redis6新功能还有

1、RESP3新的 Redis 通信协议：优化服务端与客户端之间通信

2、Client side caching客户端缓存：基于 RESP3 协议实现的客户端缓存功能。为了进一步提升缓存的性能，将客户端经常访问的数据cache到客户端。减少TCP网络交互。

3、Proxy集群代理模式：Proxy 功能，让 Cluster 拥有像单实例一样的接入方式，降低大家使用cluster的门槛。不过需要注意的是代理不改变 Cluster 的功能限制，==不支持的命令还是不会支持，比如跨 slot 的多Key操作。==

4、Modules API

Redis 6中模块API开发进展非常大，因为Redis Labs为了开发复杂的功能，从一开始就用上Redis模块。Redis可以变成一个框架，利用Modules来构建不同系统，而不需要从头开始写然后还要BSD许可。Redis一开始就是一个向编写各种系统开放的平台。









