---

---

# JavaWeb学习笔记

## 概述

- **JavaWeb技术体系**



![image-20211028222119082](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211028222119082-16354308824161.png)

- **书城项目**

![image-20211028222444305](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211028222444305-16354310857932.png)

- **书城项目阶段目标**

![image-20211028222544505](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211028222544505-16354311470803.png)



## 第1章 HTML

### 1、概念：b/s与c/s

a) 现在的软件开发的整体架构主要分为B/S架构与C/S架构：

- b/s：浏览器/服务器

- c/s：客户端/服务器

客户端：需要安装在系统里，才可使用

浏览器：浏览网页，读取HTML并显示

服务器：处理浏览器的请求

 

b) b/s与c/s优劣

- b/s只要能上网就能使用，因为基本每台电脑都会有浏览器，维护方便。

- c/s必须安装在系统中，安装成功才可使用。在新的系统中没有安装不能使用，便携性差，维护成本高。

 

c) 网页

浏览器中显示的内容，浏览器是网页的展示器。编写好的网页，放在浏览器中即可运行。编写网页我们使用的就是HTML语言



### 2、前端的开发流程

![image-20211029082045411](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211029083345021-16354676264517.png)

### 3、网页的组成部分

![image-20211029082118467](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211029082458151-16354670995946.png)

### 4、HTML简介

- HTML 是用来描述网页的一种语言。

- HTML 指的是超文本标记语言 (Hyper Text Markup Language)

- 超文本就是指页面内可以包含图片、链接，甚至音乐、程序等非文字元素

- HTML 不是一种编程语言，而是一种标记语言 (markup language)

- 标记语言是一套标记标签 (markup tag)

- HTML 使用标记标签来描述网页

### 5、创建HTML文件

![image-20211029083345021](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211029082045411-16354668466474.png)

![image-20211029082458151](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211029082118467-16354668796775.png)

### 6、HTML文件的书写规范

```html
<html>								<!-- 表示整个html页面的开始 -->
    <head>							<!-- 头信息 -->
        <title>网页标题</title>		  <!-- 标题 -->
    </head>
    <body>							<!-- body是页面的主体内容 -->
    	页面主体内容
    </body>
</html>								<!-- 表示整个html页面的结束 -->
```

注释内容可以在右键查看页面源代码中显示！



### 7、HTML标签介绍

- 标签的格式：

```html
<标签名>封装的数据</标签名>
```

- 标签名的大小写不敏感
- 标签拥有自己的属性
	- 分为基本属性：bgcolor=“red”				可以修改简单的样式效果
	- 事件属性：onclick="alert('你好！');"       可以直接设置事件响应后的代码
- 标签又分为，单标签和双标签

```html
单标签格式
<标签名/>

双标签格式
<标签名>封装的数据</标签名>
```



### 8、常用标签介绍

- n 标题：h1~h6  如:<h1>你好</h1>

- n 段落：p   如：<p>锄禾日当午</p>

- n 格式化：b  如：<b>宝塔镇河妖</b>

- n 换行：br   如：<br />这是个自结束标签

- n 无序列表:ul li  

```html
- 如：<ul>

<li>天王盖地虎</li>

<li>雪碧两块五</li>

</ul> 这是个组合标签，我们需要把两个一起使用
```

- n 图片：img  如：<img src=”美女.jpg”/> src表示图片的位置

- n 内联框架：iframe  如：<iframe src="1.html"></iframe>

- n 超链接：a  如：

```html
<a href="1.html">去1.html</a> href表示点击后跳转去的位置
```

  

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>grammar</title>
</head>
<body>

   <!-- ①标签可以嵌套但不能交叉嵌套 -->
   正确：<p><i>早安，尚硅谷</i></p>
   错误：<p><i>早安，尚硅谷</p></i>
   
   <!-- ②标签必须正确关闭 -->
   <!-- i.有文本内容的标签： -->
   正确：<p>早安，尚硅谷</p>
   错误：<p>早安，尚硅谷
   
   <!-- ii.没有文本内容的标签： -->
   正确：<br />
   错误：<br>
   
   <!-- ③属性必须有值，属性值必须加引号 -->
   正确：<font color="blue">早安，尚硅谷</font>
   错误：<font color=blue>早安，尚硅谷</font>
   错误：<font color>早安，尚硅谷</font>
      
   <!-- ④注释不能嵌套 -->
   正确：<!-- 注释内容 -->
   错误：<!-- 注释内容<!-- 注释内容 --> -->
   

</body>
</html>
```

#### 8.1、font 字体标签

font标签是字体标签，他可以用来修改文本的字体、大小、颜色

```html
<font color="blue" face="黑体" size="14">hello</font>
```



#### 8.2、特殊字符

```html
空格: &nbsp;

   < : &lt;

   \> : &gt;
```

![image-20211029090316695](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211029090316695-16354693980648.png)

#### 8.3、标题标签

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>标题</title>
</head>
<body >
<!--演示标题标签-->
<!--h1最大
    h6最小
    不存在h7
    
    align 对齐属性
        left 左对齐（默认）
        center 居中
        right 右对齐
-->
<h1 align="left">标题1</h1>
<h2 align="center">标题2</h2>
<h3 align="right">标题3</h3>
<h4>标题4</h4>
<h5>标题5</h5>
<h6>标题6</h6>

</body>
</html>
```

![image-20211029090835066](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211029090835066-16354697165829.png)

#### 8.4、超链接

- a标签是 超链接
	- href属性设置连接的地址        
	- target属性设置 哪个目标进行跳转      
		- _self  在当前窗口打开【默认值】 
		-  _blank 通过新标签页打开



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>标题</title>
</head>
<body >

<!--a标签是 超链接
        href属性设置连接的地址
        target属性设置 哪个目标进行跳转
            _self  在当前窗口打开【默认值】
            _blank 通过新标签页打开

-->
<a href="https://www.cnblogs.com/Tianhaoblog/">TianHao的博客园</a><br />
<a href="https://www.cnblogs.com/Tianhaoblog/" target="_self">TianHao的博客园_self</a><br />
<a href="https://www.cnblogs.com/Tianhaoblog/" target="_blank">TianHao的博客园_blank</a><br />

</body>
</html>
```

#### 8.5、列表标签

- ol  是有序列表
- ul  是无序列表
- li  是列表项
- type属性可以修改列表项前面的符号

![image-20211029092853660](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211029092853660-163547093504610.png)



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>标题</title>
</head>
<body >
    <ul type="none">
        <li>张无忌</li>
        <li>赵敏</li>
        <li>周芷若</li>
        <li>小昭</li>
    </ul>
    <ul>
        <li>张无忌</li>
        <li>赵敏</li>
        <li>周芷若</li>
        <li>小昭</li>
    </ul>
    <ol>
        <li>张无忌</li>
        <li>赵敏</li>
        <li>周芷若</li>
        <li>小昭</li>
    </ol>

</body>
</html>
```

#### 8.6、img 标签

img标签是图片标签，用来显示图片

- src 属性可以设置图片的路径
- width 属性可以设置图片的宽度
- height 属性可以设置图片的高度
- border 属性可以设置图片的边框大小
- alt 属性可以设置图片路径找不到内容时，显示文字
- ![image-20211029094916002](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211029094132222-163547169357312.png)

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>image</title>
</head>
<body>

   <img src="ismg/girls.jpg" width="500" height="300" border="2" alt="找不到图片哈哈">
   <img alt="picture" src="../02.常用标签/girls.jpg">

</body>
</html>
```

在JavaSE中

- 相对路径：从工程名开始算
- 绝对路径：盘符：/目录/文件名

在Web中

- 相对路径：
	- .	            表示当前文件所在的目录
	- ..               表示当前文件所在目录的上一级目录
	- 文件名      表示当前文件所在目录的文件，相当于./文件名【./可以省略】
- 绝对路径：http://ip:port/工程名/资源路径



**同一目录下：**

![image-20211029093915254](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211029094916002-163547215729513.png)

**上层目录的子目录：**

![image-20211029094132222](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211029100953662-163547339548514.png)



#### 8.7、表格标签

table 标签是表格标签

- border 设置表格边框宽度
- width 设置表格宽度
- height 设置表格高度
- align 设置表格位置的对齐方式
- cellspacing 设置单元格间距，等于0时，是两个单元格挨在一起，并不是重合，是相邻
- 此时就是等于0的效果，是双倍的边框宽度，因为挨在一起了![image-20211029100953662](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211029235441027-163552288264316.png)

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>table</title>
</head>
<body>
   <table border="1" align="center" cellspacing="0">
      <tr><!-- tr行标签-->
         <th>姓名</th><!-- th表头标签-->
         <th>阵营</th>
         <th>职业</th>
         <th>武器</th>
      </tr>
      <tr>
         <td width="80" align="center">刘备</td>
         <td width="60" align="center">蜀</td>
         <td width="200">蜀汉集团董事长</td>
         <td width="80">双股剑</td>
      </tr>
      <tr>
         <td align="center">诸葛亮</td>
         <td align="center">蜀</td>
         <td>蜀汉集团CEO</td>
         <td>羽扇</td>
      </tr>
      <tr>
         <td align="center">关羽</td>
         <td align="center">蜀</td>
         <td>荆襄总裁</td>
         <td>青龙偃月刀</td>
      </tr>
      <tr>
         <td align="center">张飞</td>
         <td align="center">蜀</td>
         <td>阆中销售经理</td>
         <td>丈八蛇矛</td>
      </tr>
   </table>
</body>
</html>
```



tr 是行标签

th 是表头标签

td 是单元格标签

- align 设置单元格文本对齐方式

b 是加粗标签



#### 8.8、跨行跨列表格

- colspan 属性设置跨列
- rowspan 属性设置跨行

<font color=red>注意：跨行或者跨列后，记得删除多余的行，否则表格变形</font>

需求：新建一个五行五列的表格

第一行，第一列的单元格要跨两列

第二行第一列的单元格跨两行

第四行第四列的单元格跨两行两列

![image-20211029102411491](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211029102411491-163547425299315.png)

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>table_blank</title>
</head>
<body>
    <table align="center" width="300" height="300" cellspacing="0" border="1">
        <tr>
            <td colspan="2">1.1</td>
            <td>1.3</td>
            <td>1.4</td>
            <td>1.5</td>
        </tr>
        <tr>
            <td>2.1</td>
            <td>2.2</td>
            <td rowspan="2">2.3</td>
            <td>2.4</td>
            <td>2.5</td>
        </tr>
        <tr>
            <td>3.1</td>
            <td>3.2</td>
            <td>3.4</td>
            <td>3.5</td>
        </tr>
        <tr>
            <td colspan="2" rowspan="2">4.1</td>
            <td>4.3</td>
            <td>4.4</td>
            <td>4.5</td>
        </tr>
        <tr>
            <td>5.3</td>
            <td>5.4</td>
            <td>5.5</td>
        </tr>
    </table>
   
</body>
</html>
```



#### 8.9、了解iframe框架标签

iframe 标签他可以在一个html页面上，打开一个小窗口，去加载一个单独的页面

iframe 标签和a标签组合使用的步骤：【就是点击超链接，在iframe小窗口中显式内容】

- 1、在iframe标签中使用name属性，定义一个名称
- 2、在a标签的target属性上设置iframe的name属性值

![image-20211029235441027](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211029093915254-163547155702211.png)

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>form空白</title>
</head>
<body>
我是一个单独的页面<br />
<iframe src="../05.表格/table.html" width="600" height="200" name="window"></iframe><br/>
<ul>
    <li><a href="../05.表格/table.html" target="window">三国演义</a></li>
    <li><a href="../03.插入图片/img.html" target="window">美女图片</a></li>
    <li><a href="../05.表格/table空白.html" target="window">自定义表格</a></li>
</ul>

</body>
</html>
```



#### 8.10、表单标签

##### 一、属性

表单就是html页面中，用来收集用户所有信息的

form标签就是表单标签

- <font color='red'>input  type=text   是文本输入框   </font>
	- value 属性设置默认显示内容
- <font color='red'>input  type=password    是密码输入框   </font>
	- value 属性设置默认填充内容
- <font color='red'>input  type=radio    是单选框   </font>
	- name属性可以对其进行分组，【只有分组才能单选，要不然每个都是独立的都可以选】 
	- checked=“checked"表示默认选中
- <font color='red'>input type=checkbook   是复选框   </font>
	- checked=“checked"表示默认选中
- <font color='red'>input type=“reset”   是重置按钮</font>
	- value 属性修改重置按钮中的内容
- <font color='red'>input type=“submit”   是提交按钮</font>
	- value 属性修改提交按钮中的内容

- <font color='red'>input type=“button”   是按钮</font>
	- value 属性修改按钮中的内容
- <font color='red'>input type=“file”   是文件上传域</font>
- <font color='red'>input type=“hidden”   是隐藏域</font>，当我们要发送某些信息，不需要用户参与，就可以使用隐藏域（提交的时候会同步提交给服务器）

- <font color='red'>select 标签是下拉列表框</font>
	- option 标签是下拉列表框中的选项 
		- select=“select”设置默认选中
- <font color='red'>textarea 表示多行文本输入框</font>【起始标签和结束标签中的内容是默认值，value设置默认值不再适用】
	- rows  属性设置显式几行的高度
	- cols  属性设置每行可以显式几个字符宽度

![image-20211030082751905](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211030082751905-163555367309617.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <form>
        用户名：<input type="text" value="请填写用户名"/><br/>
        密码：<input type="password" value="123"/><br/>
        确认密码：<input type="password" value="123"/><br/>
        性别：<input type="radio" name="sex"/>男<input type="radio" name="sex"/>女<br/>
        兴趣爱好：<input type="checkbox" checked="checked"/>Java<input type="checkbox" checked="checked"/>C++<input type="checkbox" checked="checked"/>Python<br/>
        国籍：<select>
                    <option>中国</option>
                    <option>美国</option>
                    <option>瑞士</option>
                    <option>挪威</option>
             </select><br/>
        自我评价：<textarea rows="8" cols="16">请输入自我评价，显式文本框尺寸高8行，宽16行</textarea><br/>
        <input type="file"/><br/>
        <input type="hidden" name="我是隐藏的" value="你看不到我哈哈！"/><br/>

        <input type="reset" value="点击重置"/>
        <input type="submit" value="点击提交"/><br/>
    </form>
</body>
</html>
```

##### 二、表单格式化：

**表单对齐工整，通过表格来实现，代码如下**

![image-20211030084325825](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211030084325825-163555460746918.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <form>
        <h2 align="center">用户注册</h2>
        <table align="center">
            <tr>
                <td>用户名：</td>
                <td>
                    <input type="text" value="请填写用户名"/>
                    <br/>
                </td>
            </tr>
            <tr>
                <td>密码：</td>
                <td>
                    <input type="password" value="123"/>
                    <br/>
                </td>
            </tr>
            <tr>
                <td>确认密码：</td>
                <td>
                    <input type="password" value="123"/>
                    <br/>
                </td>
            </tr>
            <tr>
                <td>性别：</td>
                <td>
                    <input type="radio" name="sex"/>男
                    <input type="radio" name="sex"/>女
                    <br/>
                </td>
            </tr>
            <tr>
                <td>兴趣爱好：</td>
                <td>
                    <input type="checkbox" checked="checked"/>Java
                    <input type="checkbox" checked="checked"/>C++
                    <input type="checkbox" checked="checked"/>Python
                    <br/>
                </td>
            </tr>
            <tr>
                <td>国籍：</td>
                <td>
                    <select>
                        <option>中国</option>
                        <option>美国</option>
                        <option>瑞士</option>
                        <option>挪威</option>
                    </select><br/>
                </td>
            </tr>
            <tr>
                <td>自我评价：</td>
                <td>
                    <textarea rows="8" cols="16">请输入自我评价，显式文本框尺寸高8行，宽16行</textarea>
                    <br/>
                </td>
            </tr>
            <tr>
                <td colspan="2">
                    <input type="file"/><br/>
                </td>
                <td>
                    <input type="hidden" name="我是隐藏的" value="你看不到我哈哈！"/><br/>
                </td>
            </tr>
            <tr>
                <td>
                    <input type="reset"/>
                </td>
                <td>
                    <input type="submit"/><br/>
                </td>
            </tr>
        </table>
    </form>
</body>
</html>
```

##### 三、提交表单数据

- action属性设置提交的服务器地址
- method属性设置提交的方式GET（默认值）或者POST

**表单提交时，数据没有发送给服务器的三种情况：**

- 1、表单项没有写name属性值
- 2、单选、复选、下拉列表中的option都需要添加value属性，以便发送给服务器
- 3、表单项不在form标签中，写到外边去了

<FONT COLOR='RED'>**GET和POST对比**</FONT>

<FONT COLOR='blue'>GET请求的特点是：</font>

- 浏览器地址栏中的地址是：action属性值+？+请求参数
- 请求参数格式为：name=value&name=value........
- 不安全，所有表单信息全部暴露在地址栏中
- 他有字符长度限制

<FONT COLOR='RED'>POST请求的特点是：</font>

- 浏览器地址栏中只有action属性
- 相对于GET请求更安全，因为不在地址栏中暴露信息
- 理论上没有长度限制



#### 8.11、其他标签

- div标签：默认独占一行【就是省去了后边的换行符】
- span标签：将需要的文本括起来，可以为其设置颜色、超链接等属性之类的
- p段落标签：默认会在标签上方和下方各空出一行来，若有空行存在，则不再空

![image-20211030092008032](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211030121617360-163556737889421.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <div>我是div</div>
    <div>我不是div</div>

    我其实是一个标签，我是什么标签呢？<span style="color: blue">我是一个span标签</span>，我真神奇啊


    <p>上边下边各空一行</p>
    <p>段落的常规操作</p>
</body>
</html>
```

## 第2章 CSS

### 1、CSS技术介绍

CSS指层叠样式表(CascadingStyleSheets)。主要用来设置网页中元素的样式。如边框，颜色，位置等…

CSS即可以现在HTML中，也可以写在元素的style属性里面，还可以写在.css外部文件里然后引入到页面

### 2、CSS语法规则

![image-20211030121617360](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211030123750651-163556867167622.png)



- **选择器：**浏览器根据“选择器”决定受CSS样式影响的HTML元素（标签）
- **属性（property）：**是你要改变的样式名，并且每个属性都有一个值。属性和值被冒号分开，并由花括号包围，这样就组成了一个完整的样式声明（declaration），例如p{color:blue}
- **多个声明：**如果要定义不止一个声明，则需要用分号将每个声明分开。虽然最后一条声明的最后可以不加分号（但尽量在每条声明的末尾都加上分号）
- 例如：

```css
p{
	color:blue;
	font-size:30px;
}
注：一般情况下，每行只描述一个属性
CSS注释：/*注释内容*/
```

### 3、CSS和HTML的结合方式

#### 3.1 第一种

- **在标签style属性上设置“key：value value;”，修改标签样式**

需求：分别定义两个div、span标签，分别修改每个div标签的样式为：边框1个像素，实线，红色。

![image-20211030123750651](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211030124612843-163556917494123.png)

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>CSS基本语法</title>

</head>
<body>
   <p>师傅领进门，修行靠个人</p>
   <div style="border: 1px solid red">div标签1</div>
   <div style="border: 2px solid blue">div标签2</div>
   <span style="border: 3px solid black">span标签1</span>
   <span style="border: 4px solid greenyellow">span标签2</span>
</body>
</html>
```

- **这只方式的缺点？**
	- 如果标签多了，样式多了。代码量非常庞大
	- 可读性非常差
	- CSS代码没什么复用性可言

#### 3.2 第二种

- 在head标签中使用style标签来定义各种自己需要的CSS样式

格式如下：

```html
xxx{
	Key:value value;
}
```

![image-20211030124612843](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211030125629998-163556979114124.png)

```html
<!DOCTYPE html>
<html>
<head>
   <meta charset="UTF-8">
   <title>CSS基本语法</title>
   <!--style标签专门用来定义CSS样式代码   -->
   <style type="text/css">
      /*这里是CSS代码格式，html语法的注释不能用*/
      div{
         border: 1px solid red;
      }
      span{
         border: 1px solid red;
      }
   </style>
</head>
<body>
   <p>师傅领进门，修行靠个人</p>
   <div>div标签1</div>
   <div>div标签2</div>
   <span>span标签1</span>
   <span>span标签2</span>
</body>
</html>
```

- **这只方式的缺点？**
	- 只能在同一页面内复用代码，不能在多个页面中复用CSS代码
	- 维护起来不方便，实际的项目中会有成千上万的页面，要到每个页面中去修改。工作量太大了

#### 3.3 第三种【最终版】

把CSS样式写成一个单独的文件，再通过link标签引入即可复用。

```html
使用html的<link rel="stylesheet" type="text/css" href="./style.css">标签导入CSS样式
```



```html
<!DOCTYPE html>
<html>
<head>
   <meta charset="UTF-8">
   <title>CSS基本语法</title>
   <!--link标签专门用来引用CSS样式代码    -->
   <link rel="stylesheet" type="text/css" href="styleTiaN.css"/>
</head>
<body>
   <p>师傅领进门，修行靠个人</p>
   <div>div标签1</div>
   <div>div标签2</div>
   <span>span标签1</span>
   <span>span标签2</span>
</body>
</html>
```



这里就相当于一个properties文件，把他单独写出去，然后用的时候在head标签中调用

```css
/*这里是CSS代码格式，html语法的注释不能用*/
div{
    border: 1px solid red;
}
span{
    border: 1px solid red;
}
```

![image-20211030125629998](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211030162547499-163558234908225.png)



### 4、CSS选择器

#### 4.1、标签名选择器

**格式：**

```css
标签名{
	属性名：值
}
```



需求：在所有div标签上修改字体颜色为蓝色，字体大小为30个像素。边框为1个像素黄色实线。

并修改所有span标签的字体颜色为黄色，字体大小为20个像素，边框为5像素蓝色虚线

![image-20211030162547499](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211030163421369-163558286278226.png)

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>CSS选择器</title>
   <style type="text/css">
      div{
         border: 1px solid yellow;
         color: blue;
         font-size: 30px;
      }
      span{
         border: 5px dashed yellow;
         color: yellow;
         font-size: 20px;
      }
   </style>
</head>
<body>
   <h2>冬夜读书示子聿</h2>
   <p>宋代•陆游</p>
   <div>古人学问无遗力</div>
   <span>少壮工夫老始成</span>
   <p>纸上得来终觉浅</p>
   <p>绝知此事要躬行</p>
</body>
</html>
```



#### 4.2、id选择器

格式：

```css
#id 属性值{
	属性名：值
}
```

**id选择器可以让我们通过id属性来选择CSS样式**





需求：

分别定义两个div标签

- 第一个div标签定义id为id001，然后根据id属性定义CSS样式修改字体颜色为蓝色字体大小为30px，边框为1像素黄色实线
- 第二个div标签定义id为id002，然后根据id属性定义CSS样式 修改字体颜色为红色，字体大小为20px，边框为5像素蓝色点线

![image-20211030163421369](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211030164216408-163558333766527.png)

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>CSS选择器</title>
   <style type="text/css">
      #id001{
         color: blue;
         font-size: 30px;
         border: 1px yellow solid;
      }
      #id002{
         color: red;
         font-size: 20px;
         border: 5px blue dotted;
      }

   </style>
</head>
<body>
   <h2>冬夜读书示子聿</h2>
   <p>宋代•陆游</p>
   <div id="id001">古人学问无遗力</div>
   <span>少壮工夫老始成</span>
   <div id="id002">纸上得来终觉浅</div>
   <p>绝知此事要躬行</p>
</body>
</html>
```



#### 4.3、class选择器（类选择器）

格式：

```css
.class 属性值{
	属性名：值
}
```

**class选择器可以让我们通过class属性来选择CSS样式**



需求1：修改 class 属性值为 class01 的span或者div标签，字体颜色为蓝色，字体大小为30像素，边框为1像素黄色实线

需求2：修改 class 属性值为 class02的 div标签，字体颜色为灰色，字体大小为20像素，边框为1像素红色实线

![image-20211030164216408](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211031173220225-16356727423601.png)

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>CSS选择器</title>
   <style type="text/css">
      .class01{
         color: blue;
         font-size: 30px;
         border: 1px solid yellow;
      }
      .class02{
         color: gray;
         font-size: 20px;
         border: 1px solid red;
      }

   </style>
</head>
<body>
   <h2>冬夜读书示子聿</h2>
   <p>宋代•陆游</p>
   <div class="class01">古人学问无遗力</div>
   <span class="class01">少壮工夫老始成</span>
   <div class="class02">纸上得来终觉浅</div>
   <p>绝知此事要躬行</p>
</body>
</html>
```



#### 4.4、组合选择器（类选择器）

格式：

```css
选择器1，选择器2，。。。。选择器n{
	属性名：值
}
```

**组合选择器可以让我们通过多个选择器来共用CSS样式**



```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>CSS选择器</title>
   <!------------------------------------------------------> 
   <style type="text/css">
      .class01,#id001{
         color: blue;
         font-size: 30px;
         border: red solid 1px;
      }
   <!------------------------------------------------------> 

   </style>
</head>
<body>
   <h2>冬夜读书示子聿</h2>
   <p>宋代•陆游</p>
   <div class="class01">古人学问无遗力</div>
   <span id="id001">少壮工夫老始成</span>
   <div class="class02">纸上得来终觉浅</div>
   <p>绝知此事要躬行</p>
</body>
</html>
```



### 5、CSS常用样式

- 颜色
	- color：red；颜色可以写颜色名如：black,blue,red,green,white,yellow等颜色也可以写rgb值和十六进制表示值：如rgb(255,0,0)，#00F6DE，如果写十六进制值必须加#

- 宽度
	- width:19px;宽度可以写像素值：19px；也可以写百分比值：20%；

- 高度
	- height:20px;同宽度一样

- 背景颜色
	- background-color:#0F2D4C

- 字体样式字体颜色
	- color:#bbffaa;
- 字体大小
	- font-size:20px;

- 黑色1像素实线边框
	- border:1pxsolidblack;

- div标签居中
	- margin-left:auto;margin-right:auto;

- 文本居中

	- text-align:center;

	```css
	div{
	   color: red;
	   border: 1px yellow solid;
	   width: 300px;
	   height: 300px;
	   background-color: gray;
	   font-size: 30px;
	   margin-left: auto;
	   margin-right: auto;
	   text-align: center;
	}
	```

- 超链接去下划线

	```css
	a{
	   text-decoration: none;
	}
	```

- 表格细线

	```css
	table{
	   border: 1px red solid;/*设置边框*/
	   border-collapse: collapse;/*将边框合并*/
	}
	```

- 列表去除修饰

	```CSS
	ul{
	   list-style: none;/*就是关闭了前边的着重号，或者序号，仅显示列表本身*/
	}
	```



## 第3章 JavaScript

### 1、JavaScript 介绍

**起源：**

在1995年时，由Netscape公司的BrendanEich，在网景导航者浏览器上首次设计实现而成。

Netscape在最初将其脚本语言命名为LiveScript，因为Netscape与Sun合作，网景公司管理层希望它外观看起来像Java，因此取名为JavaScript。

<font color='red' >JavaScript是弱类型，Java是强类型</font>

弱类型就是类型可变；

强类型，就是定义变量的时候，类型已经确定了。int a=0；

**作用：**

- 在前段页面中验证用户提交信息是否符合要求和服务器发生交互，判断用户名是否存在[ajax]

**特点：**

- 交互性：（他可以做的就是信息的动态交互）
- 安全性（不允许直接访问本地磁盘）
- 跨平台性（只要是解释JavaScript的浏览器都可以执行，和平台无关）



### 2、JavaScript 和 html 代码的结合方式

#### 2.1、第一种方式

只需要在 head 标签中，或者在body标签中，使用script 标签来书写JavaScript代码

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript">
        //alert是JavaScript语言提供的一个警告框函数
        //他可以接受任何类型的参数，这个参数就是警告框的提示信息
        alert("hello javascript");
    </script>
</head>
<body>

</body>
</html>
```



#### 2.2、第二种方式

使用script 标签引入 单独的JavaScript代码文件

- <font color='red'>**script标签可以用来定义JavaScript代码，也可以用来引入JavaScript代码文件，但是只能二选一，不能同时使用**</font>
- **想要在一个HTML文件中既实现引用，又实现自己写，用两个script标签就行**



JavaScript文件：【就相当于一个properties文件，代码写在里面，通过引用调用】

```javascript
alert("hello javascript");
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <!--
        现在需要使用script标签引入外部的JavaScript文件来执行
            src 属性专门用来引入JavaScript文件路径（可以是相对路径，也可以是绝对路径）
    -->
    <script type="text/javascript" src="src/1.js"></script>
</head>
<body>

</body>
</html>
```

### 3、变量

变量就是可以存放某些值的内存的命名

**JavaScript的变量类型**

- 数值类型：number
- 字符串类型：string
- 对象类型：object
- 布尔类型：boolean
- 函数类型：function

**JavaScript 里的特殊值**

- undefined：未定义，所有JavaScript变量未赋值时，默认值都是undefined
- null：空值
- NAN：全称：Not a Number。非数字。非数值。

**JavaScript 中的定义变量的格式：**

- var 变量名；

- var 变量名=值；

```javascript
<script type="text/javascript">
    var i;
    i = 12;
    alert(i);//12
    alert(typeof (i));//number
    i = "abc";
    alert(typeof (i));//string【变量类型根据赋值可以改变】

    var a = 88;
    var b = "zbc";
    alert(a*b);//NaN，非数字，非数值。


</script>
```



#### 3.1、关系（比较）运算

- 等于：==    【等于是简单的做字面值的比较】

- 全等于：===   【除了做字面值的比较之外，还会比较两个变量的数据类型】

```javascript
<script type="text/javascript">
    var a = "12";
    var b = 12;
    alert(a==b);//true
    alert(a===b);//false

</script>
```



#### 3.2、逻辑运算

- 且运算：&&
- 或运算：||
- 取反运算：！

在JavaScript语言中，所有的变量都可以作为一个boolean类型的变量去使用

- <font color="red">0、null、undefined、“”（空字符串）</font>、都认为是<font color="blue">false</font>



##### &&且运算

- 一、当表达式全为真的时候，返回最后一个表达式的值。

- 二、当表达式中，有一个为假的时候，返回第一个为假的表达式的值

```javascript
<script type="text/javascript">
    var a = "abc";
    var b = true;
    var c = false;
    var d = null;
    alert(a && b);//true
    alert(a && c);//false
    alert(a && b && d);//null
    alert(c && b);//false
</script>
```

##### ||或运算

- 一、当表达式全为假时，返回最后一个表达式的值
- 二、只要有一个表达式为真，就返回第一个为真的表达式的值

```javascript
<script type="text/javascript">
    var a = "abc";
    var b = true;
    var c = false;
    var d = null;

    alert(c || d);//null
    alert(a || b);//abc
    alert(a || c);//abc
    alert(a || b || d);//abc
    alert(c || b);//true
</script>
```



##### 短路

&& 和||运算 都是有短路的

就是说只要有任何一个运算有了结果，后边的表达式就不再执行。



### 4、数组

#### 4.1数组的定义方式

格式：

```javascript
<script type="text/javascript">
    var 数组名 = [];  //空数组
    var 数组名 = [1,"abc",true];  //定义数组、同时赋值
</script>
```

```javascript
<script type="text/javascript">
    var 数组名 = [];  //空数组
    var 数组名 = [1,"abc",true];  //定义数组、同时赋值

    //JavaScript 语言中的数组，只要我们通过数组下标赋值，那么最大的下标值，就会自动的给数组做扩容操作
    //而且可以跳跃赋值
    var arr = [];
    alert(arr.length)//长度为0
    arr[0] = "abc";
    alert(arr.length)//长度为1
    arr[6] = 88;
    alert(arr[6]);//88
    alert(arr.length)//长度为7
    alert(arr[3]);//undefined

    // 遍历
    for (var i = 0; i < arr.length; i++) {//不能定义int，要用var
        alert(arr[i]);
    }
</script>
```

### 5、函数

#### 5.1、函数的两种定义方式

##### 5.1.1、第一种：可以使用function关键字来定义函数

格式如下：

```javascript
function 函数名(参数1，参数2...){//可以无参数，参数不需要定义类型，根据传入的类型确定
    函数体;
    //若需要返回值，直接在函数体重加入return语句就可以了
}
```



