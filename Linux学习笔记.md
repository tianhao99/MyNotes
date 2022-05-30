# Linux基础

## 1、网络连接的三种方式

​	![image-20220113014707128](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220113014707128.png)

![image-20220113014805760](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220113014805760.png)

### 1、桥接模式：

方式：主机和虚拟机共同使用同一个外网网段，虚拟机可以直接和外部网络进行连接。

缺点：每个虚拟机占一个IP，100人有100个虚拟机，就需要200个IP，容易造成IP冲突

### 2、NAT模式：

方式：主机和虚拟机使用同一个网段，并且网段和外网网段不同，连接外网时统一由另一个代理IP进行连接

### 3、主机模式：

方式：这是个独立的系统

## 2、虚拟机克隆

### 1、拷贝文件

直接拷贝虚拟机文件夹，然后用VMware导入

这个虚拟机文件使用任何虚拟机软件都可以打开，甚至拷贝给其他电脑也是完全能用的，里面账户密码设置等全部一致

![](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220113190348052.png)

![image-20220113190546869](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220113190546869.png)

### 2、使用VMware

使用VMware的克隆操作，注意此时必须关闭虚拟机

## 3、虚拟机快照

就是保存虚拟机状态的一个节点，作为恢复数据的节点，可以随意恢复，前进or后退

根据不同快照内容，会形成继承、并列等形式。

不建议大量拍摄快照，浪费空间



![image-20220113191744125](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220113191744125.png)

## 4、虚拟机的迁移和删除

因为虚拟系统的本质就是那个文件夹

- 迁移：直接拷贝剪切文件夹
- 删除：直接删除文件夹，或者现在虚拟机中移除，再去删除文件



## 5、Linux目录结构

**<font color="red">在Linux世界中，一切皆文件！！！</font>**

Linux的文件系统是**采用层级式的树状目录结构**，在此结构中的最上层是根目录“/”然后在此目录下再创建其他的目录



- ==/bin==  是Binary的缩写，这个目录存放这最经常使用的命令
  - /usr/bin、/usr/local/bin
- ==/sbin== s就是Super User的意思，这里存放的是系统管理员使用的系统管理程序
  - /usr/sbin、/usr/local/sbin
- ==/home==  存放普通用户的主目录，在Linux中每一个用户都拥有一个自己的目录，一般该目录名是以用户的账户号命名的
- ==/root==  该目录为系统管理员，也称作超级权限着的用户主目录
- ==/lib== 系统开机所需要最基本的动态连接共享库，其作用类似于Windows里的DLL文件。几乎所有的应用程序都需要用到这些共享库
- ==/lost+found== 这个目录一般情况下是空的，当系统非法关机后，这里就存放了一些文件
- ==/etc==  所有的系统管理所需要的配置文件和子目录，比如安装MySQL数据库 my.conf
- ==/usr==  这是一个非常重要的目录，用户的很多应用程序和文件都放在这个目录下，类似Windows下的program files目录
- ==/boot==   存放的是启动Linux时使用的一些核心文件，包括一些连接文件以及镜像文件
- ==/proc==  这个目录是一个虚拟的目录，它是系统内存的映射，访问这个目录来获取系统信息<font color="red">【勿动】</font>
- ==/srv==  service缩写，该目录存放一些服务启动之后需要提取的数据<font color="red">【勿动】</font>
- ==/sys==  这是Linux2.6内核一个很大的变化，该目录下安装了2.6内核汇总新出现的文件系统sysfs<font color="red">【勿动】</font>
- ==/tmp==  这个目录用来存放一些临时文件
- ==/dev==  类似于Windows的设备管理器，吧所有的硬件用文件的形式存储
- ==/media==  Linux系统会自动识别一些设备，如U盘、光驱等，当识别以后，Linux会把识别的设备挂载到这个目录下
- ==/mnt==  系统提供该目录是为了让用户临时挂载别的文件系统的，我们可以将外部的存储挂载在/mnt/上，然后进入该目录就可以查看里面的内容了。如共享文件目录
- ==/opt==  这是给主机额外安装软件所存放的目录，默认为空。约定大家把安装软件都放到这里
- ==/usr/local==  这是另一个给主机额外安装软件所安装的目录，一般是通过编译源码方式安装的程序
- ==/var==  这个目录中存放着不断扩充着的东西，习惯将经常被修改的目录放在这个目录下，包括各种日志文件
- ==/selinux==  是Security-Enhanced Linux缩写 SELinux是一种安全子系统，它能控制程序只能访问特定文件，有三种工作模式，可以自行设置



