

# Java学习笔记

## 一、基础部分

#### 1、软件开发介绍

**常用的DOS命令**

​	**dir** ： 列出当前目录下的文件及文件夹

​	**md** ：创建目录

​	**rd** ：删除目录

​	**cd** ：进入指定目录

​	**cd..** ：退回到上一级目录

​	**cd\\** ：退回到根目录

​	**del** ：删除文件

​	**exit** ：退出dos命令行



####  2、注释方式

Java规范的三种注释方式：

1、单行注释    //

```java
//单行注释
```

2、多行注释   /*                    */

```java
/*
	多行
    注释
*/
```

3、文档注释【java特有的】    /**              */

◆注释内容可以被JDK提供的工具javadoc所解析，生成一套以网页文件形式体现的该程序的说明文档

◆操作方式

盘符：路径\javadoc   -d  定义个文件名  -author  -version  程序名.java

```java
 /**
 	@author  指定Java程序的作者
 	@version  指定源文件的版本
 */
```



#### 3、第一个小程序总结

**Java程序编写---编译---运行的过程**

**编写：**我们将编写的Java代码保存在以“.java”结尾的源文件中；

**编译：**使用javac.exe命令编译我们的java源文件，格式：javac  源文件名.java；

**运行：**使用java.exe命令解释运行我们的字节码文件，格式：java  类名。



◆在一个java源文件中可以声明多个class，但是只能最多有一个类声明为public的。

而且要求声明为public的类的类名必须与源文件名相同。

◆程序的入口是main（）方法。格式是固定的。

◆输出语句：

```java
System.out.println();
//输出文字后换行

System.out.print();
//只输出数据，不换行
```

◆每个语句用英文   ;    结束

◆编译的过程：编译过后，会生成一个或多个字节码文件。字节码文件的文件名与java源文件中的类名相同。

#### 4、小知识点

##### 1）for循环可以加标签

使用break或者continue时，若存在多层嵌套循环可指定标签的for循环

```java
public class ForLabel {
    public static void main(String[] args){
        label:for (int i = 1; i <= 5; i++) {
            for (int j = 1; j <= 5; j++) {
                System.out.print(j);
                if(j == 3){
                    //break label;跳出标签为label的for循环
                    continue label;//label可以是任意字符
                }    
            }
        }
    }
}
```

##### 2）对属性赋值的位置：

​	1、默认初始化

​	2、显式初始化

​	3、构造器中初始化

​	4、有了对象以后，可以通过 “对象.属性”（非private类型属性） 或者 “对象.方法”的方式进行赋值

​	5、在代码块中赋值

​	先后赋值顺序：1-->2或5-->3-->4，    2、5同级别，按书写的先后顺序执行。

##### 3）方法的重载：

​	在同一个类中，方法名相同，但是参数类型、参数列表、参数个数不同；

​	在通过对象调用方法时，如何确定某一个指定的方法：

​					方法名----->参数列表

```java
public class OverLoadTest{
    //同名，仅参数处不同，可构成重载
    //跟方法的权限修饰符、返回值类型、形参变量名、方法体都没有关系；
    public void getSum(int i, int j){
        System.out.println(i + j);
    }
    
    public void getSum(double i, double j){
        System.out.println(i + j);
    }
    
    public void getSum(String s, int i){
        
    }
    
    public void getSum(int i, String s){
        
    }
}
```



##### 4）可变个数形参的定义：

​	1、多个形参的方法  与  同类型数组方法不能共存；

​	2、多个形参必须声明在最后一个；

```java
//1、
public void show(String...strs){
    
}
public void show(String[] strs) {  //不能跟上一个构成重载,不能同时存在。
        
}

//2、
public void show(int i ,String...strs){//正确
    
}

public void show(String...strs ， int i){//错误
    
}
```

##### 5）this关键字的使用

​	类似Python中的self，可以用来修饰  属性、方法、构造器；

​	1、在类的方法、构造器中，我们可以使用 “ **this . 属性**” 或者 “**this . 方法**” 的方式，调用当前对象的属性或者方		法。但是，通常情况下，我们都选择省略 “this” ，特殊情况下，如果方法的形参和类的属性同名时，我们必须		显式的使用 “this . 变量” 的方式，表明此变量时属性，而非形参。

​	2、构造器中调用构造器

​		①我们在类的构造器中，可以显式的使用 “ **this（形参列表）**” 的方式，调用本类中指定的其他构造器。

​		②构造器中不能够通过 “ this（形参列表）”  的方式调用自己。

​		③如果一个类中有n个构造器，则最多有n-1个构造器中使用了“ this（形参列表）”，不能相互调用，形成闭环。

​		④**规定：“ this（形参列表）” 必须声明在当前构造器的首行。**

​		⑤构造器内部最多只能声明一个“ this（形参列表）” 用来调用其他的构造器。

```java
public class TriAngle {
    //属性
    private double base;
    private double hight;

    //构造器
    public TriAngle(){   //空参

    }
    public TriAngle(double base ,double hight){   //带参
        this();   //调用构造器，，，，必须放在第一行！！！！
        this.base = base;
        this.hight = hight;
    }

    //方法
    public void setBase(double base){
        this.base = base;//!!!!!!!!!!!!!!!!!!这样定义形参名字，清晰明了。
    }
    public double getBase(){
        return base;
    }
    public void setHight(double hight){
        this.hight = hight;
    }
    public double getHight(){
        return hight;
    }
    public void eat(){
        System.out.println("干饭人，干饭魂！");
        work();//此处隐藏了this
        this.work();//调用方法，this表示与eat（）同一个对象
    }
    public void work(){
        System.out.println("打工人，打工魂！");
    }
}

```



##### 6）super关键字的使用

​		1、super理解为：父类的

​		2、super可以用来调用父类的：属性、方法、构造器

​		3、super的使用：调用属性和方法

​				3.1、我们可以在子类的方法或构造器中，通过 “ super.属性 ” 或 “super.方法”的方式，显式的调用父类						中声明的属性和方法。但是通常情况下我们省略 “super”

​				3.2、特殊情况：当子父类定义了同名的属性时，我们想要在子类中调用父类中声明的属性时，则必须显						式的使用 “ super.属性 ” 的方式，表明调用的是父类中声明的属性。

​				3.3、特殊情况：当子类重写了父类中的方法以后，我们想在子类的方法中调用父类中被重写的方法时，						则必须显式的使用 “ super.方法 ” 的方式，表明调用的是父类中声明的属性。

​		4、super的使用：调用构造器

​				4.1、我们可以在子类的构造器中显式的使用 “super（形参列表）” 的方式，调用父类中声明的指定的构						造器。

​				4.2、 “super（形参列表）” 的使用，必须声明在子类构造器的首行！

​				4.3、我们在类的构造器中，针对 “this（形参列表）” 或“super（形参列表）”，只能二选一，不能同时出							现，因为都要放在首行。

​				4.4、在构造器的首行，没有显式的声明 “this（形参列表）” 或“super（形参列表）”时，则默认调用的是						父类中空参的构造器。

​				4.5、在类的多个构造器中，至少有一个类的构造器中使用了“super（形参列表）”，调用父类中的构造器

**super和this：**

​		**this先在本类中查找，属性或方法，若没有则进入父类寻找。**

​		**super先在直接父类中查找，属性或方法，若没有则进入间接父类。**

​		**平时习惯省略，但是子父类中有同名的属性或方法时，用super可以区分调用。**

![image-20210816175635790](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210816175635790-16291077986081.png)

**子类对象实例化的全过程：**

​		1、从结果来看：

​				子类继承父类以后，就获取了父类中声明的属性和方法。

​				创建子类对象，在堆空间中，就会加载所有父类中声明的属性。

​		2、从过程来看：

​				当我们通过子类的构造器创建子类对象时，我们一定会直接或间接的调用其父类的构造器，进而调用父类的父类的构造器，直到调用了java.lang.Object类中的空参构造器为止，正因为加载过所有的父类结构，所以才可以看到内存中有父类中的结构，子类对象才可以考虑进行调用。

​		**3、明确：**虽然创建子类对象时，调用了父类的构造器，但是自始至终就创建过一个对象，即new的子类对象，不会创建父类对象。



###### **注意：**

​		若父类中没有空参构造器，子类创建继承时会报错，因为子类中的构造器默认是有一个空参的super（），此时因为父类没有，所以报错，解决方案：

一、在父类中，除了带参的构造器之外，再创建一个空参的构造器；

二、在子类中，子类的构造器中写一个super（形参列表），跳转父类带参的构造器，这样就不会有空参构造器了；

![image-20210816175718553](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210816175718553-16291078403752.png)





##### 7）import关键字的使用

​	import导入

​	1、在源文件中显式的使用import结构导入指定包下的类、接口

​	2、位置写在包的声明和类的声明之间

​	3、如果需要导入多个结构，并列写出即可

​	4、可以使用 “ **import java . *** ”的方式导入java包下的所有结构，但要使用java下的子包里的结构时，

​			还需要导入，xxx.*只能导入同层级的，再内层包的需要再导入；

​	5、如果使用的类或接口是java.lang包下定义的，则可以省略import结构

​	6、如果使用的类或接口是本包下定义的，则可以省略import结构

​	7、如果在源文件中，使用了不同包下的同名的类，则必须至少有一个类需要以全类名的方式显示

​	8、import static ：导入指定类或接口中的静态结构：属性或方法

​	

![](https://pledge99.oss-cn-beijing.aliyuncs.com/img/同名不同包.png)



```java
package Practice;//包

import Practice_Customer_Account.Account;//导入

public class Test {
    public static void main(String[] args) {
        Account acc = new Account(1000,233,33);//此处用import导入的
        Practice_Account_Customer_Bank.Account acc1 = new Practice_Account_Customer_Bank.Account(999);//因为重名，不能导入，只能写全名。
    }
}
```

##### 8）instanceof关键字的使用（防止ClassCastExecption的异常）

​		a instanceof A：判断对象a是否是类A的实例，如果是，返回true，如果不是返回false。

​		使用情景：为了避免在向下转型时出现ClassCastException的异常，我们在向下转型前，先进行instanceof的判断，一旦返回true就进行向下转型，如果返回false，就不进行向下转型。

​		如果 a instanceof A 返回tru，则类A的所有父类B C D .......等，都可以返回true。例a instanceof B也返回true，

```java
	父类：Person()
子类：man()、woman()
        测试类：Test()    
public class Test{
    public static void main(String[] args){
        Person pman = new man();
        Person pwoman = new woman();
        //向下转型，使用强制类型转换符
        man m1 = (man)pman;//此时m1可以调用man()的特有属性和方法
        //使用强制转换时，可能出现ClassCastExecption的异常
        if(pwoman instanceof woman){
            woman w1 = (woman)pwoman;
        }
    }
}
```

##### 9）static关键字的使用

​		**1、static：静态的**

​		**2、static可以用来修饰：**属性、方法、代码块、内部类

​		**3、使用static修饰属性：**静态变量

​				**3.1、属性：**按是否使用static修饰，又分为：静态属性  vs  非静态属性（实例变量）

​						**实例变量：**我们创建了类的多个对象，每个对象都独立拥有一套类中的非静态属性。当修改其中一个对象中的非静态属性时，不会导致其他对象中同样的属性值的修改。

​						**静态变量：**我们创建了类的多个对象，多个对象共享同一个静态变量。当通过某一个对象修改静态变量时，会导致其他对象调用此静态变量时，是修改过了的。

​				**3.2、static修饰属性的其他说明：**

​						① 静态变量随着类的加载而加载，可以通过“类.静态变量”的方式进行调用。

​						② 静态变量的加载要早于对象的创建。

​						③ 由于类只会加载一次，则静态变量在内存中也会只存在一份，存在方法区的静态域中。

​						④ 							类变量		实例变量

​						类（能否调用）		 yes			  no

​						对象（能否调用）	 yes			  yes

​				**3.3、静态属性举例：**System.out  (System类的，静态out，不用创建System对象，直接点.就可以调用)    							同理：Math.PI



​		**4、使用static修饰方法:静态方法**

​				① 静态变量随着类的加载而加载，可以通过“类.静态方法”的方式进行调用。

​				② 									静态方法		非静态方法

​						类（能否调用）		 yes			  no

​						对象（能否调用）	 yes			  yes

​				③ 静态方法中，只能调用静态的方法或属性，

​					非静态方法中，既可以调用非静态的方法或属性，也可以调用静态的方法或属性

![image-20210824203117559](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210824203117559-16298082791951.png)

​		**5、static注意点：**

​				① 在静态的方法内，不能使用this、super关键字

​				② 关于静态属性和静态方法的使用，从声明周期角度去理解

​		**6、总结：属性/方法**

​				① 开发中，如何确定一个属性是否要声明为static的？

​						>属性可以多个对象所共享的，不会随着对象的不同而不同的

​						>类中的常量也常常声明为static

​				② 开发中，如何确定一个方法是否要声明为static的？

​						>操作静态属性的方法，通常设置为static的

​						>工具类中的方法，习惯上声明为static的。比如：Math、Arrays、Collections等，调用时直接 ”类.xxx“即可，不用单独new对象。

```java
package KeywordTest;

public class StaticTest {
    public static void main(String[] args) {
        //未创建对象。直接调用静态(static)属性
        person.nation = "England";//此时nation属性为England

        //new第一个对象
        person p1 = new person();
        p1.name = "姚明";
        p1.age = 11;
        p1.nation = "China";//此时nation属性为China

        //new第二个对象
        person p2 = new person();
        p2.name = "科比";
        p2.age = 24;
        p2.nation = "America";//此时nation属性为America，p1对象的nation也是America，

        System.out.println(p1.nation);

        //编译不通过，非静态方法不能通过  类.方法名来调用
        //person.eat();

        //编译通过
        person.work();
    }
}

class person{
    String name;
    int age;
    static String nation;

    public void eat(){
        System.out.println("大口吃肉！");
    }

    public static void work(){
        System.out.println("打工人，打工魂！");
//        编译不通过，static静态方法中 不能使用this，super关键字
//        this.eat();
//        this.nation = "中国";
//        编译不通过，static静态方法中 不能调用非静态方法，属性
//        eat();
//        age = 66;

        nation = "中国";//静态属性前面省略的不是this，省略的是类名，补全应为：person.nation
    }
}
```



**练习：**通过静态变量自增，放在构造器中实现记录对象个数，每创建一个对象，静态变量++。

```java
public class StaticTest {
    public static void main(String[] args) {
        Circle c1 = new Circle();
        Circle c2 = new Circle();
        Circle c3 = new Circle();

        System.out.println("c1的id：" + c1.getId());
        System.out.println("c2的id：" + c2.getId());
        System.out.println("c3的id：" + c3.getId());

        System.out.println("圆的个数为：" + Circle.getTotal());
    }
}

class Circle{
    //属性
    private double radius;
    private int id;//自动赋值
    private static int total;//记录对象的个数
    private static int init = 10001;

    //构造器
    public Circle(){
        id = init++;
        total++;//通过静态变量自增，放在构造器中实现记录对象个数
    }

    public Circle(double radius) {
        this();//省略下边两行代码
        //id = init++;
        //total++;
        this.radius = radius;
    }

    //方法
    public int getId() {
        return id;
    }

    public static int getTotal() {
        return total;
    }
}
```

##### 10）final关键字的使用：

​		**final 可以用来修饰的结构：类、方法、变量**

​		>**final** 用来修饰一个类：**此类不能被其他类所继承**。

​				比如：String类、System类、StringBuffer类

```java
public final class String
```

​		>**final** 用来修饰方法：**此方法不能被其他类重写**。

​				比如：Object类中的getclass()方法

```java
public final native Class<?> getClass();
```

​		>**final** 用来修饰变量：**此时的“变量”就称为一个常量**。

​				final修饰属性，可以考虑赋值的位置有：显式初始化、代码块中初始化、构造器中初始化。

​				final修饰局部变量：尤其是使用final修饰形参时，表明形参是一个常量，当我们调用此方法时，给常量形参赋一个实参，一旦赋值以后，就只能在方法体内使用此形参，但不能重新赋值。

​		>**static final** 用来修饰属性：**全局常量（常量大写字母表示）**

```java
//修饰变量
public void show(){
    final int NUM = 10;
    //此时NUM是常量10，不能再赋值；
    //NUM = 20;报错
}

//修饰形参
public void show(final int num){
    //此时num是在调用时对其赋值，内部不能再更改或赋值；
    //NUM = 20;报错
}
```

##### 11）abstract 关键字的使用

​		1、abstract：抽象的

​		2、abstract可以用来修饰的结构：类、方法

​		3、abstract修饰类：抽象类

​				>此类不能实例化（不能造对象）

```java
public class AbstractTest{
    public static void main(String[] args){
        //报错 Person p1 = new Person();
        //p1.eat();
    }
}

abstract class Person {
    //加上abstract后，main函数中就不可以创建Person对象。
	//内容省略
}
```

​				>抽象类虽然不能造对象，但要保留构造器，因为子类实例化时要调用（涉及：子类对象实例化的全过程）

​				>开发中，抽象类都会提供子类，让子类对象实例化，完成相关操作（没子类，又不能实例化，这不是废类么）

​		4、abstract修饰方法：抽象方法

​				>抽象方法只有方法声明，没有方法体

```java
abstract class Person {//加上abstract后，main函数中就不可以创建Person对象。

    //普通方法
    public void eat(){
        
    }
    
    //抽象方法
    public abstract void eat2();
```

​				>**包含抽象方法的类一定是抽象类。**反之，抽象类中可以不存在抽象方法。

​				>若子类重写了父类中的**所有**抽象方法，此子类方可实例化

​				>若子类没有重写父类中的所有抽象方法，则此子类也是一个抽象类，需要使用abstract修饰（换言之，没全部重写，表示子类继承了父类的抽象方法，抽象方法的类必须是抽象类，所以必须用abstract修饰，还是不能实例化）

​		**5、abstract使用注意：**

​				1、abstract不能用来修饰：属性、构造器等结构

​				2、abstract不能用来修饰**私有方法**（私有方法不能被重写）、**静态方法**（静态方法不能被重写）、**final的方法**、**final的类**（final不能被重写、继承）

#### 5、Java语言的特点

##### **面向对象性：**

​	两个要素：类、对象

​	三个特征：封装、继承、多态

##### **健壮性：** 

​	去除了C语言中的指针

​	自动的垃圾回收机制----->仍然会出现内存溢出、内存泄漏

##### **跨平台性：**

write once ，run anywhere；一次编译，到处运行。



#### 6、[java命名规则/规范](https://www.cnblogs.com/Tianhaoblog/p/15069051.html)

##### **规则：**

名称只能由字母、数字、下划线、$符号组成。

不能以数字开头，不能包含空格。

名称不能使用Java中的关键字。

 

##### 规范：

**项目名**全部小写：   project

**包名**全部小写：  woshibao

类名、接口名，多单词组成时，所有单词首字母大写：  WoShiLei

**变量名、方法名**，多单词组成时，第一个单词全部小写，剩余单词的首字母大写：  woShiBianLiang、woShiFangFa

**常量名**全部大写，多个单词时用下划线分割：  WO_SHI_CHANG_LIANG

****

**起名时为了提高阅读性，尽量有意义，做到“见名知意”！！！**

#### 7、[Java的数据类型](https://www.cnblogs.com/Tianhaoblog/p/15069293.html)

##### 一、变量按照数据类型来分：

###### 　　基本数据类型：

　　　　整型：byte \ short \ int \ long

　　　　浮点型：float \ double

　　　　字符型：char

　　　　布尔型：boolean

​				当byte、short、char做运算时，结果自动提升为int类型。

```java
//定义long类型变量时，需在末尾加上L/l
long m = 1234567L;
//定义float类型变量时，需在末尾加上F/f
float n = 12.1234567f;
```

​		**强制类型转换：**（目标类型）原变量

​						（int）变量

```java
double a = 22.2；
int b = (int)a；   //强制类型转换，可能会导致精度缺失。相当于截断操作；
```



###### 　　引用数据类型：

　　　　类（class）

　　　　接口（interface）

　　　　数组（array）

##### 二、变量在类中声明的位置来分：

###### 　　**成员变量：**

​		在方法体外，类体内声明的变量

　　　　**实例变量**（不以static修饰）

　　　　**类变量**（以static修饰）

###### 　　**局部变量：**

​		在方法体内部声明的变量

　　　　**形参**（方法、构造器中定义的变量）

　　　　**方法局部变量**（在方法内定义）

　　　　**代码块局部变量**（在代码块内定义）

　　**相同点：**二者都有生命周期

　　**不同点：**局部变量除形参外，需要显示初始化

#### 8、逻辑运算符

**& 和&&的区别**

&& 短路与 ，一个条件不成立，跳出判断
& 与   ，  全部判断

```java

boolean b1 = false;
int num = 9;
if(b1 & (num++ > 10)){      //此处即使发现b1为假，仍判断num++ > 0条件是否满足，进行了num++操作。
    System.out.println("降龙十八掌");
}else{
    System.out.println("凌波微步");
}
System.out.println(num);


boolean b2 = false;
int num2 = 9;
if(b1 && (num2++ > 10)){     //此处发现b1为假，立即跳出判断，不论 num++ > 0条件是否满足，num++操作未执行。
    System.out.println("小李飞刀");
}else{
    System.out.println("一阳指");
}
System.out.println(num2);
```

#### 9、键盘获取数据

```java
import java.util.Scanner; //导入包

public class HelloWord {
    public static void main(String[] args){

        Scanner scan = new Scanner(System.in);//创建一个对象

        //从键盘获取字符串类型数据
        System.out.println("请输入你的姓名：");
        String name = scan.next();
        System.out.println(name);

        //从键盘获取整型数据
        System.out.println("请输入你的学号：");
        int num = scan.nextInt();
        System.out.println(num);

        //从键盘获取浮点型数据
        System.out.println("请输入你的体重：");
        double weight = scan.nextDouble();
        System.out.println(weight);

        //从键盘获取布尔型数据
        System.out.println("你喜欢喝咖啡吗？（true/false）：");
        boolean iscoffee = scan.nextBoolean();
        System.out.println(iscoffee);

    }
}
```



#### 10、面向对象的特征一：封装性（*Encapsulation*）

##### 	一、问题的引入：

​		当我们创建一个类的对象以后，我们可以通过 “ 对象+属性 ” 的方式，对对象的属性值进行赋值，这里赋值操作要受到属性的数据类型和存储范围的制约，除此之外，没有其他制约条件。但是，在实际问题中，我们往往要给属性赋值并加入额外的限制条件。这个条件就不能在属性声明时体现，我们只能通过方法进行限制条件的添加。比如setLegs（），同时，我们需要避免用户再使用 “ 对象+属性 ” 的方式对属性进行赋值，则需要将属性声明为私有的（private）。------>此时针对属性就体现了封装性。

```java
public class Test {
    public static void main(String[] args){
        Animal a = new Animal();
        a.name = "大象";
        a.age = 1;
        a.legs = 4;    //报错，不能再调用、赋值等
        int l = a.setLegs();//通过方法来调用；
        a.show();

        a.setLegs(-9);	//legs会被置为0，因为-9不在其范围；
        a.setLegs(88);
        a.show();

    }
}

class Animal{
    String name;
    int age;
    private int legs;    //私有属性，类外不能调用.只能通过给提供的setLegs方法，作为接口，进行赋值等操作；
    
    //对于私有属性的设置
    public void setLegs(int leg){
        if(leg >= 0 ){
            legs = leg;
        }else{
            legs = 0;
        }
    }
    //对私有属性的获取，通过方法；
    public int getLegs(){
        return legs;
    }
    
    
    
    public void show(){    //打印各个属性值
        System.out.print("名称是：" + name + "，年龄是：" + age + "，腿的个数为：" + legs + "\n");
    }
}
```

##### 二、封装性的体现：

​	我们将类的属性**私有化（private）**，同时，提供**公共（public）**的方法来**获取（getXxx）**和**设置（setXxx）**属性的值。

拓展：封装性的体现

​	①如上；

​	②不对外暴露的私有的方法；

​	③单例模式。。。。



##### 三、封装性的体现，需要权限修饰符来配合

​		1、Java规定的4种权限（从小到大排序）：private、缺省、protected、public

![](https://pledge99.oss-cn-beijing.aliyuncs.com/img/java封装性.png)

​		2、4种权限修饰符可以用来修饰类及类的内部结构：属性、方法、构造器、内部类；

​		3、具体的，**修饰类的话，只能使用：缺省、public**

##### 总结封装性：

​		Java提供了4种权限修饰符来修饰类及类的内部结构，体现类及类的内部结构在被调用时的可见性的大小。

![](https://pledge99.oss-cn-beijing.aliyuncs.com/img/java封装性2.png)



#### 11、面向对象的特征二：继承性（Inheritance）

##### 		一、继承性的好处：

​				①减少了代码的冗余，提高了代码的复用性

​				②便于功能的扩展

​				③为之后多态性的使用提供了前提

##### 		二、继承性的格式：class A extends B {}

​				A：子类、派生类、subclass

​				B：父类、超类、基类、superclass

​				①体现：一旦子类A继承了父类B之后，子类A中就获取了父类B中声明的所有的属性、方法

​				**特别的：**父类中声明为private的属性和方法，子类继承父类以后，仍然认为获取了父类中的私有结构，								只是因为封装性的影响，使得子类不能直接调用父类的结构而已，通过get、set方法获取修改

​				②子类继承父类以后，还可以声明自己特有的属性或方法，实现功能的拓展

​					子类和父类的关系，不同于子集和集合的关系

​				**extends：延展、扩展**

##### 		三、Java中关于继承性的规定：

​				Java只支持单继承和多层继承，不允许多重继承

​				①一个子类只能有一个父类

​				②一个父类可以派生出多个子类

​				③子父类是一个相对的概念

​				④子类直接继承的父类称为：直接父类。间接继承的父类称为，间接父类。

​				⑤子类继承父类以后，就获取了直接父类以及所有的间接父类中声明的属性和方法



![image-20210815135850886](https://pledge99.oss-cn-beijing.aliyuncs.com/img/子父类.png)

##### 		四、默认继承类

​				①如果我们没有显式的声明一个类的父类的话，则此类继承于java.lang.Object类

​				②所有的java类（除java.lang.Object类之外）都直接或间接继承于java.lang.Object类

​				③意味着，所有的java类中java.lang.Object类声明的功能

##### 		五、方法的重写（Override）

​				①重写：子类继承父类以后，可以对父类中的同名同参数的方法，进行覆盖操作

​				②应用：重写以后，当创建子类对象以后，通过子类对象调用子父类中的同名同参数的方法时，

​								实际执行的是子类中重写父类的方法

​				③重写的规定：

​								方法的声明：权限修饰符 返回值类型 方法名（形参列表）throws 异常类型{

​														//方法体

​														}

​								约定俗成：子类中的方法叫 “重写的方法”，父类中的方法叫 “被重写的方法”。

​								①子类重写的方法的方法名和形参列表与父类中被重写的方法和形参列表相同

​								②子类中的权限修饰符要**大于等于**父类中被重写的方法的权限修饰符

​								③**子类不能够重写父类中权限声明为为private的方法**

​								④返回值类型：

​									>父类被重写的方法的返回值类型void ，则子类重写的方法的返回值类型也必须时void！

​									>父类被重写的方法的返回值类型A类型，则子类重写的方法的返回值类型可以是A类型

​										或者A类型的子类。

​								⑤子类重写的方法，抛出的异常类型，不大于父类被重写的方法抛出的异常类型。

**子类父类中同名同参数的方法，要么都声明为static的（可以考虑重写），要么都声明为非static的（不可以重写），必须一致！**



#### 12、面向对象的特征三：多态性（Polymorphism）

​		1、理解多态性：可以理解为一个事物得到多种形态。

​		2、何为多态性：对象的多态性：父类的引用指向子类的对象（或子类的对象赋给父类的引用）,**实现代码的通用性**

​		3、多态的使用：虚拟方法的调用

​				有了对象的多态性以后，我们在编译期，只能调用父类中声明的方法，但是运行期，我们实际执行的是子类重写父类的方法。

```java
父类：Person()
    子类：man()、woman()
测试类：Test()    
public class Test{
    public static void main(String[] args){
        Person pman = new man();
        Person pwoman = new woman();
        //new man（）和new woman（）后，内存中实际上也加载了子类所特有的属性和方法，但是由于变量声明为父类类型，导致编译时，只能调用父类中声明的属性和方法，子类所特有的属性和方法不能调用。
        //如何调用子类所特有的属性和方法？
        //向下转型，使用强制类型转换符
        man m1 = (man)pman;//此时m1可以调用man()的特有属性和方法
        
        //使用强制转换时，可能出现ClassCastExecption的异常
    }
}
```

​		**总结：①编译：看左边，运行：看右边、②不能调用子类所特有的方法，只能调用重写的**

​		4、多态性的使用前提：①类的继承关系②方法的重写

​		5、对象的多态性，只适用于方法，不适用于属性（**属性的编译和运行都看左边**）。

![image-20210816200540499](https://pledge99.oss-cn-beijing.aliyuncs.com/img/java构造器.png)

![image-20210816200741163](https://pledge99.oss-cn-beijing.aliyuncs.com/img/java构造器2.png)



#### 13、类的结构之-------构造器（constructor）

​		类的结构：属性、方法、构造器（或构造方法）

​		一、构造器的作用：

​				1、创建对象      new + 构造器

​				2、初始化对象的信息

​		二、说明：

​			1、如果没有显示的定义类的构造器的话，则系统默认提供一个空参的构造器

​			2、定义构造器的格式：权限修饰符  类名（形参列表）{}

​			3、一个类中定义多个构造器，彼此构成重载

​			4、**一旦我们显示的定义了类的构造器之后，系统就不在提供默认的空参的构造器。**

​								所以必须先写一个空参的在前边。

![](https://pledge99.oss-cn-beijing.aliyuncs.com/img/接口.png)

​		既然系统提供的是空参的构造器，那么我也可以创建一个带有参数的构造器：

![](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210816200540499-16291155429993.png)

```java
//构造器（constructor）
public class Test {
    public static void main(String[] args){
        Person p = new Person();
        p.eat();
        
        Person p1 = new Person("铁蛋" , 9);//创建对象的同时，直接带参数，例如：将属性赋值
        System.out.println("p1新对象的name为：" + p1.name + "，p1新对象的age为：" + p1.age);
    }
}

class Person{
    //属性
    String name;
    int age;


    //构造器
    public Person(){//空参
        
    }
    public Person(String m,int n){ //创建对象的同时，直接带参数，例如：将属性赋值
        name = m;
        age = n;
    }


    //方法
    public void eat(){
        System.out.println("大口吃肉");
    }
}
```



#### 14、Object类

##### 		toString（）方法：

​		1、当我们输出一个对象的引用时，实际上就是调用当前对象的toString()方法；

​		2、Object类中toString()方法的定义：

```java
public String toString() {
    return getClass().getName() + "@" + Integer.toHexString(hashCode());
}
```

​		3、像String、Data、File、包装类等，都重写了Object类中的toString()方法。使得我们在调用时对象的toString()时，返回 “实体内容” 的信息，不是地址值。

​		4、自定义类也可以重写toString()方法，当调用此方法时，返回对象的 “实体内容”。

```java
import Inheritance.Test;
import java.util.Date;

public class equals1 {
    public static void main(String[] args) {
        Test t = new Test();
        //Test()重写toString()前   输出如下：地址值
        System.out.println(t.toString());//Inheritance.Test@1b6d3586 
        System.out.println(t);//Inheritance.Test@1b6d3586，println中默认调用了toString()方法。
        
        //Test()重写toString()后   输出如下：“实体内容”
        System.out.println(t);//Test{name='dog', age=18}

        String str = new String("我是字符串");//此时虽然也是对象，但是输出的是对象的“实体内容”，因为String()中重写了toString()方法；
        System.out.println(str);//我是字符串

        Date dat = new Date(2345234673268L);//理由同上
        System.out.println(dat);//Tue Apr 26 06:04:33 CST 2044
    }

}
```

Test（）类如下：

```java
package Inheritance;

public class Test {
    public String name = "dog";
    public int age = 18;

    @Override//类中重写了toString()，再调用后，不会输出地址值
    public String toString() {
        return "Test{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
```



###### 举例：toString()输出数组

```java
int[] a1 = {2, 4, 3, 8, 55, 22, 15};

System.out.println(a1);
//------------------直接输出
[I@1b6d3586

String sarr = Arrays.toString(a1);//注意！！！！是Arrays，，，不是Array
System.out.println(sarr);
//------------------转换后输出
[2, 4, 3, 8, 55, 22, 15]
```

Arrays（）中重写的toString（）方法如下：

```java
public static String toString(int[] a) {
    if (a == null)
        return "null";
    int iMax = a.length - 1;
    if (iMax == -1)
        return "[]";

    StringBuilder b = new StringBuilder();
    b.append('[');
    for (int i = 0; ; i++) {
        b.append(a[i]);
        if (i == iMax)
            return b.append(']').toString();
        b.append(", ");
    }
}
```



##### equals（）方法：

​		1、A.equals（B）,返回true或者false

​		2、只能够适用于引用数据类型

​		3、Object类中equals（）方法的定义：

```java
public boolean equals(Object obj) {
    return (this == obj);
}
//此时表明：在Object类中定义的equals()方法和“==”运算符的作用是相同的；
```

​		4、像String、Data、File、包装类等，都重写了Object类中的equals（）方法。重写以后，比较的不是两个引用的地址是否相同，而是比较两个对象的 ”实体内容“ 是否相同。

​		5、通常情况下，我们自定义的类如果使用equals（）的话，也通常是比较两个对象的 “实体内容”，是否相同，那么我们就需要重写Object类中的equals（）方法。

#### 15、包装类

​		**基本数据类型-----包装类-----String类型**   三者之间的相互转换

```java
import org.junit.Test;

public class WrapperTest {
    @Test
    public void test(){
        //基本数据类型num---->转换为包装类对象in111
        int num = 999;
        Integer in111 = new Integer(num);
        Integer in222 = num;        //JDK5.0新特性，自动装箱，不用new对象；

        //此时可以使用in111.toString()方法
        System.out.println(in111.toString());
        System.out.println(in222.toString());

        //包装类---->转换为基本数据类型
        int num2 = in111.intValue();
        int num3 = in111;       //自动拆箱，不用调用方法；
        System.out.println(num2);
        System.out.println(num3);

        //基本数据类型、包装类---->String类型；
        //方法一：连接运算
        int num4 = 9;
        String str1 = num4 + "";
        System.out.println(str1);
        //方法二：调用String的valueOf(Xxx xxx)方法
        float f1 = 12.3f;
        String str2 = String.valueOf(f1);
        System.out.println(str2);

        //String类型---->基本数据类型、包装类；
        //调用包装类的parseXxx)
        String str3 = "123";
        int num5 = Integer.parseInt(str3);
        System.out.println(num5);
        System.out.println(str3);
    }
}

```

##### 练习题：

```java
/**Practice
 * 利用Vector代替数组处理：从键盘读入学生成绩（以负数代表结束），
 * 找出最高分，并输出学生等级。
 * 若与最高分相差10分以内：A等
 * 20分以内：B等
 * 30分以内：C等
 * 其他：D等
 */

import java.util.Scanner;
import java.util.Vector;

public class ScoreTest {
    public static void main(String[] args){
        //创建对象
        System.out.println("请输入学生成绩，输入负数结束");
        Scanner scan = new Scanner(System.in);
        Vector v = new Vector();
        
		//录入并添加数据,同时记录最大值
        int maxScore = 0;
        while(true){
            int score = scan.nextInt();
            if(score < 0){
                break;
            }
            if(score > 100){
                System.out.println("输入数据非法，请重新输入！");
                continue;
            }
            if(maxScore < score){
                maxScore = score;
            }
//            jdk5.0之前：
//            Integer inScore = new Integer(score);
//            v.addElement(inScore);//多态

            //jdk5.0之后
            v.addElement(score);//自动装箱,转为对象。
            
        }
        System.out.println("最大值为：" + maxScore);

        //遍历并输出等级
        char level;
        for(int i = 0;i < v.size();i++){
            Object obj = v.elementAt(i);

//            jdk5.0之前：
//            Integer inScore = (Integer) obj;  Object --->Integer---->.xxxValue取到值
//            int score = inScore.intValue();

            //jdk5.0之后
            int score = (int)obj;//Object --->int取到值

            if(maxScore -10 <= score){
                level = 'A';
            }else if (maxScore -20 <= score){
                level = 'B';
            }else if (maxScore -30 <= score){
                level = 'C';
            }else{
                level = 'D';
            }
            //输出成绩
            System.out.println("student is: "+ i +"\tscore is: " + score + "\tlevel is: " + level);
        }
    }
}
```

#### 16、单例（Singleton）设计模式

​		**设计模式：**是在大量的实践中总结和理论化之后优选的代码结构、编程风格、以及解决问题的思考方式。设计模式就像经典的棋谱，不同的棋局我们用不同的棋谱，免得我们自己再去思考和摸索。

​		**单利设计模式：**就是采取一定的方法保证在整个的软件系统中，**对某个类只能存在一个对象实例**，并且该类只提供一个取得对象实例的方法。如果我们要让类在虚拟机中只能产生一个对象，我们首先必须将类的构造器的访问权限设置为private，这样，就不能用new操作符在类的外部产生类的对象了，但在类的内部仍可以产生该类的对象，只能调用该类的某个静态方法以返回类内部创建的对象，静态方法只能访问类中的静态成员变量，所以，指向类内部产生的该类的对象的变量也必须定义成静态的。

​		**单例设计模式：**饿汉式 VS 懒汉式

​				饿汉式：直接创建对象，使用时调用；

​								坏处：对象加载时间过长。

​								好处：饿汉式是线程安全的。

​				懒汉式：暂不创建，使用时创建；

​								好处：延迟对象的创建。

​								坏处：目前的写法线程不安全，多线程时同时满足instance == null，同时进入if语句，创建多个对象，----------------后续在多线程时修改

```java
//饿汉式

public class Singleton_hungry {
    public static void main(String[] args){
        Singleton s1 = Singleton.getInstance();
        Singleton s2 = Singleton.getInstance();
        //因为静态对象已经创建完毕，此时仅仅是调用，所以s1 和s2 是同一个对象。
    }
}
class Singleton{
    //1、私有化构造器
    private Singleton(){

    }
    //2、内部创建类的对象
    private static Singleton instance = new Singleton();

    //3、提供公共的静态的方法，返回类的对象
    public static Singleton getInstance(){
        return instance;
    }
    //2、3必须是static静态结构，因为内部创建对象，如果不是静态结构，需在外部创建对象后方能调用getinstance()方法，
    // 但是对象又只能在内部创建，故形成闭环，死锁。
    // 如果是静态结构，初始就已经完成创建对象，并且直接在外部通过   类.方法（） 直接调用getInstance（）。
}
```



```java
//懒汉式
public class Singleton_lazy {
    public static void main(String[] args){
        Singleton_2 s1 = Singleton_2.getInstance();
        Singleton_2 s2 = Singleton_2.getInstance();
        if(s1 == s2)
            System.out.println(true);
    }
}


class Singleton_2{
	//创建私有化构造器
    private Singleton_2(){

    }

    static Singleton_2 instance = null;
	
    //获取对象方法getInstance()
    public static Singleton_2 getInstance() {
        //未创建，则进入创建，此处若多线程，则会出现创建多个对象的情况
        if(instance == null){
            instance = new Singleton_2();
        }
        return instance;
    }
}
```



#### 17、代码块

​		1、代码块的作用：用来初始化类、对象。

​		2、代码块如果有修饰的话，只能是static。

​		3、分类：静态代码块  and  非静态代码块

​		4、静态代码块：

​				>内部可以有输出语句

​				>随着类的加载而执行，而且只执行一次

​				>作用：初始化类的信息，对静态属性进行赋值

​				>如果一个类中定义了多个静态代码块，则按照声明的先后顺序执行

​				>静态代码块的执行要优先于非静态代码块

​				>只能调用静态的属性或静态的方法

​		5、非静态代码块

​				>内部可以有输出语句

​				>随着对象的创建而执行

​				>每创建一个对象，就执行一次非静态代码块

​				>作用：可以在创建对象时，对每个对象的属性等进行初始化

​				>如果一个类中定义了多个非静态代码块，则按照声明的先后顺序执行

​				>可以调用非静态的属性和方法、也可以调用静态的属性或方法



```java
//静态代码块
static{
	//随着类的加载而执行，而且只执行一次
    //只能调用静态的属性或静态的方法
}

---------------------------------------------------------------------------------------
//非静态代码块
{
	//随着对象的创建而执行
    //可以调用非静态的属性和方法、也可以调用静态的属性或方法
}
```



#### 18、接口

​		接口的使用：

​		1、接口使用interface来定义

​		2、在Java中，接口和类是并列的结构。

​		3、如何定义接口：定义接口中的成员

​				3.1、JDK7及以前：只能够定义全局常量和抽象方法

​						>全局常量：public static final 的，（但是书写时，可以不写，直接写 int、double等）

​						>抽象方法：public abstract 的

​				3.2、JDK8：除定义全局常量和抽象方法以外，还可以定义静态方法、默认方法。

​						>静态方法：使用static关键字修饰，可以通过接口直接调用静态方法，并执行方法体。

​											 经常在互相一起使用的类中使用静态方法，

​											 可以在标准库中找到像Collection/Collections或者Path/Paths这样成对的接口和类

​						>默认方法：默认方法使用default关键字修饰，可以通过实现类的对象来调用。

​											 我们在已有的接口中提供新方法的同时，还保持了与旧版本代码的兼容性。

​											 比如：java 8 API中Collection、List、Comparator等接口提供了丰富的默认方法

```java
public class SubClassTest {
    public static void main(String[] args) {
        SubClass s = new SubClass();
        s.method2();//只能调用method2，不能调用静态方法method1
        //也可以在实现类中重写方法method2

        CompareA.method1();//静态方法只能通过接口自己调用。
    }
}

//接口的实现类
class SubClass implements CompareA{

}

interface CompareA {
    //public 同样可以省略

    //静态方法
    public static void method1(){
        System.out.println("method1");
    }

    //默认方法
    public default void method2(){
        System.out.println("method2");
    }
}
```

​		4、接口中不能定义构造器！意味着接口不能实例化。

​		5、Java开发中，接口通过让类去实现（implements）的方式来实现。

​			  如果实现类覆盖了接口中的所有的抽象方法，则此实现类就可以实例化

​			  如果实现类没有覆盖接口中所有的抽象方法，则此实现类仍为一个抽象类

```java
public class InterfaceTest {
    public static void main(String[] args){
        Plane p = new Plane();
        p.fly();
        p.stop();

    }
}

interface Flyable{
    //全局变量
    public static final int MAX_SPEED = 7900;//第一宇宙速度
    int MIN_SPEED = 1;//public static final 可以省略，因为只要在接口内，必须这么写，所以省略后也是存在的。

    //抽象方法
    public abstract void fly();
    void stop();//省略了public abstract，道理同上
}

//全部重写了接口中的抽象类，此时Plane类就是可以实例化的类
class Plane implements Flyable{

    @Override
    public void fly() {
        System.out.println("起飞！");
    }

    @Override
    public void stop() {
        System.out.println("停止！");
    }
}

//没有全部重写，接口中的抽象方法，此时只能还是abstract抽象类
abstract class Kite implements Flyable{
    @Override
    public void fly(){

    }
}
```

​		6、Java类可以实现多个接口，----------接口：就是因为Java只能单继承，通过实现接口，达到多继承的效果。

​			  格式：class AA extends BB implements CC , DD , EE{}

​			  先写继承，后写接口，多个接口用逗号隔开。

```java
interface Flyable{
   void stop();//省略了public abstract，道理同上
}

interface Attackable{
    void attack();
}

//多接口
class Bullet implements Flyable,Attackable{
//全部抽象方法都要重写
	@Override
    public void stop() {

    }

    @Override
    public void attack() {

    }
}
```

​		7、接口与接口之间可以继承，而且支持多继承。

```java
interface AA{
    void method1();
}
interface BB{
    void method2();
}
//接口多继承
interface CC extends AA,BB{

}
//后续通过类实现接口CC时，要将父接口AA、BB中的抽象方法全部覆盖（重写）
```

​		8、接口的具体使用，能够体现多态性

​		9、接口实际上可以看做是一种规范

​		10、开发中，体会面向接口编程

```java
public class USBTest {
    public static void main(String[] args){
        Computer computer = new Computer();

        Flash flash = new Flash();
        computer.transferData(flash);//实际传入Flash类型---多态

        Printer printer = new Printer();
        computer.transferData(printer);//实际传入Printer类型---多态
    }
}

class Computer{//电脑运行步骤
    public void transferData(USB usb){//声明为USB类型，传入非USB，等价于USB usb = new Flash();多态
        usb.start();
        System.out.println("传输数据ing...");
        usb.stop();
    }
}
interface USB{//接口----相当于 规范，任何设备U盘、打印机都要遵循USB定义的规范，目前也就是两个方法。
    void start();
    void stop();
}

class Flash implements USB{//不同设备，实现接口

    @Override
    public void start() {
        System.out.println("U盘开始工作！");
    }

    @Override
    public void stop() {
        System.out.println("U盘结束工作！");
    }
}

class Printer implements USB{//不同设备，实现接口

    @Override
    public void start() {
        System.out.println("打印机开始工作！");
    }

    @Override
    public void stop() {
        System.out.println("打印机结束工作！");
    }
}
```

​	11、接口的匿名、非匿名实现类的匿名、非匿名对象。

```java
public class USBTest {
    public static void main(String[] args){
        Computer computer = new Computer();
        //1、创建了接口的非匿名实现类的   非匿名对象
        Flash flash = new Flash();
        computer.transferData(flash);//实际传入Flash类型---多态
        Printer printer = new Printer();
        computer.transferData(printer);//实际传入Printer类型---多态

        //2、创建了接口的非匿名实现类的   匿名对象
        computer.transferData(new Printer());

        //3、创建了接口的匿名实现类的    非匿名对象
        USB phone = new USB() {//class Flash implements USB{},其实就是把下边的名字没写，但是内容要给写出来
            @Override
            public void start() {
                System.out.println("手机开始工作了！");
            }
            @Override
            public void stop() {
                System.out.println("手机结束工作了！");
            }
        };//这里要有   ;
        computer.transferData(phone);

        //4、创建了接口的匿名实现类的    匿名对象
        computer.transferData(new USB() {
            @Override
            public void start() {
                System.out.println("不知道什么东西开始工作了！");
            }

            @Override
            public void stop() {
                System.out.println("不知道什么东西结束工作了！");
            }
        });
    }
}
```

12、如果子类（或实现类）继承的父类和实现的接口中声明了   同名同参数的方法，那么子类在没有重写此方法的情况下，默认调用的是父类中同名同参数的方法----**类优先原则，仅适用于方法，属性不可以！**

13、如果实现类实现了多个接口，而这多个接口中定义了同名同参数的方法，那么实现类在没有重写此方法的情况下，编译报错------接口冲突！那么必须在实现类中重写此方法。

14、如何在子类（实现类）的方法中调用父类、接口中已被重写的原方法：

```java
class SubClass extends SuperClass implements CompareA{
    
    public void mymethod(){
        method2();//重写之后的
        CompareA.super.method2();//接口中的原方法
        super.method2();//父类中的原方法
    }
    
    @Override
    public void method2() {
        System.out.println("重写之后的method2");
    }
}
```



```java
public class FF {
    public static void main(String[] args) {
        C c = new C();
        //C类 同时继承了父类B，又是接口A的实现类，但是调用接口A和父类B中的同名方法method时，
        //调用的是父类中的method方法----类优先原则。
        //仅限于方法，属性值不可以！
        c.method();
    }
}

class C extends B implements A {
    public void pX(){
        //编译不通过，X值不明确
        System.out.println(x);
//        System.out.println(super.x);  //调用父类x值，若多层父类，默认就近原则
//        System.out.println(A.x);  //调用接口中的x值，因为接口中的常量为全局常量，直接调用即可
    }
}
```



```java
interface A {
    int x = 0;
    default void method (){
        System.out.println("12345");
    }
}

class B{
    int x = 1;
    public void method (){
        System.out.println("sadfg");
    }
}
```



![接口](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210910202050232-16312764527592.png)



​	12、**接口的应用：代理模式（Proxy）**

​			**概述：**代理模式时Java开发中使用较多的一种设计模式，代理模式就是为了其他对象提供一种代理以控制对这个对象的访问。

​			**应用场景：**

​					**安全代理：**屏蔽对真是角色的直接访问。

​					**远程代理：**通过代理类处理远程方法调用（RMI）。

​					延迟加载：先加载轻量级的代理对象，真正需要时再加载真实对象，比如你要开发一个大文档查看软件，大文档中有大的图片，有可能一个图片有100M，在打开文件时，不可能将所有的图片都显示出来，这样就可以使用代理模式，当需要查看图片时，使用Proxy来进行大图片的打开。

​			**分类：**

​						**静态代理**（静态定义代理类）

​						**动态代理**（动态生成代理类）

​								JDK自带的动态代理，需要反射等知识。

```java
public class StaticProxyTest {

   public static void main(String[] args) {
      RealStar realStar = new RealStar();
      Proxy s = new Proxy(realStar);
//    Star s = new Proxy(new RealStar());
      s.confer();
      s.signContract();
      s.bookTicket();
      s.sing();
      s.collectMoney();
   }
}

//接口-----规范------明星的一套流程
interface Star {
   void confer();// 面谈

   void signContract();// 签合同

   void bookTicket();// 订票

   void sing();// 唱歌

   void collectMoney();// 收钱
}
//被代理类 ---具体哪位明星
class RealStar implements Star {

   public void confer() {
   }

   public void signContract() {
   }

   public void bookTicket() {
   }

   public void sing() {
      System.out.println("我是周杰伦：歌唱《稻花香》");
   }

   public void collectMoney() {
   }
}

//代理类-----经纪人-----代理明星本人
class Proxy implements Star {
   private Star real;

   public Proxy(Star real) {
      this.real = real;
   }

   //代理类----经纪人做他能做的
   public void confer() {
      System.out.println("经纪人代理明星---面谈");
   }

   public void signContract() {
      System.out.println("经纪人代理明星---签合同");
   }

   public void bookTicket() {
      System.out.println("经纪人代理明星---订票");
   }

   //唱歌只能明星本人来，调用real.sing();
   public void sing() {
      real.sing();
   }

   public void collectMoney() {
      System.out.println("经纪人代理明星---收钱");
   }
}

-----------------------------运行结果
    经纪人代理明星---面谈
	经纪人代理明星---签合同
	经纪人代理明星---订票
	我是周杰伦：歌唱《稻花香》
	经纪人代理明星---收钱

```

#### 19、内部类

​		1、Java中允许将一个类A声明在另一个类B中，则A就是内部类，B就是外部类

​		2、内部类的分类：成员内部类（静态、非静态）  vs  局部内部类（方法内、代码块内、构造器内）

​		3、成员内部类：

​					一方面：作为外部类的成员：

​								>  可以调用外部类的结构

​								>  可以被static 修饰

​								>  可以被4种不同的权限修饰（public、protected、缺省、private）

​					另一方面：作为一个类：

​								>  类内可以定义、属性、构造器、方法

​								>  可以用final修饰，表示此类不能被继承，没有final就可以被继承；

​								>  可以被abstract修饰，就不能被实例化。

​		4、关注以下3个问题

###### 				4.1、如何实例化成员内部类的对象

```java
public class InnerClassTest {
    public static void main(String[] args) {
        //创建Dog实例（静态的成员内部类）
        Person.Dog dog = new Person.Dog();

        //创建Brid实例（非静态的成员内部类）
        Person p = new Person();
        Person.Brid brid = p.new Brid();

    }
}

class Person{
    //静态成员内部类
    static class Dog{

    }

    //非静态成员内部类
    class Brid{

    }
}
```

###### 				4.2、如何在成员内部类中区分调用外部类的结构

```java
class Person{
    String name = "小明";

    //非静态成员内部类
    class Brid{
        String name = "鹦鹉";

        public void display(String name){
            System.out.println(name);//形参传入的name值
            System.out.println(this.name);//Brid类的name----鹦鹉
            System.out.println(Person.this.name);//Person类的name----小明
        }
    }
}
```

###### 				4.3、开发中局部内部类的使用

```java
public class InnerClassTest1 {
    
    //开发中很少见
    public void method(){
        //局部内部类
        class AA{
            
        }
    }
    
    //返回一个实现了Comparable接口的类的对象
    public Comparable getComparable(){
        
        //创建一个实现了Comparable接口的类：局部内部类
        //方式一：
//        class MyComparable implements Comparable{
//
//            @Override
//            public int compareTo(Object o) {
//                return 0;
//            }
//            
//        }
//        return new MyComparable();
        
        //方式二:匿名内部类
        return new Comparable() {
            @Override
            public int compareTo(Object o) {
                return 0;
            }
        };
    }
}
```

###### 总结注意：成员内部类和局部内部类，在编译以后，都会生成字节码文件

1、格式：成员内部类：外部类名$内部类名.class

​			局部内部类：外部类名$序号数字  内部类名.class   （主要是防止重名，前边会带序号123456...）

2、因为内部类外部类都会生成字节码文件，此时内部类调用外部类的属性，外部类给的是副本，不允许修改

而且外部类局部变量必须是final类型，JDK7之前不允许省略，以后的版本可以省略，但是还是final类型

```java
public class InnerClassTest3 {
    public void method(){
        //局部变量
        int num = 10;//省略了final，JDK7之前不能省略
        
        class AA {
            public void show(){
                
                //使用外部类的局部变量没问题
                System.out.println(num);
                
                //但是不能赋值,因为外部类的局部变量必须必须必须是final类型
                //num = 20;
            }
        }
    }
}
```



#### 20、异常处理

**异常：**在Java语言中，将程序执行过程中发生的不正常情况称为"异常"。（开发过程中的语法错误和逻辑错误不是异常）

##### 1、Java程序在执行过程中所发证的异常事件可以分为两类：

​		**Error：**Java虚拟机无法解决的严重问题。

​					如：JVM系统内部错误、资源耗尽等严重情况。比如：StackOverflowError和OOM。一般不编写针对性的代码进行处理。

​		**Exception：**其他因编程错误或者偶然的外在因素导致的一般性问题，可以使用针对性的代码进行处理。

​					例如：空指针访问、试图读取不存在的文件、网络连接中断、数组角标越界。



> 对于这些错误，一般有两种解决办法：一是遇到错误就终止程序的运行。另一种方式是由程序员在编写程序时，就考虑到错误的检测、错误消息的提示，以及错误的处理。

> 捕获错误最理想的时间是在编译期间，但有的错误只有在运行时才会发生。比如：除数为0，数组下标越界等。



Exception主要分为两类：**编译时异常(checked)**和**运行时异常(unchecked)**

![image-20210910191155964](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210910202712372-16312768343653.png)



##### 2、异常处理方式一：try-catch-finally

​		Java提供的是异常处理的**抓抛模型**。

​		Java程序的执行过程中如出现异常，会生成一个异常类对象，该异常对象将被提交给Java运行时系统，这个过程称为抛出（throw）异常。

​		异常对象的生成

​				由虚拟机**自动生成**：程序运行过程中，虚拟机检测到程序发生了问题，如果在当前代码中没有找到相应的处理程序，就会在后台自动创建一个对应异常类的实例对象并抛出-----自动抛出

​				由于开发人员**手动创建**：Exception exception = new ClassCastException();-------创建好的异常对象不抛出对程序没有任何影响，和创建一个普通对象一样

```java
//手动抛出！throw
public class ExceptionTest3 {
    public static void main(String[] args) {
        Student stu = new Student();
        try{
            stu.regist(-9);
        }catch(Exception e){
            System.out.println(e.getMessage());
        }
    }
}

class Student{
    private int id;

    public  void regist(int id) throws Exception {
        if (id > 0){
            this.id = id;
        }else{
            throw new Exception("您输入的数据非法，铁蛋！");
            //Exception包括编译时异常，所以需要throws上报异常。
            
            
            //throw new RuntimeException("您输入的数据非法，铁蛋！");
            //运行时异常不需要在regist方法处用throws上报。
        }
    }
}
```



![image-20210910202050232](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210910203913675-16312775555924.png)

> 如果一个方法内抛出异常，该异常对象会被抛给调用者方法中处理。如果异常没有在调用者方法中处理，它继续抛给这个调用方法的上层方法，这个过程将一直继续下去，知道异常被处理。这一过程称为**捕获（catch）异常**。

> 如果一个异常回到main()方法，并且main()也不处理，则程序运行终止。

> 程序员通常只能处理Exception，而对Error无能为力。

异常处理是通过try-catch-finally语句实现的。

![image-20210910202712372](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210910191155964-16312723211001.png)

​							e是异常类得实例变量

> **try**
>
> ​		捕获异常的第一步是用try{...}语句块选定捕获异常的范围，将可能出现的异常的代码放在try语句块中。

> **catch(Exceptiontype e)**
>
> ​		在catch语句块中是对异常对象进行处理的代码。每个try语句块可以伴随一个或者多个catch语句，用于处理可能产生的不同类型的异常现象。
>
> ​		1、如果明确知道产生的是何种异常，可以用该异常类作为catch的参数：也可以用其父类作为catch的参数。
>
> ​		2、一旦try中的异常对象匹配到某个catch时，就进入catch中进行异常处理，一旦处理完成，就跳出当前try-catch结构（在没有写finally的情况下），继续执行后序代码
>
> ​		3、catch中的异常类型如果没有子父类关系，则声明谁在上在下无所谓
>
> ​			  catch中异常类型满足子父类关系，则要求子类声明在上，父类声明在下。否则报错
>
> ```java
> public void test3(){
>     Object obj = new Date();
>     try{
>         String str = (String)obj;
>     }catch(ClassCastException e){
>         System.out.println("类型转换异常！");
>     }catch(Exception e){                        //Exception父类，放在最底下
>         System.out.println("父类对象！");
>     }
>     System.out.println("跳出try-catch结构，继续执行");
> }
> ---------------------执行结果
>     类型转换异常！
> 	跳出try-catch结构，继续执行
> 
> ```
>
> 比如：可以用ArithmeticException类作为参数的地方，就可以用RuntimeException类作为参数，或者用所有2异常的父类Exception类作为参数。但不能是与ArithmeticException类无关的异常类，如MulPointerException（catch中的语句将不会执行）。
>
> ​		4、捕获异常的有关信息：与其他对象一样，可以访问一个异常对象的成员变量或者调用它的方法。
>
> getMessage()    获取异常信息，返回字符串
>
> printStackTrace()    获取异常类名和异常信息，以及异常出现在程序中的位置，返回值void
>
> ​		5、在try结构中声明的变量，出了try结构以后，就不能再被调用。；想用可以在外边声明，try内部直接赋值使用
>
> ​		6、使用try-catch-finally处理编译时异常，是使得程序不报错，但在运行时仍可能报错，相当于我们用try-catch-finally结构将编译时可能出现的异常，延迟到运行时出现。
>
> ​		7、try-catch结构可以嵌套
>
> ​		8、开发中，由于运行时异常比较常见，所以我们通常就不针对运行时异常编写try-catch-finally结构了，针对编译时异常，我们一定要考虑异常处理，要不然跑不起来啊！

![image-20210910203913675](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210911114640174-16313320015887.png)

​		

> **finally**
>
> ​		捕获异常的最后一步是通过finally语句为异常处理提供一个统一的出口，使得在控制流转到程序的其他部分以前，能够对程序的状态做统一的管理
>
> ​		**不论在try代码块中是否发生了异常事件，catch语句是否执行，catch语句是否有异常，catch语句是否有return，finally块中的语句都会被执行。**
>
> ​		>   finally语句和catch语句是任选的
>
> ​		>   finally中声明的是一定会被执行的代码，即使catch中又出现异常了，或者try中有return语句，再或者catch中有return语句，都要执行完finally语句再return，或者退出。
>
> ​		>   像数据库连接、输入输出流、网络编程Socket等资源、JVM是不能自动回收的，我们需要自己手动的进行资源的释放。此时的资源释放就需要声明在finally中。（换言之：不管有没有异常，退出之前必须释放资源）
>
> ![image-20210910204318303](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210911114612393-16313319743266.png)





##### 3、异常处理方式二：throws + 异常类型

> 声明抛出异常是Java中处理异常的第二种方式
>
> ​		如果一个方法（中的语句执行时）可能生成某种异常，但是并不能确定如何处理中异常，则此方法应显式的声明抛出异常，表明该方法将部队这些异常进行处理，而由该方法的调用者负责处理，异常代码后边的代码就不会执行了
>
> ​		在方法声明中用throws语句可以声明抛出异常的列表，throws后面的异常类型可以是方法中产生的异常类型，也可以是它的父类。
>
> ​		注意：若父类中存在throws + 异常类型A，则子类重写的方法中的throws + 异常类型B，B必须比A小
>
> **体会：**try - catch - finally：真正的将异常给处理掉了。
>
> ​			throws的方式，只是将异常抛给了方法的调用者，并没有解决异常，只是向上汇报。
>
> ```java
> import java.io.File;
> import java.io.FileInputStream;
> import java.io.FileNotFoundException;
> import java.io.IOException;
> 
> public class ExceptionTest2 {
>     public static void main(String[] args) {
>         try{
>             method1();
>         }catch(FileNotFoundException e){
>             e.printStackTrace();
>         }catch (IOException e){
>             e.printStackTrace();
>         }
>     }
> 
>     //仍不处理，继续返回main，此处也可以处理，也可以继续上报。
>     public static void method1() throws FileNotFoundException, IOException{
>         method2();
>     }
> 
>     //仍不处理，继续返回调用者method1，此处也可以处理，也可以继续上报。
>     public static void method2() throws FileNotFoundException, IOException{
>         method3();
>     }
>     //声明可能会出现的异常类型，不处理，返回调用者method2
>     public static void method3() throws FileNotFoundException, IOException {
>         File file = new File("hello.txt");
>         FileInputStream fis = new FileInputStream(file);
>         int data = fis.read();
>         while(data != -1){
>             System.out.println((char) data);
>             data = fis.read();
>         }
>         fis.close();
>     }
> }
> ```
>
> 

##### 4、开发中如何选择	try - catch - finally	和	throws	结构？

​		1、如果父类中被重写的方法没有用throws方式处理异常，则子类重写的方法中也不能使用throws，意味着如果子类重写父类的方法中存在异常，必须使用try - catch - finally方式处理；

​		2、执行的方法method中，又先后调用了另外的几个方法，而且这几个方法时递进关系执行的，建议这几个方法使用throws方式进行处理，同一汇报到method方法中，然后再method方法中考虑用try - catch - finally方式进行处理。

##### 5、如何自定义异常类？

​		1、继承于现有的异常结构：RuntimeException、Exception

​		2、提供全局常量：serialVersionUID

​		3、提供重载的构造器

```java
public class MyException extends Exception{

    static final long serialVersionUID = -3387516993124209999L;

    public MyException(){

    }
    public MyException(String messaage){
        super(messaage);
    }
}
```

##### 6、异常练习，包括自建异常类型

![image-20210911114612393](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210913160411387-16315202533978.png)

```java
public class EcmDef {
    public static void main(String[] args) {
        try{
            int a = Integer.parseInt(args[0]);
            int b = Integer.parseInt(args[1]);
            double result = ecm(a,b);
            System.out.println(result);
        }catch(NumberFormatException e){
            System.out.println("数据类型不一致");
        }catch(ArrayIndexOutOfBoundsException e){
            System.out.println("缺少命令行参数");
        }catch(ArithmeticException e){
            System.out.println("分母为0");
        }catch (EcDef e){
            System.out.println(e.getMessage());
        }

    }

    public static double ecm(int a, int b) throws EcDef {
        if (a < 0 || b < 0) {
            throw new EcDef("请勿输入负数！");
        }
        return a / b;
    }
}
```

```java
//自定义异常类型
//输入负数异常
public class EcDef extends Exception{
    static final long serialVersionUID = -3387516993124209909L;

    public EcDef(){

    }
    public EcDef(String message){
        super(message);
    }
}
```



##### 总结：

![image-20210911114640174](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210913215953983-16315415959209.png)



## 二、高级部分

### 1、多线程（Thread）

#### ①基本概念：

​		◆**程序（program）：**是为了完成特定任务、用某种语言编写的一组指令的集合。即指的**是一段静态的代码**，静态对象。

​		◆**进程（process）：**是程序的一次执行过程，或是**正在运行的一个程序**。是动态的过程：有它自身的产生、存在、消亡的过程。------生命周期

​		>如：运行中的QQ、运行中的MP3播放器

​		>**程序是静态的，进程是动态的**

​		>**程序作为资源的分配单位**，系统在运行时会为每个进程分配不同的内存区域

​		◆**线程（thread）：**进程可以进一步细化为线程，是程序内部的一条执行路径。

​		>若一个进程同一时间**并行**执行多个线程，就是支持多线程的

​		>**线程作为调度和执行的单位，每个线程拥有独立的运行栈和程序计数器（pc）**，线程切换的开销小

​		>一个进程中多个线程共享的内存单元/内存地址空间---->他们从同一对中分配对象，可以访问相同的变量和对象。这就使得线程间通信更简单、高效。但多个线程操作共享的系统资源可能就会带来**安全隐患**。

​		◆**单核CPU和多核CPU的理解：**

​		>单核CPU，其实就是一种假的多线程，因为在一个时间单元内，也只能执行一个线程的任务。例如：虽然有多车道，但是收费站只有一个工作人员在收费，只有收了费才能通过，那么CPU就好比收费人员，如果一个人不想交费，那么收费人员可以把它“挂起”（晾着他，等他想通了，准备好钱了，再去收费）。但是因为CPU时间单元特别短，因此感觉不出来。

​		>如果是多核的话，才能更好的发挥多线程的效率。

​		>一个Java应用程序java.exe，其实至少有三个线程：main（）主线程、gc（）垃圾回收线程、异常处理线程。当然如果发生了异常，会影响主线程。

​		◆**并行与并发：**

​		>并行：多个CPU同时执行多个任务。比如：多个人同时做不同的事。

​		>并发：一个CPU（采用时间片）同时执行多个任务。比如：秒杀、多个人做同一件事。



​		◆**使用多线程的优点：**

​		1、提高应用程序的响应。对图形化界面更有意义，可增强用户体验。

​		2、提高计算机系统CPU的利用率

​		3、改善程序结构。将既长又复杂的进程分为多个线程，独立运行，利于理解和修改。

​		**◆程序何时需要多线程：**

​		1、程序需要同时执行两个或者多个任务时

​		2、程序需要实现一些需要等待的任务时，如用户输入、文件读写操作、网络操作、搜索等

​		3、需要一些后台运行的程序时。

#### ②多线程的创建：

##### **方式一：**继承Thread类的方式

**步骤：**

>1、创建一个继承于Thread类的子类
>
>2、重写Thread类的run方法-------->此线程执行的操作声明在run方法中
>
>3、创建Thread类的子类对象
>
>4、通过此对象调用start方法-------->作用：①启动当前线程、②调用当前线程的run()方法



**问题一：**通过此对象直接调用run方法可以启动线程吗？

​            答：不可以！单纯调用了方法，没有启动多线程。start包括两个作用，启动多线程，调用run。

**问题二：**此对象再启动一个线程、遍历100以内的偶数可以吗？

​            答：不可以！需要从新new一个对象，新对象再调用start方法可以。



**练习一：遍历100以内的偶数**

```java
//遍历100以内的偶数

//1、创建一个继承于Thread类的子类
class MyThread extends Thread{
    //2、重写Thread类的run方法
    @Override
    public void run(){
        for (int i = 0; i < 100; i++) {
            if(i % 2 == 0){
                System.out.println(i);
            }
        }
    }
}

public class ThreadTest{
    public static void main(String[] args){
        //3、创建Thread类的子类对象
        MyThread myThread = new MyThread();
        //4、通过此对象调用start方法
        myThread.start();//①启动当前线程、②调用当前线程的run()方法
        
    }
}
```

**练习二：三个窗口卖100张票**

```java
/**
 * 使用继承Thread的方式
 * 创建三个窗口卖票，总票数是100张；
 * 
 * 因为只创建了三个window对象，所以100张票必须用static，要不然就是300张票
 * 不完善！存在线程安全问题。重票存在。
 * 通过同步代码块的方式解决了线程安全问题
 */

class Window extends Thread{
    private static int ticket = 100;
    private static Object obj = new Object();//此处因为main中new了三个Window对象，Object设置成static才能是一把锁
    @Override
    public void run(){
        while(true){
            synchronized (obj){
                if (ticket > 0){
                    System.out.println(getName() + ": 卖票，票号为：" + ticket);
                    ticket--;
                }else{
                    System.out.println(getName() + "票已经售空了！");
                    break;
                }
            }
        }
    }
}

public class ThreadMethodTest {
    public static void main(String[] args) {
        Window w1 = new Window();
        Window w2 = new Window();
        Window w3 = new Window();
        w1.setName("窗口一");
        w2.setName("窗口二");
        w3.setName("窗口三");
        w1.start();
        w2.start();
        w3.start();
    }
}
```







##### **方式二：**实现Runnable接口的方式

**步骤：**

>1、创建一个实现了Runnable接口的类
>
>2、实现类去实现Runnable中的抽象方法：run()
>
>3、创建实现类的对象
>
>4、将此对象作为参数传递到Thread类的构造器中，创建Thread类的对象
>
>5、通过Thread类的对象调用start();

```java
//1、创建一个实现了Runnable接口的类
class MyThread2 implements Runnable{

    //2、实现类去实现Runnable中的抽象方法：run()
    @Override
    public void run() {
        for(int i = 0;i < 100; i++){
            System.out.println(Thread.currentThread().getName() + "\t"+i);
            //currentThread()当前线程对象
        }
    }
}
public class ThreadTest2 {
    public static void main(String[] args) {
        //3、创建实现类的对象
        MyThread2 myThread2 = new MyThread2();
        //4、将此对象作为参数传递到Thread类的构造器中，创建Thread类的对象
        Thread t1 = new Thread(myThread2);
        //5、通过Thread类的对象调用start();
        t1.setName("我是线程一号：");
        t1.start();

        //再启动一个线程？不用new MyThread2
        Thread t2 = new Thread(myThread2);
        t2.setName("我是线程九十九号：");
        t2.start();
    }
}
```



* 1、创建一个实现了Runnable接口的类
* 2、实现类去实现Runnable中的抽象方法：run()
* 3、创建实现类的对象
* 4、将此对象作为参数传递到Thread类的构造器中，创建Thread类的对象
* 5、通过Thread类的对象调用start();
* 
* start()方法： ①启动线程、
* ​                         ②调用当前线程的run()-----此处为什么调用的是Thread？
* ​          因为源码中调用了Runnable类型的target的run(),恰好我们重写了接口Runnable的run()方法
* 
* **注意：**start()方法是启动当前对象线程，为什么是Thread对象的start()方法可以启动线程，也没有重写Thread类的run方法？？？？？
*              ​          答：此处Thread对象创建用了带参的构造器，传入的接口Runnable的实现类对象

```java
//Thread带参构造器源码如下：

public Thread(Runnable target) {
    init(null, target, "Thread-" + nextThreadNum(), 0);
}

//Thread的run()方法源码如下：   

//如果target不存在，执行此方法------若target存在，则执行target的run()方法

//target是Runnable接口的实现类，我们又重写了Runnable接口的run()方法，所以可以实现
@Override
public void run() {
    if (target != null) {
        target.run();
    }
}

```





**练习一：三个窗口卖100张票**

```java
/**
 * 使用实现Runnable接口的方式
 * 创建三个窗口卖100张票
 * 
 * 因为只创建了一个Sell对象，所以100张票不需要用static也可以
 * 
 * 不完善！存在线程安全问题。重票存在。
 * 方式一：同步代码块解决线程不安全问题。
 */

class Sell implements Runnable{
    private int ticket = 100;
    Object obj = new Object();
    @Override
    public void run(){
        while(true){
            synchronized(obj) {//直接放个this也行，因为只new了一个Sell对象，锁唯一 
                if (ticket > 0) {
                    System.out.println(Thread.currentThread().getName() + "售票：票号为：\t" + ticket);
                    ticket--;
                } else {
                    break;
                }
            }
        }
    }
}


public class SellTicket {
    public static void main(String[] args) {
        Sell sell = new Sell();
        //因为只创建了一个Sell对象，所以100张票不需要用static也可以

        Thread t1 = new Thread(sell);
        Thread t2 = new Thread(sell);
        Thread t3 = new Thread(sell);
        t1.setName("我是窗口一一一");
        t2.setName("我是窗口二二二");
        t3.setName("我是窗口三三三");
        t1.start();
        t2.start();
        t3.start();
    }
}
```



##### 比较创建线程的两种方式：

​	开发中：优先选择实现Runnable接口的方式

​	**原因：**1、实现的方式没有类的单继承性的局限性（就是说：用接口的方式，然后有需要还能继承其他的类，若用继承的方式，因为只能单继承，就被限制了）

​				2、实现的方式更适合来处理多个线程有共享数据的情况（只创建一个对象，共享数据不用static修饰也可以）

​	**联系：**源码中，Thread类也是接口Runnable的实现类

​	**相同点：**两种方法都需要重写run()方法，将要执行的逻辑声明在run()中。

​					目前两种方法都是调用Thread类中的start()方法。

```java
//源码
public
class Thread implements Runnable {
    /* Make sure registerNatives is the first thing <clinit> does. */
    private static native void registerNatives();
    static {
        registerNatives();
    }
```

##### 方式三：实现Callable接口----JDK5.0新增

**步骤：**

> 1、创建一个Callable接口的实现类
>
> 2、实现call方法，将次线程需要执行的操作声明在call()中
>
> 3、创建Callable接口实现类的对象
>
> 4、将次Callable接口实现类的对象作为参数传递到FutureTask构造器中，创建FutureTask的对象。
>
> 5、将FutureTask的对象作为参数传递到Thread类的构造器中，创建Thread对象，并调用start()方法。
>
> 6、获取Callable中call方法的返回值，也可以不获取。FutureTask对象.get()==返回值



**与Runnable接口相比、Callable功能更强大**

> 1、**call()相比run()方法，可以有返回值**
>
> 2、**call()方法可以抛出异常**
>
> 3、支持泛型的返回值
>
> 4、需要借助FutureTask类，比如获取返回值结果

**Future接口**

> 可以对具体的Runnable、Callable任务的执行结果进行取消、查询是否完成、获取结果等。
>
> FutureTask是Future接口的唯一实现类
>
> FutureTask同时实现了Runnable、Future接口。它既可以作为Runnable被线程执行，又可以作为Future得到Callable的返回值

```java
 //100以内偶数的和
import java.util.concurrent.Callable;
import java.util.concurrent.ExecutionException;
import java.util.concurrent.FutureTask;
//1、创建一个Callable接口的实现类
class NumThread implements Callable {
    //2、实现call方法，将次线程需要执行的操作声明在call()中
    @Override
    public Object call() throws Exception{
        int sum = 0;
        //100以内偶数的和
        for(int i = 1; i <= 100;i++){
            if (i % 2 ==0){
                sum +=i;
            }
        }
        return sum;
    }
}


public class ThreadNew {
    public static void main(String[] args) {
        //3、创建Callable接口实现类的对象
        NumThread numThread = new NumThread();
        //4、将次Callable接口实现类的对象作为参数传递到FutureTask构造器中，创建FutureTask的对象。
        FutureTask futureTask = new FutureTask(numThread);
        //5、将FutureTask的对象作为参数传递到Thread类的构造器中，创建Thread对象，并调用start()方法。
        new Thread(futureTask).start();

        try {
            //6、获取Callable中call方法的返回值，也可以不获取。
            //get()返回值即为FutureTask构造器参数Callable实现类（numThread）重写的call()的返回值
            Object sum = futureTask.get();//不需要返回值时，就不用get()
            System.out.println(sum);
        } catch (InterruptedException e) {
            e.printStackTrace();
        } catch (ExecutionException e) {
            e.printStackTrace();
        }
    }
}
```

##### 方式四：使用线程池---JDK5.0新增

**步骤：**

>1、提供指定线程数量的线程池
>
>​     ExecutorService service = Executors.newFixedThreadPool(20);
>2、执行指定的线程操作，需要提供实现Runnable接口或Callable接口实现类的对象
>​        service.execute(new Number());//该方法一般用于Runnable接口
>​        service.submit(Callable callable);//该方法一般用于Callable接口，有返回值
>
>3、关闭连接池
>		service.shutdown();//关闭连接池

```java
import java.util.concurrent.Executors;
class Number implements Runnable{
    @Override
    public void run(){
        for(int i = 0;i < 1000;i++){
            System.out.println(Thread.currentThread().getName() + ":\t" +i);
        }
    }
}


public class ThreadPool {
    public static void main(String[] args) {
        //1、提供指定线程数量的线程池
        ExecutorService service = Executors.newFixedThreadPool(20);//定义线程池线程个数
        //2、执行指定的线程操作，需要提供实现Runnable接口或Callable接口实现类的对象
        service.execute(new Number());//该方法一般用于Runnable接口
//        service.submit(Callable callable);//该方法一般用于Callable接口，有返回值

        //3、关闭连接池
        service.shutdown();//关闭连接池
    }
}
```

**如何设置线程池属性：**

```java
//创建线程池，确定线程个数
ExecutorService service = Executors.newFixedThreadPool(20);
此时定义的ExecutorService是一个接口，它的实现类是ThreadPoolExecutor
    我们可以直接强转ThreadPoolExecutor t1 = (ThreadPoolExecutor)service;

然后通过实现类设置线程池属性
	t1.setCorePoolSize(100);
	t1.setKeepAliveTime();//等等
```



**背景：**

> 经常创建和销毁、使用量特别大的资源，比如并发情况下的线程，对性能影响很大

**思路：**

> 提前创建好多个线程，放入线程池中，使用时直接获取，使用完放回池中。可以避免频繁的创建销毁、实现重复利用。类似生活中的公共交通工具。

**好处：**

> 1、提法了响应速度（减少了创建新线程的时间）
>
> 2、降低资源消耗（重复利用线程池中的线程，不需要每次都创建）
>
> 3、便于线程管理
>
> ​		corePoolSize：核心线程池的大小
>
> ​		maximumPoolSize：最大线程数
>
> ​		keepAliveTime：线程没有任务时最多保持多长时间后会中止

![image-20210915110004109](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210915110004109-16316748051153.png)







#### ③Thread中的常用方法

* 1、start()：启动当前线程；调用当前线程的run()方法；
* 2、run()：通常需要重写Thread类中的此方法，将创建的线程要执行的操作声明在此方法中；
* 3、currentThread()：静态方法，返回当前代码执行的线程；
* 4、getName()：获取当前线程的名字；
* 5、setName()：设置当前线程的名字；
* 6、yield()：释放当前CPU的执行权；
* 7、join()：在线程A中，调用线程B的join()方法，此时线程A进入阻塞状态，知道线程B完全执行完成之后，线程A才结束阻塞状态。
* 8、stop()：已过时。执行此方法时，强制结束当前线程
* 9、sleep(long millitime)：让当前线程睡眠既定的millitime毫秒，在指定的millitime毫秒时间内，当前线程是阻塞状态。
* 10、isAlive()：判断当前线程是否存活，返回true或false。

#### ④线程的调度

**调度策略：**

​	>时间片：![image-20210913160411387](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210913220819719-163154210122910.png)

​	>抢占式：高优先级的线程抢占CPU

**Java的调度方法：**

​	>同优先级线程组成先进先出队列（先到先服务），使用时间片策略

​	>对高优先级，使用优先调度的抢占式策略



**线程的优先级 ：**

* 1、默认常量
* MAX_PRIORITY:10
* MIN_PRIORITY:1
* NORM_PRIORITY:5
* 2、如何获取和设置当前线程的优先级
*  获取：getPriority();
*  设置：setPriority();
*  **说明：**高优先级的线程要抢占低优先级线程的CPU执行权，但是知识从概率上讲，高优先级的线程高概率的情况下被执行，并不意味着只有当高优先级的线程全部执行完后，低优先级的线程才执行。



#### ⑤线程的生命周期

**JDK中用Thread.State类定义了线程的几种状态**

要想实现多线程，必须在主线程中创建新的线程对象。Java语言使用Thread类及其子类的对象来表示线程，在它的一个完整的生命周期中通常要经历如下的五种状态：

◆**新建：**当一个Thread类或其子类的对象被声明创建时，新生的线程对象处于新建状态。

◆**就绪：**处于新建状态的线程被start()后，将进入线程队列等待CPU时间片，此时它已经具备了运行的条件，只是没有分配到CPU资源。

◆**运行：**当就绪的线程被调度并获得CPU资源时，便进入运行状态，run()方法定义了线程的操作和功能。

◆**阻塞：**在某种特殊情况下，被认为挂起或执行输入输出操作时，让出CPU并临时中止自己的执行，进入阻塞状态。

◆**死亡：**线程完成了它的全部工作，或线程被提前强制性中止或出现异常导致结束

![image-20210913215953983](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210914183927208-16316159689471.png)



#### ⑥线程的同步

**同一把锁！！！！！！可以用类，类也是对象。**

问题提出：

​		多个线程执行的不确定性引起执行结果的不确定性。

​		多个线程对账本的共享，会造成操作的不完整性，会破坏数据。

![image-20210913220819719](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210915105918240-16316747599492.png)

在Java中，我们通过同步机制，来解决线程安全问题
* **方式一：同步代码块**

* 1、需要被同步的代码(别包多了代码，成单线程了)------即操作共享数据的代码

*    2、共享数据：多个线程共同操作的变量---如100张票

*    3、同步监视器（就是锁）：任何一个类的对象都有可以充当一个锁Object类也可以

*    **要求：多个线程必须要共用同一把锁。**

*    4、在实现Runnable接口创建多线程的方式中，我们可以考虑使用this充当监视器。

*    5、在继承Thread类创建多线程的方式中，慎用this充当同步监视器，考虑使用当前类充当同步监视器。

	

* **方式二：同步方法**

* 如果操作共享数据的代码完整个的声明在一个方法中，我们不妨将此方法声明成同步的

* 1、同步方法仍然涉及到同步监视器，只是不需要我们显式的声明

* 2、非静态的同步方法，同步监视器是：this

* 3、静态的同步方法，同步监视器是：当前类本身。（主要是继承Thread类创建多线程，因为继承Thread类要创建多个对象，通过设置方法为static静态的，形成一把锁的效果）

​	

​	

* **方式三：Lock锁----JDK5.0新增**

* ```java
	
	import java.util.concurrent.locks.ReentrantLock;//导包
	
	    private ReentrantLock lock = new ReentrantLock();//在run方法上边创建对象
	            try {
	               
	                lock.lock();//手动上锁
	                
	                //同步代码块
	            
	            }finally {
	                lock.unlock();//手动开锁
	            }
	```

​	

* **分析：**
* 同步的方式，解决了线程的安全问题-------好处
* 操作同步代码时，只能有一个线程参与，其他线程等待。相当于一个单线程的过程，效率低--------局限性
* 

```java
方式一：同步代码块
synchronized(同步监视器){
    //1、需要被同步的代码(别包多了代码，成单线程了)
}

方式二：同步方法
synchronized 方法名(){//默认同步监视器就是this

}

方式三：Lock锁----JDK5.0新增


import java.util.concurrent.locks.ReentrantLock;//导包

    private ReentrantLock lock = new ReentrantLock();//在run方法上边创建对象
	//继承的方式时，考虑加static，要不然lock就变成多把锁了
            try {
               
                lock.lock();//手动上锁
                
                //同步代码块
            
            }finally {
                lock.unlock();//手动开锁
            }
```

**面试题：**synchronized 与 lock的异同？？？

> 答：相同：二者都可以解决线程安全问题
>
> ​		不同：synchronized 机制在执行完相应的同步代码以后，自动释放同步监视器（锁）
>
> ​					lock需要手动的启动同步（lock（）方法），同时结束同步也需要手动实现（unlock（）方法）。



#### ⑦线程的死锁问题

**死锁：**

> 不同的线程分别占用对方需要的同步资源不放弃，都在等待对方放弃自己需要的同步资源，就形成了线程的死锁。
>
> 出现死锁后，不会出现异常，不会出现提示，只是所有的线程都处于阻塞状态，无法继续。

**解决办法：**

> 专门的算法、原则
>
> 尽量减少同步资源的定义
>
> 尽量避免嵌套同步

**死锁代码演示：**

A的foo方法传入形参b，内部要调用B的last方法，结束后才能释放锁A。

B的foo方法传入形参a，内部要调用A的last方法，结束后才能释放锁B。

导致A的foo方法拿不到锁B，无法执行last方法，也就无法释放锁A。同理锁B也无法释放，形成死锁。

```java
class A {
   public synchronized void foo(B b) {
      System.out.println("当前线程名: " + Thread.currentThread().getName()
            + " 进入了A实例的foo方法"); // ①
      try {
         Thread.sleep(200);
      } catch (InterruptedException ex) {
         ex.printStackTrace();
      }
      System.out.println("当前线程名: " + Thread.currentThread().getName()
            + " 企图调用B实例的last方法"); // ③
      b.last();
   }

   public synchronized void last() {
      System.out.println("进入了A类的last方法内部");
   }
}

class B {
   public synchronized void bar(A a) {
      System.out.println("当前线程名: " + Thread.currentThread().getName()
            + " 进入了B实例的bar方法"); // ②
      try {
         Thread.sleep(200);
      } catch (InterruptedException ex) {
         ex.printStackTrace();
      }
      System.out.println("当前线程名: " + Thread.currentThread().getName()
            + " 企图调用A实例的last方法"); // ④
      a.last();
   }

   public synchronized void last() {
      System.out.println("进入了B类的last方法内部");
   }
}

public class DeadLock implements Runnable {
   A a = new A();
   B b = new B();

   public void init() {
      Thread.currentThread().setName("主线程");
      // 调用a对象的foo方法
      a.foo(b);
      System.out.println("进入了主线程之后");
   }

   public void run() {
      Thread.currentThread().setName("副线程");
      // 调用b对象的bar方法
      b.bar(a);
      System.out.println("进入了副线程之后");
   }

   public static void main(String[] args) {
      DeadLock dl = new DeadLock();
      new Thread(dl).start();
      dl.init();
   }
}
```

#### ⑧线程的通信

 * 线程通信的三个方法：wait()、notify()、notifyAll()

 * 1、wait()----一旦执行此方法，当前线程进入阻塞状态，并释放同步监视器（释放锁）

 * 2、notify()----一旦执行此方法，就会唤醒被wait()的一个线程。如果多个线程被wait()，就会唤醒优先级较高的一个。

 * 3、notifyAll()----一旦执行此方法，就会唤醒所有被wait()的线程。

	![image-20210914183927208](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210915105838966-16316747214741.png)

	

 * **说明：**

 * 1、wait()、notify()、notifyAll()、这三个方法必须使用在，**同步代码块或者同步方法中**。

 * 2、wait()、notify()、notifyAll()、这三个方法的**调用者**必须是同步代码块或者同步方法中的**同步监视器**

	​       （就是充当锁那个对象，才能调用这三个方法）,否则就会出现IllegalMonitorStateException异常

 * 3、wait()、notify()、notifyAll()、这三个方法是**定义在java.lang.Object类**中，

	   （因为任何对象都能当锁，而只有锁才能调用这三个方法，所以任何对象都能调用这三个方法，只能是Object类）
	

例题：使用两个线程打印1-100.实现线程一和线程二交替打印。

```java
class Bank implements Runnable{
    private int num = 0;
    public void run(){
        while(true){
            synchronized(this){
                this.notify();

                if(num < 100) {
                    num += 1;
                    System.out.println(Thread.currentThread().getName() + "\t输出：\t" + num);

                    try {
                        this.wait();
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }

                }else{
                    break;
                }
            }
        }
    }
}


public class BankTest  {
    public static void main(String[] args) {
        Bank bank = new Bank();

        Thread t1 = new Thread(bank);
        Thread t2 = new Thread(bank);

        t1.setName("线程甲");
        t2.setName("线程乙");

        t1.start();
        t2.start();
    }
}
```



##### 线程通信的经典例题（生产者/消费者问题）

生产者（Productor）将产品交给店员（Clerk），而消费者（Customer）从店员处取走产品，店员一次只能持有固定数量的产品（比如20个），如果生产者试图生产更多产品，店员会叫生产者停一下，如果店中有空位放产品了再通知生产者继续生产；如果店中没有产品了，店员会告诉消费者等一下，如果店中有产品了再通知消费者来取走产品。

分析：

> 1、是否是多线程问题？是！生产者线程、消费者线程

> 2、是否有共享数据？有！店员（产品数量）

> 3、如何解决线程安全问题？同步机制，有三种方法

> 4、是否涉及到线程通信？是

```java
public class Clerk{//真正的同步代码段，下边两个类只是为了调用。

    private int productCount = 0;

    //消费产品
    public synchronized void coustomerProductor() {

        if (productCount > 0){
            System.out.println(Thread.currentThread().getName() + ":开始消费第" + productCount + "个产品");
            productCount--;
            notify();//生产者阻塞时，是产品满了，此时只要消费一个productCount--就可以notify唤醒
        }else{
            //等待
            try {
                wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }

    //生产产品
    public synchronized void producerProductor() {

        if (productCount < 20){
            productCount++;
            System.out.println(Thread.currentThread().getName() + ":开始生产第" + productCount + "个产品");
            notify();//消费者阻塞时，是产品卖没了，此时只要生产一个productCount++就可以notify唤醒
        }else{
            //等待
            try {
                wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

class Productor implements Runnable{//生产者

    private Clerk clerk ;

    public Productor(Clerk clerk){
        this.clerk = clerk;
    }

    @Override
    public void run(){
        System.out.println("开始生产产品。。。。");

        while(true){
            try{
                Thread.sleep(1);
            }catch(InterruptedException e){
                e.printStackTrace();
            }

            clerk.producerProductor();
        }
    }
}

class Customer implements Runnable{
    private Clerk clerk ;

    public Customer(Clerk clerk){
        this.clerk = clerk;
    }

    @Override
    public void run(){
        System.out.println("开始消费产品。。。。");

        while(true){
            try{
                Thread.sleep(10);
            }catch(InterruptedException e){
                e.printStackTrace();
            }

            clerk.coustomerProductor();
        }
    }
}
```



```java
public class ShopTest {
    public static void main(String[] args) {
        Clerk clerk = new Clerk();

        Thread p = new Thread(new Productor(clerk));
        Thread c = new Thread(new Customer(clerk));

        p.setName("生产者");
        c.setName("消费者");

        p.start();
        c.start();
    }
}
```



##### **释放锁的操作：**

![image-20210915105838966](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210910204318303-16312778009475.png)

**不会释放锁的操作：**

![image-20210915105918240](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210921174827666-16322177093124.png)



### 2、Java常用类

#### String类：

##### String类定义：

String：字符串，使用一对  “ ”引起来表示。

> 1、String声明为final的，不可被继承。
>
> 2、String实现了   Serializable接口：表示字符串是支持序列化的。
>
> ​                 实现了   Comparable接口：表示String是可以比较大小的。
>
> 3、String内部定义了final char[]  value用于存储字符串数据。
>
> 4、**String：代表了不可变的字符序列**。简称：**不可变性**。
>
> ​				体现：1、对字符串重新赋值时（s1 = "hello"），需要重写指定内存区域赋值，
>
> ​									不能使用原有的value进行赋值
>
> ​							2、当对现有的字符串进行连接操作时（s1 += "def"），也需要重写指定内存区域赋值，
>
> ​									不能使用原有的value进行赋值
>
> ​							3、当调用String的replace()方法修改指定字符或字符串时
>
> ​									（String s3 = s1.replace('a','m');//s3 = mbc），也需要重写指定内存区域赋值，
>
> ​									不能使用原有的value进行赋值
>
> 5、通过字面量的方式（区别于new方式）给一个字符串赋值，此时的字符串值声明在字符串常量池中。
>
> 6、字符串常量池中不会存储相同内容的字符串	
>
> ```java
> //1、
> String s1 = "abc";//字面量的定义方式，不用new
> String s2 = "abc";
> System.out.println(s1 == s2);//true地址值相等
> 
> //2、
> s1 = "hello";//此时不是把地址的“abc”改了，而是从新创建了个内存区
> //此时s2仍是原地址值，s1变成新的了
> 
> //3、
> s1 += "def";  //s1 = abcdef,但是也是从新创建的内存区域，原s2 = abc不变
>     
> //4、
> String s3 = s1.replace('a','m');//s3 = mbc
> ```



##### String的实例化：

方式一：通过字面量的方式

方式二：通过new + 构造器的方式

```java
	//通过字面量的方式：此时的s1和s2的数据abc声明在方法区中的字符串常量池中。
    String s1 = "abc";
    String s2 = "abc";

    //通过new + 构造器的方式：此时的s3和s4保存的地址值，是在数据的堆空间中开辟空间以后对应的对象地址值
    String s3 = new String("abc");
    String s4 = new String("abc");

    System.out.println(s1 == s2);//true
    System.out.println(s1 == s3);//false
    System.out.println(s3 == s4);//false两个对象，地址必定不同
}
```

![image-20210918225618198](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210918225618198.png)

**注意：**若定义时加了final修饰，此时s1就是常量  

```java
final String s1 = "hello";//因为加了final此时的s1其实就是一个常量。

String s4  = s1 + "world";
String s3 = "hello" + "world";

System.out.println(s3 == s4);//此时是true
```



##### String类的常用方法：

1、int length()： 返回字符串的长度： return value.length
2、char charAt(int index)： 返回某索引处的字符return value[index]
3、boolean isEmpty()： 判断是否是空字符串： return value.length == 0

```java
String str = " HELLO world ";

System.out.println(str.length());//13
System.out.println(str.charAt(0));//" "第一个空格
System.out.println(str.charAt(9));//r
System.out.println(str.isEmpty());//false
```

4、String toLowerCase()： 使用默认语言环境， 将 String 中的所有字符转换为小写
5、String toUpperCase()： 使用默认语言环境， 将 String 中的所有字符转换为大写

```java
String str = " HELLO world ";

String s1 = str.toLowerCase();//转换所有字符为---->小写
String s2 = str.toUpperCase();//转换所有字符为---->大写

System.out.println(s1);//" hello world "
System.out.println(s2);//" HELLO WORLD "
System.out.println(str);//" HELLO world "   不改变原值
```

6、String trim()： 返回字符串的副本， 忽略前导空白和尾部空白

```java
String str = " HELLO world ";

String s3 = str.trim();//去除字符串首尾空格
System.out.println(s3);//"HELLO world"
```

7、boolean equals(Object obj)： 比较字符串的内容是否相同
8、boolean equalsIgnoreCase(String anotherString)： 与equals方法类似， 忽略大小写

```java
String s1 = "HELLOWORLD";
String s2 = "helloworld";

System.out.println(s1.equals(s2));//false
System.out.println(s1.equalsIgnoreCase(s2));//true    忽略大写小写比较
```

9、String concat(String str)： 将指定字符串连接到此字符串的结尾。 等价于用“+”

```java
String s3 = s1.concat("降龙十八掌");//连接字符串，等价于 “+”
System.out.println(s3);//HELLOWORLD降龙十八掌
```

10、int compareTo(String anotherString)： 比较两个字符串的大小

```java
String s4 = "abc";//97、98、99
String s5 = new String("abg");//97、98、103
System.out.println(s4.compareTo(s5));//-4   遇到相等跳过，遇到不同作差，输出
String s6 = "aag";//97、97、103
System.out.println(s4.compareTo(s6));//1
```

11、String substring(int beginIndex)： 返回一个新的字符串， 它是此字符串的从beginIndex开始截取到最后的一个子字符串。
12、String substring(int beginIndex, int endIndex) ： 返回一个新字符串， 它是此字符串从beginIndex开始截取到endIndex(不包含)的一个子字符串。  

```java
String s7 = "降龙十八掌、六脉神剑、乾坤大挪移";
String s8 = s7.substring(6);//切片操作
String s9 = s7.substring(6,10);左闭右开[)

System.out.println(s8);//六脉神剑、乾坤大挪移
System.out.println(s9);//六脉神剑
```

13、boolean endsWith(String suffix)： 测试此字符串是否以指定的后缀结束

14、boolean startsWith(String prefix)： 测试此字符串是否以指定的前缀开始

15、boolean startsWith(String prefix, int toffset)： 测试此字符串从指定索引开始的子字符串是否以指定前缀开始  

```java
String s1 = "六脉神剑、九阳神功、一阳指";
boolean s2 = s1.startsWith("六");		//以xx开始
System.out.println(s2);//true

boolean s3 = s1.startsWith("九阳",5);		//从第index处 以xx开始
System.out.println(s3);//true

boolean s4 = s1.endsWith("指");			//以xx结束
System.out.println(s4);//true
```

16、boolean contains(CharSequence s)： 当且仅当此字符串包含指定的 char 值序列时，返回 true

```java
String s1 = "六脉神剑、九阳神功、一阳指";

String s5 = "九阳神功";
System.out.println(s1.contains(s5));//true
```

17、int indexOf(String str)： 返回指定子字符串在此字符串中第一次出现处的索引

18、int indexOf(String str, int fromIndex)： 返回指定子字符串在此字符串中第一次出现处的索引，从指定的索引开始
19、int lastIndexOf(String str)： 返回指定子字符串在此字符串中最右边出现处的索引

20、int lastIndexOf(String str, int fromIndex)： 返回指定子字符串在此字符串中最后一次出现处的索引，从指定的索引开始反向搜索
注： indexOf和lastIndexOf方法如果未找到都是返回-1  

```java
String s1 = "六脉神剑、九阳神功、一阳指";

System.out.println(s1.indexOf("神剑"));//2
System.out.println(s1.indexOf("神剑", 6));//-1
System.out.println(s1.lastIndexOf("神"));//7
System.out.println(s1.lastIndexOf("神", 5));//2
```

21、String replace(char oldChar, char newChar)： 返回一个新的字符串， 它是通过用 newChar 替换此字符串中出现的所有 oldChar 得到的。

22、String replace(CharSequence target, CharSequence replacement)： 使用指定的字面值替换序列替换此字符串所有匹配字面值目标序列的子字符串。

```java
String s1 = "六脉神剑、九阳神功、一阳指";
System.out.println(s1.replace("神", "鬼"));//六脉鬼剑、九阳鬼功、一阳指
```

23、String replaceAll(String regex, String replacement) ： 使用给定的replacement 替换此字符串所有匹配给定的正则表达式的子字符串。

```java
String str = "12hello34world5java7891mysql456";
//把字符串中的数字替换成 ","如果结果中开头和结尾有，的话去掉
String string = str.replaceAll("\\d+", ",").replaceAll("^,|,$", "");//正则表达式
System.out.println(string);
//hello,world,java,mysql
```

24、String replaceFirst(String regex, String replacement) ： 使用给定的replacement 替换此字符串匹配给定的正则表达式的第一个子字符串。

```java
String s1 = "六脉神剑、九阳神功、一阳指";
System.out.println(s1.replace("神", "鬼"));//六脉鬼剑、九阳鬼功、一阳指
String str = "1111AAAA2222BBBB999";
//把字符串中的数字替换成,，如果结果中开头和结尾有，的话去掉
String string = str.replaceFirst("\\d+", ",");
System.out.println(string);//,AAAA2222BBBB999
```

25、boolean matches(String regex)： 告知此字符串是否匹配给定的正则表达式。

```java
String str = "12345";
//判断str字符串中是否全部有数字组成，即有1-n个数字组成
boolean matches = str.matches("\\d+");
System.out.println(matches);//true


String tel = "0476-4534289";
//判断这是否是一个赤峰的固定电话
boolean result = tel.matches("0476-\\d{7,8}");
System.out.println(result);//true
```

26、String[] split(String rege	x)： 根据给定正则表达式的匹配拆分此字符串。

27、String[] split(String regex, int limit)： 根据匹配给定的正则表达式来拆分此字符串， 最多不超过limit个， 如果超过了， 剩下的全部都放到最后一个元素中。  

```java
String str = "hello|world|java";
String[] strs = str.split("\\|");
for (int i = 0; i < strs.length; i++) {
    System.out.print(strs[i] + "\t");
}
//hello	world	java
System.out.println();
String str2 = "hello.world.java";
String[] strs2 = str2.split("\\.",2);
for (int i = 0; i < strs2.length; i++) {
    System.out.print(strs2[i] + "\t");
}
//hello	world.java	
```



##### String类与其他结构之间的转换

###### 1、基本数据类型和String类

```java
 //基本数据类型、包装类---->String类型；
        //方法一：连接运算
        int num4 = 9;
        String str1 = num4 + "";
        System.out.println(str1);//"9"
        //方法二：调用String的valueOf(Xxx xxx)方法
        float f1 = 12.3f;
        String str2 = String.valueOf(f1);
        System.out.println(str2);//"12.3"

        //String类型---->基本数据类型、包装类；

        //调用包装类的parseXxx)
        String str3 = "123";
        int num5 = Integer.parseInt(str3);
        System.out.println(num5);//123
        System.out.println(str3);//"123"
```

###### 2、String类和char[]数组

String -------->>>char[]：调用String的toCharArray（）方法

```java
String str = "12ab";

char[] chars = str.toCharArray();
for (int i = 0; i < chars.length; i++) {
    System.out.println(chars[i]);
}
//1
//2
//a
//b
```

 char[]-------->>>String：调用String的构造器

```java
char[] arr = new char[]{'1','2','a','b'};
String str1 = new String(arr);
System.out.println(str1);
//12ab
```

###### 3、String类和byte[]数组

编码 ：String -------->>>byte[]：调用String的getBytes（）方法

```java
String str = "12ab天";

byte[] bytes = str.getBytes();//使用默认的字符集UTF-8，进行转换
System.out.println(Arrays.toString(bytes));
//[49, 50, 97, 98, -27, -92, -87]

byte[] bytes1 = new byte[0];//使用gbk字符集，进行编码
bytes1 = str.getBytes("GBK");
System.out.println(Arrays.toString(bytes1));
//[49, 50, 97, 98, -52, -20]
```

解码：byte[] -------->>>String：调用String的构造器

```java
String str2 = new String(bytes);
System.out.println(str2);
//12ab天

String str3 = new String(bytes1);
System.out.println(str3);
//12ab��   因为默认是utf-8，所以这个GBK会乱码

str4 = new String(bytes1,"GBK");//对其指定解码字符集，这时编码解码一致，不会乱码
System.out.println(str4);
//12ab天
```



##### String、StringBuffer、StringBuilder三者有何异同？

String：不可变的字符序列，底层结构使用char[]数组存储

StringBuffer：可变的字符序列，线程安全的，效率偏低；底层结构使用char[]数组存储

StringBuilder：可变的字符序列，JDK5.0新增，线程不安全，效率高些；底层结构使用char[]数组存储

**源码分析：**

```java
String str = new String();  //char[] value = new value[0];
String str1 = new String("abc");    //char[] value = new value[]{'a','b','c'};
StringBuffer sbf = new StringBuffer();  //char[] value = new value[16];底层创建了一个长度为16的空数组
StringBuffer sbf2 = new StringBuffer("abc");  //char[] value = new value["abc".length() + 16];底层创建了一个长度为3加16的空数组
sbf.append('a');//value[0] = 'a';
sbf.append('b');//value[1] = 'b';

    
```

**问题一：**sbf2.length()是多少？
    	      答：3，因为源码重写了length()方法。
**问题二：**扩容问题，如果要添加的数据底层数组装不下了，那就要扩容底层数组。
		      默认情况下，扩容为原来容量的2倍+2，同时将原有数组中的元素复制到新的数组中。

**开发习惯：**在开发中尽可能使用StringBuffer(int capacity)  或者 StringBuilder(int capacity)，可预见的情况下，直接定义数组长度capacity

**问题三：**String、StringBuffer、StringBuilder三者的效率谁高？

​				答：从高到低：StringBuilder  >  StringBuffer > String

​						StringBuffer需要考虑线程安全，用的同步方法，StringBuilder不考虑线程安全，所以StringBuffer比StringBuilder慢，String每次增加字符，都要重新创建，最慢。



#### StringBuffer类

##### 1、StringBuffer类的定义及创建

**StringBuffer：**可变的字符序列，线程安全的，效率偏低；底层结构使用char[]数组存储

**实例化：**

```java
StringBuffer sbf = new StringBuffer();  
//char[] value = new value[16];底层创建了一个长度为16的空数组
StringBuffer sbf2 = new StringBuffer("abc");  
//char[] value = new value["abc".length() + 16];底层创建了一个长度为3加16的空数组
```



##### 2、StringBuffer类的常用方法

1、StringBuffer append(xxx)：提供了很多的append()方法， 用于进行字符串拼接

```java
StringBuffer str = new StringBuffer("abc");
str.append("def");
System.out.println(str);//abcdef
```

2、StringBuffer delete(int start,int end)：删除指定位置的内容

```java
StringBuffer str = new StringBuffer("abcdef");
str.delete(1,3);
System.out.println(str);//adef
```

3、StringBuffer replace(int start, int end, String str)：把[start,end)位置替换为str

```java
StringBuffer str = new StringBuffer("abcdef");
str.replace(0,2,"B");
System.out.println(str);//Bcdef
```

4、StringBuffer insert(int offset, xxx)：在指定位置插入xxx

```java
StringBuffer str = new StringBuffer("abcdef");
str.insert(3,"A");
System.out.println(str);//abcAdef
```

5、StringBuffer reverse() ：把当前字符序列逆转  

```java
StringBuffer str = new StringBuffer("abcdef");
str.reverse();
System.out.println(str);//fedcba
```

6、public int indexOf(String str)：**返回**字符串所在位置索引

```java
StringBuffer str = new StringBuffer("abcdef");
int num = str.indexOf("bc");
System.out.println(num);//1
```

7、public String substring(int start,int end)：**返回**一个从start开始到end索引结束的左闭右开[ )区间的字符串

```java
StringBuffer str = new StringBuffer("abcdef");
String s1 = str.substring(2,5);//左闭右开
System.out.println(s1);//cde
```

8、public int length()：**返回**字符串长度

```java
StringBuffer str = new StringBuffer("abcdef");
int length = str.length();  //因为重写了length()方法，返回是有效长度，不是底层数组长度
System.out.println(length);//6
```

9、public char charAt(int n )：**返回**字符串索引为n的字符

```java
StringBuffer str = new StringBuffer("abcdef");
char ch = str.charAt(2);
System.out.println(ch);//c
```

10、public void setCharAt(int n ,char ch)：设置字符串索引n处的值为ch  

```java
StringBuffer str = new StringBuffer("abcdef");
str.setCharAt(1,'B');
System.out.println(str);//aBcdef
```



总结：

增：append（xxx）

删：delete（int start,int end）

改：setCharAt（int n, char ch）、replace（int start , int end,String str）

查：charAt（int n）

长度：length（）；

遍历：for   +    charAt（）、toString（）



#### Date类

##### 1、System类中的currentTimeMillis()

```java
long time = System.currentTimeMillis();
//返回当前时间与1970年1月1日0时0分0秒之间以毫米为单位的时间差
//称为时间戳
System.out.println(time);//1632041977923
```

##### 2、java.util.Date类【以及其子类java.sql.Date类】

> 1、两个构造器的使用
>
> ```java
> import java.util.Date;
> 
> //构造器一：Date()  创建一个对应当前时间的Date对象
> Date date1 = new Date();
> System.out.println(date1.toString());//Sun Sep 19 17:07:24 CST 2021
> System.out.println(date1.getTime());//1632042444401
> 
> //构造器二：Date()  创建指定毫秒数的Date对象
> Date date2 = new Date(16320424444L);
> System.out.println(date2);//Thu Jul 09 05:27:04 CST 1970
> ```
>
> 2、两个方法的使用
>
> ​	①toString()：显式当前的年、月、日、时、分、秒
>
> ​	②getTime()：获取当前时间Date对象对应的毫秒数，（时间戳）
>
> 3、java.sql.Date 对应着数据库中的日期类型的变量
>
> ​	①如何实例化
>
> ```java
> import java.sql.Date;
> 
> Date date3 = new Date(1632042444401l);
> System.out.println(date3.toString());//2021-09-19
> ```
>
> ​	②如何将java.util.Date对象转换称为java.sql.Date对象
>
> ```java
> import java.util.Date;
> //如何将java.util.Date对象转换称为java.sql.Date对象
> //情况一：//本身就是sql的Date创建的，直接强转
> Date date4 = new java.sql.Date(163204244440199l);
> java.sql.Date date5 = (java.sql.Date)date4;
> 
> //情况二：//获取时间戳，放到构造器中
> Date date6 = new Date();
> java.sql.Date date7 = new java.sql.Date(date6.getTime());
> ```

##### 3、SimpleDateFormat

1、两个操作：

> 1.1格式化：日期---->字符串  format（）方法
>
> 1.2解析：字符串---->日期  parse（）方法

2、SimpleDateFormat的实例化

```java
//一：实例化SimpleDateFormat:使用默认的构造器
SimpleDateFormat sdf = new SimpleDateFormat();

//格式化：日期 ----> 字符串   sdf.format(date)
Date date = new Date();
String format = sdf.format(date);
System.out.println(format);//21-9-20 下午3:45
//解析：字符串 ----> 日期   sdf.parse(str);
String str = "21-9-20 下午3:45";
Date date1 = sdf.parse(str);
System.out.println(date1);//Mon Sep 20 15:45:00 CST 2021

//二：指定构造器：日期格式可以自己定义
SimpleDateFormat sdf2 = new SimpleDateFormat("yyyy-MM-dd hh:mm:ss");

//格式化
String format1 = sdf2.format(date);
System.out.println(format1);
//解析:要求字符串必须符合SimpleDateFormat识别的格式（按照创建对象时构造器定义的形参格式）
Date date2 = sdf2.parse("2021-9-20 3:45:00");
System.out.println(date2);//Mon Sep 20 03:45:00 CST 2021
```

练习一：字符串"2021-09-09"转换成java.sql.Date类型的日期

```java
@Test
public void practice() throws ParseException {
    String birth = "2021-09-09";//字符串
    SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");//创建对象
    Date date = sdf.parse(birth);//转为日期，此时为java.util.Date
    java.sql.Date sqDate = new java.sql.Date(date.getTime());//创建java.sql.Date对象，并提供时间戳
    System.out.println(sqDate);//2021-09-09，实际调用了toString()方法
}
```



##### 4、Calender日历类的使用

Calender是一个抽象基类，主要用于完成日期字段之间相互操作的功能。

获取Calender实例的方法：

> 使用Calender.getInstance()方法
>
> 调用它的子类GregorianCalender的构造器
>
> **注意：**获取月份时：一月是0。十二月是11。
>
> 获取星期时：周日是1。周六是7。

```java
@Test
public void testCalender(){
    //1、实例化
    Calendar calender = Calendar.getInstance();

    //2、常用方法
    //get()
    int day = calender.get(Calendar.DAY_OF_MONTH);//原日历-2021年9月20日
    System.out.println(day);//本月的20天
    System.out.println(calender.get(Calendar.DAY_OF_YEAR));//本年的263天

    //set()---没有返回值，直接将Calender修改了
    calender.set(Calendar.DAY_OF_MONTH,5);  //设置为本月的第5天----9月5日
    day = calender.get(Calendar.DAY_OF_MONTH);//5
    System.out.println(day);
    
    //add()
    calender.add(Calendar.DAY_OF_MONTH,10);//也可以是负数，表示减去
    day = calender.get(Calendar.DAY_OF_MONTH);//15,因为加了10天
    System.out.println(day);
    
    //getTime()：日历类---->Date
    Date date = calender.getTime();//Wed Sep 15 17:06:14 CST 2021因为前边修改了，所以直立式9月15日
    System.out.println(date);
    
    //setTime():Date---->日历类
    Date date1 = new Date();//获取当前时间2021年9月20日
    calender.setTime(date1);//把时间给日历类
    day = calender.get(Calendar.DAY_OF_MONTH);//20,因为重新初始化了日历
    System.out.println(day);
}
```



##### 5、 LocalDateTime----（JDK8）

**新时间日期API**

> java.time – 包含值对象的基础包

> java.time.chrono – 提供对不同的日历系统的访问

> java.time.format – 格式化和解析时间和日期

> java.time.temporal – 包括底层框架和扩展特性

> java.time.zone – 包含时区支持的类  

LocalDate、 LocalTime、 LocalDateTime 类是其中较重要的几个类，它们的实例是不可变的对象，分别表示使用 ISO-8601日历系统的日期、时间、日期和时间。它们提供了简单的本地日期或时间，并不包含当前的时间信息，也不包含与时区相关的信息。
LocalDate代表IOS格式（yyyy-MM-dd）的日期,可以存储 生日、纪念日等日期。
LocalTime表示一个时间，而不是日期。
LocalDateTime是用来表示日期和时间的， 这是一个最常用的类之一。  

###### 两个实例化方法：

```java
@Test
public void test1(){
    //now()方法实例化---本地时间
    LocalDate localDate = LocalDate.now();
    LocalTime localTime = LocalTime.now();
    LocalDateTime localDateTime = LocalDateTime.now();

    System.out.println(localDate);//2021-09-20
    System.out.println(localTime);//17:25:36.242
    System.out.println(localDateTime);//2021-09-20T17:25:36.242

    //of()方法实例化----自定义时间，没有偏移量
    LocalDateTime localDateTime1 = LocalDateTime.of(2021, 9, 9, 15, 9, 59);
    System.out.println(localDateTime1);//2021-09-09T15:09:59
}
```

###### 获取、设置、增减时间操作：

```java
@Test
public void test1(){
    //getXxxx()获取时间
    System.out.println(localDateTime.getMonth());//SEPTEMBER
    System.out.println(localDateTime.getDayOfMonth());//20
    System.out.println(localDateTime.getMonthValue());//9

    //withXxxx()自定义时间，
    //有返回值区别于Calender
    //不改变原时间，不可变性
    LocalDateTime localDateTime2 = localDateTime.withDayOfMonth(15);
    System.out.println(localDateTime2);//2021-09-15 T17:38:04.683
    System.out.println(localDateTime);//2021-09-20 T17:38:04.683----本地时间未变

    // pulsXxx()增加年月日时分秒等
    // minusXxx()减去增加年月日时分秒等
    LocalDateTime localDateTime3 = localDateTime.plusDays(5);
    System.out.println(localDateTime3);//2021-09-25T17:41:05.763
    System.out.println(localDateTime);//2021-09-20T17:41:05.763----本地时间未变
    
}
```



##### 6、Instant----（JDK8）

```java
@Test
public void test2(){
    //now()获取本初子午线的标准时间
    Instant instant = Instant.now();
    System.out.println(instant);//2021-09-20T09:51:54.287Z  子午线处时间
    
    //atOffset()添加时区偏移量
    OffsetDateTime offsetDateTime = instant.atOffset(ZoneOffset.ofHours(8));
    System.out.println(offsetDateTime);//2021-09-20T17:51:54.287+08:00  东八区偏移8小时

    //toEpochMilli()获取自1970年1月1日0时0分0秒（UTC）开始的毫秒数
    long milli = instant.toEpochMilli();
    System.out.println(milli);//1632131690937

    //毫秒数反推时间Instant实例
    Instant instant1 = Instant.ofEpochMilli(milli);
    System.out.println(instant1);//2021-09-20T09:56:28.630Z 都是本初子午线的时间
}
```

##### 7、DateTimeFormatter:格式化或解析日期、时间

java.time.format.DateTimeFormatter 类：该类提供了三种格式化方法：

**预定义的标准格式。**如：ISO_LOCAL_DATE_TIME;ISO_LOCAL_DATE;ISO_LOCAL_TIME

**本地化相关的格式。**如： ofLocalizedDateTime(FormatStyle.LONG)

**自定义的格式。**如： ofPattern(“yyyy-MM-dd hh:mm:ss”)

| 方 法                      | 描 述                                                        |
| -------------------------- | ------------------------------------------------------------ |
| ofPattern(String pattern)  | 静 态 方 法 ， 返 回 一 个 指 定 字 符 串 格 式 的 DateTimeFormatter |
| format(TemporalAccessor t) | 格式化一个日期、 时间， 返回字符串                           |
| parse(CharSequence text)   | 将指定格式的字符序列解析为一个日期、 时间                    |



###### 方式一：预定义的标准格式。直接调用静态结构

```java
@Test
public void test3(){
    //方式一：预定义的标准格式。直接调用静态结构
    DateTimeFormatter formatter = DateTimeFormatter.ISO_LOCAL_DATE_TIME;
    //格式化：日期--->字符串
    LocalDateTime localDateTime = LocalDateTime.now();
    String str = formatter.format(localDateTime);
    System.out.println(str);//2021-09-20T18:37:55.397

    //解析：字符串--->日期
    TemporalAccessor parse = formatter.parse("2021-09-20T18:37:55.397");
    System.out.println(parse);//{},ISO resolved to 2021-09-20T18:37:55.397,格式不同因为调用了toString()方法
}
```

###### 方式二：本地化相关的格式一：ofLocalizedDateTime()

​    三种不同的输出格式:(适用于LocalDateTime)
​    FormatStyle.LONG:			2021年9月20日 下午06时44分36秒
​    FormatStyle.MEDIUM:		2021-9-20 18:45:09
​    FormatStyle.SHOT:				21-9-20 下午6:45

```java
DateTimeFormatter formatter1 = DateTimeFormatter.ofLocalizedDateTime(FormatStyle.SHORT);
//格式化：日期--->字符串
String str2 = formatter1.format(localDateTime);//调用上边结构new好的时间
System.out.println(str2);//21-9-20 下午6:45
//解析：字符串--->日期
TemporalAccessor parse1 = formatter1.parse("21-9-20 下午6:45");
System.out.println(parse1);
```

​		本地化相关的格式二：ofLocalizedDate()
​				四种不同的输出格式:(适用于LocalDate)
​				FormatStyle.LONG:				2021年9月20日
​				FormatStyle.MEDIUM:			2021-9-20
​				FormatStyle.SHOT:					21-9-20
​				FormatStyle.FULL：					2021年9月20日 星期一

###### 方式三（重点）：自定义格式。如：ofPattern("yyyy-MM-dd hh:mm:ss E")

```java
DateTimeFormatter formatter2 = DateTimeFormatter.ofPattern("yyyy-MM-dd hh:mm:ss");
//格式化：日期--->字符串
String str3 = formatter2.format(localDateTime);
System.out.println(str3);//2021-09-20 06:54:38
//解析：字符串--->日期
TemporalAccessor parse2 = formatter2.parse("2021-09-20 06:54:38");
System.out.println(parse2);//{HourOfAmPm=6, SecondOfMinute=38, MicroOfSecond=0, MinuteOfHour=54, NanoOfSecond=0, MilliOfSecond=0},ISO resolved to 2021-09-20
```



##### 8、其他日期API

###### **ZoneId：**

 该类中包含了所有的时区信息， 一个时区的ID， 如 Europe/Paris

```java
//ZoneId:类中包含了所有的时区信息
// ZoneId的getAvailableZoneIds():获取所有的ZoneId
Set<String> zoneIds = ZoneId.getAvailableZoneIds();
for (String s : zoneIds) {
System.out.println(s);
}
// ZoneId的of():获取指定时区的时间
LocalDateTime localDateTime = LocalDateTime.now(ZoneId.of("Asia/Tokyo"));
System.out.println(localDateTime);
```

###### **ZonedDateTime**：

 一个在ISO-8601日历系统时区的日期时间， 如 2007-12-03T10:15:30+01:00 urope/Paris。
其中每个时区都对应着ID， 地区ID都为“ {区域}/{城市}” 的格式， 例如：Asia/Shanghai等

```java
//ZonedDateTime:带时区的日期时间
// ZonedDateTime的now():获取本时区的ZonedDateTime对象
ZonedDateTime zonedDateTime = ZonedDateTime.now();
System.out.println(zonedDateTime);
// ZonedDateTime的now(ZoneId id):获取指定时区的ZonedDateTime对象
ZonedDateTime zonedDateTime1 = ZonedDateTime.now(ZoneId.of("Asia/Tokyo"));
System.out.println(zonedDateTime1);
```

###### **Clock：**

 使用时区提供对当前即时、 日期和时间的访问的时钟。

###### **Duration（持续时间）**： 

用于计算两个“时间” 间隔

```java
//Duration:用于计算两个“时间”间隔，以秒和纳秒为基准
LocalTime localTime = LocalTime.now();
LocalTime localTime1 = LocalTime.of(15, 23, 32);
//between():静态方法，返回Duration对象，表示两个时间的间隔
Duration duration = Duration.between(localTime1, localTime);
System.out.println(duration);
System.out.println(duration.getSeconds());
System.out.println(duration.getNano());
LocalDateTime localDateTime = LocalDateTime.of(2016, 6, 12, 15, 23, 32);
LocalDateTime localDateTime1 = LocalDateTime.of(2017, 6, 12, 15, 23, 32);
Duration duration1 = Duration.between(localDateTime1, localDateTime);
System.out.println(duration1.toDays());
```

###### **Period（日期间隔）**： 

用于计算两个“日期” 间隔

```java
//Period:用于计算两个“日期”间隔，以年、月、日衡量
LocalDate localDate = LocalDate.now();
LocalDate localDate1 = LocalDate.of(2028, 3, 18);
Period period = Period.between(localDate, localDate1);
System.out.println(period);
System.out.println(period.getYears());
System.out.println(period.getMonths());
System.out.println(period.getDays());
Period period1 = period.withYears(2);
System.out.println(period1);
```

###### **TemporalAdjuster :** 

时间校正器。有时我们可能需要获取例如：将日期调整到“下一个工作日”等操作。
**TemporalAdjusters :** 该类通过静态方法(firstDayOfXxx()/lastDayOfXxx()/nextXxx())提供了大量的常用TemporalAdjuster 的实现。  

```java
// TemporalAdjuster:时间校正器
// 获取当前日期的下一个周日是哪天？
TemporalAdjuster temporalAdjuster = TemporalAdjusters.next(DayOfWeek.SUNDAY);
LocalDateTime localDateTime = LocalDateTime.now().with(temporalAdjuster);
System.out.println(localDateTime);
// 获取下一个工作日是哪天？
LocalDate localDate = LocalDate.now().with(new TemporalAdjuster() {
@Override
public Temporal adjustInto(Temporal temporal) {
LocalDate date = (LocalDate) temporal;
if (date.getDayOfWeek().equals(DayOfWeek.FRIDAY)) {
return date.plusDays(3);
} else if (date.getDayOfWeek().equals(DayOfWeek.SATURDAY)) {
return date.plusDays(2);
} else {
return date.plusDays(1);
}
}
});
System.out.println("下一个工作日是： " + localDate);
```



##### 9、JDK8中新日期时间API与传统日期处理的转换

| 类                                                        | From 遗留类                 | To 遗留类                             |
| --------------------------------------------------------- | --------------------------- | ------------------------------------- |
| java.time.Instant与java.util.Date                         | date.toInstant()            | Date.from(instant)                    |
| java.time.Instant与java.sql.Timestamp                     | timestamp.toInstant()       | Timestamp.from(instant)               |
| java.time.ZonedDateTime与 java.util.GregorianCalendar     | cal.toZonedDateTime()       | GregorianCalendar.from(zonedDateTime) |
| java.time.LocalDate与java.sql.Time                        | date.toLocalDate()          | Date.valueOf(localDate)               |
| java.time.LocalTime与java.sql.Time                        | date.toLocalTime()          | Date.valueOf(localDate)               |
| java.time.LocalDateTime与 java.sql.Timestamp              | timestamp.toLocalDateTime() | Timestamp.valueOf(localDateTime)      |
| java.time.ZoneId与java.util.TimeZone                      | timeZone.toZoneId()         | Timezone.getTimeZone(id)              |
| java.time.format.DateTimeFormatter与 java.text.DateFormat | 无                          | formatter.toFormat()                  |



#### Java比较器

##### 一、说明：

> Java中的对象，正常情况下，只能进行比较： == 或者  ！=。不能使用  >  或 < 的。但是在开发场景中，我们需要对多个对象进行排序，言外之意，就需要比较对象的大小。
>
> 如何实现呢？ 使用**Comparable接口**【自然排序】   或者  **Comparator接口**【定制排序】

##### 二、Comparable接口的使用【自然排序】

* 1、像String、包装类等实现了Comparable接口，重写了compareTo(obj)方法，给出了比较两个对象大小的方法。
* 2、像String、包装类重写了compareTo()方法以后，进行了从小到大的排列
* 3、重写compareTo(obj)规则：
	* 如果当前对象this大于形参对象obj，则返回正整数，
	* 如果当前对象this小于形参对象obj， 则返回负整数，
	* 如果当前对象this等于形参对象obj， 则返回零。
* 4、实现Comparable接口的对象列表（和数组）可以通过 Collections.sort 或Arrays.sort进行自动排序。实现此接口的对象可以用作有序映射中的键或有序集合中的元素，无需指定比较器。  
* 5、对于自定义类来说，如果需要排序，我们可以让**自定义类实现Comparable接口**，**重写CompareTo(obj)方法**，在CompareTo(obj)方法中指明如何排序



**像String、包装类等已经重写了compareTo()方法，直接用**

>```java
>@Test
>public void test1(){
>    //像String、包装类等已经重写了compareTo()方法，直接用
>    String[] arr = new String[]{"AA","CC","KK","MM","JJ","DD"};
>    
>    Arrays.sort(arr);
>    System.out.println(Arrays.toString(arr));
>}
>```
>
>

**自定义类如果需要排序，我们可以让自定义类实现Comparable接口，重写CompareTo(obj)方法**

>```java
>@Test
>public void test2(){
>    Goods[] arrGoods = new Goods[4];
>    arrGoods[0] = new Goods("C铁蛋",999);
>    arrGoods[1] = new Goods("B金柱",8888);
>    arrGoods[2] = new Goods("A木头",999);
>    arrGoods[3] = new Goods("D丫蛋",777);
>    Arrays.sort(arrGoods);
>    System.out.println(Arrays.toString(arrGoods));
>}
>```
>
>**自定义类如下：**
>
>```java
>	public class Goods implements Comparable{
>    //属性
>    private String name;
>    private double price;
>    //构造器
>    public Goods(){
>
>    }
>    public Goods(String name,double price){
>        this.name = name;
>        this.price = price;
>    }
>    //方法
>    public void setName(String name){
>        this.name = name;
>    }
>    public void setPrice(double price){
>        this.price = price;
>    }
>    public String getName(){
>        return name;
>    }
>    public double getPrice(){
>        return price;
>    }
>    @Override
>    public String toString(){
>        return "Goods:{name: " + name + ",Price: " + price + "}";
>    }
>
>    //指明比较大小的方式:先按价格排序，同价位按名称均是由低到高
>    @Override
>    public int compareTo(Object o) {
>        if (o instanceof Goods){
>            Goods goods = (Goods) o;
>            if (this.price > goods.price){
>                return 1;
>            }else if (this.price < goods.price){
>                return -1;
>            }else{
>                return this.name.compareTo(goods.name);
>                //return -this.name.compareTo(goods.name); 
>                //在前边放一个符号，直接变成由高到低
>            }
>        }
>        throw new RuntimeException("传入数据类型不一致！");
>    }
>}
>```
>
>



##### 三、Comparator接口的使用【定制排序】

- 1、背景
	- 当元素的类型没有实现java.lang.Comparable接口而又不方便修改代码，或者实现了java.lang.Comparable接口的排序规则不适合当前的操作，那么可以考虑使用 Comparator 的对象来排序， 强行对多个对象进行整体排序的比较。
-  2、重写compare(Object o1,Object o2)方法，比较o1和o2的大小：
	- 如果方法返回正整数，则表示o1大于o2；
	- 如果返回0，表示相等；
	- 返回负整数，表示o1小于o2。   



**像String、包装类等已经重写了compareTo()方法，需要改变原方法**

>```java
>	@Test
>    public void test3(){
>        String[] arr = new String[]{"AA","CC","KK","MM","JJ","DD"};
>        
>        Arrays.sort(arr, new Comparator<String>() {
>            //按照字符串从大到小的顺序排列
>            @Override
>            public int compare(String o1, String o2) {
>                if (o1 instanceof String && o2 instanceof String){
>                    String s1 = (String) o1;
>                    String s2 = (String) o2;
>                    return -s1.compareTo(s2);//改成从大到小排
>                }
>                throw new RuntimeException("输入数据类型有误");
>            }
>        });
>        System.out.println(Arrays.toString(arr));
>    }
>```
>
>

**自定义类需要临时调整排序方法**

>```java
>@Test
>public void test4(){
>    Goods[] arrGoods = new Goods[4];
>    arrGoods[0] = new Goods("C铁蛋",999);
>    arrGoods[1] = new Goods("D金柱",8888);
>    arrGoods[2] = new Goods("A木头",999);
>    arrGoods[3] = new Goods("D丫蛋",777);
>    //原本已经重写了compaTo()方法，规则是：先按价格，再按名称，从低到高
>    //不改代码情况下，临时改变规则：先按名称，再按价格，从高到低
>    Arrays.sort(arrGoods, new Comparator<Goods>() {
>        @Override
>        public int compare(Goods o1, Goods o2) {
>            if (o1.getName().equals(o2.getName())){
>                return -Double.compare(o1.getPrice(),o2.getPrice());//从高到低
>            }else{
>                return -o1.getName().compareTo(o2.getName());//从高到低
>            }
>        }
>    });
>    System.out.println(Arrays.toString(arrGoods));
>}
>```
>
>

##### 四、二者区别

Comparable接口的方式一旦确定，保证Comparable接口的实现类的对象在任何位置都可以比较大小。

Comparator接口属于临时性的比较。



#### System类

System类代表系统，系统级的很多属性和控制方法都放置在该类的内部。该类位于java.lang包。
由于该类的构造器是private的，所以无法创建该类的对象，也就是无法实例化该类。其内部的成员变量和成员方法都是static的， 所以也可以很方便的进行调用。

**成员变量**
System类内部包含in、 out和err三个成员变量，分别代表标准输入流(键盘输入)，标准输出流(显示器)和标准错误输出流(显示器)。
**成员方法**

**1、native long currentTimeMillis()：**
该方法的作用是返回当前的计算机时间，时间的表达格式为当前计算机时间和GMT时间(格林威治时间)1970年1月1号0时0分0秒所差的毫秒数。

**2、void exit(int status)：**
该方法的作用是退出程序。其中status的值为0代表正常退出，非零代表异常退出。 使用该方法可以在图形界面编程中实现程序的退出功能等。  

**3、void gc()：**
该方法的作用是请求系统进行垃圾回收。至于系统是否立刻回收，则取决于系统中垃圾回收算法的实现以及系统执行时的情况。

**4、String getProperty(String key)：**
该方法的作用是获得系统中属性名为key的属性对应的值。系统中常见的属性名以及属性的作用如下表所示：  

![image-20210921094747753](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210921181344028-16322192256975.png)

```java
String javaVersion = System.getProperty("java.version");
System.out.println("java的version:" + javaVersion);

String javaHome = System.getProperty("java.home");
System.out.println("java的home:" + javaHome);

String osName = System.getProperty("os.name");
System.out.println("os的name:" + osName);

String osVersion = System.getProperty("os.version");
System.out.println("os的version:" + osVersion);

String userName = System.getProperty("user.name");
System.out.println("user的name:" + userName);

String userHome = System.getProperty("user.home");
System.out.println("user的home:" + userHome);

String userDir = System.getProperty("user.dir");
System.out.println("user的dir:" + userDir);
```



#### Math类

java.lang.Math提供了一系列静态方法用于科学计算。其方法的参数和返回值类型一般为double型。

| 函数                       | 作用                                  |
| -------------------------- | ------------------------------------- |
| abs                        | 绝对值                                |
| acos,asin,atan,cos,sin,tan | 三角函数                              |
| sqrt                       | 平方根                                |
| pow(double a,doble b)      | a的b次幂                              |
| log                        | 自然对数                              |
| exp                        | e为底指数                             |
| max(double a,double b)     | 两者取大                              |
| min(double a,double b)     | 两者取小                              |
| random()                   | 返回0.0到1.0的随机数                  |
| long round(double a)       | double型数据a转换为long型（四舍五入） |
| toDegrees(double angrad)   | 弧度—>角度                            |
| toRadians(double angdeg)   | 角度—>弧度                            |



#### BigInteger类

Integer类作为int的包装类，能存储的最大整型值为2^31-1， Long类也是有限的，最大为2^63-1。 **如果要表示再大的整数，不管是基本数据类型还是他们的包装类都无能为力，更不用说进行运算了。**

**java.math包的BigInteger可以表示不可变的任意精度的整数。** BigInteger 提供所有 Java 的基本整数操作符的对应物，并提供 java.lang.Math 的所有相关方法。

另外， BigInteger 还提供以下运算：模算术、 GCD 计算、质数测试、素数生成、位操作以及一些其他操作。

**1、构造器**
BigInteger(String val)： 根据字符串构建BigInteger对象  

**2、常用方法**
public BigInteger abs()：返回此 BigInteger 的绝对值的 BigInteger。

BigInteger add(BigInteger val) ：返回其值为 (this + val) 的 BigInteger

BigInteger subtract(BigInteger val) ：返回其值为 (this - val) 的 BigInteger

BigInteger multiply(BigInteger val) ：返回其值为 (this * val) 的 BigInteger

BigInteger divide(BigInteger val) ：返回其值为 (this / val) 的 BigInteger。整数相除只保留整数部分。

BigInteger remainder(BigInteger val) ：返回其值为 (this % val) 的 BigInteger。

BigInteger[] divideAndRemainder(BigInteger val)：返回包含 (this / val) 后跟(this % val) 的两个 BigInteger 的数组。

BigInteger pow(int exponent) ：返回其值为 (thisexponent) 的 BigInteger。  



#### BigDecimal类  

一般的Float类和Double类可以用来做科学计算或工程计算，但在商业计算中，**要求数字精度比较高，故用到java.math.BigDecimal类。**

BigDecimal类支持不可变的、任意精度的有符号十进制定点数。

**1、构造器**
public BigDecimal(double val)
public BigDecimal(String val)

**2、常用方法**

public BigDecimal add(BigDecimal augend)

public BigDecimal subtract(BigDecimal subtrahend)

public BigDecimal multiply(BigDecimal multiplicand)

public BigDecimal divide(BigDecimal divisor, int scale, int roundingMode)  



```java
public void testBigInteger() {
	BigInteger bi = new BigInteger("12433241123");//可定义任意长度
    BigDecimal bd = new BigDecimal("12435.351");
    BigDecimal bd2 = new BigDecimal("11");
    System.out.println(bi);//12433241123
    // System.out.println(bd.divide(bd2));报错，整除还行，不能整除要提供小数位。
    System.out.println(bd.divide(bd2, BigDecimal.ROUND_HALF_UP));//1130.486
    System.out.println(bd.divide(bd2, 15, BigDecimal.ROUND_HALF_UP));
    //15为小数,1130.486454545454545
}
```



### 3、枚举类（Enumeration）

#### 一、枚举类的使用

**1、类的对象只有有限个，确定的。** 

举例如下：

> 星期： Monday(星期一)、 ......、 Sunday(星期天)
> 性别： Man(男)、 Woman(女)
> 季节： Spring(春节)......Winter(冬天)
> 支付方式： Cash（现金）、 WeChatPay（微信）、 Alipay(支付宝)、 BankCard(银行卡)、 CreditCard(信用卡)
> 就职状态： Busy、 Free、 Vocation、 Dimission
> 订单状态： Nonpayment（未付款）、 Paid（已付款） 、 Delivered（已发货）、Return（退货）、 Checked（已确认） Fulfilled（已配货）、
> 线程状态：创建、就绪、运行、阻塞、死亡

**2、当需要定义一组常量时，强烈建议使用枚举类**  

**3、如果枚举类中只有一个对象，则可以作为单例模式的实现方式**

#### 二、如何定义枚举类

方式一：JDK5.0之前，自定义枚举类

```java
public class seasonTest {
    public static void main(String[] args) {
        Season spring = Season.SPRING;
        System.out.println(spring);
    }
}

//自定义枚举类
class Season{
    //1、声明Season对象的属性：private final 修饰
    private final String seasonName;
    private final String seasonDesc;

    //2、私有化类的构造器，并给对象属性赋值
    private Season(String seasonName,String seasonDesc){
        this.seasonName = seasonName;
        this.seasonDesc = seasonDesc;
    }

    //3、提供当前枚举类的多个对象：public static final 修饰
    public static final Season SPRING = new Season("春天","春暖花开");
    public static final Season SUMMER = new Season("夏天","夏日炎炎");
    public static final Season AUTUMN = new Season("秋天","秋高气爽");
    public static final Season WINTER = new Season("冬天","冰天雪地");

    //4、其他诉求：获取枚举类对象的属性
    public String getSeasonName() {
        return seasonName;
    }

    public String getSeasonDesc() {
        return seasonDesc;
    }

    @Override
    public String toString() {
        return "Season{" +
                "seasonName='" + seasonName + '\'' +
                ", seasonDesc='" + seasonDesc + '\'' +
                '}';
    }
}
```



方式二：JDK5.0,以后，可以使用enum关键字定义枚举类

说明：定义的枚举类默认继承于java.lang.Enum类，里面就不用重写toString()了，也可以自己改写

```java
public class seasonTest1 {
    public static void main(String[] args) {
        Season2 summer = Season2.SUMMER;
        System.out.println(summer);//SUMMER
    }
}

//enum关键字定义枚举类
//说明：定义的枚举类默认继承于java.lang.Enum类，里面就不用重写toString()了，也可以自己改写
enum Season2{
    //1、提供当前枚举类的对象，多个对象之间用逗号，隔开，末尾对象用;结束
    SPRING("春天","春暖花开"),
    SUMMER("夏天","夏日炎炎"),
    AUTUMN("秋天","秋高气爽"),
    WINTER("冬天","冰天雪地");
    //2、声明Season对象的属性：private final 修饰
    private final String seasonName;
    private final String seasonDesc;

    //3、私有化类的构造器，并给对象属性赋值
    private Season2(String seasonName,String seasonDesc){
        this.seasonName = seasonName;
        this.seasonDesc = seasonDesc;
    }

    //4、其他诉求：获取枚举类对象的属性
    public String getSeasonName() {
        return seasonName;
    }
    public String getSeasonDesc() {
        return seasonDesc;
    }
}
```



#### 三、Enum类的主要方法

1、values()方法：返回枚举类型的对象数组。该方法可以很方便地遍历所有的枚举值。

```java
Season2[] values = Season2.values();
for (int i = 0; i < values.length; i++) {
    System.out.println(values[i]);
} 
    //SPRING
    //SUMMER
    //AUTUMN
    //WINTER

```

2、valueOf(String str)：可以把一个字符串转为对应的枚举类对象。要求字符串必须是枚举类对象的“名字”。如不是，会有运行时异常：IllegalArgumentException。

```java
Season2 winter = Season2.valueOf("WINTER");
System.out.println(winter);
//WINTER
```

3、toString()：返回当前枚举类对象常量的名称  



#### 四、使用enum关键字定义的枚举类实现接口的情况

情况一：实现接口，在enum类中实现抽象方法

```java
interface Info{
    void show();
}

enum Season2 implements Info{
    //1、提供当前枚举类的对象，多个对象之间用逗号，隔开，末尾对象用;结束
    SPRING("春天","春暖花开"),
    SUMMER("夏天","夏日炎炎"),
    AUTUMN("秋天","秋高气爽"),
    WINTER("冬天","冰天雪地");
    //2、声明Season对象的属性：private final 修饰
    private final String seasonName;
    private final String seasonDesc;

    //3、私有化类的构造器，并给对象属性赋值
    private Season2(String seasonName,String seasonDesc){
        this.seasonName = seasonName;
        this.seasonDesc = seasonDesc;
    }
    //重写接口的抽象方法
    @Override
    public void show() {
        System.out.println("所有对象调用都是这一个方法");
    }
}
```

情况二：让枚举类的对象分别实现接口中的抽象方法【每个对象重写的抽象方法都不一样】

```java
interface Info{
    void show();
}

enum Season2 implements Info{
    //每个对象后边，单独重写show()方法
    SPRING("春天","春暖花开"){
        @Override
        public void show() {
            System.out.println("这是春天啊！");
        }
    },
    SUMMER("夏天","夏日炎炎"){
        @Override
        public void show() {
            System.out.println("这是夏天啊！");
        }
    },
    AUTUMN("秋天","秋高气爽"){
        @Override
        public void show() {
            System.out.println("这是秋天啊！");
        }
    },
    WINTER("冬天","冰天雪地"){
        @Override
        public void show() {
            System.out.println("这是冬天啊！");
        }
    };
    //2、声明Season对象的属性：private final 修饰
    private final String seasonName;
    private final String seasonDesc;

    //3、私有化类的构造器，并给对象属性赋值
    private Season2(String seasonName,String seasonDesc){
        this.seasonName = seasonName;
        this.seasonDesc = seasonDesc;
    }
}
```





### 4、注解(Annotation)

#### 一、理解Annotation：

①从 JDK 5.0 开始, Java 增加了对元数据(MetaData) 的支持, 也就是Annotation(注解)

②Annotation 其实就是代码里的特殊标记, 这些标记可以在编译, 类加载, 运行时被读取, 并执行相应的处理。通过使用 Annotation, 程序员可以在不改变原有逻辑的情况下, 在源文件中嵌入一些补充信息。 代码分析工具、开发工具和部署工具可以通过这些补充信息进行验证或者进行部署。

③Annotation 可以像修饰符一样被使用, 可用于**修饰包,类, 构造器, 方法, 成员变量, 参数, 局部变量的声明**, 这些信息被保存在 Annotation的 “name=value” 对中。  

④在JavaSE中，注解的使用目的比较简单，例如标记过时的功能，忽略警告等。在JavaEE/Android中注解占据了更重要的角色，例如用来配置应用程序的任何切面， 代替JavaEE旧版中所遗留的繁冗代码和XML配置等。  



#### 二、Annotation的使用示例

##### 示例一：生成文档相关的注解

>@author 标明开发该类模块的作者， 多个作者之间使用,分割
>@version 标明该类模块的版本
>@see 参考转向， 也就是相关主题
>@since 从哪个版本开始增加的
>@param 对方法中某参数的说明， 如果没有参数就不能写
>@return 对方法返回值的说明， 如果方法的返回值类型是void就不能写
>@exception 对方法可能抛出的异常进行说明 ， 如果方法没有用throws显式抛出的异常就不能写其中
>@param @return 和 @exception 这三个标记都是只用于方法的。
>@param的格式要求： @param 形参名 形参类型 形参说明
>@return 的格式要求： @return 返回值类型 返回值说明
>@exception的格式要求： @exception 异常类型 异常说明
>@param和@exception可以并列多个  
>
>```java
>/**
>* @author shkstart
>* @version 1.0
>* @see Math.java
>*/
>public class JavadocTest {
>	/**
>	* 程序的主方法，程序的入口
>	* @param args String[] 命令行参数
>	*/
>	public static void main(String[] args) {
>	}
>	/**
>	* 求圆面积的方法
>	* @param radius double 半径值
>	* @return double 圆的面积
>	*/
>	public static double getArea(double radius){
>		return Math.PI * radius * radius;
>	}
>}
>```
>
>

##### 示例二： 在编译时进行格式检查(JDK内置的三个基本注解)  

> **@Override:** 限定重写父类方法, 该注解只能用于方法
> **@Deprecated:** 用于表示所修饰的元素(类, 方法等)已过时。通常是因为所修饰的结构危险或存在更好的选择
> **@SuppressWarnings:** 抑制编译器警告  
>
> ```java
> public class AnnotationTest{
> 	public static void main(String[] args) {
> 		@SuppressWarnings("unused")
> 		int a = 10;//ieda中，定义了未使用，代码是灰色的，加上抑制警告后，就不是灰色了
> 	}
> 	@Deprecated//表示已经过时的方法，建议使用新的JDK方法
> 	public void print(){
> 		System.out.println("过时的方法");
> 	}
> 	@Override
> 	public String toString() {
> 		return "重写的toString方法()";
> 	}
> }
> ```
>
> 

##### 示例三： 跟踪代码依赖性，实现替代配置文件功能  

Servlet3.0提供了注解(annotation),使得不再需要在web.xml文件中进行Servlet的部署。

>  
>
> ```java
> @WebServlet("/login")
> public class LoginServlet extends HttpServlet {
> 	private static final long serialVersionUID = 1L;
> 	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws
> ServletException, IOException { }
> 	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws
> ServletException, IOException {
> 		doGet(request, response);
> 	} }
> ```
>
> ```java
> <servlet>
> <servlet-name>LoginServlet</servlet-name>
> <servlet-class>com.servlet.LoginServlet</servlet-class>
> </servlet>
> <servlet-mapping>
> <servlet-name>LoginServlet</servlet-name>
> <url-pattern>/login</url-pattern>
> </servlet-mapping>
> ```
>
> 

#### 三、如何自定义注解

参照SuppressWarnings:

1、定义新的 Annotation 类型使用 **@interface 关键字**
2、自定义注解自动继承了java.lang.annotation.Annotation接口
3、Annotation 的成员变量在 Annotation 定义中以无参数方法的形式来声明。 其方法名和返回值定义了该成员的名字和类型。 我们称为配置参数。 类型只能是八种**基本数据类型**、 **String类型**、 **Class类型**、 **enum类型**、 **Annotation类型**、以上所有类型的数组。
4、可以在定义 Annotation 的成员变量时为其指定初始值, 指定**成员变量的初始值可使用 default 关键字**
5、如果只有一个参数成员， 建议使用参数名为value
6、如果定义的注解含有配置参数， 那么使用时必须指定参数值， 除非它有默认值。 格式是“参数名 = 参数值” ， 如果只有一个参数成员， 且名称为value，可以省略“value=”
7、**没有成员定义的 Annotation 称为标记**; 包含成员变量的 Annotation 称为元数据 Annotation
**注意： 自定义注解必须配上注解的信息处理流程才有意义。**  

```java
/**
	1、注解声明为@interface
	2、内部定义成员，通常使用value表示		 String value();
	3、可以指定成员的默认值，使用default定义    String value() default "铁蛋";
	4、如果自定义注解没有成员，表明是一个标识作用

	注意：> 如果注解有成员，在使用注解时，需要指明成员的值。
		 > 自定义注解必须配上注解的信息处理流程（使用反射）才有意义。
		 > 自定义注解通常都会指明两个元注解：Retention（生命周期）、Target（使用范围）
*/
@MyAnnotation(value="金蛋")//使用自定义注解
public class MyAnnotationTest {
	public static void main(String[] args) {
		Class clazz = MyAnnotationTest.class;
		Annotation a = clazz.getAnnotation(MyAnnotation.class);
		MyAnnotation m = (MyAnnotation) a;
		String info = m.value();
		System.out.println(info);
	}
}
@Retention(RetentionPolicy.RUNTIME)//元注解：全程保留
@Target(ElementType.TYPE)//元注解TYPE：只能修饰类、接口、enum类
@interface MyAnnotation{//自定义注解
	String value() default "auguigu";
}
```



#### 四、JDK 提供的4种元注解

元注解：对现有的注解进行解释说明的注解

##### **Retention**

RetentionPolicy.SOURCE：在源文件中有效（即源文件保留），编译器直接丢弃这种策略的注释

RetentionPolicy.CLASS：在class文件中有效（即class保留） ， 当运行 Java 程序时, JVM不会保留注解。 这是默认值
RetentionPolicy.RUNTIME：在运行时有效（即运行时保留） ， 当运行 Java 程序时, JVM 会保留注释。程序可以通过反射获取该注释。  

```java
//源码
public enum RetentionPolicy{
	SOURCE,	//仅在源文件中有效
	CLASS,	//仅到编译文件中保留
	RUNTIME	//全程保留
}

@Retention(RetentionPolicy.SOURCE)
@interface MyAnnotation1{ }//自定义类

@Retention(RetentionPolicy.CLASS)
@interface MyAnnotation2{ }//自定义类

@Retention(RetentionPolicy.RUNTIME)
@interface MyAnnotation3{ }//自定义类
```

![image-20210921174451088](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210921174451088-16322174929533.png)





##### **Target**

指定被修饰的 Annotation(注解)能用于修饰哪些程序元素。 @Target 也包含一个名为 value 的成员变量。  

![image-20210921174827666](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210921181355969-16322192381326.png)

```java
//源码：
public enum ElementType {
    /** Class, interface (including annotation type), or enum declaration */
    TYPE,
    /** Field declaration (includes enum constants) */
    FIELD,
    /** Method declaration */
    METHOD,
    /** Formal parameter declaration */
    PARAMETER,
    /** Constructor declaration */
    CONSTRUCTOR,
    /** Local variable declaration */
    LOCAL_VARIABLE,
    /** Annotation type declaration */
    ANNOTATION_TYPE,
    /** Package declaration */
    PACKAGE,
    /**
     * Type parameter declaration
     *
     * @since 1.8
     */
    TYPE_PARAMETER,
    /**
     * Use of a type
     *
     * @since 1.8
     */
    TYPE_USE
}
```

```java
//使用
@Documented
@Target(ElementType.TYPE,ElementType.FIELD,ElementType.PACKAGE)
@Retention(RetentionPolicy.SOURCE)
@interface MyAnnotation1{ }//自定义类

@Target(ElementType.FIELD,ElementType.PACKAGE)
@Retention(RetentionPolicy.CLASS)
@interface MyAnnotation2{ }//自定义类

@Target(ElementType.PACKAGE)
@Retention(RetentionPolicy.RUNTIME)
@interface MyAnnotation3{ }//自定义类
```



##### **Documented**

用于指定被该元 Annotation 修饰的 Annotation 类将被javadoc 工具提取成文档。 默认情况下， javadoc是不包括注解的。

前提：**定义为Documented的注解必须设置Retention值为RUNTIME。**    

```java
//使用
@Documented
@Target(ElementType.TYPE,ElementType.FIELD,ElementType.PACKAGE)
@Retention(RetentionPolicy.SOURCE)
@interface MyAnnotation1{ }//自定义类
```

##### **Inherited**  

被它修饰的 Annotation 将具有继承性。如果某个类使用了被@Inherited 修饰的 Annotation, 则其子类将自动具有该注解。  

比如：如果把标有@Inherited注解的自定义的注解标注在类级别上，子类则可以继承父类类级别的注解
实际应用中，使用较少  

```java
//使用
@Inherited
@Documented
@Target(ElementType.TYPE,ElementType.FIELD,ElementType.PACKAGE)
@Retention(RetentionPolicy.SOURCE)
@interface MyAnnotation1{ }//自定义类
```



#### 五、通过反射获取注解信息



#### 六、JDK8 中注解的新特性

1、可重复性的注解：

> 在MyAnnoatation上声明@Repeatable，成员值为MyAnnotations.class
>
> MyAnnotation的Target 和Retention 和MyAnnotations相同

示列：

![image-20210921181344028](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210921181402587-16322192439397.png)

![image-20210921181355969](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210922211104848-16323162675518.png)

直接重复性写两个注解

![image-20210921181402587](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210923092624907-16323603863549.png)





2、可用于类型的注解   

JDK1.8之后，关于元注解@Target的参数类型ElementType枚举值多了两个：TYPE_PARAMETER  和 TYPE_USE。  

在Java 8之前， 注解只能是在声明的地方所使用， Java8开始， 注解可以**应用在任何地方**。

> ElementType.TYPE_PARAMETER	表示该注解能写在类型变量的声明语句中（如： 泛型声明） 。
> ElementType.TYPE_USE	 表示该注解能写在使用类型的任何语句中。  



```java
//修饰泛型
public class TestTypeDefine<@TypeDefine() U> {
	private U u;
	public <@TypeDefine() T> void test(T t){
	}
}
//Target必须使用ElementType.TYPE_PARAMETER
@Target({ElementType.TYPE_PARAMETER})
@interface TypeDefine{
}
```

```java
//修饰任何类型
@MyAnnotation//修饰类
public class AnnotationTest<U> {
	@MyAnnotation//修饰属性
	private String name;
	public static void main(String[] args) {
		AnnotationTest<@MyAnnotation String> t = null;//修饰泛型
		int a = (@MyAnnotation int) 2L;//修饰整型
		@MyAnnotation
		int b = 10;
	}
	public static <@MyAnnotation T> void method(T t) {
	}
	public static void test(@MyAnnotation String arg) throws @MyAnnotation Exception {
	}
}
//Target必须是ElementType.TYPE_USE
@Target(ElementType.TYPE_USE)
@interface MyAnnotation {
}
```

------

### 5、集合（Collection）

#### 一、集合框架的概述

>   1.集合、数组都是对多个数据进行存储操作的结构，简称Java容器
>
> ​	  说明：此时的存储，主要指的是内存层面的存储，不涉及到持久化的存储（.txt/.jpg/.avi/数据库中）
>
>   2.数组在存储多个数据方面的特点：
>
> ​	  ① 一旦初始化以后，其长度就确定了。
>
> ​	  ② 数组一旦定义好，其元素的类型也就确定了。我们也就只能操作指定类型的数据了。
>
> ​			比如：String[] arr;	 int[] arr1;	  Object[] arr3;
>
> 3. 数组在存储对个数据方面的缺点：
>
> 	① 一旦初始化以后，其长度就不可以更改了。
>
> 	② 数组中提供的方法非常有限，对于添加、删除、插入数据等操作，非常不便，同时效率不高。
>
> 	③ 获取数组中实际元素的个数的需求，数组没有现成的属性和方法可以调用
>
> 	④ 数组存储数据的特点：有序、可重复。对于无序、不可重复的需求，不能满足

#### 二、集合框架

**Java 集合可分为 Collection 和 Map 两种体系**

**Collection接口**： 单列数据， 定义了存取一组对象的方法的集合

​				List： 元素有序、可重复的集合---->	“动态”数组

​						   实现类：ArrayList、LinkesList、Vector

​				Set： 元素无序、不可重复的集合	

​						   实现类：HashSet、LinkedHashSet、TreeSet

**Map接口**： 双列数据，保存具有映射关系“key-value对”的集合

​					实现类：**HashMap、LinkedHashMap、TreeMap、Hashtable、properties  **

#### 三、Collection接口中的方法的使用

##### 1、 添加

​	add(Object obj)
​	addAll(Collection coll)

```java
Collection coll = new ArrayList();

//add(Object e):将元素e添加到集合coll中
coll.add("AA");
coll.add(123);//自动装箱
coll.add(new Date());

//addAll(Collection coll2): 将coll2中的元素添加到当前集合中
Collection coll2 = new ArrayList();
coll2.add(456);
coll2.add("BB");
coll.addAll(coll2);

System.out.println(coll.size());//5
System.out.println(coll);//[AA, 123, Wed Sep 22 12:54:47 CST 2021, 456, BB]
```

##### 2、 获取有效元素的个数

​	int size()

```java
Collection coll = new ArrayList();

//add(Object e):将元素e添加到集合coll中
coll.add("AA");
coll.add(123);//自动装箱
coll.add(new Date());

//size():获取添加的元素的个数
System.out.println(coll.size());//3

```

##### 3、 清空集合

​	void clear()

```java
//clear():清空集合元素
coll2.clear();
System.out.println(coll2);//[]空
```

##### 4、 是否是空集合

​	boolean isEmpty()

```java
//isEmpty():判断当前集合是否为空
System.out.println(coll.isEmpty());//false
System.out.println(coll2.isEmpty());//true
```

##### 5、 是否包含某个元素

​	boolean contains(Object obj)： 是通过元素的equals方法来判断是否是同一个对象
​	boolean containsAll(Collection c)： 也是调用元素的equals方法来比较的。 拿两个集合的元素挨个比较。  

```java
//contains(Object obj)
boolean tom = coll.add(new String("Tom"));
Boolean contains = coll.contains(123);//true
Boolean contains2 = coll.contains(new String("Tom"));//true
// 两个匿名对象返回true，是因为调用的是String中的equals方法，自定义类可以自己重写equals方法

//containsAll(Collection coll1)
Collection coll1 = Arrays.asList(123,456);
System.out.println(coll.containsAll(coll1));//true
```

##### 6、删除

​	boolean remove(Object obj) ： 通过元素的equals方法判断是否是要删除的那个元素。 只会删除找到的第一个元素
​	boolean removeAll(Collection coll)： 取当前集合的差集

```java
//remove(Object obj)
coll.remove(123);

//removeAll(Object obj)移除交集
coll.removeAll(coll1);
```

##### 7、取两个集合的交集

​	boolean retainAll(Collection c)： 把交集的结果存在当前集合中，不影响c

```java
//retainAll(Collection c)
coll.retainAll(coll1);
```

##### 8、 集合是否相等

​	boolean equals(Object obj) ：要想返回true，前提obj必须也是集合，集合存储的对象如果是ArraysList类，顺序不同，也会返回false

```java
coll.equals(coll1);
```

##### 9、 集合转成------->对象数组

​	Object[] toArray()

```java
//集合----->数组:
Object[] obj = coll.toArray();

//数组----->集合:调用Arrays类的静态方法asList()
List<String> list = Arrays.asList(new String[]{"AA","BB","CC"});

List arr1 = Arrays.asList(new int[]{123,456});//默认是一个对象
System.out.println(arr1.size());//1

List arr2 = Arrays.asList(new Integer[]{123,456});//包装类就会识别出两个
System.out.println(arr2.size());//2
```

##### 10、获取集合对象的哈希值

​	hashCode()

```java
System.out.println(coll2.hashCode());//1
System.out.println(coll1.hashCode());//5230
System.out.println(coll.hashCode());//-1904563705
```

##### 11、遍历

###### 	11.1	iterator()： 返回迭代器对象，用于集合遍历  

> Iterator对象称为迭代器(设计模式的一种)，主要用于遍历 Collection 集合中的元素。

> GOF给迭代器模式的定义为：提供一种方法访问一个容器(container)对象中各个元素，而又不需暴露该对象的内部细节。 迭代器模式，就是为容器而生。 类似于“公交车上的售票员”、“火车上的乘务员”、 “空姐” 。

> Collection接口继承了java.lang.Iterable接口，该接口有一个iterator()方法，那么所有实现了Collection接口的集合类都有一个iterator()方法，用以返回一个实现了Iterator接口的对象。

> Iterator 仅用于遍历集合， Iterator 本身并不提供承装对象的能力。如果需要创建Iterator 对象，则必须有一个被迭代的集合。

**集合对象每次调用iterator()方法都得到一个全新的迭代器对象，默认游标都在集合的第一个元素之前。**  

```java
@Test
public void test1(){
    Collection coll = new ArrayList();
    coll.add(123);
    coll.add(456);
    coll.add("Tom");
    coll.add(new Date());
    coll.add(false);

    Iterator iterator = coll.iterator();
    //方式一：
    System.out.println(iterator.next());//123
    System.out.println(iterator.next());//456
    System.out.println(iterator.next());//Tom
    System.out.println(iterator.next());//Wed Sep 22 20:40:05 CST 2021
    System.out.println(iterator.next());//false
    //System.out.println(iterator.next());//异常NoSuchElementException

    //方式二：
    for (int i = 0; i < coll.size(); i++) {
        System.out.println(iterator.next());
    }
-------------------------------------------------------*******************************************************
    //方式三：最常用写法！！！！！！！！！！！！！！！！！！！！！！！！！！
    while(iterator.hasNext()){
        System.out.println(iterator.next());
    }
}
```

错误方式：

```java
@Test
public void test1(){
    Collection coll = new ArrayList();
    coll.add(123);
    coll.add(456);
    coll.add("Tom");
    coll.add(new Date());
    coll.add(false);

    Iterator iterator = coll.iterator();
    
    //错误方式一：此时在while判断处下移了一次指针，导致跳跃输出，最后一次为空还会报异常NoSuchElementException
    while(iterator.next() != null){//判断不空继续
        System.out.println(iterator.next());
    }
    
    //错误方式二：每次返回一个新的Iterator对象，默认再第一个位置，永远输出第一个对象123，不会停止
    while(coll.iterator().hasNext()){//省略创建Iterator对象
        System.out.println(coll.iterator().next());
    }
}
```



**Iterator接口remove()方法**  

```java
Iterator iter = coll.iterator();//回到起点
while(iter.hasNext()){
	Object obj = iter.next();
	if(obj.equals("Tom")){
		iter.remove();
	}
}

//遍历
iter = coll.iterator();//再次回到起点，要不然指针还在结尾空指针处
while(iter.hasNext()){
    System.out.println(iter.next());
}
```

注意：
Iterator可以删除集合的元素， 但是是遍历过程中通过迭代器对象的remove方法， 不是集合对象的remove方法。
如果还未调用next()或在上一次调用 next 方法之后已经调用了 remove 方法，再调用remove都会报IllegalStateException。  

###### 11.2	使用 foreach 循环遍历集合元素  

> Java 5.0 提供了 foreach 循环迭代访问 Collection和数组。
>
> 遍历操作不需获取Collection或数组的长度，无需使用索引访问元素。
>
> 遍历集合的底层调用Iterator完成操作。
>
> foreach还可以用来遍历数组。  
>
> ![image-20210922211104848](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210923100230094-163236255184910.png)

```java
@Test
public void test2(){
    Collection coll = new ArrayList();
    coll.add(123);
    coll.add(456);
    coll.add("Tom");
    coll.add(new Date());
    coll.add(false);

    //for(集合元素的类型 局部变量 ： 集合对象){}也可以用来遍历数组，相应对象换成数组对象
    for (Object obj : coll){
        System.out.println(obj);
    }
    
    //for(数组元素的类型 局部变量 ： 数组对象){}
    int[] arr = new int[]{1,2,3,4,5};
    for (int i : arr){
        System.out.println(i);
    }
}
```



练习：程序输出结果？

```java
@Test
public void test3(){
    String[] str = new String[5];
    for (String myStr : str) {
        myStr = "atguigu";
        System.out.println(myStr);
    }
    for (int i = 0; i < str.length; i++) {
        System.out.println(str[i]);
    }
}
----------------------
钢蛋
钢蛋
钢蛋
钢蛋
钢蛋
null
null
null
null
null
```

#### 四、Collection子接口之一：List接口

##### 1、List实现类之一：ArrayList  

###### 1.1	List接口的框架

**Collection接口**： 单列数据， 定义了存取一组对象的方法的集合

​				List： 元素有序、可重复的集合---->	“动态”数组

​						   实现类：ArrayList、LinkesList、Vector

###### 1.2	List接口中的常见方法：

List除了从Collection集合继承的方法外， List 集合里添加了一些根据索引来操作集合元素的方法。

**void add(int index, Object ele):**在index位置插入ele元素

**boolean addAll(int index, Collection eles):**从index位置开始将eles中的所有元素添加进来

**Object get(int index):**获取指定index位置的元素

**int indexOf(Object obj):**返回obj在集合中首次出现的位置

**int lastIndexOf(Object obj):**返回obj在当前集合中末次出现的位置

**Object remove(int index):**移除指定index位置的元素，并返回此元素

**Object set(int index, Object ele):**设置指定index位置的元素为ele

**List subList(int fromIndex, int toIndex):**返回从fromIndex到toIndex位置的子集合  



增：add(int index, Object ele)

删：remove(int index)---按索引删除或者remove(Object obj)---按对象删除

改： set(int index, Object ele)

查：get(int index)

长度：size()

遍历：①Iterator	②增强for循环	③普通循环

##### 3、List实现类之二： LinkedList  

对于频繁的插入或删除元素的操作，建议使用LinkedList类，效率较高
新增方法：

> void addFirst(Object obj)
> void addLast(Object obj)
> Object getFirst()
> Object getLast()
> Object removeFirst()
> Object removeLast()  

LinkedList： 双向链表， 内部没有声明数组，而是定义了Node类型的first和last，用于记录首末元素。同时，定义内部类Node，作为LinkedList中保存数据的基本结构。 Node除了保存数据，还定义了两个变量：
	prev变量记录前一个元素的位置
	next变量记录下一个元素的位  

```java
private static class Node<E> {
	E item;
	Node<E> next;
	Node<E> prev;
	Node(Node<E> prev, E element, Node<E> next) {
		this.item = element;
		this.next = next;
		this.prev = prev;
	}
}
```



##### 4、List 实现类之三： Vector  

Vector 是一个古老的集合， JDK1.0就有了。大多数操作与ArrayList相同，区别之处在于Vector是线程安全的。

在各种list中，最好把ArrayList作为缺省选择。当插入、删除频繁时，使用LinkedList； Vector总是比ArrayList慢，所以尽量避免使用。  





#### 五、Collection子接口之二：Set接口

**Set接口的框架**

**Collection接口**： 单列数据， 定义了存取一组对象的方法的集合

​				**Set：** 元素无序、不可重复的集合	

​				 **实现类：** **HashSet：**作为Set接口的主要实现类；线程不安全的，可以存储null值；

​								**LinkedHashSet：**作为HashSet的子类，遍历其内部数据时，可以按照添加的顺序进行遍历

​								**TreeSet：**可以按照添加对象的指定属性，进行排序。

注意：Set 接口中没有额外定义新的方法，使用的都是Collection中声明的方法

**Set的理解**

**Set：** 元素无序、不可重复的集合

以HashSet为例说明：

> 1、无序性：不等于随机性，存储的数据在底层数组中并非按照数组索引的顺序添加而是根据数据的**哈希值**存储的。
>
> 2、不可重复性：保证添加的元素，按照equals方法判断时，不能返回true，即相同元素只能存一个。



3、添加元素的过程：以HashSet为例：



##### 1、Set实现类之一： HashSet 



- HashSet 是 Set 接口的典型实现，大多数时候使用 Set 集合时都使用这个实现类。
- HashSet 按 Hash 算法来存储集合中的元素，因此具有很好的存取、查找、删除性能。
- **HashSet 具有以下特点：**
	- 不能保证元素的排列顺序
	- HashSet 不是线程安全的
	- 集合元素可以是 null
- **HashSet 集合判断两个元素相等的标准：** 两个对象通过 hashCode() 方法比较相等，并且两个对象的 equals() 方法返回值也相等。
- 对于存放在Set容器中的对象， **对应的类一定要重写equals()和hashCode(Object obj)方法**，以实现对象相等规则。即： **“相等的对象必须具有相等的散列码”** 。  

- **向HashSet中添加元素的过程：**
	- 当向 HashSet 集合中存入一个元素时， HashSet 会调用该对象的 hashCode() 方法来得到该对象的 hashCode 值， 然后根据 hashCode 值， 通过某种散列函数决定该对象在 HashSet 底层数组中的存储位置。 （这个散列函数会与底层数组的长度相计算得到在数组中的下标， 并且这种散列函数计算还尽可能保证能均匀存储元素， 越是散列分布，该散列函数设计的越好）
	- 如果两个元素的hashCode()值相等， 会再继续调用equals方法， 如果equals方法结果为true， 添加失败； 如果为false， 那么会保存该元素， 但是该数组的位置已经有元素了，那么会通过链表的方式继续链接。
- 如果两个元素的 equals() 方法返回 true，但它们的 hashCode() 返回值不相等， hashSet 将会把它们存储在不同的位置，但依然可以添加成功。  

![image-20210923092624907](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210925095535418-16325349372521.png)

底层也是数组， 初始容量为16， 当如果使用率超过0.75， （16*0.75=12），就会扩大容量为原来的2倍。 （16扩容为32， 依次为64,128....等）  



**重写 hashCode() 方法的基本原则**  

- 在程序运行时，同一个对象多次调用 hashCode() 方法应该返回相同的值。
- 当两个对象的 equals() 方法比较返回 true 时，这两个对象的 hashCode()方法的返回值也应相等。
- 对象中用作 equals() 方法比较的 Field，都应该用来计算 hashCode 值。 

- **以自定义的Customer类为例，何时需要重写equals()？**
	当一个类有自己特有的“逻辑相等”概念,当改写equals()的时候，总是要改写hashCode()，根据一个类的equals方法（改写后），两个截然不同的实例有可能在逻辑上是相等的，但是， 根据Object.hashCode()方法，它们仅仅是两个对象。
- 因此，违反了“相等的对象必须具有相等的散列码”。
- 结论：**复写equals方法的时候一般都需要同时复写hashCode方法。 通常参与计算hashCode的对象的属性也应该参与到equals()中进行计算。**   



##### 2、Set实现类之二： LinkedHashSet 

- LinkedHashSet 是 HashSet 的子类
- LinkedHashSet 根据元素的 hashCode 值来决定元素的存储位置，但它同时使用双向链表维护元素的次序，这使得元素看起来是以插入顺序保存的。
- LinkedHashSet插入性能略低于 HashSet， 但在迭代访问 Set 里的全部元素时有很好的性能。
- LinkedHashSet 不允许集合元素重复。  

![image-20210923100230094](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210923100615598-163236277752411.png)



##### 3、Set实现类之三： TreeSet   

- TreeSet 是 SortedSet 接口的实现类， TreeSet 可以确保集合元素处于排序状态。
- **向TreeSet中添加数据，要求必须是相同类的对象，因为要用树排序，要不然没法比较。**
- TreeSet底层使用红黑树结构存储数据
- 新增的方法如下： (了解)
	- Comparator comparator()
	- Object first()
	- Object last()
	- Object lower(Object e)
	- Object higher(Object e)
	- SortedSet subSet(fromElement, toElement)
	- SortedSet headSet(toElement)
	- SortedSet tailSet(fromElement)
- TreeSet 两种排序方法： 自然排序和定制排序。默认情况下， TreeSet 采用自然排序。  

TreeSet和后面要讲的TreeMap采用红黑树的存储结构
特点：有序，查询速度比List快  

![image-20210923100615598](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210924104409797-163245145167812.png)



###### **排 序—自然排序（Comparable接口）：**  

**自然排序：** TreeSet 会调用集合元素的 compareTo(Object obj) 方法来比较元素之间的大小关系，然后将集合元素按升序(默认情况)排列
**如果试图把一个对象添加到 TreeSet 时，则该对象的类必须实现 Comparable接口。**

- 实现 Comparable 的类必须实现 compareTo(Object obj) 方法，两个对象即通过compareTo(Object obj) 方法的返回值来比较大小。
- Comparable 的典型实现：
	- BigDecimal、 BigInteger 以及所有的数值型对应的包装类：按它们对应的数值大小进行比较
	- Character：按字符的 unicode值来进行比较
	- Boolean： true 对应的包装类实例大于 false 对应的包装类实例
	- String：按字符串中字符的 unicode 值进行比较
	- Date、 Time：后边的时间、日期比前面的时间、日期大  

- 向 TreeSet 中添加元素时，只有第一个元素无须比较compareTo()方法，后面添加的所有元素都会调用compareTo()方法进行比较。
- **因为只有相同类的两个实例才会比较大小，所以向 TreeSet 中添加的应该是同一个类的对象。**
- 对于 TreeSet 集合而言，它**判断两个对象是否相等的唯一标准**是：**两个对象通过 compareTo(Object obj) 方法比较返回值，跟equals无关了。**
- 当需要把一个对象放入 TreeSet 中，重写该对象对应的 equals() 方法时，应保证该方法与 compareTo(Object obj) 方法有一致的结果：如果两个对象通过equals() 方法比较返回 true，则通过CompareTo(Object obj) 方法比较应返回 0。否则，让人难以理解。  

```java
public void test5(){
        TreeSet<Object> set = new TreeSet<>();
        set.add(new Person("Tom",15));
        set.add(new Person("铁蛋",10));
        set.add(new Person("金柱",99));
        set.add(new Person("翠花",18));
        set.add(new Person("狗蛋",25));
        set.add(new Person("狗蛋",38));


        Iterator iterator = set.iterator();
        while(iterator.hasNext()){
            System.out.println(iterator.next());
        }
//        for (Object i : set){
//            System.out.println(i);
//        }
    }
```

```java
public class Person implements Comparable{
    //属性
    private String name;
    private int age;
    //构造器
    public Person(){}
    public Person(String name,int age){
        this.name = name;
        this.age = age;
    }
    //方法
    public void setName(String name){
        this.name = name;
    }
    public void setAge(int age){
        this.age = age;
    }
    public String getName(){
        return name;
    }
    public int getAge(){
        return age;
    }
    @Override
    public String toString(){
        return "Person:{ name:" + name + " age:" + age + "}";
    }

    //按照姓名排序，从小到大，同名再按年龄从小到大
    @Override
    public int compareTo(Object o) {
        if (o instanceof Person){
            Person p = (Person)o;
//            return -this.name.compareTo(p.name);
            int compare = -this.name.compareTo(p.name);
            if(compare != 0){
                return compare;
            }else{
                return Integer.compare(this.age,p.age);
            }
        }else{
            throw new RuntimeException("输入类型不符！");
        }
    }
}
```

###### **排 序—定制排序（Comparator接口）：**  

- TreeSet的自然排序要求元素所属的类实现Comparable接口，如果元素所属的类没有实现Comparable接口，或不希望按照升序(默认情况)的方式排列元素或希望按照其它属性大小进行排序，则考虑使用定制排序。定制排序，通过Comparator接口来实现。 需要重写compare(T o1,T o2)方法。
- 利用int compare(T o1,T o2)方法，比较o1和o2的大小：
	- 如果方法返回正整数，则表示o1大于o2；
	- 如果返回0，表示相等；
	- 返回负整数，表示o1小于o2。
- 要实现定制排序，需要将实现Comparator接口的实例作为形参传递给TreeSet的构造器。
- 此时，仍然只能向TreeSet中添加类型相同的对象。否则发生ClassCastException异常。
- **使用定制排序判断两个元素相等的标准是：通过Comparator比较两个元素返回了0，跟equals无关了**。  

```java
@Test
public void test6(){
    Comparator com = new Comparator() {//创建Comparator对象，并制定比较方法
        @Override
        public int compare(Object o1, Object o2) {
            if (o1 instanceof Person && o2 instanceof Person){
                Person p1 = (Person)o1;
                Person p2 = (Person)o2;
                return Integer.compare(p1.getAge(),p2.getAge());
            }else{
                throw new RuntimeException("输入类型不符！");
            }

        }
    };

	//把Comparator对象做形参，给TreeSet构造器
    //不给的话，还是按照Person类中的默认方法进行排序
    TreeSet<Object> set = new TreeSet<>(com);
    set.add(new Person("Tom",15));
    set.add(new Person("铁蛋",10));
    set.add(new Person("金柱",99));
    set.add(new Person("翠花",18));
    set.add(new Person("狗蛋",25));
    set.add(new Person("狗蛋",38));

    Iterator ite = set.iterator();
    while(ite.hasNext()){
        System.out.println(ite.next());
    }
}
```



#### 六、Collection子接口之三：Map接口

**Map接口**： 双列数据，保存具有映射关系“key-value对”的集合

![image-20210925095535418](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210925210805868-16325752877424.png)

实现类：

**HashMap:**作为Map接口的主要实现类：线程不安全的，效率高；存储null的key和value

**LinkedHashMap:**保证在遍历map元素时，可以按照添加顺序实现遍历，

​							原因：在原有的HashMap底层结构基础上，添加了一对指针，指向一个前一个后

​							对于频繁的遍历操作，此类执行效率高于HashMap

**TreeMap:**保证按照添加的key-value对进行排序，实现排序遍历，此时使用key进行排序

​					底层使用红黑树

**Hashtable:**作为古老的实现类；线程安全的，效率低；不能存储null的key和value

​	**properties: **常用来处理配置文件，key和value都是String类型





**HashMap的底层：**数组＋链表（JDK7及以前）

​								数组＋链表＋红黑树（JDK8）



##### 1、Map结构的理解

Map中的key：无序的、不可重复的、使用Set存储所有的key----->

> 所以key所在的类要重写equals（）和hashCode（）方法（HashMap的话）

Map中的value：无序的，可重复的，使用Collection存储所有的value

> value所在的类要重写equals（）方法

一个键值对：key-value构成了一个Entry对象。

Map中的entry：无序的，不可重复的，使用Set存储所有的entry

![image-20210924104409797](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210926154109755-16326420713641.png)

##### 2、Map接口的常用方法

- 添加、 删除、修改操作：

	- Object put(Object key,Object value)：将指定key-value添加到(或修改)当前map对象中

	- void putAll(Map m):将m中的所有key-value对存放到当前map中

	- Object remove(Object key)：移除指定key的key-value对，并返回value

	- void clear()：清空当前map中的所有数据

	- ```java
		@Test
		public void test1(){
		    /**
		     * 添加、 删除、修改操作：
		     *
		     * - Object put(Object key,Object value)：将指定key-value添加到(或修改)当前map对象中
		     * - void putAll(Map m):将m中的所有key-value对存放到当前map中
		     * - Object remove(Object key)：移除指定key的key-value对，并返回value
		     * - void clear()：清空当前map中的所有数据
		     */
		    Map hashMap = new HashMap();
		    //添加
		    hashMap.put("金柱",123);
		    hashMap.put("铁蛋",456);
		    hashMap.put("翠花",888);
		    //修改---铁蛋的value为999
		    hashMap.put("铁蛋",999);
		    System.out.println(hashMap);//{金柱=123, 铁蛋=999, 翠花=888}
		
		    Map hashMap1 = new HashMap();
		    hashMap1.put("张无忌","九阳神功");
		    hashMap1.put("周芷若","九阴白骨爪");
		    hashMap1.put("乔峰","降龙十八掌");
		    hashMap.putAll(hashMap1);
		    System.out.println(hashMap);
		    //{金柱=123, 乔峰=降龙十八掌, 铁蛋=999, 周芷若=九阴白骨爪, 张无忌=九阳神功, 翠花=888}
		
		    Object removeMap = hashMap1.remove("乔峰");
		    System.out.println(removeMap);//降龙十八掌
		    System.out.println(hashMap1);//{周芷若=九阴白骨爪, 张无忌=九阳神功}
		
		    hashMap1.clear();
		    System.out.println(hashMap1);//{}
		}
		```

- 元素查询的操作：

	- Object get(Object key)：获取指定key对应的value
	- boolean containsKey(Object key)：是否包含指定的key
	- boolean containsValue(Object value)：是否包含指定的value
	- int size()：返回map中key-value对的个数
	- boolean isEmpty()：判断当前map是否为空
	- boolean equals(Object obj)：判断当前map和参数对象obj是否相等
	- 

- 元视图操作的方法：

	- Set keySet()：返回所有key构成的Set集合
	- Collection values()：返回所有value构成的Collection集合
	- Set entrySet()：返回所有key-value对构成的Set集合  

```java
//代码
Map map = new HashMap();
//map.put(..,..)省略

//输出map的所有key
Set keys = map.keySet();// HashSet
for (Object key : keys) {//遍历：增强for循环
	System.out.println(key + "->" + map.get(key));
}

//输出map的所有的value
Collection values = map.values();
Iterator iter = values.iterator();//遍历：迭代器
while (iter.hasNext()) {
	System.out.println(iter.next());
}
//输出map所有的映射关系
// 映射关系的类型是Map.Entry类型，它是Map接口的内部接口
Set mappings = map.entrySet();
for (Object mapping : mappings) {
	Map.Entry entry = (Map.Entry) mapping;
	System.out.println("key是： " + entry.getKey() + "， value是： " + entry.getValue());
}
```

**总结：**常用方法

添加：Object put(Object key,Object value)

删除：Object remove(Object key)

修改：Object put(Object key,Object value)

查询：Object get(Object key)

长度：int size()

遍历：Set keySet() 	\	 values()	\	 entrySet()：







------



##### 3、Map实现类之一： HashMap  

###### 1、HashMap的底层实现原理？？？

**以JDK7为例：**

```java
HashMap map = new HashMap();
```

在实例化以后，底层创建了长度为16的一维数组Entry[] table

```java
map.put(key,value);
....//添加许多元素以后
map.put(key1,value1);
```

添加操作，首先调用key1所在类的hashCode()计算key1的哈希值，得到在Entry数组中存放的位置。

- 情况一：如果此位置上数据为空，此时的key1-value1添加成功

- 情况二：如果此位置上数据不为空，（意味着此位置上存在一个或多个数据【以链表的形式存在】），此时比较key1和已经存在的一个或多个数据的哈希值：

	- 1、如果key1的哈希值与已经存在的数据的哈希值都不同，此时key1-value1添加成功
	- 2、如果key1的哈希值与已经存在的某个数据（key2）的哈希值相同，继续比较：调用key1所在类的equals（key2）和key2比较
		- 2.1如果equals()返回false：此时key1-value1添加成功
		- 2.2如果equals()返回true：则使用value1替换key2的value2,。

	**补充：**关于情况1和2.1，此时key1-value1和原来的数据以链表的方式存储。

	**扩容：**在不断添加过程中，当超出临界值且要存放位置非空时，会涉及到扩容的问题，默认的扩容方式是：扩容为原来容量的2倍，并将原有的数据复制过来。

**JDK8中的改变**

1、new HashMap()	时，底层没有创建一个长度为16的数组。

2、JDK8底层数组是：Node[]，而非Entry[]。

3、首次调用put()方法时，底层创建长度为16的数组。

4、JDK7底层结构只有：数组＋链表。JDK8中地层结构增加了红黑树：**数组＋链表＋红黑树**。

​	  当数组的某一索引位置上的元素是以链表形式存在的数据个数 > 8时，且当前数组的长度 > 64时，

​	  此时索引位置上的所有数据改为使用红黑树存储。【就是同一哈希地址值上元素大于8个时，用红黑树存，好找】

###### 2、HashMap的存储结构

![image-20210925100849337](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210926154130508-16326420921792.png)

![image-20210925100741112](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210927103526772-16327101287701.png)





###### 3、HashMap源码中的重要常量  

**DEFAULT_INITIAL_CAPACITY : HashMap的默认容量， 16**

MAXIMUM_CAPACITY ： HashMap的最大支持容量， 2^30

**DEFAULT_LOAD_FACTOR： HashMap的默认加载因子，0.75**

**TREEIFY_THRESHOLD： Bucket中链表长度大于该默认值，转化为红黑树 0.75 * 16 = 12**

UNTREEIFY_THRESHOLD： Bucket中红黑树存储的Node小于该默认值，转化为链表

MIN_TREEIFY_CAPACITY： 桶中的Node被树化时最小的hash表容量。（当桶中Node的数量大到需要变红黑树时，若hash表容量小于MIN_TREEIFY_CAPACITY时，此时应执行resize扩容操作这个MIN_TREEIFY_CAPACITY的值至少是TREEIFY_THRESHOLD的4倍。）

table： 存储元素的数组，总是2的n次幂

entrySet： 存储具体元素的集

size： HashMap中存储的键值对的数量

modCount： HashMap扩容和结构改变的次数。

threshold： 扩容的临界值， = 容量*填充因子

loadFactor： 填充因子  

------



##### 4、Map实现类之二： LinkedHashMap    

- LinkedHashMap 是 HashMap 的子类，底层结构一样
- 在HashMap存储结构的基础上，使用了**一对双向链表来记录添加元素的顺序**
- 与LinkedHashSet类似， LinkedHashMap 可以维护 Map 的迭代顺序：迭代顺序与 Key-Value 对的插入顺序一致  

**HashMap中的内部类： Node**  

```java
static class Node<K,V> implements Map.Entry<K,V> {
	final int hash;
	final K key;
	V value;
	Node<K,V> next;
}
```

**LinkedHashMap中的内部类： Entry**  

```java
static class Entry<K,V> extends HashMap.Node<K,V> {
	Entry<K,V> before, after;//能够记录添加的元素的先后顺序
	Entry(int hash, K key, V value, Node<K,V> next) {
		super(hash, key, value, next);
	}
}
```

------





##### 5、Map实现类之三： TreeMap    

- 像TreeMap中存储数据，必须保证key是由同一个类创建的对象【因为要排序，不同没法比】

- TreeMap存储 Key-Value 对时， 需要根据 key-value 对进行排序。

- TreeMap 可以保证所有的 Key-Value 对处于有序状态。

- TreeSet底层使用红黑树结构存储数据

- TreeMap 的 Key 的排序：
	- 自然排序： TreeMap 的所有的 Key 必须实现 Comparable 接口，而且所有的 Key 应该是同一个类的对象，否则将会抛出 ClasssCastException
	- 定制排序：创建 TreeMap 时，传入一个 Comparator 对象，该对象负责对TreeMap 中的所有 key 进行排序。此时不需要 Map 的 Key 实现Comparable 接口
- TreeMap判断两个key相等的标准：两个key通过compareTo()方法或者compare()方法返回0。  

------





##### 6、Map实现类之四：Hashtable  

- Hashtable是个古老的 Map 实现类， JDK1.0就提供了。不同于HashMap，Hashtable是线程安全的。
- Hashtable实现原理和HashMap相同，功能相同。底层都使用哈希表结构，查询速度快，很多情况下可以互用。
- 与HashMap不同， Hashtable 不允许使用 null 作为 key 和 value
- 与HashMap一样， Hashtable 也不能保证其中 Key-Value 对的顺序
- Hashtable判断两个key相等、两个value相等的标准， 与HashMap一致。  

------



##### 7、Map实现类之五： Properties  

- Properties 类是 Hashtable 的子类，该对象用于处理属性文件
- 由于属性文件里的 key、 value 都是字符串类型，所以 Properties 里的 key和 value 都是字符串类型
- 存取数据时，建议使用setProperty(String key,String value)方法和getProperty(String key)方法  



```java
Properties pros = new Properties();
//方式一：
pros.load(new FileInputStream("jdbc.properties"));//加载流配置文件、默认识别位置：当前module下
String user = pros.getProperty("user");
System.out.println(user);

//方式二：
ClassLoader cL = 当前类.class.getClassLoader();
InputStream is = cL.getResourceAsStream("jdbc.properties");//默认在当前module的src下面
pros,load(is);
String user = pros.getProperty("user");
System.out.println(user);
```



------

#### 七、Collections工具类

- Collections 是一个操作 Set、 List 和 Map 等集合的工具类
- Collections 中提供了一系列静态的方法对集合元素进行排序、查询和修改等操作，还提供了对集合对象设置不可变、对集合对象实现同步控制等方法

##### Collections常用方法  

- **排序操作：（均为static方法）**

	- reverse(List)： 反转 List 中元素的顺序
	- shuffle(List)： 对 List 集合元素进行随机排序
	- sort(List)： 根据元素的自然顺序对指定 List 集合元素按升序排序
	- sort(List， Comparator)： 根据指定的 Comparator 产生的顺序对 List 集合元素进行排序
	- swap(List， int， int)： 将指定 list 集合中的 i 处元素和 j 处元素进行交换  

	```java
	@Test
	    public void test3(){
	        List list = new ArrayList();
	        list.add(123);
	        list.add(56);
	        list.add(109);
	        list.add(109);
	        list.add(-4);
	
	        System.out.println(list);//[123, 56, 109, 109, -4]
	        Collections.reverse(list);//反转列表
	        System.out.println(list);//[-4, 109, 109, 56, 123]
	
	        Collections.shuffle(list);//随机排序
	        System.out.println(list);//[109, -4, 123, 109, 56]
	
	        Collections.sort(list);//根据列表对象的“自然排序”
	        Collections.sort(list, new Comparator<Object>() {"重写排序"});//“定制排序”
	        System.out.println(list);//[-4, 56, 109, 109, 123]
	
	        Collections.swap(list,1,3);//交换指定位置元素
	        System.out.println(list);//[-4, 109, 109, 56, 123]
	
	    }
	```

- **查找、替换**

	- Object max(Collection)： 根据元素的自然顺序，返回给定集合中的最大元素

	- Object max(Collection， Comparator)： 根据 Comparator 指定的顺序，返回给定集合中的最大元素

	- Object min(Collection)

	- Object min(Collection， Comparator)

	- int frequency(Collection， Object)： 返回指定集合中指定元素的出现次数

	- void copy(List dest,List src)：将src中的内容复制到dest中

		```java
		@Test
		public void test2(){
		    List list = new ArrayList();
		    list.add(123);
		    list.add(56);
		    list.add(109);
		    list.add(-4);
		
		    //copy方式一：报异常：IndexOutOfBoundsException: Source does not fit in dest
		    //因为新建dest长度不够
		    //List dest = new ArrayList();
		    //Collections.copy(dest,list);
		
		    //copy方式二：用准备拷贝的数组的size为尺寸，定制一个数组
		    List dest = Arrays.asList(new Object[list.size()]);
		    System.out.println(dest);//[null, null, null, null]
		
		    Collections.copy(dest,list);
		    System.out.println(list);//[123, 56, 109, -4]
		    System.out.println(dest);//[123, 56, 109, -4]
		
		
		}
		```

	- boolean replaceAll(List list， Object oldVal， Object newVal)： 使用新值替换List 对象的所有旧值  

- **同步控制**  

	- Collections 类中提供了多个 synchronizedXxx() 方法，该方法可使将指定集合包装成线程同步的集合，从而可以解决多线程并发访问集合时的线程安全问题

		  

		```java
		@Test
		public void test3(){
		    List list = new ArrayList();
		    list.add(123);
		    list.add(56);
		    list.add(109);
		    list.add(-4);
		
		    //此时返回的list1 就是线程安全的，源码中所有的常用操作都加了synchronized
		    List list1 = Collections.synchronizedList(list);
		}
		```

![image-20210925210805868](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210927165804538-16327330862181.png)

##### 练习题一：请从键盘随机输入10个整数保存到List中，并按倒序、从大到小的顺序显示出来  

```java
public static void main(String[] args) {
    Scanner scan = new Scanner(System.in);
    List list = new ArrayList();
    for (int i = 0; i < 10; i++) {
        list.add(scan.nextInt());
    }
    Collections.reverse(list);
    System.out.println(list);//倒序输出
    
    Collections.sort(list, new Comparator<Object>() {
        @Override
        public int compare(Object o1, Object o2) {
            if (o1 instanceof Integer && o2 instanceof Integer){
                Integer m = (Integer) o1;
                Integer n = (Integer) o2;
                return -Integer.compare(m,n);
            }
            throw new RuntimeException("类型错误");
        }
    });
    System.out.println(list);//从大到小
}
```

##### 练习二：请把学生名与考试分数录入到集合中，并按分数显示前三名成绩学员的名字。  

```java
public class Student implements Comparable<Student>{
    //属性
    private String name;
    private int score;
    private int id;
    //构造器
    public Student(){};
    public Student(String name,int score){
        this.name = name;
        this.score = score;
    }
    //方法
    public void setName(String name){
        this.name = name;
    }
    public void setScore(int score){
        this.score = score;
    }
    public String getName(){
        return name;
    }
    public int getScore(){
        return score;
    }

    @Override
    public int hashCode() {
        return super.hashCode();
    }

    @Override
    public boolean equals(Object obj) {
        return super.equals(obj);
    }

    @Override
    public String toString(){
        return "Student--->  name:" + name + " score:" + score;
    }
    @Override
    public int compareTo(Student o) {
        int num = o.score - score;
        if (num == 0){
            return this.name.compareTo(o.name);
        }
        return num;
    }

}
```



```java
import java.util.Iterator;
import java.util.TreeSet;

public class ScoreSystem {
    public static void main(String[] args) {
        Student qf = new Student("乔峰",88);
        Student zwj = new Student("张无忌",99);
        Student dy = new Student("段誉",74);
        Student yg = new Student("杨过",66);
        Student zm = new Student("赵敏",100);
        TreeSet<Student> set = new TreeSet<>();
        set.add(qf);
        set.add(zwj);
        set.add(dy);
        set.add(yg);
        set.add(zm);

        Iterator iterator = set.iterator();
        while(iterator.hasNext()){
            System.out.println(iterator.next());
        }
        int temp = 0;
        for(Student stu : set){
            if (temp == 3) break;
            temp++;
            System.out.println(stu.getName() + " : " + stu.getScore() );
        }
    }
}
```



------

### 6、泛型（Generic）

#### 一、泛型的概念：

- **所谓泛型， 就是允许在定义类、 接口时通过一个标识表示类中某个属性的类型或者是某个方法的返回值及参数类型。 这个类型参数将在使用时（例如，继承或实现这个接口， 用这个类型声明变量、 创建对象时） 确定（即传入实际的类型参数， 也称为类型实参）。**
- 从JDK1.5以后， Java引入了“参数化类型（ Parameterized type） ” 的概念，允许我们在创建集合时再指定集合元素的类型， 正如： List<String>， 这表明该List只能保存字符串类型的对象。
- JDK1.5改写了集合框架中的全部接口和类， 为这些接口、 类增加了泛型支持，从而可以在声明集合变量、 创建集合对象时传入类型实参。  

![image-20210926154109755](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210927170238928-16327333603012.png)

​	![image-20210926154130508](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210921094747753-16321888700412.png)

**在集合中不使用泛型时**

> ```java
> //在集合中使用泛型前的情况
>     @Test
>     public void test(){
>         //需求：列表存放学生成绩
>         ArrayList list = new ArrayList();
>         list.add(12);
>         list.add(88);
>         list.add(60);
>         list.add("小明");//假如操作失误，放了一个String,因为add()可以添加任何类型。
> 
>         for (Object obj : list){
>             //因为是成绩，所以转成int类型
>             int score = (int) obj;//这是就会报错，ClassCastException，因为  小明
>             System.out.println(score);
>         }
>     }
> 
> ```
>
> 



#### **二、在集合中使用泛型**

> ```java
>     //在集合中使用泛型后的情况:以ArrayList为例
>     @Test
>     public void test1(){
>         //需求：列表存放学生成绩
>         ArrayList<Integer> list = new ArrayList<>();
>         list.add(12);
>         list.add(88);
>         list.add(60);
>         //假如操作失误，放了一个String,因为泛型声明了Integer，不允许添加其他的类型，编译就会报错。
>         list.add("小明");
> 
>         for (Integer obj : list){
>             //避免了强转操作
>             int score = obj;
>             System.out.println(score);
>         }
> 
>         Iterator<Integer> iterator = list.iterator();
>         while(iterator.hasNext()){
>             int score = iterator.next();
>             System.out.println(score);
>         }
>     }
>     @Test
>     public void test3(){
>         Map<String, Integer> hashMap = new HashMap<>();
> 
>         hashMap.put("小明",22);
>         hashMap.put("丫蛋",18);
>         hashMap.put("二狗",99);
> 
>         //泛型的嵌套
>         Set<Map.Entry<String, Integer>> entry = hashMap.entrySet();
> 
>         Iterator<Map.Entry<String, Integer>> iterator = entry.iterator();
>         while(iterator.hasNext()){
>             Map.Entry<String, Integer> next = iterator.next();
>             String key = next.getKey();
>             Integer value = next.getValue();
> 
>             System.out.println("key---" + key + "\tvalue---" + value);
>         }
> 
>     }
> ```
>
> 

**总结：**

> 1、集合接口或者集合类，在JDK 5.0时，全部修改为带泛型的结构
>
> 2、在实例化集合类时，可以指明具体的泛型类型
>
> 3、指明完以后，在集合类或接口中，凡是定义类或者接口时，内部结构（比如：方法、构造器、属性等）使用到类的泛型的位置，都指定为实例化时的泛型类型。
>
> - 比如：add(E e)------>实例化以后：add(Integer e)；也可以是其他类型，看实例化时的泛型类型
>
> 4、注意点：泛型的类型必须是类，不能是基本数据类型，需要用到基本数据类型时，用包装类替换
>
> 5、如果实例化时，没有指明泛型的类型。默认类型为java.lang.Object类型



#### 三、自定义泛型

##### 1、自定义泛型类、接口

- 泛型类可能有多个参数，此时应将多个参数一起放在尖括号内。比如：<E1,E2,E3>

- 泛型类的构造器如下： public GenericClass(){}。

	而下面是错误的： public GenericClass<E>(){}，类已经声明了，构造器就不用再声明了

- 实例化后，操作原来泛型位置的结构必须与指定的泛型类型一致。

- 泛型不同的引用不能相互赋值。

	- 尽管在编译时ArrayList<String>和ArrayList<Integer>是两种类型，但是，在运行时只有
		一个ArrayList被加载到JVM中。

- 泛型如果不指定，将被擦除，泛型对应的类型均按照Object处理，但不等价于Object。 

	- 经验： 泛型要使用一路都用。要不用，一路都不要用。

- 如果泛型结构是一个接口或抽象类，则不可创建泛型类的对象。

- jdk1.7，泛型的简化操作： ArrayList<Fruit> flist = new ArrayList<>();后边<>不用写，默认识别前边的一致

- 泛型的指定中不能使用基本数据类型，可以使用包装类替换。  

```java
//类中定义了泛型，但是创建对象时没使用，默认是Object类，但不等同于Object类
class GenericTest {
	public static void main(String[] args) {
		// 1、使用时：类似于Object，不等同于Object
		ArrayList list = new ArrayList();
		// list.add(new Date());//有风险
		list.add("hello");
		test(list);// 泛型擦除，编译不会类型检查
        
		// ArrayList<Object> list2 = new ArrayList<Object>();
		// test(list2);//一旦指定Object，编译会类型检查，必须按照Object处理
	}
	public static void test(ArrayList<String> list) {
		String str = "";
		for (String s : list) {
			str += s + ",";
		}
		System.out.println("元素:" + str);
	}
}
```



- 在类/接口上声明的泛型，在本类或本接口中即代表某种类型，可以作为非静态属性的类型、非静态方法的参数类型、非静态方法的返回值类型。但在静态方法中不能使用类的泛型。

- 异常类不能是泛型的

- 不能使用new E[]。但是可以： E[] elements = (E[])new Object[capacity];

	- 参考： ArrayList源码中声明： Object[] elementData， 而非泛型参数类型数组。

- 父类有泛型，子类可以选择保留泛型也可以选择指定泛型类型：

- 子类不保留父类的泛型：按需实现

	- 没有类型 擦除
	- 具体类型

- 子类保留父类的泛型：泛型子类

	- 全部保留
	- 部分保留

- 结论：子类必须是“富二代”，子类除了指定或保留父类的泛型，还可以增加自己的泛型  

	```java
	class Father<T1, T2> {
	}
	// 子类不保留父类的泛型
	// 1)没有类型 擦除
	class Son1 extends Father {// 等价于class Son extends Father<Object,Object>{
	}
	// 2)具体类型
	class Son2 extends Father<Integer, String> {
	}
	// 子类保留父类的泛型
	// 1)全部保留
	class Son3<T1, T2> extends Father<T1, T2> {
	}
	// 2)部分保留
	class Son4<T2> extends Father<Integer, T2> {
	}
	```



```java
class Father<T1, T2> {
}
// 子类不保留父类的泛型
// 1)没有类型 擦除
class Son<A, B> extends Father{//等价于class Son extends Father<Object,Object>{
}
// 2)具体类型
class Son2<A, B> extends Father<Integer, String> {
}
// 子类保留父类的泛型
// 1)全部保留
class Son3<T1, T2, A, B> extends Father<T1, T2> {
}
// 2)部分保留
class Son4<T2, A, B> extends Father<Integer, T2> {
}
```

```java
class Person<T> {
	// 使用T类型定义变量
	private T info;
	// 使用T类型定义一般方法
	public T getInfo() {
		return info;
	}
	public void setInfo(T info) {
		this.info = info;
	}
	// 使用T类型定义构造器
	public Person() {
	}
	public Person(T info) {
		this.info = info;
	}
// static的方法中不能声明泛型
//public static void show(T t) {
//
//}
// 不能在try-catch中使用泛型定义
//public void test() {
//try {
//
//} catch (MyException<T> ex) {
//
//}
//}
}
```



##### 2、自定义泛型方法  

- 方法，也可以被泛型化，不管此时定义在其中的类是不是泛型类。 在泛型方法中可以定义泛型参数，此时，参数的类型就是传入数据的类型。
- 泛型方法的格式：
	**[访问权限] <泛型> 返回类型 方法名([泛型标识 参数名称]) 抛出的异常**
- 泛型方法声明泛型时也可以指定上限

```java
public class DAO {
    //Method
	public <E> E get(int id, E e) {
		E result = null;
		return result;
	}
}
```

```java
public static <T> void fromArrayToCollection(T[] a, Collection<T> c) {
	for (T o : a) {
		c.add(o);
	}
}
public static void main(String[] args) {
	Object[] ao = new Object[100];
	Collection<Object> co = new ArrayList<Object>();
	fromArrayToCollection(ao, co);
    
	String[] sa = new String[20];
	Collection<String> cs = new ArrayList<>();
	fromArrayToCollection(sa, cs);
    
	Collection<Double> cd = new ArrayList<>();
	// 下面代码中T是Double类，但sa是String类型，编译错误。
	// fromArrayToCollection(sa, cd);
	// 下面代码中T是Object类型， sa是String类型，可以赋值成功。
	fromArrayToCollection(sa, co);
}
```



```java
class Creature{}
class Person extends Creature{}
class Man extends Person{}
class PersonTest {
	public static <T extends Person> void test(T t){
		System.out.println(t);
	}
	public static void main(String[] args) {
		test(new Person());
		test(new Man());
		//The method test(T) in the type PersonTest is not
		//applicable for the arguments (Creature)
		test(new Creature());
	}
}
```



#### 四、泛型在继承上的体现

**虽然类A是 类B的父类，但是G<A> 和G<B>二者不具备子父类关系，二者是并列关系**

补充：类A 是 类B的父类，A<G>  是 B<G>的父类，因为泛型相同，可以相互赋值，保持原关系。

```java
public class GenericClassTest {
    @Test
    public void test(){
        Object obj = null;
        String str = null;
        obj = str;  //成功，没问题，子类对象赋给父类对象

        List<Object> list1 = null;
        List<String> list2 = null;
        list1 = list2;//失败，此时的list1和list2的类型，不具备子父类关系。
        /*
        证明：假设：list1 = list2;成功赋值
             此时调用add方法，因为list1是Object类型，所以我可以添加Integer型
             list1.add(123);
             但是list2数组里面是String类型，现在进去一个Integer类型的数据，这不乱套了么，出错
         */
    }
}
```



#### 五、通配符的使用	

- 使用类型通配符：**？**
	- 比如： List<?> ， Map<?,?>
	- List<?>是List<String>、 List<Object>等各种泛型List的父类。
- 读取List<?>的对象list中的元素时，永远是安全的，因为不管list的真实类型是什么，它包含的都是Object。
- 写入list中的元素时，不行。因为我们不知道c的元素类型，我们不能向其中添加对象。
	- 唯一的例外是null，它是所有类型的成员  

- 将任意元素加入到其中不是类型安全的：

	```java
	Collection<?> c = new ArrayList<String>();
	c.add(new Object()); // 编译时错误
	```

	因为我们不知道c的元素类型，我们不能向其中添加对象。 add方法有类型参数E作为集合的元素类型。我们传给add的任何参数都必须是一个未知类型的子类。因为我们不知道那是什么类型，所以我们无法传任何东西进去。

	唯一的例外的是null，它是所有类型的成员。

	<font color='red'>另一方面，我们可以调用get()方法并使用其返回值。返回值是一个未知的类型，但是我们知道，它总是一个Object。  

**虽然类A是 类B的父类，但是G<A> 和G<B>二者不具备子父类关系，二者是并列关系**、<font color='red'>二者的共同父类是G<？></font>

```java
@Test
public void test1(){
    List<Object> list1 = null;
    List<String> list2 = null;

    List<?> list = null;

    list = list1;
    list = list2;//都可以成功

}
public void print(List<?> list){
    Iterator<?> iterator = list.iterator();
    while(iterator.hasNext()){
        //此时因为不知道？代表什么类型，可以写一个Object类来接收对象
        Object obj = iterator.next();
        System.out.println(obj);
    }
}
```



- 将任意元素加入到其中不是类型安全的：
	Collection<?> c = new ArrayList<String>();
	c.add(new Object()); // 编译时错误
- 因为我们不知道c的元素类型，我们不能向其中添加对象。 add方法有类型参数E作为集合的元素类型。我们传给add的任何参数都必须是一个未知类型的子类。因为我们不知道那是什么类型，所以我们无法传任何东西进去。
- 唯一的例外的是null，它是所有类型的成员。
- 另一方面，我们可以调用get()方法并使用其返回值。返回值是一个未知的类型，但是我们知道，它总是一个Object。  

##### 有限制的通配符

- <font color = 'red'><?></font>
- 允许所有泛型的引用调用
- 通配符指定上限
	- 上限extends：使用时指定的类型必须是继承某个类，或者实现某个接口，即<=
- 通配符指定下限
	- 下限super：使用时指定的类型不能小于操作的类，即>=
- 举例：
	- **<? extends Number> (无穷小 , Number]**
		只允许泛型为Number及Number子类的引用调用
	- **<? super Number> [Number , 无穷大)**
		只允许泛型为Number及Number父类的引用调用
	-  **<? extends Comparable>**
		只允许泛型为实现Comparable接口的实现类的引用调用  



### 7、IO流

#### 一、File类的使用  

##### 1、File类概述

- java.io.File类： 文件和文件目录路径的抽象表示形式，与平台无关
- File 能新建、删除、重命名文件和目录，但 File 不能访问文件内容本身。
	- 如果需要访问文件内容本身，则需要使用输入/输出流。
- 想要在Java程序中表示一个真实存在的文件或目录，那么必须有一个File对象，但是Java程序中的一个File对象，可能没有一个真实存在的文件或目录。
- File对象可以作为参数传递给流的构造器  

##### 2、常用构造器  

- <font color = 'red'>public File(String pathname)</font>
	以pathname为路径创建File对象，可以是绝对路径或者相对路径，如果pathname是相对路径，则默认的当前路径在系统属性user.dir中存储。
	- 绝对路径： 是一个固定的路径,从盘符开始
	- 相对路径： 是相对于某个位置开始
	- **IDEA说明：**
		- 如果开发中用JUnit中的单元测试方法测试，相对路径即为当前module下。
		- 如果使用main()方法测试，相对路径即为当前的Protect下
	- **Eclipse说明：**
		- 无论是JUnit还是main（），相对路径都是Protect下。
- <font color='red'>public File(String parent,String child)</font>
	以parent为父路径， child为子路径创建File对象。
- <font color='red'>public File(File parent,String child)</font>
	根据一个父File对象和子文件路径创建File对象  

- 路径中的每级目录之间用一个路径分隔符隔开。
- 路径分隔符和系统有关：
	- windows和DOS系统默认使用“\”来表示
	- UNIX和URL使用“/”来表示
- Java程序支持跨平台运行，因此路径分隔符要慎用。
- 为了解决这个隐患， File类提供了一个常量：
	- public static final String separator。根据操作系统，动态的提供分隔符。
- 举例：  

```java
File file1 = new File("d:\\atguigu\\info.txt");
File file2 = new File("d:" + File.separator + "atguigu" + File.separator + "info.txt");
File file3 = new File("d:/atguigu");
```

##### 3、常用方法  

<font color='blue'>File类的获取功能</font>

- public String getAbsolutePath()： 获取绝对路径
- public String getPath() ： 获取路径
- public String getName() ： 获取名称
- public String getParent()： 获取上层文件目录路径。 若无， 返回null
- public long length() ： 获取文件长度（即：字节数） 。 不能获取目录的长度。
- public long lastModified() ： 获取最后一次的修改时间， 毫秒值

- ```java
	@Test
	public void test(){
	    File file1 = new File("hello.txt");
	    File file2 = new File("d:\\io\\hi.txt");
	
	    //获取绝对路径
	    System.out.println(file1.getAbsolutePath());
	    //获取路径
	    System.out.println(file1.getPath());
	    //获取名称
	    System.out.println(file1.getName());
	    //获取上层文件目录路径。 若无， 返回null
	    System.out.println(file1.getParent());
	    //获取文件长度（即：字节数） 。 不能获取目录的长度。
	    System.out.println(file1.length());
	    // 获取最后一次的修改时间， 毫秒值
	    System.out.println(new Date(file1.lastModified()));//返回的是时间戳，new个Date返回具体时间
	
	    System.out.println("---------------");
	    System.out.println(file2.getAbsolutePath());
	    System.out.println(file2.getPath());
	    System.out.println(file2.getName());
	    System.out.println(file2.getParent());
	    System.out.println(file2.length());
	    System.out.println(file2.lastModified());
	}
	```

**如下的两个方法适用于文件目录：**

- public String[] list() ： 获取指定目录下的所有文件或者文件目录的名称数组

- public File[] listFiles() ： 获取指定目录下的所有文件或者文件目录的File数组

- ```java
	@Test
	public void test1(){
	    File file = new File("E:\\computer\\Java");
	
	    //返回当前地址下的文件夹中的内容
	    String[] list = file.list();
	    for (String i:list){
	        System.out.println(i);
	    }
	    //----------输出文件名---------------
	    //尚硅谷Java文件集合
	    //javalianxi
	    //HouseHoldBills
	    //Algorithm
	    //idea主题
	    //Customer_Software
	    //Practice
	    //MyProject
	
	    File[] files = file.listFiles();
	    for (File f:files){
	        System.out.println(f);
	    }
	    //----------输出文件的绝对地址---------------
	    //E:\computer\Java\尚硅谷Java文件集合
	    //E:\computer\Java\javalianxi
	    //E:\computer\Java\HouseHoldBills
	    //E:\computer\Java\Algorithm
	    //E:\computer\Java\idea主题
	    //E:\computer\Java\Customer_Software
	    //E:\computer\Java\Practice
	    //E:\computer\Java\MyProject
	
	}
	```

<font color='blue'>File类的重命名功能</font>

- public boolean renameTo(File dest):把文件重命名为指定的文件路径  【移动+重命名】

- **注意：**要想成功（返回true），需要file1在硬盘中存在，而且file2不能在硬盘中存在。

- ```java
	@Test
	public void test2(){
	    File file1 = new File("hello.txt");
	    File file2 = new File("d:\\io\\hi.txt");
	    boolean renameTo = file1.renameTo(file2);
	    System.out.println(renameTo);
	}
	```

<font color='blue'>File类的判断功能</font>

- <font color='red'>public boolean isDirectory()： 判断是否是文件目录</font>

- <font color='red'>public boolean isFile() ： 判断是否是文件</font>

- <font color='red'>public boolean exists() ： 判断是否存在</font>

- public boolean canRead() ： 判断是否可读

- public boolean canWrite() ： 判断是否可写

- public boolean isHidden() ： 判断是否隐藏  

- ```java
	@Test
	public void test3(){
	    File file1 = new File("hello.txt");
	
	    //判断是否是文件目录
	    System.out.println(file1.isDirectory());
	    //判断是否是文件
	    System.out.println(file1.isFile());
	    //判断是否存在
	    System.out.println(file1.exists());
	    //判断是否可读
	    System.out.println(file1.canRead());
	    //判断是否可写
	    System.out.println(file1.canWrite());
	    //判断是否隐藏
	    System.out.println(file1.isHidden());
	}
	```

<font color='blue'>File类的创建功能</font>

- public boolean createNewFile() ： 创建文件。 若文件存在， 则不创建， 返回false

- ```java
	@Test
	public void test4() throws IOException {
	    File file = new File("xixi.txt");
	    
	    if (!file.exists()){//判断存在否
	        //文件创建
	        file.createNewFile();
	        System.out.println("创建成功！");
	    }else{
	        //文件删除
	        file.delete();
	        System.out.println("删除成功！");
	    }
	}
	```

- public boolean mkdir() ： 创建文件目录。 如果此文件目录存在， 就不创建了。
	如果此文件目录的上层目录不存在， 也不创建。

- public boolean mkdirs() ： 创建文件目录。 如果上层文件目录不存在， 一并创建
	注意事项：如果你创建文件或者文件目录没有写盘符路径， 那么， 默认在项目路径下。

- ```java
	@Test
	public void test5() throws IOException {
	    //D:\code\day01目录都存在，mkdir()只能在存在的目录下创建
	    File file1 = new File("D:\\code\\day01\\张无忌");
	    boolean mkdir = file1.mkdir();
	    if (mkdir){
	        System.out.println("file1创建成功！");
	    }
	
	    //D:\code\目录存在,day02不存在，mkdirs()可以创建不存在的上层目录，再创建目标目录
	    File file2 = new File("D:\\code\\day02\\赵敏");
	    boolean mkdir2 = file2.mkdirs();
	    if (mkdir2){
	        System.out.println("file2创建成功！");
	    }
	}
	```

<font color='blue'>File类的删除功能</font>

- public boolean delete()： 删除文件或者文件夹

	<font color='red'>删除注意事项：</font>

	<font color='red'>Java中的删除不走**回收站**。</font>

	<font color='red'>要删除一个文件目录， 请注意该文件目录内不能包含文件或者文件目录  </font>



![image-20210927103526772](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210927170434218-16327334754204.png)

------



#### 二、IO流原理及流的分类  

##### 1、Java IO原理

- I/O是Input/Output的缩写， I/O技术是非常实用的技术， 用于处理设备之间的数据传输。 如读/写文件，网络通讯等。
- Java程序中，对于数据的输入/输出操作以“流(stream)” 的方式进行。
- java.io包下提供了各种“流”类和接口，用以获取不同种类的数据，并通过标准的方法输入或输出数据。  

- 输入input： 读取外部数据（磁盘、光盘等存储设备的数据）到程序（内存）中。
- 输出output： 将程序（内存）数据输出到磁盘、光盘等存储设备中。  

![image-20210927165804538](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210927170503970-16327335050195.png)

##### 2、流的分类

- 按操作**数据单位**不同分为： 字节流(8 bit)，字符流(16 bit)
- 按数据流的**流向**不同分为： 输入流，输出流
- 按流的**角色**的不同分为： 节点流，处理流  

| (抽象基类) | 字节流       | 字符流 |
| ---------- | ------------ | ------ |
| 输入流     | InputStream  | Reader |
| 输出流     | OutputStream | Writer |

- Java的IO流共涉及40多个类，实际上非常规则，都是从如下4个抽象基类派生的。
- 由这四个类派生出来的子类名称都是以其父类名作为子类名后缀。  

![image-20210927170238928](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210928104928437-16327973697321.png)

处理流：作用在流上的。

##### 3、IO 流体系 

| 抽象基类     | 节点流（或文件流） | 缓冲流（处理流的一种） |
| ------------ | ------------------ | ---------------------- |
| InputStream  | FileInputStream    | BufferedInputStream    |
| OutputStream | FileOutputStream   | BufferedOutputStream   |
| Reader       | FileReader         | BufferedReader         |
| Writer       | FileWriter         | BufferedWriter         |



![image-20210927170358323](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210928105215037-16327975361733.png)



##### 4、节点流和处理流

- **节点流：**直接从数据源或目的地读写数据  

![image-20210927170434218](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210928164316322-16328185975301.png)

- **处理流：**不直接连接到数据源或目的地，而是“连接” 在已存在的流（节点流或处理流）之上，通过对数据的处理为程序提供更为强大的读写功能。  

![image-20210927170503970](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210928173557158-16328217582723.png)

- 

#### 三、节点流(或文件流)

##### 1、InputStream & Reader  

- InputStream 和 Reader 是所有**输入流**的基类。
- **InputStream**（典型实现： <font color='red'>FileInputStream</font>）**【字节流，处理jpg、p3、mp4、avi、ppt等】**
	- int read()
	- <font color='red'>int read(byte[] b)</font>
	- int read(byte[] b, int off, int len)
- **Reader**（典型实现： <font color='red'>FileReader</font>）**【字符流、处理字符txt、java、c、cpp、等】**
	- int read()
	- <font color='red'>int read(char [] c)</font>
	- int read(char [] c, int off, int len)
- 程序中打开的文件 IO 资源不属于内存里的资源，垃圾回收机制无法回收该资源，所以应该<font color='red'>显式关闭文件 IO 资源</font>。
- **FileInputStream** 从文件系统中的某个文件中获得输入字节。 FileInputStream用于读取非文本数据之类的原始字节流。要读取字符流， 需要使用 FileReader  

###### <font color='red'>**1.1  InputStream**</font>

- **int read()**
	从输入流中读取数据的下一个字节。 返回 0 到 255 范围内的 int 字节值。 如果因为已经到达流末尾而没有可用的字节， 则返回值 -1。
- **int read(byte[] b)**
	从此输入流中将最多 b.length 个字节的数据读入一个 byte 数组中。 如果因为已经到达流末尾而没有可用的字节， 则返回值 -1。 否则以整数形式返回实际读取的字节数。
- **int read(byte[] b, int off,int len)**
	将输入流中最多 len 个数据字节读入 byte 数组。 尝试读取 len 个字节， 但读取的字节也可能小于该值。 以整数形式返回实际读取的字节数。 如果因为流位于文件末尾而没有可用的字节， 则返回值 -1。
- **public void close() throws IOException**
	关闭此输入流并释放与该流关联的所有系统资源。  



###### **<font color='red'>1.2  Reader</font>**

- **int read()**
	读取单个字符。 作为整数读取的字符， 范围在 0 到 65535 之间 (0x00-0xffff)（2个字节的Unicode码） ， 如果已到达流的末尾， 则返回 -1

- > ```java
	> //不完整版，理解步骤；
	> @Test
	> public void test() throws IOException {
	>     //1、实例化File类的对象，指明要操作的对象
	>     File file = new File("hello.txt");//使用相对路径
	>     //2、提供具体的流
	>     FileReader fileReader = new FileReader(file);
	>     //3、数据的读入
	>     int data = fileReader.read();//返回读入的一个字符，如果到达文末，返回-1.可以用来判断是否读完。
	>     while(data != -1){
	>         System.out.print((char) data);//abcd
	>         data = fileReader.read();
	>     }
	>     //4、流的关闭操作
	>     fileReader.close();
	> }
	> ```
	>
	> ```java
	> //完整版
	> //异常的处理：为了保证流资源的关闭操作一定可以执行，需要使用try-catch-finally处理
	> //读入的文件一定要存在，否则就会包FileNotFoundException异常
	> 
	> 
	> @Test
	> public void test(){
	>     FileReader fileReader = null;
	>     try {
	>         //1、实例化File类的对象，指明要操作的对象
	>         File file = new File("hello.txt");//使用相对路径
	>         //2、提供具体的流
	>         fileReader = new FileReader(file);
	>         //3、数据的读入
	>         int data = fileReader.read();//返回读入的一个字符，如果到达文末，返回-1.可以用来判断是否读完。
	>         while(data != -1){
	>             System.out.print((char) data);//abcd
	>             data = fileReader.read();
	>         }
	>     } catch (IOException e) {
	>         e.printStackTrace();
	>     } finally {
	>         //4、流的关闭操作
	>         try {
	>             if (fileReader != null)//如果前边报异常了，可能没创建对象，这时候就不用关闭操作
	>                 fileReader.close();
	>         } catch (IOException e) {
	>             e.printStackTrace();
	>         }
	>     }
	> }
	> ```

- **int read(char[] cbuf)**
	将字符读入数组。 如果已到达流的末尾， 则返回 -1。 否则返回本次读取的字符数。

- ```java
	@Test
	    public void test1(){
	        FileReader fileReader = null;
	        try {
	            //1、实例化File类的对象，指明要操作的对象
	            File file = new File("hello.txt");//使用相对路径
	            //2、提供具体的流
	            fileReader = new FileReader(file);
	            //3、数据的读入
	            //read(char[] charBuffer):返回每次读入charbuffer数组中的字符的个数，如果到达文件末尾，返回-1；
	            char[] charBuffer = new char[5];//自定义每次取几个字符
	            int len;//每次读取的长度fileReader.read(charBuffer)
	            while((len = fileReader.read(charBuffer)) != -1){
	                //错误
	//                for (int i = 0; i < charBuffer.length;i++){
	//                    //hello  world  12rld【原数据helloworld12】，每组charBuffer 5个，最后一组不足5个，i<length会输出的多了
	//                    System.out.print(charBuffer[i]);
	//                }
	                //方式一：
	                for (int i = 0; i < len;i++){
	                    System.out.print(charBuffer[i]);
	                }
	                //方式二
	                String str = new String(charBuffer,0,len);//char数组转为字符串，每次从0开始，到len结束
	                System.out.print(str);
	            }
	        } catch (IOException e) {
	            e.printStackTrace();
	        } finally {
	            //4、流的关闭操作
	            try {
	                if (fileReader != null)//如果前边报异常了，可能没创建对象，这时候就不用关闭操作
	                    fileReader.close();
	            } catch (IOException e) {
	                e.printStackTrace();
	            }
	        }
	    }
	```
	
- **int read(char[] cbuf,int off,int len)**
	将字符读入数组的某一部分。 存到数组cbuf中， 从off处开始存储， 最多读len个字符。 如果已到达流的末尾， 则返回 -1。 否则返回本次读取的字符数。

- **public void close() throws IOException**
	关闭此输入流并释放与该流关联的所有系统资源。  

##### 2、OutputStream & Writer

- OutputStream 和 Writer 也非常相似：
	- void write(int b/int c);
	- void write(byte[] b/char[] cbuf);
	- void write(byte[] b/char[] buff, int off, int len);
	- void flush();
	- void close(); 需要先刷新，再关闭此流
- 因为字符流直接以字符作为操作单位，所以 Writer 可以用字符串来替换字符数组，即以 String 对象作为参数
	- void write(String str);
	- void write(String str, int off, int len);
- FileOutputStream 从文件系统中的某个文件中获得输出字节。 FileOutputStream用于写出非文本数据之类的原始字节流。 要写出字符流， 需要使用 FileWriter  

###### **<font color='red'>2.1  OutputStream</font>**

- <font color='red'>void write(int b)</font>
	将指定的字节写入此输出流。 write 的常规协定是：向输出流写入一个字节。 要写入的字节是参数 b 的八个低位。 b 的 24 个高位将被忽略。 即写入0~255范围的。
- <font color='red'>void write(byte[] b)</font>
	将 b.length 个字节从指定的 byte 数组写入此输出流。 write(b) 的常规协定是：应该与调用 write(b, 0, b.length) 的效果完全相同。
- <font color='red'>void write(byte[] b,int off,int len)</font>
	将指定 byte 数组中从偏移量 off 开始的 len 个字节写入此输出流。
- <font color='red'>public void flush()throws IOException</font>
	刷新此输出流并强制写出所有缓冲的输出字节， 调用此方法指示应将这些字节立即写入它们预期的目标。
- <font color='red'>public void close() throws IOException</font>
	关闭此输出流并释放与该流关联的所有系统资源。  

###### **<font color='red'>2.2  Writer</font>**

- <font color='red'>void write(int c)</font>
	写入单个字符。 要写入的字符包含在给定整数值的 16 个低位中， 16 高位被忽略。 即写入0 到 65535 之间的Unicode码。
- <font color='red'>void write(char[] cbuf)</font>
	写入字符数组。
- <font color='red'>void write(char[] cbuf,int off,int len)</font>
	写入字符数组的某一部分。 从off开始， 写入len个字符
- <font color='red'>void write(String str)</font>
	写入字符串。
- <font color='red'>void write(String str,int off,int len)</font>
	写入字符串的某一部分。
- <font color='red'>void flush()</font>
	刷新该流的缓冲， 则立即将它们写入预期目标。
- <font color='red'>public void close() throws IOException</font>
	关闭此输出流并释放与该流关联的所有系统资源。  

```java
/**
 * 1、输出操作：对应的File文件可以不存在
 * 2、File对应的硬盘中文件不存在，在输出过程中，会自动创建
 *    File对应的硬盘中文件存在：
 *
 *              如果调用FileWriter(file,false)或者 FileWriter(file)构造器：对原有文件进行覆盖；
 *              如果调用FileWriter(file,true)构造器，在原有文件的后面进行追加append；
 * 
 */
@Test
    public void test2() {
        FileWriter fileWriter = null;
        try {
            //1、提供File类的对象，指明要写出到的文件
            File file = new File("hello999");
            //2、提供FileWriter的对象，用于数据写出
            fileWriter = new FileWriter(file);
            //3、写出操作
            fileWriter.write("I have a dream!\n");
            fileWriter.write("You need to have a dream!");
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
                try {
                    if (fileWriter != null)
                        //4、流资源关闭
                        fileWriter.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
        }
    }
```



<font color='red'>**先读后写----步骤演示【异常处理----暂不处理】**</font>

```java
@Test
public void test3() throws IOException {
    //1、创建File类的对象，指明读入和写出的文件
    File file1 = new File("hello999");
    File file2 = new File("hello123.txt");

    //2、创建输入流和输出流的对象
    FileReader fileReader = new FileReader(file1);
    FileWriter fileWriter = new FileWriter(file2);

    //3、数据的读入和写出操作
    char[] chars = new char[5];
    int len;
    while((len = fileReader.read(chars)) != -1){
        fileWriter.write(chars,0,len);
    }

    //4、流的关闭操作
    fileWriter.close();
    fileReader.close();
}
```



##### <font color='red'>**字符流先读后写（复制）----完整版【Reader&Writer】**</font>

```java
@Test
public void test3(){
    FileReader fileReader = null;
    FileWriter fileWriter = null;
    try {
        //1、创建File类的对象，指明读入和写出的文件
        File file1 = new File("hello999");
        File file2 = new File("hello123.txt");

        //2、创建输入流和输出流的对象
        fileReader = new FileReader(file1);
        fileWriter = new FileWriter(file2);

        //3、数据的读入和写出操作
        char[] chars = new char[5];
        int len;
        while((len = fileReader.read(chars)) != -1){
            fileWriter.write(chars,0,len);
        }
    } catch (IOException e) {
        e.printStackTrace();
    } finally {

        //4、流的关闭操作
        try {
            if (fileWriter != null)
                fileWriter.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
        //要写两个try-catch，保证哪怕另一个出异常，第二个也能关闭
        try {
            if (fileReader != null)
                fileReader.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

##### <font color='red'>**字节流先读后写（复制）----完整版【InputStream&OutputStream】**</font>

```java
@Test
public void test(){
    FileInputStream fileIn = null;
    FileOutputStream fileOut = null;
    try {
        //1、创建待处理文件对象
        File file1 = new File("car.jpg");
        File file2 = new File("bigCar.jpg");

        //2、创建输入输出流对象
        fileIn = new FileInputStream(file1);
        fileOut = new FileOutputStream(file2);

        //3、处理文件
        byte[] bytes = new byte[5];
        int len;
        while((len = fileIn.read(bytes)) != -1){
            //写入操作
            fileOut.write(bytes,0,len);
        }
    } catch (IOException e) {
        e.printStackTrace();
    } finally {

        //4、关闭流操作
        try {
            if (fileIn != null)
                fileIn.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
        try {
            if (fileOut != null)
                fileOut.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```



可以将上边的【复制】操作封装成一个方法，后序直接调用，只需要将地址作为形参处理即可

**调用函数：**

> ```java
> @Test
> public void test1(){
>     long start = System.currentTimeMillis();
> 
>     String srcPath = "C:\\Users\\kingb\\Desktop\\01-视频.mp4";
>     String destPath = "C:\\Users\\kingb\\Desktop\\02-视频.mp4";
>     copyByte(srcPath,destPath);
> 
>     long end = System.currentTimeMillis();
>     System.out.println("复制花费的时间为：" + (end - start) + "毫秒");//2304
> }
> ```

**Copy函数：**

> ```java
> public void copyByte(String srcPath,String destPath){
>     FileInputStream fileIn = null;
>     FileOutputStream fileOut = null;
>     try {
>         //1、创建待处理文件对象
>         File file1 = new File(srcPath);
>         File file2 = new File(destPath);
> 
>         //2、创建输入输出流对象
>         fileIn = new FileInputStream(file1);
>         fileOut = new FileOutputStream(file2);
> 
>         //3、处理文件
>         byte[] bytes = new byte[1024];
>         int len;
>         while((len = fileIn.read(bytes)) != -1){
>             //写入操作
>             fileOut.write(bytes,0,len);
>         }
>     } catch (IOException e) {
>         e.printStackTrace();
>     } finally {
> 
>         //4、关闭流操作
>         try {
>             if (fileIn != null)
>                 fileIn.close();
>         } catch (IOException e) {
>             e.printStackTrace();
>         }
>         try {
>             if (fileOut != null)
>                 fileOut.close();
>         } catch (IOException e) {
>             e.printStackTrace();
>         }
>     }
> }
> ```



##### 节点流(或文件流)：注意点  

- 定义文件路径时，注意：可以用“/”或者“\\”。
- 在写入一个文件时，如果使用构造器FileOutputStream(file)，则目录下有同名文件将被覆盖。
- 如果使用构造器FileOutputStream(file,true)，则目录下的同名文件不会被覆盖，在文件内容末尾追加内容。
- 在读取文件时，必须保证该文件已存在，否则报异常。
- 字节流操作字节，比如： .mp3， .avi， .rmvb， mp4， .jpg， .doc， .ppt
- 字符流操作字符，只能操作普通文本文件。 最常见的文本文件： .txt， .java， .c， .cpp 等语言的源代码。尤其注意.doc,excel,ppt这些不是文本文件。  



#### 四、处理流之一：缓冲流  

【相当于给    字节流/字符流    加一个推进器】

为了提高数据读写的速度， Java API提供了带缓冲功能的流类，在使用这些流类时，会创建一个内部缓冲区数组，缺省使用8192个字节(8Kb)的缓冲区。  

![image-20210928104928437](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210928173548372-16328217502322.png)



- 缓冲流要“套接”在相应的节点流之上，根据数据操作单位可以把缓冲流分为：
	- BufferedInputStream 和 BufferedOutputStream
	- BufferedReader 和 BufferedWriter  

- 当读取数据时，数据按块读入缓冲区，其后的读操作则直接访问缓冲区
- 当使用BufferedInputStream读取字节文件时， BufferedInputStream会一次性从文件中读取8192个(8Kb)， 存在缓冲区中， 直到缓冲区装满了， 才重新从文件中读取下一个8192个字节数组。
- 向流中写入字节时， 不会直接写到文件， 先写到缓冲区中直到缓冲区写满，BufferedOutputStream才会把缓冲区中的数据一次性写到文件里。使用方法flush()可以强制将缓冲区的内容全部写入输出流
- 关闭流的顺序和打开流的顺序相反。只要关闭最外层流即可， 关闭最外层流也会相应关闭内层节点流
- flush()方法的使用：手动将buffer中内容写入文件
- 如果是带缓冲区的流对象的close()方法， 不但会关闭流， 还会在关闭流之前刷新缓冲区， 关闭后不能再写出  

![image-20210928105205761](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210928174042735-16328220440644.png)

![image-20210928105215037](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210927170358323-16327334396793.png)



**非文本文件：**

增加缓冲流以后的**Copy方法**-----------------------效率提升明显

**调用函数：**

> ```java
> @Test
> public void test(){
>     long start = System.currentTimeMillis();
>     String srcPath = "C:\\Users\\kingb\\Desktop\\01-视频.mp4";
>     String destPath = "C:\\Users\\kingb\\Desktop\\05-视频.mp4";
>     copyBufferedFile(srcPath,destPath);
>     long end = System.currentTimeMillis();
>     System.out.println("复制花费的时间为：" + (end - start) + "毫秒");//571
> 
> }
> ```

**Copy函数：**

> ```java
> public void copyBufferedFile(String srcPath,String destPath){
>         BufferedInputStream buffIn = null;
>         BufferedOutputStream buffTo = null;
>         try {
>             //1、创建待处理文件对象
>             File file1 = new File(srcPath);
>             File file2 = new File(destPath);
> 
>             //2、创建输出输出流对象
>             FileInputStream fileIn = new FileInputStream(file1);
>             FileOutputStream fileTo = new FileOutputStream(file2);
> 
>             //3、创建缓冲流对象
>             buffIn = new BufferedInputStream(fileIn);
>             buffTo = new BufferedOutputStream(fileTo);
> 
>             //4、处理文件
>             byte[] bytes = new byte[1024];
>             int len;
>             while((len = buffIn.read(bytes)) != -1){
>                 buffTo.write(bytes,0,len);
>             }
>         } catch (IOException e) {
>             e.printStackTrace();
>         } finally {
> 
>             //5、关闭流操作：外层流关闭后，默认内层也关闭，不需要再人为操作
>             try {
>                 if (buffIn != null)
>                     buffIn.close();
>             } catch (IOException e){
>                 e.printStackTrace();
>             }
>             try {
>                 if (buffTo != null)
>                     buffTo.close();
>             } catch (IOException e) {
>                 e.printStackTrace();
>             }
>         }
>     }
> ```



**文本文件：**

增加缓冲流以后的**Copy方法**-----------------------效率提升明显------读操作可以按行读取，不一定用char[]数组

**调用函数：**

> ```java
> @Test
> public void test1(){
>     long start = System.currentTimeMillis();
> 
>     String srcPath = "dbcp.txt";
>     String destPath = "dbcp_Copy.txt";
>     copyChar(srcPath,destPath);
>     
>     long end = System.currentTimeMillis();
>     System.out.println("复制花费的时间为：" + (end - start) + "毫秒");//2304
> }
> ```

**Copy函数：**

> ```java
> public void copyChar(String srcPath,String destPath){
>     BufferedReader buffRead = null;
>     BufferedWriter buffWri = null;
>     try {
>         //1、文件和流的创建
>         buffRead = new BufferedReader(new FileReader(new File(srcPath)));
>         buffWri = new BufferedWriter(new FileWriter(new File(destPath)));
> 
>         //2、文件读写
> //            //方式一：char[]数组
> //            char[] chars = new char[1024];
> //            int len;
> //            while((len = buffRead.read(chars)) != -1){//每次读char[1024]，文末返回-1；
> //                buffWri.write(chars,0,len);
> //            }
>         //方式二：直接按行读取，一次一行，但是不读换行符
>         String data;
>         while((data = buffRead.readLine()) != null){
>             //每次读一行，文末返回null；【并且不读换行符】
>             
>             //写：方式一
>             //buffWri.write(data + "\n");
>             //这种方式读取的数据，没有读换行符，写的时候就是一行，手动加一个\n
>             
>             //写：方式二
>             buffWri.write(data);
>             buffWri.newLine();//调用这个方法，也是每次换行。
>         }
>     } catch (IOException e) {
>         e.printStackTrace();
>     } finally {
>         //3、流关闭
>         try {
>             if (buffRead != null)
>                 buffRead.close();
>         } catch (IOException e) {
>             e.printStackTrace();
>         }
>         try {
>             if (buffWri != null)
>                 buffWri.close();
>         } catch (IOException e) {
>             e.printStackTrace();
>         }
>     }
> 
> }
> ```

##### 练习一：图片加密----解密



```java
/**
 * 通过对每个字节异或5，进行加密
 */
@Test
public void test(){
    FileInputStream file1 = null;
    FileOutputStream file2 = null;
    try {
        file1 = new FileInputStream(new File("car.jpg"));
        file2 = new FileOutputStream(new File("carSecret.jpg"));

        byte[] bytes = new byte[20];
        int len;
        while((len = file1.read(bytes)) != -1){
            for (int i = 0; i<len;i++){
                bytes[i] = (byte) (bytes[i] ^ 5);
            }
            file2.write(bytes,0,len);
        }
    } catch (IOException e) {
        e.printStackTrace();
    } finally {
        try {
            if (file1 != null)
                file1.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
        try {
            if (file2 != null)
                file2.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

}
```

```java
/**
 * 通过对每个字节异或5，进行解密，解密操作读取的文件是carSecret.jpg
 */
@Test
public void test1(){
    FileInputStream file1 = null;
    FileOutputStream file2 = null;
    try {
        file1 = new FileInputStream(new File("carSecret.jpg"));
        file2 = new FileOutputStream(new File("carNew.jpg"));

        byte[] bytes = new byte[20];
        int len;
        while((len = file1.read(bytes)) != -1){
            for (int i = 0; i<len;i++){
                bytes[i] = (byte) (bytes[i] ^ 5);
            }
            file2.write(bytes,0,len);
        }
    } catch (IOException e) {
        e.printStackTrace();
    } finally {
        try {
            if (file1 != null)
                file1.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
        try {
            if (file2 != null)
                file2.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

}
```



##### 练习二：获取文本上每个字符出现的次数

提示：遍历文本的每一个字符；字符及出现的次数保存在Map中；将Map中数据写入文件  

```java
@Test
public void test() {
    FileReader fileReader = null;
    FileWriter fileWriter = null;
    try {
        //创建读入写入文件
        fileReader = new FileReader(new File("dbcp.txt"));
        fileWriter = new FileWriter(new File("StatisticsChar.txt"));
        //创建保存的哈希表
        HashMap<Character, Integer> map = new HashMap<>();

        //不用使用char[]数组存储，因为要拿到每一个字符，要不然还得遍历char[]数组，南辕北辙了
        int c;
        while((c = fileReader.read()) != -1){//因为返回int，Ascii码，所以先用int接收，再强转
            char ch = (char) c;
            if (map.containsKey(ch)){//如果key存在，value+1
                map.put(ch,map.get(ch) + 1);
            }else{
                map.put(ch,1);
            }
        }

        Set<Map.Entry<Character, Integer>> entries = map.entrySet();
        Iterator<Map.Entry<Character, Integer>> iterator = entries.iterator();
        while(iterator.hasNext()){
            Map.Entry<Character,Integer> entry = iterator.next();

//        for (Map.Entry<Character,Integer> entry1 : entries){//增强for循环
            switch (entry.getKey()) {
                case ' ':
                    fileWriter.write("空格：" + " 次数：" + entry.getValue() + "\n");
                    break;
                case '\t':
                    fileWriter.write("tab键：" + " 次数：" + entry.getValue() + "\n");
                    break;
                case '\r':
                    fileWriter.write("回车：" + " 次数：" + entry.getValue() + "\n");
                    break;
                case '\n':
                    fileWriter.write("换行：" + " 次数：" + entry.getValue() + "\n");
                    break;
                default:
                    fileWriter.write(entry.getKey() + ":  次数：" + entry.getValue() + "\n");
                    break;
            }

        }
    } catch (IOException e) {
        e.printStackTrace();
    } finally {
        
        //关闭流
        try {
            if (fileReader != null)
                fileReader.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
        try {
            if (fileWriter != null)
                fileWriter.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```



#### 五、处理流之二：转换流  

- 转换流提供了在字节流和字符流之间的转换
- Java API提供了两个转换流：
	- **InputStreamReader：将InputStream转换为Reader【字节----->字符   解码】**
	- **OutputStreamWriter：将Writer转换为OutputStream【字符----->字节   编码】**
- 字节流中的数据都是字符时，转成字符流操作更高效。
- 很多时候我们使用转换流来处理文件乱码问题。实现编码和解码的功能。  

##### InputStreamReader

- 实现将字节的输入流按指定字符集转换为字符的输入流。

- 需要和InputStream“套接”。

- 构造器

	- public InputStreamReader(InputStream in)
	- public InputSreamReader(InputStream in,String charsetName)
		如： Reader isr = new InputStreamReader(System.in,”gbk”);     gbk----指定字符集  

	

	```java
	public class TestInputStreamReader {
	    @Test
	    public void test(){
	        InputStreamReader inputSR = null;//也可以不写UTF-8，默认使用系统编码方式
	        try {
	            //创建文件对象
	            FileInputStream fileIn = new FileInputStream(new File("dbcp.txt"));//字节流
	            //转换
	            inputSR = new InputStreamReader(fileIn, "UTF-8");
	
	            //读文件
	            char[] chars = new char[20];//因为完成了转换，所以字节流可以用char[]数组读
	            int len;
	            while((len = inputSR.read(chars)) != -1){
	                String str = new String(chars,0,len);
	                System.out.println(str);
	            }
	        } catch (IOException e) {
	            e.printStackTrace();
	        } finally {
	            try {
	                if (inputSR != null)
	                    inputSR.close();
	            } catch (IOException e) {
	                e.printStackTrace();
	            }
	        }
	    }
	}
	```

##### OutputStreamWriter

- 实现将字符的输出流按指定字符集转换为字节的输出流。
- 需要和OutputStream“套接”。
- 构造器
	- public OutputStreamWriter(OutputStream out)
	- public OutputSreamWriter(OutputStream out,String charsetName)  



![image-20210928164316322](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210928174255631-16328221770286.png)



##### 练习一：综合使用InputStreamReader和OutputStreamWriter：

将一个由UTF-8编码的文件，打开、读取、并用GBK编码重写在另一个文件中。

```java
public class TestInputStreamReaderANDOutputStreamWriter {
    //此处处理异常的方式不对，应该用try-catch-finally,因为这种方式加入有异常，后边的关闭流操作不会执行
    //目前为了步骤看起来清晰明了，暂不用try-catch-finally处理
    @Test
    public void test1() throws IOException {
        //1、创建文件对象
        File file1 = new File("dbcp.txt");
        File file2 = new File("dbcp_To_GBK.txt");

        //2、创建流对象
        FileInputStream inpS = new FileInputStream(file1);
        FileOutputStream outpS = new FileOutputStream(file2);

        //3、创建转换对象
        InputStreamReader inpSR = new InputStreamReader(inpS, "UTF-8");
        OutputStreamWriter outpSR = new OutputStreamWriter(outpS, "GBK");

        //4、文件读写
        char[] chars = new char[20];
        int len;
        while((len = inpSR.read(chars)) != -1){
            outpSR.write(chars,0,len);
        }

        //5、关闭流操作
        inpSR.close();
        outpSR.close();
    }
}
```



#### 六、字符编码

##### 1、编码表的由来

​		计算机只能识别二进制数据，早期由来是电信号。为了方便应用计算机，让它可以识别各个国家的文字。就将各个国家的文字用数字来表示，并一一对应，形成一张表，这就是编码表。

##### 2、常见的编码表

- **ASCII：** 美国标准信息交换码。
	- 用一个字节的7位可以表示。
- **ISO8859-1：** 拉丁码表。欧洲码表
	- 用一个字节的8位表示。
- **GB2312：** 中国的中文编码表。最多两个字节编码所有字符
- **GBK：** 中国的中文编码表升级，融合了更多的中文文字符号。最多两个字节编码
- **Unicode：** 国际标准码， 融合了目前人类使用的所有字符。为每个字符分配唯一的字符码。所有的文字都用两个字节来表示。
- **UTF-8：** 变长的编码方式，可用1-4个字节来表示一个字符。  



![image-20210928173548372](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210930181617528-16329969790291.png)

![image-20210928173557158](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210925100741112-16325356626482.png)

<font color='blue'>在Unicode出现之前，所有的字符集都是和具体编码方案绑定在一起的（即字符集≈编码方式），都是直接将字符和最终字节流绑定死了。</font>

- **GBK等双字节编码方式， 用最高位是1或0表示两个字节和一个字节。**  

- Unicode不完美，这里就有三个问题，一个是，我们已经知道，英文字母只用一个字节表示就够了，第二个问题是如何才能区别Unicode和ASCII？计算机怎么知道两个字节表示一个符号，而不是分别表示两个符号呢？第三个，如果和GBK等双字节编码方式一样，用最高位是1或0表示两个字节和一个字节，就少了很多值无法用于表示字符，不够表示所有字符。 Unicode在很长一段时间内无法推广，直到互联网的出现。
- 面向传输的众多 UTF（UCS Transfer Format）标准出现了，顾名思义，<font color='red'> UTF-8就是每次8个位传输数据，而UTF-16就是每次16个位。</font> 这是为传输而设计的编码，并使编码无国界，这样就可以显示全世界上所有文化的字符了。
- <font color='blue'>Unicode只是定义了一个庞大的、全球通用的字符集，并为每个字符规定了唯一确定的编号，具体存储成什么样的字节流，取决于字符编码方案。</font> 推荐的Unicode编码是UTF-8和UTF-16。  

```java
	Unicode符号范围  | UTF-8编码方式
	(十六进制) 		 | （二进制）
—————————————————————–
0000 0000-0000 007F | 0xxxxxxx（兼容原来的ASCII）
0000 0080-0000 07FF | 110xxxxx 10xxxxxx
0000 0800-0000 FFFF | 1110xxxx 10xxxxxx 10xxxxxx
0001 0000-0010 FFFF | 11110xxx 10xxxxxx 10xxxxxx 10xxxxxx
```



![image-20210928174042735](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210930183140338-16329979018773.png)

![image-20210928174255631](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210930181641968-16329970032162.png)

- **编码：** 字符串----->字节数组
- **解码：** 字节数组---->字符串
- **转换流的编码应用**
	- 可以将字符按指定编码格式存储
	- 可以对文本数据按指定编码格式来解读
	- 指定编码表的动作由构造器完成  



#### 七、处理流之三：标准输入、输出流

- System.in和System.out分别代表了系统标准的输入和输出设备
- 默认输入设备是： 键盘， 输出设备是：显示器
- System.in的类型是InputStream
- System.out的类型是PrintStream，其是OutputStream的子类
	- FilterOutputStream 的子类
- 重定向：通过System类的setIn， setOut方法对默认设备进行改变。
	- public static void setIn(InputStream in)
	- public static void setOut(PrintStream out)  

**<font color='blue'>练习1：</font>**从键盘输入字符串，要求将读取到的整行字符串转成大写输出。然后继续进行输入操作，直至当输入“e”或者“exit”时，退出程序。  

##### 方式一：使用Scanner

> ```java
> //方式一：使用Scanner实现
> public static void main(String[] args) {
>     Scanner scan = new Scanner(System.in);
>     while(true){
>         String data = scan.next();
>         if ("e".equalsIgnoreCase(data) || "exit".equalsIgnoreCase(data)){
>             System.out.println("程序结束！");
>             break;
>         }
>         String capitalData = data.toUpperCase();
>         System.out.println(capitalData);
>     }
> }
> ```

##### 方式二：使用System.in

> ```java
> //方式二：使用System.in实现
> public static void main(String[] args){
>     BufferedReader br = null;
>     try {
>         InputStreamReader isr = new InputStreamReader(System.in);
>         br = new BufferedReader(isr);
>         while(true){
>             String data = br.readLine();//读一行
>             if ("e".equalsIgnoreCase(data) || "exit".equalsIgnoreCase(data)){
>                 System.out.println("程序结束！");
>                 break;
>             }
>             String capitalData = data.toUpperCase();
>             System.out.println(capitalData);
>         }
>     } catch (IOException e) {
>         e.printStackTrace();
>     } finally {
>         try {
>             if (br != null)
>                 br.close();
>         } catch (IOException e) {
>             e.printStackTrace();
>         }
>     }
> 
> }
> ```



#### 八、处理流之四：打印流

- 实现将基本数据类型的数据格式转化为字符串输出
- 打印流： PrintStream和PrintWriter
	- 提供了一系列重载的print()和println()方法，用于多种数据类型的输出
	- PrintStream和PrintWriter的输出不会抛出IOException异常
	- PrintStream和PrintWriter有自动flush功能
	- PrintStream 打印的所有字符都使用平台的默认字符编码转换为字节。
		- 在需要写入字符而不是写入字节的情况下，应该使用 PrintWriter 类。
	- System.out返回的是PrintStream的实例  

```java
public static void main(String[] args){
    PrintStream ps = null;
	try {
        FileOutputStream fos = new FileOutputStream(new File("D:\\IO\\text.txt"));
// 创建打印输出流,设置为自动刷新模式(写入换行符或字节 '\n' 时都会刷新输出缓冲区)
        ps = new PrintStream(fos, true);
        if (ps != null) {// 把标准输出流(控制台输出)改成文件
            System.setOut(ps);
        }
        for (int i = 0; i <= 255; i++) { // 输出ASCII字符
            System.out.print((char) i);
            if (i % 50 == 0) { // 每50个数据一行
                System.out.println(); // 换行
            }
        }
    } catch (FileNotFoundException e) {
        e.printStackTrace();
    } finally {
        if (ps != null) {
            ps.close();
        }
    }
}

```



#### 九、处理流之五：数据流  

- 为了方便地操作Java语言的基本数据类型和String的数据，可以使用数据流。

- 数据流有两个类： (用于读取和写出基本数据类型、 String类的数据）

	- DataInputStream 和 DataOutputStream
	- **作用：**<font color='red'>用于读取或者写出基本数据类型的变量或字符串</font>
	- 分别“套接”在 InputStream 和 OutputStream 子类的流上

- DataInputStream中的方法

	- > boolean readBoolean()
		>
		> double readDouble()
		>
		> String readUTF()
		>
		> long readLong()
		>
		> char readChar()
		>
		> byte readByte()
		>
		> float readFloat() 
		>
		> short readShort()
		>
		> int readInt()
		>
		> void readFully(byte[] b)

- DataOutputStream中的方法
	- 将上述的方法的read改为相应的write即可。
	- **注意读取不同类型的数据的顺序要与当初写入文件时，保存的数据的顺序一致。**

```java
@Test//写进去
public void test(){
    DataOutputStream dos = null;
    try { // 创建连接到指定文件的数据输出流对象
        dos = new DataOutputStream(new FileOutputStream("destData.dat"));
        dos.writeUTF("我爱北京天安门"); // 写UTF字符串
        dos.writeBoolean(false); // 写入布尔值
        dos.writeLong(1234567890L); // 写入长整数
        System.out.println("写文件成功!");
    } catch (IOException e) {
        e.printStackTrace();
    } finally { // 关闭流对象
        try {
            if (dos != null) {
// 关闭过滤流时,会自动关闭它包装的底层节点流
                dos.close();
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```



```java
@Test//读出来
public void test(){
    DataInputStream dis = null;
    try {
        dis = new DataInputStream(new FileInputStream("destData.dat"));
        String info = dis.readUTF();
        boolean flag = dis.readBoolean();
        long time = dis.readLong();
        System.out.println(info);
        System.out.println(flag);
        System.out.println(time);
    } catch (Exception e) {
        e.printStackTrace();
    } finally {
        if (dis != null) {
            try {
                dis.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}
```



#### 十、处理流之六：对象流  

- ObjectInputStream和OjbectOutputSteam
	- 用于存储和读取基本数据类型数据或对象的处理流。它的强大之处就是可以把Java中的对象写入到数据源中，也能把对象从数据源中还原回来。
- 序列化： 用ObjectOutputStream类保存基本类型数据或对象的机制
- 反序列化： 用ObjectInputStream类读取基本类型数据或对象的机制
- **ObjectOutputStream和ObjectInputStream不能序列化static和transient修饰的成员变量**  

##### 1、对象的序列化

- <font color='red'>**对象序列化机制**</font>允许把内存中的Java对象转换成平台无关的二进制流，从而允许把这种二进制流持久地保存在磁盘上，或通过网络将这种二进制流传输到另一个网络节点。 //当其它程序获取了这种二进制流，就可以恢复成原来的Java对象
- 序列化的好处在于可将任何实现了Serializable接口的<font color='red'>**对象转化为字节数据**</font>，使其在保存和传输时可被还原
- 序列化是 RMI（Remote Method Invoke – 远程方法调用）过程的参数和返回值都必须实现的机制，而 RMI 是 JavaEE 的基础。因此序列化机制是JavaEE 平台的基础
- **如果需要让某个对象支持序列化机制，则必须让对象所属的类及其属性是可序列化的，为了让某个类是可序列化的，该类必须实现如下两个接口之一。否则，会抛出NotSerializableException异常**
	- <font color='red'>Serializable</font>
	- Externalizable

- 凡是实现Serializable接口的类都有一个表示序列化版本标识符的静态变量：
	- private static final long serialVersionUID;
	- <font color='blue'>**serialVersionUID**</font><font color='red'>用来表明类的不同版本间的兼容性。 简言之，其目的是以序列化对象进行版本控制，有关各版本反序列化时是否兼容。</font>
	- **如果类没有显示定义这个静态常量，它的值是Java运行时环境根据类的内部细节自动生成的。<font color='blue'> 若类的实例变量做了修改， serialVersionUID 可能发生变化。</font> 故建议，显式声明。**
- 简单来说， Java的序列化机制是通过在运行时判断类的serialVersionUID来验证版本一致性的。在进行反序列化时， JVM会把传来的字节流中的serialVersionUID与本地相应实体类的serialVersionUID进行比较，如果相同就认为是一致的，可以进行反序列化，否则就会出现序列化版本不一致的异常。 (InvalidCastException)  



【就是《自定义类》定义结束后，序列化写入到文件中，没显式声明<font color='blue'>**serialVersionUID**</font>的话，会系统默认生成一个值，**但是**当《自定义类》修改了某个参数后，此时系统分配的<font color='blue'>**serialVersionUID**</font>值就变了，跟文件中的那个值不一样了，在反序列化读对象时，就会报错】



<font color='red'>**序列化：将对象写入到磁盘或者进行网络传输。**</font>
**要求：对象必须实现序列化，实现**  

```java
ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream(“data.txt"));//指定对象存储位置
Person p = new Person("韩梅梅", 18, "中华大街", new Pet());//new一个对象
oos.writeObject(p);//把这个对象存到文件中
oos.flush();//刷新
oos.close();//关闭流
```

##### 2、使用对象流序列化对象  

- 若某个类实现了 Serializable 接口，该类的对象就是可序列化的：
	- 创建一个 ObjectOutputStream
	- 调用 ObjectOutputStream 对象的 writeObject(对象) 方法输出可序列化对象
	- 注意写出一次，操作flush()一次
- 反序列化
	- 创建一个 ObjectInputStream
	- 调用 readObject() 方法读取流中的对象
- 强调： 如果某个类的属性不是基本数据类型或 String 类型，而是另一个引用类型，那么这个引用类型必须是可序列化的，否则拥有该类型的Field 的类也不能序列化  

**<font color='red'>反序列化：将磁盘中的对象数据源读出。  </font>**

```java
ObjectInputStream ois = new ObjectInputStream(new FileInputStream(“data.txt"));//找到文件位置
Person p1 = (Person)ois.readObject();//读入对象
System.out.println(p1.toString());//输出对象toString
ois.close();//关闭流
```



##### 3、自定义一个可序列化的类

要求：

1. 需要实现接口：Serializable或者Externalizable

2. 需要当前类提供一个全局常量：serialVersionUID；和自定义异常类一致

	```java
	public static final long serialVersionUID = 342354346476L;//具体值不做要求
	```

​    3.除了当前的<自定义类>需要实现Serializable接口之外，还需要保证其内部所有属性也必须时可序列化的。



```java
public class SerializableTest implements Serializable {
    public static final long serialVersionUID = 342354346476L;

    //Fields
    private String name;
    private int age;
    //Constructors
    public SerializableTest(String name, int age) {
        this.name = name;
        this.age = age;
    }
    //Methods
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "SerializableTest{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
```



#### 十一、随机存取文件流

##### 1、RandomAccessFile 类  

- RandomAccessFile 声明在java.io包下，但直接继承于java.lang.Object类。 并且它实现了DataInput、 DataOutput这两个接口，也就意味着这个类既**可以读也可以写**。
- RandomAccessFile 类支持 “随机访问” 的方式，程序可以直接跳到文件的任意地方来读、写文件
	- 支持只访问文件的部分内容
	- 可以向已存在的文件后追加内容
- RandomAccessFile 对象包含一个记录指针，用以标示当前读写处的位置。
	- RandomAccessFile 类对象可以自由移动记录指针：
		- long getFilePointer()： 获取文件记录指针的当前位置
		- **void seek(long pos)**： 将文件记录指针定位到 pos 位置  

- 构造器
	- public RandomAccessFile(File file, String mode)
	- public RandomAccessFile(String name, String mode)
- 创建 <font color='blue'>RandomAccessFile 类实例需要指定一个 mode 参数，该参数指定 RandomAccessFile 的访问模式：</font>
	- **r**: 以只读方式打开
	- **rw**：打开以便读取和写入
	- **rwd**:打开以便读取和写入；同步文件内容的更新
	- **rws**:打开以便读取和写入； 同步文件内容和元数据的更新
- 如果模式为只读r。则不会创建文件，而是会去读取一个已经存在的文件，如果读取的文件不存在则会出现异常。 如果模式为rw读写。如果<font color='blue'>文件不存在则会去创建文件，如果存在则不会创建。  </font>

###### **一、读取文件内容** 

> ```java
> RandomAccessFile raf = new RandomAccessFile(“test.txt”, “rw”） ;
> raf.seek(5);
> byte [] b = new byte[1024];
> int off = 0;
> int len = 5;
> raf.read(b, off, len);
> String str = new String(b, 0, len);
> System.out.println(str);
> raf.close();
> ```



###### **二、写入文件内容**

> ```java
> RandomAccessFile raf = new RandomAccessFile("test.txt", "rw");
> raf.seek(5);
> //先读出来
> String temp = raf.readLine();
> raf.seek(5);
> raf.write("xyz".getBytes());
> raf.write(temp.getBytes());
> raf.close();
> ```



###### **三、 RandomAccessFile实现“<<font color='blue'>插入操作</font>>”文件内容**

①先将要插入后面的数据copy保存

②调指针到带插入位置

③插入数据

④追加原copy的数据

> ```java
> RandomAccessFile raf1 = new RandomAccessFile("hello.txt", "rw");
> raf1.seek(5);
> //方式一：
> //StringBuilder info = new StringBuilder((int) file.length());
> //byte[] buffer = new byte[10];
> //int len;
> //while((len = raf1.read(buffer)) != -1){
> ////info += new String(buffer,0,len);
> //info.append(new String(buffer,0,len));
> //}
> //方式二：
> ByteArrayOutputStream baos = new ByteArrayOutputStream();
> byte[] buffer = new byte[10];
> int len;
> while((len = raf1.read(buffer)) != -1){
> baos.write(buffer, 0, len);
> }
> raf1.seek(5);//指针调到要插入位置
> raf1.write("xyz".getBytes());//插入数据
> raf1.write(baos.toString().getBytes());//插入原指针后面的数据
> baos.close();
> raf1.close();
> ```
>
> 



##### 2、RandomAccessFile类，实现一个多线程断点下载的功能:

我们可以用RandomAccessFile这个类，来实现一个多线程断点下载的功能，用过下载工具的朋友们都知道，下载前都会建立两个临时文件，一个是与被下载文件大小相同的空文件，另一个是记录文件指针的位置文件，每次暂停的时候，都会保存上一次的指针，然后断点下载的时候，会继续从上一次的地方下载，从而实现断点下载或上传的功能.



#### 十二、NIO.2中Path、 Paths、 Files类的使用

##### 1、Java NIO 概述

- Java NIO (New IO， Non-Blocking IO)是从Java 1.4版本开始引入的一套新的IO API，可以替代标准的Java IO API。 NIO与原来的IO有同样的作用和目的，但是使用的方式完全不同， NIO支持面向缓冲区的(IO是面向流的)、基于通道的IO操作。 NIO将以更加高效的方式进行文件的读写操作。
- Java API中提供了两套NIO， 一套是针对标准输入输出NIO， 另一套就是网络编程NIO。
	- |-----java.nio.channels.Channel
		- |-----FileChannel:处理本地文件
		- |-----SocketChannel： TCP网络编程的客户端的Channel
		- |-----ServerSocketChannel:TCP网络编程的服务器端的Channel
		- |-----DatagramChannel： UDP网络编程中发送端和接收端的Channel  

##### 2、NIO. 2

随着 JDK 7 的发布， Java对NIO进行了极大的扩展，增强了对文件处理和文件系统特性的支持，以至于我们称他们为 NIO.2。因为 NIO 提供的一些功能， NIO已经成为文件处理中越来越重要的部分。  

##### 3、NIO.2中Path、 Paths、 Files类的使用

- 早期的Java只提供了一个File类来访问文件系统，但File类的功能比较有限，所提供的方法性能也不高。而且， 大多数方法在出错时仅返回失败，并不会提供异常信息。

- NIO. 2为了弥补这种不足，引入了Path接口，代表一个平台无关的平台路径，描述了目录结构中文件的位置。 Path可以看成是File类的升级版本，实际引用的资源也可以不存在。

- 在以前IO操作都是这样写的:

	```java
	import java.io.File;
	File file = new File("index.html");
	```

	

- 但在Java7 中，我们可以这样写：

	```java
	import java.nio.file.Path;
	import java.nio.file.Paths;
	Path path = Paths.get("index.html");  
	
	
	```

	

- 同时， NIO.2在java.nio.file包下还提供了Files、 Paths工具类， Files包含了大量静态的工具方法来操作文件； Paths则包含了两个返回Path的静态工厂方法。

- Paths 类提供的静态 get() 方法用来获取 Path 对象：

	```java
	static Path get(String first, String … more) // 用于将多个字符串串连成路径
	static Path get(URI uri)// 返回指定uri对应的Path路径  
	```

	

##### 4、Path接口

###### **Path 常用方法：**

> String toString() ： 返回调用 Path 对象的字符串表示形式
>
> boolean startsWith(String path) : 判断是否以 path 路径开始
>
> boolean endsWith(String path) : 判断是否以 path 路径结束
>
> boolean isAbsolute() : 判断是否是绝对路径
>
> Path getParent() ：返回Path对象包含整个路径，不包含 Path 对象指定的文件路径
>
> Path getRoot() ：返回调用 Path 对象的根路径
>
> Path getFileName() : 返回与调用 Path 对象关联的文件名
>
> int getNameCount() : 返回Path 根目录后面元素的数量
>
> Path getName(int idx) : 返回指定索引位置 idx 的路径名称
>
> Path toAbsolutePath() : 作为绝对路径返回调用 Path 对象
>
> Path resolve(Path p) :合并两个路径，返回合并后的路径对应的Path对象
>
> File toFile(): 将Path转化为File类的对象  



##### 5、Files 类

java.nio.file.Files 用于操作文件或目录的工具类。

###### **Files常用方法：**  

> Path copy(Path src, Path dest, CopyOption … how) : 文件的复制
>
> Path createDirectory(Path path, FileAttribute<?> … attr) : 创建一个目录
>
> Path createFile(Path path, FileAttribute<?> … arr) : 创建一个文件
>
> void delete(Path path) : 删除一个文件/目录，如果不存在，执行报错
>
> void deleteIfExists(Path path) : Path对应的文件/目录如果存在，执行删除
>
> Path move(Path src, Path dest, CopyOption…how) : 将 src 移动到 dest 位置
>
> long size(Path path) : 返回 path 指定文件的大小  

###### **Files常用方法：用于判断**

> boolean exists(Path path, LinkOption … opts) : 判断文件是否存在
>
> boolean isDirectory(Path path, LinkOption … opts) : 判断是否是目录
>
> boolean isRegularFile(Path path, LinkOption … opts) : 判断是否是文件
>
> boolean isHidden(Path path) : 判断是否是隐藏文件
>
> boolean isReadable(Path path) : 判断文件是否可读
>
> boolean isWritable(Path path) : 判断文件是否可写
>
> boolean notExists(Path path, LinkOption … opts) : 判断文件是否不存在

###### **Files常用方法：用于操作内容**

> SeekableByteChannel newByteChannel(Path path, OpenOption…how) : 获取与指定文件的连接， how 指定打开方式。
>
> DirectoryStream<Path> newDirectoryStream(Path path) : 打开 path 指定的目录
>
> InputStream newInputStream(Path path, OpenOption…how):获取 InputStream 对象
>
> OutputStream newOutputStream(Path path, OpenOption…how) : 获取 OutputStream 对象  



------

### 8、网络编程

#### 一、网络编程概述

------

- Java是 Internet 上的语言，它从语言级上提供了对网络应用程序的支持，程序员能够很容易开发常见的网络应用程序。
- Java提供的网络类库，可以实现无痛的网络连接，联网的底层细节被隐藏在 Java 的本机安装系统里，由 JVM 进行控制。并且 Java 实现了一个跨平台的网络库， <font color='blue'>程序员面对的是一个统一的网络编程环境。  </font>

**网络基础:**

- 计算机网络：
	把分布在不同地理区域的计算机与专门的外部设备用通信线路互连成一个规模大、功能强的网络系统，从而使众多的计算机可以方便地互相传递信息、共享硬件、软件、数据信息等资源。
- 网络编程的目的：
	<font color='blue'>直接或间接地通过网络协议与其它计算机实现数据交换，进行通讯。</font>
- 网络编程中有两个主要的问题：
	- <font color='blue'>如何准确地定位网络上一台或多台主机；定位主机上的特定的应用</font>
	- <font color='blue'>找到主机后如何可靠高效地进行数据传输  </font>



#### 二、网络通信要素概述

------

##### 1、如何实现网络中的主机互相通信？

- **通信双方地址**
	- IP
	- 端口号
- **一定的规则（即：网络通信协议。有两套参考模型）**
	- OSI参考模型：模型过于理想化，未能在因特网上进行广泛推广
	- TCP/IP参考模型(或TCP/IP协议)：事实上的国际标准。  

##### 2、网络通信协议

![image-20210930181617528](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210930193451291-16330016925131.png)



![image-20210930181641968](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210930193516079-16330017171862.png)



#### 三、通信要素1： IP和端口号

------

##### 1、IP 地址： InetAddress

- 唯一的标识 Internet 上的计算机（通信实体）
- **本地回环地址(hostAddress)： 127.0.0.1       主机名(hostName)： localhost**
- IP地址分类方式1： <font color='blue'>IPV4</font> 和 <font color='blue'>IPV6</font>
	- **IPV4：** 4个字节组成， 4个0-255。大概42亿， 30亿都在北美，亚洲4亿。 2011年初已经用尽。 以点分十进制表示，如192.168.0.1
	- **IPV6：** 128位（16个字节） ， 写成8个无符号整数，每个整数用四个十六进制位表示，数之间用冒号（：）分开，如： 3ffe:3201:1401:1280:c8ff:fe4d:db39:1984
- IP地址分类方式2： <font color='blue'>公网地址(万维网使用)</font>和<font color='blue'>私有地址(局域网使用)</font>。 192.168. 开头的就是私有址址，范围即为192.168.0.0--192.168.255.255，专门为组织机构内部使用
- 特点：不易记忆

##### 2、端口号：标识正在计算机上运行的进程（程序）

- 不同的进程有不同的端口号
- 被规定为一个 16 位的整数 0~65535。
- 端口分类：
	- <font color='blue'>公认端口</font>： 0~1023。被预先定义的服务通信占用（如： HTTP占用端口80， FTP占用端口21， Telnet占用端口23）
	- <font color='blue'>注册端口</font>： 1024~49151。分配给用户进程或应用程序。（如： Tomcat占用端口8080， MySQL占用端口3306， Oracle占用端口1521等） 。
	- <font color='blue'>动态/私有端口</font>： 49152~65535。
- <font color='blue'>端口号与IP地址的组合得出一个网络套接字： Socket。 </font>

![image-20210930183140338](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210930183658900-16329982205734.png)

##### 3、InetAddress类

- Internet上的主机有两种方式表示地址：
	- <font color='red'>域名(hostName)</font>： www.123.com
	- <font color='red'>IP 地址(hostAddress)</font>： 202.108.35.210
	
- InetAddress类主要表示IP地址， 两个子类： Inet4Address、 Inet6Address。

- InetAddress 类 对 象 含 有 一 个 Internet 主 机 地 址 的 域 名 和 IP 地 址 ：www.123.com 和 202.108.35.210。

- 域名容易记忆，当在连接网络时输入一个主机的域名后， 域名服务器(DNS)负责将域名转化成IP地址，这样才能和主机建立连接。<font color='blue'> -------域名解析</font>

	

![image-20210930183658900](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211001160041139-16330752435584.png)

###### 3.1  InetAddress类创建对象

InetAddress类没有提供公共的构造器，而是提供了如下几个静态方法来获取InetAddress实例

- public static InetAddress getLocalHost()  获取本机地址
- public static InetAddress getByName(String host)  

###### 3.2  InetAddress的常用的方法

- public String getHostAddress()： 返回 IP 地址字符串（以文本表现形式）。
- public String getHostName()： 获取此 IP 地址的主机名
- public boolean isReachable(int timeout)： 测试是否可以达到该地址  

```java
public class InetAddressTest {
    public static void main(String[] args){
        try {
            //1、获取对象（实例）
            InetAddress inet1 = InetAddress.getByName("192.168.15.99");
            System.out.println(inet1);///192.168.15.99

            InetAddress inet2 = InetAddress.getByName("www.baidu.com");
            System.out.println(inet2);//www.baidu.com/220.181.38.150

            InetAddress inetLocal = InetAddress.getByName("127.0.0.1");
            System.out.println(inetLocal);///127.0.0.1

            InetAddress localHost = InetAddress.getLocalHost();
            System.out.println(localHost);//DELL/10.11.143.14

            //2、常用方法
            
            // 返回 IP 地址字符串（以文本表现形式） 。
            System.out.println(inet2.getHostAddress());//220.181.38.149
            //获取此 IP 地址的主机名
            System.out.println(inet2.getHostName());//www.baidu.com
            //测试是否可以达到该地址 
            System.out.println(inet2.isReachable(88));//true

        } catch (UnknownHostException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }

    }
}
```



#### 四、通信要素2：网络协议

------

- **网络通信协议**
	计算机网络中实现通信必须有一些约定，即**通信协议**， 对<font color='blue'>速率、传输代码、代码结构、传输控制步骤、出错控制等制定标准。</font>
- **问题：网络协议太复杂**
	计算机网络通信涉及内容很多，比如指定源地址和目标地址，加密解密，压缩解压缩，差错控制，流量控制，路由控制，如何实现如此复杂的网络协议呢？
- **通信协议分层的思想**
	在制定协议时，把复杂成份分解成一些简单的成份，再将它们复合起来。最常用的复合方式是层次方式，即<font color='blue'>同层间可以通信、上一层可以调用下一层，而与再下一层不发生关系</font>。各层互不影响，利于系统的开发和扩展。  

##### 1、TCP/IP协议簇

- 传输层协议中有两个非常重要的协议：
	- 传输控制协议TCP(Transmission Control Protocol)
	- 用户数据报协议UDP(User Datagram Protocol)。
- <font color='blue'>TCP/IP 以其两个主要协议：传输控制协议(TCP)和网络互联协议(IP)而得名</font>，实际上是一组协议，包括多个具有不同功能且互为关联的协议。
- IP(Internet Protocol)协议是网络层的主要协议，支持网间互连的数据通信。
- TCP/IP协议模型从更实用的角度出发，形成了高效的四层体系结构，即<font color='blue'>物理链路层、 IP层、传输层和应用层。  </font>

##### 2、TCP 和 UDP

- **<font color='red'>TCP协议：</font>**【先建立连接，再传输-------打电话】
	- 使用TCP协议前，须先建立TCP连接，形成传输数据通道
	- 传输前，采用“三次握手” 方式，点对点通信， <font color='red'>是可靠的</font>
	- TCP协议进行通信的两个应用进程：客户端、 服务端。
	- 在连接中<font color='red'>可进行大数据量的传输</font>
	- 传输完毕，<font color='red'>需释放已建立的连接， 效率低</font>
- <font color='red'>**UDP协议：**</font>【直接传输-------发短信】
	- 将数据、源、目的封装成数据包，<font color='red'> 不需要建立连接</font>
	- 每个数据报的大小限制在64K内
	- 发送不管对方是否准备好，接收方收到也不确认， 故是不可靠的
	- 可以广播发送
	- 发送数据结束时<font color='red'>无需释放资源，开销小，速度快</font>

##### 3、TCP三次握手

![image-20210930193451291](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211001170325721-16330790068125.png)



##### 4、TCP四次挥手

![image-20210930193516079](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211001171120983-16330794828366.png)

##### 5、Socket

- 利用套接字(Socket)开发网络应用程序早已被广泛的采用，以至于成为事实上的标准。
- <font color='red'>网络上具有唯一标识的IP地址和端口号组合在一起才能构成唯一能识别的标识符套接字。</font>
- 通信的两端都要有Socket，是两台机器间通信的端点。
- 网络通信其实就是Socket间的通信。
- Socket允许程序把网络连接当成一个流， 数据在两个Socket间通过IO传输。
- 一般主动发起通信的应用程序属客户端，等待通信请求的为服务端。
- Socket分类：
	- <font color='red'>流套接字（stream socket）：使用TCP提供可依赖的字节流服务</font>
	- <font color='red'>数据报套接字（datagram socket）：使用UDP提供“尽力而为”的数据报服务</font>

###### 5.1  Socket类的常用构造器：

- **public Socket(InetAddress address,int port)**创建一个流套接字并将其连接到指定 IP 地址的指定端口号。
- **public Socket(String host,int port)**创建一个流套接字并将其连接到指定主机上的指定端口号。  



###### 5.2  Socket类的常用方法：

- **public InputStream getInputStream()**返回此套接字的输入流。 可以用于接收网络消息
- **public OutputStream getOutputStream()**返回此套接字的输出流。 可以用于发送网络消息
- **public InetAddress getInetAddress()**此套接字连接到的远程 IP 地址；如果套接字是未连接的， 则返回null。
- **public InetAddress getLocalAddress()**获取套接字绑定的本地地址。 即本端的IP地址
- **public int getPort()**此套接字连接到的远程端口号；如果尚未连接套接字， 则返回 0。
- **public int getLocalPort()**返回此套接字绑定到的本地端口。 如果尚未绑定套接字， 则返回 -1。 即本端的端口号。
- **public void close()**关闭此套接字。 套接字被关闭后， 便不可在以后的网络连接中使用（即无法重新连接或重新绑定） 。 需要创建新的套接字对象。 关闭此套接字也将会关闭该套接字的 InputStream 和OutputStream。
- **public void shutdownInput()**如果在套接字上调用 shutdownInput() 后从套接字输入流读取内容， 则流将返回 EOF（文件结束符） 。 即不能在从此套接字的输入流中接收任何数据。
- **public void shutdownOutput()**禁用此套接字的输出流。 对于 TCP 套接字， 任何以前写入的数据都将被发送， 并且后跟 TCP 的正常连接终止序列。 如果在套接字上调用 shutdownOutput() 后写入套接字输出流，则该流将抛出 IOException。 即不能通过此套接字的输出流发送任何数据。  





#### 五、TCP网络编程

------

##### 1、基于Socket的TCP编程

- <font color='blue'>客户端Socket的工作过程包含以下四个基本的步骤：</font>
	- <font color='blue'>创建 Socket：</font> 根据指定服务端的 IP 地址或端口号构造 Socket 类对象。若服务器端响应，则建立客户端到服务器的通信线路。若连接失败，会出现异常。
	- <font color='blue'>打开连接到 Socket 的输入/出流：</font> 使用 getInputStream()方法获得输入流，使用getOutputStream()方法获得输出流，进行数据传输
	- <font color='blue'>按照一定的协议对 Socket 进行读/写操作：</font> 通过输入流读取服务器放入线路的信息（但不能读取自己放入线路的信息），通过输出流将信息写入线程。
	- <font color='blue'>关闭 Socket：</font> 断开客户端到服务器的连接，释放线路

###### 1.1  客户端创建Socket对象

- 客户端程序可以使用Socket类创建对象，<font color='blue'> 创建的同时会自动向服务器方发起连接</font>。 Socket的构造器是：
	- <font color='blue'>Socket(String host,int port)  throws UnknownHostException,IOException</font>： 向服务器(域名是host。端口号为port)发起TCP连接，若成功，则创建Socket对象，否则抛出异常。
	- <font color='blue'>Socket(InetAddress address,int port)  throws IOException</font>： 根据InetAddress对象所表示的IP地址以及端口号port发起连接。
	- 客户端建立socketAtClient对象的过程就是向服务器发出套接字连接请求  

```java
//client端
Socket s = new
Socket(“192.168.40.165” ,9999);
OutputStream out = s.getOutputStream();
out.write(" hello".getBytes());
s.close();
```

- <font color='red'>服务器程序的工作过程包含以下四个基本的步骤：</font>
	- <font color='red'>调用 ServerSocket(int port) </font>： 创建一个服务器端套接字，并绑定到指定端口上。用于监听客户端的请求。
	- <font color='red'>调用 accept()</font>： 监听连接请求，如果客户端请求连接，则接受连接，返回通信套接字对象。
	- <font color='red'>调用 该Socket类对象的 getOutputStream() 和 getInputStream ()</font>： 获取输出流和输入流，开始网络数据的发送和接收。
	- <font color='red'>关闭ServerSocket和Socket对象</font>： 客户端访问结束，关闭通信套接字。  

###### 1.2  服务器建立 ServerSocket 对象

- ServerSocket 对象负责等待客户端请求建立套接字连接，类似邮局某个窗口中的业务员。也就是说， <font color='red'>服务器必须事先建立一个等待客户请求建立套接字连接的ServerSocket对象。</font>
- 所谓“接收”客户的套接字请求，就是accept()方法会返回一个 Socket 对象  

```java
//server端
ServerSocket ss = new ServerSocket(9999);
Socket s = ss.accept ();
InputStream in = s.getInputStream();
byte[] buf = new byte[1024];
int num = in.read(buf);
String str = new String(buf,0,num);
System.out.println(s.getInetAddress().toString()+” :” +str);
s.close();
ss.close();
```

###### 1.3  总结：

![image-20211001151241703](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211001151241703-16330723634863.png)

###### 1.4  练习题一：

客户端发送内容给服务端，服务端将内容打印到控制台上。  

> ```java
> import org.junit.Test;
> import java.io.ByteArrayOutputStream;
> import java.io.IOException;
> import java.io.InputStream;
> import java.io.OutputStream;
> import java.net.InetAddress;
> import java.net.ServerSocket;
> import java.net.Socket;
> 
> /**
>  * @ClassName TCPTest1
>  * @Description TODO:实现TCP网络编程
>  * 例子一：客户端发送内容给服务端，服务端将内容打印到控制台上。
>  * @Author sth_199509@163.com
>  * @Date 2021/9/30 21:12
>  * @Version 1.0
>  */
> public class TCPTest1 {
>     //服务端
>     @Test
>     public void server(){
>         ServerSocket serverSocket = null;
>         Socket accept = null;
>         InputStream inputStream = null;
>         ByteArrayOutputStream byaos = null;
>         try {
>             //1、创建创建服务器端的serverSocket，指明自己的端口号
>             serverSocket = new ServerSocket(2789);
>             //2、调用accept()表示接收来自于客户端的socket
>             accept = serverSocket.accept();
>             //3、获取输入流
>             inputStream = accept.getInputStream();
>             //4、读取输入流中的数据
>             byaos = new ByteArrayOutputStream();
>             byte[] bytes = new byte[5];
>             int len;
>             while((len = inputStream.read(bytes)) != -1){
>                 byaos.write(bytes,0,len);
>             }
>             System.out.println(byaos.toString());
>             System.out.println("收到来自于：" + accept.getInetAddress().getHostAddress() + "的文件");//输出发送文件的客户端的IP，
>         } catch (IOException e) {
>             e.printStackTrace();
>         } finally {
>             //5、资源的关闭
>             if (byaos != null) {
>                 try {
>                     byaos.close();
>                 } catch (IOException e) {
>                     e.printStackTrace();
>                 }
>             }
>             if (inputStream != null) {
>                 try {
>                     inputStream.close();
>                 } catch (IOException e) {
>                     e.printStackTrace();
>                 }
>             }
>             if (accept != null) {
>                 try {
>                     accept.close();
>                 } catch (IOException e) {
>                     e.printStackTrace();
>                 }
>             }
>             if (serverSocket != null) {
>                 try {
>                     serverSocket.close();
>                 } catch (IOException e) {
>                     e.printStackTrace();
>                 }
>             }
>         }
>     }
> 
>     //客户端
>     @Test
>     public void client(){
>         Socket socket = null;
>         OutputStream outputStream = null;
>         try {
>             //1、创建Socket对象，指明服务器端的IP和端口号
>             InetAddress byName = InetAddress.getByName("127.0.0.1");
>             socket = new Socket(byName, 2789);
>             //2、获取一个输出流，用于输出数据
>             outputStream = socket.getOutputStream();
>             //3、写出数据操作
>             outputStream.write("你好!,我是客户端！".getBytes());
>         } catch (IOException e) {
>             e.printStackTrace();
>         } finally {
>             //4、资源关闭
>             if (outputStream != null){
>                 try {
>                     outputStream.close();
>                 } catch (IOException e) {
>                     e.printStackTrace();
>                 }
> 
>             }
>             if (socket != null){
>                 try {
>                     socket.close();
>                 } catch (IOException e) {
>                     e.printStackTrace();
>                 }
>             }
>         }
>     }
> }
> ```



###### 1.5  练习题二：

客户端发送文件给服务端， 服务端将文件保存在本地。  

> ```java
> import org.junit.Test;
> import java.io.*;
> import java.net.InetAddress;
> import java.net.ServerSocket;
> import java.net.Socket;
> 
> /**
>  * @ClassName TCPTest2
>  * @Description TODO:实现TCP网络编程
>  * 练习二：客户端发送文件给服务端，服务端将文件保存在本地。
>  * @Author sth_199509@163.com
>  * @Date 2021/10/1 14:09
>  * @Version 1.0
>  */
> public class TCPTest2 {
>     //服务端
>     @Test
>     public void server(){
>         ServerSocket serverSocket = null;
>         Socket accept = null;
>         InputStream inputStream = null;
>         ByteArrayOutputStream byaos = null;
>         FileOutputStream fout = null;
>         try {
>             //1、创建创建服务器端的serverSocket，指明自己的端口号
>             serverSocket = new ServerSocket(2789);
>             //2、调用accept()表示接收来自于客户端的socket
>             accept = serverSocket.accept();
>             //3、获取输入流
>             inputStream = accept.getInputStream();
>             fout = new FileOutputStream(new File("carCopyyy.jpg"));
>             //4、读取输入流中的数据
>             byte[] bytes = new byte[1024];
>             int len;
>             while((len = inputStream.read(bytes)) != -1){
>                 fout.write(bytes,0,len);
>             }
>             System.out.println("收到来自于：" + accept.getInetAddress().getHostAddress() + "的文件");//输出发送文件的客户端的IP，
>         } catch (IOException e) {
>             e.printStackTrace();
>         } finally {
>             //5、资源的关闭
>             if (fout != null){
>                 try {
>                     fout.close();
>                 } catch (IOException e) {
>                     e.printStackTrace();
>                 }
>             }
>             if (byaos != null) {
>                 try {
>                     byaos.close();
>                 } catch (IOException e) {
>                     e.printStackTrace();
>                 }
>             }
>             if (inputStream != null) {
>                 try {
>                     inputStream.close();
>                 } catch (IOException e) {
>                     e.printStackTrace();
>                 }
>             }
>             if (accept != null) {
>                 try {
>                     accept.close();
>                 } catch (IOException e) {
>                     e.printStackTrace();
>                 }
>             }
>             if (serverSocket != null) {
>                 try {
>                     serverSocket.close();
>                 } catch (IOException e) {
>                     e.printStackTrace();
>                 }
>             }
>         }
>     }
> 
>     //客户端
>     @Test
>     public void client(){
>         Socket socket = null;
>         OutputStream outputStream = null;
>         FileInputStream finput = null;
>         try {
>             //1、创建Socket对象，指明服务器端的IP和端口号
>             InetAddress byName = InetAddress.getByName("127.0.0.1");
>             socket = new Socket(byName, 2789);
>             //2、获取一个输出流，用于输出数据
>             outputStream = socket.getOutputStream();
>             finput = new FileInputStream(new File("car.jpg"));
>             //3、读入数据操作
>             byte[] bytes = new byte[1024];
>             int len;
>             while((len = finput.read(bytes)) != -1){
>                 //发送数据
>                 outputStream.write(bytes,0,len);
>             }
>         } catch (IOException e) {
>             e.printStackTrace();
>         } finally {
>             //4、资源关闭
>             if (finput != null){
>                 try {
>                     finput.close();
>                 } catch (IOException e) {
>                     e.printStackTrace();
>                 }
>             }
>             if (outputStream != null){
>                 try {
>                     outputStream.close();
>                 } catch (IOException e) {
>                     e.printStackTrace();
>                 }
> 
>             }
>             if (socket != null){
>                 try {
>                     socket.close();
>                 } catch (IOException e) {
>                     e.printStackTrace();
>                 }
>             }
>         }
>     }
> }
> ```



###### 1.6  练习题三：【标准步骤版-----未处理异常】

从客户端发送文件给服务端，服务端保存到本地。并返回“发送成功”给客户端。并关闭相应的连接。  

> ```java
> import org.junit.Test;
> import java.io.*;
> import java.net.InetAddress;
> import java.net.ServerSocket;
> import java.net.Socket;
> 
> /**
>  * @ClassName TCPTest3
>  * @Description TODO:实现TCP网络编程
>  * 练习三：从客户端发送文件给服务端，服务端保存到本地。并返回“发送成功”给客户端。并关闭相应的连接。
>  * @Author sth_199509@163.com
>  * @Date 2021/10/1 14:27
>  * @Version 1.0
>  */
> public class TCPTest3 {
>     //服务端
>     @Test
>     public void server()throws IOException{
>         //1、创建创建服务器端的serverSocket，指明自己的端口号
>         ServerSocket serverSocket = new ServerSocket(2789);
> 
>         //2、调用accept()表示接收来自于客户端的socket
>         Socket accept = serverSocket.accept();
> 
>         //3、获取输入流
>         InputStream inputStream = accept.getInputStream();
>         FileOutputStream fout = new FileOutputStream(new File("carCopyy22y.jpg"));
> 
>         //4、读取输入流中的数据
>         byte[] bytes = new byte[1024];
>         int len;
>         while((len = inputStream.read(bytes)) != -1){
>             fout.write(bytes,0,len);
>         }
>         //在控制台输出文件来自何方
>         System.out.println("收到来自于：" + accept.getInetAddress().getHostAddress() + "的文件");//输出发送文件的客户端的IP，
> 
>         //5、服务器端给与客户端反馈
>         OutputStream outputStream = accept.getOutputStream();
>         outputStream.write("你好客户端，我已经成功接收了你发送的文件。".getBytes());
> 
>         //6、资源的关闭
>         outputStream.close();
>         fout.close();
>         inputStream.close();
>         accept.close();
>         serverSocket.close();
>     }
> 
>     //客户端
>     @Test
>     public void client() throws IOException {
>         //1、创建Socket对象，指明服务器端的IP和端口号
>         InetAddress byName = InetAddress.getByName("127.0.0.1");
>         Socket socket = new Socket(byName, 2789);
> 
>         //2、获取一个输出流，用于输出数据
>         OutputStream outputStream = socket.getOutputStream();
>         FileInputStream finput = new FileInputStream(new File("car.jpg"));
> 
>         //3、读入数据操作
>         byte[] bytes = new byte[1024];
>         int len;
>         while((len = finput.read(bytes)) != -1){
>             //发送数据
>             outputStream.write(bytes,0,len);
>         }
>         //关闭数据输出【使服务器端知道，文件发送完了】
>         socket.shutdownOutput();
> 
>         //4、接收服务器端发来的反馈，并输出到控制台
>         InputStream inputStream = socket.getInputStream();
>         ByteArrayOutputStream baos = new ByteArrayOutputStream();
>         byte[] bytes1 = new byte[5];
>         int len1;
>         while((len1 = inputStream.read(bytes1)) != -1){
>             baos.write(bytes1,0,len1);
>         }
>         //将接收到的反馈内容，输出到控制台上
>         System.out.println(baos.toString());
> 
>         //5、资源关闭
>         baos.close();
>         inputStream.close();
>         finput.close();
>         outputStream.close();
>         socket.close();
>     }
> }
> ```



#### 六、UDP网络编程

------

##### 1、UDP网络通信

- 类 DatagramSocket 和 DatagramPacket 实现了基于 UDP 协议网络程序。
- UDP数据报通过数据报套接字 DatagramSocket 发送和接收， 系统不保证
	UDP数据报一定能够安全送到目的地，也不能确定什么时候可以抵达。
- DatagramPacket 对象封装了UDP数据报，在数据报中包含了发送端的IP地址和端口号以及接收端的IP地址和端口号。
- UDP协议中每个数据报都给出了完整的地址信息，因此无须建立发送方和接收方的连接。 如同发快递包裹一样  

##### 2、DatagramSocket 类的常用方法

- public DatagramSocket(int port)创建数据报套接字并将其绑定到本地主机上的指定端口。 套接字将被绑定到通配符地址， IP 地址由内核来选择。
- public DatagramSocket(int port,InetAddress laddr)创建数据报套接字， 将其绑定到指定的本地地址。本地端口必须在 0 到 65535 之间（包括两者） 。 如果 IP 地址为 0.0.0.0， 套接字将被绑定到通配符地址， IP 地址由内核选择。
- public void close()关闭此数据报套接字。
- public void send(DatagramPacket p)从此套接字发送数据报包。 DatagramPacket 包含的信息指示：将要发送的数据、 其长度、 远程主机的 IP 地址和远程主机的端口号。
- public void receive(DatagramPacket p)从此套接字接收数据报包。 当此方法返回时， DatagramPacket的缓冲区填充了接收的数据。 数据报包也包含发送方的 IP 地址和发送方机器上的端口号。 此方法在接收到数据报前一直阻塞。 数据报包对象的 length 字段包含所接收信息的长度。 如果信息比包的长度长， 该信息将被截短。
- public InetAddress getLocalAddress()获取套接字绑定的本地地址。
- public int getLocalPort()返回此套接字绑定的本地主机上的端口号。
- public InetAddress getInetAddress()返回此套接字连接的地址。 如果套接字未连接， 则返回 null。
- public int getPort()返回此套接字的端口。 如果套接字未连接， 则返回 -1。  

- public DatagramPacket(byte[] buf,int length)构造 DatagramPacket， 用来接收长度为 length 的数据包。 length 参数必须小于等于 buf.length。
- public DatagramPacket(byte[] buf,int length,InetAddress address,int port)构造数据报包， 用来将长度为 length 的包发送到指定主机上的指定端口号。 length参数必须小于等于 buf.length。
- public InetAddress getAddress()返回某台机器的 IP 地址， 此数据报将要发往该机器或者是从该机器接收到的。
- public int getPort()返回某台远程主机的端口号， 此数据报将要发往该主机或者是从该主机接收到的。
- public byte[] getData()返回数据缓冲区。 接收到的或将要发送的数据从缓冲区中的偏移量 offset 处开始， 持续 length 长度。
- public int getLength()返回将要发送或接收到的数据的长度。  

##### 3、UDP网络通信流程

- 流 程：
	1. DatagramSocket与DatagramPacket
	2. 建立发送端，接收端
	3. 建立数据包
	4. 调用Socket的发送、 接收方法
	5. 关闭Socket
- 发送端与接收端是两个独立的运行程序  

##### 4、发送端

```java
DatagramSocket ds = null;
InetAddress inet = null;
try {
	ds = new DatagramSocket();
	byte[] by = "你好啊！我叫赛丽亚！".getBytes();
    inet = InetAddress.getByName("127.0.0.1");
    DatagramPacket dp = new DatagramPacket(by, 0, by.length,inet,10000);
	ds.send(dp);
} catch (Exception e) {
	e.printStackTrace();
} finally {
	if (ds != null)
	ds.close();
}
```

##### 5、接收端

在接收端，要指定监听的端口。  

```java
DatagramSocket ds = null;
try {
	ds = new DatagramSocket(10000);
	byte[] by = new byte[1024];
	DatagramPacket dp = new DatagramPacket(by,0, by.length);
	ds.receive(dp);
	String str = new String(dp.getData(), 0, dp.getLength());
	System.out.println(str + "--" + dp.getAddress());
} catch (Exception e) {
	e.printStackTrace();
} finally {
	if (ds != null)
	ds.close();
}
```





#### 七、URL编程

------

##### 1、URL类

- <font color='red'>**URL(Uniform Resource Locator)**</font>：统一资源定位符，它表示 Internet 上某一资源的地址。
- 它是一种具体的URI，即URL可以用来标识一个资源，而且还指明了如何locate这个资源。
- 通过 URL 我们可以访问 Internet 上的各种网络资源，比如最常见的 www， ftp站点。浏览器通过解析给定的 URL 可以在网络上查找相应的文件或其他资源。
- URL的基本结构由5部分组成：
	<font color='red'>**<传输协议>://<主机名>:<端口号>/<文件名>#片段名?参数列表**</font>
	- 例如:
		http://192.168.1.100:8080/helloworld/index.jsp#a?username=shkstart&password=123
	- #片段名：即锚点，例如看小说，直接定位到章节
	- 参数列表格式：参数名=参数值&参数名=参数值....  

##### 2、URL类构造器

- 为了表示URL， java.net 中实现了类 URL。我们可以通过下面的构造器来初始化一个 URL 对象：
	- <font color='red'>public URL (String spec)</font>：通过一个表示URL地址的字符串可以构造一个URL对象。
		- 例如： URL url = new URL ("http://www. atguigu.com/");
	- <font color='red'>public URL(URL context, String spec)</font>：通过基 URL 和相对 URL 构造一个 URL 对象。
		- 例如： URL downloadUrl = new URL(url, “download.html")
	- public URL(String protocol, String host, String file); 
		- 例如： new URL("http","www.atguigu.com", “download. html");
	- public URL(String protocol, String host, int port, String file); 
		- 例如: URL gamelan = newURL("http", "www.atguigu.com", 80, “download.html");
	- URL类的构造器都声明抛出非运行时异常，必须要对这一异常进行处理，通常是用 try-catch 语句进行捕获。  

##### 3、URL类常用方法

- 一个URL对象生成后，其属性是不能被改变的，但可以通过它给定的方法来获取这些属性：

| public String getProtocol( )                        | 获取该URL的协议名                            |
| --------------------------------------------------- | -------------------------------------------- |
| public String getHost( )                            | 获取该URL的主机名                            |
| public String getPort( )                            | 获取该URL的端口号                            |
| <font color='red'>public String getPath( ) </font>  | <font color='red'>获取该URL的文件路径</font> |
| public String getFile( )                            | 获取该URL的文件名                            |
| <font color='red'>public String getQuery( ) </font> | <font color='red'>获取该URL的查询名</font>   |

```java
URL url = new URL("http://localhost:8080/examples/myTest.txt");
System.out.println("getProtocol() :"+url.getProtocol());
System.out.println("getHost() :"+url.getHost());
System.out.println("getPort() :"+url.getPort());
System.out.println("getPath() :"+url.getPath());
System.out.println("getFile() :"+url.getFile());
System.out.println("getQuery() :"+url.getQuery());
```

##### 4、针对HTTP协议的URLConnection类

- URL的方法 openStream()：能从网络上读取数据
- 若希望输出数据，例如向服务器端的 CGI （公共网关接口-Common GatewayInterface-的简称，是用户浏览器和服务器端的应用程序进行连接的接口）程序发送一些数据，则必须先与URL建立连接，然后才能对其进行读写，此时需要使用URLConnection 。
- URLConnection：表示到URL所引用的远程对象的连接。当与一个URL建立连接时，首先要在一个 URL 对象上通过方法 openConnection() 生成对应的 URLConnection对象。如果连接过程失败，将产生IOException.
	- URL netchinaren = new URL ("http://www.atguigu.com/index.shtml");
	- URLConnectonn u = netchinaren.openConnection( );  

- 通过URLConnection对象获取的输入流和输出流，即可以与现有的CGI程序进行交互。

	- public Object getContent( ) throws IOException

	- public int getContentLength( )

	- public String getContentType( )

	- public long getDate( )

	- public long getLastModified( )

	- public InputStream getInputStream( )throws IOException

	- public OutputSteram getOutputStream( )throws IOException  

	- ```java
		//异常处理应该用try-catch-finally，此处用throws仅仅是为了代码方便理解步骤。
		public class URLTest {
		    public static void main(String[] args) throws IOException {
		        //1、创建URL对象
		        URL url = new URL("http://localhost:8080/car,jpg");
		        //2、打开连接
		        HttpURLConnection urlConnection = (HttpURLConnection) url.openConnection();
		        urlConnection.connect();
		        //3、连接中获取流
		        InputStream inputStream = urlConnection.getInputStream();
		        FileOutputStream fout = new FileOutputStream("copyCar.jpg");
		        //4、操作文件读写
		        byte[] bytes = new byte[1024];
		        int len;
		        while((len = inputStream.read(bytes)) != -1){
		            fout.write(bytes,0,len);
		        }
		        //5、关闭资源
		        fout.close();
		        inputStream.close();
		        urlConnection.disconnect();
		    }
		}
		```

##### 5、URI、 URL和URN的区别

- URI，是uniform resource identifier，统一资源标识符， 用来唯一的标识一个资源。而URL是uniform resource locator，统一资源定位符，它是一种具体的URI，即URL可以用来标识一个资源，而且还指明了如何locate这个资源。
- URN， uniform resource name，统一资源命名，是通过名字来标识资源，比如mailto:java-net@java.sun.com。也就是说， URI是以一种抽象的，高层次概念定义统一资源标识，而URL和URN则是具体的资源标识的方式。 URL和URN都是一种URI。
- 在Java的URI中，一个URI实例可以代表绝对的，也可以是相对的，只要它符合URI的语法规则。而URL类则不仅符合语义，还包含了定位该资源的信息，因此它不能是相对的。  

![image-20211001160041139](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211001215928811-16330967719737.png)

##### 6、小 结

- 位于网络中的计算机具有唯一的IP地址，这样不同的主机可以互相区分。
- 客户端－服务器是一种最常见的网络应用程序模型。服务器是一个为其客户端提供某种特定服务的硬件或软件。客户机是一个用户应用程序，用于访问某台服务器提供的服务。 端口号是对一个服务的访问场所，它用于区分同一物理计算机上的多个服务。 套接字用于连接客户端和服务器，客户端和服务器之间的每个通信会话使用一个不同的套接字。 TCP协议用于实现面向连接的会话。
- Java 中有关网络方面的功能都定义在 java.net 程序包中。 Java 用 InetAddress 对象表示 IP地址，该对象里有两个字段：主机名(String) 和 IP 地址(int)。
- 类 Socket 和 ServerSocket 实现了基于TCP协议的客户端－服务器程序。 Socket是客户端和服务器之间的一个连接，连接创建的细节被隐藏了。这个连接提供了一个安全的数据传输通道，这是因为 TCP 协议可以解决数据在传送过程中的丢失、损坏、重复、乱序以及网络拥挤等问题，它保证数据可靠的传送。
- 类 URL 和 URLConnection 提供了最高级网络应用。 URL 的网络资源的位置来同一表示Internet 上各种网络资源。通过URL对象可以创建当前应用程序和 URL 表示的网络资源之间的连接，这样当前程序就可以读取网络资源数据，或者把自己的数据传送到网络上去。  



### 9、Java反射机制

#### 一、Java反射机制概述

------

##### 1、Java Reflection

- Reflection（反射）是被视为<font color='red'>动态语言</font>的关键，反射机制允许程序在执行期借助于Reflection API取得任何类的内部信息，并能直接操作任意对象的内部属性及方法。
- 加载完类之后， 在堆内存的方法区中就产生了一个Class类型的对象（ 一个类只有一个Class对象） ， 这个对象就包含了完整的类的结构信息。 我们可以通过这个对象看到类的结构。<font color='red'>这个对象就像一面镜子， 透过这个镜子看到类的结构， 所以， 我们形象的称之为： **反射**。  </font>

![image-20211001170325721](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211001220551894-16330971533518.png)

##### 2、补充：动态语言 vs 静态语言

###### 2.1  动态语言

> 是一类在运行时可以改变其结构的语言：例如新的函数、对象、甚至代码可以被引进，已有的函数可以被删除或是其他结构上的变化。<font color='red'>通俗点说就是在运行时代码可以根据某些条件改变自身结构。</font>
> 主要动态语言： **Object-C、 C#、 JavaScript、 PHP、 Python、 Erlang。**

###### 2.2  静态语言

> 与动态语言相对应的， <font color='blue'>运行时结构不可变的语言就是静态语言。</font>
>
> 如**Java、 C、C++。**  

Java不是动态语言， 但Java可以称之为<font color='red'>“准动态语言” </font>。 即Java有一定的动态性， 我们可以利用反射机制、 字节码操作获得类似动态语言的特性。Java的动态性让编程的时候更加灵活！  

##### 3、Java反射机制研究及应用  

- Java反射机制提供的功能
	- 在运行时判断任意一个对象所属的类
	- 在运行时构造任意一个类的对象
	- 在运行时判断任意一个类所具有的成员变量和方法
	- 在运行时获取泛型信息
	- 在运行时调用任意一个对象的成员变量和方法
	- 在运行时处理注解
	- 生成动态代理  

##### 4、反射相关的主要API

- **java.lang.Class**:代表一个类
- java.lang.reflect.Method:代表类的方法
- java.lang.reflect.Field:代表类的成员变量
- java.lang.reflect.Constructor:代表类的构造器
- … …  



#### 二、理解Class类并获取Class实例

------

##### 1、Class 类

- **类的加载过程：**

- >  程序经过java.exe命令以后，会生成一个或者多个字节码文件（.class结尾）。
	>
	> 接着我们使用java.exe命令对某个字节码文件进行解释运行。相当于将某个字节码文件加载到内存中。
	>
	> 此过程就称为类的加载。<font color='red'>加载到内存中的类，我们就称为运行时类，此时运行时类，就作为Class的一个实例。</font>
	>
	> 换句话说：Class的实例（对象）就对应着一个运行时类。



在Object类中定义了以下的方法，此方法将被所有子类继承：

- **public final Class getClass()**
	以上的方法返回值的类型是一个Class类，此类是Java反射的源头，实际上所谓反射从程序的运行结果来看也很好理解，即：可以通过对象反射求出类的名称。  

![image-20211001171120983](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211002111616948-16331445787101.png)

- 对象照镜子后可以得到的信息：某个类的属性、方法和构造器、某个类到底实现了哪些接口。对于每个类而言， JRE 都为其保留一个不变的 Class 类型的对象。一个 Class 对象包含了特定某个结构（class/interface/enum/annotation/primitive type/void/[])的有关信息。
	- Class本身也是一个类
	- Class 对象只能由系统建立对象
	- 一个加载的类在 JVM 中只会有一个Class实例
	- 一个Class对象对应的是一个加载到JVM中的一个.class文件
	- 每个类的实例都会记得自己是由哪个 Class 实例所生成
	- 通过Class可以完整地得到一个类中的所有被加载的结构
	- Class类是Reflection的根源，针对任何你想动态加载、运行的类，唯有先获得相应的Class对象  

##### 2、Class类的常用方法

| 方法名                                           | 功能说明                                                     |
| ------------------------------------------------ | ------------------------------------------------------------ |
| static Class forName(String name)                | 返回指定类名 name 的 Class 对象                              |
| Object newInstance()                             | 调用缺省构造函数，返回该Class对象的一个实例                  |
| getName()                                        | 返回此Class对象所表示的实体（类、接口、数组类、基本类型 或void）名称 |
| Class getSuperClass()                            | 返回当前Class对象的父类的Class对象                           |
| Class [] getInterfaces()                         | 获取当前Class对象的接口                                      |
| ClassLoader getClassLoader()                     | 返回该类的类加载器                                           |
| Class getSuperclass()                            | 返回表示此Class所表示的实体的超类的Class                     |
| Constructor[] getConstructors()                  | 返回一个包含某些Constructor对象的数组                        |
| Field[] getDeclaredFields()                      | 返回Field对象的一个数组                                      |
| Method getMethod(String name,Class … paramTypes) | 返回一个Method对象，此对象的形参类型为paramType              |

##### 3、反射的应用举例

- String str = "test4.Person";

- Class clazz = Class.forName(str);

- Object obj = clazz.newInstance();

- Field field = clazz.getField("name");

- field.set(obj, "Peter");

- Object name = field.get(obj);

- System.out.println(name);

	注： test4.Person是test4包下的Person类  

##### 4、获取Class类的实例（四种方法）

1. 前提： 若已知具体的类，通过类的class属性获取， 该方法最为安全可靠，程序性能最高

	- 实例：

	- > ```java
		> //方式一：调用运行时类的属性 ： .class 
		> Class<Person> clazz = Person.class;
		> ```

2. 前提： 已知某个类的实例，调用该实例的getClass()方法获取Class对象

	- 实例： Class clazz = “www.atguigu.com”.getClass();

	- > ```java
		> //方式二：通过运行时类的对象，调用getClass()
		> Person p = new Person();//假设已知某个对象，反求类
		> Class clazz = p.getClass();
		> 
		> Class clazz = “www.atguigu.com”.getClass();//String
		> ```

3. 前提： 已知一个类的全类名，且该类在类路径下， 可通过Class类的静态方法forName()获取，可能抛出ClassNotFoundException

	- 实例： Class clazz = Class.forName(“java.lang.String”);

	- > ```java
		> //方式三：调用Class的静态方法：forName(String classPath)
		> Class clazz = Class.forName("com.atguigu.java.Person");//包括包在内的全名
		> ```

4. 其他方式(不做要求)

	- ClassLoader cl = this.getClass().getClassLoader();

	- Class clazz4 = cl.loadClass(“类的全类名”);  

	- > ```java
		> //方式四：使用类的加载器：ClassLoader
		> ClassLoader cl = test1.getClass().getClassLoader();//test1是当前的类名
		> Class clazz4 = cl.loadClass("com.atguigu.java.Person");  //包括包在内的全名
		> ```

##### 5、哪些类型可以有Class对象？

- class：外部类， 成员(成员内部类， 静态内部类)， 局部内部类， 匿名内部类
- interface： 接口
- []：数组
- enum：枚举
- annotation：注解@interface
- primitive type：基本数据类型
- void  

```java
Class c1 = Object.class;
Class c2 = Comparable.class;
Class c3 = String[].class;
Class c4 = int[][].class;
Class c5 = ElementType.class;
Class c6 = Override.class;
Class c7 = int.class;
Class c8 = void.class;
Class c9 = Class.class;
int[] a = new int[10];
int[] b = new int[100];
Class c10 = a.getClass();
Class c11 = b.getClass();
// 只要元素类型与维度一样，就是同一个Class
System.out.println(c10 == c11);//true    不管数组大小是否相同，只要是维度一样，就可以
```





#### 三、类的加载与ClassLoader的理解

------

##### 1、类的加载过程

当程序主动使用某个类时，如果该类还未被加载到内存中，则系统会通过如下三个步骤来对该类进行初始化。

![image-20211001215928811](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211002180711385.png)

- 加载：将class文件字节码内容加载到内存中，并将这些静态数据转换成方法区的运行时数据结构，然后生成一个代表这个类的java.lang.Class对象，作为方法区中类数据的访问入口（即引用地址）。所有需要访问和使用类数据只能通过这个Class对象。这个加载的过程需要类加载器参与。
- 链接：将Java类的二进制代码合并到JVM的运行状态之中的过程。
	- **验证：**确保加载的类信息符合JVM规范，例如：以cafe开头，没有安全方面的问题
	- **准备：**正式为类变量（static）分配内存并设置类变量默认初始值的阶段，这些内存都将在方法区中进行分配。
	- **解析：**虚拟机常量池内的符号引用（常量名）替换为直接引用（地址）的过程。
- 初始化：
	- 执行类构造器<clinit>()方法的过程。 类构造器<clinit>()方法是由编译期自动收集类中所有类变量的赋值动作和静态代码块中的语句合并产生的。 （类构造器是构造类信息的，不是构造该类对象的构造器） 。
	- 当初始化一个类的时候，如果发现其父类还没有进行初始化，则需要先触发其父类的初始化。
	- 虚拟机会保证一个类的<clinit>()方法在多线程环境中被正确加锁和同步。  

```java
public class ClassLoadingTest {
	public static void main(String[] args) {
		System.out.println(A.m);
	}
}
class A {
	static {
		m = 300;
	}
	static int m = 100;
}
//第二步：链接结束后m=0
//第三步：初始化后， m的值由<clinit>()方法执行决定
// 这个A的类构造器<clinit>()方法由类变量的赋值和静态代码块中的语句按照顺序合并
产生，类似于
// <clinit>(){
// m = 300;
// m = 100;
// }
```

##### 2、什么时候会发生类初始化？  

- 类的主动引用（一定会发生类的初始化）
	- 当虚拟机启动， 先初始化main方法所在的类
	- new一个类的对象
	- 调用类的静态成员（除了final常量） 和静态方法
	- 使用java.lang.reflect包的方法对类进行反射调用
	- 当初始化一个类， 如果其父类没有被初始化， 则先会初始化它的父类
- 类的被动引用（不会发生类的初始化）
	- 当访问一个静态域时， 只有真正声明这个域的类才会被初始化
	- 当通过子类引用父类的静态变量， 不会导致子类初始化
	- 通过数组定义类引用， 不会触发此类的初始化
	- 引用常量不会触发此类的初始化（ 常量在链接阶段就存入调用类的常量池中了）  

```java
public class ClassLoadingTest {
	public static void main(String[] args) {
		// 主动引用：一定会导致A和Father的初始化
		// A a = new A();
		// System.out.println(A.m);
		// Class.forName("com.atguigu.java2.A");
		// 被动引用
		A[] array = new A[5];//不会导致A和Father的初始化
		// System.out.println(A.b);//只会初始化Father
		// System.out.println(A.M);//不会导致A和Father的初始化
	}
	static {
		System.out.println("main所在的类");
	}
}
class Father {
	static int b = 2;
	static {
		System.out.println("父类被加载");
	}
}
class A extends Father {
	static {
		System.out.println("子类被加载");
		m = 300;
	}
	static int m = 100;
	static final int M = 1;
}
```

##### 3、类加载器的作用：  

- 类加载的作用： 将class文件字节码内容加载到内存中， 并将这些静态数据转换成方法区的运行时数据结构， 然后在堆中生成一个代表这个类的java.lang.Class对象， 作为方法区中类数据的访问入口。
- 类缓存： 标准的JavaSE类加载器可以按要求查找类， 但一旦某个类被加载到类加载器中， 它将维持加载（缓存） 一段时间。 不过JVM垃圾回收机制可以回收这些Class对象。  

![image-20211001220551894](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211002183054277-16331706560454.png)

##### 4、ClassLoader

**类加载器作用是用来把类(class)装载进内存的。** JVM 规范定义了如下类型的类的加载器。  

![image-20211001220642000](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210816200741163-16291156628375.png)

```java
@Test
public void test() throws ClassNotFoundException {
    //1.获取一个系统类加载器
    ClassLoader classloader = ClassLoader.getSystemClassLoader();
    System.out.println(classloader);
    //2.获取系统类加载器的父类加载器，即扩展类加载器
    classloader = classloader.getParent();
    System.out.println(classloader);
    //3.获取扩展类加载器的父类加载器，即引导类加载器
    //无法获取引导类加载器，引导类加载器主要负责加载java的核心类库，且无法被获取；
    classloader = classloader.getParent();
    System.out.println(classloader);//null
    //4.测试当前类由哪个类加载器进行加载
    classloader = Class.forName("One.Person").getClassLoader();//One包名，Person类名
    System.out.println(classloader);
    //5.测试JDK提供的Object类由哪个类加载器加载
    classloader = Class.forName("java.lang.Object").getClassLoader();
    System.out.println(classloader);
    //*6.关于类加载器的一个主要方法： getResourceAsStream(String str):获取类路径下的指定文件的输入流
    InputStream in = null;
    in = this.getClass().getClassLoader().getResourceAsStream("exer2\\test.properties");
    System.out.println(in);
}
```



#### 四、创建运行时类的对象

------

- **创建类的对象： 调用Class对象的newInstance()方法**
	
	- 要求：
	
		- 类必须有一个无参数的构造器。
	
		- 类的构造器的访问权限需要足够。一般 public，缺省也可以
	
		- ```java
			Class<Person> clazz = Person.class;
			Person p = clazz.newInstance();//取到对象
			```
	
		```java
		@Test
		public void test() throws Exception{
		    for (int i = 0; i < 50; i++) {//加一个循环，体现每次随机数rand结果不一样，调用不一样的类
		        int rand = new Random().nextInt(3);
		        switch (rand){
		            case 0:
		                Object instance2 = getInstance("java.lang.Object");
		                System.out.println(instance2);
		                break;
		            case 1:
		                Object instance1 = getInstance("java.util.Date");
		                System.out.println(instance1);
		                break;
		            case 2:
		                Object instance = getInstance("One.Person");
		                System.out.println(instance);
		                break;
		        }
		    }
		}
		
		/**
		 * 创建一个指定类的对象
		 * @param classPath 指定类的全名
		 * @return 返回指定类的对象
		 * @throws Exception 找不到指定类
		 */
		public Object getInstance(String classPath) throws Exception {
		    Class<?> clazz = Class.forName(classPath);
		    return clazz.newInstance();
		}
		```

- 难道没有无参的构造器就不能创建对象了吗？
	- 不是！只要在操作的时候明确的调用类中的构造器， 并将参数传递进去之后，才可以实例化操作。
		**步骤如下：**
		- 通过Class类的getDeclaredConstructor(Class … parameterTypes)取得本类的指定形参类型的构造器
		- 向构造器的形参中传递一个对象数组进去，里面包含了构造器中所需的各个参数。
		- 通过Constructor实例化对象。

```java
//1.根据全类名获取对应的Class对象
String name = “atguigu.java.Person";
Class clazz = null;
clazz = Class.forName(name);

//2.调用指定参数结构的构造器，生成Constructor的实例
Constructor con = clazz.getConstructor(String.class,Integer.class);

//3.通过Constructor的实例创建对应类的对象，并初始化类属性
Person p2 = (Person) con.newInstance("Peter",20);
System.out.println(p2);
```



#### 五、获取运行时类的完整结构

------

**通过反射获取运行时类的完整结构：Field、 Method、 Constructor、 Superclass、 Interface、 Annotation**  



##### 1、实现的全部接口

```java
public Class<?>[] getInterfaces()
//确定此对象所表示的类或接口实现的接口。
```

> **代码演示：**
>
> ```java
> @Test
> public void test2(){
>     Class clazz = Person.class;
>     //获取运行时类的接口
>     Class[] interfaces = clazz.getInterfaces();
>     for (Class anInterface : interfaces) {
>         System.out.println(anInterface);
>         //interface Two.MyInterface
>         //interface java.lang.Comparable
>     }
> 
> 
>     //获取运行时类父类的接口
>     Class<?>[] superClassInterfaces = clazz.getSuperclass().getInterfaces();
>     for (Class<?> superClassInterface : superClassInterfaces) {
>         System.out.println(superClassInterface);//interface java.io.Serializable
>     }
> 
> }
> ```



##### 2、所继承的父类

```java
public Class<? Super T> getSuperclass()
//返回表示此 Class 所表示的实体（类、接口、基本类型）的父类的Class。
```

> **演示代码：**
>
> ```java
> @Test
> public void test1(){
>     Class clazz = Person.class;
> 
>     //1、获取运行时类的父类
>     Class superclass = clazz.getSuperclass();
>     System.out.println(superclass);//class Two.Creature
> 
>     //2、获取运行时类的带泛型的父类
>     Type genericSuperclass = clazz.getGenericSuperclass();
>     System.out.println(genericSuperclass);//Two.Creature<java.lang.String>
> 
>     //3、获取运行时类的带泛型的父类的泛型
>     Type genericSuper = clazz.getGenericSuperclass();
>     ParameterizedType paraType = (ParameterizedType) genericSuper;
>     Type[] actualTypeArguments = paraType.getActualTypeArguments();
>     for (Type ata : actualTypeArguments) {
>         System.out.println(ata.getTypeName());//java.lang.String
>     }
> 
> }
> ```



##### 3、全部的构造器

```java
public Constructor<T>[] getConstructors()
//返回此 Class 对象所表示的类的所有public构造方法。
public Constructor<T>[] getDeclaredConstructors()
//返回此 Class 对象表示的类声明的所有构造方法。
    
Constructor类中：
取得修饰符: public int getModifiers();
取得方法名称: public String getName();
取得参数的类型： public Class<?>[] getParameterTypes();
```

> **演示代码：**
>
> ```java
> @Test
> public void test(){
>     Class clazz = Person.class;
>     //getConstructors()：获取当前运行时类中声明为public的构造器【不要父类的，子类构造器默认继承父类，拿父类没意义】
>     Constructor[] constructors = clazz.getConstructors();
>     for (Constructor con : constructors) {
>         System.out.println(con);
>     }
> 
>     //getDeclaredConstructors()：获取当前运行时类中声明的所有的构造器
>     Constructor[] declaredConstructors = clazz.getDeclaredConstructors();
>     for (Constructor decCon : declaredConstructors) {
>         System.out.println(decCon);
>     }
> }
> ```



##### 4、全部的方法

```java
public Method[] getDeclaredMethods()
//返回此Class对象所表示的类或接口的全部方法
public Method[] getMethods()
//返回此Class对象所表示的类或接口的public的方法

Method类中：
取得全部的返回值: public Class<?> getReturnType()
取得全部的参数: public Class<?>[] getParameterTypes()
取得修饰符: public int getModifiers()
取得异常信息: public Class<?>[] getExceptionTypes()
```

> **演示代码：**
>
> <font color='blue'>**获取方法**</font>
>
> ```java
> @Test
> public void test(){
>     Class clazz = Person.class;
>     
>     //getMethods()：获取当前运行时类及其父类的所有声明为public权限的方法
>     Method[] methods = clazz.getMethods();
>     for (Method m : methods) {
>         System.out.println(m);
>     }
> 
>     //getDeclaredMethods()：获取当前运行时类中声明的所有方法，任何权限都获取。【但是不包含父类中的】
>     Method[] declaredMethods = clazz.getDeclaredMethods();
>     for (Method m : declaredMethods){
>         System.out.println(m);
>     }
> 
> }
> ```
>
>  * **<font color='blue'>获取方法的其他结构</font>**
>      * @Xxxx
>      * 权限修饰符    返回值类型   方法名(参数1类型 参数1，参数2类型 参数2...) throws 异常类型{}
>
> ```java
> /**
>  * 获取方法的其他结构
>  * @Xxxx
>  * 权限修饰符    返回值类型   方法名(参数1类型 参数1，参数2类型 参数2...) throws 异常类型{}
>  */
> @Test
> public void test1(){
>     Class clazz = Person.class;
> 
>     Method[] declaredMethods = clazz.getDeclaredMethods();
>     for (Method m : declaredMethods){
>         //1、获取方法声明的注解
>         Annotation[] annotations = m.getAnnotations();
>         for (Annotation a : annotations){
>             System.out.println(a);
>         }
> 
>         //2、获取方法的权限修饰符
>         int modifiers = m.getModifiers();
>         String str = Modifier.toString(modifiers);//代号转换
>         System.out.print(str + "\t");
> 
>         //3、获取方法的返回值类型
>         Class<?> returnType = m.getReturnType();
>         System.out.print(returnType.getName() + "\t");
> 
>         //4、获取方法的方法名
>         String name = m.getName();
>         System.out.print(name);
> 
>         //5、获取方法的参数类型及参数
>         System.out.print("(");
>         Class<?>[] parameterTypes = m.getParameterTypes();
>         for (int i = 0; i < parameterTypes.length; i++) {
>             if (i == parameterTypes.length-1){
>                 System.out.print(parameterTypes[i] + " args_" + i);
>                 break;
>             }
>             System.out.print(parameterTypes[i] + " args_" + i + ",");
>         }
>         System.out.print(")");
> 
>         //获取方法抛出的异常
>         Class<?>[] exceptionTypes = m.getExceptionTypes();
>         for (int i = 0; i < exceptionTypes.length; i++) {
>             System.out.print("throws ");
>             if (i == exceptionTypes.length-1){
>                 System.out.print(exceptionTypes[i].getName());
>                 break;
>             }
>             System.out.print(exceptionTypes[i].getName() + ",");
>         }
>         System.out.println();
>     }
> }
> ```





##### 5、全部的Field  

```java
public Field[] getFields()
//返回此Class对象所表示的类或接口的public的Field。
public Field[] getDeclaredFields()
//返回此Class对象所表示的类或接口的全部Field。

Field方法中：
以整数形式返回此Field的修饰符: public int getModifiers() 
得到Field的属性类型: public Class<?> getType() 
返回Field的名称: public String getName() 
```

**演示代码：**

> <font color='blue'>**获取属性结构**</font>

> ```java
> //获取属性结构
> @Test
> public void test(){
>     Class<Person> clazz = Person.class;
>  
>     //getFields()：获取当前运行时类及其父类中声明为public访问权限的所有属性
>     Field[] fields = clazz.getFields();
>     for (Field f : fields){
>         System.out.println(f);
>     }
>     ---------------------------------------------->>>
>     //public int Two.Person.id
>     //public double Two.Creature.weight
> 
>     //getDeclaredFields()：获取当前运行时类中声明的所有属性，任何权限都获取。【但是不包含父类中的】
>     Field[] declaredFields = clazz.getDeclaredFields();
>     for (Field f : declaredFields){
>         System.out.println(f);
>     }
>     ---------------------------------------------->>>
>     //private java.lang.String Two.Person.name
>     //int Two.Person.age
>     //public int Two.Person.id
> }
> ```
>
> <font color='blue'>**获取属性的具体信息：权限修饰符、数据类型、变量名**</font>
>
> ```java
> //获取属性的具体信息：权限修饰符、数据类型、变量名
> @Test
> public void Test1(){
>     Class<Person> clazz = Person.class;
>     
>     Field[] declaredFields = clazz.getDeclaredFields();
>     for (Field f : declaredFields){
>         //1、权限修饰符
>         int modifiers = f.getModifiers();//返回的是代号，0、1、2、等代表不同的权限修饰符
>         String str = Modifier.toString(modifiers);//通过他自己的toString()方法,转成权限修饰符
>         System.out.print(str + "\t");
>         //private【代号：2】
>         //       【代号：0】
>         //public 【代号：1】
> 
>         //2、数据类型
>         Class<?> type = f.getType();
>         System.out.print(type.getName() + "\t");
> 
>         //3、变量名
>         String name = f.getName();
>         System.out.println(name);
>        
>     }
> }        
> 		---------------------------------------------->>>
>         权限修饰符		数据类型		变量名
>         private	  java.lang.String	  name
> 	                   int	           age
> 		public		   int				id
> 
> ```





##### 6、Annotation相关  

```java
get Annotation(Class<T> annotationClass)
getDeclaredAnnotations()
```

> **代码演示：**
>
> ```java
> @Test
> public void test3(){
>     Class clazz = Person.class;
>     //获取运行时类的注解
>     Annotation[] annotations = clazz.getAnnotations();
>     for (Annotation annotation : annotations) {
>         System.out.println(annotation);//@Two.MyAnnotation(value=hi)
>     }
> 
> }
> ```



##### 7、泛型相关  

```java
获取父类泛型类型： Type getGenericSuperclass()
泛型类型： ParameterizedType
获取实际的泛型类型参数数组： getActualTypeArguments()
    代码见【五、2所继承的父类】
```



##### 8、类所在的包

```java
Package getPackage()  
```

> **代码演示：**
>
> ```java
> @Test
> public void test3(){
>     Class clazz = Person.class;
>     //获取运行时类所在的包
>     Package aPackage = clazz.getPackage();
>     System.out.println(aPackage);//package Two
> }
> ```





#### 六、调用运行时类的指定结构

------

##### 1、调用指定方法

通过反射，调用类中的方法，通过Method类完成。步骤：

- 通过Class类的getMethod(String name,Class…parameterTypes)方法取得一个Method对象，并设置此方法操作时所需要的参数类型。
- 之后使用Object invoke(Object obj, Object[] args)进行调用，并向方法中传递要设置的obj对象的参数信息。  

![image-20211002111616948](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211001220642000-16330972033809.png)

```java
@Test
public void test3() throws InstantiationException, IllegalAccessException, NoSuchFieldException, NoSuchMethodException, InvocationTargetException {
    Class<Person> clazz = Person.class;
    //1、创建运行时类的对象
    Person person = clazz.newInstance();
    //2、获取指定的方法:getDeclaredMethod(String fieldName)
    //参数1：指明方法的名称，参数2：指明获取方法的形参列表
    Method show = clazz.getDeclaredMethod("show", String.class);
    //3、保证当前方法是可访问的
    show.setAccessible(true);
    //4、调用方法的invoke()：参数1：方法的调用者，参数2：方法形参赋值
    Object China = show.invoke(person, "中国");//invoke()的返回值根据方法而定，不一定有返回值
    System.out.println(China);

---------------------------------如何调用静态方法-------------------------------------------
       
    Method showDest = clazz.getDeclaredMethod("showDest");
    showDest.setAccessible(true);
    
    //通过运行时对象调用
    showDest.invoke(person);
    //直接类.class也可以，因为是静态的
    showDest.invoke(Person.class);
    //【不知道类的话用getClass()】
    showDest.invoke(showDest.getClass());
  
    //直接写null，也行，因为是静态的， get、set方法时，对象位置同样可以写null
    showDest.invoke(null);
}
}
```

**<font color='red'>Object invoke(Object obj, Object … args) </font>**

**说明：**

- Object 对应原方法的返回值，若原方法无返回值，此时返回null
- 若原方法若为静态方法，此时形参Object obj可为null
- 若原方法形参列表为空，则Object[] args为null
- 若原方法声明为private,则需要在调用此invoke()方法前，显式调用方法对象的setAccessible(true)方法，将可访问private的方法。  



##### 2、调用指定属性

在反射机制中，可以直接通过Field类操作类中的属性，通过Field类提供的set()和get()方法就可以完成设置和取得属性内容的操作。  

> public Field getField(String name) 返回此Class对象表示的类或接口的指定的public的Field。【不常用】
>
> ```java
> @Test【因为只能获取public权限的属性，所以不常用】
> public void test() throws InstantiationException, IllegalAccessException, NoSuchFieldException {
>     Class<Person> clazz = Person.class;
>     //创建运行时类的对象
>     Person person = clazz.newInstance();
>     //获取指定的属性:getField()-----只能获取public权限的属性，，，所以开发中不常用
>     Field id = clazz.getField("id");
>     //设置当前属性的值
>     // set() 参数1：指明设置哪个对象的属性，参数2：设置属性的具体值
>     id.set(person,999);
>     //获取当前属性的值
>     //get() 参数1：获取那个对象的当前属性值
>     Object perID = id.get(person);
>     int perID1 = (int) perID;
>    
> ```

> **<font color='red'>public Field getDeclaredField(String name)	返回此Class对象表示的类或接口的指定的Field。</font>**
>
> ```java
> @Test【常用！！！！！！！！！！！！！！！！！！1！！】
> public void test2() throws InstantiationException, IllegalAccessException, NoSuchFieldException {
>     Class<Person> clazz = Person.class;
>     //1、创建运行时类的对象
>     Person person = clazz.newInstance();
>     //2、获取指定的属性:getDeclaredField(String fieldName)
>     //获取运行时类中指定变量名的属性
>     Field name = clazz.getDeclaredField("name");
>     //3、保证当前属性是可访问的
>     name.setAccessible(true);
>     //4、设置属性值
>     name.set(person,"张无忌");
>     //5、获取属性值
>     Object perName = name.get(person);
>     System.out.println(perName);
> }
> ```

- 在Field中：
	- public Object get(Object obj) 取得指定对象obj上此Field的属性内容
	- public void set(Object obj,Object value) 设置指定对象obj上此Field的属性内容  

##### 3、调用指定的构造器

```java
@Test
public void test4() throws Exception {
    Class<Person> clazz = Person.class;
    Person person = clazz.newInstance();//最最最常用的new对象的方法【调用空参构造器】

    //1、获取指定的构造器
    Constructor<Person> constructor = clazz.getDeclaredConstructor(String.class);
    //2、保证此构造器是可以访问的
    constructor.setAccessible(true);
    //3、调用此构造器创建运行时对象
    Person person1 = constructor.newInstance("张无忌");
    System.out.println(person1);
}
```



##### 4、关于setAccessible方法的使用

**Method和Field、 Constructor对象都有setAccessible()方法。**

- setAccessible启动和禁用访问安全检查的开关。
- 参数值为true则指示反射的对象在使用时应该取消Java语言访问检查。
- 提高反射的效率。 如果代码中必须用反射， 而该句代码需要频繁的被调用， 那么请设置为true。
- 使得原本无法访问的私有成员也可以访问
- 参数值为false则指示反射的对象应该实施Java语言访问检查。  







#### 七、反射的应用：动态代理

------

##### 1、动态代理

**代理设计模式的原理:**

> 使用一个代理将对象包装起来, 然后用该代理对象取代原始对象。任何对原始对象的调用都要通过代理。代理对象决定是否以及何时将方法调用转到原始对象上。

<font color="red">**静态代理**</font>的特征是代理类和目标对象的类都是在编译期间确定下来，不利于程序的扩展。同时，每一个代
理类只能为一个接口服务，这样一来程序开发中必然产生过多的代理。 最好可以通过一个代理类完成全部的代理功能。  

<font color="red">**动态代理**</font>是指客户通过代理类来调用其它对象的方法，并且是在程序运行时根据需要动态创建目标类的代理对象。

- 动态代理使用场合:
	- 调试
	- 远程方法调用
	- <font color="red">动态代理相比于静态代理的优点：</font>
		抽象角色中（接口）声明的所有方法都被转移到调用处理器一个集中的方法中处理，这样，我们可以更加灵活和统一的处理众多的方法。  

##### 2、Java动态代理相关API

<font color="red">**Proxy **</font>：专门完成代理的操作类，是所有动态代理类的父类。通过此类为一个或多个接口动态地生成实现类。

- 提供用于创建动态代理类和动态代理对象的静态方法

- ```java
	//创建一个动态代理类所对应的Class对象
	static Class<?> getProxyClass(ClassLoader loader, Class<?>... interfaces) 
	
	//直接创建一个动态代理对象
	static Object newProxyInstance(ClassLoader loader, Class<?>[] interfaces,InvocationHandler h) 
	    //三个参数
	    ClassLoader loader			类加载器
	    Class<?>[] interfaces		得到被代理类实现的全部接口
	    InvocationHandler h			得到InvocationHandler接口的实现类实例
	```



##### 3、动态代理步骤

###### **一、创建一个实现接口InvocationHandler的类，它必须实现invoke方法，以完成代理的具体操作。**  

```java
public Object invoke(Object theProxy, Method method, Object[] params)throws Throwable{
	try{
		Object retval = method.invoke(targetObj, params);
		// Print out the result
		System.out.println(retval);
		return retval;
	}catch (Exception exc){}
}

-----------------------------------------------------
    Object theProxy		代理类的对象
    Method method		要调用的方法
    Object[] params		方法调用时所需要的参数
```



###### 二、创建被代理的类以及接口  

![image-20211002180711385](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211002182811736-16331704932863.png)

###### 三、通过Proxy的静态方法

```java
Proxy.newProxyInstance(ClassLoader loader, Class[] interfaces, InvocationHandler h) 
//创建一个Subject接口代理
    
RealSubject target = new RealSubject();
// Create a proxy to wrap the original implementation
DebugProxy proxy = new DebugProxy(target);
// Get a reference to the proxy through the Subject interface
Subject sub = (Subject) Proxy.newProxyInstance(
Subject.class.getClassLoader(),new Class[] { Subject.class }, proxy);
```



###### 四、通过 Subject代理调用RealSubject实现类的方法

```java
String info = sub.say("Peter", 24);
System.out.println(info);
```



##### 4、一般静态代理结构【代码】

```java
//接口
interface ClothesFactory{
    void produceClothes();
}

//代理类
class ProxyFactory implements ClothesFactory{
    ClothesFactory clothesFactory = null;
    //构造器把被代理类Nike对象当做形参传进去
    public ProxyFactory(ClothesFactory clothesFactory){
        this.clothesFactory = clothesFactory;
    }
    @Override
    public void produceClothes() {
        System.out.println("工厂开始生产了");
        clothesFactory.produceClothes();//调用代理类的produceClothes方法【nike】
        System.out.println("工厂生产结束了");
    }
}

//被代理类
class NikeFactory implements ClothesFactory{
    @Override
    public void produceClothes() {
        System.out.println("我是Nike工厂");
    }
}

public class StaticProxyTest {
    public static void main(String[] args) {
        NikeFactory nikeFactory = new NikeFactory();//被代理对象
        ProxyFactory proxyFactory = new ProxyFactory(nikeFactory);//代理类对象
        proxyFactory.produceClothes();//通过代理类对象，调用被代理类方法
    }
}
```



##### 5、一般动态代理结构【代码】

```java
//接口
interface Human{
    String getbelief();
    void eat(String food);
}

//被代理类
class Superman implements Human{
    @Override
    public String getbelief() {
        return "我是超人，我会飞，~~~~~";
    }
    @Override
    public void eat(String food) {
        System.out.println("I like eat " + food);
    }
}

//创建动态代理类对象
class ProxyFactory{
    //该方法是静态的static，直接类.方法名----调用
    public static Object getProxyInstance(Object obj){//传入的obj是被代理的对象superman
        MyInvocation myInvocation = new MyInvocation(obj);//调用处理器对象
        return Proxy.newProxyInstance(obj.getClass().getClassLoader(), obj.getClass().getInterfaces(),myInvocation);
        //通过Reflection下的Proxy类的newProxyInstance()返回代理类对象，【三个参数，被代理类的类加载器、接口、调用处理器】
    }

}

class MyInvocation implements InvocationHandler{
    private Object obj;
	//构造器要传入，，，被代理的对象
    //getProxyIntance(Object obj)传入的也是被代理对象，在里面给new MyInvocation用
    public MyInvocation (Object obj){
        this.obj = obj;
    }
    //当我们通过代理类对象，调用方法A时，就会自动调用下列方法：invoke()
    //将代理类要执行的方法A的功能就声明在invoke()中
    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        //method:即为代理类对象调用的方法，此方法也就作为了被代理类对象要调用的方法
        //obj：被代理的对象
        return method.invoke(obj, args);
        //返回值就是当前类中的invoke()的返回值，java反射invoke()，方法有值就返回。
    }
}

public class ProxyTest {
    public static void main(String[] args) {
        Superman superman = new Superman();//被代理对象
        Object intance = ProxyFactory.getProxyIntance(superman);//创建代理类对象
        Human intance1 = (Human) intance;//类型转换

        intance1.eat("eggs");//通过代理类对象    调用被代理类方法
        String getbelief = intance1.getbelief();//接收返回值
        System.out.println(getbelief);
    }
}
```



##### 6、动态代理与AOP（Aspect Orient Programming)

![image-20211002182811736](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211002194622794-16331751993261.png)



动态代理改进后的说明：代码段1、代码段2、代码段3和深色代码段分离开了，但代码段1、 2、 3又和一个特定的方法A耦合了！最理想的效果是：代码块1、 2、 3既可以执行方法A，又无须在程序中以硬编码的方式直接调用深色代码的方法

- 使用Proxy生成一个动态代理时，往往并不会凭空产生一个动态代理，这样没有太大的意义。通常都是为指定的目标对象生成动态代理

- 这种动态代理在AOP中被称为AOP代理， AOP代理可代替目标对象， AOP代理包含了目标对象的全部方法。但AOP代理中的方法与目标对象的方法存在差异：<font color='red'>AOP代理里的方法可以在执行目标方法之前、之后插入一些通用处理。</font>

![image-20211002183054277](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211002194914189-16331753554733.png)

就是创建一个类，在原动态代理位置

```java
class HumanUtil{
    public void method1(){
        System.out.println("我是方法一")
    }
    public void method2(){
        System.out.println("我是方法二")
    }
}
class MyInvocation implements InvocationHandler{
    private Object obj;
    public MyInvocation (Object obj){
        this.obj = obj;
    }
    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        //在这里new一个通用方法对象
        HumanUtil ht = new HumanUtil();
        ht.method1();//调用通用方法一
        Object obj1 = method.invoke(obj, args);
        ht.method2();//调用通用方法2
        return obj1;
    }
}
//这种方式就会在，每次调用被代理方法的时候，
//1、先调用通用方法一
//2、再调用被代理方法
//3、再调用通用方法二
实现了包裹的效果，也可以移动通用方法的位置，根据需要

```



### 10、Java 8 其他新特性

**Java 8新特性简介**

Java 8 (又称为 jdk 1.8) 是 Java 语言开发的一个主要版本。
Java 8 是oracle公司于2014年3月发布，可以看成是自Java 5 以来最具革命性的版本。 Java 8为Java语言、编译器、类库、开发工具与JVM带来了大量新特性。  



![](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211002194901794-16331753429982.png)



并行流就是把一个内容分成多个数据块，并用不同的线程分别处理每个数据块的流。 相比较串行的流， **并行的流可以很大程度上提高程序的执行效率。**

Java 8 中将并行进行了优化，我们可以很容易的对数据进行并行操作。

Stream API 可以声明性地通过 parallel() 与 sequential() 在并行流与顺序流之间进行切换。  







#### 一、Lambda表达式

------

Lambda 是一个**匿名函数**，我们可以把 Lambda 表达式理解为是一段可以传递的代码（将代码像数据一样进行传递）。使用它可以写出更简洁、更灵活的代码。作为一种更紧凑的代码风格，使Java的语言表达能力得到了提升。  

![image-20211002194901794](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211002195333223-16331756159824.png)

![image-20211002194914189](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211002195354111-16331756351535.png)

##### 1、Lambda语法

Lambda 表达式： 在Java 8 语言中引入的一种新的语法元素和操作符。

这个操作符为 “**<font color='red'>-></font>**” ， 该操作符被称为 <font color='red'>Lambda 操作符或箭头操作符</font>。它将 Lambda 分为两个部分：

<font color='red'>左侧</font>： 指定了 Lambda 表达式需要的参数列表

<font color='red'>右侧</font>： 指定了 Lambda 体， 是抽象方法的实现逻辑，也即Lambda 表达式要执行的功能。  



- <font color='red'>语法格式一： 无参，无返回值</font>

![image-20211002195333223](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211002195445049-16331756861108.png)

```java
//语法格式一：无参数，无返回值
@Test
public void test(){
    //原
    Runnable r1 = new Runnable() {
        @Override
        public void run() {
            System.out.println("我是张无忌");
        }
    };
    r1.run();

    //Lambda
    Runnable r2 = () -> System.out.println("我是赵敏");
    r2.run();
}
```

- <font color='red'>语法格式二： Lambda 需要一个参数，但是没有返回值。</font>

![image-20211002195354111](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211002195459706-16331757007299.png)

```java
//语法格式二： Lambda 需要一个参数，但是没有返回值。
@Test
public void test1(){
    //原
    Consumer<String> c1 = new Consumer<String> () {
        @Override
        public void accept(String s) {
            System.out.println(s);

        }
    };
    c1.accept("谎言和誓言的区别是什么？");

    //Lambda
    Consumer<String> c2 = (String s) -> System.out.println(s);
    c2.accept("一个是听的人当真了，一个是说的人当真了");
}
```

- <font color='red'>语法格式三：</font><font color='blue'> 数据类型可以省略，</font><font color='red'>因为可由编译器推断得出，称为“类型推断”</font>

![image-20211002195412393](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211002195412393-16331756543856.png)

```java
//语法格式三：数据类型可以省略，因为可由编译器推断得出，称为“类型推断”
@Test
public void test2(){
    //原Lambda
    Consumer<String> c2 = (String s) -> System.out.println(s);
    c2.accept("一个是听的人当真了，一个是说的人当真了");

    //改进Lambda
    Consumer<String> c3 = (s) -> System.out.println(s);//省略括号中的String
    c3.accept("一个是听的人当真了，一个是说的人当真了");
}
```

- <font color='red'>语法格式四： Lambda 若只需要一个参数时， </font><font color='blue'>参数的小括号可以省略</font>

![image-20211002195430901](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211002195538142-163317573937110.png)

```java
//语法格式四： Lambda 若只需要一个参数时， 参数的小括号可以省略
@Test
public void test3(){
    //原Lambda
    Consumer<String> c2 = (String s) -> System.out.println(s);
    c2.accept("一个是听的人当真了，一个是说的人当真了");

    //改进Lambda
    Consumer<String> c3 = s -> System.out.println(s);//省略括号
    c3.accept("一个是听的人当真了，一个是说的人当真了");
}
```

- <font color='red'>语法格式五： Lambda 需要两个或以上的参数，多条执行语句，并且可以有返回值</font>

![image-20211002195445049](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210925100849337-16325357303693.png)

```java
//语法格式五： Lambda 需要两个或以上的参数，多条执行语句，并且可以有返回值
@Test
public void test4(){
    //原
    Comparator<Integer> cm1 = new Comparator<Integer>() {
        @Override
        public int compare(Integer o1, Integer o2) {
            System.out.println(o1);
            System.out.println(o2);
            return o1.compareTo(o2);
        }
    };
    System.out.println(cm1.compare(3, 7));

    //Lambda
    Comparator<Integer> cm2 = (o1,o2) ->{
        System.out.println(o1);
        System.out.println(o2);
        return o1.compareTo(o2);
    };
    System.out.println(cm2.compare(2, 6));
}
```

- <font color='red'>语法格式六： 当 Lambda 体只有</font><font color='blue'>一条</font><font color='red'>语句时，</font><font color='blue'> return 与大括号</font><font color='red'>若有，都可以省略</font>

![image-20211002195459706](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211002200815765-163317649688512.png)

```java
//语法格式六： 当 Lambda 体只有一条语句时， return 与大括号若有，都可以省略
@Test
public void test5(){
    //原Lambda
    Comparator<Integer> cm2 = (o1,o2) ->{
        return o1.compareTo(o2);
    };
    System.out.println(cm2.compare(2, 6));

    //改进后的Lambda
    Comparator<Integer> cm3 = (o1,o2) -> o1.compareTo(o2);
    System.out.println(cm3.compare(2, 6));
}
```



##### 2、类型推断  

上述 Lambda 表达式中的参数类型都是由编译器推断得出的。 Lambda表达式中无需指定类型，程序依然可以编译，这是因为 javac 根据程序的上下文，在后台推断出了参数的类型。 Lambda 表达式的类型依赖于上下文环境，是由编译器推断出来的。这就是所谓的“类型推断” 。  

![image-20211002195538142](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211002200746503-163317646828211.png)



##### 3、总结：

Lambda表达式的本质：作为函数式接口的实例

- <font color='red'>左侧</font>： 
	- Lambda 表达式的参数列表的参数类型可以省略（类型推断）
	- 如果Lambda形参列表只有一个参数，那么一对（）小括号也可以省略

- <font color='red'>右侧</font>： 
	- Lambda 体应该使用一对{}大括号包裹
	- 如果Lambda体只有一条执行语句（可能是return语句），省略这一对{}大括号和return关键字





#### 二、函数式(Functional)接口

------

##### 1、什么是函数式(Functional)接口

- **<font color='red'>只包含一个抽象方法的接口，称为函数式接口</font>。**
- 可以通过 Lambda 表达式来创建该接口的对象。（若 Lambda 表达式抛出一个受检异常(即：非运行时异常)，那么该异常需要在目标接口的抽象方法上进行声明）。
- 我们可以在一个接口上使用 <font color='red'>**@FunctionalInterface** </font>注解，这样做可以检查它是否是一个函数式接口。同时 javadoc 也会包含一条声明，说明这个接口是一个函数式接口。
- 在java.util.function包下定义了Java 8 的丰富的函数式接口  

##### 2、如何理解函数式接口

- Java从诞生日起就是一直倡导“一切皆对象”， 在Java里面面向对象(OOP)编程是一切。但是随着python、 scala等语言的兴起和新技术的挑战， Java不得不做出调整以便支持更加广泛的技术要求，也即**java不但可以支持OOP还可以支持OOF（面向函数编程）**
- 在函数式编程语言当中，函数被当做一等公民对待。在将函数作为一等公民的编程语言中， Lambda表达式的类型是函数。但是在Java8中，有所不同。在Java8中， Lambda表达式是对象，而不是函数，它们必须依附于一类特别的对象类型——**函数式接口**。
- 简单的说，在Java8中， **Lambda表达式就是一个函数式接口的实例**。 这就是Lambda表达式和函数式接口的关系。也就是说，只要一个对象是函数式接口的实例，那么该对象就可以用Lambda表达式来表示。
- **所以以前用匿名实现类表示的现在都可以用Lambda表达式来写。**  



##### 3、函数式接口举例

![image-20211002200746503](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211002200836641-163317651816813.png)



**自定义函数式接口 ：**

![image-20211002200815765](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211002200916927-163317655824614.png)

**函数式接口中使用泛型：**  

![image-20211002200836641](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211002201003862-163317660511515.png)

**作为参数传递 Lambda 表达式：**

![image-20211002200916927](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211003140943175-16332413845892.png)

##### 4、Java 内置四大核心函数式接口  

![image-20211002201003862](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211003140925947-16332413673271.png)

**Consumer<T>**

> ```java
> @Test
> public void test6(){
>     //老办法调用方法
>     happyTime(500, new Consumer<Double>() {
>         @Override
>         public void accept(Double aDouble) {
>             System.out.println("买了个奥特曼，花了我" + aDouble + "元");
>         }
>     });
> 
>     //Lambda表达式
>     happyTime(900,money -> System.out.println("买了个小怪兽，花了我" + money + "元"));
> }
> //定义了一个方法，形参包含Consumer类型
> public void happyTime(double money,Consumer<Double> consumer){
>     consumer.accept(money);
> }
> ```

**Predicate<T>**

> ```java
> @Test
> public void test7(){
>     List<String> list = Arrays.asList("南京","北京","天津","上海","东京");
>     //原方法
>     List<String> filterStrs = filterString(list, new Predicate<String>() {
>         @Override
>         public boolean test(String s) {
>             return s.contains("京");
>         }
>     });
>     System.out.println(filterStrs);
> 
>     //Lambda表达式
>     List<String> filterStrs2 = filterString(list,s -> s.contains("京"));
>     System.out.println(filterStrs2);
> }
> 
> //实现字符串过滤，，具体怎么过滤，根据重写的test方法确定
> public List<String> filterString(List<String> list, Predicate<String> predicate){
>     ArrayList<String> strs = new ArrayList<>();
>     for (String s : list){
>         if (predicate.test(s)){
>             strs.add(s);
>         }
>     }
>     return strs;//返回的是list结构
> }
> ```



##### 5、其他接口

![image-20211002201024879](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211003141151100-16332415127113.png)







#### 三、方法引用与构造器引用

------

##### 1、方法引用(Method References)

- 当要传递给Lambda体的操作，已经有实现的方法了，可以使用方法引用！
- 方法引用可以看做是Lambda表达式深层次的表达。换句话说，方法引用就是Lambda表达式，也就是函数式接口的一个实例，通过方法的名字来指向一个方法，可以认为是Lambda表达式的一个语法糖。
- 要求： 实现接口的抽象方法的参数列表和返回值类型，必须与方法引用的方法的参数列表和返回值类型保持一致！
- 格式： 使用操作符 “::” 将类(或对象) 与 方法名分隔开来。
- 如下三种主要使用情况：
	- <font color='red'>**对象::实例方法名**</font>
	- **<font color='red'>类::静态方法名</font>**
	- **<font color='red'>类::实例方法名  </font>**

![image-20211003140925947](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211003141255006-16332415760544.png)

![image-20211003140943175](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211003181945139-16332563863995.png)

**<font color='red'>注意： 当函数式接口方法的第一个参数是需要引用方法的调用者，并且第二个参数是需要引用方法的参数(或无参数)时： ClassName::methodName</font>**

##### 2、构造器引用

**<font color='red'>格式： ClassName::new</font>**
与函数式接口相结合，自动与函数式接口中方法兼容。

可以把构造器引用赋值给定义的方法，要求构造器参数列表要与接口中抽象方法的参数列表一致！且方法的返回值即为构造器对应类的对象。  

![image-20211003141151100](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211002201024879-163317662721716.png)

##### 3、数组引用

**<font color='red'>格式： type[] :: new  </font>**

![image-20211003141255006](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211003192019762-16332600223738.png)





#### 四、强大的Stream API

------

##### 1、Stream API说明

- Java8中有两大最为重要的改变。第一个是 **Lambda 表达式**；另外一个则是 **Stream API**。
- Stream API ( java.util.stream) 把真正的函数式编程风格引入到Java中。这是目前为止对Java类库最好的补充，因为Stream API可以极大提供Java程序员的生产力，让程序员写出高效率、干净、简洁的代码。
- Stream 是 Java8 中处理集合的关键抽象概念，它可以指定你希望对集合进行的操作，可以执行非常复杂的查找、过滤和映射数据等操作。<font color='red'> 使用Stream API 对集合数据进行操作，就类似于使用 SQL 执行的数据库查询。</font>也可以使用 Stream API 来并行执行操作。简言之， Stream API 提供了一种高效且易于使用的处理数据的方式。  

##### 2、为什么要使用Stream API

- 实际开发中，项目中多数数据源都来自于Mysql， Oracle等。但现在数据源可以更多了，有MongDB， Radis等，而这些NoSQL的数据就需要Java层面去处理。
- Stream 和 Collection 集合的区别： <font color='red'>Collection 是一种静态的内存数据结构，而 Stream 是有关计算的</font>。 前者是主要面向内存，存储在内存中，后者主要是面向 CPU，通过 CPU 实现计算。  

##### 3、什么是 Stream

- Stream到底是什么呢？

	- 是数据渠道，用于操作数据源（集合、数组等）所生成的元素序列。
	- <font color='blue'>“集合讲的是数据， Stream讲的是计算！</font>

	

- <font color='red'>**注意：**</font>

	- ①Stream 自己不会存储元素。
	- ②Stream 不会改变源对象。相反，他们会返回一个持有结果的新Stream。
	- ③Stream 操作是延迟执行的。这意味着他们会等到需要结果的时候才执行。  

##### 4、Stream 的操作三个步骤

1. <font color='red'>创建 Stream</font>
	一个数据源（如：集合、数组），获取一个流
2. <font color='red'>中间操作</font>
	一个中间操作链，对数据源的数据进行处理
3. <font color='red'>终止操作(终端操作)</font>
	一旦执行终止操作， 就执行中间操作链，并产生结果。之后，不会再被使用  



![image-20211003181945139](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211003201646325-16332634076129.png)

##### 5、Stream的创建操作

###### 一、创建 Stream方式一：通过集合

Java8 中的 Collection 接口被扩展，提供了两个获取流的方法：

- default Stream<E> stream() : 返回一个顺序流
- default Stream<E> parallelStream() : 返回一个并行流  

```java
//创建方式一：通过集合
@Test
public void test(){
    List<Employee> employees = EmployeeData.getEmployees();//自定义类的静态方法，返回一个list

    //default Stream<E> stream() : 返回一个顺序流
    Stream<Employee> stream = employees.stream();

    //default Stream<E> parallelStream() : 返回一个并行流
    Stream<Employee> parallelStream = employees.parallelStream();

}
```



###### 二、创建 Stream方式二：通过数组

Java8 中的 Arrays 的静态方法 stream() 可以获取数组流：

- <font color='red'>static <T> Stream<T> stream(T[] array): 返回一个流</font>
- 重载形式，能够处理对应基本类型的数组：
	- public static IntStream stream(int[] array)
	- public static LongStream stream(long[] array)
	- public static DoubleStream stream(double[] array)  

```java
//创建方式二：通过数组
@Test
public void test1(){
    int[] arr = new int[]{1,2,3,4,5};
    //调用Arrays类的static <T> Stream<T> stream(T[] array): 返回一个流
    IntStream stream = Arrays.stream(arr);//根据输入的数组类型，返回IntStream

    //自定义数组
    Employee e1 = new Employee(1001, "张无忌");
    Employee e2 = new Employee(1002, "赵敏");
    Employee[] employees = {e1, e2};
    Stream<Employee> stream1 = Arrays.stream(employees);

}
```

###### 三、创建 Stream方式三：通过Stream的of()

可以调用Stream类静态方法 of(), 通过显示值创建一个流。它可以接收任意数量的参数。

- <font color='red'>public static<T> Stream<T> of(T... values) : 返回一个流  </font>

```java
//创建方式三：通过Stream的of()
@Test
public void test2(){
    Stream<Integer> integerStream = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9);
}
```

###### 四、创建 Stream方式四：创建无限流

可以使用静态方法 Stream.iterate() 和 Stream.generate(),创建无限流。

- <font color='red'>迭代</font>
	<font color='blue'>public static<T> Stream<T> iterate(final T seed, final UnaryOperator<T> f)</font>
- <font color='red'>生成</font>
	<font color='blue'>public static<T> Stream<T> generate(Supplier<T> s)  </font>

```java
//创建方式四：创建无限流
@Test
public void test3(){
    //迭代
    //public static<T> Stream<T> iterate(final T seed, final UnaryOperator<T> f)
    //遍历前十个偶数
    Stream.iterate(0,t -> t+2).limit(10).forEach(System.out::println);
    //生成
    //public static<T> Stream<T> generate(Supplier<T> s)
    //输出十个随机数
    Stream.generate(Math::random).limit(10).forEach(System.out::println);
}
```



##### 9、Stream 的中间操作

<font color='red'>多个中间操作可以连接起来形成一个流水线，除非流水线上触发终止操作，否则中间操作不会执行任何的处理！而在终止操作时一次性全部处理，称为“惰性求值” 。  </font>

###### 一、筛选与切片  

![image-20211003191943628](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211002195430901-16331756721467.png)

- filter(Predicate p)-------接收 Lambda ， 从流中排除某些元素

	- ```java
		List<Employee> employees = EmployeeData.getEmployees();
		
		//filter(Predicate p) 接收 Lambda ， 从流中排除某些元素
		Stream<Employee> stream = employees.stream();
		//保留工资大于7000的员工
		stream.filter(e -> e.getSalary() > 7000).forEach(System.out :: println);
		```

- distinct()-------筛选，通过流所生成元素的 hashCode() 和 equals() 去除重复元素

	- ```java
		List<Employee> employees = EmployeeData.getEmployees();
		
		//distinct() 筛选，通过流所生成元素的 hashCode() 和 equals() 去除重复元素
		employees.add(new Employee(1009,"刘强东",45,8000));
		employees.add(new Employee(1009,"刘强东",45,8000));//添加重复元素
		employees.add(new Employee(1009,"刘强东",45,8000));
		employees.add(new Employee(1009,"刘强东",45,8000));
		employees.forEach(System.out :: println);//输出现在所有对象
		
		employees.stream().distinct().forEach(System.out :: println);//输出筛选后的
		```



- limit(long maxSize)-------截断流，使其元素不超过给定数量

	- ```java
		List<Employee> employees = EmployeeData.getEmployees();
		
		
		//limit(long maxSize) 截断流，使其元素不超过给定数量
		employees.stream().limit(3).forEach(System.out :: println);//仅输出前3个
		```

- skip(long n)-------跳过元素，返回一个扔掉了前n个空流。与 limit(n) 互补 n 个元素的流。若流中元素不足 n 个，则返回一个空流。与 limit(n) 互补

	- ```java
		List<Employee> employees = EmployeeData.getEmployees();
		
		//skip(long n) 跳过元素，返回一个扔掉了前n个空流。与 limit(n) 互补 n 个元素的流。若流中元素不足 n 个，则返回一个空流。与 limit(n) 互补
		employees.stream().skip(3).forEach(System.out :: println);//跳过前三条数据
		```

###### 二、映 射

![image-20211003191927553](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210928105205761-16327975269502.png)

- map(Function f)------接收一个函数作为参数，该函数会被应用到每个元 素上，并将其映射成一个新的元素。

	- ```java
		@Test
		public void test1(){
		    //map(Function f)
		    List<String> list = Arrays.asList("aa", "bb", "cc");
		    list.stream().map(str -> str.toUpperCase()).forEach(System.out::println);//将每个元素转大写，并输出
		
		    //练习1：获取员工名字长度大于3个字的员工
		    List<Employee> employees = EmployeeData.getEmployees();
		    Stream<String> namesStream = employees.stream().map(Employee::getName);
		    namesStream.filter(name -> name.length() > 3).forEach(System.out::println);
		}
		```

- mapToDouble(ToDoubleFunction f)--------接收一个函数作为参数，该函数会被应用到每个元 素上，产生一个新的 DoubleStream。

	- 

- mapToInt(ToIntFunction f)------接收一个函数作为参数，该函数会被应用到每个元 素上，产生一个新的IntStream。

	- 

- mapToLong(ToLongFunction f)----接收一个函数作为参数，该函数会被应用到每个元 素上，产生一个新的 LongStream。

	- 

- flatMap(Function f)-------接收一个函数作为参数，将流中的每个值都换成另一个流，然后把所有流连接成一个流

	- ```java
		@Test
		public void test1(){
		    //map(Function f)
		    List<String> list = Arrays.asList("aa", "bb", "cc");
		
		    //练习2：用map实现flatMap功能
		    Stream<Stream<Character>> streamStream = list.stream().map(StreamAPITest1::fromStringToStream);
		    streamStream.forEach(s -> {s.forEach(System.out::println);});//相当于嵌套循环
		
		    //flatMap(Function f)
		    Stream<Character> characterStream = list.stream().flatMap(StreamAPITest1::fromStringToStream);
		    characterStream.forEach(System.out::println);
		
		}
		
		//将字符串中的多个字符构成的集合转换为对应的Stream的实例
		public static Stream<Character> fromStringToStream(String str){
		    ArrayList<Character> list = new ArrayList<>();
		    for (Character c : str.toCharArray()){//取出字符串每一个元素
		        list.add(c);//添加到列表
		    }
		    return list.stream();//转成Stream实例
		}
		```

**map和flatMap：**

map相当于list的add（）-------flatmap相当于list的addAll（）

```java
//举例
list1 = {1,2,3}
list2 = {4,5,6}

list1.add(list2)---------此时list1 = {1,2,3，[4,5,6]}
list1.addAll(list2)------此时list1 = {1,2,3,4,5,6}//将list2打开后添加

flatmap也是同样的道理，将stream打开整体后添加，形成一个流
```



###### 三、排序  

![image-20211003192019762](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211003191927553-16332599686466.png)



- sorted()------产生一个新流，其中按自然顺序排序

	- ```java
		@Test
		public void test2(){
		    //sorted()------产生一个新流，其中按自然顺序排序
		    List<Integer> list = Arrays.asList(23, 54, 33, 76, 12, 8);
		    list.stream().sorted().forEach(System.out::println);
		}
		```

- sorted(Comparator com) -------产生一个新流，其中按比较器顺序排序

	- ```java
		@Test
		public void test2(){
		    //sorted(Comparator com) -------产生一个新流，其中按比较器顺序排序
		    List<Employee> employees = EmployeeData.getEmployees();
		    //仅按照年龄排序
		    employees.stream().sorted((e1,e2) -> Integer.compare(e1.getAge(),e2.getAge())).forEach(System.out::println);
		    System.out.println();
		    
		    //先按照年龄排序，年龄相同的按照id排序
		    employees.stream().sorted((e1,e2) -> {
		        int compare = Integer.compare(e1.getAge(), e2.getAge());
		        if (compare != 0){
		            return compare;
		        }else{
		            return Integer.compare(e1.getId(), e2.getId());
		        }
		    }).forEach(System.out::println);
		}
		```



##### 10、Stream 的终止操作

- 终端操作会从流的流水线生成结果。其结果可以是任何不是流的值，
	- 例如： List、 Integer，甚至是 void 。
- 流进行了终止操作后，不能再次使用。  

###### 一、匹配与查找

![image-20211003201646325](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211003220835267-163327011670911.png)

![image-20211003201658429](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211003201658429-163326341960910.png)

- allMatch(Predicate p)---检查是否匹配所有元素

	- ```java
		   @Test
		   public void test(){
		      List<Employee> employees = EmployeeData.getEmployees();
		      //检查是否所有员工年龄都大于18岁
		      boolean allMatch = employees.stream().allMatch(e -> e.getAge() > 18);
		      System.out.println(allMatch);//false
		   }
		```

- anyMatch(Predicate p)-----检查是否至少匹配一个元素

	- ```java
		   @Test
		   public void test(){
		      List<Employee> employees = EmployeeData.getEmployees();
		      //是否存在员工的工资大于10000元
		      boolean anyMatch = employees.stream().anyMatch(e -> e.getSalary() > 10000);
		      System.out.println(anyMatch);//false
		   }
		```

- noneMatch(Predicate p)------检查是否没有匹配所有元素

	- ```java
		   @Test
		   public void test(){
		      List<Employee> employees = EmployeeData.getEmployees();
		      //是否存在姓“雷”的员工
		      boolean noneMatch = employees.stream().noneMatch(e -> e.getName().startsWith("雷"));
		      System.out.println(noneMatch);//false【没有---返回true，有---返回false】
		   }
		```

		

- findFirst()------返回第一个元素

	- ```java
		   @Test
		   public void test(){
		      List<Employee> employees = EmployeeData.getEmployees();
		//    findFirst()------返回第一个元素
		      Optional<Employee> first = employees.stream().findFirst();
		      System.out.println(first);
		   }
		```

- findAny()-------返回当前流中的任意元素

	- ```java
		@Test
		   public void test(){
		      List<Employee> employees = EmployeeData.getEmployees();
		
		//    findAny()-------返回当前流中的任意元素
		      Optional<Employee> any = employees.stream().findAny();
		      System.out.println(any);
		   }
		```

- count()-------返回流中元素总数

	- ```java
		@Test
		   public void test(){
		      List<Employee> employees = EmployeeData.getEmployees();
		
		//    count()-------返回流中元素总数
		      long count = employees.stream().count();
		      System.out.println(count);//8个
		      //可以中间加操作，比如返回当前流中工资大于5000的人数
		      long count1 = employees.stream().filter(e -> e.getSalary() > 5000).count();
		      System.out.println(count1);//5个
		   }
		```

- max(Comparator c)-------返回流中最大值

	- ```java
		@Test
		   public void test(){
		      List<Employee> employees = EmployeeData.getEmployees();
		//max(Comparator c)-------返回流中最大值
		      //返回员工的最高工资
		      Optional<Double> max = employees.stream().map(e -> e.getSalary()).max(Double::compareTo);
		      System.out.println(max);
		      //Optional[9876.12]
		   }
		```

- min(Comparator c)-------返回流中最小值

	- ```java
		@Test
		   public void test(){
		      List<Employee> employees = EmployeeData.getEmployees();
		
		//min(Comparator c)-------返回流中最小值
		      //返回最低工资的员工
		      Optional<Employee> min = employees.stream().min((e1, e2) -> Double.compare(e1.getSalary(), e2.getSalary()));
		      System.out.println(min);
		       //Optional[Employee{id=1008, name='扎克伯格', age=35, salary=2500.32}]
		   }
		```

- forEach(Consumer c)-------内部迭代(使用 Collection 接口需要用户去做迭代， 称为外部迭代。相反，Stream API 使用内部迭 代——它帮你把迭代做了)

	- ```java
		@Test
		   public void test(){
		      List<Employee> employees = EmployeeData.getEmployees();
		//forEach(Consumer c)-------内部迭代(使用 Collection 接口需要用户去做迭代， 称为外部迭代。相反，Stream API 使用内部迭 代——它帮你把迭代做了)
		      employees.stream().forEach(System.out::println);
		   }
		```

###### 二、归约

![image-20211003220835267](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211003191943628-16332599847187.png)

**备注： map 和 reduce 的连接通常称为 map-reduce 模式，因 Google用它来进行网络搜索而出名。**  

- reduce(T iden, BinaryOperator b)-------可以将流中元素反复结合起来，得到一 个值。返回 T

	- ```java
		public class StreamAPITest3 {
		    @Test
		    public void test(){
		        //计算1-10的自然数的和
		        List<Integer> list = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
		        Integer sum = list.stream().reduce(0, Integer::sum);
		        //0是初始值，相当于额外加一个数
		        System.out.println(sum);//55
		
		    }
		}
		```

- reduce(BinaryOperator b)--------可以将流中元素反复结合起来，得到一 个值。返回 Optional<T>

	- ```java
		public class StreamAPITest3 {
		    @Test
		    public void test(){
		        //计算公司所有员工每月工资的总和
		        List<Employee> employees = EmployeeData.getEmployees();
		        Stream<Double> salaryStream = employees.stream().map(Employee::getSalary);
				//方法引用
		        Optional<Double> sumMoney = salaryStream.reduce(Double::sum);
		        //自己写
		        Optional<Double> sumMoney2 = salaryStream.reduce((d1,d2)->(d1 + d2));
		        System.out.println(sumMoney);//Optional[48424.08]
		        //Optional类的get()方法，直接取到值，但是前提是保证值存在
		        System.out.println(sumMoney.get());//48424.08
		        System.out.println(sumMoney2);//Optional[48424.08]
		    }
		}
		```







###### 三、收集

![image-20211003220925478](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211004165527660-16333377289352.png)

Collector 接口中方法的实现决定了如何对流执行收集的操作(如收集到 List、 Set、Map)。
另外， Collectors 实用类提供了很多静态方法，可以方便地创建常见收集器实例，

- collect（Collector c）------将流转换为其他形式。接收一个 Collector 接口的实现，用于给Stream中元素做汇总的方法。

	- ```java
		@Test
		public void test1(){
		    //查找工资大于6000的员工
		    List<Employee> employees = EmployeeData.getEmployees();
		    //返回list
		    List<Employee> list = employees.stream().filter(e -> e.getSalary() > 6000).collect(Collectors.toList());
		    list.forEach(System.out::println);
		    System.out.println();
		    //返回set
		    Set<Employee> set = employees.stream().filter(e -> e.getSalary() > 6000).collect(Collectors.toSet());
		    set.forEach(System.out::println);
		}
		```

具体方法与实例如下表：  

![image-20211003221008988](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211003221008988-163327021041413.png)

![image-20211003221040442](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211004165458352-16333377004001.png)



#### 五、Optional类

------

- Optional<T> 类(java.util.Optional) 是一个容器类， 它可以保存类型T的值， 代表这个值存在。或者仅仅保存null，表示这个值不存在。原来用 null 表示一个值不存在，现在 Optional 可以更好的表达这个概念。并且可以避免空指针异常。  
- Optional类的Javadoc描述如下：这是一个可以为null的容器对象。如果值存在则isPresent()方法会返回true，调用get()方法会返回该对象。  
- <font color='blue'>Optional提供很多有用的方法，这样我们就不用显式进行空值检测。  </font>

##### 1、创建Optional类对象的方法：

- Optional.of(T t) : 创建一个 Optional 实例， t必须非空；
- Optional.empty() : 创建一个空的 Optional 实例
- Optional.ofNullable(T t)： t可以为null  

```java
//Optional.of(T t)  保证t是非空的
@Test
public void test(){
    Girl girl = new Girl();
//        girl = null;//NullPointerException空指针异常
    Optional<Girl> girl1 = Optional.of(girl);
}

//ofNullable(T t)   t可以为null
@Test
public void test1(){
    Girl girl = new Girl();
    girl = null;
    Optional<Girl> girl1 = Optional.ofNullable(girl);
    System.out.println(girl1);//Optional.empty
}
```

##### 2、判断Optional容器中是否包含对象：

- boolean isPresent() : 判断是否包含对象
- void ifPresent(Consumer<? super T> consumer) ： 如果有值，就执行Consumer接口的实现代码，并且该值会作为参数传给它。  

##### 3、获取Optional容器的对象：

- T get(): 如果调用对象包含值，返回该值，否则抛异常【和of(T t)搭配使用，因为都不能为空】
- T orElse(T other) ： 如果有值则将其返回，否则返回指定的other对象。【和ofNullable(T t)搭配使用，因为可以为空】
- T orElseGet(Supplier<? extends T> other) ： 如果有值则将其返回，否则返回由Supplier接口实现提供的对象。
- T orElseThrow(Supplier<? extends X> exceptionSupplier) ： 如果有值则将其返回，否则抛出由Supplier接口实现提供的异常。  

```java
类结构：Boy中定义了Girl属性，其中Girl也是自定义类
    通过Boy调用Girl再调用Girl属性
//方式一：可能报空指针异常
    //传进去的boy为空，直接调用方法，空指针。
    //传进去的boy不空，boy中的Girl空，直接调用getName，空指针。
public String getGirlName(Boy boy){//获取女孩的名字
    return boy.getGirl().getName();
}
//方式二：可以用if嵌套语句，判断对象不空时再调用方法，空返回null
public String getGirlName11(Boy boy){//获取女孩的名字
    if (boy != null){
        if (boy.getGirl() != null){
            return boy.getGirl().getName();
        }
    }   
    return null;
}
//方式三：使用Optional提供的T orElse(T other) 方法，如果有值则将其返回，否则返回指定的other对象。
public String getGirlName111(Boy boy){//获取女孩的名字
    //主旨：使用Optional提供的T orElse(T other) 方法： 如果有值则将其返回，否则返回指定的other对象。
    //不空，你返回自己值，空了，我设定一个默认值让你返回。
    
    Optional<Boy> optionalBoy = Optional.ofNullable(boy);//把传进来的boy封起来
    //如果boy空了，那就new一个，里面属性为new Girl 名字为贾静雯，boy=null，返回贾静雯
    Boy boy1 = optionalBoy.orElse(new Boy(new Girl("贾静雯")));

    //boy不空时，内部Girl属性再判断是不是空，同理
    Girl girl = boy1.getGirl();
    Optional<Girl> optionalGirl = Optional.ofNullable(girl);
    Girl girl1 = optionalGirl.orElse(new Girl("高圆圆"));
    return girl1.getName();//此时返回getName必定不空，因为可能出现空的情况，前边已经放了替补
}

@Test
public void test5(){
    Boy boy = new Boy();//里面的Girl空------返回  高圆圆
    boy = null;//Boy直接空-----返回  贾静雯
    boy = new Boy(new Girl("毛晓彤"));//都不空------正常执行  返回  毛晓彤
    String girlName = getGirlName111(boy);
    System.out.println(girlName);
}

```





### 11、Java9&Java10&Java11新特性

#### 一、Java 9 的新特性

------

- 模块化系统
- jShell命令
- 多版本兼容jar包
- 接口的私有方法
- 钻石操作符的使用升级
- 语法改进： try语句
- String存储结构变更
- 便利的集合特性： of()
- 增强的Stream API
- 全新的HTTP客户端API
- Deprecated的相关API
- javadoc的HTML 5支持
- Javascript引擎升级： Nashorn
- java的动态编译器  

##### 1、目录结构改变

![image-20211004165458352](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211003221040442-163327024178314.png)



![image-20211004165527660](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211004170645023-16333384070164.png)



##### 2、模块化系统 Jigsaw-->Modularity  

谈到 Java 9 大家往往第一个想到的就是 Jigsaw 项目。 众所周知， Java 已经发展超过 20 年（95 年最初发布）， Java 和相关生态在不断丰富的同时也越来越暴露出一些问题：

- Java 运行环境的膨胀和臃肿。 每次JVM启动的时候，至少会有30～60MB的内存加载，主要原因是JVM需要加载rt.jar，不管其中的类是否被classloader加载，第一步整个jar都会被JVM加载到内存当中去（而模块化可以根据模块的需要加载程序运行需要的class）
- 当代码库越来越大，创建复杂，盘根错节的“意大利面条式代码”的几率呈指数级的增长。 不同版本的类库交叉依赖导致让人头疼的问题，这些都阻碍了 Java 开发和运行效率的提升。
- 很难真正地对代码进行封装, 而系统并没有对不同部分（也就是 JAR 文件）之间的依赖关系有个明确的概念。 每一个公共类都可以被类路径之下任何其它的公共类所访问到，这样就会导致无意中使用了并不想被公开访问的 API。  
- <font color='blue'>**本质上讲也就是说， 用模块来管理各个package，通过声明某个package暴露，模块(module)的概念，其实就是package外再裹一层， 不声明默认就是隐藏。因此，模块化使得代码组织上更安全，因为它可以指定哪些部分可以暴露，哪些部分隐藏。**</font>
- 实现目标
	- 模块化的主要目的在于减少内存的开销
	- 只须必要模块，而非全部jdk模块，可简化各种类库和大型应用的开发和维护
	- 改进 Java SE 平台，使其可以适应不同大小的计算设备
	- 改进其安全性，可维护性，提高性能  
- **模块将由通常的类和新的模块声明文件（module-info.java） 组成。 该文件是位于java代码结构的顶层， 该模块描述符明确地定义了我们的模块需要什么依赖关系，以及哪些模块被外部使用。 在exports子句中未提及的所有包默认情况下将封装在模块中， 不能在外部使用。**  

![image-20211004165923461](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211004165923461-16333379646573.png)

<font color='red'>**要想在java9demo模块中调用java9test模块下包中的结构， 需要在java9test的module-info.java中声明：**  </font>

```java
module java9test {
	//package we export
	exports com.atguigui.bean;
}
//exports：控制着哪些包可以被其它模块访问到。 所有不被导出的包默认都被封装在模块里面。
```

<font color='red'>**对应在java 9demo 模块的src 下创建module-info.java文件：  **  </font>

```java
module java9demo {
	requires java9test;
}
//requires：指明对其它模块的依赖。
```



##### 3、Java的REPL工具： jShell命令

【就是通过jShell可以直接在控制台写代码了，不用先编译、再执行，类似Python】

- <font color='red'>**Java 9 中终于拥有了 REPL工具： jShell。 让Java可以像脚本语言一样运行，从控制台启动jShell， 利用jShell在没有创建类的情况下直接声明变量，计算表达式，执行语句。**</font>即开发时可以在命令行里直接运行Java的代码，而无需创建Java文件，无需跟人解释” public static void main(String[] args)”这句废话。
- jShell也可以从文件中加载语句或者将语句保存到文件中。
- jShell也可以是tab键进行自动补全和自动添加分号。  



![image-20211004170645023](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211004170715745-16333384378556.png)

![image-20211004170659841](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211004170659841-16333384213655.png)



![image-20211004170715745](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211004170752157-16333384737038.png)

![image-20211004170734020](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211004170734020-16333384552467.png)



![image-20211004170752157](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211004172317242-16333393996589.png)



##### 4、语法改进：接口的私有方法  

- Java 8中规定接口中的方法除了抽象方法之外， 还可以定义静态方法和默认的方法。 一定程度上， 扩展了接口的功能， 此时的接口更像是一个抽象类。
- 在Java 9中， **接口更加的灵活和强大， 连方法的访问权限修饰符都可以声明为private的了**， 此时方法将不会成为你对外暴露的API的一部分。  

```java
interface MyInterface {
	void normalInterfaceMethod();
	default void methodDefault1() {//默认方法1
		init();
	}
	public default void methodDefault2() {//默认方法2
		init();
	}
	// This method is not part of the public API exposed by MyInterface
	private void init() {//私有方法、只能内部调用
		System.out.println("默认方法中的通用操作");
	}
}
```

```java
class MyInterfaceImpl implements MyInterface {
	@Override
	public void normalInterfaceMethod() {
		System.out.println("实现接口的方法");
	}
}
public class MyInterfaceTest {
	public static void main(String[] args) {
		MyInterfaceImpl impl = new MyInterfaceImpl();
		impl.methodDefault1();
		// impl.init();//私有方法不能外部调用
	}
}
```



##### 5、语法改进:钻石操作符使用升级

我们将能够与**匿名实现类共同使用钻石操作符**（diamond operator） 

在Java 8中如下的操作是会报错的：  【java 9 可以如下编译】

> ```java
> //JDK 8会报错-----编译报错信息： Cannot use “<>” with anonymous inner classes
> Comparator<Object> com = new Comparator<>(){
> 	@Override
> 	public int compare(Object o1, Object o2) {
> 		return 0;
> 	}
> };
> 
> ```
>
> 

##### 6、语法改进： try语句

Java 8 中， 可以实现资源的自动关闭， 但是要求执行后必须关闭的所有资源必须在try子句中初始化， 否则编译不通过。 如下例所示：  

> ```java
> //必须关闭的流之类的，必须声明在try()的小括号内，不需要在finally中再关闭操作
> try(InputStreamReader reader = new InputStreamReader(System.in)){
> 	//读取数据细节省略
> }catch (IOException e){
> 	e.printStackTrace();
> }
> ```
>
> 

Java 9 中， 用资源语句编写try将更容易， 我们可以在try子句中使用已经初始化过的资源， 此时的资源是final的：  

> ```java
> //在外边声明，把变量名放到try()的小括号中即可，他会自己执行关闭操作
> InputStreamReader reader = new InputStreamReader(System.in);
> OutputStreamWriter writer = new OutputStreamWriter(System.out);
> try (reader, writer) {
> 	//reader是final的，不可再被赋值
> 	//reader = null;
> 	//具体读写操作省略
> } catch (IOException e) {
> 	e.printStackTrace();
> }
> ```
>
> 

##### 7、String存储结构变更

![image-20211004172317242](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211004172901986-163333974327010.png)

##### 8、集合工厂方法：快速创建只读集合

要创建一个只读、 不可改变的集合， 必须构造和分配它， 然后添加元素， 最后包装成一个不可修改的集合。  

```java
List<String> namesList = new ArrayList <>();
namesList.add("Joe");
namesList.add("Bob");
namesList.add("Bill");
//静态方法unmodifiableList()使集合变成只读
//原集合若是只读-----unmodifiableList()返回的新集合与原集合地址相同；
//原集合非只读----unmodifiableList()返回一个新集合；
namesList = Collections.unmodifiableList(namesList);
System.out.println(namesList);
```

缺点：我们一下写了五行。 即：它不能表达为单个表达式。  

```java
//方式一：只读集合
//Arrays.aslist()创建的集合就是只读的
List<String> list = Collections.unmodifiableList(Arrays.asList("a", "b", "c"));
Set<String> set = Collections.unmodifiableSet(new HashSet<>(Arrays.asList("a",
"b", "c")));
// 如下操作不适用于jdk 8 及之前版本,适用于jdk 9
Map<String, Integer> map = Collections.unmodifiableMap(new HashMap<>() {
{
	put("a", 1);
	put("b", 2);
	put("c", 3);
}
});
map.forEach((k, v) -> System.out.println(k + ":" + v));
```



Java 9因此引入了方便的方法， 这使得类似的事情更容易表达。  

![image-20211004172901986](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211004220552999-163335635433414.png)

**List firsnamesList = List.of(“Joe”,”Bob”,”Bill”);**
调用集合中<font color='red'>**静态方法of()**</font>， 可以将不同数量的参数传输到此工厂方法中。 此功能可用于Set和List， 也可用于Map的类似形式。 此时得到的集合， 是不可变的：在创建后， 继续添加元素到这些集合会导致 “UnsupportedOperationException” 。

由于Java 8中接口方法的实现， 可以直接在List， Set和Map的接口内定义这些方法，便于调用。  

```java
List<String> list = List.of("a", "b", "c");
Set<String> set = Set.of("a", "b", "c");

Map<String, Integer> map1 = Map.of("Tom", 12, "Jerry", 21, "Lilei", 33,
"HanMeimei", 18);

Map<String, Integer> map2 = Map.ofEntries(Map.entry("Tom", 89),
Map.entry("Jim", 78), Map.entry("Tim", 98));
```

##### 9、InputStream 加强

InputStream 终于有了一个非常有用的方法： <font color='red'>**transferTo**</font>，可以用来将数据直接传输到 OutputStream，这是在处理原始数据流时非常常见的一种用法，如下示例。  

```java
ClassLoader cl = this.getClass().getClassLoader();
try (InputStream is = cl.getResourceAsStream("hello.txt");
	OutputStream os = new FileOutputStream("src\\hello1.txt")) {
	is.transferTo(os); // 把输入流中的所有数据直接自动地复制到输出流中
} catch (IOException e) {
	e.printStackTrace();
}
```

##### 10、增强的 Stream API

- Java 的 Steam API 是java标准库最好的改进之一， 让开发者能够快速运算，从而能够有效的利用数据并行计算。 Java 8 提供的 Steam 能够利用多核架构实现声明式的数据处理。
- 在 Java 9 中， Stream API 变得更好， Stream 接口中添加了<font color='red'>**4 个新的方法：takeWhile, dropWhile, ofNullable，还有个 iterate 方法的新重载方法**</font>，可以让你提供一个 Predicate (判断条件)来指定什么时候结束迭代。
- 除了对 Stream 本身的扩展， Optional 和 Stream 之间的结合也得到了改进。<font color='red'>现在可以通过 Optional 的新方法 stream() 将一个 Optional 对象转换为一个(可能是空的) Stream 对象。  </font>

###### 一、takeWhile()的使用

用于从 Stream 中获取一部分数据， 接收一个 Predicate 来进行选择。 在有序的Stream 中， takeWhile 返回从开头开始的尽量多的元素。  <font color='red'>**【从头输出，发现不符合条件的停止，跳出】**</font>

```java
List<Integer> list = Arrays.asList(45, 43, 76, 87, 42, 77, 90, 73, 67, 88);

list.stream().takeWhile(x -> x < 50).forEach(System.out::println);
//45  43 
System.out.println();

list = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8);

list.stream().takeWhile(x -> x < 5).forEach(System.out::println);
// 1 2 3 4 
```

###### 二、dropWhile()的使用

dropWhile 的行为与 takeWhile 相反， 返回剩余的元素。   <font color='red'>**【发现不符合条件的开始输出，到结尾为止】**</font>

```java
List<Integer> list = Arrays.asList(45, 43, 76, 87, 42, 77, 90, 73, 67, 88);
list.stream().dropWhile(x -> x < 50).forEach(System.out::print);
//76 87 42 77 90 73 67 88
System.out.println();
list = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8);
list.stream().dropWhile(x -> x < 5).forEach(System.out::print);
//5 6 7 8
```

###### 三、ofNullable()的使用

Java 8 中 Stream 不能完全为null， 否则会报空指针异常。 而 Java 9 中的 ofNullable 方法允许我们创建一个单元素 Stream， 可以包含一个非空元素， 也可以创建一个空Stream。  

  <font color='red'>**【jdk 8 中Stream.of("AA", "BB", null);不能仅仅有一个null元素，你可以有多个元素包含null，甚至甚至你可以有两个null元素---Stream.of(null, null);-------jdk 9中可以了，Stream.ofNullable(null);只有一个null元素】**</font>

```java
// 报NullPointerException
// Stream<Object> stream1 = Stream.of(null);
// System.out.println(stream1.count());
// 不报异常，允许通过
Stream<String> stringStream = Stream.of("AA", "BB", null);
System.out.println(stringStream.count());// 3
// 不报异常，允许通过
List<String> list = new ArrayList<>();
list.add("AA");
list.add(null);
System.out.println(list.stream().count());// 2
// ofNullable()：允许值为null
Stream<Object> stream1 = Stream.ofNullable(null);
System.out.println(stream1.count());// 0
Stream<String> stream = Stream.ofNullable("hello world");
System.out.println(stream.count());// 1
```

###### 四、iterate()重载的使用

这个 iterate 方法的新重载方法， 可以让你提供一个 Predicate (判断条件)来指定什么时候结束迭代。  

```java
// 原来的控制终止方式：
Stream.iterate(1, i -> i + 1).limit(10).forEach(System.out::println);//需要终止限制
// 现在的终止方式：
Stream.iterate(1, i -> i < 100, i -> i + 1).forEach(System.out::println);
//简单说就是融入了for循环，中间是判断语句，不满足就跳出
```





##### 11、Optional获取Stream的方法

Optional类中stream()的使用

```java
List<String> list = new ArrayList<>();
list.add("Tom");
list.add("Jerry");
list.add("Tim");
Optional<List<String>> optional = Optional.ofNullable(list);

Stream<List<String>> stream = optional.stream();
stream.flatMap(x -> x.stream()).forEach(System.out::println);
```



#### 二、Java 10 的新特性

------

##### 1、 局部变量类型推断

- 产生背景

	- 开发者经常抱怨Java中引用代码的程度。 局部变量的显示类型声明，常常被认为是不必须的，给一个好听的名字经常可以很清楚的表达出下面应该怎样继续。

- 好处：

	- 减少了啰嗦和形式的代码，避免了信息冗余，而且对齐了变量名，更容易阅读！

- 举例如下：

	- 场景一： 类实例化时

		> 作为 Java开发者， 在声明一个变量时， 我们总是习惯了敲打两次变量类型， 第一次用于声明变量类型， 第二次用于构造器。  
		>
		> ```java
		> LinkedHashSet<Integer> set = new LinkedHashSet<>();
		> ```

	- 场景二： 返回值类型含复杂泛型结构

		> 变量的声明类型书写复杂且较长，尤其是加上泛型的使用
		>
		> ```java
		> Iterator<Map.Entry<Integer, Student>> iterator = set.iterator();
		> ```

	- 场景三：我们也经常声明一种变量， 它只会被使用一次， 而且是用在下一行代码中，比如：  

		> ```java
		> URL url = new URL("http://www.atguigu.com");
		> URLConnection connection = url.openConnection();
		> Reader reader = new BufferedReader(new
		> InputStreamReader(connection.getInputStream()));
		> ```

	尽管 IDE可以帮我们自动完成这些代码，但当变量总是跳来跳去的时候，可读性还是会受到影响，因为变量类型的名称由各种不同长度的字符组成。而且，有时候开发人员会尽力避免声明中间变量，因为太多的类型声明只会分散注意力，不会带来额外的好处。  

<font color='red'>**适用于以下情况：**</font>

```java
//1.局部变量的初始化
var list = new ArrayList<>();
//2.增强for循环中的索引
for(var v : list) {
	System.out.println(v);
}
//3.传统for循环中
for(var i = 0;i < 100;i++) {
	System.out.println(i);
}
```

<font color='blue'>**在局部变量中使用时，如下情况不适用：**</font>

![image-20211004214952645](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211003220925478-163327016684312.png)

<font color='blue'>**不适用以下的结构中：**</font>

- 情况1： 没有初始化的局部变量声明
- 情况2： 方法的返回类型
- 情况3： 方法的参数类型
- 情况4： 构造器的参数类型
- 情况5： 属性
- 情况6： catch块  



**工作原理:**

在处理 var时， 编译器先是查看表达式右边部分， 并根据右边变量值的类型进行推断， 作为左边变量的类型， 然后将该类型写入字节码当中。  

**注 意:**

- **<font color='red'>var不是一个关键字</font>**
	你不需要担心变量名或方法名会与 var发生冲突， 因为 var实际上并不是一个关键字，而是一个类型名， 只有在编译器需要知道类型的地方才需要用到它。 除此之外， 它就是一个普通合法的标识符。 也就是说， 除了不能用它作为类名， 其他的都可以，但极少人会用它作为类名。

- <font color='red'>**这不是JavaScript**</font>
	首先我要说明的是， var并不会改变Java是一门静态类型语言的事实。 编译器负责推断出类型， 并把结果写入字节码文件， 就好像是开发人员自己敲入类型一样。

- 下面是使用 IntelliJ（实际上是 Fernflower的反编译器）反编译器反编译出的代码： 

	> ```java
	> //编译器使用局部变量类型推断后
	> var url = new URL("http://www.atguigu.com");
	> var connection = url.openConnection();
	> var reader = new BufferedReader(
	> new InputStreamReader(connection.getInputStream()));
	> ```

	> ```java
	> //编译好的文件如下：【反编译代码如下】
	> //还是给写出来的，只不过在编译阶段看到的是用了var
	> URL url = new URL("http://www.atguigu.com");
	> URLConnection connection = url.openConnection();
	> BufferedReader reader = new BufferedReader(
	> new InputStreamReader(connection.getInputStream()));
	> ```

从代码来看，就好像之前已经声明了这些类型一样。事实上，这一特性只发生在编译阶段，与运行时无关，所以对运行时的性能不会产生任何影响。所以请放心，这不是 JavaScript。  



##### 2、集合新增创建不可变集合的方法

自 Java 9 开始， Jdk 里面为集合（List / Set / Map） 都添加了 of (jdk9新增)和copyOf (jdk10新增)方法， 它们两个都用来创建不可变的集合， 来看下它们的使用和区别。  

```java
//示例1：
var list1 = List.of("Java", "Python", "C");
var copy1 = List.copyOf(list1);
System.out.println(list1 == copy1); // true
//示例2：
var list2 = new ArrayList<String>();
var copy2 = List.copyOf(list2);
System.out.println(list2 == copy2); // false
//示例1和2代码基本一致， 为什么一个为true,一个为false?
```

从 源 码 分 析 ， 可 以 看 出 copyOf 方 法 会 先 判 断 来 源 集 合 是 不 是AbstractImmutableList 类型的， 如果是， 就直接返回， 如果不是， 则调用 of 创建一个新的集合。

示例2因为用的 new 创建的集合， 不属于不可变 AbstractImmutableList 类的子类，所以 copyOf 方法又创建了一个新的实例， 所以为false。

**注意：**使用of和copyOf创建的集合为不可变集合， 不能进行添加、 删除、 替换、排序等操作， 不然会报 java.lang.UnsupportedOperationException 异常。

上面演示了 List 的 of 和 copyOf 方法， Set 和 Map 接口都有。  



#### 三、Java 11 的新特性  

------

JDK 11 是一个长期支持版本（LTS, Long-Term-Support）

- 对于企业来说， 选择 11 将意味着长期的、 可靠的、 可预测的技术路线图。
- 其中免费的OpenJDK11 确定将得到 OpenJDK 社区的长期支持， LTS 版本将是可以放心选择的版本。
- 从 JVM GC 的角度， JDK11 引入了两种新的 GC， 其中包括也许是划时代意义的 ZGC， 虽然其目前还是实验特性， 但是从能力上来看， 这是 JDK 的一个巨大突破， 为特定生产环境的苛刻需求提供了一个可能的选择。 例如， 对部分企业核心存储等产品， 如果能够保证不超过 10ms 的 GC 暂停， 可靠性会上一个大的台阶， 这是过去我们进行 GC 调优几乎做不到的， 是能与不能的问题。  

新的<font color='red'>**长期支持版本每三年**</font>发布一次，根据后续的发布计划，下一个长期支持版 Java 17 将于2021年发布

##### 1、新增了一系列字符串处理方法

![image-20211004220250508](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211004214952645-163335539399911.png)

##### 2、Optional 加强

Optional 也增加了几个非常酷的方法， 现在可以很方便的将一个 Optional 转成一个 Stream, 或者当一个空 Optional 时给它一个替代的。  

![image-20211004220324640](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211004220324640-163335620737813.png)



##### 3、局部变量类型推断升级

**<font color ='red'>在var上添加注解的语法格式</font>**，在jdk10中是不能实现的。在JDK11中加入了这样的语法。  

```java
//错误的形式: 必须要有类型, 可以加上var
//Consumer<String> con1 = (@Deprecated t) ->
System.out.println(t.toUpperCase());
//正确的形式:
//使用var的好处是在使用lambda表达式时给参数加上注解。
Consumer<String> con2 = (@Deprecated var t) ->
System.out.println(t.toUpperCase());
```



##### 4、全新的HTTP 客户端API

- HTTP，用于传输网页的协议，早在1997年就被采用在目前的1.1版本中。直到2015年， HTTP2才成为标准。
- ![image-20211004220552999](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20210918225600492-16319769623091.png)  

- HTTP/1.1和HTTP/2的主要区别是如何在客户端和服务器之间构建和传输数据。
	HTTP/1.1依赖于请求/响应周期。 HTTP/2允许服务器“push”数据：它可以发送比客户端请求更多的数据。 这使得它可以优先处理并发送对于首先加载网页至关重要的数据。
- 这是 Java 9 开始引入的一个处理 HTTP 请求的的 HTTP Client API， 该API 支持同步和异步， 而在 Java 11 中已经为正式可用状态， 你可以在java.net 包中找到这个 API。
- 它 将 替 代 仅 适 用 于 blocking 模 式 的 HttpURLConnection（ HttpURLConnection是在HTTP 1.0的时代创建的， 并使用了协议无关的方法） ， 并提供对WebSocket 和 HTTP/2的支持。  

```java
HttpClient client = HttpClient.newHttpClient();
HttpRequest request =
HttpRequest.newBuilder(URI.create("http://127.0.0.1:8080/test/")).build();
BodyHandler<String> responseBodyHandler = BodyHandlers.ofString();
HttpResponse<String> response = client.send(request, responseBodyHandler);
String body = response.body();
System.out.println(body);
```

```java
HttpClient client = HttpClient.newHttpClient();
HttpRequest request =
HttpRequest.newBuilder(URI.create("http://127.0.0.1:8080/test/")).build();
BodyHandler<String> responseBodyHandler = BodyHandlers.ofString();
CompletableFuture<HttpResponse<String>> sendAsync =
client.sendAsync(request, responseBodyHandler);
sendAsync.thenApply(t -> t.body()).thenAccept(System.out::println);
//HttpResponse<String> response = sendAsync.get();
//String body = response.body();
//System.out.println(body);
```

##### 5、更简化的编译运行程序

看下面的代码。

```java
// 编译
javac Javastack.java
// 运行
java Javastack
```


在我们的认知里面， 要运行一个 Java 源代码必须先编译， 再运行， 两步执行动作。

而在未来的 Java 11 版本中， 通过一个 java 命令就直接搞定了， 如以下所示：

**<font color ='red'>java Javastack.java</font>**

**一个命令编译运行源代码的注意点：**

- 执行源文件中的第一个类, 第一个类必须包含主方法。
- 并且不可以使用其它源文件中的自定义类, 本文件中的自定义类是可以使用的。  

##### 6、废弃Nashorn引擎

废除Nashorn javascript引擎， 在后续版本准备移除掉， 有需要的可以考虑使用GraalVM。  

##### 7、ZGC

- <font color ='red'>GC是java主要优势之一</font>。 然而, 当GC停顿太长, 就会开始影响应用的响应时间。 消除或者减少GC停顿时长, java将对更广泛的应用场景是一个更有吸引力的平台。 此外, 现代系统中可用内存不断增长,用户和程序员希望JVM能够以高效的方式充分利用这些内存, 并且无需长时间的GC暂停时间。
- <font color ='red'>ZGC, A Scalable Low-Latency Garbage Collector(Experimental) ZGC, 这应该是JDK11最为瞩目的特性, 没有之一</font>。 但是后面带了Experimental,说明这还不建议用到生产环境。
- ZGC是一个并发, 基于region, 压缩型的垃圾收集器, 只有root扫描阶段会STW(stop the world), 因此GC停顿时间不会随着堆的增长和存活对象的增长而变长。  

- 优势：
	- GC暂停时间不会超过10ms
	- 既能处理几百兆的小堆, 也能处理几个T的大堆(OMG)
	- 和G1相比, 应用吞吐能力不会下降超过15%
	- 为未来的GC功能和利用colord指针以及Load barriers优化奠定基础
	- 初始只支持64位系统
- ZGC的设计目标是：支持TB级内存容量， 暂停时间低（<10ms） ， 对整个程序吞吐量的影响小于15%。 将来还可以扩展实现机制， 以支持不少令人兴奋的功能， 例如多层堆（即热对象置于DRAM和冷对象置于NVMe闪存），或压缩堆。  

##### 8、其它新特性

- Unicode 10
- Deprecate the Pack200 Tools and API
- 新的Epsilon垃圾收集器
- 完全支持Linux容器（包括Docker）
- 支持G1上的并行完全垃圾收集
- 最新的HTTPS安全协议TLS 1.3S
- Java Flight Recorder  



------------------------------------

## 九、面试题

#### 1、== 操作符和 equals（）的区别

​		**==：是一个运算符**

​				1、可以使用在基本数据类型变量和引用数据类型变量中

​				2、如果比较的是基本数据类型变量，比较两个变量保存的数据，是否相等，（不一定类型相同）

​				3、如果比较的是引用数据类型变量，比较两个对象的地址值，是否相等。



​		**equals（）：是一个方法**

​				1、A.equals（B）,返回true或者false

​				2、只能够适用于引用数据类型

​				3、Object类中equals（）方法的定义：

```java
public boolean equals(Object obj) {
    return (this == obj);
}
//此时表明：在Object类中定义的equals()方法和“==”运算符的作用是相同的；
```

​				4、像String、Data、File、包装类等，都重写了Object类中的equals（）方法。重写以后，比较的不是两个引用的地址是否相同，而是比较两个对象的 ”实体内容“ 是否相同。

​				5、通常情况下，我们自定义的类如果使用equals（）的话，也通常是比较两个对象的 “实体内容”，是否相同，那么我们就需要重写Object类中的equals（）方法。



#### 2、包装类

​		①下面两段代码输出的结果是否相同，若不同则分别说出输出什么内容

​		**主要考察：**Object o1 = true ? new Integer(1) : new Double(2.0);编译时会进行自动类型提升Integer--->Double

```java
import org.junit.Test;
//第一段代码
public class InterviewTest {
    @Test
    public void test1(){
        Object o1 = true ? new Integer(1) : new Double(2.0);
        System.out.println(o1);//1.0
        //因为编译阶段Integer类型被自动类型提升为Double类型
    }

//第二段代码
    @Test
    public void test2(){
        Object o2;
        if(true)
            o2 = new Integer(1);
        else
            o2 = new Double(2.0);
        System.out.println(o2);//1
        //正常执行
    }
}
```

​		

​		②请说出下面三段代码的输出内容

​		**主要考察：**Integer内部定义了IntegerCache结构,IntegerCache中定义了Integer[]类型的名为cache[]的数组， 数组中存储了-128~127范围的整数，因为使用频繁，相当于提前缓存（cache），提高效率，当给Integer赋值的范围在-128~127范围内时，可以直接使用数组中元素，不用再去new了，所以返回地址值相同。

```java
import org.junit.Test;

public class InterviewTest {
    @Test
    public void test3(){
        Integer i = new Integer(1);
        Integer j = new Integer(1);
        System.out.println(i == j);//false
        //因为操作符==比较两个对象的地址值，必然不同，返回false

        Integer m = 1;
        Integer n = 1;
        System.out.println(m == n);//true
        //此时采用自动装箱
        //Integer内部定义了IntegerCache()结构,IntegerCache中定义了Integer[]类型的名为cache[]的数组，
        // 数组中存储了-128~127范围的整数，因为使用频繁，相当于提前缓存（cache），提高效率
        // 给Integer赋值的范围在-128~127范围内时，可以直接使用数组中元素，不用再去new了，
        //此时m和n定义为1，地址值均为cache[]数组中1的地址值，所以返回true

        Integer x = 128;
        Integer y = 128;
        System.out.println(x == y);
        //因为128不在cache[]数组范围之内，所以每次new了一个新的对象，故地址不同，返回false
    }
}
```



#### 3、单例模式（Singleton）

​		**设计模式：**是在大量的实践中总结和理论化之后优选的代码结构、编程风格、以及解决问题的思考方式。设计模式就像经典的棋谱，不同的棋局我们用不同的棋谱，免得我们自己再去思考和摸索。

​		**单利设计模式：**就是采取一定的方法保证在整个的软件系统中，**对某个类只能存在一个对象实例**，并且该类只提供一个取得对象实例的方法。如果我们要让类在虚拟机中只能产生一个对象，我们首先必须将类的构造器的访问权限设置为private，这样，就不能用new操作符在类的外部产生类的对象了，但在类的内部仍可以产生该类的对象，只能调用该类的某个静态方法以返回类内部创建的对象，静态方法只能访问类中的静态成员变量，所以，指向类内部产生的该类的对象的变量也必须定义成静态的。

​		**单例模式的优点：**由于单例模式只生成一个实例，减少了系统性能的开销，当一个对象的产生需要比较多的资源时，如读取配置、产生其他依赖对象时、则可以通过在应用启动时直接产生一个单例对象，然后永久驻留内存的方式来解决。

​		**单例设计模式： **    **饿汉式** VS **懒汉式**

​				饿汉式：直接创建对象，使用时调用；

​								坏处：对象加载时间过长。

​								好处：饿汉式是线程安全的。

​				懒汉式：暂不创建，使用时创建；

​								好处：延迟对象的创建。

​								坏处：需要考虑线程不安全问题，多线程时同时满足instance == null，同时进入if语句，创建多个对象。

```java
//饿汉式

//测试
public class Singleton_hungry {
    public static void main(String[] args){
        Singleton s1 = Singleton.getInstance();
        Singleton s2 = Singleton.getInstance();
    }
}

class Singleton{
    private Singleton(){

    }
    private static Singleton instance = new Singleton();

    public static Singleton getInstance(){
        return instance;
    }
   
}
```



```java
//懒汉式
//测试
public class Singleton_lazy {
    public static void main(String[] args){
        Singleton_2 s1 = Singleton_2.getInstance();
        Singleton_2 s2 = Singleton_2.getInstance();
        if(s1 == s2)
            System.out.println(true);
    }
}
//直接锁方法----和-----同步代码块把方法内部全包起来一样。
//效率不高，并发性低，除了第一个new对象时，需要线程锁【单线程】之外
//已经new了对象之后，剩余的进来取对象，谁来谁取，根本不用等，而这种写法是任何时候到要等。
class Singleton_2{
    private Singleton_2(){}
    private static Singleton_2 instance = null;

    public static synchronized Singleton_2 getInstance() {
        if(instance == null){
        	instance = new Singleton_2();   
        }
        return instance;
    }
}


//双重检查锁
//这种方法在第一个new对象之后，剩余的取对象线程在第一个if语句！=null时，直接return取走对象，根本不涉及线程锁，只有第一个会判断两遍，然后进锁，new对象
class Singleton_2{
    private Singleton_2(){}
    private static Singleton_2 instance = null;

    public static Singleton_2 getInstance() {
        if(instance == null){
            synchronized(Singleton_2.class){ 
                if(instance == null){//这个if是为了第一次new对象时，第一个if满足条件进来多个线程，等拿到锁的线程new完后，将其他已经来的线程筛选出去，不满足第二个if
                    instance = new Singleton_2();
                }
            }
        }
        return instance;
    }
}
```

####      4、排错题

##### 1、调用方法输出X值时，不能区分是哪个X，因为接口和类是平级的。

```java
interface A {
    int x = 0;
}

class B{
    int x = 1;
}

class C extends B implements A {
    public void pX(){
        //编译不通过，X值不明确
        System.out.println(x);
        
//        System.out.println(super.x);  //调用父类x值，若多层父类，默认就近原则
//        System.out.println(A.x);  //调用接口中的x值，因为接口中的常量为全局常量，直接调用即可
    }

    public static void main(String[] args){
        new C().pX();
    }
}
```

##### 2、接口中定义类型：

​						>全局常量：public static final 的，（但是书写时，可以不写，直接写 int、double等）

​						>抽象方法：public abstract 的                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             

```java
public class Ball implements Rollable{
    private String name;

    public String getName(){
        return name;
    }

    public Ball(String name){
        this.name = name;
    }

    public void play(){//因为接口Playable、Bounceable中的play()方法重名，此处重写一个play()也可以

        //ball虽然在Rollable中定义了类型，但是接口中变量隐藏了public static final，
        //方法隐藏了public abstract。
        //因为有final 所以此处的ball不允许再赋值或赋对象
        ball = new Ball("Football");//错！！！！！！！！！！！！！
        System.out.println(ball.getName());
    }
}

interface Playable{
    void play();
}
interface Bounceable{
    void play();
}
interface Rollable extends Playable,Bounceable{
    Ball ball = new Ball("PingPang");
//    public static final Ball ball = new Ball("PingPang");
}
```



#### 5、常见的异常有哪些？请举例说明：

> 运行时异常
>
> ```java
> //NullPointerException空指针异常
> 
> public void test1(){
>     //举例一
>     int[] arr = null;
>     System.out.println(arr[1]);
> 
>     //举例二
>     String str = null;
>     System.out.println(str.charAt(0));
> }
> ```

```java
//IndexOutOfBoundsException角标越界

public void test2(){
    //举例一:ArrayIndexOutOfBoundsException数组角标越界
    int[] arr = new int[3];
    System.out.println(arr[99]);

    //举例二:StringIndexOutOfBoundsException字符串角标越界
    String str = "abcd";
    System.out.println(str.charAt(99));
}
```

```java
//ClassCastException类型转换异常

public void test3(){
    Object obj = new Date();
    String str = (String)obj;
}
```

```java
//NumberFormatException数字格式异常

public void test4(){
    String str = "12345";//正常
    str = "abc";
    int num = Integer.parseInt(str);
}
```

```java
//InputMismatchException输入不匹配异常

public void test5(){
    Scanner scan = new Scanner(System.in);
    //若输入数据不是int类型，则报出异常
    int score = scan.nextInt();
    System.out.println(score);
}
```

```java
//ArithmeticException算数异常

public void test6(){
    int a = 10;
    int b = 0;
    System.out.println(a / b);
}
```

#### 6、throw和throws

throws属于异常处理的一种方式，声明在方法体外。

​				放在A方法后边，声明A方法可能要抛出的异常类，将异常向上汇报，反馈至调用者。

throw表示抛出一个异常类的对象，是生成异常对象的过程。声明在方法体内。

```java
public static double ecm(int a, int b) throws EcDef {		//throws
    if (a < 0 || b < 0) {
        throw new EcDef("请勿输入负数！");						//throw
    }
    return a / b;
}
//EcDef是自定义的异常类型
```



#### 7、synchronized 与 lock的异同？？？

> 答：1、Lock是显式锁（手动开启和关闭锁，别忘记关闭锁），synchronized是隐式锁，出了作用域自动释放
>
> ​		2、Lock只有代码块锁，synchronized有代码块锁和方法锁
>
> ​		3、使用Lock锁，JVM将花费较少的时间来调度线程，性能更好。并且具有更好的扩展性（提供了更多的子类）
>
> ​		相同：二者都可以解决线程安全问题
>
> ​		不同：synchronized 机制在执行完相应的同步代码以后，自动释放同步监视器（锁）
>
> ​					lock需要手动的启动同步（lock（）方法），同时结束同步也需要手动实现（unlock（）方法）。
>
> 优先使用顺序：Lock------->同步代码块（已经进入了方法体，分配了相应的资源）------->同步方法（在方法体之外）

#### 8、如何解决线程安全问题？有几种方式？

```java
方式一：同步代码块
synchronized(同步监视器){
    //需要被同步的代码(别包多了代码，成单线程了)
}

方式二：同步方法
synchronized 方法名(){//默认同步监视器就是this

}

方式三：Lock锁----JDK5.0新增
import java.util.concurrent.locks.ReentrantLock;//导包
private ReentrantLock lock = new ReentrantLock();//在run方法上边创建对象
        try {
           
            lock.lock();//手动上锁
            
            //同步代码块
        
        }finally {
            lock.unlock();//手动开锁
        }
```

* **方式一：同步代码块**

* 1、需要被同步的代码    (别包多了代码，成单线程了)------即操作共享数据的代码

*    2、共享数据：多个线程共同操作的变量---如100张票

*    3、同步监视器（就是锁）：任何一个类的对象都有可以充当一个锁Object类也可以

*    **要求：多个线程必须要共用同一把锁。**

*    4、在实现Runnable接口创建多线程的方式中，我们可以考虑使用this充当监视器。

*    5、在继承Thread类创建多线程的方式中，慎用this充当同步监视器，考虑使用当前类充当同步监视器。

	

* **方式二：同步方法**

* 如果操作共享数据的代码完整个的声明在一个方法中，我们不妨将此方法声明成同步的

* 1、同步方法仍然涉及到同步监视器，只是不需要我们显式的声明

* 2、非静态的同步方法，同步监视器是：this

* 3、静态的同步方法，同步监视器是：当前类本身。（主要是继承Thread类创建多线程，因为继承Thread类要创建多个对象，通过设置方法为static静态的，形成一把锁的效果）

​	

* **方式三：Lock锁----JDK5.0新增**

* 手动开启和关闭锁

#### 9、sleep() 和 wait() 的异同？？？

> 1、相同点：一旦执行方法，都可以是的当前的线程进入阻塞状态。
>
> 2、不同点：①两个方法声明的位置不同：Thread类中声明sleep（），Object类中声明wait（）
>
> ​					 ②调用要求不同：sleep（）可以在任何需要的场景下调用。wait（）必须使用在同步代码块或同步方法中
>
> ​					 ③关于是否释放同步监视器：如果两个方法都使用在同步代码块或同步方法中时，sleep（）不会释放锁，wait（）会释放锁

#### 10、String str = new String("abc");方式创建对象，在内存中创建了几个对象？

> 答：两个：一个是堆空间中new结构创建的对象，另一个是char[]对象的常量池中的数据：abc

![image-20210918225600492](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211004220250508-163335617173112.png)

#### 11、下列程序运行结果

##### 		1、输出结果：good and best

```java
public class StringTest {
    String str = new String("good");
    char[] ch = { 't', 'e', 's', 't' };
    public void change(String str, char ch[]) {
        str = "test ok";
        ch[0] = 'b';
    }
    public static void main(String[] args) {
        StringTest ex = new StringTest();
        ex.change(ex.str, ex.ch);
        System.out.print(ex.str + " and ");
        System.out.println(ex.ch);
        //输出结果：good and best
    }
}
```

##### 	2、增强for循环

```java
@Test
public void test3(){
    String[] str = new String[5];
    for (String s : str) {
        s = "钢蛋";
        System.out.println(s);//相当于原for循环，你把i的值改了，不影响原数组
    }
    
    
    for (int i = 0; i < str.length; i++) {
        System.out.println(str[i]);
    }
}
----------------------
钢蛋
钢蛋
钢蛋
钢蛋
钢蛋
null
null
null
null
null
```

##### 	3、List的remove()方法

remove可以按索引移除，还可以按对象移除



```java
@Test
public void testListRemove() {
    List list = new ArrayList();
    list.add(1);
    list.add(2);
    list.add(3);
    updateList(list);
    System.out.println(list);//1，2
}
private static void updateList(List list) {
    list.remove(2);//按索引，将3移除
    list.remove(new Integer(2));//按对象移除，将2移除
}
```

##### 4、Set接口理解

其中Person类中重写了hashCode()和equal()方法

```java
HashSet set = new HashSet();
Person p1 = new Person(1001,"AA");
Person p2 = new Person(1002,"BB");
set.add(p1);
set.add(p2);

p1.name = "CC";
set.remove(p1);
System.out.println(set);
//[Person{age=1002, name='BB'}, Person{age=1001, name='CC'}]
//并没有移除p1，为什么？？
//因为remove方法去查找p1时，按照name == CC去找到，肯定找不到，因为p1时按照AA哈希值存的

set.add(new Person(1001,"CC"));
System.out.println(set);
//[Person{age=1002, name='BB'}, Person{age=1001, name='CC'}, Person{age=1001, name='CC'}]
//同名的添加成功了，为什么？？
//跟上边一个道理，原有的name == CC存放的时name == AA的哈希地址，
//添加操作时name == CC哈希地址处为空，自然添加成功

set.add(new Person(1001,"AA"));
System.out.println(set);
//[Person{age=1002, name='BB'}, Person{age=1001, name='CC'}, Person{age=1001, name='CC'}, Person{age=1001, name='AA'}]
//那为什么name == AA的哈希地址位置占着，还能添加成功？？？？
//哈希地址判断不空，此时equals比较属性，因为AA和CC不同，默认为是两个对象，通过链表在同一个哈希地址后边增加

```



#### 12、String、StringBuffer、StringBuilder三者有何异同？

String：不可变的字符序列，底层结构使用char[]数组存储

StringBuffer：可变的字符序列，线程安全的，效率偏低；底层结构使用char[]数组存储

StringBuilder：可变的字符序列，JDK5.0新增，线程不安全，效率高些；底层结构使用char[]数组存储

**源码分析：**

```java
String str = new String();  
//char[] value = new value[0];
String str1 = new String("abc");    
//char[] value = new value[]{'a','b','c'};

StringBuffer sbf = new StringBuffer();  
//char[] value = new value[16];底层创建了一个长度为16的空数组
StringBuffer sbf2 = new StringBuffer("abc");  
//char[] value = new value["abc".length() + 16];底层创建了一个长度为3加16的空数组

sbf.append('a');//value[0] = 'a';
sbf.append('b');//value[1] = 'b';

    
```

**问题一：**sbf2.length()是多少？
    	      答：3，因为源码重写了length()方法。
**问题二：**扩容问题，如果要添加的数据底层数组装不下了，那就要扩容底层数组。
		      默认情况下，扩容为原来容量的2倍+2，同时将原有数组中的元素复制到新的数组中。

**指导意义：**在开发中尽可能使用StringBuffer(int capacity)  或者 StringBuilder(int capacity)，可预见的情况下，直接定义数组长度capacity

#### 13、“三天打鱼两天晒网”？

渔夫在1888-01-01日开始打鱼，问2021-09-09日   在打鱼？还是晒网？

```java
@Test
public void practice2() throws ParseException {
    String start = "1988-01-03";
    String end = "2021-09-09";
    SimpleDateFormat simpleDateFormat = new SimpleDateFormat("yyyy-MM-dd");
    Date dateStart = simpleDateFormat.parse(start);
    Date dateEnd = simpleDateFormat.parse(end);
    
    long day = (dateEnd.getTime() - dateStart.getTime())/(24 * 60 * 60 * 1000);
    long remainder = (dateEnd.getTime() - dateStart.getTime()) % (24 * 60 * 60 * 1000);
    if (remainder != 0) day += 1;

    if (day % 5 == 1 || day % 5 == 2 || day % 5 == 3){
        System.out.println("正在打鱼");
    }else{
        System.out.println("正在晒网");
    }

}
```



#### 14、线程通信的经典例题（生产者/消费者问题）

生产者（Productor）将产品交给店员（Clerk），而消费者（Customer）从店员处取走产品，店员一次只能持有固定数量的产品（比如20个），如果生产者试图生产更多产品，店员会叫生产者停一下，如果店中有空位放产品了再通知生产者继续生产；如果店中没有产品了，店员会告诉消费者等一下，如果店中有产品了再通知消费者来取走产品。

分析：

> 1、是否是多线程问题？是！生产者线程、消费者线程

> 2、是否有共享数据？有！店员（产品数量）

> 3、如何解决线程安全问题？同步机制，有三种方法

> 4、是否涉及到线程通信？是

```java
public class Clerk{//真正的同步代码段，下边两个类只是为了调用。

    private int productCount = 0;

    //消费产品
    public synchronized void coustomerProductor() {

        if (productCount > 0){
            System.out.println(Thread.currentThread().getName() + ":开始消费第" + productCount + "个产品");
            productCount--;
            notify();//生产者阻塞时，是产品满了，此时只要消费一个productCount--就可以notify唤醒
        }else{
            //等待
            try {
                wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }

    //生产产品
    public synchronized void producerProductor() {

        if (productCount < 20){
            productCount++;
            System.out.println(Thread.currentThread().getName() + ":开始生产第" + productCount + "个产品");
            notify();//消费者阻塞时，是产品卖没了，此时只要生产一个productCount++就可以notify唤醒
        }else{
            //等待
            try {
                wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

class Productor implements Runnable{//生产者

    private Clerk clerk ;

    public Productor(Clerk clerk){
        this.clerk = clerk;
    }

    @Override
    public void run(){
        System.out.println("开始生产产品。。。。");

        while(true){
            try{
                Thread.sleep(1);
            }catch(InterruptedException e){
                e.printStackTrace();
            }

            clerk.producerProductor();
        }
    }
}

class Customer implements Runnable{
    private Clerk clerk ;

    public Customer(Clerk clerk){
        this.clerk = clerk;
    }

    @Override
    public void run(){
        System.out.println("开始消费产品。。。。");

        while(true){
            try{
                Thread.sleep(10);
            }catch(InterruptedException e){
                e.printStackTrace();
            }

            clerk.coustomerProductor();
        }
    }
}
```



```java
public class ShopTest {
    public static void main(String[] args) {
        Clerk clerk = new Clerk();

        Thread p = new Thread(new Productor(clerk));
        Thread c = new Thread(new Customer(clerk));

        p.setName("生产者");
        c.setName("消费者");

        p.start();
        c.start();
    }
}
```



#### 15、ArrayList、LinkedList、Vector三者的异同？

**请问ArrayList/LinkedList/Vector的异同？ 谈谈你的理解？ ArrayList底层是什么？扩容机制？ Vector和ArrayList的最大区别?**  

**答：**

> **ArrayList和LinkedList的异同**
> 二者都线程不安全，相对线程安全的Vector，执行效率高。
> 此外， ArrayList是实现了基于动态数组的数据结构， LinkedList基于链表的数据结构。对于随机访问get和set， ArrayList觉得优于LinkedList，因为LinkedList要移动指针。对于新增和删除操作add(特指插入)和remove， LinkedList比较占优势，因为ArrayList要移动数据。\
> **ArrayList和Vector的区别**
> Vector和ArrayList几乎是完全相同的,唯一的区别在于Vector是同步类(synchronized)，属于强同步类。因此开销就比ArrayList要大，访问要慢。正常情况下,大多数的Java程序员使用ArrayList而不是Vector,因为同步完全可以由程序员自己来控制。 Vector每次扩容请求其大小的2倍空间，而ArrayList是1.5倍。 Vector还有一个子类Stack。  





**相同点：**三个类都是实现了List接口，存储数据的特点相同：都是存储有序的，可重复的数据

**不同点：**

​			ArrayList：作为List接口的主要实现类，线程不安全的，效率高；底层使用Object[] elementData存储

​			LinkedList：底层使用双向链表存储：对于频繁的插入、删除操作，此类效率比ArrayList高

​			Vector：作为List接口的古老实现类；线程安全的，效率低，底层使用Object[] elementData存储

**源码分析：**

**ArrayList：**

> JDK7情况下：
>
> ```java
> ArrayList list = new ArrayList();	//底层创建了长度为10的Object[]数组elementData
> List.add(123);//elementData[0] = new Integer(123);
> ...
> List.add(11);//添加超过10个，导致底层elementData[]数组容量不够，进行扩容。
> //默认情况下，扩容为原来容量的1.5倍，同时将原有数组中的数据复制到新的数组中。
> 
> //结论：建议开发中使用带参的构造器：ArrayList list = new ArrayList(int capacity);
> //直接确定第一次创建的底层数组大小
> ```

> JDK8情况下：【先不创建数组，第一次添加操作时再创建】
>
> ```java
> ArrayList list = new ArrayList();	//底层Object[]数组elementData初始化为{}，并没有创建数组
> List.add(123);//第一次调用add()时，底层才创建了长度为10的数组，并将数据123添加到elementData数组中
> //后续操作与JDK7一致
> ```

总结：JDK7中的ArrayList的对象的创建类似于单例模式中的饿汉式，而JDK8中的ArrayList的对象的创建类似于单例模式中的懒汉式，延迟了数组的创建，节省内存。



**LinkedList：**

> ```java
> @Test
> public void test4(){
>     LinkedList linkedList = new LinkedList();//内部声明了Node类型的first和last属性，默认值为null
>     linkedList.add(123);//将123封装到Node中，创建了Node对象。
>  
> }
> ```
>
> ```java
> //Node源码：体现了LinkedList的双向链表的说法
> private static class Node<E> {
>     E item;
>     LinkedList.Node<E> next;
>     LinkedList.Node<E> prev;
> 
>     Node(LinkedList.Node<E> prev, E element, LinkedList.Node<E> next) {
>         this.item = element;
>         this.next = next;
>         this.prev = prev;
>     }
> }
> ```



**Vector：**

> 对象之初就创建长度为10的底层数组，添加操作扩容时是原数组的2倍。



#### 16、集合Collection中存储自定义对象时，要重写哪个方法？

问：集合Collection中存储自定义对象时，要自定义类重写哪个方法？为什么？

答：equals()方法

List接口：重写equals()方法

Set接口：HashSet类、LinkedHashSet类：重写equals()、hashCode()方法

​				 TreeSet类：自然排序时（Comparable）：重写comparTo（Object obj）

​									   定制排序时（Comparator）：重写compare（Object o1，Object o2）



#### 17、说说HashMap的底层实现原理？？

**以JDK7为例：**

```java
HashMap map = new HashMap();
```

在实例化以后，底层创建了长度为16的一维数组Entry[] table

```java
map.put(key,value);
....//添加许多元素以后
map.put(key1,value1);
```

添加操作，首先调用key1所在类的hashCode()计算key1的哈希值，得到在Entry数组中存放的位置。

- 情况一：如果此位置上数据为空，此时的key1-value1添加成功

- 情况二：如果此位置上数据不为空，（意味着此位置上存在一个或多个数据【以链表的形式存在】），此时比较key1和已经存在的一个或多个数据的哈希值：

	- 1、如果key1的哈希值与已经存在的数据的哈希值都不同，此时key1-value1添加成功
	- 2、如果key1的哈希值与已经存在的某个数据（key2）的哈希值相同，继续比较：调用key1所在类的equals（key2）和key2比较
		- 2.1如果equals()返回false：此时key1-value1添加成功
		- 2.2如果equals()返回true：则使用value1替换key2的value2,。

	**补充：**关于情况1和2.1，此时key1-value1和原来的数据以链表的方式存储。

	**扩容：**在不断添加过程中，当超出临界值且要存放位置非空时，会涉及到扩容的问题，默认的扩容方式是：扩容为原来容量的2倍，并将原有的数据复制过来。

**JDK8中的改变**

1、new HashMap()	时，底层没有创建一个长度为16的数组。

2、JDK8底层数组是：Node[]，而非Entry[]。

3、首次调用put()方法时，底层创建长度为16的数组。

4、JDK7底层结构只有：数组＋链表。JDK8中地层结构增加了红黑树：**数组＋链表＋红黑树**。

​	  当数组的某一索引位置上的元素是以链表形式存在的数据个数 > 8时，且当前数组的长度 > 64时，

​	  此时索引位置上的所有数据改为使用红黑树存储。【就是同一哈希地址值上元素大于8个时，用红黑树存，好找】



#### 18、说说HashMap和Hashtable的异同？？

**HashMap:**作为Map接口的主要实现类：线程不安全的，效率高；存储null的key和value

**Hashtable:**作为古老的实现类；线程安全的，效率低；不能存储null的key和value



#### 19、**那么HashMap什么时候进行扩容呢？【JDK 7】**

当HashMap中的元素个数超过数组大小(数组总大小length,不是数组中个数size) × loadFactor 时 ， 就 会 进 行 数 组 扩 容 ， loadFactor 的 默 认 值(DEFAULT_LOAD_FACTOR)为0.75， 这是一个折中的取值。 也就是说， 默认情况下， **数组大小(DEFAULT_INITIAL_CAPACITY)为16， 那么当HashMap中元素个数超过16×0.75=12（这个值就是代码中的threshold值， 也叫做临界值） 的时候， 就把数组的大小扩展为 2×16=32， 即扩大一倍**， 然后重新计算每个元素在数组中的位置，而这是一个非常消耗性能的操作， 所以如果我们已经预知HashMap中元素的个数，那么预设元素的个数能够有效的提高HashMap的性能。  

#### 20、那么HashMap什么时候进行扩容和树形化呢【JDK 8】？

当HashMap中的元素个数超过数组大小(数组总大小length,不是数组中个数size) × loadFactor 时 ， 就 会 进 行 数 组 扩 容 ， loadFactor 的 默 认 值(DEFAULT_LOAD_FACTOR)为0.75， 这是一个折中的取值。 也就是说， 默认
情况下， 数组大小(DEFAULT_INITIAL_CAPACITY)为16， **那么当HashMap中元素个数超过16 × 0.75=12（这个值就是代码中的threshold值， 也叫做临界值）的时候， 就把数组的大小扩展为 2 × 16=32， 即扩大一倍，** 然后重新计算每个元素在数组中的位置， 而这是一个非常消耗性能的操作， 所以如果我们已经预知HashMap中元素的个数， 那么预设元素的个数能够有效的提高HashMap的性能。**当HashMap中的其中一个链的对象个数如果达到了8个，此时如果capacity没有达到64，那么HashMap会先扩容解决，如果已经达到了64，那么这个链会变成树，**结点类型由Node变成TreeNode类型。当然，如果当映射关系被移除后，下次resize方法时判断树的结点个数低于6个，也会把树再转为链表。  

#### 21、关于映射关系的key是否可以修改？ 

**答：不要修改**

映射关系存储到HashMap中会存储key的hash值，这样就不用在每次查找时重新计算每一个Entry或Node（TreeNode）的hash值了，因此如果已经put到Map中的映射关系，再修改key的属性，而这个属性又参与hashcode值的计算，那么会导致匹配不上。

#### 22、面试题：负载因子值的大小，对HashMap有什么影响

1、负载因子的大小决定了HashMap的数据密度。

2、负载因子越大密度越大，发生碰撞的几率越高，数组中的链表越容易长,造成查询或插入时的比较次数增多，性能会下降。

3、负载因子越小，就越容易触发扩容，数据密度也越小，意味着发生碰撞的几率越小，数组中的链表也就越短，查询和插入时比较的次数也越小，性能会更高。但是会浪费一定的内容空间。而且经常扩容也会影响性能，建
议初始化预设大一点的空间。

4、按照其他语言的参考及研究经验，会考虑将负载因子设置为0.7~0.75，此时平均检索长度接近于常数。    

#### 23、Collection 和 Collections的区别？

Collection是接口，

Collections是工具类

#### 24、Map常用的实现类结构？？

Map：双列数据，存储key-value对数据，类似函数y = f（x）

- **HashMap:**作为Map接口的主要实现类：线程不安全的，效率高；存储null的key和value
	- **LinkedHashMap:**保证在遍历map元素时，可以按照添加顺序实现遍历，

​							原因：在原有的HashMap底层结构基础上，添加了一对指针，指向一个前一个后

​							对于频繁的遍历操作，此类执行效率高于HashMap

- **TreeMap:**保证按照添加的key-value对进行排序，实现排序遍历，此时使用key进行排序底层层使用红黑树
- **Hashtable:**作为古老的实现类；线程安全的，效率低；不能存储null的key和value
	- **properties: **常用来处理配置文件，key和value都是String类型





**HashMap的底层：**数组＋链表（JDK7及以前）

​								数组＋链表＋红黑树（JDK8）

#### 25、自定义类-----实现Scanner类的功能

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class MyInput {

    //Read a string from the keyboard
    public static String readString(){
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        //Get a string from the keyboard
        String str = null;
        try {
            str = br.readLine();
        } catch (IOException e) {
            e.printStackTrace();
        }
        //Return the string obtained from the keyboard
        return str;
    }

    //Read an int value from the keyboard
    public static int readInt(){
        return Integer.parseInt(readString());
    }
    //Read a double value from the keyboard
    public static double readDouble(){
        return Double.parseDouble(readString());
    }
    //Read a float value from the keyboard
    public static float readFloat(){
        return Float.parseFloat(readString());
    }
    //Read a byte value from the keyboard
    public static byte readByte(){
        return Byte.parseByte(readString());
    }
    //Read a short value from the keyboard
    public static short readShort(){
        return Short.parseShort(readString());
    }
    //Read a long value from the keyboard
    public static long readLong(){
        return Long.parseLong(readString());
    }
    //Read an boolean value from the keyboard
    public static boolean readBoolean(){
        return Boolean.parseBoolean(readString());
    }
}
```



#### 26、谈谈你对java.io.Serializable接口的理解，我们知道它用于序列化，是空方法接口，还有其它认识吗？  

- 实现了Serializable接口的对象，可将它们转换成一系列字节，并可在以后完全恢复回原来的样子。 <font color='red'>**这一过程亦可通过网络进行。这意味着序列化机制能自动补偿操作系统间的差异。**</font> 换句话说，可以先在Windows机器上创建一个对象，对其序列化，然后通过网络发给一台Unix机器，然后在那里准确无误地重新“装配”。不必关心数据在不同机器上如何表示，也不必关心字节的顺序或者其他任何细节。
- 由于大部分作为参数的类如String、 Integer等都实现了java.io.Serializable的接口，也可以利用多态的性质，作为参数使接口更灵活。  

#### 27、谈谈TCP 和 UDP的区别？

- **<font color='red'>TCP协议：</font>**【先建立连接，再传输-------打电话】
	- 使用TCP协议前，须先建立TCP连接，形成传输数据通道
	- 传输前，采用“三次握手” 方式，点对点通信， <font color='red'>是可靠的</font>
	- TCP协议进行通信的两个应用进程：客户端、 服务端。
	- 在连接中<font color='red'>可进行大数据量的传输</font>
	- 传输完毕，<font color='red'>需释放已建立的连接， 效率低</font>
- <font color='red'>**UDP协议：**</font>【直接传输-------发短信】
	- 将数据、源、目的封装成数据包，<font color='red'> 不需要建立连接</font>
	- 每个数据报的大小限制在64K内
	- 发送不管对方是否准备好，接收方收到也不确认， 故是不可靠的
	- 可以广播发送
	- 发送数据结束时<font color='red'>无需释放资源，开销小，速度快</font>

