# 算法笔记（Java版）



#### 1、最大公约数and最小公倍数

```java
import java.util.Scanner;
public class DivisorAndMultiple {
    public static void main(String[] args){
        //创建一个对象
        Scanner scan = new Scanner(System.in);
        //输入两个整数
        System.out.println("请输入第一个整数");
        int num1 = scan.nextInt();
        System.out.println("请输入第二个整数");
        int num2 = scan.nextInt();

        int min = 1;
        int max = 1;
        int divisor = 1;        //divisor保存最大公约数
        int multiple = 1;       //multiple保存最小公倍数

        if(num1 > num2){
            max = num1;
            min = num2;
        }else if(num1 < num2){
            max = num2;
            min = num1;
        }else{
            divisor = num1;     //两数相等时，最大公约数==最小公倍数
            multiple = num1;
        }


        //最大公约数
        //取小的那个值，递减迭代
        for (int i = min; i >= 1; i--) {//公约数
            if(num2 % i ==0 && num1 % i ==0){
                divisor = i;
                break;
            }
        }
        //最小公倍数
        multiple = max;        //假设最小公倍数为max本身
        for (int i = 1; multiple <= num1 * num2; i++){//公倍数
            multiple = max * i;     //倍数迭代
            if(multiple % min == 0){
                break;
            }
        }
        System.out.println(num1 + "和" + num2 + "的最大公约数是" + divisor + ",最小公倍数是" + multiple);
    }
}
```





#### 2、水仙花数(MultiplicationTables)

水仙花数：一个三位数，其各位数字立方和等于该数本身。例如:153=1^3 + 5^3 + 3^3。就说明153是一个水仙花数；

```java
//水仙花数：一个三位数,其各位数字立方和等于该数本身。例如:153=1*1*1 + 5*5*5 + 3*3*3.这就说明153是一个水仙花数；
public class NarcissisticNumber {
    public static void main(String[] args){
        for (int i = 100; i <1000; i++) {
            int unit = i % 100 % 10; //个位
            int ten = i % 100 / 10;  //十位
            int hundred = i / 100;   //百位
            if(unit*unit*unit + ten*ten*ten + hundred*hundred*hundred == i){
                System.out.println(i);
            }
        }
    }
}
```



#### 3、九九乘法表(MultiplicationTables)

```java
//九九乘法表
public class MultiplicationTables {
    public static void main(String[] args){
        for (int i = 1; i <= 9; i++) {
            for (int j = 1; j <= i; j++) {
                System.out.print(j + "*" + i + "=" + (i*j) + " ");
            }
            System.out.println();
        }
    }
}
```



#### 4、输出质数（素数-PrimeNumber）

素数（质数）：是指在大于1的自然数中,除了1和它本身外,不能被其他自然数整除(除0以外)的数

```java
public class PrimeNumber {
    public static void main(String[] args){
        int isLine = 5;//控制换行输出
        boolean isFlag = true; //标记位
        for (int i = 2; i <100; i++) {  //输出100以内的素数，外循环遍历100以内自然数。
            for (int j = 2; j <i; j++) {  //内循环遍历小于 i 本身的所有自然数，不包括 1 和 i 本身。
                if(i % j == 0){  //存在可以除尽的非1非i的数据
                    isFlag = false;    //标记为false
                }
            }
            if(isFlag){          //若isFlag仍为原始的true，则 i 为素数。
                System.out.print(i + " ");//数据整行输出
                isLine--;
                if(isLine == 0){//5个数据后，输出换行，标记isLine重置为5
                    System.out.println();
                    isLine = 5;
                }
            }else{              //isFlag已经变为false，不是素数，此时将isFlag重置原始值true。
                isFlag = true;
            }
        }
    }
}
```

##### 4.1优化算法-----输出素数

优化一：在遍历内循环时，只要满足一个“非1非自身”的数可以整除，直接break跳出循环，因为此时“i”已经不是质数。对“非质数”数据优化明显；

优化二：在遍历内循环时，判断“i”是否为质数，不用遍历2-->i，只要判断2-->根号i，若不能被整除，就说明“i”是质数。对所有数据均有优化，但因优化一存在，非质数已经跳出循环，所以此条优化更有助于“质数”的数据优化；