```javascript
<script type="text/javascript">
    //定义一个无参函数
    function fun(){
        alert("无参函数被调用了");
    }
    //定义一个有参函数
    function fun2(a,b){
        alert("有参函数被调用了；a=" + a + ",b=" + b);
    }
    //定义一个带有返回值的函数【其他都一样，在里面直接加一个return就行】
    function fun3(a,b){
        var result = a+b;
        return result;
    }

    //函数调用
    fun();
    fun2(123,"abcddsf");
    alert(fun3(3,8));

</script>
```



##### 5.1.2、第二种

```JavaScript
var 函数名 = function(形参列表){函数体}
```

```javascript
<script type="text/javascript">
    //定义一个无参函数
    var fun = function(){
        alert("无参函数被调用了");
    }
    //定义一个有参函数
    var fun2 = function(a,b){
        alert("有参函数被调用了；a=" + a + ",b=" + b);
    }
    //定义一个带有返回值的函数【其他都一样，在里面直接加一个return就行】
    var fun3 = function(a,b){
        var result = a+b;
        return result;
    }

    //函数调用
    fun();
    fun2(123,"abcddsf");
    alert(fun3(3,8));

</script>
```

<font color='red'>注：java中的函数允许重载，但是在JavaScript中函数的重载会直接覆盖掉上一次的定义</font>

#### 5.2、函数的arguments 隐形参数（只在function函数内）

**隐形参数：**就是在function函数中不需要定义，但却可以直接用来获取所有参数的变量

隐形参数特别像Java中的可变长参数一样。

public void test(Object ...args){}

可变长参数args其实是一个数组。

JavaScript中的隐形参数和Java的可变长参数一样，操作了类似数组。

```javascript
//隐形参数
function funArgu(){
    alert(arguments.length);//可看参数的个数【4】
    alert(arguments[0]);//1234
    alert(arguments[1]);//true
    alert(arguments[2]);//abc
    alert(arguments[3]);//null
    //遍历
    for (var i = 0;i < arguments.length;i++){
        alert(arguments[i]);
    }
}

funArgu(1234,true,"abc",null);
```

**应用：**

需求：编写一个函数，计算所有传入的参数相加，并返回
【此时不确定出入参数数量，先写两个参数】

```javascript
function sumAll(a,b){
    var result = 0;
    for (var i = 0; i < arguments.length; i++) {
        if (typeof(arguments[i] == "number")){//有传入非数值型数据，排除在外，不予计算
            result += arguments[i];
        }
    }
    return result;
}

alert(sumAll(1,2,3,4,5,6,7,8));
alert(sumAll(1));
```



### 6、JavaScript中的自定义对象

#### 一、Object形式的自定义对象

- **对象的定义：**

```javascript
var 变量名 = new Object();  //对象实例（空对象）
变量名.属性名 = 值;		   //定义一个属性
变量名.函数名 = function(){}  //定义一个函数
```

- **对象的访问：**

```javascript
变量名.属性/函数名();
```



```javascript
<script type="text/javascript">
    
    var obj = new Object();
    obj.name = "张无忌";
    obj.age = 99;
    obj.user = function (){
        alert("姓名：" + this.name + ",年龄：" + this.age);
    }
	
	//属性/函数调用
    alert(obj.name);//张无忌
    alert(obj.age);//99
    obj.user();//姓名：张无忌,年龄：99
</script>
```



#### 二、{}花括号形式的自定义对象

- **对象的定义：**【最后面要有分号，中间用逗号隔开】

```javascript
var 变量名 = {};//空对象

var 变量名 = {
    属性名1：值1,		//定义一个属性
    属性名2：值2,		//定义一个属性
    函数名3：function(){}  //定义一个函数
    //中间用逗号隔开，最后一个不要加逗号
};
```

**注意：**

- 属性名和值之间用分号！！！！不是等号

- 中间用逗号隔开，最后一个属性或函数不加逗号

- 花括号结尾要有分号

	

```javascript
<script type="text/javascript">
    // 方式一
    // var obj = new Object();
    // obj.name = "张无忌";
    // obj.age = 99;
    // obj.user = function (){
    //     alert("姓名：" + this.name + ",年龄：" + this.age);
    // }
    // 方式二
    var obj = {
        name:"张无忌",
        age:99,
        user:function (){
            alert("姓名：" + this.name + ",年龄：" + this.age);
        }
    };

    alert(obj.name);//张无忌
    alert(obj.age);//99
    obj.user();//姓名：张无忌,年龄：99
</script>
```



### 7、JavaScript中的事件

**事件：**是电脑输入设备与页面进行交互的响应，称之为事件

#### 事件的注册：

**事件的注册（绑定）：**就是告诉浏览器，当事件响应后要执行哪些操作代码；

##### 一、静态注册

通过html标签的时间属性直接赋予事件响应后的代码。这种方式叫静态注册

##### 二、动态注册

是指先通过JavaScript代码得到标签的DOM对象，然后再通过

```html
DOM对象名.事件名 = function(){}
```

这种形式赋予事件响应后的代码，叫做动态注册。



#### 常用的事件：

- **onload 加载完成事件：**页面加载完成之后，常用语做页面JavaScript代码初始化操作

	- 静态方式一【直接写】

		```html
		<body onload="alert('我是静态注册的onload');">
		```

	- 静态方式二【调用方法】

		```html
		<!--静态注册onload事件-->
		    <script type="text/javascript">
		        //创建一个onload事件的方法
		        function onloadFun(){
		            alert('我是动态注册的onload');
		        }
		    </script>
		
		<body onload="onloadFun()">
		```

	- 动态方法

		```html
		<script type="text/javascript">
		    
			// 动态注册
		    window.onload = function (){
		        alert('我是动态注册的onload');
		    }
		</script>
		```

- **onclick 单击事件：**常用于按钮的点击响应操作

	- 静态方法【调用方法】

		```html
		<head>
		    <meta charset="UTF-8">
		    <title>Title</title>
		    <script type="text/javascript">
		        //创建一个onclick事件的方法
		        function onclickFun(){
		            alert('我是静态注册的onclick');
		        }
		
		    </script>
		</head>
		
		<body>
		    <!--静态注册onload事件-->
			<button onclick="onclickFun()">按钮1【静态注册】</button>
		</body>
		</html>
		```

	- 动态方法

		```html
		<head>
		    <meta charset="UTF-8">
		    <title>Title</title>
		    <script type="text/javascript">
		    //    动态注册
		        window.onload = function (){
		            //1、获取标签对象
		            /**
		             * document:表示当前整个html页面
		             * getElementById，通过id获取标签对象
		             */
		            var btnObj = document.getElementById("but1");
		            
		            //2、通过标签对象.事件名=function(){}
		            btnObj.onclick=function (){
		                alert('我是动态注册的onclick');
		            }
		        }
		    </script>
		</head>
		<body>
		    <button id="but1">按钮2【动态注册】</button>
		</body>
		```

- **onblur 失去焦点事件：**常用于输入框失去焦点后验证其输入内容是否合法

	![image-20211031083359157](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211030092008032-163555680918920.png)

	- 静态注册

		```html
		    <script type="text/javascript">
		        //静态注册
		        function onblurFun(){
		            // console 是控制台对象，有JavaScript提供，专门用来向浏览器的控制台打印输出，用于测试使用
		            // log() 是打印方法
		            console.log("静态注册失去焦点事件！");
		        }
		        
		    </script>
		
		</head>
		<body>
		    用户名：<input type="text" onblur="onblurFun()"><br/>
		    密码：<input type="text" id="password"><br/>
		
		</body>
		</html>
		```

	- 动态注册

		```html
		    <script type="text/javascript">
		
		        //动态注册
		        window.onload = function (){//这里就是onload，没错
		            //1、获取标签对象
		            var passwordObj = document.getElementById("password");
		            //2、通过标签对象.事件名=function(){};展示事件
		            passwordObj.onblur=function (){
		                console.log("动态注册失去焦点事件！");
		            }
		        }
		    </script>
		</head>
		<body>
		    用户名：<input type="text" onblur="onblurFun()"><br/>
		    密码：<input type="text" id="password"><br/>
		
		</body>
		</html>
		```

- **onchange 内容发生改变事件：**常用于下拉列表和输入框内容发生改变后操作

	- 静态注册

		```html
		<script type="text/javascript">
		    //静态注册
		    function onchangeFun(){
		        alert("静态onchange事件")
		    }
		</script>
		<body>
		    <select onchange="onchangeFun()">
		        <option>--武当派--</option>
		        <option>张三丰</option>
		        <option>张翠山</option>
		        <option>殷六侠</option>
		    </select>
		</body>
		```

	- 动态注册

		```html
		<script type="text/javascript">
		    //动态注册
		    window.onload=function (){
		        //1、获取标签对象
		        //2、通过标签对象.事件名=function(){};
		        var onchangeObj = document.getElementById("mingjiao");
		        onchangeObj.onchange=function (){
		            alert("六大派决战光明顶")
		        }
		    }
		
		</script>
		<body>
		    <select id="mingjiao">
		        <option>武当派</option>
		        <option>张三丰</option>
		        <option>张翠山</option>
		        <option>殷六侠</option>
		    </select>
		</body>
		```

- **onsubmit 表单提交事件：**常用于表单提交前，验证所有表单项是否合法

	- 静态注册

		```html
		<script type="text/javascript">
		    //静态注册
		    function onsubmitFun(){
		        alert("静态注册表单提交事务---发现不合法的了，要禁止提交");
		        return false;
		    }
		   
		</script>
		
		<body>
		    <!--return false 可以阻止 表单的提交-->
		    <form action="http://www.baidu.com" method="get" onsubmit="return onsubmitFun()">
		        <input type="submit" value="静态注册"/>
		    </form>
		</body>
		```

	- 动态注册

		```html
		<script type="text/javascript">
		    //动态注册
		    window.onload=function (){
		        //1、获取标签对象
		        //2、通过标签对象.事件名=function(){}
		        var onsubObj = document.getElementById("onsub");
		        onsubObj.onsubmit=function (){
		            alert("静态注册表单提交事务---发现不合法的了，要禁止提交");
		            return false;//true就是不阻止
		        }
		    }
		</script>
		
		<body>
		    <!--return false 可以阻止 表单的提交-->
		    <form action="http://www.baidu.com" id="onsub">
		        <input type="submit" value="动态注册"/>
		    </form>
		</body>
		```

### 8、正则表达式

#### 8.1 、语法

- pattern：描述了表达式的模式
- modifiers：用于指定全局匹配，区分大小写的匹配和多行匹配

```javascript
var patt = new RegExp(pattern,modifiers);
或者
var patt = /pattern/modifiers;
```

```javascript
<script type="text/javascript">
        //两种声明方式
        var patt = new RegExp("e");
        var patt1 = /e/;
        //是否包含最少3个连续的a，最多5个。【实际最多5个不起作用】
        var patt2 = /a{3,5}/;
        //是否包含最少3个连续的a，最多5个。【此时^表示开头，$表示结尾,此表达式表示从头到尾检查，有一个不匹配都不行】
        var patt3 = /^a{3,5}$/;

        var str = "aaaaaaabcd";
        // test：判断是否
        alert(patt2.test(str));
    </script>
```

#### 8.2 、修饰符

| 修饰符                   | 描述                                                     |
| ------------------------ | -------------------------------------------------------- |
| [i](jsref_regexp_i.html) | 执行对大小写不敏感的匹配。                               |
| [g](jsref_regexp_g.html) | 执行全局匹配（查找所有匹配而非在找到第一个匹配后停止）。 |
| m                        | 执行多行匹配。                                           |

#### 8.3 、方括号

方括号用于查找某个范围内的字符：

| 表达式                                   | 描述                               |
| ---------------------------------------- | ---------------------------------- |
| [[abc\]](jsref_regexp_charset.html)      | 查找方括号之间的任何字符。         |
| [[^abc\]](jsref_regexp_charset_not.html) | 查找任何不在方括号之间的字符。     |
| [0-9]                                    | 查找任何从 0 至 9 的数字。         |
| [a-z]                                    | 查找任何从小写 a 到小写 z 的字符。 |
| [A-Z]                                    | 查找任何从大写 A 到大写 Z 的字符。 |
| [A-z]                                    | 查找任何从大写 A 到小写 z 的字符。 |
| [adgk]                                   | 查找给定集合内的任何字符。         |
| [^adgk]                                  | 查找给定集合外的任何字符。         |
| (red\|blue\|green)                       | 查找任何指定的选项。               |

#### 8.4 、元字符

元字符（Metacharacter）是拥有特殊含义的字符：

| 元字符                                  | 描述                                        |
| --------------------------------------- | ------------------------------------------- |
| [.](jsref_regexp_dot.html)              | 查找单个字符，除了换行和行结束符。          |
| [\w](jsref_regexp_wordchar.html)        | 查找单词字符。                              |
| [\W](jsref_regexp_wordchar_non.html)    | 查找非单词字符。                            |
| [\d](jsref_regexp_digit.html)           | 查找数字。                                  |
| [\D](jsref_regexp_digit_non.html)       | 查找非数字字符。                            |
| [\s](jsref_regexp_whitespace.html)      | 查找空白字符。                              |
| [\S](jsref_regexp_whitespace_non.html)  | 查找非空白字符。                            |
| [\b](jsref_regexp_begin.html)           | 匹配单词边界。                              |
| [\B](jsref_regexp_begin_not.html)       | 匹配非单词边界。                            |
| \0                                      | 查找 NUL 字符。                             |
| [\n](jsref_regexp_newline.html)         | 查找换行符。                                |
| \f                                      | 查找换页符。                                |
| \r                                      | 查找回车符。                                |
| \t                                      | 查找制表符。                                |
| \v                                      | 查找垂直制表符。                            |
| [\xxx](jsref_regexp_octal.html)         | 查找以八进制数 xxx 规定的字符。             |
| [\xdd](jsref_regexp_hex.html)           | 查找以十六进制数 dd 规定的字符。            |
| [\uxxxx](jsref_regexp_unicode_hex.html) | 查找以十六进制数 xxxx 规定的 Unicode 字符。 |

#### 8.5 、量词

| 量词                                 | 描述                                        |
| ------------------------------------ | ------------------------------------------- |
| [n+](jsref_regexp_onemore.html)      | 匹配任何包含至少一个 n 的字符串。           |
| [n*](jsref_regexp_zeromore.html)     | 匹配任何包含零个或多个 n 的字符串。         |
| [n?](jsref_regexp_zeroone.html)      | 匹配任何包含零个或一个 n 的字符串。         |
| [n{X}](jsref_regexp_nx.html)         | 匹配包含 X 个 n 的序列的字符串。            |
| [n{X,Y}](jsref_regexp_nxy.html)      | 匹配包含 X 至 Y 个 n 的序列的字符串。       |
| [n{X,}](jsref_regexp_nxcomma.html)   | 匹配包含至少 X 个 n 的序列的字符串。        |
| [n$](jsref_regexp_ndollar.html)      | 匹配任何结尾为 n 的字符串。                 |
| [^n](jsref_regexp_ncaret.html)       | 匹配任何开头为 n 的字符串。                 |
| [?=n](jsref_regexp_nfollow.html)     | 匹配任何其后紧接指定字符串 n 的字符串。     |
| [?!n](jsref_regexp_nfollow_not.html) | 匹配任何其后没有紧接指定字符串 n 的字符串。 |

#### 8.6 、RegExp 对象属性

| 属性                                       | 描述                                     | FF   | IE   |
| ------------------------------------------ | ---------------------------------------- | ---- | ---- |
| [global](jsref_regexp_global.html)         | RegExp 对象是否具有标志 g。              | 1    | 4    |
| [ignoreCase](jsref_regexp_ignorecase.html) | RegExp 对象是否具有标志 i。              | 1    | 4    |
| [lastIndex](jsref_lastindex_regexp.html)   | 一个整数，标示开始下一次匹配的字符位置。 | 1    | 4    |
| [multiline](jsref_multiline_regexp.html)   | RegExp 对象是否具有标志 m。              | 1    | 4    |
| [source](jsref_source_regexp.html)         | 正则表达式的源文本。                     | 1    | 4    |

#### 8.7 、RegExp 对象方法

| 方法                                 | 描述                                               | FF   | IE   |
| ------------------------------------ | -------------------------------------------------- | ---- | ---- |
| [compile](jsref_regexp_compile.html) | 编译正则表达式。                                   | 1    | 4    |
| [exec](jsref_exec_regexp.html)       | 检索字符串中指定的值。返回找到的值，并确定其位置。 | 1    | 4    |
| [test](jsref_test_regexp.html)       | 检索字符串中指定的值。返回 true 或 false。         | 1    | 4    |

#### 8.8 、支持正则表达式的 String 对象的方法

| 方法                          | 描述                             | FF   | IE   |
| ----------------------------- | -------------------------------- | ---- | ---- |
| [search](jsref_search.html)   | 检索与正则表达式相匹配的值。     | 1    | 4    |
| [match](jsref_match.html)     | 找到一个或多个正则表达式的匹配。 | 1    | 4    |
| [replace](jsref_replace.html) | 替换与正则表达式匹配的子串。     | 1    | 4    |
| [split](jsref_split.html)     | 把字符串分割为字符串数组。       | 1    | 4    |









### 9、DOM模型

#### 9.1     DOM标准

​    Document Object Model：文档对象模型 定义了访问和处理 HTML 文档的标准方法。是W3C国际组织制定的统一标准，在很多计算机语言中都有不同实现如C#、PHP、 Java、Ruby、perl、python等

#### 9.2     document对象

​          window对象的一个属性，代表当前HTML文档，包含了整个文档的树形结构。获取document对象的本质方法是：<font color='red'>window.document，而“window.”可以省略。</font>

#### 9.3     DOM树

![image-20211031173220225](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211031182116042-16356756770482.png)

- **父元素：**直接包含当前元素的元素就是当前元素的父元素

- **子元素：**当前元素直接包含的元素就是当前元素的子元素

- **祖先元素：**直接或间接包含当前元素的所有元素都是当前元素的祖先元素

- **后代元素：**当前元素直接或间接包含的元素就是当前元素的后代元素

- **兄弟元素：**有相同父元素的元素是兄弟元素

#### 9.4   Document 对象中常用的方法介绍

![image-20211031182116042](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211101073607280-16357233684911.png)

