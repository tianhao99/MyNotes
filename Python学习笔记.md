



# Python学习笔记

## 一、基础查缺补漏

### 1、小知识点

#### 字符串中设置变量

```python
j = '如来神掌'
a = f'Hello,Word!{j}'   #通过大括号，可以在字符串中设置变量
print(a)
#-----------
>>>Hello,Word!如来神掌
```

#### startswith（）

```python
 with open('file.txt',mode='r',encoding='utf-8') as f:
    for line in f:#读取文件中的每一行
            if line.startswith('#'):#如果该行中开头是#井号，则跳过。
                continue
            else:
                line = line.strip()#去掉目标行左右空格、换行符。
```

#### **模块查找路径**

同级目录中的第三方模块可直接调用，因为第一个查找路径就是py文件本身的位置。

```python
import sys
import os

print(sys.path)
sys.path.append('I:/计算机/Python/Python练习')#手动添加路径

print(__file__)  #打印当前脚本文件路径   I:/计算机/Python/Python练习/pythonProject1/venv/测试.py
dongtai = os.path.dirname(__file__)  #I:\计算机\Python\Python练习\pythonProject1\venv
dongtai2 = os.path.dirname(dongtai)  #I:\计算机\Python\Python练习\pythonProject1
print(dongtai2)

# os.path.dirname(路径)-------剔除目录中最后一个目录或文件
```

#### **打印时间**

```python
import time
print(time.strftime('%Y-%m-%d %H:%M:%S')) 
#strftime 将时间戳转换为固定格式的日期，(time.strftime('%Y-%m-%d %H:%M:%S'),被转换时间戳)
#不写默认转换当时时间
```

#### **列表去重**

```python
list_123=[2,6,5,22,2,33,'a','vb','c','java','c']
list_end =list(set(list_123))   #先转换成集合，自动去重，在转换成列表
print(list_end)

------------->>>
[33, 2, 5, 6, 22, 'a', 'c', 'java', 'vb']   #因其转换集合，会乱序

#恢复顺序
#sort排序方法：list.sort( key=None, reverse=False)
	#key：表示排序方式
	#reverse -- 排序规则：
	#reverse = True 降序， reverse = False 升序（默认）。
list_end.sort(key=list_123.index)#用第一个列表的索引进行排序
print(list_end)
-------------->>>
[2, 6, 5, 22, 33, 'a', 'vb', 'c', 'java']
```



### 2、函数

####  strip()函数

**函数说明：**移除“字符串”中**首尾**指定的字符，当（）中为空时，默认移除空格或者换行符

**日常用途：**爬取的数据可能首尾有不需要的字符，这时直接在末尾＋.strip（）移除就可以了

```python
# strip()函数展示：
a = '¥¥12¥¥12¥¥'
m = a.strip('¥')
print(m)
#------------
>>>12¥¥12

```



#### split()函数

**函数说明：**拆分字符串，通过指定分隔符对字符串进行切片，返回拆分后的列表。

rsplit()：从右侧开始切割

lsplit()：从左侧开始切割

**日常用途：**对链接进行切片

```python
temp = 'http://c8nh/yi66/tyde.jpg'
templist = temp.split('/')
temp1 = temp.split('/')[-1]      #平时可直接取列表中的位置,-1表示生成的列表中最后一项tyde.jpg
print(templist)
print(temp1)
#-------------
>>>['http:','','c8nh','yi66','tyde.jpg']   #templist
>>>tyde,jpg                                #等价于templist[-1]

temp = 'http://c8nh/yi66/tyde.jpg'
temp2 = temp.split('tyde.')
#temp2 :['http://c8nh/yi66/','jpg']
temp3 = temp.rsplit('/',2)#从右侧开始切割，切割2次
#temp3 ：['http://c8nh','yi66','tyde.jpg']
```



#### join()函数

**函数说明：**通过指定字符，将列表中的几个元素连接起来。

```python
# join()函数展示：
list1 = ['Hello','Word','!']    #列表list1中共3个元素，分别是Hello、Word和！
m = '如来神掌'.join(list1)        #用如来神掌将其连接
print(m)
#------------
>>>Hello如来神掌Word如来神掌!
```

**日常用途：**商品网站展示信息时，你要搜索的内容会被‘’加粗显示‘’，这时源代码会用<标签>将加粗内容与原标题分割开来，此时获取的信息就会存在断点，

```python
#例如：搜索内容为SaaS,
<p class='title'>企业管理系统办公软件OA仓库管理ERP系统<hl>SaaS</hl>系统开发</p>  #网页源码
#目标数据为【企业管理系统办公软件OA仓库管理ERP系统SaaS系统开发】

list1 = ['企业管理系统办公软件OA仓库管理ERP系统','系统开发']  #所得数据
#此时使用join()函数将两个字符串连接，
list2 = 'SaaS'.join(list1)
print(list2)
#------------
>>>企业管理系统办公软件OA仓库管理ERP系统SaaS系统开发


```

#### replace()函数

**函数说明：**替换字符串中的指定元素 

**日常用途：**某些地址需要融合拼接，将指定元素替换进去。

```python
a = 'Hello凌波微步word!'
m = a.replace('凌波微步',"如来神掌")     #用‘如来神掌’替换字符串中的‘凌波微步’
print(m)
#------------
>>>Hello如来神掌word!
```

#### json.dumps()函数

**函数说明：**将字典转化成字符串

**日常用途：**url中需要字符串，而不是字典