![image](https://img2020.cnblogs.com/blog/2405733/202107/2405733-20210730095246102-2145600315.png)
如何判断是否在两数相乘等于第三个数
 即 ：a × b = c
因为不包含1，所以 a 、b 两个数最小均为 2 ，且最大均为c / 2。
a = 2 时，b = c / 2，满足条件a × b = c；
a = c / 2 时，b = 2，满足条件a × b = c；

a 从 2 开始不断递增，到 c / 2截止（2，3，4，5，6，7————c / 2）
此时 b 从 c / 2 开始不断减小，到 2 截止（c / 2————7，6，5，4，3，2）
此时 a = 2 和 b = 2 时相当于重复遍历，找到 a 和 b 的临界点，停止遍历，这样就不会重复了，临界点就是 a = b 的点，如上述例子中的10，当 a = b 时，恰好 a 为根号c

```java
public class PrimeNumber {
    public static void main(String[] args){
        long start = System.currentTimeMillis();//开始时间
        int isLine = 5;
        boolean isFlag = true;
        for (int i = 2; i <100000; i++) {//输出100000以内的素数
            for (int j = 2; j <= Math.sqrt(i); j++) {  //优化二：只取根号i ---对本身质数的数据优化！！！！
                if(i % j == 0){
                    isFlag = false;
                    break;//优化一：对本身为非质数的数据优化！！！！！
                }
            }
            if(isFlag){
                System.out.print(i + " ");
                isLine--;
                if(isLine == 0){
                    System.out.println();
                    isLine = 5;
                }
            }else{
                isFlag = true;
            }
        }
        long end = System.currentTimeMillis();//结束时间
        System.out.println("程序运行时间：" + (end-start));//输出程序运行时间
    }
}

```

##### 4.2【最简版】输出素数代码：

```java
public class PrimeNumber {
    public static void main(String[] args){
        label:for (int i = 2; i <100000; i++) {
            for (int j = 2; j <= Math.sqrt(i); j++) {
                if (i % j == 0) {
                    continue label;//存在可以整除的数，跳出当前循环，回到外层循环继续执行。
                }
            }
            System.out.println(i);//因非质数已经通过continue跳出本层循环，凡是可以运行到此位置的，均为质数
        }
    }
}
```

#### 5、完全数(PerfectNumber)

完全数（完数）：如果一个数等于它的因子之和，则称该数为“完数”（或“完全数”）。
例如，6的因子为1、2、3,而 6=1+2+3,因此6是“完数”。

内层循环时，遍历到 “i/2” 即可，因数1和 i ，2和i/2，3和i/3............不包括本身，所以最大遍历到 i/2。

```java
public class PerfectNumber {
    public static void main(String[] args){
        int factor = 0;//统计因子之和
        //输出10000以内的完全数
        for (int i = 1; i <= 10000; i++) {
            for (int j = 1; j <= i/2; j++) {//   i/2为最大值，因不包含小数，
                if(i % j == 0){         //求因数1和本身，2和i/2，3和i/3，不包括本身，所以最大遍历到i/2.
                    factor += j;
                }
            }
            if(factor == i){
                System.out.println(i);
            }
            factor = 0;//本次循环结束，重置为0，开始下次因子计数。
        }
    }
}
```

#### 6、杨辉三角（Pascal's Triangle）

​	1、每个数等于它上方两数之和【直角模式等于上方和左上方元素之和】。

​	2、每行数字左右对称，由1开始逐渐变大。

​	3、第一行有1个元素，第n行有n个元素。

示例输出10行：

![image](https://img2020.cnblogs.com/blog/2405733/202107/2405733-20210731193035651-1127221330.png)

```java
public class PascalTriangle {
    public static void main(String[] args){
        int line = 10;                    //输出10行的杨辉三角
        int[][] triangle = new int[line][];

        for (int i = 0; i < line; i++) {  //动态初始化列元素
            triangle[i] = new int[i+1];
        }
        for (int i = 0; i < triangle.length; i++) {
            for (int j = 0; j < triangle[i].length; j++) {
                //根据性质对杨辉三角进行赋值
                if (j == 0 || j == i){
                    triangle[i][j] = 1;
                }else{
                    triangle[i][j] = triangle[i-1][j] + triangle[i-1][j-1];
                }
                //输出整列元素
                System.out.print(triangle[i][j] + " ");
            }
            //整列输出完毕，换行操作
            System.out.println();
        }
    }
}
```