- **getElementById(): 根据id值，查找并返回一个具体的标签对象**
	- 需求，当前用户单击校验按钮，获取输入框中的内容，然后验证其是否合法
	     * 验证规则：必须由数字字母下划线组成，长度是5-12位
	     * ![image-20211101073607280](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211031083359157-163564044198528.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript">
        /**
         * 需求，当前用户单击校验按钮，获取输入框中的内容，然后验证其是否合法
         * 验证规则：必须由数字字母下划线组成，长度是5-12位
         *
         */
        function onclickFun(){
            var usenameObj = document.getElementById("username");
            var value = usenameObj.value;
            var patt = /^\w{5,12}$/;//正则：由数字字母下划线组成，长度是5-12位
            var spanIdObj = document.getElementById("usenameSpan");
            if (patt.test(value)){//test方法，就是判断是否符合该正则表达式，符合返回true，不符合返回false
                //一、用文字表示不合法
                // spanIdObj.innerHTML = "输入名称合法";
                //二、用小对号，或者小×来表示合法与否【此处用两张随意图片代替对勾和叉】
                spanIdObj.innerHTML = "<img src=\"IMG_2911.JPG\" width=\"20\" height=\"20\">";
            }else{
                // spanIdObj.innerHTML = "输入名称不合法";
                spanIdObj.innerHTML = "<img src=\"段誉.jpeg\" width=\"20\" height=\"20\">";
            }
        }
    </script>
</head>
<body>
    用户名：<input type="text" id="username" value="zym"/>
    <span id="usenameSpan" style="color: red;"></span>
    <button onclick="onclickFun()">校验</button>
</body>
</html>
```

- **getElementsByName():返回指定name属性查询查询，返回多个标签对象的集合**
	- 需求：复选框，通过点击事件，实现【全选】、【全不选】、【反选】操作
	- ![image-20211101080233141](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211101085928057-16357283693564.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript">
        //全选
        function allSel(){
            /**
             * document.getElementsByName("hobby");返回指定name属性查询查询，返回多个标签对象的集合
             * 集合中每个元素都是一个DOM对象
             * 这个集合中元素的顺序，就是他们在html页面中，【从上到下】的顺序
             */
            var hobbies = document.getElementsByName("hobby");
            for (var hobby of hobbies) {
                hobby.checked=true;
            }
        }
        //全不选
        function nothSel(){
            var hobbies = document.getElementsByName("hobby");
            for (var hobby of hobbies) {
                hobby.checked=false;
            }
        }
        //反选
        function inverSel(){
            var hobbies = document.getElementsByName("hobby");
            for (var hobby of hobbies) {
                hobby.checked=!hobby.checked;//取反
            }
        }
    </script>
</head>
<body>
    兴趣爱好：
    <input type="checkbox" name="hobby" value="c++">C++
    <input type="checkbox" name="hobby" value="java">Java
    <input type="checkbox" name="hobby" value="python">Python<br/>
    <!--方法调用要加括号啊，亲！！！！！！方法名()    -->
    <button onclick="allSel()">全选</button>
    <button onclick="inverSel()">反选</button>
    <button onclick="nothSel()">全不选</button>
</body>
</html>
```



- **getElementsByTagName(): 按照指定标签名进行查询，并返回集合**

	- 需求：没有name属性时，通过标签名实现全选、反选、全不选操作

	```html
	<!DOCTYPE html>
	<html lang="en">
	<head>
	    <meta charset="UTF-8">
	    <title>Title</title>
	    <script type="text/javascript">
	        /**
	         * document.getElementsByName("hobby");通过指定标签名查询，返回多个标签对象的集合
	         * 集合中每个元素都是一个DOM对象
	         * 这个集合中元素的顺序，就是他们在html页面中，【从上到下】的顺序
	         */
	        var hobbies = document.getElementsByTagName("input");
	        //全选
	        function allSel(){
	            for (var hobby of hobbies) {
	                hobby.checked=true;
	            }
	        }
	        //全不选getElementByNameTest.html
	        function nothSel(){
	            for (var hobby of hobbies) {
	                hobby.checked=false;
	            }
	        }
	        //反选
	        function inverSel(){
	            for (var hobby of hobbies) {
	                hobby.checked=!hobby.checked;//取反
	            }
	        }
	    </script>
	</head>
	<body>
	    兴趣爱好：
	    <input type="checkbox" value="c++">C++
	    <input type="checkbox" value="java">Java
	    <input type="checkbox" value="python">Python<br/>
	    <!--方法调用要加括号啊，亲！！！！！！方法名()    -->
	    <button onclick="allSel()">全选</button>
	    <button onclick="inverSel()">反选</button>
	    <button onclick="nothSel()">全不选</button>
	</body>
	</html>
	```

#### 9.5  节点（Node）

- 1、HTML文档中的每个成分都是一个节点，HTML文档是由DOM节点构成的集合。

- **2、节点的分类**
	- ①<font color='red'>文档节点(Document)</font>：DOM标准将整个HTML文档的相关信息封装后得到的对象。
	- ②<font color='red'>元素节点(Element)</font>：DOM标准将HTML标签的相关信息封装后得到的对象。
	- ③<font color='red'>属性节点(Attribute)</font>：DOM标准将HTML标签属性的相关信息封装后得到的对象。
	- ④<font color='red'>文本节点(Text)</font>：DOM标准将HTML文本的相关信息封装后得到的对象。
- **3、节点的属性**
	- ① <font color='red'>nodeName</font>: 代表当前节点的名字，只读属性。如果给定节点是一个文本节点，nodeName 属性将返回内容为 #text 的字符串。
	- ② <font color='red'>nodeType</font>：返回一个整数, 这个数值代表着给定节点的类型，只读属性。
		-  1 -- 元素节点   
		-  2 -- 属性节点  
		-  3 -- 文本节点
	- ③<font color='red'> nodeValue</font>：返回给定节点的当前值(字符串)，可读写的属性。
		- 元素节点, 返回值是 null
		- 属性节点: 返回值是这个属性的值
		- 文本节点: 返回值是这个文本节点的内容

![image-20211101081926605](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211101090348276-16357286297565.png)

#### 9.6  DOM查询大练习

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>dom查询</title>
<link rel="stylesheet" type="text/css" href="style/css.css" />
<script type="text/javascript">
	window.onload = function(){
		//1.查找#bj节点
		document.getElementById("btn01").onclick=function (){
			alert(document.getElementById("bj").innerHTML);
		}
		//2.查找所有li节点
		var btn02Ele = document.getElementById("btn02");
		btn02Ele.onclick = function(){
			var lis = document.getElementsByTagName("li");
			for (var li of lis) {
				alert(li.innerHTML);
			}
		};
		//3.查找name=gender的所有节点
		var btn03Ele = document.getElementById("btn03");
		btn03Ele.onclick = function(){
			var genders = document.getElementsByName("gender");
			for (var gender of genders) {
				alert(gender.value);
			}
		};
		//4.查找#city下所有li节点
		var btn04Ele = document.getElementById("btn04");
		btn04Ele.onclick = function(){
			var city = document.getElementById("city");
			var cityLis = city.getElementsByTagName("li");
			for (var cityLi of cityLis) {
				alert(cityLi.innerHTML);
			}
		};
		//5.返回#city的所有子节点
		var btn05Ele = document.getElementById("btn05");
		btn05Ele.onclick = function(){
			var city = document.getElementById("city");
			var cityLis = city.childNodes;
			for (var cityLi of cityLis) {
				alert(cityLi.innerHTML);//li标签左右的空白字符也算一个对象，所以除了北京上海等，还有5个空白字符
			}
		};
		//6.返回#phone的第一个子节点
		var btn06Ele = document.getElementById("btn06");
		btn06Ele.onclick = function(){
			var firstPhone = document.getElementById("phone").firstChild;
			alert(firstPhone.innerHTML);
		};
		//7.返回#bj的父节点
		var btn07Ele = document.getElementById("btn07");
		btn07Ele.onclick = function(){
			var parentBj = document.getElementById("bj").parentNode;
			alert(parentBj.id);
		};
		//8.返回#android的前一个兄弟节点
		var btn08Ele = document.getElementById("btn08");
		btn08Ele.onclick = function(){
			var previousSib = document.getElementById("android").previousSibling;
			alert(previousSib.innerHTML)
		};
		//9.读取#username的value属性值
		var btn09Ele = document.getElementById("btn09");
		btn09Ele.onclick = function(){
			alert(document.getElementById("username").value);
		};
		//10.设置#username的value属性值
		var btn10Ele = document.getElementById("btn10");
		btn10Ele.onclick = function(){
			var useObj = document.getElementById("username");
			useObj.value = "12345";
		};
		//11.返回#city的文本值
		var btn11Ele = document.getElementById("btn11");
		btn11Ele.onclick = function(){
			var bjObj = document.getElementById("city");
			alert(bjObj.innerHTML);//获取/设置起始标签和结束标签中的内容
			alert(bjObj.innerText);//获取/设置起始标签和结束标签中的文本
		};
	};
</script>
</head>
<body>
<div id="total">
	<div class="inner">
		<p>
			你喜欢哪个城市?
		</p>

		<ul id="city">
			<li id="bj">北京</li>
			<li>上海</li>
			<li>东京</li>
			<li>首尔</li>
		</ul>

		<br>
		<br>

		<p>
			你喜欢哪款单机游戏?
		</p>

		<ul id="game">
			<li id="rl">红警</li>
			<li>实况</li>
			<li>极品飞车</li>
			<li>魔兽</li>
		</ul>

		<br />
		<br />

		<p>
			你手机的操作系统是?
		</p>

		<ul id="phone"><li>IOS</li><li id="android">Android</li><li>Windows Phone</li></ul>
	</div>

	<div class="inner">
		gender:
		<input type="radio" name="gender" value="male"/>
		Male
		<input type="radio" name="gender" value="female"/>
		Female
		<br>
		<br>
		name:
		<input type="text" name="name" id="username" value="abcde"/>
	</div>
</div>
<div id="btnList">
	<div><button id="btn01">查找#bj节点</button></div>
	<div><button id="btn02">查找所有li节点</button></div>
	<div><button id="btn03">查找name=gender的所有节点</button></div>
	<div><button id="btn04">查找#city下所有li节点</button></div>
	<div><button id="btn05">返回#city的所有子节点</button></div>
	<div><button id="btn06">返回#phone的第一个子节点</button></div>
	<div><button id="btn07">返回#bj的父节点</button></div>
	<div><button id="btn08">返回#android的前一个兄弟节点</button></div>
	<div><button id="btn09">返回#username的value属性值</button></div>
	<div><button id="btn10">设置#username的value属性值</button></div>
	<div><button id="btn11">返回#city的文本值</button></div>
</div>
</body>
</html>
```

![image-20211101085928057](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211101090419716-16357286610116.png)





#### 9.7  DOM增删改API【通过JavaScript代码创建html内容】

| **API**                                  | **功能**                                   |
| ---------------------------------------- | ------------------------------------------ |
| document.createElement(“标签名”)         | 创建元素节点并返回，但不会自动添加到文档中 |
| document.createTextNode(“文本值”)        | 创建文本节点并返回，但不会自动添加到文档中 |
|                                          |                                            |
| element.appendChild(ele)                 | 将ele添加到element所有子节点后面           |
| parentEle.insertBefore(newEle,targetEle) | 将newEle插入到targetEle前面                |
|                                          |                                            |
| parentEle.replaceChild(newEle, oldEle)   | 用新节点替换原有的旧子节点                 |
| parentEle.removeChild(childNode)         | 删除指定的子节点                           |
|                                          |                                            |
| element.innerHTML                        | 读写标签起始中的所有内容                   |
| element.innerText                        | 读写标签起始中的文本                       |

**对比   innerHTML  和   innerText**

```javascript
//11.返回#city的文本值
var btn11Ele = document.getElementById("btn11");
btn11Ele.onclick = function(){
   var bjObj = document.getElementById("city");
   alert(bjObj.innerHTML);//获取/设置起始标签和结束标签中的内容
   alert(bjObj.innerText);//获取/设置起始标签和结束标签中的文本
};
```

- **innerHTML：**

![image-20211101090348276](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211101091346569-16357292275447.png)

- **innerText：**

![image-20211101090419716](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211101080233141-16357249543462.png)



在一个空白表中，通过JavaScript代码创建div标签，并显示<div>张三丰爱郭襄一百年</div>

![image-20211101091346569](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211101180331189-16357610124548.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript">
        //此处需要用window.onload，确保在网页加载完毕后运行
        //否则按顺序执行，在添加body操作时，body还不存在，会报错
        window.onload=function (){
            //1、创建标签对象
            var divObj = document.createElement("div");
            
            
            //2、添加标签内容【方式一:直接添加】
            divObj.innerHTML = "张三丰爱了郭襄一百年";
            //【方式二：将文本封装成一个对象，然后添加该对象】
            var textObj = document.createTextNode("张三丰爱了郭襄一百年");
            divObj.appendChild(textObj);
            
            //此时虽然实现<div>张三丰爱郭襄一百年</div>，但还是在内存中
            
            
            //3、添加到body对象中，作为body的子元素
            document.body.appendChild(divObj);
            //此处没有用getElementByName()，因为body太常用了，官方直接给了个body属性，
            //就是等价于getElementByName("body")

        }
    </script>
</head>
<body>

</body>
</html>
```



## 第4章 jQuery

### 1、jQuery 介绍

- 什么是jQuery？
	- 就是JavaScript和Query（查询），他就是辅助JavaScript开发的js类库
- jQuery核心思想
	- write less ，do more （写得更少，做的更多），所以它实现了很多浏览器的兼容问题

### 2、jQuery 的初体验

- 为按钮添加click事件

	```html
	<!DOCTYPE html>
	<html>
	<head>
	   <meta charset="UTF-8">
	   <title>HellojQuery</title>
	   <script type="text/javascript" src="../script/jquery-1.7.2.js"></script>
	   <script type="text/javascript">
	      // window.onload = function (){
	      //     var butObj = document.getElementById("btnId");
	      //     butObj.onclick = function (){
	      //        alert("这里JavaScript是原生的单击事件");
	      //     }
	      // }
	      $(function (){ // 表示页面加载完成之后，相当于window.onload = function(){}
	         var $btnObj = $("#btnId");// 表示按id查询标签对象
	         $btnObj.click(function (){
	            alert("这里是jQuery的单击事件");
	         })
	      })
	   </script>
	
	</head>
	<body>
	   <button id="btnId">SayHello</button>
	</body>
	</html>
	```

- 常见问题：

	- jQuery使用一定要先引入jQuery库

		```javascript
		<script type="text/javascript" src="../script/jquery-1.7.2.js"></script>
		//另起一行，单独写一个<script>   </script>
		```

	- $ 其实是一个函数

	- 添加按钮响应事件步骤

		- 1、使用jQuery查询到标签对象

		- 2、使用标签对象.click（function（）{}）；

			```javascript
			$(function (){ // 表示页面加载完成之后，相当于window.onload = function(){}
				var $btnObj = $("#btnId");// 表示按id查询标签对象
				$btnObj.click(function (){
				alert("这里是jQuery的单击事件");
				})
			})
			```

			

### 3、jQuery 核心函数

$ 是jQuery的核心函数，能完成jQuery的很多功能。$()就是调用$这个函数

#### 1、传入参数为（函数）时

表示页面加载完成之后，运行该函数！相当于window.onload = function(){};

```javascript
$(function (){
   alert("页面加载完成之后，自动调用");
})
```

#### 2、传入参数为（HTML字符串）时

直接创建HTML字符串标签对象

![image-20211101180331189](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211101231731749-163577985306810.png)

```javascript
$(function (){
   alert("页面加载完成之后，自动调用");
   $("<ul id=\"city\">\n" +
         "\t\t<li id=\"bj\">北京</li>\n" +
         "\t\t<li>上海</li>\n" +
         "\t\t<li>东京</li>\n" +
         "\t\t<li>首尔</li>\n" +
         "\t</ul>").appendTo("body");
    //直接创建，在body对象内部
})
```

#### 3、传入参数为（选择器字符串）时

$("#id属性值")；id选择器，根据id查询标签对象

$("标签名");  标签名选择器，根据指定的标签名查询标签对象

$(".class属性值");  类型选择器，根据指定的class属性查询标签对象

```javascript
var $btnObj = $("#btnId");// 表示按id查询标签对象
//该返回数组时，仍会返回数组，直接按数组处理即可
```

#### 4、传入参数为（DOM对象）时

会把DOM对象转换为jQuery对象

```javascript
var butObj = document.getElementById("btnId");//DOM对象
var $jQueryObj = $(butObj);//jQuery对象
```



### 4、jQuery 对象和DOM 对象区分

#### 4.1、jQuery对象

- 通过 getElementBy**()查询出来的标签对象，是DOM对象
- 通过createElement()方法创建的对象，是DOM对象
- DOM对象Alert 出来的效果是：[object HTMLXxxxxxxxElement]

#### 4.2、DOM对象

- 通过jQuery 提供API创建的对象，是jQuery对象
- 通过jQuery 包装的DOM对象，是jQuery对象
- 通过jQuery提供的API查询到的对象，是jQuery对象
- jQuery对象Alert 出来的效果是：[object Object]

#### 4.3、jQuery对象的本质

<font color='red'>**jQuery 对象是 DOM 对象的数组 ＋ jQuery 提供的一些列功能函数**</font>

#### 4.4、jQuery 对象和 Dom 对象的使用区别

jQuery对象不能使用DOM对象的属性和方法

DOM对象也不能使用jQuery对象的属性和方法

#### 4.5、DOM对象和jQuery对象相互转换

- **<font color='red'>DOM 对象转化为jQuery对象</font>**

	- $(DOM对象)       就可以转换成jQuery对象

		```javascript
		var butObj = document.getElementById("btnId");//DOM对象
		var $jQueryObj = $(butObj);//jQuery对象
		```

		

- **<font color='red'>jQuery 对象转化为 DOM 对象</font>**

	- jQuery 对象[下标]，取出相应的DOM对象【jQuery对象时DOM对象的集合，当数组取出来就是DOM对象了】

		```javascript
		var $btnObj = $("#btnId");// 表示按id查询标签获得jQuery对象
		var domObj = $btnObj[0];//DOM对象
		```

		

### 5、jQuery 选择器

- jQuery最牛的地方就是其强大的选择器, 使用其选择器基本可以快速轻松的找到页面的任意节点

- jquery的选择器分类
	- 基本选择器
	- 层次选择器
	- 过滤选择器
		- 基本
		- 内容
		- 可见
		- 属性
		- 子元素
		- 表单
		- 表单属性

#### 1). 基本选择器

- l  基本选择器是jquery中最简单，也是最常用的选择器

- l  它通过标签名,id属性,class属性来查找匹配的DOM元素

##### 1.1)  id选择器  

- l  用法:$(‘#id’)
- l  返回值：根据id属性匹配一个标签, 封装成jQuery对象

##### 1.2)  标签选择器

- l  用法:  $(‘tagName’)
- l  返回值：根据标签名匹配的一个或多个标签, 封装成jQuery对象

##### 1.3)  class选择器

- l  用法:  $(‘.class’)
- l  返回值：根据class属性值匹配一个或多个标签, 封装成jQuery对象

##### 1.4)  *选择器

- l  用法:  $(*) 
- l  返回值: 匹配所有标签, 封装成jQuery对象

##### 1.5)  selector1,selector2,…

- l  用法:  $(”div,span,.myClass”)  
- l  返回值: 所有匹配选择器的标签, 封装成jQuery对象

![image-20211101231731749](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211101231629648-16357797924309.png)

```javascript
<script type="text/javascript">
   $(function(){
      //1.选择 id 为 one 的元素
      $("#btn1").click(function (){
         $("#one").css("background-color","#bbffaa");
      })
      //2.选择 class 为 mini 的所有元素
      $("#btn2").click(function(){
         $(".mini").css("background-color","#bbffaa");
      });

      //3.选择 元素名是 div 的所有元素
      $("#btn3").click(function(){
         $("div").css("background-color","#bbffaa");
      });

      //4.选择所有的元素
      $("#btn4").click(function(){
         $("*").css("background-color","#bbffaa");
      });

      //5.选择所有的 span 元素和id为two的元素
      $("#btn5").click(function(){
         $("span,#two").css("background-color","#bbffaa");
      });
   });
</script>
```

#### 2). 层次选择器

- l  如果想通过DOM元素之间的层次关系来获取特定元素。例如子元素、兄弟元素等。则需要通过层次选择器。

##### 2.1). ancestor descendant

- l  用法:$(”form input”)
- l  说明:在给定的祖先元素下匹配所有后代元素

##### 2.2)  parent > child

- l  用法: $(”form > input”) 
- l  说明: 在指定父元素下匹配所有子元素.注意:要区分好后代元素与子元素

##### 2.3)  prev + next

- l  用法: $(”label + input”) 
- l  说明: 匹配所有紧接在prev元素后的next元素

##### 2.4)  prev ~ siblings

- l  用法: $(”form ~ input”) 
- l  说明: 匹配prev元素之后的所有 siblings元素, 不包含该元素在内,并且siblings匹配的是和prev同辈的元素,其后辈元素不被匹配.

![image-20211101231629648](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211102125717733-16358290395421.png)

```javascript
<script type="text/javascript">
   $(function(){
      //1.选择 body 内的所有 div 元素
      $("#btn1").click(function(){
         $("body div").css("background", "#bbffaa");
      });

      //2.在 body 内, 选择div子元素
      $("#btn2").click(function(){
         $("body > div").css("background", "#bbffaa");
      });

      //3.选择 id 为 one 的下一个 div 元素
      $("#btn3").click(function(){
         $("#one + div").css("background", "#bbffaa");
      });

      //4.选择 id 为 two 的元素后面的所有 div 兄弟元素
      $("#btn4").click(function(){
         $("#two ~ div").css("background", "#bbffaa");
      });
   });
</script>
```

#### 3). 基本过滤选择器

- l  **过滤选择器主要是通过特定的过滤规则来筛选出所需的DOM元素**, 该选择器都以 “<font color='red'>**:**</font>” 开头
- l  按照不同的过滤规则, 过滤选择器可以分为基本过滤, 内容过滤, 可见性过滤, 属性过滤, 子元素过滤, 表单过滤和表单属性过滤选择器.

##### 3.1). :first

- l  用法: $(”tr:first”) ;  
- l  说明: 匹配找到的第一个元素

##### 3.2). :last

- l  用法: $(”tr:last”) 
- l  说明: 匹配找到的最后一个元素.与 :first 相对应

##### 3.3). :not(selector)

- l  用法: $(”input:not(:checked)”)
- l  说明: 去除所有与给定选择器匹配的元素.有点类似于”非”,意思是没有被选中的input(当input的type=”checkbox”).

##### 3.4). :even

- l  用法: $(”tr:even”)  
- l  说明: 匹配所有索引值为偶数的元素，从0开始计数.js的数组都是从0开始计数的.

##### 3.5). :odd

- l  用法: $(”tr:odd”) 
- l  说明: 匹配所有索引值为奇数的元素,和:even对应,从 0 开始计数.

##### 3.6). :eq(index)

- l  用法: $(”tr:eq(0)”)  
- l  说明: 匹配一个给定索引值的元素.eq(0)就是获取第一个tr元素.括号里面的是索引值,不是元素排列数.

##### 3.7). :gt(index)

- l  用法: $(”tr:gt(0)”) 
- l  说明: 匹配所有大于给定索引值的元素.

##### 3.8). :lt(index)

- l  用法: $(”tr:lt(2)”)  
- l  说明: 匹配所有小于给定索引值的元素.





#### 4). 内容过滤选择器

- l  内容过滤选择器的过滤规则主要体现在它所包含的子元素和文本内容上

##### 4.1).  :contains(text)

- l  用法: $(”div:contains(’John’)”) 
- l  说明: 匹配包含给定文本的元素.这个选择器比较有用，当我们要选择的不是dom标签元素时,它就派上了用场了,它的作用是查找被标签”围”起来的文本内容是否符合指定的内容的.

##### 4.2). :empty

- l  用法: $(”td:empty”) 
- l  说明: 匹配所有不包含子元素或者文本的空元素

##### 4.3). :has(selector)

- l  用法: $(”div:has(p)”).addClass(”test”)
- l  说明: 匹配含有选择器所匹配的元素的元素.这个解释需要好好琢磨,但是一旦看了使用的例子就完全清楚了:给所有包含p元素的div标签加上class=”test”.

##### 4.4). :parent

- l  用法: $(”td:parent”) 
- l  说明: 匹配含有子元素或者文本的元素.注意:这里是”:parent”,可不是”.parent”哦!感觉与上面讲的”:empty”形成反义词. 

#### 5). 可见过滤选择器

- l  根据元素的可见和不可见状态来选择相应的元素

##### 5.1).  :hidden

- l  用法: $(”tr:hidden”) 
- l  说明: 匹配所有的不可见元素，input 元素的 type 属性为 “hidden” 的话也会被匹配到.意思是css中display:none和input type=”hidden”的都会被匹配到.同样,要在脑海中彻底分清楚冒号”:”, 点号”.”和逗号”,”的区别. 

##### 5.2). :visible

- l  用法: $(”tr:visible”) 
- l  说明: 匹配所有的可见元素.

#### 6). 属性过滤选择器

- l  属性过滤选择器的过滤规则是通过元素的属性来获取相应的元素

##### 6.1). [attribute]

- l  用法: $(”div[id]“) 
- l  说明: 匹配包含给定属性的元素. 例子中是选取了所有带id属性的div标签.

##### 6.2). [attribute=value]

- l  用法: $(”input[name='newsletter']“).attr(”checked”, true)
- l  说明: 匹配给定的属性是某个特定值的元素.例子中选取了所有name属性是newsletter的 input 元素.

##### 6.3). [attribute!=value]

- l  用法: $(”input[name!='newsletter']“).attr(”checked”, true)。  
- l  说明：匹配所有不含有指定的属性，或者属性不等于特定值的元素.此选择器等价于:not([attr=value]),要匹配含有特定属性但不等于特定值的元素,请使用[attr]:not([attr=value]).之前看到的 :not 派上了用场.

##### 6.4). [attribute^=value]

- l  用法: $(”input[name^=‘news’]“)
- l  说明: 匹配给定的属性是以某些值开始的元素.,我们又见到了这几个类似于正则匹配的符号.现在想忘都忘不掉了吧?!

##### 6.5). [attribute$=value]

- l  用法: $(”input[name$=‘letter’]“)
- l  说明: 匹配给定的属性是以某些值结尾的元素.

##### 6.6). [attribute*=value]

- l  用法: $(”input[name*=‘man’]“)
- l  说明: 匹配给定的属性是以包含某些值的元素.

#### 7). 子元素过滤选择器

##### 7.1). :nth-child(index/even/odd/equation)

- l  用法: $(”ul li:nth-child(2)”) 
- l  说明: 匹配其父元素下的第N个子或奇偶元素.这个选择器和之前说的[基础过滤](http://flex.joelove.cn/jquery-selectors-basicfilters/)[(Basic Filters)](http://flex.joelove.cn/jquery-selectors-basicfilters/)中的 eq() 有些类似,不同的地方就是前者是从0开始,后者是从1开始.

##### 7.2). :first-child

- l  用法: $(”ul li:first-child”) 
- l  说明: 匹配第一个子元素.’:first’ 只匹配一个元素,而此选择符将为每个父元素匹配一个子元素.这里需要特别的记忆一下区别.

##### 7.3). :last-child

- l  用法: $(”ul li:last-child”)
- l  说明: 匹配最后一个子元素.’:last’只匹配一个元素,而此选择符将为每个父 元素匹配一个子元素.

##### 7.4). : only-child

- l  用法: $(”ul li:only-child”)
- l  说明: 如果某个元素是父元素中唯一的子元素,那将会被匹配.如果父元素中含有其他元素,那将不会被匹配.意思就是:只有一个子元素的才会被匹配!

#### 【代码】内容、可见、属性、子元素过滤器

```javascript
<script type="text/javascript" src="../script/jquery-1.7.2.js"></script>
<script type="text/javascript">
   $(function(){
      function anmateIt(){
         $("#mover").slideToggle("slow", anmateIt);
      }
      anmateIt();
   });
   
   $(function(){
      //1.选择第一个 div 元素
      $("#btn1").click(function(){
         $("div:first").css("background", "#bbffaa");
         $("div").first.css("background", "#bbffaa");
      });
      //2.选择class不为 one 的所有 div 元素
      $("#btn2").click(function(){
         $("div:not(.one)").css("background", "#bbffaa");
         $("div").not('.one').css("background", "#bbffaa");
      });
      //3.选择索引值为等于 3 的 div 元素
      $("#btn3").click(function(){
         $("div:eq(3)").css("background", "#bbffaa");
         $("div").eq(3).css("background", "#bbffaa");
      });
      //4.选择当前正在执行动画的所有元素
      $("#btn4").click(function(){
         $(":animated").css("background", "#bbffaa");
      });
      //5.选择含有子元素的div元素
      $("#btn5").click(function(){
         $("div:parent").css("background", "#bbffaa");
      });
      //6.选择所有不可见的 div 元素
      $("#btn6").click(function(){
         $(":hidden").show("normal").css("background", "#bbffaa");
      });
      //7.选取 属性title值等于'test'的div元素
      $("#btn7").click(function() {
         $("div[title='test']").css("background", "#bbffaa");
      });
      //8.选取每个class为one的div父元素下的第一个子元素
      $("#btn8").click(function(){
         $(".one").css("background","#bbffaa");
      });
       //9.选取每个属性title值，以‘te’开始的div元素
      $("#btn9").click(function(){
         $("div[title^='te']").css("background","#bbffaa");
      });
       //10.选取每个属性title值，以‘est’结束的div元素
      $("#btn10").click(function(){
         $("div[title$='est']").css("background","#bbffaa");
      });
       //11.选取每个属性title值，含有‘es’的div元素
      $("#btn11").click(function(){
         $("div[title*='es']").css("background","#bbffaa");
      });
       //12.选取有属性id的div元素，然后在结果中 选取属性title值，含有‘es’的div元素
      $("#btn12").click(function(){
         $("div[id][title*='es']").css("background","#bbffaa");
      });
       //13.选取含有属性title值，且title值不等于test的div元素
      $("#btn13").click(function(){
         $("div[titl][title!='test']").css("background","#bbffaa");
      });
   });
</script>
```

#### 8). 表单选择器

##### 9.1). :input

- l  用法: $(”:input”)  
- l  说明:匹配所有 text, textarea, select 和 button 元素 

##### 9.2). :text

- l  用法: $(”:text”) 
- l  说明: 匹配所有的单行文本框.

##### 9.3). :password

- l  用法: $(”:password”) 
- l  说明: 匹配所有密码框.

##### 9.4). :radio

- l  用法: $(”:radio”) 
- l  说明: 匹配所有单选按钮.

##### 9.5). :checkbox

- l  用法: $(”:checkbox”) 
- l  说明: 匹配所有复选框

##### 9.6). :submit

- l  用法: $(”:submit”) 
- l  说明: 匹配所有提交按钮

##### 9.7). :image

- l  用法: $(”:image”) 
- l  说明: 匹配所有图像域.

##### 9.8). :reset

- l  用法: $(”:reset”) 
- l  说明: 匹配所有重置按钮.

#### 9.9). :button

- l  用法: $(”:button”) 
- l  说明: 匹配所有按钮.这个包括直接写的元素button.

##### 9.10). :file

- l  用法: $(”:file”) 
- l  说明: 匹配所有文件域.

##### 9.11). :hidden

- l  用法: $(”input:hidden”) 
- l  说明: 匹配所有不可见元素，或者type为hidden的元素.这个选择器就不仅限于表单了,除了匹配input中的hidden外,那些style为hidden的也会被匹配.

#### 9). 表单对象属性过滤选择器

- l  此选择器主要对所选择的表单元素进行过滤

##### 8.1). :enabled

- l  用法: $(”input:enabled”)
- l  说明: 匹配所有可用元素.意思是查找所有input中不带有disabled=”disabled”的input.不为disabled,当然就为enabled啦.

##### 8.1). :disabled

- l  用法: $(”input:disabled”)
- l  说明: 匹配所有不可用元素.与上面的那个是相对应的. 

##### 8.1). :checked

- l  用法: $(”input:checked”)
- l  说明: 匹配所有被选中的元素(复选框、单选框等，不包括select中的option).

##### 8.1). :selected

- l  用法: $(”select option:selected”)
- l  说明: 匹配所有选中的option元素.

  ![image-20211102003057810](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211102165246187-16358431679433.png)

```html
<!DOCTYPE html>
<html>
   <head>
      <meta charset="UTF-8">
      <title>表单对象属性过滤选择器</title>
      <script type="text/javascript" src="../script/jquery-1.7.2.js"></script>
      <script type="text/javascript">
         $(function(){
            //1.对表单内 可用的input 赋值操作
            $("#btn1").click(function(){
               //jQuery对象的val()方法，可以操作表单项value的属性值
               //他可以实现设置和获取操作
               $(":text:enabled").val("New Value");
            });
            //2.对表单内 不可用的input 赋值操作
            $("#btn2").click(function(){
               $(":text:disabled").val("New Value Too");
            });
            //3.获取多选框选中的个数
            $("#btn3").click(function(){
               alert($(":checkbox:checked").length);
            });
            //4.获取多选框选中的内容
            $("#btn4").click(function(){
               var $Obj = $(":checkbox:checked");

               //老方法【遍历】
               // for (var i = 0; i < $Obj.length; i++) {
               //     alert($Obj[i].value)
               // }


               //each方法时jQuery对象提供的用来遍历元素的方法
               //在遍历的function函数中，有一个this对象，就是当前遍历到的DOM对象
               $Obj.each(function (){
                  alert(this.value)
               })
            });
            //5.获取下拉框选中的内容
            $("#btn5").click(function(){
               //获取option标签中选中的文本内容
               var $selObj = $("select option:selected");
               //遍历，获取option中的文本内容
               $selObj.each(function (){
                  alert(this.innerHTML)
               })
            });
         }) 
      </script>
   </head>
   <body>
      <h3>表单对象属性过滤选择器</h3>
       <button id="btn1">对表单内 可用input 赋值操作.</button>
       <button id="btn2">对表单内 不可用input 赋值操作.</button><br /><br />
       <button id="btn3">获取多选框选中的个数.</button>
       <button id="btn4">获取多选框选中的内容.</button><br /><br />
         <button id="btn5">获取下拉框选中的内容.</button><br /><br />
       
      <form id="form1" action="#">         
         可用元素: <input name="add" value="可用文本框1"/><br>
         不可用元素: <input name="email" disabled="disabled" value="不可用文本框"/><br>
         可用元素: <input name="che" value="可用文本框2"/><br>
         不可用元素: <input name="name" disabled="disabled" value="不可用文本框"/><br>
         <br>
         
         多选框: <br>
         <input type="checkbox" name="newsletter" checked="checked" value="test1" />test1
         <input type="checkbox" name="newsletter" value="test2" />test2
         <input type="checkbox" name="newsletter" value="test3" />test3
         <input type="checkbox" name="newsletter" checked="checked" value="test4" />test4
         <input type="checkbox" name="newsletter" value="test5" />test5
         
         <br><br>
         下拉列表1: <br>
         <select name="test" multiple="multiple" style="height: 100px">
             <!-- multiple="multiple"属性，让下拉菜单可以实现多选，ctrl+点击 -->
            <option>浙江</option>
            <option selected="selected">辽宁</option>
            <option>北京</option>
            <option selected="selected">天津</option>
            <option>广州</option>
            <option>湖北</option>
         </select>
         
         <br><br>
         下拉列表2: <br>
         <select name="test2">
            <option>浙江</option>
            <option>辽宁</option>
            <option selected="selected">北京</option>
            <option>天津</option>
            <option>广州</option>
            <option>湖北</option>
         </select>
      </form>       
   </body>
</html>
```

### 6、jQuery 元素筛选

#### 用法

- ```javascript
	$("p").eq(1);	  //全部通过【jQuery对象.方法】调用
	```

#### 过滤

- eq(index|-index)：获取第N个元素
- first()：获取第一个元素
- last()：获取最后一个元素
- hasClass(class)：检查当前的元素是否含有某个特定的类，如果有，则返回true。
	- 这其实就是 is("." + class)。
- filter(expr|obj|ele|fn)：筛选出与指定表达式匹配的元素集合。
	- 这个方法用于缩小匹配的范围。用逗号分隔多个表达式
- is(expr|obj|ele|fn)：根据选择器、DOM元素或 jQuery 对象来检测匹配元素集合，如果其中至少有一个元素符合这个给定的表达式就返回true。
- map(callback)：将一组元素转换成其他数组（不论是否是元素数组）
- has(expr|ele)：保留包含特定后代的元素，去掉那些不含有指定后代的元素。
- not(expr|ele|fn)：删除与指定表达式匹配的元素
- slice(start,[end\])：选取一个匹配的子集

#### 查找

- children([expr\])：取得一个包含匹配的元素集合中每一个元素的所有子元素的元素集合。
- closest(expr,[con\]|obj|ele)：从元素本身开始，逐级向上级元素匹配，并返回最先匹配的元素。
- find(expr|obj|ele)：搜索所有与指定表达式匹配的元素。这个函数是找出正在处理的元素的后代元素的好方法。
- next([expr\])：取得一个包含匹配的元素集合中每一个元素紧邻的后面同辈元素的元素集合。
- nextall([expr\])：查找当前元素之后所有的同辈元素。
- nextUntil([exp|ele\][,fil])：查找当前元素之后所有的同辈元素，直到遇到匹配的那个元素为止。
- offsetParent()：返回第一个匹配元素用于定位的父节点。
- parent([expr\])：取得一个包含着所有匹配元素的唯一父元素的元素集合。
- parents([expr\])：取得一个包含着所有匹配元素的祖先元素的元素集合（不包含根元素）。可以通过一个可选的表达式进行筛选。
- parentsUntil([exp|ele\][,fil])：查找当前元素的所有的父辈元素，直到遇到匹配的那个元素为止。
- prev([expr\])：取得一个包含匹配的元素集合中每一个元素紧邻的前一个同辈元素的元素集合。
- prevall([expr\])：查找当前元素之前所有的同辈元素
- prevUntil([exp|ele\][,fil])：查找当前元素之前所有的同辈元素，直到遇到匹配的那个元素为止。
- siblings([expr\])：取得一个包含匹配的元素集合中每一个元素的所有唯一同辈元素的元素集合。可以用可选的表达式进行筛选。

#### 串联

- add(expr|ele|html|obj[,con\])：把与表达式匹配的元素添加到jQuery对象中。这个函数可以用于连接分别与两个表达式匹配的元素结果集。
- andSelf()：加入先前所选的加入当前元素中
- contents()：查找匹配元素内部所有的子节点（包括文本节点）。如果元素是一个iframe，则查找文档内容
- end()：回到最近的一个"破坏性"操作之前。即，将匹配的元素列表变为前一次的状态

#### 练习：

功能需求：

- ①全选框：点击后让所有爱好的选中状态和自己一致
- ②爱好框：点满后将全选框选中，否则取消选中
- ③全选按钮：点击后所有爱好都选中
- ④全不选按钮：点击后所有爱好都不选中
- ⑤反选按钮：点击后所有爱好选中状态反转
- ⑥提交按钮：点击后依次弹出选中内容

![image-20211102125717733](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211102003057810-163578425912511.png)

```html
<!DOCTYPE html>
<html>
   <head>
   <meta charset="UTF-8">
   <title>全选全不选2(空白)</title>
   <script type="text/javascript" src="../../script/jquery-1.7.2.js"></script>
   <script type="text/javascript">
      /* 
      功能需求：
         ①全选框：点击后让所有爱好的选中状态和自己一致
         ②爱好框：点满后将全选框选中，否则取消选中
      */
      $(function(){
         //全选
         $("#checkedAllBtn").click(function (){
            $(":checkbox").prop("checked",true);
         })
          
         //全不选
         $("#checkedNoBtn").click(function (){
            $(":checkbox").prop("checked",false);
         })
          
         //反选
         $("#checkedRevBtn").click(function (){
            var $checkbox = $(":checkbox[name='items']");
            $checkbox.each(function (){
               this.checked = !this.checked;
            })
            //遍历完成后，判断是否满选，满选把上边的全选也要选中
            //获取球类的总个数
            var length = $(":checkbox[name='items']").length;
            //获取选中的个数
            var checklen = $(":checkbox[name='items']:checked").length;
            //判断若，相等则满选
            // if (length==checklen){
            //     $("#checkedAllBox").prop("checked",true);
            // }else{
            //     $("#checkedAllBox").prop("checked",false);
            // }
            // 优化:相等就true，不等就false
            $("#checkedAllBox").prop("checked",length==checklen);
         })
          
         //提交：获取输出选中的球类信息
         $("#sendBtn").click(function (){
            $(":checkbox[name='items']:checked").each(function (){
               alert(this.value);
            });
         })
          
         //给【全选/全不选】绑定单击事件
         $("#checkedAllBox").click(function (){
            //this是事件中的当前DOM对象，this.checked就看这个全选框是不是被选了，
            // 如果选了，单击后触发，所有球类checked=true
            $(":checkbox").prop("checked",this.checked);
         })
          
         //如果满选了，让全选框自动选上
         $(":checkbox[name='items']").click(function (){
            //获取球类的总个数
            var length = $(":checkbox[name='items']").length;
            //获取选中的个数
            var checklen = $(":checkbox[name='items']:checked").length;
            //判断若，相等则满选
            $("#checkedAllBox").prop("checked",length==checklen);
         })

      });
      
   </script>
   </head>
   <body>
   
      <form method="post" action="">
      
         你爱好的运动是：<input type="checkbox" id="checkedAllBox" />全选/全不选 
         <br />
         <input type="checkbox" name="items" value="足球" />足球
         <input type="checkbox" name="items" value="篮球" />篮球
         <input type="checkbox" name="items" value="羽毛球" />羽毛球
         <input type="checkbox" name="items" value="乒乓球" />乒乓球
         <br/>
         <input type="button" id="checkedAllBtn" value="全　选" />
         <input type="button" id="checkedNoBtn" value="全不选" />
         <input type="button" id="checkedRevBtn" value="反　选" />
         <input type="button" id="sendBtn" value="提　交" />
      </form>
   
   </body>
</html>
```



### 7.    文档处理(CRUD)

#### 1). 内部插入节点

##### 1.1). append(content) 

- l  向每个匹配的元素的内部的结尾处追加内容

##### 1.2). appendTo(content) 

- l  把所有匹配的元素追加到另一个指定的元素集合中

##### 1.3). prepend(content)

- l  向每个匹配的元素的内部的开始处插入内容

##### 1.4). prependTo(content) 

- l  将每个匹配的元素插入到指定的元素内部的开始处

#### 2). 外部插入节点

##### 2.1). after(content) :

- l  在每个匹配的元素之后插入内容 

##### 2.2). before(content)

- l  在每个匹配的元素之前插入内容 

##### 2.3). insertAfter(content)

- l  把所有匹配的元素插入到另一个、指定的元素集合的后面 

##### 2.4). insertBefore(content) 

- l  把所有匹配的元素插入到另一个、指定的元素集合的前面 

#### 3).查找节点

##### 3.1). 使用jQuery选择器查询

- **$(selector)** 
- l  得到一个包含所有匹配的dom节点对象的jQuery对象

##### 3.2). 查询jQuery对象内部数据

- **l  $object.find(selector)**
- l  在Jquery对象中根据selector查找其中匹配的后代节点

##### 3.3). 遍历jQuery对象包含的数据

- **l  $(selector1).each(function(index, itemDom){ })**
- l  遍历jQuery对象所包含的所有节点, 每取一个dom节点对象都去调用设置的回调函数, 并将取出的节点在数组中的下标和节点对象传入函数

#### 4).创建节点

- **l  $(htmlString).**
- l  动态创建的新元素节点不会被自动添加到文档中, 需要使用其他方法将其插入到文档中;
- l  当创建单个元素时, 需注意闭合标签和使用标准的 XHTML 格式. 例如创建一个<p>元素, 可以使用 $(“<p/>”) 或 $(“<p></p>”), 但不能使用 $(“<p>”) 或 $(“</P>”)
- l  创建文本节点就是在创建元素节点时直接把文本内容写出来; 创建属性节点也是在创建元素节点时一起创建

#### 5). 替换节点

- ##### replaceWith():  


- l  【a.replaceWith(b)】-----结果-----用b替换掉a

- ##### replaceAll():  


- l  【a.replaceAll(b)】-----结果-----**用a替换掉所有的b**

#### 6). 删除节点

- ##### empty():


- l  删除匹配的元素集合中所有的子节点(不包括本身)。

- ##### remove(): 


- l  删除匹配的元素及其子元素(包括本身)【标签也干掉】

![image-20211102142434150](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211101081926605-16357259677003.png)

```html
<!DOCTYPE html>
<html>
   <head>
   <meta charset="UTF-8">
   <title>Untitled Document</title>
   <link rel="stylesheet" type="text/css" href="styleB/css.css" />
   <script type="text/javascript" src="../../script/jquery-1.7.2.js"></script>
   <script type="text/javascript">
      $(function(){//外边套一个，表示页面加载完成之后运行
         
          //创建一个可以复用调用的删除函数
         var deleteFun = function (){
            // 先确定要删除哪一行，function中有一个this，就是当前对象，这里就是点击的那个a标签
            // 第一次parent()找到父类列标签，再找一次父类就是行标签
            var $rowObj = $(this).parent().parent();
            var name = $rowObj.find("td:first").text();

            // confirm（）是JavaScript提供的提示框函数，传什么提示什么，
            // 点击确定后，返回true，点击取消返回false
            if (confirm("你确定要删除"+ name +"的人员信息吗？？？")){
               $rowObj.remove();
            }

            // 不让超链接跳转
            return false;
         }

         
         //实现submit单击操作
         $("#addEmpButton").click(function (){
            //获取输入框的内容
            var name = $("#empName").val();
            var email = $("#email").val();
            var salary = $("#salary").val();
            //创建对象模板
            var $rowObj = $("<tr>" +
                  "<td>"+ name +"</td>" +
                  "<td>"+ email +"</td>" +
                  "<td>"+ salary +"</td>" +
                  "<td><a href=\"deleteEmp?id=001\">Delete</a></td>" +
                  "</tr>")
            //添加对象
            $rowObj.appendTo($("#employeeTable"));
            //添加对象后，给a标签绑定点击删除操作，因为之前的检索没有这个新的a标签，
            $rowObj.find("a").click(deleteFun);
         })


         //实现delete操作
         // $("a").click(deleteFun());  //click需要的是函数，这样写就把函数deleteFun()的返回值传给click了
         $("a").click(deleteFun);  //去掉括号，直接给函数
      });


   </script>
   </head>
   <body>
   
      <table id="employeeTable">
         <tr>
            <th>Name</th>
            <th>Email</th>
            <th>Salary</th>
            <th>&nbsp;</th>
         </tr>
         <tr>
            <td>Tom</td>
            <td>tom@tom.com</td>
            <td>5000</td>
            <td><a href="deleteEmp?id=001">Delete</a></td>
         </tr>
         <tr>
            <td>Jerry</td>
            <td>jerry@sohu.com</td>
            <td>8000</td>
            <td><a href="deleteEmp?id=002">Delete</a></td>
         </tr>
         <tr>
            <td>Bob</td>
            <td>bob@tom.com</td>
            <td>10000</td>
            <td><a href="deleteEmp?id=003">Delete</a></td>
         </tr>
      </table>
   
      <div id="formDiv">
      
         <h4>添加新员工</h4>
   
         <table>
            <tr>
               <td class="word">name: </td>
               <td class="inp">
                  <input type="text" name="empName" id="empName" />
               </td>
            </tr>
            <tr>
               <td class="word">email: </td>
               <td class="inp">
                  <input type="text" name="email" id="email" />
               </td>
            </tr>
            <tr>
               <td class="word">salary: </td>
               <td class="inp">
                  <input type="text" name="salary" id="salary" />
               </td>
            </tr>
            <tr>
               <td colspan="2" align="center">
                  <button id="addEmpButton" value="abc">
                     Submit
                  </button>
               </td>
            </tr>
         </table>
   
      </div>
   
   </body>
</html>
```

#### 7). 属性操作

- ##### attr(name ,[value])


- l  根据属性名获取属性值或者设置一个属性**【不推荐操作checked、readOnly、selected、disabled】**

- #####  prop(name ,[value])


- l  可以设置和获取属性的值**【推荐操作checked、readOnly、selected、disabled】**

- #####  removeAttr(name)


- l  根据属性名删除对应的属性

- #####  removeprop(name)


- l  根据属性名删除对应的属性

#### 8). HTML代码/值

- ##### html([val])


- l  得到元素的内容或者设置元素的内容，传参是设置，不传参是获取

- #####  text([val])


- l  得到元素的内容或者设置元素的【文本内容】，传参是设置，不传参是获取

- ##### val([value])


- l  获得匹配元素的当前值或者设置其值

#### 9) CSS样式操作

- #####  addClass(className)


- l  添加样式

- ##### removeClass()


- l  移除样式

- ##### toggleClass()


- l  样式存在就删除，不存在就添加

- ##### offset()

- l  获取和设置元素的坐标
- **css(name,[value])**

- l  查看某个样式属性, 或设置某个样式属性

![image-20211102165246187](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211102142434150-16358342756452.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript" src="../../script/jquery-1.7.2.js"></script>
    <style type="text/css">
        div{
            width: 100px;
            height: 260px;
        }
        div.whiteborder{
            border: 2px solid white;
        }
        div.redDi{
            background-color: red;
        }
        div.bluBorder{
            border: #0050D0 5px solid;
        }
    </style>
    <script type="text/javascript">
        $(function (){
            var $newObj = $("div:first");

            $("#btn01").click(function (){
                $newObj.addClass("redDi bluBorder");
            })
            $("#btn02").click(function (){
                $newObj.removeClass("redDi");
            })
            $("#btn03").click(function (){
                $newObj.toggleClass("redDi");
            })
            $("#btn04").click(function (){
                $newObj.offset();
                $newObj.offset({
                    top:100,
                    left:200
                });
                console.log($newObj.offset());

            })
        })
    </script>
</head>
<body>
    <table align="center">
        <tr>
<!--        要被操作的div-->
            <td>
                <div class="border"></div>
            </td>
            <td>
                <div class="btn" >
                    <input type="button" value="addClass()" id="btn01"/><br/>
                    <input type="button" value="removeClass()" id="btn02"/><br/>
                    <input type="button" value="toggleClass()" id="btn03"/><br/>
                    <input type="button" value="offset()" id="btn04"/>
                </div>
            </td>
        </tr>
    </table>

</body>
</html>
```





### 8、jQuery 动画

#### 8.1 基本动画

- **show()**

- l  将隐藏的元素显示

- **hide()**

- l  将可见的元素隐藏

- **toggle()**

- l  元素可见就隐藏，不可见就显示



- **以上动画方法都可以添加参数：**

	- **参数1：**动画执行时间，以毫秒为单位
	- **参数2：**动画的回调函数，就是动画执行完自动调用该函数

	```javascript
	//两个参数
	$("#btn02").click(function (){
	    $newObj.hide(1000,function (){
	        alert("hide动画完成");
	    });
	});
	
	//一个参数【也可以无参数】
	$("#btn03").click(function (){
	    $newObj.toggle(1000);
	});
	```

**如何实现：动画自己出来又消失，不断动动动？**

```javascript
//递归函数
var toggleAllTime = function (){
    $newObj.toggle(1000,toggleAllTime);//切记传函数名，不要带括号
};
//启动函数
toggleAllTime();
```





#### 8.2 淡入淡出动画

- **fadeln()**
- l   淡入（慢慢可见）
- **fadeOut()**
- l  淡出（慢慢消失）
- **fadeTo()**
- l  在指定时长内，将透明度慢慢的修改到指定值
- **fadeToggle()**
- l  淡入淡出切换



![image-20211102172726182](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211102183206865-16358491287005.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript" src="../../script/jquery-1.7.2.js"></script>
    <style type="text/css">
        div{
            width: 100px;
            height: 260px;
        }
        div.whiteborder{
            border: 2px solid white;
        }
        div.redDi{
            background-color: red;
        }
        div.bluBorder{
            border: #0050D0 5px solid;
        }
    </style>
    <script type="text/javascript">
        $(function (){
            var $newObj = $("div:first");

            $("#btn01").click(function (){
                $newObj.show(1000,function (){
                    alert("show动画完成");
                });
            });
            $("#btn02").click(function (){
                $newObj.hide(1000,function (){
                    alert("hide动画完成");
                });
            });
            $("#btn03").click(function (){
                $newObj.toggle(1000);
            });
            // //递归函数
            // var toggleAllTime = function (){
            //     $newObj.toggle(1000,toggleAllTime);//切记传函数名，不要带括号
            // };
            // //启动函数
            // toggleAllTime();

            $("#btn04").click(function (){
                $newObj.fadeIn(1000,function (){
                    alert("fadeIn动画完成")
                });
            });
            $("#btn05").click(function (){
                $newObj.fadeOut(1000,function (){
                    alert("fadeOut动画完成")
                });
            });
            $("#btn06").click(function (){//1秒内，将透明度改至0.2
                $newObj.fadeTo(1000,0.2,function (){
                    alert("fadeTo动画完成")
                });
            });
            $("#btn07").click(function (){
                $newObj.fadeToggle(1000,function (){
                    alert("fadeToggle动画完成")
                });
            });
        })
    </script>
</head>
<body>
    <table align="center">
        <tr>
<!--        要被操作的div-->
            <td>
                <div class="border" style="background-color: #99ff99"></div>
            </td>
            <td>
                <div class="btn" >
                    <input type="button" value="show()展示" id="btn01"/><br/>
                    <input type="button" value="hide()隐藏" id="btn02"/><br/>
                    <input type="button" value="toggle()切换" id="btn03"/><br/>
                    <input type="button" value="fadeIn()淡入" id="btn04"/>
                    <input type="button" value="fadeOut()淡出" id="btn05"/>
                    <input type="button" value="fadeTo()时间内改透明度至" id="btn06"/>
                    <input type="button" value="fadeToggle()淡入淡出切换" id="btn07"/>
                </div>
            </td>
        </tr>
    </table>

</body>
</html>
```

#### 8.3  练习：品牌展示动画

实现：页面中仅显示部分品牌名称，点击加载更多，展示全部品牌，还可以再次收起

![image-20211102183206865](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211102183218646-16358491397956.png)



![image-20211102183218646](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211103144412574-16359218551101.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style type="text/css">
        *{
            margin: 0;
            padding: 0;
        }
        body{
            font-size: 12px;
            text-align: center;
        }
        a{
            color: #04D;
            text-decoration: none;
        }
        a:hover{
            color: red;
            text-decoration: underline;
        }
        .SubCategoryBox{
            width: 600px;
            margin: 0 auto;
            text-align: center;
            margin-top: 40px;
        }
        .SubCategoryBox ul{
            list-style: none;
        }
        .SubCategoryBox ul li{
            display: block;
            float: left;
            width: 200px;
            line-height: 20px;
        }
        .showmore , .showless{
            clear: both;
            text-align: center;
            padding-top: 10px;
        }
        .showmore a, .showless a{
            display: block;
            margin: 0 auto;
            width: 120px;
            line-height: 24px;
            border: 1px solid #AAA;
        }
        .showmore a span{
            padding-left: 15px;
            background: url(audi.JPG) no-repeat 0 0;
        }
        .showless a span{
            padding-left: 15px;
            background: url(BMW.JPG) no-repeat 0 0;
        }
        .promoted a{
            color: #f50;
        }
    </style>
    <script type="text/javascript" src="../../script/jquery-1.7.2.js"></script>
    <script type="text/javascript">
        $(function (){//页面加载完成后启动
            //1、初始状态
            $("li:gt(3):not(:last)").hide();//获取li标签数组，取大于索引5的，不包括最后一个，然后隐藏
            //2、获取全部品牌对象,并绑定单击事件
            $("div:eq(1) a").click(function (){
                //切换隐藏的品牌状态
                $("li:gt(3):not(:last)").toggle();
                if($("li:gt(3):not(:last)").is(":hidden")){//判断目标品牌，是隐藏还是显示
                    // 返回true，部分品牌是隐藏的，此时需要【角标向下】的图片，文字【展示全部品牌】
                    // 文字
                    $("div:eq(1) a span").text("展示全部品牌");
                    // 图片
                    $("div:eq(1)").removeClass();//删除样式，class="showmore"
                    $("div:eq(1)").addClass("showmore");

                    // 部分展示时，关闭突出部分品牌颜色
                    $("li:contains('苹果')").removeClass("promoted");
                }else{
                    // 返回false，全部品牌显示，此时需要【角标向上】的图片，文字【展示部分品牌】
                    // 文字
                    $("div:eq(1) a span").text("展示部分品牌");
                    // 图片
                    $("div:eq(1)").removeClass();//删除样式，class="showmore"
                    $("div:eq(1)").addClass("showless");//showless就是向上的箭头图片

                    // 全展示时，突出部分品牌 高亮显示
                    $("li:contains('苹果')").addClass("promoted");
                }


                return false;//禁止自动跳转
            });
        });
    </script>
</head>
<body>
    <div class="SubCategoryBox">
        <ul type="none">
            <li><a href="#">苹果</a><i>（11100）</i></li><!--i标签斜体-->
            <li><a href="#">三星</a><i>（10101） </i></li>
            <li><a href="#">索尼</a><i>（22222） </i></li>
            <li><a href="#">松下</a><i>（33333） </i></li>
            <li><a href="#">尼康</a><i>（32414） </i></li>
            <li><a href="#">格力</a><i>（44444） </i></li>
            <li><a href="#">美的</a><i>（32432） </i></li>
            <li><a href="#">富士康</a><i>（22323） </i></li>
            <li><a href="#">小米</a><i>（99999） </i></li>
            <li><a href="#">华为</a><i>（09090） </i></li>
            <li><a href="#">其他品牌</a><i>（12321） </i></li>
        </ul>
    </div>
    <div class="showmore">
        <a href="more.html"><span>显示全部品牌</span></a>
    </div>
</body>
</html>
```

**标签中class属性，可以在外边定义好，直接调用改名，就换了新的样式，**

**此处用来实现状态不同，所带的图片不同**

###  9、jQuery 事件操作

#### 1)  常用的事件

##### 1.1). ready(fn)

l  当DOM载入就绪可以查询及操纵时绑定一个要执行的函数

l  **$(function(){})**与**window.onload**是有区别的

![image-20211103144412574](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211103152141555-16359241031092.png)

```javascript
<script type="text/javascript" src="../../script/jquery-1.7.2.js"></script>
<script type="text/javascript">
   window.onload=function (){
      alert("这是原生JavaScript页面加载完成之后--1")
   }
   window.onload=function (){
      alert("这是原生JavaScript页面加载完成之后--2")
   }
   //只会执行第二个，因为第二个将前面的覆盖了
   $(function (){
      alert("这是jQuery的页面加载完成之后--1")
   })
   $(function (){
      alert("这是jQuery的页面加载完成之后--2")
   })
   //两个都会执行，而且在window.onload前面执行

   //window.onload执行慢，是因为他在等待页面所有内容加载完成【如图片，加载进来等】
   //jQuery 直接代码跑完，就执行，不等内容是否加载进来
</script>
```

##### 1.2). click([fn])

l  触发或绑定每一个匹配元素的click事件【传function就是绑定单击事件，不传参数直接click()，就是触发】

##### 1.3). blur([fn])

l  触发每一个匹配元素的blur事件

##### 1.4). change([fn])

l  触发每一个匹配元素的change事件

##### 1.5). mouseover([fn])

l  鼠标移入触发该事件

##### 1.6). mouseout([fn])

l  鼠标移出触发该事件

#### 2)  绑定与解绑事件

##### 2.1). bind(type, fn)

l   为每个匹配元素的特定事件绑定事件处理函数。

##### 2.2). unbind(type)

l  bind()的反向操作，从每一个匹配的元素中删除绑定的事件

##### 2.3). live(type，fn)

l  跟bind作用相同，可以绑定一个或多个事件，**但是**使用ive绑定的，哪怕是后面从新创建的符合条件的对象，也会被绑定上，她是动态绑定，bind只能绑定创建时已存在的对象。

```javascript
<script type="text/javascript">
   /* 通过jquery绑定事件 */
   $(function(){
      bind绑定多个事件
      $("#btn01").bind("click mouseout mouseover",function (){
         console.log("bind绑定的事件");
      });
      //live 绑定，，实现动态
      $("#btn01").live("click mouseout mouseover",function (){
         console.log("bind绑定的事件");
      });
      //对下边创建的新的对象，也能给绑定上
      $("<button id=\"btn01\">按钮1</button>").appendTo("body");

      //unbind移除事件
      $("#btn01").unbind("click mouseover");
   });

</script>
```

#### 3)  事件切换

##### 3.1). hover(over,out)

l  当鼠标移动到一个匹配的元素上面时，会触发指定的第一个函数。当鼠标移出这个元素时，会触发指定的第二个函数。

#### 4)  事件冒泡

l  描述: 事件会按照 DOM 层次结构像水泡一样不断向上只止顶端**【就是父元素和子元素绑定了相同类型的事件，触发子元素的事件，父元素也会被触发】**

l  解决: 在事件处理函数中返回 false, 会对事件停止冒泡

![image-20211103152141555](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211102172726182-16358452475504.png)

```html
<!DOCTYPE html>
<html>
   <head>
      <meta charset="UTF-8">
      <title>Untitled Document</title>
      <style type="text/css">
         *{margin: 0;padding: 0;}
         body{font-size: 13px;line-height: 130%;padding: 60px;}
         div{width: 220px;border: 1px solid #0050D0;background: #96E555;}
         span{width: 200px;margin: 10px;background: #666666;cursor: pointer;color: white;display: block;}
      </style>
      <script type="text/javascript" src="../../script/jquery-1.7.2.js"></script>
      <script type="text/javascript">
         $(function(){
            //父元素单击事件
            $("#content").click(function (){
               alert("我是父元素div的单击事件")
            })
            //内层子元素的单击事件
            $("span").click(function (){
               alert("我是子元素span的单击事件")
               // 子元素处添加return false就不会向父类冒泡了，执行完就停止了
               return false;
            })
         });
      </script>
   </head>
   <body>
      <div id="content">
         外层div元素
            <span>内层span元素</span>
         外层div元素
      </div>
   </body>
</html>
```

### 10 、jQuery 事件对象

**事件对象：是封装有触发的事件信息的一个JavaScript对象。**

**如何获取？**

- 在给元素绑定事件的时候，在事件函数<font color='red'>function(event){}；</font>参数列表中添加一个参数，这个参数名一般命名为event，而触发事件以后，event就是JavaScript 传递事件处理函数的事件对象

event事件对象包含所有所有内容：

![捕获](https://pledge99.oss-cn-beijing.aliyuncs.com/img/捕获-16359265086403.PNG)



#### 1、原生JavaScript 获取 事件对象

```javascript
//JavaScript代码获取  事件对象
window.onload=function (){
   document.getElementById("areaDiv").onclick=function (event){
      console.log(event);
   }
}
```

#### 2、jQuery 代码获取 事件对象

```javascript
// jQuery代码获取  事件对象
$(function() {// 页面加载函数不能忘！！！！！！！！！！！
   $("#showMsg").click(function (event){
      console.log(event);
   })
});
```

#### 3、使用bind 同时对多个事件绑定同一个函数。怎么获取当前操作是什么事件？

```javascript
// 使用bind 同时对多个事件绑定同一个函数。怎么获取当前操作是什么事件？
<script type="text/javascript">
		$(function (){// 页面加载函数不能忘！！！！！！！！！！！
			$("#areaDiv").bind("mouseout mouseover",function (event){
				if (event.type == "mouseout"){
					console.log("鼠标移出，，，事件对象信息");
					console.log(event);
				}else if(event.type == "mouseover"){
					console.log("鼠标移入，，，事件对象信息");
					console.log(event);
				}
			});
		})
</script>
```



### 11、图片跟随练习

需求：实现淘宝主页，鼠标放到图片上时，出现放大的图，并跟随鼠标移动

![洒点水](https://pledge99.oss-cn-beijing.aliyuncs.com/img/洒点水-16359374572324.PNG)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript" src="../../script/jquery-1.7.2.js"></script>
    <script type="text/javascript">
        $(function (){
            $("#small").bind("mouseover mouseout mousemove",function (event){
                if (event.type == "mouseover"){
                    // 进入图片，显式大图
                    $("#showBig").show();
                }else if (event.type == "mouseout"){
                    // 离开图片，隐藏大图
                    $("#showBig").hide();
                }else if (event.type == "mousemove"){
                    // 设置大图坐标，根据鼠标坐标设置
                    $("#showBig").offset({
                        // 这里离开10个像素，要不然向右下角移动时，
                        // 鼠标出现在大图上方，会引起系统误会，以为鼠标离开了小图范围，
                        // 等大图过去以后，再次恢复，就会出现卡顿现象【即便设置错开10，但如果移动过快还是会卡】
                        left:event.pageX + 10,
                        top:event.pageY + 10
                    })
                }
            })
        })
    </script>
</head>
<body>
    <img id="small" src="../../Demo04.事件/01.文档加载/img/1.jpg"/>
    <div id="showBig">
        <img src="../品牌展示/BMW.JPG"/>
    </div>
</body>
</html>
```



**注意：**

- 设置大图坐标，根据鼠标坐标设置
- 这里离开10个像素，要不然向右下角移动时，                    
- 鼠标出现在大图上方，会引起系统误会，以为鼠标离开了小图范围，
- 等大图过去以后，再次恢复，就会出现卡顿现象【即便设置错开10，但如果移动过快还是会卡】                    
- $("#showBig").offset({
	          left:event.pageX + 10,
	          top:event.pageY + 10
	  })；



## 第5章 XML

### 1、什么是XML？

xml 是可扩建的标记性语言

- **XML**--可扩展标记语言
	-   e**X**tensible**M**arkup**L**anguage

- 由W3C组织发布，目前推荐遵守的是W3C组织于2000年发布的XML1.0规范

- **XML**的使命，就是以一个统一的格式，组织有关系的数据，为不同平台下的应用程序服务

- **XML**用来<font color='red'>传输和存储数据</font>，**HTML**用来<font color='red'>显示数据</font>

- **XML**没有预定义标签，均为自定义标签

### 2、XML的用途

- 1.配置文件【就像properties文件】
	- JavaWeb中的web.xml
	- C3P0中的c3p0-config.xml

- 2.数据交换格式
	- Ajax
	- WebService

- 3.数据存储
	- 保存关系型数据

- 4.作为网络传输数据的格式（现在json文件为主）

	![image-20211104101618599](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211104101720862111.png)

![image-20211104101720862](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211104122916342.png)

### 3、XML的基本语法

- **语法规则**
	- XML声明要么不写，要写就写在第一行，并且前面没有任何其他字符
	- 只能有一个根标签
	- 标签必须正确结束
	- 标签不能交叉嵌套
	- 严格区分大小写
	- 属性必须有值，且必须加引号
	- 标签不能以数字开头
	- 注释不能嵌套

- **XML文档组成**
- XML声明
	- version属性指定XML版本，固定值是1.0
	- encoding指定的字符集，是告诉解析器使用什么字符集进行解码，而编码是由文本编辑器决定的
- **CDATA区**【里边内容，就是纯文本，不会被解析】
	- 当XML文档中需要写一些程序代码、SQL语句、<等特殊符号 或其他不希望XML解析器进行解析的内容时，就可以写在CDATA区中
	- XML解析器会将CDATA区中的内容原封不动的输出
	- CDATA区的定义格式：<![CDATA[…]]>

```xml
<?xml version="1.1" encoding="utf-8"?>
<!--
    <?xml verson="1.0" encoding="utf-8" ?>
    以上内容就是xml文件的声明
    verson="1.0"        verson      表示xml 的版本
    encoding="utf-8"    encoding    表示xml文件本身的编码方式
-->



<books><!--books【根元素：唯一、无父元素】 表示多个图书信息-->
<!--    多标签-->
    <book sn="SN1234567"><!-- book 表示一本书的信息   SN是图书的序列号-->
        <name>百年孤独</name><!--name 标签表示书名-->
        <author>加西亚·马尔克斯</author><!--author 标签表示作者-->
        <price>99</price><!--price 标签表示价格-->
    </book>
    <book sn="SN987654"><!-- book 表示一本书的信息   SN是图书的序列号-->
        <name>杀死一只知更鸟</name><!--name 标签表示书名-->
        <author>
            哈珀·李<![CDATA[<!=李==3332>》]]>

        </author><!--author 标签表示作者-->
        <price>88</price><!--price 标签表示价格-->
    </book>
<!--    单标签-->
    <book sn="9292929" name="围城" author="钱钟书" price="77"/>
</books>
```



### 4、XML解析

- XML解析是指通过解析器读取XML文档，解释语法，并将文档转化成对象

- 对XML的一切操作都是由解析开始的，所以解析非常重要。

- Java 平台同时提供了 DOM（Document Object Model）和 SAX（Simple API for XML）。

#### XML解析技术体系

![image-20211104122732299](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211104122732299.png)



#### DOM和SAX对比

![image-20211104122916342](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211104101618599.png)

#### dom4j

- dom4j是一个开源XML解析包
- dom4j是一个非常优秀的Java XML API，具有**性能优异、功能强大和极易使用的特点**。现在很多软件都采用dom4j，例如Hibernate。
- 使用dom4j开发，**需导入dom4j相应的jar包dom4j-1.6.1.jar**

##### 1、创建对应XML文件的对应类

![image-20211105081738968](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211105081738968.png)

![image-20211105081432344](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211105081432344.png)



##### 2、读取并输出

```java
/**
 * 读取books.xml文件生成Book类
 */
@Test
public void test2() throws DocumentException {
    // 1、读取books.xml文件
    SAXReader saxReader = new SAXReader();
    	// 在Junit测试中，相对路径是从【当前模块名开始的】
    Document document = saxReader.read("XML_01/books.xml");
    
    // 2、通过Document对象获取【根元素】
    Element root = document.getRootElement();
    
    // 3、通过根元素获取【book标签对象】
        // root.element和book.elements都是获取对象类，多个用elements，单个用element
    List<Element> books = root.elements("book");
    
    // 4、遍历，处理每一个book标签对象转换成的Book类
    for(Element book : books){
        // asXML()方法是将标签对象，转换成标签字符串
        Element nameElement = book.element("name");
        // getText();可以获取标签中的文本
        String nameText = nameElement.getText();//不能获取单标签中的内容
        // 直接获取指定标签名的文本内容
        String priceText = book.elementText("price");
        String authorText = book.elementText("author");

        // 获取属性
        String snValue = book.attributeValue("sn");

        System.out.println(new Book(snValue,nameText,new BigDecimal(priceText),authorText));
    }
}
```

**注：什么是BigDecimal？？**

Java在java.math包中提供的API类BigDecimal，用来对超过16位有效位的数进行精确的运算。双精度浮点型变量double可以处理16位有效数。在实际应用中，需要对更大或者更小的数进行运算和处理。float和double只能用来做科学计算或者是工程计算，在商业计算中要用java.math.BigDecimal。BigDecimal所创建的是对象，我们不能使用传统的+、-、*、/等算术运算符直接对其对象进行数学运算，而必须调用其相对应的方法。方法中的参数也必须是BigDecimal的对象。构造器是类的特殊方法，专门用来创建对象，特别是带有参数的对象。



#### dom4j 解析关键步骤

- 1、解析

	```java
	//1.创建解析器对象
	SAXReader saxReader = new SAXReader();
	//2.解析xml文件获取document对象
	Document document = saxReader.read("students.xml");
	//3.得到根元素
	Element root = document.getRootElement();
	
	```

- 2、修改

	```java
	//添加一个新的student节点
	Element newEle = rootElement.addElement("student");
	//创建一个良好的xml格式
	OutputFormat format = OutputFormat.createPrettyPrint();
	//写入文件
	XMLWriter xmlWriter = new XMLWriter(new FileWriter("students.xml"),format);
	xmlWriter.write(document);
	xmlWriter.close();
	
	```

- 3、新建

	```java
	//1.创建文档
	Document document = DocumentHelper.createDocument();
	//2.添加根元素
	Element root = document.addElement("teachers");
	//3.添加元素节点
	Element tcEle = root.addElement("teacher");
	Element tcEle2 = root.addElement("teacher");
	```



#### Xpath查询

- XPath 是在 XML 文档中查找信息的语言

- XPath通过元素和属性进行查找，简化了Dom4j查找节点的过程，是W3C组织发布的标准。

- 使用XPath必须导入jaxen-1.1-beta-6.jar包

- 具体语法见 XPathTutorial(菜鸟必备)

- **<font color='red'>两个重要方法：</font>**

	```java
	document.selectSingleNode("/students/student[@id='1']");
	document.selectNodes("/students/student")
	```

	

## 第6章 Web

### 1、概念

![image-20211105090547661](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211105090547661-16360748104221.png)

- **javaWeb** 是指，所有通过 Java 语言编写可以通过浏览器访问的程序的总称
	- JavaWeb是基于请求和响应开发的

- **请求** 是指 客户端给服务器发送数据，叫请求（request）
- **响应** 是指服务器给客户端回传数据，叫响应（response） 

请求和响应是成对出现的，有请求就有响应

![image-20211105091305193](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211105091305193.png)





### 2、Web 资源的分类

- **静态资源：**html、css、js、txt、mp4、jpg等
- **动态资源：**jsp页面、servelet 程序

### 3、Web 知识体系

- **JavaWeb 知识体系**

	![image-20211105091001002](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211105091001002.png)

- **JavaWeb 应用原理**

	![image-20211105091056593](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211105091056593.png)



### 4、常用的 Web服务器

- <font color='red'>**Tomcat**</font>：由 Apache 组织提供的一种 Web 服务器，提供对 jsp 和 Servlet 的支持。它是一种<font color='red'>轻量级的 javaWeb 容器（服务器）</font>，也是当前应用最广的 JavaWeb 服务器（免费）。 

- **Jboss**：是一个遵从 JavaEE 规范的、开放源代码的、纯 Java 的 EJB 服务器，它支持所有的 JavaEE 规范（免费）。 
- **GlassFish**： 由 Oracle 公司开发的一款 JavaWeb 服务器，是一款强健的商业服务器，达到产品级质量（应用很少）。 
- **Resin**：是 CAUCHO 公司的产品，是一个非常流行的服务器，对 servlet 和 JSP 提供了良好的支持， 性能也比较优良，resin 自身采用 JAVA 语言开发（收费，应用比较多）。 
- **WebLogic**：是 Oracle 公司的产品，是目前应用最广泛的 Web 服务器，支持 JavaEE 规范， 而且不断的完善以适应新的开发要求，适合大型项目（收费，用的不多，适合大公司）。



## 第7章 Tomcat 服务器

### 7.1 Tomcat 简介

Tomcat是Apache 软件基金会（Apache Software Foundation）的Jakarta 项目中的一个核心项目，由Apache、Sun 和其他一些公司及个人共同开发而成。由于有了Sun 的参与和支持，最新的Servlet 和JSP 规范总是能在Tomcat 中得到体现，因为<font color='blue'>Tomcat 技术先进、性能稳定，而且免费</font>，因而深受Java 爱好者的喜爱并得到了部分软件开发商的认可，成为目前比较流行的Web 应用服务器。目前最新版本是9.0。我们要用的是7.0。

因为tomcat服务器软件需要使用java环境，所以需要正确的配置java_home

### 7.2 Tomcat 安装

解压apache-tomcat-7.0.77-windows-x64.zip到**非中文无空格**目录中

![image-20211105092418791](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211105092418791.png)

- **bin**：该目录下存放的是二进制可执行文件，如果是安装版，那么这个目录下会有两个exe文件：tomcat6.exe、tomcat6w.exe，前者是在控制台下启动Tomcat，后者是弹出GUI窗口启动Tomcat；如果是解压版，那么会有startup.bat和shutdown.bat文件，startup.bat用来启动Tomcat，但需要先配置JAVA_HOME环境变量才能启动，shutdawn.bat用来停止Tomcat；

- **conf**：这是一个非常非常重要的目录，这个目录下有四个最为重要的文件：

	- server.xml：配置整个服务器信息。例如修改端口号
	- tomcat-users.xml：存储tomcat用户的文件，这里保存的是tomcat的用户名及密码，以及用户的角色信息。可以按着该文件中的注释信息添加tomcat用户，然后就可以在Tomcat主页中进入Tomcat Manager页面了；
	- web.xml：部署描述符文件，这个文件中注册了很多MIME类型，即文档类型。这些MIME类型是客户端与服务器之间说明文档类型的，如用户请求一个html网页，那么服务器还会告诉客户端浏览器响应的文档是text/html类型的，这就是一个MIME类型。客户端浏览器通过这个MIME类型就知道如何处理它了。当然是在浏览器中显示这个html文件了。但如果服务器响应的是一个exe文件，那么浏览器就不可能显示它，而是应该弹出下载窗口才对。MIME就是用来说明文档的内容是什么类型的！

	- context.xml：对所有应用的统一配置，通常我们不会去配置它。

- **lib**：Tomcat的类库，里面是一大堆jar文件。如果需要添加Tomcat依赖的jar文件，可以把它放到这个目录中，当然也可以把应用依赖的jar文件放到这个目录中，这个目录中的jar所有项目都可以共享之，但这样你的应用放到其他Tomcat下时就不能再共享这个目录下的jar包了，所以建议只把Tomcat需要的jar包放到这个目录下；

- **logs**：这个目录中都是日志文件，记录了Tomcat启动和关闭的信息，如果启动Tomcat时有错误，那么异常也会记录在日志文件中。

- **temp**：存放Tomcat的临时文件，这个目录下的东西可以在停止Tomcat后删除！

- **webapps**：存放web项目的目录，其中每个文件夹都是一个项目；如果这个目录下已经存在了目录，那么都是tomcat自带的项目。其中ROOT是一个特殊的项目，在地址栏中没有给出项目目录时，对应的就是ROOT项目。http://localhost:8080/examples，进入示例项目。其中examples就是项目名，即文件夹的名字。

- **work**：运行时生成的文件，最终运行的文件都在这里。通过webapps中的项目生成的！可以把这个目录下的内容删除，再次运行时会生再次生成work目录。当客户端用户访问一个JSP文件时，Tomcat会通过JSP生成Java文件，然后再编译Java文件生成class文件，生成的java和class文件都会存放到这个目录下。

- **LICENSE**：许可证。

- **NOTICE**：说明文件。

###  7.3 Tomcat 配置

- 如果双击startup.bat后窗口一闪而过，请查看JAVA_HOME是否配置正确

 ![image-20211105100056319](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211105100056319.png)

- 或者单独创建一个环境变量
	- 新建环境变量CATALINA_HOME=解压目录
	- 在Path环境变量中加入Tomcat解压目录\bin目录

###  7.4 Tomcat 启动

- 启动方法
	- 方式一：在命令行中运行catalina run【如果启动失败，会显示报错信息，查看哪里错了】
		- ![image-20211105095626093](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211105095626093.png)
	- 方式二：bin目录下点击 startup.bat 启动Tomcat服务器【如果启动失败，小黑窗口一闪而过，over】

- 测试是否成功启动
	- 在浏览器地址栏访问如下地址进行测试

		- **http://localhost:8080**
		- http://127.0.0.1:8080
		- http://真实IP:8080

	- 浏览器显式如下界面【Tomcat里的webapps里的ROOT工程】，就是启动成功了

		![image-20211105094436865](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211105094436865.png)

 

- 如果启动失败，提示端口号被占用，则将默认的8080端口修改为其他未使用的值，例如10086等。
	- 打开：解压目录\conf\server.xml，找到第一个Connector标签
	- 修改port属性将8080改成相应的你修改的值

### 7.5 Tomcat 关闭

- **关闭方法：**
	- 方式一：点击Tomcat 服务器的关闭按钮【就是那个命令行关闭】
		- ![image-20211105102315766](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211105102315766.png)
	- 方式二：在Tomcat 服务器页面 用快捷键Ctrl +C
	- 方式三【<font color='red'>主要方法</font>】：在Tomcat 服务器的安装目录的bin目录中点击shutdown.bat
		- ![image-20211105102231520](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211105102231520.png)

### 7.6 修改Tomcat 端口号

MySQL 默认端口号：3306

Tomcat 默认端口号：8080

- 打开：解压目录\conf\server.xml，找到第一个Connector标签
	- ![image-20211105102511095](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211105102511095.png)
- 修改port属性将8080改成相应的你修改的值
- 端口号范围：【1~65535】
- 修改后要重启Tomcat 服务器才有效
- 再测试启动成功时
	- http://localhost:8080【此处也要改成相应的端口号】

### 7.7 如何部暑 web 工程到 Tomcat 中

#### 方式一：工程拷贝到 Tomcat 的 webapps 目录下

**1、只需要把 web 工程的目录拷贝到 Tomcat 的 webapps 目录下即可**

![image-20211105153207988](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211105153207988.png)



**2、如何访问Tomcat 下的文本工程**

直接在浏览器输入如下格式

http://IP:端口/工程名/目录/具体文件名

![image-20211105153807286](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211105153807286.png)

#### 方式二：引用外部的项目

**1、引用外部的项目（如果项目存放在其他盘，不想复制到webapps下，可采用）**

- 创建一个XML文件【假设名字为OutBooks.xml】【注意格式是UTF-8】，至【安装目录->conf->catalina->localhost】下
- 内容为<Context docBase="F:/OutBooks"  docBase="E:\computer\Books">
	-  path为访问项目的路径
	- docBase为项目的存放地址

- OutBooks是自定义的，可以根据工程随便起名

![image-20211105162932196](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211105162932196.png)

**2、如何访问Tomcat 下的文本工程**

直接在浏览器输入如下格式

http://IP:端口/OutBooks/目录/具体文件名

**注意：OutBooks已经指到E:\computer\Books，在浏览器中就不要写Books了，直接写内部目录就行了**



#### ROOT 和index.html的访问

当我们在浏览器地址栏输入

http://ip:port/     ----------------》》》》》没有工程名时默认访问的是Tomcat里webapps里的ROOT工程

当我们在浏览器地址栏输入

http://ip:port/工程名     ----------------》》》》》默认访问的是Tomcat里webapps里的相应工程的index.html文件







#### 手托【html文件】到浏览器和在浏览器中输入 http://ip:端 口号/工程名/访问的区别

![image-20211105164342844](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211105164342844.png)

![image-20211105164407608](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211105164407608.png)



### 7.8 IDEA 整合 Tomcat 服务器



- IDEA添加Tomcat 服务器，可以添加多个不同的版本

![image-20211105172429130](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211105172429130.png)



- 创建工程时选择Tomcat 服务器

![image-20211105172714716](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211105172714716.png)



### 7.9 IDEA中实现动态web工程

#### 一、IDEA中如何创建动态web 工程

![image-20211105173238567](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211105173238567.png)



创建成功如下：

![image-20211105173741191](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211105173741191.png)



#### 二、Web 工程的目录介绍

![image-20211105173801848](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211105173801848.png)

#### 三、如何给动态 web 工程添加额外 jar 包

直接复制jar 包到lib 目录下

右键Add as Libaray

![image-20211105174226541](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211105174226541.png)



#### 四、在 IDEA 中部署工程到 Tomcat 上运行

##### 1、建议修改 web 工程对应的 Tomcat 运行实例名称：

![image-20211105195140157](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211105195140157.png)

##### 2、确认你的 Tomcat 实例中有你要部署运行的 web 工程模块

![image-20211105195223670](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211105195223670.png)



##### 3、你还可以修改你的 Tomcat 实例启动后默认的访问地址

![image-20211105195254032](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211105195254032.png)

##### 4、在 IDEA 中如何运行和停止 Tomcat 实例。 

4.1、正常启动 Tomcat 实例

![image-20211105195333044](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211105195333044.png)

4.2、Debug 方式启动 Tomcat 

![image-20211105195354342](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211105195544734.png)

4.3、停止 Tomcat 运行实例

![image-20211105195411782](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211105195612528.png)

4.4、重启 Tomcat 运行实例

![image-20211105195438201](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211105195703550.png)

##### 5、修改工程访问路径

![image-20211105195544734](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211105195632227.png)

##### 6、修改运行的端口号

![image-20211105195612528](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211105195354342.png)

##### 7、修改运行使用的浏览器

![image-20211105195632227](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211105195411782.png)

##### 8、配置资源热部署【不用重启服务器，刷新网页就可以更新内容】

![image-20211105195703550](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211105195438201.png)



## 第8章 Servlet 技术

### 一、什么是Servlet技术

- 1、Servlet 是 JavaEE 规范之一。规范就是接口 
- 2、Servlet 就 JavaWeb 三大组件之一。<font color='blue'>三大组件分别是：Servlet 程序、Filter 过滤器、Listener 监听器。 </font>
- 3、Servlet 是运行在服务器上的一个 java 小程序，<font color='red'>它可以接收客户端发送过来的请求，并响应数据给客户端。</font>

### 二、手动实现Servlet 程序

- Servlet 程序代码【是Java】

在这个位置编写Java程序：

![image-20211106074306062](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211106074728011.png)

```java
import javax.servlet.*;
import java.io.IOException;

// 继承接口、重写方法
public class MyServlet implements Servlet {
    public MyServlet() {
    }

    @Override
    public void init(ServletConfig servletConfig) throws ServletException {
    }

    @Override
    public ServletConfig getServletConfig() {
        return null;
    }

    /**
     * service 方法 是专门用来处理请求和响应的
     * @param servletRequest
     * @param servletResponse
     * @throws ServletException
     * @throws IOException
     */
    @Override
    public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {
        System.out.println("hello servlet 被访问了");
    }

    @Override
    public String getServletInfo() {
        return null;
    }

    @Override
    public void destroy() {

    }
}
```



- web.xml 中的配置：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

    <!-- servlet 标签给Tomcat 配置Servlet程序-->
    <servlet>
        <!--servlet-name 标签 Servlet程序起一个别名【一般是类名】-->
        <servlet-name>MyServlet</servlet-name>
        <!--servlet-class 标签 Servlet程序的全类名-->
        <servlet-class>TH.One.MyServlet</servlet-class>
    </servlet>

    <!--servlet-mapping标签给servlet程序配置访问地址-->
    <servlet-mapping>
        <!-- 此处servlet-name标签作用是告诉服务器，我当前配置的地址给哪个servlet程序使用-->
        <servlet-name>MyServlet</servlet-name>
        <!-- url-pattern标签配置访问地址<br/>
            /        斜杠在服务器解析的时候，表示地址为：http://ip:port/工程路径   <br/>
            /hello   表示地址为：http://ip:port/工程路径/hello        <br/>

        -->
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>
</web-app>
```



### 三、常见的错误

#### 1、url-pattern 中配置的路径没有以斜杠打头

![image-20211106074627977](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211106074708308.png)

#### 2、servlet-name 配置的值不存在

![image-20211106074708308](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211106074306062.png)

#### 3、servlet-class 标签的全类名配置错误

![image-20211106074728011](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211106074627977.png)

### 四、url 地址到 Servlet 程序的访问【流程】

![image-20211106074821991](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211106074821991.png)

### 五、Servlet 的生命周

- **1、执行 Servlet 构造器方法**
- **2、执行 init 初始化方法** 
	- 第一、二步，是在第一次访问的时候创建 Servlet 程序会调用。【仅一次】 
- **3、执行 service 方法** 
	- 第三步，每次访问都会调用。
- **4、执行 destroy 销毁方法** 
	- 第四步，在 web 工程停止的时候调用【也是一次，就结束了】



### 六、GET 和 POST 请求的分发处

```java
@Override
public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {
    // 类型转换（因为它的子类有getMethod()方法，所以转换一下）
    HttpServletRequest servletRequest1 = (HttpServletRequest) servletRequest;
    // 获取请求方式
    String method = servletRequest1.getMethod();
    
    // 判断请求类型，调用不同的方法
    if ("GET".equals(method)){
        doGet();
    }else if ("POST".equals(method)){
        doPost();
    }
}



public void doGet(){
    // 这里写GET请求要做的事情
    System.out.println("哈哈，你想要get请求做什么呀");
}



public void doPost(){
    // 这里写POST请求要做的事情
    System.out.println("哈哈，你想要post请求做什么呀");
}
```



### 七、通过继承 HttpServlet 实现 Servlet 程序

一般在实际项目开发中，都是使用继承 HttpServlet 类的方式去实现 Servlet 程序。

- 1、编写一个类去继承 HttpServlet 类 
- 2、根据业务需要重写 doGet 或 doPost 方法 
- 3、到 web.xml 中的配置 Servlet 程序的访问地址 Servlet 类的代码



Servlet 代码

```java
public class HelloHttpServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("这里是HttpServlet 的GET方法，你要做什么啊？？？");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("这里是HttpServlet 的POST方法，你要做什么啊？？？");
    }
}
```

web.xml 配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

<!--配置MyServlet 工程-->
    <servlet>
        <servlet-name>MyServlet</servlet-name>
        <servlet-class>TH.One.MyServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>MyServlet</servlet-name>
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>
<!--配置HelloHttpServlet 工程-->
    <servlet>
        <servlet-name>HelloHttpServlet</servlet-name>
        <servlet-class>TH.One.HelloHttpServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>HelloHttpServlet</servlet-name>
        <url-pattern>/helloHttp</url-pattern>
    </servlet-mapping>
</web-app>
```



### 八、使用 IDEA 创建 Servlet 程序

菜单：new ->Servlet

![image-20211106083213214](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211106083213214.png)



配置 Servlet 的信息

![image-20211106083443042](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211106083443042.png)



### 九、Servlet 类的继承体系

![image-20211106083547284](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211106083547284.png)

### 十、ServletConfig 类

- ServletConfig 类从类名上来看，就知道是 Servlet 程序的配置信息类。 

- Servlet 程序和 ServletConfig 对象都是由 Tomcat 负责创建，我们负责使用。 

- Servlet 程序默认是第一次访问的时候创建，ServletConfig 是每个 Servlet 程序创建时，就创建一个对应的 ServletConfig 对 象。

- **ServletConfig 类的三大作用** 
	- 1、可以获取 Servlet 程序的别名 servlet-name 的值 
	- 2、获取初始化参数 init-param 
	- 3、获取 ServletContext 对象



web.xml 中的配置：

```xml
<!-- servlet 标签给 Tomcat 配置 Servlet 程序 -->
<servlet>
	<!--servlet-name 标签 Servlet 程序起一个别名（一般是类名） -->
	<servlet-name>HelloServlet</servlet-name>
	<!--servlet-class 是 Servlet 程序的全类名-->
	<servlet-class>com.atguigu.servlet.HelloServlet</servlet-class>
	<!--init-param 是初始化参数-->
	<init-param>
		<!--是参数名-->
		<param-name>username</param-name>
		<!--是参数值-->
		<param-value>root</param-value>
	</init-param>
	<!--init-param 是初始化参数-->
	<init-param>
		<!--是参数名-->
		<param-name>url</param-name>
		<!--是参数值-->
		<param-value>jdbc:mysql://localhost:3306/test</param-value>
	</init-param>
</servlet>


<!--servlet-mapping 标签给 servlet 程序配置访问地址-->
<servlet-mapping>
	<!--servlet-name 标签的作用是告诉服务器，我当前配置的地址给哪个 Servlet 程序使用-->
	<servlet-name>HelloServlet</servlet-name>
	<!--
		url-pattern 标签配置访问地址 <br/>
		/ 斜杠在服务器解析的时候，表示地址为：http://ip:port/工程路径 <br/>
		/hello 表示地址为：http://ip:port/工程路径/hello <br/>
	-->
	<url-pattern>/hello</url-pattern>
</servlet-mapping>
```

Servlet 中的代码：

```java
@Override
public void init(ServletConfig servletConfig) throws ServletException {
	System.out.println("2 init 初始化方法");
	// 1、可以获取 Servlet 程序的别名 servlet-name 的值
	System.out.println("HelloServlet 程序的别名是:" + servletConfig.getServletName());
	
    // 2、获取初始化参数 init-param
	System.out.println("初始化参数 username 的值是;"+	     servletConfig.getInitParameter("username"));
	
    System.out.println("初始化参数 url 的值是;" + servletConfig.getInitParameter("url"));
	
    // 3、获取 ServletContext 对象
	System.out.println(servletConfig.getServletContext());
}
```



**注意：**

![image-20211106173741114](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211106173741114.png)



### 十一、ServletContext 类

- 什么是 ServletContext? 

	- 1、ServletContext 是一个接口，它表示 Servlet 上下文对象 
	- 2、一个 web 工程，只有一个 ServletContext 对象实例。 
	- 3、ServletContext 对象是一个域对象。 
	- 4、**ServletContext 是在 web 工程部署启动的时候创建。在 web 工程停止的时候销毁。** 
	- 5、相当于存在内存中，创建就存在，工程结束就没了。可以被同一工程下其他Servlet程序读取

- 什么是域对象? 

	- 域对象，是可以像 Map 一样存取数据的对象，叫域对象。 

	- 这里的域指的是存取数据的操作范围，整个 web 工程。 

		

|        | 存数据         | 取数据         | 删除数据           |
| ------ | -------------- | -------------- | ------------------ |
| Map    | put()          | get()          | remove()           |
| 域对象 | setAttribute() | getAttribute() | removeAttribute(); |



- **ServletContext 类的四个作用** 

	- 1、获取 web.xml 中配置的上下文参数 context-param 

		```java
		public class ContextServlet extends HttpServlet {
		    @Override
		    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		        ServletContext context = getServletConfig().getServletContext();
		        // 1、获取 web.xml 中配置的上下文参数 context-param
		        String username = context.getInitParameter("username");
		        String password = context.getInitParameter("password");
		        System.out.println("context-param参数：username的值是" + username);
		        System.out.println("context-param参数：password的值是" + password);
		        //context-param参数：username的值是张无忌
		        //context-param参数：password的值是赵敏
		    }
		}
		```

	- 2、获取当前的工程路径，格式: /工程路径 

		```java
		public class ContextServlet extends HttpServlet {
		    @Override
		    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		        ServletContext context = getServletConfig().getServletContext();
		        // 2、获取当前的工程路径，格式: /工程路径
		        System.out.println("当前的工作路径是：" + context.getContextPath());//当前的工作路径是：/DynamicWeb
		    }
		}
		```

	- 3、获取工程部署后在服务器硬盘上的绝对路径 

		```java
		public class ContextServlet extends HttpServlet {
		    @Override
		    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		        ServletContext context = getServletConfig().getServletContext();
		        // 3、获取工程部署后在服务器硬盘上的绝对路径
		        // / 斜杠被服务器解析地址为：http://ip:port/工程名/
		        // 映射到IDEA代码的target\DynamicWeb-1.0-SNAPSHOT目录，取其中其他内容，在后边填写【相对路径】就可以了
		        System.out.println("工程部署的硬盘路径是：" + context.getRealPath("/"));
		        
		//        工程部署的硬盘路径是：E:\computer\Java\JavaWebLearn\DynamicWeb\target\DynamicWeb-1.0-SNAPSHOT\
		        
		        System.out.println("本工程lib目录硬盘路径是：" + context.getRealPath("/WEB-INF/lib"));
		        
		//        本工程lib目录硬盘路径是：E:\computer\Java\JavaWebLearn\DynamicWeb\target\DynamicWeb-1.0-SNAPSHOT\WEB-INF\lib
		    }
		}
		```

	- 4、像 Map 一样存取数据

	```java
	public class ContextServlet extends HttpServlet {
	    @Override
	    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
	        ServletContext context = getServletConfig().getServletContext();
	        
	        // 4、像 Map 一样存取数据
	        System.out.println("context 未创建之前 获取key1 的值是：" + context.getAttribute("key1"));
	        
	        context.setAttribute("key1","value1");
	
	        System.out.println("context 中获取域数据key1 的值是：" + context.getAttribute("key1"));
	        // context context 未创建之前 获取key1 的值是：null【第一遍 还没创建】
	        // context 中获取域数据key1 的值是：value1
	        // context context 未创建之前 获取key1 的值是：value1【第二遍，未结束工程，此时刷新已经创建了，所以存在】
	        // context 中获取域数据key1 的值是：value1【也可以在其Servlet程序中获取到，只要创建了，他是存在整个web工程下的】
	    }
	}
	```

![image-20211106190611743](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211106190611743.png)



### 十二、HttpServletRequest 类  

##### 1、HttpServletRequest 类的作用。

每次只要有请求进入 Tomcat 服务器， Tomcat 服务器就会把请求过来的 HTTP 协议信息解析好封装到 Request 对象中。
然后传递到 service 方法（ doGet 和 doPost） 中给我们使用。 我们可以通过 HttpServletRequest 对象， 获取到所有请求的信息。

##### 2、HttpServletRequest 类的常用方法

- getRequestURI() 				获取请求的资源路径

- getRequestURL()				获取请求的统一资源定位符（绝对路径）

- getRemoteHost() 			   获取客户端的 ip 地址

- getHeader() 						获取请求头

- getParameter() 				  获取请求的参数
- getParameterValues() 	  获取请求的参数（多个值的时候使用）
- getMethod()					    获取请求的方式 GET 或 POST
- setAttribute(key, value)	 设置域数据
- getAttribute(key)			    获取域数据
- getRequestDispatcher()    获取请求转发对象

常见的API代码展示

```java
public class RequestAPIServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
//         getRequestURI()              获取请求的资源路径
        System.out.println("URI =>" + req.getRequestURI());
//         getRequestURL()          获取请求的统一资源定位符（绝对路径）
        System.out.println("URL =>" + req.getRequestURL());
//         getRemoteHost()              获取客户端的 ip 地址
        // 在IDEA中，使用localhost 访问时，得到的客户端地址是 -----> 127.0.0.1
        // 在IDEA中，使用127.0.0.1 访问时，得到的客户端地址是 -----> 127.0.0.1
        // 在IDEA中，使用222.19.66.113 访问时，得到的客户端地址是 -----> 222.19.66.113【真实的本机地址】
        System.out.println("客户端  IP地址 =>" + req.getRemoteHost());
//         getHeader()                    获取请求头
        System.out.println("请求头User-Agent =>" + req.getHeader("User-Agent"));
//         getMethod()                 获取请求的方式 GET 或 POST
        System.out.println("请求方式是 =>" + req.getMethod());
//
    }
}
```





![image-20211108083517105](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211108083517105.png)



##### 3、如何获取请求参数

**表单：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <form action="http://localhost:8080/07_Servlet/parameterServlet" method="get">
        用户名:<input type="text" name="username"><br/>
        密码：<input type="text" name="password"><br/>
        兴趣爱好：
        <input type="checkbox" name="hobby" value="C++">C++
        <input type="checkbox" name="hobby" value="Java">Java
        <input type="checkbox" name="hobby" value="Python">Python<br/>
        <input type="submit">
    </form>

</body>
</html>
```

**Java代码：**

```java
public class parameterServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        // 获取请求参数        
        String name = request.getParameter("username");
        String password = request.getParameter("password");
        String hobby = request.getParameter("hobby");// 仅选中一个
        String[] hobbies = request.getParameterValues("hobby");// 选中多个时，返回数组

        System.out.println("用户名：" + name);
        System.out.println("密码：" + password);
        System.out.println("兴趣爱好：" + hobby);
        System.out.println("兴趣爱好：" + Arrays.toString(hobbies));// 兴趣爱好：[C++, Java, Python]
        System.out.println("兴趣爱好：" + Arrays.asList(hobbies));// 兴趣爱好：[C++, Java, Python]

    }
}
```



##### 4、doGet 、doPost请求的中文乱码解决：  

- doGet

```java
// 获取请求参数
String username = req.getParameter("username");
//1 先以 iso8859-1 进行编码
//2 再以 utf-8 进行解码
username = new String(username.getBytes("iso-8859-1"), "UTF-8");
```

- doPost

```java
// 设置请求体的字符集为 UTF-8， 从而解决 post 请求的中文乱码问题
req.setCharacterEncoding("UTF-8"); // 必须在获取参数请求之前设置 

// 获取请求参数
String username = req.getParameter("username");
```

##### 5、请求的转发

请求转发是指， 服务器收到请求后， 从一次资源跳转到另一个资源的操作叫请求转发。

**请求转发的特点：**

- 实现了跳转页面，但是浏览器地址栏没有发生变化
- 他们虽然跳转了，但是是一次请求
- 他们共享Request 域中的数据
- 通过转发可以打开WEB-INF目录下的 文件【直接访问是不能访问WEB-INF中的文件的】
- 不能访问工程文件之外的内容，如：www.baidu.com

![image-20211108091640386](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211108091640386.png)

![image-20211108103139155](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211108103139155.png)



**Servlet1 代码：**

```java
public class Servlet1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 1、获取请求参数
        String username = request.getParameter("username");

        // 2、加盖Servlet1 的章
        request.setAttribute("key1","我柜台1 给盖章通过了");

        // 3、获取跳转 Servlet2 的路径
        // 请求转发路径必须要用斜杠打头，斜杠/表示：http://ip:port/工程名/   ,映射代码到webapps目录
        // RequestDispatcher requestDispatcher = request.getRequestDispatcher("/servlet2");
        // 网址访问不支持访问，WEB-INF目录下的文件，但是通过请求转发，可以实现访问
        RequestDispatcher requestDispatcher = request.getRequestDispatcher("/WEB-INF/form.html");

        // 4、 前往Servlet2 办理相关业务
        requestDispatcher.forward(request,response);
    }

}
```



**Servlet2 代码：**

```java
public class Servlet2 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 1、获取相关参数
        String username = request.getParameter("username");

        // 2、检查是否有servlet1 的章
        Object key1 = request.getAttribute("key1");
        System.out.println("你的章拿出来我看看！" + key1);

        // 3、处理servlet2 自己的业务
        System.out.println("好的，那我就继续给你办业务吧");
    }
}
```



##### 6、base 标签的作用

【就是相对路径的标准，让相对路径不根据地址栏变化，根据base标签变化】

假如想实现页面跳转

index.html文件的原地址为http://localhost:8080/07_servlet/index.html，

点击后目标地址为：http://localhost:8080/07_servlet/a/b/c.html

点击跳转后，c.html文件中，有两种方式进行跳回

- 方式一：直接写目标路径为../../index.html

	- 【这样就返回返回两次，最终实际访问地址为：http://localhost:8080/07_servlet/index.html】

- 方式二：用请求转发

	- 【但是！！！！！请求转发地址栏不变，你用两次../../地址就变成：http://localhost:8080/index.html】这成啥了？工程名都给干没了

	- 这时候就需要base标签【相对路径，参照地址，不再参照地址栏】

	- <head>
			<meta charset="UTF-8">
			<title>Title</title>
			<!--base 标签设置页面相对路径工作时参照的地址
				href 属性就是参数的地址值
			-->
			<base href="http://localhost:8080/07_servlet/a/b/">
		</head>

- 在实际开发中， 路径都使用绝对路径， 而不简单的使用相对路径。
	1、 绝对路径
	2、 base+相对  

![image-20211108104819541](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211108104819541.png)

![image-20211108104834681](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211108104834681.png)

```html
<!DOCTYPE html>
<html lang="zh_CN">
<head>
	<meta charset="UTF-8">
	<title>Title</title>
	<!--base 标签设置页面相对路径工作时参照的地址
		href 属性就是参数的地址值
	-->
	<base href="http://localhost:8080/07_servlet/a/b/">