```python
import json    #需要先导入json

a = {'dog':'ddd','pig':'ppp'}
m = json.dumps(a)
print(m)          #{"dog": "ddd", "pig": "ppp"}
print(a['dog'])   #ddd   a为字典，可以用key，value格式输出
print(m['dog'])   #报错：TypeError: string indices must be integers
				  #虽然m和a长得一样，但m为字符串，所以不能用字典格式输出。
```

```python
import json    #需要先导入json
import requests
url_txt = 'http://dushu.baidu.com/api/pc/getChapterContent?data={"book_id":"4306063500","cid":"4306063500|9999999","need_bookinfo":1}'
#原url，此时book_id、cid的数据需要不断变化，可将url拆分
bid = '4306063500'
cid = '11348571'

data_one = {				#全部设置为变量，bid和cid可以在外部设置
    "book_id":f"{bid}",
    "cid":f"{bid}|{cid}",
    "need_bookinfo":"1"
}
data_sec = json.dumps(data_one)         #！！！！！！！！！！！！！
#最终url调整为如下格式，直接塞入data_one不是字符串，不能通过url调用
url= f'http://dushu.baidu.com/api/pc/getChapterContent?data={data_sec}'
resp = requests.get(url)
print(resp.text)
    
```

### 3、装饰器

**通用装饰器：**

```python
def wrapper(fn):
    """
    装饰器
    :param fn: 被装饰的函数
    :return: inner
    """
    def inner(*args,**kwargs):
        """执行目标函数之前需要的操作"""
        ret = fn(*args,**kwargs)
        """执行目标函数之后需要的操作"""
        return ret
    return inner

@wrapper
def temp():
    pass
```

演示装饰器：

```python
def wrapper(fn):
    """
    装饰器
    :param fn: 被装饰的函数
    :return: inner
    """
    def inner(*args,**kwargs):
        print('降龙十八掌乔峰')
        """执行目标函数之前需要的操作"""
        ret = fn(*args,**kwargs)
        """执行目标函数之后需要的操作"""
        print('凌波微步段誉')
        return ret
    return inner

@wrapper
def temp():
    print('小李飞刀李寻欢')


if __name__ == '__main__':
    temp()
#----------------
>>>降龙十八掌乔峰
小李飞刀李寻欢
凌波微步段誉
```



## 二、进阶学习

### 1、文件存储操作

#### ①文字表格类存储

```python
import csv
i = 'Hello'
j = 'Word'
m = '!' 
f = open('文件名.csv',mode='a',encoding='utf-8')#.csv可以写成.txt等等
#'a'：文件存在写入，不存在创建，而且连续写入，不覆盖。
#'w'：文件存在写入，不存在创建，而且每次写入都覆盖文件中已有内容。
wri = csv.writer(f)#wri为自定义操作名
#f.writer(字符串)，若txt格式，直接写也可以，就不能出现列表，数据应为字符串
wri.writerow([i,j,m])#将所有项都写在同一行
#wri.writerows([i,j,m])#将每一项写在一行，且拆改字符串每个字符
f.close()#注意要关闭文件，要不然打开文件后发现什么也没有，且文件不能被删除。
```

![image-20210528112312548](C:\Users\kingb\AppData\Roaming\Typora\typora-user-images\image-20210528112312548.png)

![image-20210528112328642](C:\Users\kingb\AppData\Roaming\Typora\typora-user-images\image-20210528112328642.png)

#### ②图片存储

```python
import requests

img = requests.get(src)         #下载图片
img_name = src.split('/')[-1]   #拿到http://c8nh/yi66/tyde.jpg中最后一个下划线以后的内容，为每一个图片命名，截取的名字后面有.jpg后边无需再加
with open('bizhi/'+img_name,mode='wb') as f:  #'bizhi'为此次创建的文件夹，存储本次下载的图片。也可以不创建，直接存在外边
	f.write(img.content)            #图片写入文件     img.content是图片的字节---解码
print('over!!!',img_name)            #写入一个，输出一个over和名字
#f.close()  with相当于创建会话，f.write在内部，在外侧就不用再写f.close（）
```



### 2、requests获取url

#### 基本操作：

```python
import requests

url = 'www.baidu.com'
result = requests.get(url)   #get和post功能一样，根据网站要求选择
#get中可加入headers参数，设置访问的浏览器，或者携带cookie访问
result.encoding = 'utf-8'   #调整相对应的编码规则，防止获得的源码为乱码，utf-8、GBK之类的，可以在网页查看对应编码规则
```

```python
import requests#携带cookie访问网站

url = 'www.baidu.com'
header = {
    'cookie':'school_code=10694; cookiesession1=678B286FQRSTUV01234567898901F182; gr_user_id=377b5501-d1b8-4b3f-a29f-1b43e80d70e7; grwng_uid=95030642-a915-4e2b-a010-44b366347c86; ci_session=af98697cd1b9141d939c530f25e46ae1da78b0d3'
    }
result = requests.get(url,headers=header)   #get和post功能一样，根据网站要求选择
result.encoding= 'utf-8'   #调整相对应的编码规则，防止获得的源码为乱码，utf-8、GBK之类的，可以在网页查看对应编码规则
```



#### 代理获取：

```python
#代理访问
import requests

proxies = {
    # 'http':'https://218.60.8.83:3129'    #根据url地址，选择是用http还是https
    'https':'https://218.60.8.83:3129'     #前面是IP地址，后边是端口。
                                           #IP地址状态，【透明】基本可以使用，【高匿】基本不怎么能用
    }

url = 'https://www.baidu.com'
resp = requests.get(url,proxies=proxies)
resp.encoding = 'utf-8'
print(resp.text)
```



