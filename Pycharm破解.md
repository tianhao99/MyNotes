# Pycharm破解

##  1、卸载旧版本

 

## 2、官网下载新版本，M系列芯片的，可以下载ARM版本

- 默认Intel版本，点箭头会显示Apple Silicon这个就是适配M芯片的 

![img](https://img-blog.csdnimg.cn/5617c0fc0c2141d5b776368bd7071d5f.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)编辑



## 3、安装idea 打开后要登录JetBrains 账户，可以在他官网注册一个，登录完成后退出idea

## 4、下载破解插件

- 将破解插件放在一个固定的地方，傍边可以放一个文档注释，readme.txt之类的，放止以后忘了这个文件夹是干嘛的，最后给删除了，就GG了
- 插件文末免费获取

## 5、找到配置文件

- 找到idea.vmoptions文件，我的位置如下
- 建议打开访达，点击前往  /Users/用户/Library/Application Support/JetBrains/
- 在文件夹下，按照我下边这个位置，找到idea.vmoptions文件，打开修改

## 6、修改配置文件内容【追加，原本里面有其他内容不用管】

```bash
# 补丁的绝对路径【这个是我的存放路径】
-javaagent:/Users/用户/Tools/ja-netfilter/ja-netfilter.jar

# 最新 IDEA 版本需要添加下面两行，否则会报 key valid
--add-opens=java.base/jdk.internal.org.objectweb.asm=ALL-UNNAMED
--add-opens=java.base/jdk.internal.org.objectweb.asm.tree=ALL-UNNAMED
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

## 7、重启idea或者PyCharm，用激活码激活

![img](https://img-blog.csdnimg.cn/68c65de60a154684870c79195bfe239d.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)编辑

##  8、idea和PyCharm的激活码

激活码和插件打包放在资源里了，大家可以免费下载

[IDEA和PyCharm技术资料-Java文档类资源-CSDN下载](https://download.csdn.net/download/m0_51360693/86396614)





转载于https://www.exception.site/article/29

原文是Windows的，这里我分享了Mac版本的破解过程，遇到无法启动的情况，可以评论我