</head>
<body>
	这是 a 下的 b 下的 c.html 页面<br/>
	<a href="../../index.html">跳回首页</a><br/>
</body>
</html>
```



##### 7、Web 中 / 斜杠的不同意义

在 web 中 / 斜杠 是一种绝对路径。

- <font color='red'>/ 斜杠 如果被浏览器解析</font>， 得到的地址是： http://ip:port/

```html
<a href="/">斜杠</a>
```

- <font color='red'>/ 斜杠 如果被服务器解析</font>， 得到的地址是： http://ip:port/工程路径
	- 1、 <url-pattern>/servlet1</url-pattern>
	- 2、 servletContext.getRealPath(“/”);
	- 3、 request.getRequestDispatcher(“/”);
- <font color='red'>**特殊情况**</font>： response.sendRediect(“/”); 把斜杠发送给浏览器解析。 得到 http://ip:port/  



### 十三、HttpServletResponse 类

#### 1、HttpServletResponse 类的作用

HttpServletResponse 类和 HttpServletRequest 类一样。 每次请求进来， Tomcat 服务器都会创建一个 Response 对象传递给 Servlet 程序去使用。 

- HttpServletRequest 表示请求过来的信息
- HttpServletResponse 表示所有响应的信息，

我们如果需要设置返回给客户端的信息， 都可以通过 HttpServletResponse 对象来进行设置

#### 2、两个输出流的说明。



| 字节流     | getOutputStream(); | 常用于下载（传递二进制数据） |
| ---------- | ------------------ | ---------------------------- |
| **字符流** | **getWriter();**   | **常用于回传字符串（常用）** |

两个流同时只能使用一个。

使用了字节流， 就不能再使用字符流， 反之亦然， 否则就会报错。

![image-20211108160747569](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211108160747569.png)

![image-20211108160728337](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211108160728337.png)



#### 3、如何往客户端回传数据

要求 ： 往客户端回传 字符串 数据。  

```java
public class ResponeIOServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 要求 ： 往客户端回传 字符串 数据。
        PrintWriter writer = response.getWriter();
        writer.write("这是返回的字符串【中文会乱码，下面有设置方法】");
    }
}
```



#### 4、响应的乱码解决

解决响应中文乱码方案一（<font color= 'red'>不推荐使用</font>） ：  

```java
// 1、设置服务器字符集为 UTF-8
response.setCharacterEncoding("UTF-8");