### 3、Xpath

**注意：**

1、Xpath复制路径之前要对比网页源代码和开发者工具是否一致，因为交给Xpath的是获取的网页源代码，搜索时直接用开发者工具的路径若不同，则会无法获得数据。

如下例，谷歌浏览器自动添加了<tbody>标签，复制后仍带有，此时需删除路径中的<tbody>标签才能获得正常的数据。

![image-20210531222314089](C:\Users\kingb\AppData\Roaming\Typora\typora-user-images\image-20210531222314089.png)

2、尽可能根据代码结构划分路径，必要时可分多步完成，尽可能避免一次到位的情况。

```python
from lxml import etree

temp = '''    代码    '''
tree = etree.XML(temp)   #转成对象，当文本为HTML语言时，需更改XML为HTML
result = tree.xpath('/根节点')   #/表示层级关系，第一个/是根节点
result = tree.xpath('/根节点/子目标节点')   
result = tree.xpath('/根节点/子目标节点/text()')   #text()表示拿子节点中的文本信息
result = tree.xpath('/根节点/子节点//子子目标节点text()')    #‘//’两个表示所有后代
result = tree.xpath('/根节点/子节点/*/子子目标节点text()')   #‘*’是通配符，取子节点下的任意目标
result = tree.xpath('/根节点/子节点/目标节点[2]/text()')   #几个相同名字的目标节点，可直接中括号＋索引，默认从1开始
result = tree.xpath("/根节点/子节点/目标节点[@href='属性值']/text()")   #目标节点中括号＋@属性名字，可直接获得该属性的text
result = tree.xpath('/根节点/子节点/几个相同的目标节点')  #此时result是一个列表，保存了几个相同节点，可直接遍历
trs = result.xpath('./标签[position()>1]')#表示标签的位置从第二个开始，一般用于放弃表头，只取数据 
# #遍历
for i in result:
    #从每一个li中提取到文字信息
    result1 = i.xpath('./i中的第一个子节点/子子节点/目标节点/text()')    #相对根节点中必须前面有一个‘./’，只有绝对根节点才可以直接用/
    #获得某个标签的属性值如：href、id、class之类的，直接@
    result2 = i.xpath('./i中的第一个子节点/子子节点/目标节点/@href')

```

### 4、re-->正则表达式

```python
url = 'https://www.91kanju.com/vod-play/541-2-1.html'
resp = requests.get(url)
txt = resp.text
#正则表达式
rex = re.compile(r'txt中尽可能唯一的任何代码(?p<自定义名字>.*?)结尾代码',re.S)#re.S扩展整个字符串，不分行检测，
m = rex.search(txt).group('自定义名字')#search检索到第一个满足的停止
return m
```

```python
import re

str1 = '''<link type="application/wlwmanifest+xml" rel="wlwmanifest" href="https://www.cnblogs.com/moning/wlwmanifest.xml" />
    <script>
        var currentBlogId = 367433;
        var currentBlogApp = 'moning';
        var cb_enable_mathjax = false;
        var isLogined = true;
        var isBlogOwner = false;
        var skinName = 'Valentine';
        var visitorUserId = 'e4e111e8-8ff3-4414-2ff4-08d91391c27c';
    </script>
        <script>'''


#正则表达式
rex = re.compile(r"currentBlogId = (?P<id>.*?);.*?skinName = '(?P<skin>.*?)';",re.S)
m = rex.search(str1)


str_id = m.group('id')       #367433
str_skin = m.group('skin')   #Valentine
print(str_id,str_skin)
#-------------
367433 Valentine
```



### 5、BeautifulSoup

```python
from bs4 import BeautifulSoup

str1 = '''<link type="application/wlwmanifest+xml" rel="wlwmanifest" href="https://www.cnblogs.com/moning/wlwmanifest.xml" />
    <script>
        var currentBlogId = 367433;
        var currentBlogApp = 'moning';
        var cb_enable_mathjax = false;
        var isLogined = true;
        var isBlogOwner = false;
        var skinName = 'Valentine';
        var visitorUserId = 'e4e111e8-8ff3-4414-2ff4-08d91391c27c';
    </script>
        <script>'''
#对象都是源代码，resp.text

main_page = BeautifulSoup(str1, 'html.parser')#告知是html文件
src = main_page.find('link')   #查找<标签>
src = main_page.find('link',type='application/wlwmanifest+xml')#若标签名相同，可增加标签中的属性值，两个条件同时约束，当标签名与Python重复时，如class，可用class_
src_1 = src.get('href')        #get<标签>中的属性值 
print(src_1)
#--------------
https://www.cnblogs.com/moning/wlwmanifest.xml

```



### 6、selenium

#### 安装

selenium原本是自动化测试软件，模拟真人操作浏览器

使用前需安装浏览器驱动，如chromedriver，要匹配自己的浏览器版本，同时放在Python解释器所在的文件夹中。

**注意：**Python文件中不能有selenium为名字的文件，要不然会报错

驱动下载地址：https://chromedriver.chromium.org/home版本一定要对应谷歌浏览器版本

谷歌浏览器版本查看：![image-20211104091059216](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211104091059216.png)

---->帮助---->关于Google Chrome

![image-20211104091626637](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211104091626637.png)