# Linux实操

## 1、远程登录Linux服务器

### 为什么需要远程登录Linux

- Linux服务器是开发小组共享
- 正式上线的项目是运行在公网
- 因此程序员需要远程登录到Linux进行项目管理或者开发
- 远程登录客户端主要有Xshell6，Xftp6等



## 2、vi和vim

### 基本介绍

Linux 系统会内置 vi 文本编辑器

Vim 具有程序编辑的能力，可以看做是vi的增强版本，可以主动的以字体颜色辨别语法的正确性，方便程序设计，代码补完、编译及错误跳转等方便编程的功能特别丰富，在程序员中被广泛使用。

### 常用的三种模式

- 正常模式
  - 以vim打开一个档案就直接进入一般模式了（这是默认的模式）。在这个模式中，可以使用「上下左右」按键来移动光标，可以使用「删除字符」或者「删除整行」来处理档案内容，也可以使用「复制、粘贴」来处理文件数据
- 插入模式
  - 按下i、I、o、O、a、A、r、R等任何一个字母之后，才会进入编辑模式，一般按 **i** 即可
- 命令行模式
  - 在这个模式中，可以提供相关指令，完成读取、存盘、替换、离开vim、显示行号等的动作则是在此模式中达成的

![IMG_5AD9BC2291A8-1](https://pledge99.oss-cn-beijing.aliyuncs.com/img/IMG_5AD9BC2291A8-1.jpeg)

### 快捷键

- yy：拷贝当前行
  - 9yy：拷贝当前行向下9行
  - p：粘贴
- dd：删除当前行
  - 9dd：删除当前行向下9行
- /关键字：在文件中查找某个单词
  - 回车：查找
  - n：查找下一个
- :set nu：设置文件的行号【:冒号，进入命令行模式，同:wq】
- :set nonu：取消文件的行号
- G：到达文件的最末行
- gg：到达文件的首行
- u：在文件中输入，然后撤销这个动作【一般模式下】
- 9shift+g：将光标移动到 9 行

## 	3、开机、重启

### 基本命令

- ```shutdown -h now```   立即关机
- ```shutdown -h 1```   “hello ，1分钟后执行关机操作”
- ```shutdown -r now```    立即重启计算机
- ```halt```    关机，作用和上面一样
- ```reboot```    立即重启计算机
- ```sync```   把内存的数据同步到磁盘
- 注意：
  - 1、不管是重启系统还是关闭系统，首先要运行sync命令，把内存中的数据写到磁盘中
  - 2、目前的shutdown、reboot、halt等命令均已经在关机前进行了sync

## 4、登录、注销

### 基本介绍

1、登录时尽量少用root账号登录，因为他是系统管理员，最大的权限，避免操作失误，可以利用普通用户登录，登陆以后再用```su-用户名``` 命令来切换成系统管理员的身份

2、在提示符下输入```logout```即可注销用户

注意：

- logout 注销指令在图形运行级别无效，在运行级别3下有效【带图形界面的注销用户操作无效】

![image-20220122233234821](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220122233234821.png)

## 5、用户管理

### 基本介绍

Linux系统是一个多用户多任务的操作系统，任何一个要使用资源的用户，都必须首先向系统管理员申请一个账号，然后以这个账号的身份进入系统。

### 添加用户

- 基本语法
  - ```useradd 用户名```
- 注意：
  - 当创建用户成功以后，会自动创建和用户同名的家目录
  - 也可以通过```useradd -d 指定目录 新用户名```，给创建的用户指定家目录

### 指定、修改密码

- 基本语法
  - ```passwd 用户名```

![image-20220124215537900](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220124215537900.png)

补充：```pwd```显示当前在那个目录

### 删除用户

- 基本语法
  - ```userdel 用户名```  删除用户，但是保留该用户的家目录
  - ```userdel -r 用户名```  删除用户和该用户的家目录【慎重】



### 查询用户信息

- 基本语法
  - ```id 用户名```

### 切换用户

在操作Linux时，如果当前用户的权限不够，可以通过```su - 用户名```的指令，切换到高权限用户，比如root

或者创建了一个新用户，然后切换过去

- 基本语法
  - ```su - 要切换的用户名```

- 补充
  - <font color="red">从权限高的用户切换到权限低的用户，不需要输入密码，反之需要</font>
  - 当需要返回原来的用户时，使用```exit/logout```指令

### 查看当前用户/登录用户

- 基本语法
  - ```whoami```或者```who am i/I``` 查询目前登录用户的信息
  - ![image-20220124221219669](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220124221219669.png)

### 用户组

- 介绍
  - 类似于角色，系统可以对有共性的多个用户进行统一的管理
- 新增组
  - 指令：```groupadd 组名```
- 删除组
  - 指令：```groupdel 组名```
- 增加用户时直接加上组
  - 指令：```useradd -g 用户组 用户名```
- 补充：如果创建用户时，没有指定组，系统会默认创建一个以用户名命名的新组，然后把这个用户放到组中
  - ![image-20220124222000613](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220124222000613.png)

```java
[root@CentOS7-01 home]# id tianhao
uid=1000(tianhao) gid=1000(tianhao) 组=1000(tianhao)

// 创建组
[root@CentOS7-01 home]# groupadd mingjiao

// 创建用户并添加到一个组
[root@CentOS7-01 home]# useradd -g mingjiao zhangwuji
  
// 查看用户信息
[root@CentOS7-01 home]# id zhangwuji
uid=1001(zhangwuji) gid=1001(mingjiao) 组=1001(mingjiao)
```

- 更改用户所在组
  - 指令：```usermod -g 目标组名称 移动用户名称``` 将某用户移动到某组

### 用户和组相关文件

- /etc/passwd 文件
  - 用户（user）的配置文件，记录用户的各种信息
  - 每行的含义：用户名：口令：用户标识号：组标识号：注释性描述：主目录：登录Shell
- /etc/shadow 文件
  - 口令的配置文件
  - 每行的含义：登录名：加密口令：最后一次修改时间：最小时间间隔：最大时间间隔：警告时间：不活动时间：失效时间：标志
- /etc/group 文件
  - 组（group）的配置文件，记录Linux包含的组的信息
  - 每行的含义：组名：口令：组标识号：组内用户列表

## 6、实用指令

### 运行级别

#### 1、运行级别介绍

- 0：关机
- 1：单用户【找回丢失密码】
- 2：多用户状态没有网络服务
- 3：多用户状态有网络服务
- 4：系统未使用保留给用户
- 5：图形界面
- 6：系统重启
- 常用运行级别是==3==和==5==也可以指定默认的运行级别



#### 2、指定运行级别

在CentOS 7以前，/etc/inittab文件中

CentOS 7以后

- ```multi-user.target```：analogous to runlevel 3
- ```graphical.target```：analogous to runlevel 5

#### 3、查看当前运行级别

```systemctl get-default```

#### 4、设置默认运行级别

```systemctl set-default TARGET.target```

![image-20220125075315155](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220125075315155.png)

### 找回root密码

1、首先启动系统，进入开机界面，在开机界面按“e”进入编辑界面

![image-20220125172835465](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220125172835465.png)

2、移动光标，找到UTF-8，在后边追加输入 ```init=/bin/sh```

![image-20220125173030808](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220125173030808.png)

3、完成后按 ```Ctrl + X ```进入单用户模式

4、接着，在光标闪烁的位置中输入```mount -o remount,rw/```按回车

5、出现新的界面，直接输入```passwd```,然后回车

6、按要求输入两次密码

7、接着，在鼠标闪烁的位置输入```touch /.autoreabel``` 注意，touch与/之间有一个空格，然后回车

8、继续在光标闪烁的位置输入```exec /sbin/init```注意，exec和/之间有一个空格，完成后按回车，等待系统自动修改密码，这个过程有些漫长，完成后系统会自动重启，**新密码就生效了**



### 帮助指令

- man 获取帮助信息
  - 基本语法
  - ```man 命令或配置文件```
  - 在Linux中，隐藏文件是用```.```开头的,选项可以组合使用
    - 如```ls -a```是包含隐藏文件的所有文件
    - ```ls -al```或者```ls -la```都是一个意思，表示全部文件按行展示
    - ```ls -al /tianhao``` 可以展示任何目录下的内容，自定义
  - 查看ls命令的帮助信息 ```man ls``` 【按q返回】
    - ![image-20220125175056826](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220125175056826.png)

- help指令【获取shell内置命令的帮助信息】
  - 基本语法：```help 命令```
  - 查看cd命令的帮助信息```help cd```

![image-20220125175501390](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220125175501390.png)

<font color="red">不如直接百度来的实际</font>



### 文件目录指令

#### pwd指令

显示当前工作目录的绝对路径

#### ls指令

```ls 选项 目录或文件夹```查看当前目录的所有内容

- 常用选项
  - ```-a```：显示当前目录所有的文件和目录，包括隐藏文件
  - ```-l```：以列表的形式显示信息
- 如：```ls -a /home```：显示home目录的所有信息
- ```ls -al /home```或者```ls -la /home```：用列表的形式、显示home目录的所有信息

#### ```cd```指令

基本语法：```cd 参数``` 切换到指定目录

```cd ~```或者```cd```：回到自己的家目录，比如root用户，不论在哪个文件夹，执行命令后回到/root

```cd ..```：回到上一级目录



例：目前在/home/tom目录下，如何回到root目录

- 1、绝对路径：```cd /root```
- 2、相对路径：```cd ../../root```



#### mkdir指令

用于创建目录

基本语法：```mkdir 选项 要创建的目录```

常用选项：

- ```-p```：创建多级目录【因为imidir默认只能创建一级目录】



举例：

- ```mkdir /home/dog``` 创建一个/home/dog目录
- ```mkdir -p /home/adimal/tiger```创建多级目录



#### rmdir指令

用于删除目录

基本语法：```rmdir 选项 要删除的空目录```

举例：

- 删除一个目录/home/dog
  - ```rmdir /home/dog```
- 删除/home/animal目录，animal内部还有其他目录
  - ```rm -rf /home/animal```

<font color="red">务必谨慎，这个操作是递归删除，如果写到是家目录，直接递归全删完了</font>



#### touch指令

用于创建空文件

基本语法：```touch 文件名称```

举例：在/home目录下创建一个空文件hello.txt

- ```cd /home```
- ```touch hello.txt```



#### cp指令

拷贝文件到指定目录

基本语法：```cp 选项 从哪 到哪```

常用选项：

- ```-r``` 递归复制整个文件夹



举例：

- 将/home/hello.txt 拷贝到 /home/bbb 目录下
  - ```cp hello.txt /home/bbb```
- 将/home/bbb 整个目录，拷贝到 /opt
  - ```cp -r /home/bbb /opt```
- 注意：==强制覆盖不提示的方法==
  - ```\cp```
  - ```\cp -r /home/bbb /opt```

#### rm指令

移除文件或目录

基本语法：```rm 选项 要删除的文件或目录```

常用选项：

- -r：递归删除整个文件夹
- -f：强制删除不提醒是否删除



举例：

- 将/home/hello.txt 删除
  - ```rm /home/hello.txt```
- 递归删除整个文件夹/home/bbb且不需要确认
  - ```rm -rf /home/bbb```
- 注意：强制删除不提示的方法，带上选项 -f 就行了



#### mv指令

移动文件目录或者重命名

基本语法：

- ```mv oldNameFile newNameFile``` 重命名【如果文件在同一个目录下，那就是重命名】
- ```mv /temp/movefile /targetFolder``` 移动文件

注意：

- 如果移动过程还写了名字，那就是移动并且重命名
- 移动当前文件夹内的文件，就不需要写当前路径，直接写目标路径

#### cat指令

查看文件内容



基本语法：```cat 选项 要查看的文件```

常用选项：

- ```-n``` 显示行号

举例：

- 查看/etc/profile 文件内容，并显示行号

注意：cat 只能浏览文件，而不能修改文件，为了浏览方便，一般会带上    管道命令 | more

```cat -n /etc/profile |more```

==**管道命令**==：就是将前一个命令结果  交给下一个命令继续处理



#### more指令

more指令是一个基于VI编辑器的文本过滤器，它以全屏幕的方式按页显示文本文件的内容，more指令中内置了若干快捷键

基本语法：```more 要查看的文件```

操作说明：

- 空格键：代表向下翻一页
- 回车键：代表向下翻一行
- q：代表立即离开more，不再显示该文件内容
- Ctrl+F：向下滚动一屏
- Ctrl+B：返回上一屏
- =：输出当前行的行号
- :f：输出文件名和当前行的行号

#### less指令

用来分屏查看文件内容，他的功能与more指令类似，但是比more指令更加强大，支持各种显示终端

less指令在显示文件内容时，并不是一次将整个文件加载之后才显示，而是根据显示需要加载内容，对于显示大型文件具有较高的效率

基本语法：```less 要查看的文件```

操作说明：

- 空格键：向下翻动一页
- pagedown：向下翻动一页
- pageup：向上翻动一页
- /字串：向下搜寻「字串」的功能；
  - n：向下查找
  - N：向上查找
- ？字串：向上搜寻「字串」的功能；
  - n：向上查找
  - N：向下查找
- q：离开less这个程序

#### echo指令

输出内容到控制台

基本语法：```echo 选项 输出内容```

举例：

- 输出环境变量HOSTNAME：```echo $HOSTNAME```
- 输出hello，world！：```echo hello,word!```

#### head指令

用于显示文件的开头部分内容，默认情况下head指令显示前10行内容

基本语法：

- ```head 文件```：查看文件头10行内容
- ```head -n 5 文件```：查看文件头5行内容，5可以是任意行数

#### tail指令

用于输出文件中的尾部内容，默认情况下tail指令显示文件的末尾10行内容

基本语法：

- ```tail 文件```查看文件尾10行内容
- ```tail -n 5 文件``` 查看文件尾5行内容，5可以是任意行数
- ```tail -f 文件```实时追踪该文档的所有更新

查看/etc/profile 最后5行的代码     ```tail -n 5 /etc/profile```

实时监控 mydate.txt ，看看到文件有变化时，是否看到，实时的追加日期

![image-20220126171706931](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220126171706931.png)

上图处于监控状态，占用光标，如果这个被监控文件发生了更改，更改内容立马出现在下边



#### >指令和>>指令

- ```>```覆盖------输出重定向

- ```>>```追加

基本语法：

- ```ls -l > a.txt```   列表的内容写到文件a.txt中【覆盖写】
- ```ls -al >> a.txt``` 列表的内容追加到文件a.txt的末尾
- ```cat file1 > file2``` 将 file1 的内容覆盖到 file2
- ```echo "内容" >> 文件``` 本来echo 内容是输出到控制台，这里给追加到文件了

#### ln指令

软连接也称为符号链接，类似于Windows里的快捷方式，主要存放了链接和其他文件的路径

基本语法：```ln -s 原文件或目录 软链接名``` 给原文件创建一个软链接

举例：

在/home 目录下创建一个软链接 myroot ，连接到/root目录

```ln -s /root /home/myroot```

删除软链接 myroot【最后不要带/呦】

```rm /home/myroot```

注意：当我们使用pwd指令查看目录时，仍然看到的是软链接所在目录

#### history指令

查看已经执行过的历史命令，也可以执行历史指令

基本语法：

```history``` 查看已经执行过历史命令

举例：

- ```history```显示所有历史命令
- ```history 10```显示最近是用过的10个指令
- ```!6```执行历史编号为 5 的指令



### 时间日期

#### date指令---显示当前日期

基本语法：

- ```date```显示当前时间
- ```date +%Y```显示当前年份
- ```date +%m```显示当前月份
- ```date +%d```显示当前是哪一天
- ```date "+%Y-%m-%d %H:%M:%S"```显示年月日时分秒

#### date指令---设置日期

基本语法：```date -s 字符串时间```

举例：

- 设置系统当前时间，比如设置成 2121年07月10日08:23:09
- ```date -s "2121-07-10 08:23:09"```



#### call指令---查看日历指令

基本语法：```cal 选项``` 【不加选项，默认显示本月日历】



举例：

- 显示当前日历```cal```

![image-20220126213727324](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220126213727324.png)

- 显示2099年日历```cal 2099```

![image-20220126213758178](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220126213758178.png)

### 搜索查找

#### find指令

**find指令将从指定目录向下递归地遍历其整个子目录，将满足条件的文件或者目录显示在终端***

基本语法：```find 搜索范围 选项```

选项说明：

- **-name<查询方式>**     按照指定的文件名查找模式查找文件
- **-user<用户名>**     查找属于指定用户的所有文件
- **-size<文件大小>**    按照指定的文件大小查找文件

举例：

1. 按文件名：根据名称查找/home 目录下的hello.txt文件
   1. ```find /home -name hello.txt```
   2. ![image-20220126214733765](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220126214733765.png)
2. 按拥有者：查找/opt 目录下，用户名称为 tianhao的文件
   1. ```find /opt -user root |more```【组合 |more 使用，便于查看】
3. 查找整个Linux 系统下大于200M的文件 （==+n 大于 -n小于 n等于，单位有k、M、G==）
   1. ```find / -size +200M```



#### locate指令

locate指令可以快速定位文件路径，locate指令利用事先建立的系统中所有文件名称及路径的locate数据库，实现快速定位给定的文件，locate指令无序遍历整个文件系统，查询速度较快，为了保证查询结果的准确度，管理员必须定期更新locate时刻

基本语法：```locate 搜索文件```

特别说明：locate指令基于数据库进行查询，所以第一次运行前，必须使用updatedb指令创建locate数据库

举例：请使用locate指令快速定位info.txt文件所在目录

```properties
[root@CentOS7-01 home]# updatedb
[root@CentOS7-01 home]# locate info.txt
```

#### which指令

可以查看某个指令在哪个目录下

举例：查看ls指令在哪个目录下

```properties
[root@CentOS7-01 home]# which ls
alias ls='ls --color=auto'
	/usr/bin/ls
```



#### grep指令和管道符号==|==

grep 过滤查找，管道符“|” 表示将前一个命令的处理结果输出传递给后面的命令处理

基本语法：```grep 选项 查找内容 源文件```

常用选项：

- **-n**： 显示匹配行及行号
- -i：忽略字母大小写

举例：在info.txt中，查找true所在的行，并显示行号

- 方法一：```cat info.txt | grep -ni "true"```
- 方法二：``` grep -ni "true" info.txt```

![image-20220126221829550](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220126221829550.png)

### 压缩和解压

#### gzip、gunzip指令

- gzip 用于压缩文件

- gunzip 用于解压文件

基本语法：

- ```gzip 文件``` 压缩文件，只能将文件压缩文为*.gz格式
- ```gunzip 文件.gz``` 解压文件

举例：

将/home 下的info.txt 文件进行压缩

- ```gzip /home/hello.txt```

将/home 下的info.txt.gz 文件进行解压

- ```gunzip /home/hello.txt.gz```



#### zip、unzip指令

- zip 用于压缩文件

- unzip 用于解压文件

基本语法：

- ```zip 选项 XXX.zip 准备压缩的内容``` 压缩文件和目录，并可指定压缩后的文件名
- ```unzip 选项 XXX.zip ``` 解压文件

- zip常用选项
  - -r：递归压缩，即压缩目录

- unzip常用选项
  - -d<目录>：指定解压后的文件存放位置，默认解压到当前目录

举例：

将/home 下的所有文件   压缩成 myhome.zip

- ```zip -r myhome.zip /home/```【将home目录 和 其包含的文件和子文件夹都压缩】

将 myhome.zip 文件解压到/opt/tmp目录下

- ```unzip -d /opt/tmp myhome.zip```



#### tar指令

tar指令 是打包指令，最后打包后的文件是==.tar.gz==的文件

基本语法：```tar 选项 XXX.tar.gz 打包的内容``` 打包目录，压缩后的文件格式.tar.gz

选项说明

- -c  产生.tar打包文件
- -v 显示详细信息
- -f 指定压缩后的文件名
- -z 打包同时压缩
- -x 解包.tar文件

举例：

- 压缩多个文件，将/home/pig.txt 和 /home/cat.txt 压缩成pc.tar.gz
  - ```tar -zcvf pc.tar.gz /home/pig.txt /home/cat.txt```
- 将/home 的文件夹压缩成 myhome.tar.gz
  - ```tar -zcvf myhome.tar.gz /home/```
- 将pc.tar.gz 解压到当前目录
  - ```tar -zcvf pc.tar.gz```
- 将myhome.tar.gz 解压到 /opt/tmp2 目录下
  - ```mkdir /opt/tmp2```
  - ```tar -zcvf /home/myhome.tar.gz -C /opy/tmp2```



## 7、组管理和权限管理

### Linux组基本介绍

在Linux中的每个用户必须属于一个组，不能独立于组外，在Linux中每个文件都有所有者、所在组、其他组的概念



### 文件、目录 所有者

一般为文件的创建者，谁创建了该文件，就自然的称为该文件的所有者

查看文件的所有者```ls -ahl```

修改文件所有者```chown 用户名 文件名```

![image-20220126232340499](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220126232340499.png)

### 组的创建

基本指令：```groupadd 组名```

举例：

- 创建一个组 monster-------->```groupadd monster```
- 创建一个用户fox，并放入到 monster组中------->```useradd -g monster fox```

### 文件、目录 所在组

当某个用户创建了一个文件后，这个文件的所在组就是该用户所在的组

### 修改文件所在的组

基本指令：```chgrp 组名 文件名```

举例：使用root用户创建文件orange.txt，看看该文件属于哪个组，然后将这个文件所在组，修改到fruit组

```properties
groupadd fruit
touch orange.txt
ls -ahl
chgrp fruit orange.txt
```

![image-20220126233608219](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220126233608219.png)

### 其它组

除文件的所有者和所在组的用户外，系统的其他用户都是文件的其他组



### 改变用户所在的组

在添加用户时，可以指定将该用户添加到哪个组中，同样的用root的管理权限可以改变某个用户所在的组

- 改变用户所在的组：
  - ```usermod -g 新组名 用户名```
  - ```usermod -d 目录名 用户名``` 改变该用户登录的初始目录
    - 注意：改变了目录，用户需要有进入新目录的权限