// 2、通过响应头， 设置浏览器也使用 UTF-8 字符集
response.setHeader("Content-Type", "text/html; charset=UTF-8");
```

应用：

```java
public class ResponeIOServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
// 解决响应中文乱码方案一
        // 1、设置服务器字符集为 UTF-8
        response.setCharacterEncoding("UTF-8");

        // 2、通过响应头， 设置浏览器也使用 UTF-8 字符集
        response.setHeader("Content-Type", "text/html; charset=UTF-8");
        
        // 要求 ： 往客户端回传 字符串 数据。
        PrintWriter writer = response.getWriter();
        writer.write("这是返回的字符串!");
    }
}
```



解决响应中文乱码方案二（<font color= 'red'>推荐使用</font>） ：  

```java
// 它会同时设置服务器和客户端都使用 UTF-8 字符集， 还设置了响应头
// 注意！！！：此方法一定要在获取流对象之前调用才有效
response.setContentType("text/html; charset=UTF-8");
```

应用：

```java
public class ResponeIOServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
// 解决响应中文乱码方案二
        
        // 它会同时设置服务器和客户端都使用 UTF-8 字符集， 还设置了响应头
        // 注意！！！：此方法一定要在获取流对象之前调用才有效
        response.setContentType("text/html; charset=UTF-8");
        
        
        // 要求 ： 往客户端回传 字符串 数据。
        PrintWriter writer = response.getWriter();
        writer.write("这是返回的字符串!");
    }
}
```

解决乱码后的，显式效果，不再乱码



![image-20211108162124653](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211108162124653.png)

#### 5、请求重定向

请求重定向， 是指客户端给服务器发请求， 然后服务器告诉客户端说。 我给你一个新的地址。 你去新地址访问。 叫请求重定向（因为之前的地址可能已经被废弃） 。  

**请求重定向的特点：**

- 浏览器地址栏会发生变化
- 两次请求
- 不共享Request域中的数据
- 不能访问WEN-INF下的资源
- 可以访问工程外的资源

![image-20211108161013362](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211108161013362.png)



请求重定向的第一种方案：  

```java
// 设置响应状态码 302 ， 表示重定向， （已搬迁）
resp.setStatus(302);
// 设置响应头， 说明 新的地址在哪里
resp.setHeader("Location", "http://localhost:8080");
```

请求重定向的第二种方案（<font color='red'>推荐使用</font>） ：

```java
resp.sendRedirect("http://localhost:8080");
```



**应用：**

response1 程序代码【表示已废弃的】

```java
public class Response1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("程序来过response1 程序");

        // 方式一：
        // 设置响应状态码302，表示重定向（已搬迁）
        response.setStatus(302);
        // 设置响应头，说明 新的地址在哪里
        response.setHeader("Location","http://localhost:8080/07_Servlet/response2");

        
        // 方式二：
        response.sendRedirect("http://localhost:8080/07_Servlet/response2");
    }
}
```

response2 程序代码【表示要跳转的，重定向地址】

```java
public class Response2 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("成功运行重定向，已到response2 程序中");
    }
}
```



## 第9章 HTTP

### 什么是协议?

- 协议是指双方，或多方，相互约定好，大家都需要遵守的规则，叫协议。

- 所谓 HTTP 协议，就是指，客户端和服务器之间通信时，发送的数据，需要遵守的规则，叫 HTTP 协议。 
- HTTP 协议中的数据又叫报文。 

### 请求的 HTTP 协议格式 

- 客户端给服务器发送数据叫请求。 
- 服务器给客户端回传数据叫响应。 
- 请求又分为 GET 请求，和 POST 请求两种



- GET 请求 
- 1、请求行 
	- (1) 请求的方式                   GET 
	- (2) 请求的资源路径           [+?+请求参数] 
	- (3) 请求的协议的版本号     HTTP/1.1 
- 2、请求头 
	- key : value 组成 不同的键值对，表示不同的含义。

![image-20211106221245762](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211106221245762.png)



- POST 请求 

- 1、请求行 

	- (1) 请求的方式                        POST 
	- (2) 请求的资源路径                [+?+请求参数] 
	- (3) 请求的协议的版本号        HTTP/1.1 

- 2、请求头 

	- key : value 不同的请求头，有不同的含义 

		空行 

- 3、请求体 ===>>> 就是发送给服务器的数

![image-20211106221454790](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211106221454790.png)



**常用请求头的说明** 

- Accept: 表示客户端可以接收的数据类型 
- Accpet-Language: 表示客户端可以接收的语言类型 
- User-Agent: 表示客户端浏览器的信息 
- Host： 表示请求时的服务器 ip 和端口号 

**哪些是 GET 请求，哪些是 POST 请求** 

- GET 请求有哪些： 
	- form 标签 method=get 
	- a 标签 
	- link 标签引入 css 
	- Script 标签引入 js 文件 
	- img 标签引入图片 
	- iframe 引入 html 页面 
	- 在浏览器地址栏中输入地址后敲回车 
- POST 请求有哪些： 
	- form 标签 method=post

### 响应的 HTTP 协议格式

- 1、响应行 

	- (1) 响应的协议和版本号 
	- (2) 响应状态码 
	- (3) 响应状态描述符 

- 2、响应头 

	- (1) key : value 不同的响应头，有其不同含义 

		空行 

- 3、响应体 ---->>> 就是回传给客户端的数据

![image-20211106230013468](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211106230013468.png)

### 常用的响应码说明 

- 200 表示请求成功 

- 302 表示请求重定向

- 404 表示请求服务器已经收到了，但是你要的数据不存在（请求地址错误） 

- 500 表示服务器已经收到请求，但是服务器内部错误（代码错误） 

	

### MIME 类型说明 

- MIME 是 HTTP 协议中数据类型。 

- MIME 的英文全称是"Multipurpose Internet Mail Extensions" 多功能 Internet 邮件扩充服务。
- MIME 类型的格式是“大类型/小 类型”，并与某一种文件的扩展名相对应。 

**常见的 MIME**

![image-20211106230231249](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211106230231249.png)

![image-20211106230243108](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211106230243108.png)

**谷歌浏览器如何查看 HTTP 协议：**

![image-20211106230324305](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211106230324305.png)

**火狐浏览器如何查看 HTTP 协议:**

![image-20211106230401012](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211106230401012.png)





## 第10章 Java Server Page【jsp】

### 1、jsp的作用

- 代替 Servlet 程序回传 html 页面的数据。

- 因为 Servlet 程序回传 html 页面数据是一件非常繁锁的事情。 开发成本和维护成本都极高。  

#### 通过Servlet回传一个html页面：

```java
package com.tianhao.jsp_08; /**
 * @ClassName ${NAME}
 * @Description TODO:
 * @Author sth_199509@163.com
 * @Date 2021/11/9 10:37
 * @Version 1.0
 */