将刚刚解压的chromedriver文件放置在/usr/local/bin目录中。Mac下/usr/local/bin目录默认对于Finder是隐藏，如果需要到/usr/local/bin中去，打开Finder，然后使用command+shift+G，在弹出的弹窗中填写/usr/local/bin就可以跳到该目录了。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210629165957126.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NjMwODkwNA==,size_16,color_FFFFFF,t_70)
在终端中输入chromedriver --version验证是否安装成功
查看到安装的驱动的版本，与本地浏览器的版本一致后，则可正常运行代码啦～





#### 对象页面切换

```python
from selenium.webdriver import Chrome

web = Chrome()
#···省略···已打开主页面

#窗口选项卡之间的切换
#-----------------
web.switch_to_window(web.window_handles[-1])
#window_handles就是选项卡列表，直接调用索引切换
web.close()#关闭子窗口
web.switch_to_window(web.window_handles[0])#回到主窗口
#-----------------

#网页将视频嵌套在iframe中的切换
#-----------------
iframe123 = web.find_element_by_xpath('//*[@id="player_iframe"]') #先找到iframe
web.switch_to.frame(iframe123)    #切换到iframe
#开始操作，爬取等
web.switch_to.default_content     #切换回原页面
#-----------------

```

#### 无头浏览器

```python
from selenium.webdriver import Chrome
from selenium.webdriver.chrome.options import Options  # 无头浏览器

# 无头浏览器
# 准备好配置参数
opt = Options()
opt.add_argument('--headless')
opt.add_argument('--disable-gpu')

web = Chrome(options=opt)  # 无头浏览器对象
# web = Chrome()           # 普通对象
```



#### 模拟鼠标操作

<font color='red'>**！！！必须在后边加上.perform（） 表示执行操作，否则事件链不执行。**</font>

**ActionChains方法列表**

click(on_element=None) ——单击鼠标左键

click_and_hold(on_element=None) ——点击鼠标左键，不松开

context_click(on_element=None) ——点击鼠标右键

double_click(on_element=None) ——双击鼠标左键

drag_and_drop(source, target) ——拖拽到某个元素然后松开

drag_and_drop_by_offset(source, xoffset, yoffset) ——拖拽到某个坐标然后松开

key_down(value, element=None) ——按下某个键盘上的键

key_up(value, element=None) ——松开某个键

move_by_offset(xoffset, yoffset) ——鼠标从当前位置移动到某个坐标

move_to_element(to_element) ——鼠标移动到某个元素

move_to_element_with_offset(to_element, xoffset, yoffset) ——移动到距某个元素（左上角坐标）多少距离的位置

perform() ——执行链中的所有动作

release(on_element=None) ——在某个元素位置松开鼠标左键

send_keys(*keys_to_send) ——发送某个键到当前焦点的元素

send_keys_to_element(element, *keys_to_send) ——发送某个键到指定元素

**示例1：**

```python
from selenium.webdriver.common.action_chains import ActionChains

ActionChains(web).drag_and_drop_by_offset(button,300,0).perform()
# 点击鼠标并拖拽，从button位置，横向移动300，纵向不变
# 事件链操作，拖拽在x,y坐标系中，以button为顶点建立坐标系，长度用截图工具可直观看到
```

**示例2：**

```python
from selenium.webdriver.common.action_chains import ActionChains

ActionChains(web).move_to_element_with_offset(img_base,50,20).click().perform()
#移动鼠标到img_base位置，建立坐标系，点击坐标系中（50,20）位置
```

#### 处理下拉菜单

```python
from selenium.webdriver import Chrome
from selenium.webdriver.support.select import Select   # 处理下拉菜单
import time

web = Chrome()       
web.get('https://www.endata.com.cn/BoxOffice/BO/Year/index.html')

# 先定位到下拉菜单
sel_element = web.find_element_by_xpath('//*[@id="OptionDate"]')
# 对元素进行包装
sel = Select(sel_element)
# 让浏览器进行调整选项
for i in range(len(sel.options)):
    # 三种查找方法，<option value="2021">2021年</option>
    # index()用列表的索引，value()用属性值更换，visible_text()用菜单中的文本更换
    sel.select_by_index(i)          #本例中索引值
    # sel.select_by_value()         #本例中2021
    # sel.select_by_visible_text()  #本例中2021年
    time.sleep(1)
    #开始抓取数据
    table123 = web.find_element_by_xpath('//*[@id="TableList"]/table')
    tbody_list = table123.find_elements_by_xpath('./tbody/tr') # element只查找第一个，elements查找多个，形成列表
    for j in tbody_list:#处理文件，写入《票房数据》文件夹，并每年度形成一个文件
        name = j.find_element_by_xpath('./td[2]/a/p').text
        type = j.find_element_by_xpath('./td[3]').text
        box_office = j.find_element_by_xpath('./td[4]').text
        country = j.find_element_by_xpath('./td[7]').text
        date = j.find_element_by_xpath('./td[8]').text
        years = web.find_element_by_xpath(f'//*[@id="OptionDate"]/option[{i+1}]').text
        f =  open('票房数据/'+f'{years}票房数据.csv',mode='a',encoding = 'utf-8')
        wri = csv.writer(f)
        wri.writerow([name,type,box_office,country,date])
f.close()
web.close()
```

#### selenium基本操作

