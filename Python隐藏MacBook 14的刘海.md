# Python隐藏MacBook 14的刘海

## 实现原理：

主要是通过修改图片尺寸，调整壁纸刘海部分为黑色，形成隐藏刘海的效果

![image-20220328215111988](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220328215111988.png)

## 1、PS修改

![image-20220328220226322](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220328220226322.png)

[PS模板、点击下载](https://download.csdn.net/download/m0_51360693/85049776)

查看显示器尺寸为：3024×1964

![image-20220328215303656](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220328215303656.png)

刘海部分是65像素，也就是说我们需要如下操作

- 创建一个纯黑色的图像
  - 尺寸：==3024×1964==
  - 颜色：黑色
- 调整目标壁纸
  - 尺寸：==3024×1899==
- 添加壁纸到纯黑色画布上
- 保存输出



## 2、Python修改

这里原理是相同的，只不过是通过代码实现了

代码如下：

```python
from PIL import Image  #Pillow

def ResizeImage(imgin, imgout, width, height):
    # 打开文件
    img = Image.open(imgin)
    # 调整文件尺寸    尺寸留出上方刘海65像素的位置
    out = img.resize((width, height-65), Image.ANTIALIAS)
    # 创建新的背景图，颜色为黑色，尺寸是显示器尺寸3024×1964
    markImg = Image.new('RGB', (width, height), color=0)
    # 合并图片，从65像素位置开始
    markImg.paste(out,(0,65))
    # 保存图片
    markImg.save(imgout)
    exit()

if __name__ == '__main__':
    
    # 选择图片位置
    filein = input("请输入要更改图片路径: ")
    fileout = filein.split(".")[0] + '_finish.png'
    
    width = 3024
    height = 1964
    
    ResizeImage(filein, fileout, width, height)
```

运行后，输入图片的地址，回车即可

![image-20220328220018855](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20220328220018855.png)

得到图片==picture_finish.png==，直接设置为壁纸就可以了



## 3、最终效果

![IMG_5993](https://pledge99.oss-cn-beijing.aliyuncs.com/img/IMG_5993.jpg)