import javax.servlet.*;
import javax.servlet.http.*;
import java.io.IOException;
import java.io.PrintWriter;

public class PrintHtmlServlet extends HttpServlet {
    @Override
    protected void  doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 通过响应的回传流回传html的页面数据
        PrintWriter writer = response.getWriter();
        response.setContentType("text/html;charset=UTF-8");

        writer.write("<!DOCTYPE html>\r\n");
        writer.write("<html lang=\"en\">\r\n");
        writer.write("<head>\r\n");
        writer.write("    <meta charset=\"UTF-8\">\r\n");
        writer.write("    <title>Title</title>\r\n");
        writer.write("</head>\r\n");
        writer.write("<body>\r\n");
        writer.write("        这是html页面\r\n");
        writer.write("</body>\r\n");
        writer.write("</html>\r\n");
    }
}
```

#### 通过jsp回传html页面

创建一个jsp文件，地址栏访问他就可以了

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
<title>Title</title>
</head>
<body>
这是 html 页面数据
</body>
</html>
```

### 2、jsp文件的访问

jsp文件和html文件一样，都是存放在webapp 目录下，访问也跟访问html 一样。

a.html 页面			访问地址是 =======>>>>>> http://ip:port/工程路径/a.html

 b.jsp 页面				访问地址是 =======>>>>>> http://ip:port/工程路径/b.jsp

地址栏直接输入就能访问 



### 3、jsp 的本质是什么

**jsp 页面本质上是一个 Servlet 程序。**

当我们第一次访问 jsp 页面的时候。 Tomcat 服务器会帮我们把 jsp 页面翻译成为一个 java 源文件。 并且对它进行编译成为.class 字节码程序。 我们打开 java 源文件不难发现其里面的内容是：  

![image-20211109111456079](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211109111456079.png)



我们跟踪原代码发现， HttpJspBase 类。 它直接地继承了 HttpServlet 类。 也就是说。 jsp 翻译出来的 java 类， 它间接了继承了 HttpServlet 类。 也就是说， 翻译出来的是一个 Servlet 程序  

![image-20211109111516838](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211109111516838.png)

**总结： 通过翻译的 java 源代码我们就可以得到结果： jsp 就是 Servlet 程序。**

大家也可以去观察翻译出来的 Servlet 程序的源代码， 不难发现。 其底层实现， 也是通过输出流。 把 html 页面数据回传给客户端。  



```jsp
public void _jspService(final javax.servlet.http.HttpServletRequest request, final
javax.servlet.http.HttpServletResponse response)
	throws java.io.IOException, javax.servlet.ServletException {
	final java.lang.String _jspx_method = request.getMethod();
	if (!"GET".equals(_jspx_method) && !"POST".equals(_jspx_method) && !"HEAD".equals(_jspx_method)
&& !javax.servlet.DispatcherType.ERROR.equals(request.getDispatcherType())) {response.sendError(HttpServletResponse.SC_METHOD_NOT_ALLOWED, "JSPs only permit GET POST or HEAD");
		return;
	} 
	final javax.servlet.jsp.PageContext pageContext;
	javax.servlet.http.HttpSession session = null;
	final javax.servlet.ServletContext application;
	final javax.servlet.ServletConfig config;
	javax.servlet.jsp.JspWriter out = null;
	final java.lang.Object page = this;
	javax.servlet.jsp.JspWriter _jspx_out = null;
	javax.servlet.jsp.PageContext _jspx_page_context = null;
	try {
		response.setContentType("text/html;charset=UTF-8");
		pageContext = _jspxFactory.getPageContext(this, request, response,null, true, 8192, true);
		_jspx_page_context = pageContext;
		application = pageContext.getServletContext();
		config = pageContext.getServletConfig();
        session = pageContext.getSession();
        out = pageContext.getOut();
        _jspx_out = out;
        out.write("\r\n");
        out.write("\r\n");
        out.write("<html>\r\n");
        out.write("<head>\r\n");
        out.write(" <title>Title</title>\r\n");
        out.write("</head>\r\n");
        out.write("<body>\r\n");
        out.write(" a.jsp 页面\r\n");
        out.write("</body>\r\n");
        out.write("</html>\r\n");
	} catch (java.lang.Throwable t) {
        if (!(t instanceof javax.servlet.jsp.SkipPageException)){
            out = _jspx_out;
            if (out != null && out.getBufferSize() != 0)
                try {
                if (response.isCommitted()) {
                	out.flush();
                } else {
                	out.clearBuffer();
                }
                } catch (java.io.IOException e) {}
		if (_jspx_page_context != null) _jspx_page_context.handlePageException(t);
		else throw new ServletException(t);}
	} finally {
		_jspxFactory.releasePageContext(_jspx_page_context);
	}
}
```



### 4、jsp 的三种语法

#### 4.1、jsp 头部的 page 指令  

jsp 的 page 指令可以修改 jsp 页面中一些重要的属性， 或者行为。  

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
```



- language 属性   				表示 jsp 翻译后是什么语言文件。 暂时只支持 java。
- contentType 属性 		    表示 jsp 返回的数据类型是什么。 也是源码中 response.setContentType()参数值
- pageEncoding 属性          表示当前 jsp 页面文件本身的字符集。
- import 属性                       跟 java 源代码中一样。 用于导包， 导类。

========================两个属性是给 out 输出流使用=============================

- autoFlush 属性                  设置当 out 输出流缓冲区满了之后， 是否自动刷新冲级区。 默认值是 true。
- buffer 属性                         设置 out 缓冲区的大小。 默认是 8kb

**缓冲区溢出错误：**  

![image-20211109112204784](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211109112204784.png)

========================两个属性是给 out 输出流使用=============================

- errorPage 属性               设置当 jsp 页面运行时出错， 自动跳转去的错误页面路径。

	- ```html
		<!--
		errorPage 表示错误后自动跳转去的路径 <br/>
		这个路径一般都是以斜杠打头， 它表示请求地址为 http://ip:port/工程路径/映射到代码的 Web 目录
		-->
		```

- isErrorPage 属性             设置当前 jsp 页面是否是错误信息页面。 默认是 false。 如果是 true 可以获取异常信息。
- session 属性                     设置访问当前 jsp 页面， 是否会创建 HttpSession 对象。 默认是 true。
- extends 属性                     设置 jsp 翻译出来的 java 类默认继承谁。



#### 4.2、jsp 中的常用脚本

##### 4.2.1、声明脚本(<font color='red'>极少使用</font>)  

- 声明脚本的格式是： <%! 声明 java 代码 %>
- 作用： 可以给 jsp 翻译出来的 java 类定义属性和方法甚至是静态代码块。 内部类等。  

**【百分号跟！是声明，=是表达式，什么都没有 代码脚本】**

- 练习：
	1、 声明类属性
	2、 声明 static 静态代码块
	3、 声明类方法
	4、 声明内部类  

```jsp
<%--1、 声明类属性--%>
    <%!
        private Integer id;
        private String name;
        private static Map<String,Object> map;
    %>
<%--2、 声明 static 静态代码块--%>
    <%!
        static {
            map = new HashMap<String,Object>();
            map.put("key1", "value1");
            map.put("key2", "value2");
            map.put("key3", "value3");
        }
    %>
<%--3、 声明类方法--%>
    <%!
        public int abc(){
        	return 12;
        }
    %>
<%--4、 声明内部类--%>
    <%!
        public static class A {
        private Integer id = 12;
        private String abc = "abc";
    }
    %>
```



声明脚本代码翻译对照：  

![image-20211109112933437](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211109112933437.png)

##### 4.2.2、表达式脚本（<font color='red'>常用</font>）

- 表达式脚本的格式是： <%=表达式%>

- 表达式脚本的作用是： 的 jsp 页面上输出数据。

- 表达式脚本的特点：

	- 1、 所有的表达式脚本都会被翻译到_jspService() 方法中
	- 2、 表达式脚本都会被翻译成为 out.print()输出到页面上
	- 3、 由于表达式脚本翻译的内容都在_jspService() 方法中,所以_jspService()方法中的对象都可以直接使用。
	- 4、 表达式脚本中的表达式不能以分号结束。

- 练习：

	- 输出整型

	- 输出浮点型

	- 输出字符串

	- 输出对象  



示例代码：  

```jsp
<%=12 %> <br>
<%=12.12 %> <br>
<%="我是字符串" %> <br>
<%=map%> <br>
<%=request.getParameter("username")%>
```

翻译对照：  

![image-20211109113234611](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211109113234611.png)



##### 4.2.3、代码脚本

- 代码脚本的格式是：

```jsp
<%
	java 语句
%>
```

- 代码脚本的作用是： 可以在 jsp 页面中， 编写我们自己需要的功能（写的是 java 语句） 。
- 代码脚本的特点是：
	- 1、 代码脚本翻译之后都在_jspService 方法中
	- 2、 代码脚本由于翻译到_jspService()方法中， 所以在_jspService()方法中的现有对象都可以直接使用。
	- 3、 还可以由多个代码脚本块组合完成一个完整的 java 语句。
	- 4、 代码脚本还可以和表达式脚本一起组合使用， 在 jsp 页面上输出数据
- 练习：
	- \1. 代码脚本----if 语句
	- \2. 代码脚本----for 循环语句
	- \3. 翻译后 java 文件中_jspService 方法内的代码都可以写
- 示例代码：  

```jsp
<%--练习： --%>
<%--1.代码脚本----if 语句--%>
    <%
        int i = 13 ;
        if (i == 12) {
    %>
        <h1>国哥好帅</h1>
    <%
        } else {
    %>
        <h1>国哥又骗人了！ </h1>
    <%
        }
    %>
    <br>
<%--2.代码脚本----for 循环语句--%>
    <table border="1" cellspacing="0">
        <%
            for (int j = 0; j < 10; j++) {
        %>
        <tr>
            <td>第 <%=j + 1%>行</td>
        </tr>
        <%
            }
        %>
    </table>
<%--3.翻译后 java 文件中_jspService 方法内的代码都可以写--%>
    <%
        String username = request.getParameter("username");
        System.out.println("用户名的请求参数值是： " + username);
    %>
```



**翻译之后的对比：**

![image-20211109114049644](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211109114049644.png)

#### 4.3、jsp 中的三种注释

- html 注释

	- html 注释会被翻译到 java 源代码中。 在_jspService 方法里， 以 out.writer 输出到客户端。

	```jsp
	<!-- 这是 html 注释 -->
	```

- java 注释  

	- java 注释会被翻译到 java 源代码中。

	```jsp
	<%
		// 单行 java 注释
		/* 多行 java 注释 */
	%>
	```

-   jsp 注释

	- jsp 注释可以注掉， jsp 页面中所有代码。  

	```jsp
	<%-- 这是 jsp 注释 --%>
	```

### 5、jsp 九大内置对象

jsp 中的内置对象， 是指 Tomcat 在翻译 jsp 页面成为 Servlet 源代码后， 内部提供的九大对象， 叫内置对象。  

- request				请求对象
- response 			响应对象
- pageContext	   jsp的上下文对象
- session				会话对象
- application 		 ServletContext对象
- config 				  ServletConfig对象
- out						jsp输出流对象
- page					 指向当前的jsp的对象
- exception			异常对象

![image-20211109114509673](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211109114509673.png)



### 6、jsp 四大域对象

四个域对象分别是：

- pageContext     
	-  (PageContextImpl 类) 【当前 jsp 页面范围内有效】

- request 
	- (HttpServletRequest 类)【 一次请求内有效】

- session 
	- (HttpSession 类)【 一个会话范围内有效（打开浏览器访问服务器， 直到关闭浏览器）】

- application 
	- (ServletContext 类) 【整个 web 工程范围内都有效（只要 web 工程不停止， 数据都在）】

- 域对象是可以像 Map 一样存取数据的对象。 四个域对象功能一样。 不同的是它们对数据的存取范围。
- 虽然四个域对象都可以存取数据。 在使用上它们是有优先顺序的。
- 四个域在使用的时候， 优先顺序分别是， 他们从小到大的范围的顺序。
	- pageContext ====>>> request ====>>> session ====>>> application




scope.jsp 页面

```jsp
<body>
    <h1>scope.jsp 页面</h1>
    <%
        // 往四个域中都分别保存了数据
        pageContext.setAttribute("key", "pageContext");
        request.setAttribute("key", "request");
        session.setAttribute("key", "session");
        application.setAttribute("key", "application");
    %>
    pageContext 域是否有值： <%=pageContext.getAttribute("key")%> <br>
    request 域是否有值： <%=request.getAttribute("key")%> <br>
    session 域是否有值： <%=session.getAttribute("key")%> <br>
    application 域是否有值： <%=application.getAttribute("key")%> <br>
    <%
    request.getRequestDispatcher("/scope2.jsp").forward(request,response);
    %>
</body>
```



scope2.jsp 页面

```jsp
<body>
    <h1>scope2.jsp 页面</h1>
    pageContext 域是否有值： <%=pageContext.getAttribute("key")%> <br>
    request 域是否有值： <%=request.getAttribute("key")%> <br>
    session 域是否有值： <%=session.getAttribute("key")%> <br>
    application 域是否有值： <%=application.getAttribute("key")%> <br>
</body>
```



### 7、jsp 中的 out 输出和 response.getWriter 输出的区别  

- **response** 中表示响应， 我们经常用于设置返回给客户端的内容（输出）
- **out** 也是给用户做输出使用的。  

![image-20211109190511841](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211117122315217.png)

由于 jsp 翻译之后， 底层源代码都是使用 out 来进行输出， 所以一般情况下。 我们在 jsp 页面中统一使用 out 来进行输出。 避免打乱页面输出内容的顺序。  

- <font color='red'>out.write()</font> 输出字符串没有问题【只能输出字符串，其他类型不能输出】
- <font color='red'>out.print() </font>输出任意数据都没有问题【任何类型都转换成为字符串后调用的 write 输出】

深入源码， 浅出结论： <font color='red'>在 jsp 页面中， 可以统一使用 out.print()来进行输出</font>

### 8、jsp 的常用标签

#### 8.1、jsp 静态包含

就是单独写一个jsp文件【相当于一个函数】展示一个内容，假设为内容A

任何其他地方需要用到内容A的地方，使用静态包含直接调用

这样如果需要修改内容A，直接改它的jsp文件就行了，其他成百上千的调用者，显示内容都改了

 **静态包含的特点：**
    1、 静态包含不会翻译被包含的 jsp 页面。
    2、 静态包含其实是把被包含的 jsp 页面的代码拷贝到包含的位置执行输出。

示例说明：

```jsp
<%--
    <%@ include file=""%> 就是静态包含

        file 属性指定你要包含的 jsp 页面的路径
        地址中第一个斜杠 / 表示为 http://ip:port/工程路径/ 映射到代码的 web 目录   
--%>
调用
<%@ include file="/include/footer.jsp"%>
```

#### 8.2、jsp 动态包含



动态包含的特点：
        1、 动态包含会把包含的 jsp 页面也翻译成为 java 代码
        2、 动态包含底层代码使用如下代码去调用被包含的 jsp 页面执行输出。
        JspRuntimeLibrary.include(request, response, "/include/footer.jsp", out, false);
        3、 动态包含， 还可以传递参数

示例说明：

```jsp
<%--
    <jsp:include page=""></jsp:include> 这是动态包含
        
    page 属性是指定你要包含的 jsp 页面的路径
    动态包含也可以像静态包含一样。 把被包含的内容执行输出到包含位置
        
--%>
调用
<% 
    JspRuntimeLibrary.include(request, response, "/include/footer.jsp", out, false);
%>
```



```jsp
<jsp:include page="/include/footer.jsp">
    <jsp:param name="username" value="bbj"/>
    <jsp:param name="password" value="root"/>
</jsp:include>
```

动态包含的底层原理：

![image-20211109191052597](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211110203421090.png)

#### 8.3、jsp 标签-转发

示例说明：

```jsp
<%--
    <jsp:forward page=""></jsp:forward> 是请求转发标签， 
        它的功能就是请求转发 page 属性设置请求转发的路径
--%>
<jsp:forward page="/scope2.jsp"></jsp:forward>
```

### 9、jsp 的练习题

#### 9.1、在 jsp 页面中输出九九乘法口诀表

```jsp
<%--
  Created by IntelliJ IDEA.
  User: kingb
  Date: 2021/11/10
  Time: 8:49
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<title>Title</title>
<style type="text/css">

    table{
        width: 650px;
    }

</style>
</head>
<body>
    <%-- 练习一：在jsp页面中输出九九乘法口诀表 --%>
    <h1 align="center">九九乘法口诀表</h1>
    <table align="center">
        <% for (int i = 1; i <= 9; i++) { %>
        <tr>
            <% for (int j = 1; j <= i ; j++) { %>
            <td><%=j + "x" + i + "=" + (i*j)%></td>
            <% } %>
        </tr>
        <% } %>
</table>
</body>
</html>

```

#### 9.2、jsp 输出一个表格， 里面有 10 个学生信息。



![image-20211110091048688](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211110091048688.png)



Student 类：  

```java
public class Student {
private Integer id;
private String name;
private Integer age;
private String phone;
```

SearchStudentServlet 程序：  

```java
public class SearchStudentServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException,IOException {
        // 获取请求的参数
        // 发 sql 语句查询学生的信息
        // 使用 for 循环生成查询到的数据做模拟
        List<Student> studentList = new ArrayList<Student>();
        for (int i = 0; i < 10; i++) {
            int t = i + 1;
            studentList.add(new Student(t,"name"+t, 18+t,"phone"+t));
        } //保存查询到的结果（学生信息） 到 request 域中
        req.setAttribute("stuList", studentList);
        // 请求转发到 showStudent.jsp 页面
        req.getRequestDispatcher("/test/showStudent.jsp").forward(req,resp);
    }
}
```

showStudent.jsp 页面：

```jsp
<%@ page import="java.util.List" %>
<%@ page import="com.atguigu.pojo.Student" %>
<%@ page import="java.util.ArrayList" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
    <style>
        table{
            border: 1px blue solid;
            width: 600px;
            border-collapse: collapse;
        } td,th{
       		border: 1px blue solid;
        }
    </style>
</head>
<body>
    <%--练习二： jsp 输出一个表格， 里面有 10 个学生信息。 --%>
    <%
    	List<Student> studentList = (List<Student>) request.getAttribute("stuList");
    %>
    <table>
        <tr>
            <td>编号</td>
            <td>姓名</td>
            <td>年龄</td>
            <td>电话</td>
            <td>操作</td>
        </tr>
        <% for (Student student : studentList) { %>
            <tr>
                <td><%=student.getId()%></td>
                <td><%=student.getName()%></td>
                <td><%=student.getAge()%></td>
                <td><%=student.getPhone()%></td>
                <td>删除、 修改</td>
            </tr>
        <% } %>
	</table>
</body>
</html>
```



## 第11章 listener 监听器

1、 Listener 监听器它是 JavaWeb 的三大组件之一。 

- JavaWeb 的三大组件分别是： <font color = 'red'>Servlet 程序、 Filter 过滤器、 Listener 监听器</font>。

2、 Listener 它是 JavaEE 的规范， 就是接口

3、 监听器的作用是， 监听某种事物的变化。 然后通过回调函数， 反馈给客户（程序） 去做一些相应的处理。  



### 11.1、ServletContextListener 监听器  

- ServletContextListener 它可以监听 ServletContext 对象的创建和销毁。
- ServletContext 对象在 web 工程启动的时候创建， 在 web 工程停止的时候销毁。
- 监听到创建和销毁之后都会分别调用 ServletContextListener 监听器的方法反馈。



- 两个方法分别是：  

```java
public interface ServletContextListener extends EventListener {
    /**
    * 在 ServletContext 对象创建之后马上调用，做初始化
    */
    public void contextInitialized(ServletContextEvent sce);
    /**
    * 在 ServletContext 对象销毁之后调用
    */
    public void contextDestroyed(ServletContextEvent sce);
}
```

**如何使用 ServletContextListener 监听器监听 ServletContext 对象。**

使用步骤如下：
1、 编写一个类去实现 ServletContextListener
2、 实现其两个回调方法
3、 到 web.xml 中去配置监听器  



监听器实现类：

```java
public class MyServletContextListenerImpl implements ServletContextListener {
    @Override
    public void contextInitialized(ServletContextEvent sce) {
    	System.out.println("ServletContext 对象被创建了");
    } 
    @Override
    public void contextDestroyed(ServletContextEvent sce) {
    	System.out.println("ServletContext 对象被销毁了");
    }
}
```

web.xml 中的配置：  

```xml
<!--配置监听器-->
<listener>
	<listener-class>com.atguigu.listener.MyServletContextListenerImpl</listener-class>
</listener>
```





## 第12章 EL表达式 

### 1、什么是 EL 表达式， EL 表达式的作用?

- EL 表达式的全称是： Expression Language。 是表达式语言。
- EL 表达式的什么作用： EL 表达式主要是代替 jsp 页面中的表达式脚本在 jsp 页面中进行数据的输出。
	因为 EL 表达式在输出数据的时候， 要比 jsp 的表达式脚本要简洁很多。  

```jsp
<body>
    <%
    	request.setAttribute("key","值");
    %>
    	表达式脚本输出 key 的值是：
    	<%=request.getAttribute("key1")==null?"":request.getAttribute("key1")%><br/>
   		
    	EL 表达式输出 key 的值是： ${key1}
</body>
```

**EL 表达式的格式是： ${表达式}**

EL 表达式在输出 null 值的时候， 输出的是空串。 jsp 表达式脚本输出 null 值的时候， 输出的是 null 字符串。  



### 2、EL 表达式搜索域数据的顺序

EL 表达式主要是在 jsp 页面中输出数据。
主要是输出域对象中的数据。

当四个域中都有相同的 key 的数据的时候， EL 表达式会按照四个域的从小到大的顺序去进行搜索， 找到就输出。  

```jsp
<body>
    <%
        //往四个域中都保存了相同的 key 的数据。
        request.setAttribute("key", "request");session.setAttribute("key", "session");
        application.setAttribute("key", "application");
        pageContext.setAttribute("key", "pageContext");
    %>
    ${ key }
</body>
```



### 3、EL 表达式的输出属性

- Bean 的普通属性， 数组属性。
- List 集合属性， map 集合属性  

Person 类：

```java
public class Person {
    // i.需求——输出 Person 类中普通属性， 数组属性。 list 集合属性和 map 集合属性。
    private String name;
    private String[] phones;
    private List<String> cities;
    private Map<String,Object> map;
    