```python
from selenium.webdriver import Chrome
from selenium.webdriver.common.keys import Keys    #获得伪键盘操作，如enter
import time

web = Chrome()#创建对象
web.get('https://www.lagou.com')  #进入网页

el = web.find_element_by_xpath('//*[@id="changeCityBox"]/p[1]/a')#浏览器F12直接代码右键copy xpath
el.click()    #点击操作
time.sleep(1) #沉睡1秒

web.find_element_by_xpath('//*[@id="search_input"]').send_keys('Python',Keys.ENTER)
#xpath找到搜索框，send_keys发送搜索内容，同时携带Keys.ENTER，输入完成直接回车
# 也可以重复上边操作，xpath找到‘搜索’，通过click（）点击

# li_list = web.find_element_by_xpath('//*[@id="s_position_list"]/ul/li[1]')
li_list = web.find_elements_by_xpath('//*[@id="s_position_list"]/ul/li')#复制过来的li[1],要获得的是所有li，去掉末尾的[1]
#注意！！！这里用的elements，多了一个s，表示查找所有，element表示 查找第一个就停止
for li in li_list:
    job_name = li.find_element_by_tag_name('h3').text  #tag_name标签名
    job_price = li.find_element_by_xpath('./div[1]/div[1]/div[2]/div/span').text
    company = li.find_element_by_xpath('./div[1]/div[2]/div[1]/a').text
    base = li.find_element_by_tag_name('em').text
    need = li.find_element_by_xpath('./div[1]/div[1]/div[2]/div').text
    print(company,job_name,job_price,need,base)

```

#### 获取网页中Elements中的代码

因为网页看到的Elements和网页源代码不一致，有的信息时通过请求加载进来的，并不直接存储于网页源代码中，所以F12看到的Elements信息需用page_source来获取

```python
#···同上 省略一万字···
txt = web.page_source
```

#### 浏览器识别为自动化软件

**软件启动：**

![image-20210615174729987](C:\Users\kingb\AppData\Roaming\Typora\typora-user-images\image-20210615174729987.png)

**手动启动：**

![image-20210615174954178](C:\Users\kingb\AppData\Roaming\Typora\typora-user-images\image-20210615174954178.png)

解决方法：

```python
from selenium.webdriver.chrome.options import Options
# 浏览器识别为自动化测试，登录失败解决
# 1、谷歌浏览器版本低于88
# 亲测, 88版本之前可以⽤.
# web = Chrome()
#
#
web.execute_cdp_cmd("Page.addScriptToEvaluateOnNe
wDocument", {
# "source": """
# navigator.webdriver = undefined
# Object.defineProperty(navigator,
'webdriver', {
# get: () => undefined
# })
# """
# })
# 2、谷歌浏览器版本大于等于88
option = Options()
option.add_experimental_option('excludeSwitches',['enable-automation']) # 此行可写可不写
option.add_argument('--disable-blink-features=AutomationControlled')

web = Chrome(options=option)
```

#### **实例登录12306：**

```python
from selenium.webdriver import Chrome
from selenium.webdriver.common.action_chains import ActionChains
from chaojiying import Chaojiying_Client
from selenium.webdriver.chrome.options import Options
import time

# 13206中识别为自动化测试，登录失败解决
# 1、谷歌浏览器版本低于88
# web = Chrome()
# web.execute_cdp_cmd("Page.addScriptToEvaluateOnNewDocument", {
#     "source": """
#                 navigator.webdriver = undefined
#                 Object.defineProperty(navigator,'webdriver', {
#                      get: () => undefined
#                 })
#             """
# })
# 2、谷歌浏览器版本大于等于88
option = Options()
option.add_experimental_option('excludeSwitches',['enable-automation']) # 可写可不写
option.add_argument('--disable-blink-features=AutomationControlled')


# 创建对象
web = Chrome(options=option) # 浏览器对象
chaojiying = Chaojiying_Client('13139313534', '13139313534', '918377') # 超级鹰对象

# 打开主页面
web.get('https://kyfw.12306.cn/otn/resources/login.html')
time.sleep(2)
web.find_element_by_xpath('/html/body/div[2]/div[2]/ul/li[2]/a').click()
time.sleep(3)

# 输入账号密码
web.find_element_by_xpath('//*[@id="J-userName"]').send_keys('888888888')
web.find_element_by_xpath('//*[@id="J-password"]').send_keys('888888888')
time.sleep(2)

# 处理验证码

# 找到验证码图片
img_base = web.find_element_by_xpath('//*[@id="J-loginImg"]')
coordinate = chaojiying.PostPic(img_base.screenshot_as_png,9004)['pic_str'] #将验证码截图传给超级鹰，返回坐标
# 9004-->坐标多选,返回1~4个坐标,如:x1,y1|x2,y2|x3,y3
# 字典中'pic_str'为返回的验证码必要信息，此处返回坐标点
coordinate_list = coordinate.split('|')
for i in coordinate_list:
    x_x = int(i.split(',')[0])   #此时虽然拆分出坐标，但是是'字符串'格式，需加int转换成  数值。
    y_y = int(i.split(',')[1])
    ActionChains(web).move_to_element_with_offset(img_base,x_x,y_y).click().perform()
    # move_to_element 移动鼠标到此前找到的element位置，如img_base
    # with_offset    移动到位置之后，以该位置顶点为原点，建立坐标系，通过x，y偏移量 移动鼠标到 精确位置
    # ActionChains.......一系列定义了一个事件链，如何操作，最后perform表示执行，不加perform，即使有click也不会点击
time.sleep(5)

# 点击登陆
web.find_element_by_xpath('//*[@id="J-login"]').click()

time.sleep(5)  # 必须要睡会，还要睡够，要不然找不到界面直接报错

# 解决滑块验证
button = web.find_element_by_xpath('//*[@id="nc_1_n1z"]')
ActionChains(web).drag_and_drop_by_offset(button,300,0).perform()
# 事件链操作，拖拽在x,y坐标系中，以button为顶点建立坐标系，长度用截图工具可直观看到
```

