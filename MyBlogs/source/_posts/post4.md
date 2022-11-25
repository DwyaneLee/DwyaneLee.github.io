---
title: 10个有趣的高级脚本
date: 2022-11-25 15:34:08
tags:
    - #Python
categories:
    - #Script
feature: true
cover: /img/sio.png
---

# 10个有趣的高级脚本  

## ▍1、Jpg转Png
- 图片格式转换，以前可能第一时间想到的是【格式工厂】这个软件。
- 如今编写一个Python脚本就能完成各种图片格式的转换，此处以jpg转成png为例。
- 有两种解决方法，都分享给大家。
```python
# 图片格式转换, Jpg转Png

# 方法①
from PIL import Image

img = Image.open('test.jpg')
img.save('test1.png')


# 方法②
from cv2 import imread, imwrite

image = imread("test.jpg", 1)
imwrite("test2.png", image)
```

## ▍2、PDF加密和解密
- 如果你有100个或更多的PDF文件需要加密，手动进行加密肯定是不可行的，极其浪费时间。
- 使用Python的pikepdf模块，即可对文件进行加密，写一个循环就能进行批量加密文档。
```python
# PDF加密
import pikepdf

pdf = pikepdf.open("test.pdf")
pdf.save('encrypt.pdf', encryption=pikepdf.Encryption(owner="your_password", user="your_password", R=4))
pdf.close()
```
- 有加密那么便会有解密，代码如下。
```python
# PDF解密
import pikepdf

pdf = pikepdf.open("encrypt.pdf",  password='your_password')
pdf.save("decrypt.pdf")
pdf.close()
```

## ▍3、获取电脑的配置信息
- 很多小伙伴可能会使用鲁大师来看自己的电脑配置，这样还需要下载一个软件。
- 使用Python的WMI模块，便可以轻松查看你的电脑信息。
```python
# 获取计算机信息
import wmi


def System_spec():
    Pc = wmi.WMI()
    os_info = Pc.Win32_OperatingSystem()[0]
    processor = Pc.Win32_Processor()[0]
    Gpu = Pc.Win32_VideoController()[0]
    os_name = os_info.Name.encode('utf-8').split(b'|')[0].decode('utf-8')
    ram = float(os_info.TotalVisibleMemorySize) / 1048576
    print(f'操作系统: {os_name}')
    print(f'CPU: {processor.Name}')
    print(f'内存: {ram} GB')
    print(f'显卡: {Gpu.Name}')
    print("\n计算机信息如上 ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑")

if __name__ == '__main__':
    System_spec()
```
- 就以我自己的电脑为例，运行代码就能看到配置
```text
操作系统: Microsoft Windows 10 专业版
CPU: Intel(R) Core(TM) i3-10100 CPU @ 3.60GHz
内存: 15.833415985107422 GB
显卡: Intel(R) UHD Graphics 630

计算机信息如上 ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑
```