    public int getAge() {
        // 输出 Person 的 age 属性： ${p.age}
        // 没有age属性，只给一个getAge方法，奇迹的是 ${p.age}  可以查到age的值
        // 证明他是通过查getAge方法找到，不会判断你是不是存在该属性
    	return 18;
	}
```

输出的代码：

```html
<body>
    <%
        Person person = new Person();
        person.setName("国哥好帅！ ");
        person.setPhones(new String[]{"18610541354","18688886666","18699998888"});
        List<String> cities = new ArrayList<String>();
        cities.add("北京");
        cities.add("上海");
        cities.add("深圳");
        person.setCities(cities);
        Map<String,Object>map = new HashMap<>();
        map.put("key1","value1");
        map.put("key2","value2");
        map.put("key3","value3");
        person.setMap(map);pageContext.setAttribute("p", person);
    %>
        输出 Person： ${ p }<br/>
        输出 Person 的 name 属性： ${p.name} <br>
        输出 Person 的 pnones 数组属性值： ${p.phones[2]} <br>
        输出 Person 的 cities 集合中的元素值： ${p.cities} <br>
        输出 Person 的 List 集合中个别元素值： ${p.cities[2]} <br>
        输出 Person 的 Map 集合: ${p.map} <br>
        输出 Person 的 Map 集合中某个 key 的值: ${p.map.key3} <br>
        输出 Person 的 age 属性： ${p.age} <br>
</body>
```



### 4、EL 表达式——运算

- 语法： ${ 运算表达式 }

EL 表达式支持如下运算符：  

#### 4.1、关系运算  

![image-20211110203421090](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211109190511841.png)



#### 4.2、逻辑运算

![image-20211110203505516](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211110203505516.png)

#### 4.3、算数运算

![image-20211110204037394](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211110204037394.png)



#### 4.4、empty 运算

**empty 运算可以判断一个数据是否为空， 如果为空， 则输出 true,不为空输出 false。**

以下几种情况为空：
	1、 值为 null 值的时候，为空
	2、 值为空串的时候，为空
	3、 值是 Object 类型数组， 长度为零的时候，为空
	4、 list 集合， 元素个数为零，为空
	5、 map 集合， 元素个数为零，为空

```jsp
<body>
    <%
        // 1、 值为 null 值的时候， 为空
        request.setAttribute("emptyNull", null);
        // 2、 值为空串的时候， 为空
        request.setAttribute("emptyStr", "");
        // 3、 值是 Object 类型数组， 长度为零的时候
        request.setAttribute("emptyArr", new Object[]{});
        // 4、 list 集合， 元素个数为零
        List<String> list = new ArrayList<>();
        // list.add("abc");
        request.setAttribute("emptyList", list);
        // 5、 map 集合， 元素个数为零
        Map<String,Object> map = new HashMap<String, Object>();
        // map.put("key1", "value1");
        request.setAttribute("emptyMap", map);
    %>
    ${ empty emptyNull } <br/>       // true
    ${ empty emptyStr } <br/>        // true
    ${ empty emptyArr } <br/>        // true
    ${ empty emptyList } <br/>       // true
    ${ empty emptyMap } <br/>        // true
</body>
```



#### 4.5、三元运算

表达式 1？ 表达式 2： 表达式 3

如果表达式 1 的值为真， 返回表达式 2 的值， 如果表达式 1 的值为假， 返回表达式 3 的值。

示例：

```jsp
${ 12 != 12 ? "哈哈":"嘻嘻" } // 嘻嘻  
```

#### 4.6、“.”点运算 和 [] 中括号运算符

- .点运算， 可以输出 Bean 对象中某个属性的值。
- []中括号运算， 可以输出有序集合中某个元素的值。
- 并且[]中括号运算， 还可以输出 map 集合中 key 里含有特殊字符的 key 的值。  

本来直接用map.key就可以了
            但是因为key包含其他运算符，直接用点. 就错了

​            如：【map.a.a.a】   这是个啥？？？ 别说计算机，我都不认识
​            所以用中括号加单引号或者双引号包起来，想Python中的字典

```jsp
<body>
    <%
        Map<String,Object> map = new HashMap<String, Object>();
        map.put("key","value");
        map.put("a.a.a", "aaaValue");
        map.put("b+b+b", "bbbValue");
        map.put("c-c-c", "cccValue");
        request.setAttribute("map", map);
    %>
    ${ map.key } <br>          <%--输出：value--%>
    ${ map['a.a.a'] } <br>     <%--输出：aaaValue--%>
    ${ map["b+b+b"] } <br>     <%--输出：bbbValue--%>
    ${ map['c-c-c'] } <br>     <%--输出：cccValue--%>
    <%--    本来直接用map.key就可以了
            但是因为key包含其他运算符，直接用点就错了
            如：map.a.a.a   这是个啥？？？别说计算机，我都不认识
            所以用中括号加单引号或者双引号包起来，想Python中的字典
      --%>
</body>
```

### 5、EL 表达式的 11 个隐含对象

**EL 个达式中 11 个隐含对象， 是 EL 表达式中自己定义的， 可以直接使用。**  

![image-20211110223153437](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211110223153437.png)

### 6、EL 获取四个特定域中的属性  

| **pageScope**        | **pageContext 域**    |
| -------------------- | --------------------- |
| **requestScope**     | **Request 域**        |
| **sessionScope**     | **Session 域**        |
| **applicationScope** | **ServletContext 域** |



```jsp
<body>
    <%
        pageContext.setAttribute("key1", "pageContext1");
        pageContext.setAttribute("key2", "pageContext2");
        request.setAttribute("key2", "request");
        session.setAttribute("key2", "session");
        application.setAttribute("key2", "application");
    %>
    ${ applicationScope.key2 }
</body>
```



### 7、pageContext 对象的使用

1. 协议：

2. 服务器 ip：
3. 服务器端口：
4. 获取工程路径：
5. 获取请求方法：
6. 获取客户端 ip 地址：
7. 获取会话的 id 编号：  



```jsp
<body>
    <%--
        request.getScheme() 它可以获取请求的协议
        request.getServerName() 获取请求的服务器 ip 或域名
        request.getServerPort() 获取请求的服务器端口号
        getContextPath() 获取当前工程路径
        request.getMethod() 获取请求的方式（GET 或 POST）
        request.getRemoteHost() 获取客户端的 ip 地址
        session.getId() 获取会话的唯一标识
    --%>
    <%
    	pageContext.setAttribute("req", request);
    %>
    <%=request.getScheme() %> <br>
    1.协议： ${ req.scheme }<br>底下所有的都可以用req替换掉 pageContext.request，因为上边设置了req
    2.服务器 ip： ${ pageContext.request.serverName }<br>
    3.服务器端口： ${ pageContext.request.serverPort }<br>
    4.获取工程路径： ${ pageContext.request.contextPath }<br>
    5.获取请求方法： ${ pageContext.request.method }<br>
    6.获取客户端 ip 地址： ${ pageContext.request.remoteHost }<br>
    7.获取会话的 id 编号： ${ pageContext.session.id }<br>这个要把表达式脚本改成session.getId
</body>
```

### 8、EL 表达式其他隐含对象的使用

#### 8.1、请求参数

| **param**       | Map<String,String>       | 它可以获取请求参数的值                                |
| --------------- | ------------------------ | ----------------------------------------------------- |
| **paramValues** | **Map<String,String[]>** | **它也可以获取请求参数的值， 获取多个值的时候使用。** |

示例代码：

```jsp
输出请求参数 username 的值： ${ param.username } <br>
输出请求参数 password 的值： ${ param.password } <br>
输出请求参数 username 的值： ${ paramValues.username[0] } <br>
输出请求参数 hobby 的值： ${ paramValues.hobby[0] } <br>
输出请求参数 hobby 的值： ${ paramValues.hobby[1] } <br>
```

#### 8.2、请求地址  

| header           | Map<String,String>       | 它可以获取请求头的信息                                |
| ---------------- | ------------------------ | ----------------------------------------------------- |
| **headerValues** | **Map<String,String[]>** | **它可以获取请求头的信息， 它可以获取多个值的情况  ** |

http://localhost:8080/09_EL_JSTL/other_el_obj.jsp?username=wzg168&password=666666&hobby=java&hobby=cpp  

示例代码：  

```jsp
输出请求头【User-Agent】 的值： ${ header['User-Agent'] } <br>
输出请求头【Connection】 的值： ${ header.Connection } <br>
输出请求头【User-Agent】 的值： ${ headerValues['User-Agent'][0] } <br>
```



#### 8.3、请求cookie

| cookie | Map<String,Cookie> | 它可以获取当前请求的 Cookie 信息 |
| ------ | ------------------ | -------------------------------- |

示例代码：  

```jsp
获取 Cookie 的名称： ${ cookie.JSESSIONID.name } <br>
获取 Cookie 的值： ${ cookie.JSESSIONID.value } <br>
```



#### 8.4、请求上下文

| initParam | Map<String,String> | 它可以获取在 web.xml 中配置的<context-param>上下文参数 |
| --------- | ------------------ | ------------------------------------------------------ |

web.xml 中的配置：  

```xml
<context-param>
    <param-name>username</param-name>
    <param-value>root</param-value>
</context-param>
<context-param>
    <param-name>url</param-name>
    <param-value>jdbc:mysql:///test</param-value>
</context-param>
```



示例代码：  

```jsp
输出&lt;Context-param&gt;username 的值： ${ initParam.username } <br>
输出&lt;Context-param&gt;url 的值： ${ initParam.url } <br>
```





## **第13章 JSTL**标签库

JSTL 标签库 全称是指 JSP Standard Tag Library JSP 标准标签库。 

是一个不断完善的开放源代码的 JSP 标签库。

EL 表达式主要是为了替换 jsp 中的表达式脚本， 而标签库则是为了替换代码脚本。 

这样使得整个 jsp 页面变得更佳简洁。  



JSTL 由五个不同功能的标签库组成。  

![image-20211110225100036](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211110225100036.png)

**在 jsp 标签库中使用 taglib 指令引入标签库**

```jsp
CORE 标签库
	<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
XML 标签库
	<%@ taglib prefix="x" uri="http://java.sun.com/jsp/jstl/xml" %>
FMT 标签库
	<%@ taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt" %>
SQL 标签库
	<%@ taglib prefix="sql" uri="http://java.sun.com/jsp/jstl/sql" %>
FUNCTIONS 标签库
	<%@ taglib prefix="fn" uri="http://java.sun.com/jsp/jstl/functions" %>
```



### 1、JSTL 标签库的使用步骤

- 第一步，先导入 jstl 标签库的 jar 包。

	- taglibs-standard-impl-1.2.1.jar
	- taglibs-standard-spec-1.2.1.jar

- 第二步， 使用 taglib 指令引入标签库。  

	```jsp
	<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
	```

	

### 2、core 核心库使用

#### 2.1、<c:set />（使用很少）

- 作用： set 标签可以往域中保存数据
- 域对象.setAttribute(key,value);
- scope 属性                  设置保存到哪个域
- page                             表示 PageContext 域（默认值）
- request                        表示 Request 域
- session                         表示 Session 域
- application                  表示 ServletContext 域
- var 属性                        设置 key 是多少
- value 属性                    设置值



作用： set 标签可以往域中保存数据  

```jsp
保存之前： ${ sessionScope.abc } <br>
<c:set scope="session" var="abc" value="abcValue"/>
保存之后： ${ sessionScope.abc } <br>
```

#### 2.2、<c:if />  

- if 标签用来做 if 判断。
- test 属性表示判断的条件（使用 EL 表达式输出）



```jsp
<c:if test="${ 12 == 12 }">
	<h1>12 等于 12</h1>
</c:if>
<c:if test="${ 12 != 12 }">
	<h1>12 不等于 12</h1>
</c:if>
```

#### 2.3、<c:choose> <c:when> <c:otherwise>标签 

- 作用： 多路判断。 跟 switch ... case .... default 非常接近
- <font color = 'red'>choose 标签</font>               开始选择判断【<font color = 'blue'>就是switch</font>】
- <font color = 'red'>when 标签</font>                  表示每一种判断情况【<font color = 'blue'>就是case</font>】
	- test 属性                     表示当前这种判断情况的值

- <font color = 'red'>otherwise</font>                   标签表示剩下的情况【<font color = 'blue'>就是default</font>】
- <c:choose> <c:when> <c:otherwise>标签使用时需要注意的点：
  - 标签里不能使用 html 注释， 要使用 jsp 注释
  - **when 标签的父标签一定要是 choose 标签**  

```jsp
<%--
<c:choose> <c:when> <c:otherwise>标签使用时需要注意的点：
	1、 标签里不能使用 html 注释， 要使用 jsp 注释
	2、 when 标签的父标签一定要是 choose 标签
--%>
<%
	request.setAttribute("height", 180);
%>
<c:choose>
    <%-- 这是 html 注释 --%>
    <c:when test="${ requestScope.height > 190 }">
    	<h2>小巨人</h2>
    </c:when>
    <c:when test="${ requestScope.height > 180 }">
    	<h2>很高</h2>
    </c:when>
    <c:when test="${ requestScope.height > 170 }">
    	<h2>还可以</h2>
    </c:when>
    <c:otherwise>
        <c:choose>
            <c:when test="${requestScope.height > 160}">
            	<h3>大于 160</h3>
            </c:when>
            <c:when test="${requestScope.height > 150}">
            	<h3>大于 150</h3>
            </c:when>
            <c:when test="${requestScope.height > 140}">
            	<h3>大于 140</h3>
            </c:when>
            <c:otherwise>
            	其他小于 140
        	</c:otherwise>
        </c:choose>
    </c:otherwise>
</c:choose>
```

#### 2.4、<c:forEach />  

作用： 遍历输出使用。  



##### 示列代码一：遍历 1 到 10输出

格式：

```jsp
<c:forEach begin="1" end="10" var="i">
```

- begin 属性设置开始的索引
- end 属性设置结束的索引
- var 属性表示循环的变量(也是当前正在遍历到的数据)

```jsp
<%--
    1.遍历 1 到 10输出
    begin 属性设置开始的索引
    end 属性设置结束的索引
    var 属性表示循环的变量(也是当前正在遍历到的数据)
    for (int i = 1; i < 10; i++)
--%>
<table border="1">
    <c:forEach begin="1" end="10" var="i">
        <tr>
        	<td>第${i}行</td>
        </tr>
    </c:forEach>
</table>
```

##### 示例代码二：遍历 Object 数组

- items 表示遍历的数据源（遍历的集合）
- var 表示当前遍历到的数据

```jsp
<%-- 
    2.遍历 Object 数组
	for (Object item: arr)
	items 表示遍历的数据源（遍历的集合）
	var 表示当前遍历到的数据
--%>
<%
	request.setAttribute("arr", new String[]{"18610541354","18688886666","18699998888"});
%>
<c:forEach items="${ requestScope.arr }" var="item">
	${ item } <br>
</c:forEach>
```

##### 示例代码三：遍历 Map 集合

```jsp
<%
    Map<String,Object> map = new HashMap<String, Object>();
    map.put("key1", "value1");
    map.put("key2", "value2");
    map.put("key3", "value3");
    // for ( Map.Entry<String,Object> entry : map.entrySet()) {
    // }
    request.setAttribute("map", map);
%>
<c:forEach items="${ requestScope.map }" var="entry">
	<h1>${entry.key} = ${entry.value}</h1>
</c:forEach>
```

##### 示例代码四：遍历 List 集合

list 中存放 Student 类， 有属性： 编号， 用户名， 密码， 年龄，电话信息  

格式：

```jsp
<c:forEach begin="2" end="7" step="2" varStatus="status" items="${requestScope.stus}" var="stu">
```

- items 表示遍历的集合
- var 表示遍历到的数据
- begin 表示遍历的开始索引值
- end 表示结束的索引值
- step 属性表示遍历的步长值
- varStatus 属性表示当前遍历到的数据的状态

Student 类：  

```java
public class Student {
//4.编号， 用户名， 密码， 年龄， 电话信息
private Integer id;
private String username;
private String password;
private Integer age;
private String phone;
```

示例代码：

```jsp
<%--4.遍历 List 集合---list 中存放 Student 类， 有属性： 编号， 用户名， 密码， 年龄， 电话信息--%>
<%
    List<Student> studentList = new ArrayList<Student>();
    for (int i = 1; i <= 10; i++) {
    	studentList.add(new Student(i,"username"+i ,"pass"+i,18+i,"phone"+i));
    } 
	request.setAttribute("stus", studentList);
%>
<table>
    <tr>
        <th>编号</th>
        <th>用户名</th>
        <th>密码</th>
        <th>年龄</th>
        <th>电话</th>
        <th>操作</th>
    </tr>
    <%--
    items 表示遍历的集合
    var 表示遍历到的数据
    begin 表示遍历的开始索引值
    end 表示结束的索引值
    step 属性表示遍历的步长值
    varStatus 属性表示当前遍历到的数据的状态
    for（int i = 1; i < 10; i+=2）
    --%>
    <c:forEach begin="2" end="7" step="2" varStatus="status" items="${requestScope.stus}" var="stu">
        <tr>
            <td>${stu.id}</td>
            <td>${stu.username}</td>
            <td>${stu.password}</td>
            <td>${stu.age}</td>
            <td>${stu.phone}</td>
            <td>${status.step}</td>
        </tr>
</c:forEach>
</table>
```



## **第14章 文件的上传和下载**

文件的上传和下载， 是非常常见的功能。 很多的系统中， 或者软件中都经常使用文件的上传和下载。
比如： 

- QQ 头像， 就使用了上传。
- 邮箱中也有附件的上传和下载功能。
- OA 系统中审批有附件材料的上传。  

### 1、文件的上传

#### 1.1、步骤及要求：

​		1、要有一个 form 标签， method=post 请求
​		2、 form 标签的 encType 属性值必须为 multipart/form-data 值
​		3、 在 form 标签中使用 input type=file 添加上传的文件
​		4、 编写服务器代码（Servlet 程序） 接收， 处理上传的数据。

encType=multipart/form-data 表示提交的数据， 以多段（每一个表单项一个数据段） 的形式进行拼接， 然后以二进制流的形式发送给服务器  

#### 1.2、HTTP 协议的说明

![image-20211111101630002](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211111101630002.png)

#### 1.3、commons-fileupload.jar 常用 API 介绍说明

commons-fileupload.jar 需要依赖 commons-io.jar 这个包， 所以两个包我们都要引入。

第一步， 就是需要导入两个 jar 包：

- commons-fileupload-1.2.1.jar
- commons-io-1.4.jar  

![image-20211111102146895](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211111102146895.png)

**commons-fileupload.jar 和 commons-io.jar 包中， 我们常用的类有哪些？**

- **ServletFileUpload 类**
	- 用于解析上传的数据。
- **FileItem 类**
	- 表示每一个表单项。
- **boolean ServletFileUpload.isMultipartContent(HttpServletRequest request);**
	- 判断当前上传的数据格式是否是多段的格式。
- **public List<FileItem> parseRequest(HttpServletRequest request)**
	- 解析上传的数据
- **boolean FileItem.isFormField()**
	- 判断当前这个表单项， 是否是普通的表单项。 还是上传的文件类型。
	- true 表示普通类型的表单项
	- false 表示上传的文件类型
- **String FileItem.getFieldName()**
	- 获取表单项的 name 属性值
- **String FileItem.getString()**
	- 获取当前表单项的值。
- **String FileItem.getName();**
	- 获取上传的文件名
- **void FileItem.write( file );**
	- 将上传的文件写到 参数 file 所指向抽硬盘位置 。  

#### 1.4、fileupload 类库的使用：

上传文件的表单：  

```jsp
<form action="http://192.168.31.74:8080/09_EL_JSTL/uploadServlet" method="post"
enctype="multipart/form-data">
    用户名： <input type="text" name="username" /> <br>
    头像： <input type="file" name="photo" > <br>
    <input type="submit" value="上传">
</form>
```

解析上传的数据的代码：  

```java
package com.example.el_jstl_09; /**
 * @ClassName ${NAME}
 * @Description TODO:
 * @Author sth_199509@163.com
 * @Date 2021/11/11 8:50
 * @Version 1.0
 */

import org.apache.commons.fileupload.FileItem;
import org.apache.commons.fileupload.FileItemFactory;
import org.apache.commons.fileupload.FileUploadException;
import org.apache.commons.fileupload.disk.DiskFileItemFactory;
import org.apache.commons.fileupload.servlet.ServletFileUpload;

import javax.servlet.*;
import javax.servlet.http.*;
import java.io.File;
import java.io.IOException;
import java.util.List;

public class Servlet2 extends HttpServlet {
    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 1、先判断上传的数据，是否是多段数据（只有多段数据才是文件）
        if (ServletFileUpload.isMultipartContent(request)){
            // 2、创建FileItemFactory工厂实现类
            FileItemFactory fileItemFactory = new DiskFileItemFactory();
            // 3、创建用于解析上传数据的工具类ServletFileUpload类
            ServletFileUpload servletFileUpload = new ServletFileUpload(fileItemFactory);
            // 4、解析上传的数据，得到每一个表单项FileItem
            List<FileItem> list = null;
            try {
                list = servletFileUpload.parseRequest(request);
            } catch (FileUploadException e) {
                e.printStackTrace();
            }
            // 5、循环判断，每一个表单项，是文件还是普通类型
            for (FileItem fileItem:list){
                if (fileItem.isFormField()){
                    // 上传的是普通表单项
                    System.out.println("表单项的name属性值是：" + fileItem.getFieldName());
                    // utf-8 解决乱码问题
                    System.out.println("表单项的value属性值是：" + fileItem.getString("UTF-8"));
                }else{
                    // 上传的是文件
                    System.out.println("表单项的name属性值是：" + fileItem.getFieldName());
                    System.out.println("上传的文件名是：" + fileItem.getName());

                    // 写文件操作
                    try {
                        fileItem.write(new File("D:\\" + fileItem.getName()));
                    } catch (Exception e) {
                        e.printStackTrace();
                    }
                }
            }
        }
    }
}
```



### 2、文件的下载 

下载的常用 API 说明：

- response.getOutputStream();
- servletContext.getResourceAsStream();
- servletContext.getMimeType();
- response.setContentType();  

**response.setHeader("Content-Disposition", "attachment; fileName=1.jpg");**
这个响应头告诉浏览器。 这是需要下载的。 而 attachment 表示附件， 也就是下载的一个文件。 fileName=后面，表示下载的文件名。

完成上面的两个步骤， 下载文件是没问题了。 但是如果我们要下载的文件是中文名的话。 你会发现， 下载无法正确显示出正确的中文名。

原因是在响应头中， 不能包含有中文字符， 只能包含 ASCII 码。  

文件下载示例：  

```java
package com.example.el_jstl_09; /**
 * @ClassName ${NAME}
 * @Description TODO:
 * @Author sth_199509@163.com
 * @Date 2021/11/11 9:35
 * @Version 1.0
 */

import org.apache.commons.io.IOUtils;

import javax.servlet.*;
import javax.servlet.http.*;
import java.io.IOException;
import java.io.InputStream;

public class DownloadServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 1、获取要下载的文件名【此处先写死，固定的】
        String downloadFileName = "2.jpg";
        // 2、读取要下载的文件内容（通过ServletContext对象可以读取）
        ServletContext servletContext = getServletContext();

        // 3、获取要下载的文件类型
        String mimeType = servletContext.getMimeType("/file/" + downloadFileName);
        System.out.println("下载的文件类型： " + mimeType);

        // 4、 在回传前， 通过响应头告诉客户端返回的数据类型
        response.setContentType(mimeType);

        // 5、 还要告诉客户端收到的数据是用于下载使用（还是使用响应头）
            // Content-Disposition 响应头， 表示收到的数据怎么处理
            // attachment 表示附件， 表示下载使用
            // filename= 表示指定下载的文件名
        response.setHeader("Content-Disposition", "attachment; filename=" + downloadFileName);