### 7、多线程/进程

**进程**是资源单位

**线程**是执行单位

启动每一个程序默认都会有一个主线程

```python
#单线程
def func():
 for i in range(1000):
 	print("func", i)

if __name__ == '__main__':
 func()              #此时会先执行函数，完成后再执行主程序main
 for i in range(1000):
 	print("main", i)
```

```python
#多线程
#方法一
from threading import Thread    #导入线程类
def func(name):                 #设置一个参数，便于区分，也可不设置
    for i in range(1000):
 	   print(name, i)

if __name__ == '__main__':
    t = Thread(target=func,args=('第二个进程',))#传参必须是元组，一个参数后便要加逗号，保证元组
    t.start()                           #此时告知第二线程可以开始了，但是实际开始时间由CPU决定
    t2 = Thread(target=func,args=('第三个进程',))
    t2.start()
    for i in range(1000):
 	   print("main", i)

        
#-----------------此时同时输出，内容会交叉
>>>第三个进程 998
第三个进程 999

第二个进程 750
第二个进程 751
第二个进程 752
...
第二个进程 998
第二个进程 973
main 974
main 975
main 976

#方法二
from threading import Thread
class MyThread(Thread):        #定义线程类的子类，直接在类中更改。
   def run(self):
   	   for i in range(1000):
 	      print("func", i)

if __name__ == '__main__':
   t = MyThread()              
   t.start()
   for i in range(1000):
  	  print("main", i)

#-----------------此时同时输出，内容会交叉
>>>func 840
func 825841

main 826
main 827
main 828
main 829
main 830func 842
func 843
```

**多线程和多进程的在Python中使用方法完全相同**

```python
from multiprocessing import Process   #多进程
from threading import Thread          #多线程

#应用时将上述例子中的Thread换成Process即可完全通用
```

**线程池：**固定池中有N（具体个数）个线程，每次发送需求给池子，他们内部自己分配执行。

```python
from concurrent.futures import ThreadPoolExecutor,ProcessPoolExecutor
#ThreadPoolExecutor为线程池
#ProcessPoolExecutor为进程池，用法完全相同
def fn(name):
    for i in range(50):
        print(name,i)
    
if __name__ == '__main__':
    #创建线程池
    with ThreadPoolExecutor(50) as t:
        for i in range(1000):
            t.submit(fn,name=f'线程{i}')   #括号中第一个为调用函数，第二个传参
    #等待线程池中的任务全部执行完毕，才继续执行（守护）
    print('over!!')
  
```

### 8、协程

协程：单线程情况下，多任务异步操作

input（）、requests（）返回数据前，程序都是处于阻塞状态，**一般情况下，当程序处于IO操作时，线程都会处于阻塞状态**，此时CPU其实并没有为你⼯作,为了让CPU⼀直为我⽽⼯作，想办法让我的线程遇到了IO操作就挂起, 留下的都是运算操作，当线程中遇到了IO操作的时候, 将线程中的任务进⾏切换, 切换成⾮ IO操作，等原来的IO执⾏完了. 再恢复回原来的任务中，这个执行过程就是协程。宏观上看到的就是多个任务一起执行。

```python
import asyncio 

async def func():
   print("我是协程")
if __name__ == '__main__':
   # print(func()) # 注意, 此时拿到的是⼀个协程对象,和⽣成器差不多.该函数默认是不会这样执⾏的
   coroutine = func()
   asyncio.run(coroutine) # ⽤asyncio的run来执⾏协程
   
   # lop = asyncio.get_event_loop()
   # lop.run_until_complete(coroutine) # 这两句等价于asyncio.run(coroutine)
```

```python
import asyncio
import time
# await: 当该任务被挂起后,CPU会⾃动切换到其他任务中
async def func1():
   print("func1, start")
   await asyncio.sleep(3)
   print("func1, end")
async def func2():
   print("func2, start")
   await asyncio.sleep(4)
   print("func2, end")
async def func3():
   print("func3, start")
   await asyncio.sleep(2)
   print("func3, end")
async def main():
   print("start")
   # # 添加协程任务
   # t1 = asyncio.create_task(func1())
   # t2 = asyncio.create_task(func2())
   # t3 = asyncio.create_task(func3())
   # ret1 = await t1
   # ret2 = await t2
   # ret3 = await t3
   tasks = [
         asyncio.create_task(func1()),
         asyncio.create_task(func2()),
         asyncio.create_task(func3())
         ]
   # ⼀次性把所有任务都执⾏
   done, pedding = await asyncio.wait(tasks)
   #await asyncio.wait(tasks)与上一行同样的效果
   print("end")
if __name__ == '__main__':
     start = time.time()
     asyncio.run(main())
     print(time.time() - start)
#----------
>>>
start
func2, start
func1, start
func3, start
func3, end
func1, end
func2, end
end
4.152714252471924   #仅需4s，按顺序执行，sleep3+4+2=9s多才能执行完毕。

```

#### **协程爬虫模板（套用）：**

```python
import asyncio
async def download(url):#单页面爬取过程
   print("开始抓取")
   await asyncio.sleep(3) # 我要开始下载了
   print("下载结束", url)
   return "源码"

async def main():#遍历N个链接
   urls = [
   "http://www.baidu.com",
   "http://www.h.com",
   "http://luoyonghao.com"
   ]
# ⽣成任务列表
   tasks = [asyncio.create_task(download(url)) for url in urls]  #生成器
   done, pedding = await asyncio.wait(tasks)
   for d in done:
       print(d.result())
if __name__ == '__main__':
   asyncio.run(main())
```

### 6、aiohttp模块

```python
import asyncio
import aiohttp
import requests#对比普通请求用
import time#对比计时

urls = [
      'http://kr.shanghai-jiuxin.com/file/2021/0602/c4ab41ce2c692d8f7a92feb54384fb6c.jpg',
      'http://kr.shanghai-jiuxin.com/file/2021/0601/fba0a3a2fbf7368e2134fa8cd6dc0dd9.jpg',
      'http://kr.shanghai-jiuxin.com/file/2021/0602/2e96200707ae7d2391f01c00959cc493.jpg'
      ]

async def download(url):
    #  s = aiohttp.ClientSession()   ====等价于===requests,后边可直接用s.get()，s.post()之类的
    name = url.split('/')[-1]
    async with aiohttp.ClientSession() as session:
        async with session.get(url) as resp:
            #resp.content.read()等价于requests获得的resp.content
            #resp.text()等价于requests获得的resp.text
            with open (name,mode='wb') as f:
                f.write(await resp.content.read())      #读取内容是异步的，需要await挂起
            print(f'完成{name}')

async def main():
   tasks = []#一个tasks列表存放，需要异步的N个操作
   for url in urls:
      tasks.append(asyncio.create_task(download(url)))
   await asyncio.wait(tasks)
def download1(url):#对比速度用
    name = url.split('/')[-1]
    resp = requests.get(url)
    with open (name,mode='wb') as f:
        f.write(resp.content)
    print(f'完成{i}个')

if __name__ == '__main__':
   time_start = time.time()
   asyncio.run(main())#异步协程开始命令
   # for url in urls:#同步执行download1函数，对比速度
   #     download1(url)
   #     i+=1
   print(time.time()-time_start)


```

#### 协程实例：百度小说爬取

```python
import requests
import asyncio
import aiohttp

async def getChapterContent(bo_id,cid,title):
    url_txt = 'http://dushu.baidu.com/api/pc/getChapterContent?data={"book_id":"'+bo_id+'","cid":"'+bo_id+'|'+cid+'","need_bookinfo":1}'
    async with aiohttp.ClientSession() as session:
        async with session.get(url_txt) as resp:
            dic = await resp.json()
            txt = dic['data']['novel']['content']
            with open (f'novel/{title}.txt', mode='a',encoding='utf-8') as f:
                f.write(txt)
                print(title + '已完成！')
async def getCatalog(url,bo_id):
    resp = requests.get(url)
    dic = resp.json()
    tasks = []
    for items in dic['data']['novel']['items']:
        cid = items['cid']
        title = items['title']
        tasks.append(asyncio.create_task(getChapterContent(bo_id, cid, title)))
    await asyncio.wait(tasks)


if __name__ == '__main__':
    bo_id = '4306063500'
    urlone = 'http://dushu.baidu.com/api/pc/getCatalog?data={"book_id":"'+bo_id+'"}'
    #采用三个字符串拼接，因为有大括号直接f需要用转译符
    asyncio.run(getCatalog(urlone,bo_id))


```

## 三、算法

### 1、二叉树

#### 二叉搜索树的建立及遍历

```python


class BinaryTree:
    """建立搜索二叉树"""

    def __init__(self, num):
        self.val = num
        self.left = None
        self.right = None
        if type(num) == list:
            self.num = num[0]
            for n in num[1:]:
                self.insert(n)
        else:
            self.num = num

    def insert(self, num):
        """对搜索二叉树插入数据"""
        bt = self
        while True:
            if num <= bt.num:
                if bt.left == None:
                    bt.left = BinaryTree(num)
                    break
                else:
                    bt = bt.left
            else:
                if bt.right == None:
                    bt.right = BinaryTree(num)
                    break
                else:
                    bt = bt.right


def front_recursion(root):
    """利用递归实现树的前序遍历"""

    if root is None:
        return

    print(root.num)
    front_recursion(root.left)
    front_recursion(root.right)


def middle_recursion(root):
    """利用递归实现树的中序遍历"""

    if root is None:
        return

    middle_recursion(root.left)
    print(root.num)
    middle_recursion(root.right)

def back_recursion(root):
    """利用递归实现树的后序遍历"""

    if root is None:
        return

    back_recursion(root.left)
    back_recursion(root.right)
    print(root.num)


def front_stack(root):
    """利用堆栈实现树的前序遍历"""

    if root is None:
        return

    stack = []
    node = root
    while node or stack:
        # 从根节点开始，一直找它的左子树
        while node:
            print(node.num)
            stack.append(node)
            node = node.left
        # while结束表示当前节点node为空，即前一个节点没有左子树了
        node = stack.pop()
        # 开始查看它的右子树
        node = node.right



def middle_stack(root):
    """利用堆栈实现树的中序遍历"""

    if root is None:
        return

    stack = []
    node = root
    while node or stack:
        # 从根节点开始，一直找它的左子树
        while node:
            stack.append(node)
            node = node.left
        # while结束表示当前节点node为空，即前一个节点没有左子树了
        node = stack.pop()
        print(node.num)
        # 开始查看它的右子树
        node = node.right



def back_stack(root):
    """利用堆栈实现树的后序遍历"""

    if root is None:
        return

    stack1 = []
    stack2 = []
    node = root
    stack1.append(node)
    # 这个while循环的功能是找出后序遍历的逆序，存在stack2里面
    while stack1:
        node = stack1.pop()
        if node.left:
            stack1.append(node.left)
        if node.right:
            stack1.append(node.right)
        stack2.append(node)
    # 将stack2中的元素出栈，即为后序遍历次序
    while stack2:
        print(stack2.pop().num)


def level_queue(root):
    """利用队列实现树的层次遍历"""

    if root is None:
        return

    queue = []
    node = root
    queue.append(node)
    while queue:
        node = queue.pop(0)
        print(node.num)
        if node.left is not None:
            queue.append(node.left)
        if node.right is not None:
            queue.append(node.right)


if __name__ == '__main__':
    # 先输入结点总数n
    n = eval(input())

    # 输入n个结点，并加入列表
    num = []
    for i in range(n):
        num.append(eval(input()))
    bt = BinaryTree(num)

    print('队列实现层次遍历:')
    level_queue(bt)
    print('递归实现前序遍历:')
    front_recursion(bt)
    print('递归实现中序遍历:')
    middle_recursion(bt)
    print('递归实现后序遍历:')
    back_recursion(bt)
    print('堆栈实现前序遍历:')
    front_stack(bt)
    print('堆栈实现中序遍历:')
    middle_stack(bt)
    print('堆栈实现后序遍历:')
    back_stack(bt)

```