        // 6、把文件回传给客户端
            // /开头第一个斜杠，被服务器解析表示地址：http://ip:port/工程名   映射到代码的wenapp目录下
        InputStream resourceAsStream = servletContext.getResourceAsStream("/file/" + downloadFileName);
        // 获取响应的输出流
        ServletOutputStream outputStream = response.getOutputStream();
        // 读取输入流中数据，复制给输出流
        IOUtils.copy(resourceAsStream, outputStream);
    }
}
```



### 3、下载附件---中文名乱码问题解决方案：  

#### 方案一： URLEncoder 解决 IE 和谷歌浏览器的 附件中文名问题。

如果客户端浏览器是 IE 浏览器 或者 是谷歌浏览器。 我们需要使用 URLEncoder 类先对中文名进行 UTF-8 的编码
操作。
因为 IE 浏览器和谷歌浏览器收到含有编码后的字符串后会以 UTF-8 字符集进行解码显示。  

```java
//未处理时：
response.setHeader("Content-Disposition", "attachment; filename=中国汉字.jpg);

//处理后:

// 把中文名进行 UTF-8 编码操作。
String str = "attachment; fileName=" + URLEncoder.encode("中国汉字.jpg", "UTF-8");
// 然后把编码后的字符串设置到响应头中
response.setHeader("Content-Disposition", str);
```

#### 方案二： BASE64 编解码 解决 火狐浏览器的附件中文名问题  

如果客户端浏览器是火狐浏览器。 那么我们需要对中文名进行 BASE64 的编码操作。

这时候需要把请求头 Content-Disposition: attachment; filename=中文名

编码成为： Content-Disposition: attachment; filename==?charset?B?xxxxx?=  

![image-20211111103508667](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211111103508667.png)

```java
//未处理时：
response.setHeader("Content-Disposition", "attachment; filename=中国汉字.jpg);

//处理后:

// 使用下面的格式进行 BASE64 编码后
String str = "attachment; fileName=" + "=?utf-8?B?"
+ new BASE64Encoder().encode("中国汉字.jpg".getBytes("utf-8")) + "?=";
// 设置到响应头中
response.setHeader("Content-Disposition", str);
```





BASE64 编解码操作：

```java 
public static void main(String[] args) throws Exception {
    String content = "这是需要 Base64 编码的内容";
    // 创建一个 Base64 编码器
    BASE64Encoder base64Encoder = new BASE64Encoder();
    // 执行 Base64 编码操作
    String encodedString = base64Encoder.encode(content.getBytes("UTF-8"));
    System.out.println( encodedString );
    // 创建 Base64 解码器
    BASE64Decoder base64Decoder = new BASE64Decoder();
    // 解码操作
    byte[] bytes = base64Decoder.decodeBuffer(encodedString);
    String str = new String(bytes, "UTF-8");
    System.out.println(str);
}
```

**因为火狐使用的是 BASE64 的编解码方式还原响应中的汉字。 所以需要使用 BASE64Encoder 类进行编码操作。**  





#### 根据不同浏览器，采用不同的编码方式

我们只需要通过判断请求头中 User-Agent 这个请求头携带过来的浏览器信息即可判断出是什么浏览器。  

```java
String ua = request.getHeader("User-Agent");
// 判断是否是火狐浏览器
if (ua.contains("Firefox")) {
    
    // 使用下面的格式进行 BASE64 编码后
    String str = "attachment; fileName=" + "=?utf-8?B?"
    + new BASE64Encoder().encode("中文.jpg".getBytes("utf-8")) + "?=";
    // 设置到响应头中
    response.setHeader("Content-Disposition", str);
} else {// 不是火狐
    
    // 把中文名进行 UTF-8 编码操作。
    String str = "attachment; fileName=" + URLEncoder.encode("中文.jpg", "UTF-8");
    // 然后把编码后的字符串设置到响应头中
    response.setHeader("Content-Disposition", str);
}
```





## **第15章 cookie**

### 1、什么是 Cookie?  

​	1、 Cookie 翻译过来是饼干的意思。
​	2、 Cookie 是服务器通知客户端保存键值对的一种技术。
​	3、 客户端有了 Cookie 后， 每次请求都发送给服务器。
​	4、 每个 Cookie 的大小不能超过 4kb  

### 2、如何创建 Cookie

![image-20211115100006789](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211115100006789.png)

Servlet 程序中的代码：  

```java
protected void createCookie(HttpServletRequest req, HttpServletResponse resp) throws ServletException,IOException {
    //1 创建 Cookie 对象
    Cookie cookie = new Cookie("key4", "value4");
    //2 通知客户端保存 Cookie
    resp.addCookie(cookie);
    //1 创建 Cookie 对象
    Cookie cookie1 = new Cookie("key5", "value5");
    //2 通知客户端保存 Cookie
    resp.addCookie(cookie1);
    resp.getWriter().write("Cookie 创建成功");
}
```

### 3、服务器如何获取 Cookie

服务器获取客户端的 Cookie 只需要一行代码： request.getCookies():Cookie[]  

![image-20211115100158730](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211115100158730.png)

Cookie 的工具类：  【用于查询key值为？？？的cookie对象是否存在】

```java
public class CookieUtils {
    public static Cookie findCookie(String name,Cookie[] cookies){
        if (name == null || cookies == null || cookies.length == 0){
            return null;
        }
        for (Cookie cookie : cookies) {
            if (name.equals(cookie.getName())){
                return cookie;
            }
        }
        return null;
    }
}
```



Servlet 程序中的代码：  

```java
public class CookieServlet extends BaseServlet {

    protected void updateCookie(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 方案一：
        /**
         * 1、创建一个同名Cookie并赋值【通过构造器】
         * 2、调用addCookie(cookie)；通知客户端【其实就是从新创建一个，同名的】
         */
        Cookie cookie = new Cookie("key2", "newValue");
        response.addCookie(cookie);
        response.getWriter().write("Cookie[key2]修改成功");

        // 方案二：
        /**
         * 1、先通过查找，得到需要修改的Cookie对象
         * 2、调用setValue()方法赋予新的Cookie值。
         * 3、调用addCookie(cookie)；通知客户端
         */
        Cookie[] cookies = request.getCookies();
        Cookie cookie2 = CookieUtils.findCookie("key1",cookies);
        // setValue()方法不支持任何字符和中文，有歧义的都不行，有需要用base64编码
        cookie2.setValue("newValue222");

        response.addCookie(cookie2);
        response.getWriter().write("Cookie[key1]修改成功");

    }


    protected void getCookie(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        Cookie[] cookies = request.getCookies();
        // 一、输出所有Cookie
        for(Cookie cookie : cookies){
            // getName() 方法，返回Cookie的key值
            // getValue() 方法，返回Cookie的value值
            response.getWriter().write("Cookie[" + cookie.getName() + " = " + cookie.getValue() + "]<br/>");
        }

        // 二、查找目标Cookie
        Cookie wantKey2 = CookieUtils.findCookie("key2", cookies);
        response.getWriter().write("Cookie查找成功");
    }

    protected void createCookie(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 1、创建Cookie对象
        Cookie cookie = new Cookie("key1", "value1");
        // 2、通知客户端保存Cookie
        response.addCookie(cookie);

        Cookie cookie1 = new Cookie("key2", "value2");
        response.addCookie(cookie1);

        Cookie cookie2 = new Cookie("key3", "value3");
        response.addCookie(cookie2);

        response.getWriter().write("Cookie创建成功");
    }

}
```



### 4、Cookie 值的修改

方案一：
	1、 先创建一个要修改的同名（指的就是 key） 的 Cookie 对象
	2、 在构造器， 同时赋于新的 Cookie 值。
	3、 调用 response.addCookie( Cookie );  

```java
// 方案一：

// 1、 先创建一个要修改的同名的 Cookie 对象
// 2、 在构造器， 同时赋于新的 Cookie 值。
Cookie cookie = new Cookie("key1","newValue1");
// 3、 调用 response.addCookie( Cookie ); 通知 客户端 保存修改
resp.addCookie(cookie);
```

方案二：
	1、 先查找到需要修改的 Cookie 对象
	2、 调用 setValue()方法赋于新的 Cookie 值。
	3、 调用 response.addCookie()通知客户端保存修改  

```java
// 方案二：

// 1、 先查找到需要修改的 Cookie 对象
Cookie cookie = CookieUtils.findCookie("key2", req.getCookies());
if (cookie != null) {
    // 2、 调用 setValue()方法赋于新的 Cookie 值。
    cookie.setValue("newValue2");
    // 3、 调用 response.addCookie()通知客户端保存修改
    resp.addCookie(cookie);
}
```



### 5、浏览器查看 Cookie

#### 谷歌浏览器如何查看 Cookie：  

![image-20211115100450951](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211115100450951.png)

#### 火狐浏览器如何查看 Cookie：  

![image-20211115100508380](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211115100508380.png)

### 6、Cookie 生命控制

Cookie 的生命控制指的是如何管理 Cookie 什么时候被销毁（删除）



- setMaxAge()
	- 正数， 表示在指定的秒数后过期
	- 负数， 表示浏览器一关， Cookie 就会被删除（默认值是-1）
	- 零， 表示马上删除 Cookie  

```java
/**
* 设置存活 1 个小时的 Cooie
* @param req
* @param resp
* @throws ServletException
* @throws IOException
*/
protected void life3600(HttpServletRequest req, HttpServletResponse resp) throws ServletException,IOException {
    Cookie cookie = new Cookie("life3600", "life3600");
    cookie.setMaxAge(60 * 60); // 设置 Cookie 一小时之后被删除。 无效
    resp.addCookie(cookie);
    resp.getWriter().write("已经创建了一个存活一小时的 Cookie");
} 


/**
* 马上删除一个 Cookie
* @param req
* @param resp
* @throws ServletException
* @throws IOException
*/
protected void deleteNow(HttpServletRequest req, HttpServletResponse resp) throws ServletException,IOException {// 先找到你要删除的 Cookie 对象
    Cookie cookie = CookieUtils.findCookie("key4", req.getCookies());
    if (cookie != null) {
        // 调用 setMaxAge(0);
        cookie.setMaxAge(0); // 表示马上删除， 都不需要等待浏览器关闭
        // 调用 response.addCookie(cookie);
        resp.addCookie(cookie);
        resp.getWriter().write("key4 的 Cookie 已经被删除");
    }
}
/**
* 默认的会话级别的 Cookie
* @param req
* @param resp
* @throws ServletException
* @throws IOException
*/
protected void defaultLife(HttpServletRequest req, HttpServletResponse resp) throws ServletException,IOException {
    Cookie cookie = new Cookie("defalutLife","defaultLife");
    cookie.setMaxAge(-1);//设置存活时间
    resp.addCookie(cookie);
}
```

### 7、Cookie 有效路径 Path 的设置

Cookie 的 path 属性可以有效的过滤哪些 Cookie 可以发送给服务器。 哪些不发。
path 属性是通过请求的地址来进行有效的过滤。  

| CookieA | path=/工程路径     |
| ------- | ------------------ |
| CookieB | path=/工程路径/abc |

请求地址如下：

- http://ip:port/工程路径/a.html
	- CookieA 发送
	- CookieB 不发送
- http://ip:port/工程路径/abc/a.html
	- CookieA 发送
	- CookieB 发送  

```java
protected void testPath(HttpServletRequest req, HttpServletResponse resp) throws ServletException,IOException {
    Cookie cookie = new Cookie("path1", "path1");
    // getContextPath() ===>>>> 得到工程路径
    cookie.setPath( req.getContextPath() + "/abc" ); // ===>>>> /工程路径/abc
    resp.addCookie(cookie);
    resp.getWriter().write("创建了一个带有 Path 路径的 Cookie");
}
```



### 8、Cookie 练习---免输入用户名登录

![image-20211115101008883](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211115101008883.png)

login.jsp 页面

```html
<form action="http://localhost:8080/13_cookie_session/loginServlet" method="get">
    用户名： <input type="text" name="username" value="${cookie.username.value}"> <br>
    密码： <input type="password" name="password"> <br>
    <input type="submit" value="登录">
</form>
```



LoginServlet 程序：  

```java
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException,IOException {
    String username = req.getParameter("username");
    String password = req.getParameter("password");
    if ("wzg168".equals(username) && "123456".equals(password)) {
        //登录 成功
        Cookie cookie = new Cookie("username", username);
        cookie.setMaxAge(60 * 60 * 24 * 7);//当前 Cookie 一周内有效
        resp.addCookie(cookie);
    	System.out.println("登录 成功");
    } else {
        // 登录 失败
        System.out.println("登录 失败");
    }
}
```





## **第16章 session**

### 1、什么是 Session 会话?  

​	1、 Session 就一个接口（HttpSession） 。
​	2、 Session 就是会话。 它是用来维护一个客户端和服务器之间关联的一种技术。
​	3、 每个客户端都有自己的一个 Session 会话。
​	4、 Session 会话中， 我们经常用来保存用户登录之后的信息  

### 2、如何创建 Session 和获取(id 号,是否为新)

如何创建和获取 Session。 它们的 API 是一样的。

- request.getSession()
	- 第一次调用是： 创建 Session 会话
	- 之后调用都是： 获取前面创建好的 Session 会话对象。
- isNew(); 判断到底是不是刚创建出来的（新的）
	- true 表示刚创建
	- false 表示获取之前创建
- 每个会话都有一个身份证号。 也就是 ID 值。 而且这个 ID 是唯一的。
- getId() 得到 Session 的会话 id 值。  

### 3、Session 域数据的存取

```java
/**
* 往 Session 中保存数据
* @param req* @param resp
* @throws ServletException
* @throws IOException
*/
protected void setAttribute(HttpServletRequest req, HttpServletResponse resp) throws ServletException,IOException {
    req.getSession().setAttribute("key1", "value1");
    resp.getWriter().write("已经往 Session 中保存了数据");
} 


/**
* 获取 Session 域中的数据
* @param req
* @param resp
* @throws ServletException
* @throws IOException
*/
protected void getAttribute(HttpServletRequest req, HttpServletResponse resp) throws ServletException,IOException {
    Object attribute = req.getSession().getAttribute("key1");
    resp.getWriter().write("从 Session 中获取出 key1 的数据是： " + attribute);
}
```

### 4、Session 生命周期控制

- **public void setMaxInactiveInterval(int interval)**

	- 设置 Session 的超时时间（ 以秒为单位） ， 超过指定的时长Session就会被销毁

	- 值为正数的时候， 设定 Session 的超时时长。

	- 负数表示永不超时（极少使用）

- **public int getMaxInactiveInterval()**
	- 获取 Session 的超时时间
- **public void invalidate()** 
	- 让当前 Session 会话马上超时无效。

#### Session 默认的超时时长是多少？

Session 默认的超时时间长为 30 分钟。

因为在 Tomcat 服务器的配置文件 web.xml中默认有以下的配置， 它就表示配置了当前 Tomcat 服务器下所有的 Session超时配置默认时长为： 30 分钟。  

- ```xml
	<session-config>
		<session-timeout>30</session-timeout>
	</session-config>
	```

如果说。 你希望你的 web 工程， 默认的 Session 的超时时长为其他时长。 你可以在你自己的 web.xml 配置文件中做以上相同的配置。 就可以修改你的 web 工程所有 Seession 的默认超时时长。  

```xml
<!--表示当前 web 工程。 创建出来 的所有 Session 默认是 20 分钟 超时时长-->
<session-config>
	<session-timeout>20</session-timeout>
</session-config>
```

如果你想只修改个别 Session 的超时时长。 就可以使用上面的 API。 setMaxInactiveInterval(int interval)来进行单独的设置。

- **session.setMaxInactiveInterval(int interval)**

	- 单独设置超时时长。

	

Session 超时的概念介绍：  

![image-20211115101849034](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211115101849034.png)

示例代码：  

```java
protected void life3(HttpServletRequest req, HttpServletResponse resp) throws ServletException,IOException {
    // 先获取 Session 对象
    HttpSession session = req.getSession();
    // 设置当前 Session3 秒后超时
    session.setMaxInactiveInterval(3);
    resp.getWriter().write("当前 Session 已经设置为 3 秒后超时");
}
```

Session 马上被超时示例：

```java
protected void deleteNow(HttpServletRequest req, HttpServletResponse resp) throws ServletException,IOException {
    // 先获取 Session 对象
    HttpSession session = req.getSession();
    // 让 Session 会话马上超时
    session.invalidate();
    resp.getWriter().write("Session 已经设置为超时（无效） ");
}
```

### 5、浏览器和 Session 之间关联的技术内幕  

<font color='red'>**Session 技术， 底层其实是基于 Cookie 技术来实现的。**  </font>

![image-20211115102056318](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211115102056318.png)





## **第17章 filter过滤器**

### 1、什么是过滤器 

- Filter 过滤器它是 JavaWeb 的三大组件之一。 三大组件分别是：<font color='red'> Servlet 程序、 Listener 监听器、 Filter 过滤器</font>
- Filter 过滤器它是 JavaEE 的规范。 也就是接口
- Filter 过滤器它的**作用**是： <font color='red'>拦截请求， 过滤响应</font>。  

- 拦截请求常见的应用场景有：
	- 1、 权限检查
	- 2、 日记操作
	- 3、 事务管理
	- ……等等  

### 2、 Filter 的初体验

要求： 在你的 web 工程下， 有一个 admin 目录。 这个 admin 目录下的所有资源（html 页面、 jpg 图片、 jsp 文件、 等等） 都必须是用户登录之后才允许访问。

思考： 根据之前我们学过内容。 我们知道， 用户登录之后都会把用户登录的信息保存到 Session 域中。 所以要检查用户是否登录， 可以判断 Session 中否包含有用户登录的信息即可！ ！ ！  

```jsp
<%
    Object user = session.getAttribute("user");
    // 如果等于 null， 说明还没有登录
    if (user == null) {
        request.getRequestDispatcher("/login.jsp").forward(request,response);
        return;// return 表示不再继续执行代码
    }
%>
```

Filter 的工作流程图：

![image-20211117120955397](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211117120955397.png)

Filter 的代码：



```java
public class AdminFilter implements Filter {
    /**
    * doFilter 方法， 专门用于拦截请求。 可以做权限检查
    */
    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        HttpServletRequest httpServletRequest = (HttpServletRequest) servletRequest;
        HttpSession session = httpServletRequest.getSession();
        Object user = session.getAttribute("user");
        // 如果等于 null， 说明还没有登录
        if (user == null) {          			         					servletRequest.getRequestDispatcher("/login.jsp").forward(servletRequest,servletResponse);
            return;
        } else {
            // 让程序继续往下访问用户的目标资源
            filterChain.doFilter(servletRequest,servletResponse);
        }
    }
}
```

web.xml 中的配置：  

```xml
<!--filter 标签用于配置一个 Filter 过滤器-->
<filter>
    <!--给 filter 起一个别名-->
    <filter-name>AdminFilter</filter-name>
    <!--配置 filter 的全类名-->
    <filter-class>com.atguigu.filter.AdminFilter</filter-class>
</filter>

<!--filter-mapping 配置 Filter 过滤器的拦截路径-->
<filter-mapping>
    <!--filter-name 表示当前的拦截路径给哪个 filter 使用-->
    <filter-name>AdminFilter</filter-name>
    <!--
		url-pattern 配置拦截路径
    	/ 表示请求地址为： http://ip:port/工程路径/ 映射到 IDEA 的 web 目录
    	/admin/* 表示请求地址为： http://ip:port/工程路径/admin/*
    -->
    <url-pattern>/admin/*</url-pattern>
</filter-mapping>
```



### 3、Filter 过滤器的使用步骤：

- 1、 编写一个类去实现 Filter 接口
- 2、 实现过滤方法 doFilter()
- 3、 到 web.xml 中去配置 Filter 的拦截路径  

### 4、完整的用户登录

login.jsp 页面 == 登录表单：

```jsp
这是登录页面。 login.jsp 页面 <br>

<form action="http://localhost:8080/15_filter/loginServlet" method="get">
    用户名： <input type="text" name="username"/> <br>
    密 码： <input type="password" name="password"/> <br>
	<input type="submit" />
</form>
```

LoginServlet 程序:

```java
public class LoginServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException,IOException {
        resp.setContentType("text/html; charset=UTF-8");
        String username = req.getParameter("username");
        String password = req.getParameter("password");
        if ("wzg168".equals(username) && "123456".equals(password)) {
            req.getSession().setAttribute("user",username);
            resp.getWriter().write("登录 成功！ ！ ！ ");
        } else {
        	req.getRequestDispatcher("/login.jsp").forward(req,resp);
        }
    }
}
```



### 5、Filter 的生命周期  

- Filter 的生命周期包含几个方法
	- 1、 <font color='red'>构造器方法</font>
	- 2、<font color='red'> init 初始化方法</font>
		- 第 1， 2 步， 在 web 工程启动的时候执行（Filter 已经创建）
	- 3、<font color='red'> doFilter 过滤方法</font>
		- 第 3 步， 每次拦截到请求， 就会执行
	- 4、<font color='red'> destroy 销毁</font>
		- 第 4 步， 停止 web 工程的时候， 就会执行（停止 web 工程， 也会销毁 Filter 过滤器）  

### 6、FilterConfig 类

- FilterConfig 类见名知义， 它是 Filter 过滤器的配置文件类。
- Tomcat 每次创建 Filter 的时候， 也会同时创建一个 FilterConfig 类， 这里包含了 Filter 配置文件的配置信息。
- <font color='red'>FilterConfig 类的作用是**获取 filter 过滤器的配置内容**</font>
	- 1、 获取 Filter 的名称 filter-name 的内容
	- 2、 获取在 Filter 中配置的 init-param 初始化参数
	- 3、 获取 ServletContext 对象  

java 代码：

```java
@Override
public void init(FilterConfig filterConfig) throws ServletException {
    System.out.println("2.Filter 的 init(FilterConfig filterConfig)初始化");
    // 1、 获取 Filter 的名称 filter-name 的内容
    System.out.println("filter-name 的值是： " + filterConfig.getFilterName());
    // 2、 获取在 web.xml 中配置的 init-param 初始化参数
    System.out.println("初始化参数 username 的值是： " + filterConfig.getInitParameter("username"));
    System.out.println("初始化参数 url 的值是： " + filterConfig.getInitParameter("url"));
    // 3、 获取 ServletContext 对象
    System.out.println(filterConfig.getServletContext());
}
```

web.xml 配置：  

```xml
<!--filter 标签用于配置一个 Filter 过滤器-->
<filter>
    <!--给 filter 起一个别名-->
    <filter-name>AdminFilter</filter-name>
    <!--配置 filter 的全类名--><filter-class>com.atguigu.filter.AdminFilter</filter-class>
    <init-param>
        <param-name>username</param-name>
        <param-value>root</param-value>
    </init-param>
    
    <init-param>
        <param-name>url</param-name>
        <param-value>jdbc:mysql://localhost3306/test</param-value>
    </init-param>
</filter>
```



### 7、FilterChain 过滤器链

| **Filter**      | **过滤器**                                 |
| --------------- | ------------------------------------------ |
| **Chain**       | **链， 链条**                              |
| **FilterChain** | **就是过滤器链（多个过滤器如何一起工作）** |

 

#### 7.1 多个过滤器如何一起工作

![image-20211117125402764](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211118110710381.png)

执行顺序：

- 前值代码1
- 前置代码2
- 目标代码
- 后置代码2
- 后置代码1



#### 7.2 在多个Filter过滤器执行的时候，他们的**先后顺序**是：

- 按照web.xml配置文件的顺序，从上到下，跟名字没关系

#### 7.3 多个Filter过滤器的执行的特点

- 所有Filter 和目标资源默认都执行在同一个线程中
- 多个Filter共同执行的时候，他们都使用同一个Request对象

#### 7.4 FilterChain.doFilter() 方法的使用

- 执行下一个Filter过滤器【如果有】
- 执行目标资源【如果后边没有过滤器了】



### 8、Filter 的拦截路径

- 精确匹配

	```xml
	<url-pattern>/target.jsp</url-pattern>
	
	以上配置的路径， 表示请求地址必须为： http://ip:port/工程路径/target.jsp
	```

	

- 目录匹配

	```xml
	<url-pattern>/admin/*</url-pattern>
	
	以上配置的路径， 表示请求地址必须为： http://ip:port/工程路径/admin/*
	```

	

- 后缀名匹配【不能用斜杠打头 了】 回家咯基本

	```xml
	<url-pattern>*.html</url-pattern>
	以上配置的路径， 表示请求地址必须以.html 结尾才会拦截到
	
	<url-pattern>*.do</url-pattern>
	以上配置的路径， 表示请求地址必须以.do 结尾才会拦截到
	
	<url-pattern>*.action</url-pattern>
	以上配置的路径， 表示请求地址必须以.action 结尾才会拦截到
	```

	

	

- **Filter 过滤器它只关心请求的地址是否匹配， 不关心请求的资源是否存在！ ！ ！**  



## 第18章 json

### 1、什么是 JSON?

- JSON (JavaScript Object Notation) 是一种轻量级的数据交换格式。 易于人阅读和编写。 同时也易于机器解析和生成。 

- JSON采用完全独立于语言的文本格式， 而且很多语言都提供了对 json 的支持（包括 C, C++, C#, Java, JavaScript, Perl, Python等） 。 

- 这样就使得 JSON 成为理想的数据交换格式。
- json 是一种轻量级的数据交换格式。
	- 轻量级指的是跟 xml 做比较。
- 数据交换指的是客户端和服务器之间业务数据的传递格式。  

### 2、JSON 在 JavaScript 中的使用

#### 2.1、json 的定义

<font color='red'>json 是由键值对组成， 并且由花括号（大括号） 包围。 每个键由引号引起来， 键和值之间使用冒号进行分隔，多组键值对之间进行逗号进行分隔。</font>

可以放各种类型，还能放json本身

json 定义示例：  

```java
var jsonObj = {
    "key1":12,
    "key2":"abc",
    "key3":true,
    "key4":[11,"arr",false],
    "key5":{
    "key5_1" : 551,
    "key5_2" : "key5_2_value"
    },
    "key6":[{
    "key6_1_1":6611,
    "key6_1_2":"key6_1_2_value"},{
    "key6_2_1":6621,
    "key6_2_2":"key6_2_2_value"
    }]
};
```

#### 2.2、json 的访问

- json 本身是一个对象。

- json 中的 key 我们可以理解为是对象中的一个属性。

- json 中的 key 访问就跟访问对象的属性一样： json 对象.key

	

json 访问示例：  

```javascript
alert(typeof(jsonObj));// object json 就是一个对象
alert(jsonObj.key1); //12
alert(jsonObj.key2); // abc
alert(jsonObj.key3); // true
alert(jsonObj.key4);// 得到数组[11,"arr",false]

// json 中 数组值的遍历
for(var i = 0; i < jsonObj.key4.length; i++) {
	alert(jsonObj.key4[i]);
} 

alert(jsonObj.key5.key5_1);//551
alert(jsonObj.key5.key5_2);//key5_2_value
alert( jsonObj.key6 );// 得到 json 数组

// 取出来每一个元素都是 json 对象
var jsonItem = jsonObj.key6[0];
// alert( jsonItem.key6_1_1 ); //6611
alert( jsonItem.key6_1_2 ); //key6_1_2_value
```

#### 2.3、json 的两个常用方法  

- json 的存在有两种形式。
	- 一种是： 对象的形式存在， 我们叫它 json 对象。
	- 一种是： 字符串的形式存在， 我们叫它 json 字符串。
- 一般我们要操作 json 中的数据的时候， 需要 json 对象的格式。
- 一般我们要在客户端和服务器之间进行数据交换的时候， 使用 json 字符串。
	- **JSON.stringify()**       把 json 对象转换成为 json 字符串
	- **JSON.parse()**            把 json 字符串转换成为 json 对象  

```java
// 把 json 对象转换成为 json 字符串
var jsonObjString = JSON.stringify(jsonObj); // 特别像 Java 中对象的 toString
alert(jsonObjString)
    
// 把 json 字符串。 转换成为 json 对象
var jsonObj2 = JSON.parse(jsonObjString);
alert(jsonObj2.key1);// 12
alert(jsonObj2.key2);// abc
```

### 3、JSON 在 java 中的使用

需要导包，gson.jar

#### 3.1、javaBean 和 json 的互转

```java
@Test
public void test1(){
    Person person = new Person(1,"国哥好帅!");
    // 创建 Gson 对象实例
    Gson gson = new Gson();
    
    
    // toJson 方法可以把 java 对象转换成为 json 字符串
    String personJsonString = gson.toJson(person);
    System.out.println(personJsonString);
    
    
    // fromJson 把 json 字符串转换回 Java 对象
    // 第一个参数是 json 字符串
    // 第二个参数是转换回去的 Java 对象类型
    Person person1 = gson.fromJson(personJsonString, Person.class);
    System.out.println(person1);
}
```

#### 3.2、List 和 json 的互转

  

```java
@Test
public void test2() {
    List<Person> personList = new ArrayList<>();
    personList.add(new Person(1, "国哥"));
    personList.add(new Person(2, "康师傅"));
    Gson gson = new Gson();
    
    
    // 把 List 转换为 json 字符串
    String personListJsonString = gson.toJson(personList);
    System.out.println(personListJsonString);
    
    // 把 json 字符串 转换为 List
    List<Person> list = gson.fromJson(personListJsonString, new PersonListType().getType());
    System.out.println(list);
    Person person = list.get(0);
    System.out.println(person);
}
```



#### 3.3、map 和 json 的互转

转换成map或者集合时，要new一个TypeToken类，泛型就是要转换的类型，后边调用getType()

gson.fromJson(personMapJsonString, **new TypeToken<HashMap<Integer,Person>>(){}.getType()**）

```java
@Test
public void test3(){
    Map<Integer,Person> personMap = new HashMap<>();
    personMap.put(1, new Person(1, "国哥好帅"));
    personMap.put(2, new Person(2, "康师傅也好帅"));
    Gson gson = new Gson();
    
    
    // 把 map 集合转换成为 json 字符串
    String personMapJsonString = gson.toJson(personMap);
    System.out.println(personMapJsonString);
    
    
    // 把 json 字符串  转换成为 map 集合
    // Map<Integer,Person> personMap2 = gson.fromJson(personMapJsonString, new PersonMapType().getType());
    Map<Integer,Person> personMap2 = gson.fromJson(personMapJsonString, new TypeToken<HashMap<Integer,Person>>(){}.getType());
    System.out.println(personMap2);
    Person p = personMap2.get(1);
    System.out.println(p);
}
```





## **第19章 AJAX请求**

### 1、什么是 AJAX 请求？

AJAX 即“Asynchronous Javascript And XML”（异步 JavaScript 和 XML） ， 是指一种创建交互式网页应用的网页开发技术。

- <font color='red'>ajax 是一种浏览器通过 js 异步发起请求， 局部更新页面的技术。</font>
- <font color='red'>Ajax 请求的局部更新， 浏览器地址栏不会发生变化</font>
- <font color='red'>局部更新不会舍弃原来页面的内容  </font>

### 2、ajax 语法的使用

#### 2.1、创建 XMLHttpRequest 对象的语法：

```javascript
variable=new XMLHttpRequest();
```

#### 2.2、向服务器发送请求

如需将请求发送到服务器，我们使用 XMLHttpRequest 对象的 open() 和 send() 方法：

```javascript
xmlhttp.open("GET","test1.txt",true);
xmlhttp.send();
```

| 方法                         | 描述                                                         |
| ---------------------------- | ------------------------------------------------------------ |
| open(*method*,*url*,*async*) | 规定请求的类型、URL 以及是否异步处理请求。<br/>***method*：请求的类型；GET 或 POST  <br/>*url*：文件在服务器上的位置  <br/>*async*：true（异步）或 false（同步）** |
| send(*string*)               | 将请求发送到服务器。 *string*：仅用于 POST 请求              |

#### 2.3、服务器响应

如需获得来自服务器的响应，请使用 XMLHttpRequest 对象的 responseText 或 responseXML 属性。

| 属性         | 描述                       |
| ------------ | -------------------------- |
| responseText | 获得字符串形式的响应数据。 |
| responseXML  | 获得 XML 形式的响应数据。  |

- **responseText 属性**

如果来自服务器的响应并非 XML，请使用 responseText 属性。

responseText 属性返回字符串形式的响应，因此您可以这样使用：

```javascript
直接放到myDiv标签去
document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
```

- **responseXML 属性**

如果来自服务器的响应是 XML，而且需要作为 XML 对象进行解析，请使用 responseXML 属性：

请求 [books.xml](../example/xmle/books.xml) 文件，并解析响应：

```javascript
xmlDoc=xmlhttp.responseXML;
txt="";
x=xmlDoc.getElementsByTagName("ARTIST");
for (i=0;i<x.length;i++)
  {
  	txt=txt + x[i].childNodes[0].nodeValue + "<br />";
  }

同样，转换后将文本内容放到myDiv标签中
document.getElementById("myDiv").innerHTML=txt;
```



#### 2.4、onreadystatechange 事件

当请求被发送到服务器时，我们需要执行一些基于响应的任务。

每当 readyState 改变时，就会触发 onreadystatechange 事件。

readyState 属性存有 XMLHttpRequest 的状态信息。

下面是 XMLHttpRequest 对象的三个重要的属性：

| 属性               | 描述                                                         |
| ------------------ | ------------------------------------------------------------ |
| onreadystatechange | 存储函数（或函数名），每当 readyState 属性改变时，就会调用该函数。 |
| readyState         | 存有 XMLHttpRequest 的状态。<br/>从 0 到 4 发生变化。<br/>**0: 请求未初始化  <br/>1: 服务器连接已建立  <br/>2: 请求已接收  <br/>3: 请求处理中  <br/>4: 请求已完成，且响应已就绪** |
| status             | 200: "OK" <br/>404: 未找到页面                               |

在 onreadystatechange 事件中，我们规定当服务器响应已做好被处理的准备时所执行的任务。

当 readyState 等于 4 且状态为 200 时，表示<font color= 'red'>响应已就绪</font>：

```javascript
xmlhttp.onreadystatechange=function()
  {
      if (xmlhttp.readyState==4 && xmlhttp.status==200)
        {
        	document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
        }
  }
```

**注释：**onreadystatechange 事件被触发 5 次（0 - 4），对应着 readyState  的每个变化。

#### 2.5、使用 Callback 函数

callback 函数是一种以参数形式传递给另一个函数的函数。

如果您的网站上存在多个 AJAX 任务，那么您应该为创建 XMLHttpRequest 对象编写一个*标准*的函数，并为每个 AJAX  任务调用该函数。

该函数调用应该包含 URL 以及发生 onreadystatechange 事件时执行的任务（每次调用可能不尽相同）：

```
function myFunction()
{
loadXMLDoc("ajax_info.txt",function()
  {
  if (xmlhttp.readyState==4 && xmlhttp.status==200)
    {
    document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
    }
  });
}
```





### 2、原生 AJAX 请求的示例：

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
   <meta http-equiv="pragma" content="no-cache" />
   <meta http-equiv="cache-control" content="no-cache" />
   <meta http-equiv="Expires" content="0" />
   <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
   <title>Insert title here</title>
   <script type="text/javascript">
      // 在这里使用 javaScript 语言发起 Ajax 请求， 访问服务器 AjaxServlet 中 javaScriptAjax
      function ajaxRequest() {
         // 1、 我们首先要创建 XMLHttpRequest
         var xmlhttprequest = new XMLHttpRequest();
         // 2、 调用 open 方法设置请求参数
         xmlhttprequest.open("GET","http://localhost:8080/16_json_ajax_i18n/ajaxServlet?action=javaScriptAjax",true)
         // 4、 在 send 方法前绑定 onreadystatechange 事件， 处理请求完成后的操作。
         xmlhttprequest.onreadystatechange = function(){
            if (xmlhttprequest.readyState == 4 && xmlhttprequest.status == 200) {
               var jsonObj = JSON.parse(xmlhttprequest.responseText);
               // 把响应的数据显示在页面上
               document.getElementById("div01").innerHTML = "编号： " + jsonObj.id + " , 姓名： " + jsonObj.name;
            }
         }
         // 3、 调用 send 方法发送请求
         xmlhttprequest.send();
      }
   </script>
   </head>
   <body>
      <button onclick="ajaxRequest()">ajax request</button>
      <div id="div01">
      </div>
   </body>
</html>
```

### 3、jQuery 中的 AJAX 请求

#### $.ajax 方法：

- url                           表示请求的地址
- type                        表示请求的类型 GET 或 POST 请求
- data                        表示发送给服务器的数据
- 格式有两种：
	- 一： name=value&name=value
	- 二： {key:value}
- success                  请求成功， 响应的回调函数
- dataType               响应的数据类型
- 常用的数据类型有：
	- text                 表示纯文本
	- xml                 表示 xml 数据
	- json                表示 json 对象

```javascript
<script type="text/javascript">
   $("#ajaxBtn").click(function(){
      $.ajax({
         url:"http://localhost:8080/16_json_ajax_i18n/ajaxServlet",
         //data:"action=jQueryAjax", //data两种方式，键值对或等号
         data:{action:"jQueryAjax"},
         type:"GET",
         success:function (data) {// 成功后的回调函数
            // alert("服务器返回的数据是： " + data);
            // var jsonObj = JSON.parse(data);
            $("#msg").html("编号： " + data.id + " , 姓名： " + data.name);
         },
         dataType : "json"
      });
   });

</script>
```

#### $.get 方法和$.post 方法：

- url                  请求的 url 地址
- data               发送的数据
- callback         成功的回调函数
- type               返回的数据类型

```javascript
<script type="text/javascript">
   // ajax--get 请求
   $("#getBtn").click(function(){
      $.get("http://localhost:8080/16_json_ajax_i18n/ajaxServlet","action=jQueryGet",function (data) {
         $("#msg").html(" get 编号： " + data.id + " , 姓名： " + data.name);
      },"json");
   });
   // ajax--post 请求
   $("#postBtn").click(function(){
      $.post("http://localhost:8080/16_json_ajax_i18n/ajaxServlet","action=jQueryPost",function (data)
      {
         $("#msg").html(" post 编号： " + data.id + " , 姓名： " + data.name);},"json");
   	  }
   );
</srcipt>
```

#### $.getJSON 方法:

- url              请求的 url 地址
- data           发送给服务器的数据
- callback     成功的回调函数  

```javascript
// ajax--getJson 请求【$.getJSON(url,data,callback)】
$("#getJSONBtn").click(function(){
    $.getJSON("http://localhost:8080/16_json_ajax_i18n/ajaxServlet","action=jQueryGetJSON",function(data) {
    	$("#msg").html(" getJSON 编号： " + data.id + " , 姓名： " + data.name);
    });
});
```

#### 表单序列化 serialize()

serialize()可以把表单中所有表单项的内容都获取到， 并以 name=value&name=value 的形式进行拼接。  

```javascript
//【$("#form01").serialize() 将表单的所有内容形成键值对，不管是单选还是多选】

$("#submit").click(function(){
    // 把参数序列化
    $.getJSON("http://localhost:8080/16_json_ajax_i18n/ajaxServlet","action=jQuerySerialize&" + $("#form01").serialize(),function (data) {
    	$("#msg").html(" Serialize 编号： " + data.id + " , 姓名： " + data.name);
    });
});
```





## **第20章 i18n**

### 1、什么是 i18n 国际化？  

- 国际化（Internationalization） 指的是同一个网站可以支持多种不同的语言， 以方便不同国家， 不同语种的用户访问。
- 关于国际化我们想到的最简单的方案就是为不同的国家创建不同的网站， 比如苹果公司， 他的英文官网是：
- http://www.apple.com 而中国官网是 http://www.apple.com/cn
- 苹果公司这种方案并不适合全部公司， 而我们希望相同的一个网站， 而不同人访问的时候可以根据用户所在的区域显示不同的语言文字， 而网站的布局样式等不发生改变。
- 于是就有了我们说的国际化， 国际化总的来说就是同一个网站不同国家的人来访问可以显示出不同的语言。 但实际上这种需求并不强烈， 一般真的有国际化需求的公司， 主流采用的依然是苹果公司的那种方案， 为不同的国家创建不同的页面。 所以国际化的内容我们了解一下即可。
- 国际化的英文 Internationalization， 但是由于拼写过长， 老外想了一个简单的写法叫做 I18N， 代表的是 Internationalization这个单词， 以 I 开头， 以 N 结尾， 而中间是 18 个字母， 所以简写为 I18N。 以后我们说 I18N 和国际化是一个意思。  

### 2、国际化相关要素介绍

![image-20211118105110039](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211118105110039.png)

### 3、国际化资源 properties 测试

![image-20211118110710381](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211118105444109.png)

配置两个语言的配置文件：  

![image-20211118105444109](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211117125402764.png)

i18n_en_US.properties 英文 ：

```properties
username=username
password=password
sex=sex
age=age
regist=regist
boy=boy
email=email
girl=girl
reset=reset
submit=submit
```

i18n_zh_CN.properties 中文 ：

```properties
username=用户名
password=密码
sex=性别
age=年龄
regist=注册
boy=男
girl=女
email=邮箱
reset=重置
submit=提交
```

国际化测试代码：  

```java
public class I18nTest {
    @Test
    public void testLocale(){
        // 获取你系统默认的语言。 国家信息
        // Locale locale = Locale.getDefault();
        // System.out.println(locale);
        // for (Locale availableLocale : Locale.getAvailableLocales()) {
        // System.out.println(availableLocale);
        // }
        // 获取中文， 中文的常量的 Locale 对象
        System.out.println(Locale.CHINA);
        // 获取英文， 美国的常量的 Locale 对象
        System.out.println(Locale.US);
    }
    @Test
    public void testI18n(){
        // 得到我们需要的 Locale 对象
        Locale locale = Locale.CHINA;
        // 通过指定的 basename 和 Locale 对象， 读取 相应的配置文件
        ResourceBundle bundle = ResourceBundle.getBundle("i18n", locale);
        System.out.println("username： " + bundle.getString("username"));
        System.out.println("password： " + bundle.getString("password"));
        System.out.println("Sex： " + bundle.getString("sex"));
        System.out.println("age： " + bundle.getString("age"));
    }
}
```

### 4、通过请求头国际化页面【就是根据浏览器默认语言，选择对应的语言】

```html
<%@ page import="java.util.Locale" %>
<%@ page import="java.util.ResourceBundle" %>
<%@ page language="java" contentType="text/html; charset=UTF-8"
       pageEncoding="UTF-8"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
   <meta http-equiv="pragma" content="no-cache" />
   <meta http-equiv="cache-control" content="no-cache" />
   <meta http-equiv="Expires" content="0" />
   <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
   <title>Insert title here</title>
</head>
<body>
<%
   // 从请求头中获取 Locale 信息（语言）
   Locale locale = request.getLocale();
   System.out.println(locale);
	// 获取读取包（根据 指定的 baseName 和 Locale 读取 语言信息）
   ResourceBundle i18n = ResourceBundle.getBundle("i18n", locale);
%>
<a href="">中文</a>|
<a href="">english</a>
<center>
   <h1><%=i18n.getString("regist")%></h1>
   <table>
      <form>
         <tr>
            <td><%=i18n.getString("username")%></td><td><input name="username" type="text" /></td>
         </tr>
         <tr>
            <td><%=i18n.getString("password")%></td>
            <td><input type="password" /></td>
         </tr>
         <tr>
            <td><%=i18n.getString("sex")%></td>
            <td>
               <input type="radio" /><%=i18n.getString("boy")%>
               <input type="radio" /><%=i18n.getString("girl")%>
            </td>
         </tr>
         <tr>
            <td><%=i18n.getString("email")%></td>
            <td><input type="text" /></td>
         </tr>
         <tr>
            <td colspan="2" align="center">
               <input type="reset" value="<%=i18n.getString("reset")%>" />&nbsp;&nbsp;
               <input type="submit" value="<%=i18n.getString("submit")%>" /></td>
         </tr>
      </form>
   </table>
   <br /> <br /> <br /> <br />
</center>
国际化测试：
<br /> 1、 访问页面， 通过浏览器设置， 请求头信息确定国际化语言。
<br /> 2、 通过左上角， 手动切换语言
</body>
</html>
```





### 5、通过显示的选择语言类型进行国际化【就是手动点击选择语言】

```html
<%@ page import="java.util.Locale" %>
<%@ page import="java.util.ResourceBundle" %>
<%@ page language="java" contentType="text/html; charset=UTF-8"
       pageEncoding="UTF-8"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
   <meta http-equiv="pragma" content="no-cache" />
   <meta http-equiv="cache-control" content="no-cache" />
   <meta http-equiv="Expires" content="0" />
   <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
   <title>Insert title here</title>
</head><body>
    
    
    
<%
   // 从请求头中获取 Locale 信息（语言）
   Locale locale = null;
   String country = request.getParameter("country");
   if ("cn".equals(country)) {
      locale = Locale.CHINA;
   } else if ("usa".equals(country)) {
      locale = Locale.US;
   } else {
      locale = request.getLocale();
   }
   System.out.println(locale);
// 获取读取包（根据 指定的 baseName 和 Locale 读取 语言信息）
   ResourceBundle i18n = ResourceBundle.getBundle("i18n", locale);
%>
    
    
    
<a href="i18n.jsp?country=cn">中文</a>|
<a href="i18n.jsp?country=usa">english</a>
    
    
    
<center>
   <h1><%=i18n.getString("regist")%></h1>
   <table>
      <form>
         <tr>
            <td><%=i18n.getString("username")%></td>
            <td><input name="username" type="text" /></td>
         </tr>
         <tr>
            <td><%=i18n.getString("password")%></td>
            <td><input type="password" /></td>
         </tr>
         <tr>
            <td><%=i18n.getString("sex")%></td>
            <td>
               <input type="radio" /><%=i18n.getString("boy")%>
               <input type="radio" /><%=i18n.getString("girl")%>
            </td>
         </tr>
         <tr>
            <td><%=i18n.getString("email")%></td>
            <td><input type="text" /></td>
         </tr>
         <tr>
            <td colspan="2" align="center">
               <input type="reset" value="<%=i18n.getString("reset")%>" />&nbsp;&nbsp;
               <input type="submit" value="<%=i18n.getString("submit")%>" /></td>
         </tr></form>
   </table>
   <br /> <br /> <br /> <br />
</center>
国际化测试：
<br /> 1、 访问页面， 通过浏览器设置， 请求头信息确定国际化语言。
<br /> 2、 通过左上角， 手动切换语言
</body>
</html>
```





### 6、JSTL 标签库实现国际化

```jsp
<%--1 使用标签设置 Locale 信息--%>
<fmt:setLocale value="" />
<%--2 使用标签设置 baseName--%>
<fmt:setBundle basename=""/>
<%--3 输出指定 key 的国际化信息--%>
<fmt:message key="" />
```



```html
<%@ taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt" %>
<%@ page language="java" contentType="text/html; charset=UTF-8"
       pageEncoding="UTF-8"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
   <meta http-equiv="pragma" content="no-cache" />
   <meta http-equiv="cache-control" content="no-cache" />
   <meta http-equiv="Expires" content="0" />
   <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
   <title>Insert title here</title>
</head>
<body>
<%--1 使用标签设置 Locale 信息--%>
<fmt:setLocale value="${param.locale}" />
<%--2 使用标签设置 baseName--%>
<fmt:setBundle basename="i18n"/>
<a href="i18n_fmt.jsp?locale=zh_CN">中文</a>|
<a href="i18n_fmt.jsp?locale=en_US">english</a>
<center>
   <h1><fmt:message key="regist" /></h1>
   <table>
      <form>
         <tr><td><fmt:message key="username" /></td>
            <td><input name="username" type="text" /></td>
         </tr>
         <tr>
            <td><fmt:message key="password" /></td>
            <td><input type="password" /></td>
         </tr>
         <tr>
            <td><fmt:message key="sex" /></td>
            <td>
               <input type="radio" /><fmt:message key="boy" />
               <input type="radio" /><fmt:message key="girl" />
            </td>
         </tr>
         <tr>
            <td><fmt:message key="email" /></td>
            <td><input type="text" /></td>
         </tr>
         <tr>
            <td colspan="2" align="center">
               <input type="reset" value="<fmt:message key="reset" />" />&nbsp;&nbsp;
               <input type="submit" value="<fmt:message key="submit" />" /></td>
         </tr>
      </form>
   </table>
   <br /> <br /> <br /> <br />
</center>
</body>
</html>
```