#### 普通二叉树的建立及遍历

```python

class Node(object):
    """节点类"""

    def __init__(self, element=-1, l_child=None, r_child=None):
        self.element = element
        self.l_child = l_child
        self.r_child = r_child


class Tree(object):
    """树类"""

    def __init__(self):
        self.root = Node()
        self.queue = []

    def add_node(self, element):
        """为树添加节点"""

        node = Node(element)
        # 如果树是空的，则对根节点赋值
        if self.root.element == -1:
            self.root = node
            self.queue.append(self.root)
        else:
            tree_node = self.queue[0]
            # 此结点没有左子树，则创建左子树节点
            if tree_node.l_child is None:
                tree_node.l_child = node
                self.queue.append(tree_node.l_child)
            else:
                tree_node.r_child = node
                self.queue.append(tree_node.r_child)
                # 如果该结点存在右子树，将此节点丢弃
                self.queue.pop(0)

    def front_recursion(self, root):
        """利用递归实现树的前序遍历"""

        if root is None:
            return

        print(root.element)
        self.front_recursion(root.l_child)
        self.front_recursion(root.r_child)

    def middle_recursion(self, root):
        """利用递归实现树的中序遍历"""

        if root is None:
            return

        self.middle_recursion(root.l_child)
        print(root.element)
        self.middle_recursion(root.r_child)

    def back_recursion(self, root):
        """利用递归实现树的后序遍历"""

        if root is None:
            return

        self.back_recursion(root.l_child)
        self.back_recursion(root.r_child)
        print(root.element)

    @staticmethod
    def front_stack(root):
        """利用堆栈实现树的前序遍历"""

        if root is None:
            return

        stack = []
        node = root
        while node or stack:
            # 从根节点开始，一直找它的左子树
            while node:
                print(node.element)
                stack.append(node)
                node = node.l_child
            # while结束表示当前节点node为空，即前一个节点没有左子树了
            node = stack.pop()
            # 开始查看它的右子树
            node = node.r_child

    @staticmethod
    def middle_stack(root):
        """利用堆栈实现树的中序遍历"""

        if root is None:
            return

        stack = []
        node = root
        while node or stack:
            # 从根节点开始，一直找它的左子树
            while node:
                stack.append(node)
                node = node.l_child
            # while结束表示当前节点node为空，即前一个节点没有左子树了
            node = stack.pop()
            print(node.element)
            # 开始查看它的右子树
            node = node.r_child

    @staticmethod
    def back_stack(root):
        """利用堆栈实现树的后序遍历"""

        if root is None:
            return

        stack1 = []
        stack2 = []
        node = root
        stack1.append(node)
        # 这个while循环的功能是找出后序遍历的逆序，存在stack2里面
        while stack1:
            node = stack1.pop()
            if node.l_child:
                stack1.append(node.l_child)
            if node.r_child:
                stack1.append(node.r_child)
            stack2.append(node)
        # 将stack2中的元素出栈，即为后序遍历次序
        while stack2:
            print(stack2.pop().element)

    @staticmethod
    def level_queue(root):
        """利用队列实现树的层次遍历"""

        if root is None:
            return

        queue = []
        node = root
        queue.append(node)
        while queue:
            node = queue.pop(0)
            print(node.element)
            if node.l_child is not None:
                queue.append(node.l_child)
            if node.r_child is not None:
                queue.append(node.r_child)


if __name__ == '__main__':
    """主函数"""

    # 生成十个数据作为树节点
    # 手动输入N个结点，再逐行录入n个元素
    tree = Tree()
    n = eval(input())
    for i in range(n):
        tree.add_node(eval(input()))

    print('队列实现层次遍历:')
    tree.level_queue(tree.root)
    print('递归实现前序遍历:')
    tree.front_recursion(tree.root)
    print('递归实现中序遍历:')
    tree.middle_recursion(tree.root)
    print('递归实现后序遍历:')
    tree.back_recursion(tree.root)

    print('堆栈实现前序遍历:')
    tree.front_stack(tree.root)
    print('堆栈实现中序遍历:')
    tree.middle_stack(tree.root)
    print('堆栈实现后序遍历:')
    tree.back_stack(tree.root)
```

