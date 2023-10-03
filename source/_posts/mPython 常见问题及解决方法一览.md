---
abbrlink: ''
categories:
- - 技术
copyright: 转载
date: '2023-07-21T17:04:50.061213+08:00'
cover: /images/uploads/IMG_20230721_172244.jpg
tags:
- mPython
- Python
thumbnail: /images/uploads/IMG_20230721_172244.jpg
title: mPython 常见问题及解决方法一览
top: true
updated: 2023-7-21T17:38:6.277+8:0
---
> 注意：本贴转载于 mPython 官方账号，原文请查看 [常见问题及解决方法一览（持续更新） - 掌控板,创客教育,STEAM,编程教育 (labplus.cn)](https://labplus.cn/posts/609893054d982b612f5dfd76)，我只是优化了一下阅读体验

本贴所包含的问题大多是常见的主流问题，可能会有小伙伴报一样的错误但是按照下列问题中的解决方法可能无法解决，对于无法解决的问题，请根据[提问指南](https://www.labplus.cn/posts/60988df64d982b612f5dfd67)来提出->[提问指南](https://www.labplus.cn/posts/60988df64d982b612f5dfd67)

> **tips：可以使用“Ctrl”+“F”在页面内搜索,善用“Ctrl”+“F”**

## 其它帮助外链：

mPython图形化代码查阅帮助文档[https://mpythonsoftware.readthedocs.io/zh/latest/](https://mpythonsoftware.readthedocs.io/zh/latest/)

mPython代码查阅帮助文档[https://mpython.readthedocs.io/zh/master/index.html](https://mpython.readthedocs.io/zh/master/index.html)

mPython AI产品文档[https://labplus.readthedocs.io/zh/master/AI/index.html](https://labplus.readthedocs.io/zh/master/AI/index.html)

Labplus盛思维基百科[http://wiki.labplus.cn/](http://wiki.labplus.cn/)

掌控板硬件代码[https://github.com/labplus-cn/mpython](https://github.com/labplus-cn/mpython)

## 常见问题一览

### OSError: [Errno 110] ETIMEDOUT

![](https://qiniu.makeymonkey.com/1620611663237image.png?imageView2/2/w/800/auto-orient/format/jpg)

多数情况下解决方案：检查拓展板电源是否打开，拓展板可能没电或者电量过低。

#### 延伸错误：

> OSError: [Errno ‘XXX’]类错误 ，对于此类问题，下面的解决办法对于大多数情况是有效的。

> OSError: [Errno 1]   不允许操作

> OSError: [Errno 2]  文件或目录不存在   解决方法：如果是掌控板的资源文件，重新刷录固件；如果是自己上传的资源文件，重新上传

> OSError: [Errno 3]  没有此类进程

> OSError: [Errno 4]  中断的系统调用

> OSError: [Errno 5]   I/O错误

> OSError: [Errno 6]   没有此类设备或地址

> OSError: [Errno 7]  参数列表太长

> OSError: [Errno 8]  执行格式错误

> OSError: [Errno 9]  错误的文件编号

> OSError: [Errno 10]  没有子进程

> OSError: [Errno 11]  再试一次

> OSError: [Errno 12]  内存不足

> OSError: [Errno 13]  权限被拒绝

> OSError: [Errno 14]  错误的地址

> OSError: [Errno 15]  需要阻止设备

> OSError: [Errno 16]  设备或资源繁忙

> OSError: [Errno 17]  文件已存在

> OSError: [Errno 18]  跨设备链接

> OSError: [Errno 19]  没有此类设备。请检查：1、扩展板供电；2、I2C外设连接线；3、更换I2C外设。   解决方法：检查扩展板电源开关是否打开，是否低电量，检查线路和是否接入对应器件，所使用图形化代码是否为器件对应图形化代码

> OSError: [Errno 20]  不是目录

> OSError: [Errno 21]  是一个目录

> OSError: [Errno 22]  参数无效

> OSError: [Errno 23]  文件表溢出

> OSError: [Errno 24]  打开太多文件

> OSError: [Errno 25]  不是打字机

> OSError: [Errno 26]  文本文件繁忙

> OSError: [Errno 27]  文件太大

> OSError: [Errno 28]  设备上没有剩余空间      解决方法：清理掌控板的存储空间，如不知道怎么清理存储空间可直接刷入固件。

> OSError: [Errno 29]  非法搜寻

> OSError: [Errno 30]  只读文件系统

> OSError: [Errno 31]  链接太多

> OSError: [Errno 32]  Broken pipe

> OSError: [Errno 33]  数学参数超出函数域

> OSError: [Errno 34]  数学结果无法表示

> OSError: [Errno 97]  协议不支持的地址族

> OSError: [Errno 104]  连接超时   解决方法：检查电源有没有打开、接线有没有接错、所使用图形化代码是否为对应元器件代码；若使用到网络，检查网络是否畅通，填写的网络路径是否能够连接

> OSError: [Errno 110]  连接超时   解决方法：检查电源有没有打开、接线有没有接错、所使用图形化代码是否为对应元器件代码；若使用到网络，检查网络是否畅通，填写的网络路径是否能够连接

> OSError: [Errno 113]  路由不可达   解决方法：检查ip地址、主题名称等是否填错，尝试更换wifi或热点，检查防火墙

> OSError: [Errno 115]  正在进行中的操作

> OSError: [Errno 118]  主机无法访问

> OSError: [Errno 261]  定时器冲突

## NameError: name 'XXX' isn't defined

![](https://qiniu.makeymonkey.com/1620612814382image.png?imageView2/2/w/800/auto-orient/format/jpg)

使用的变量‘XXX’未定义

解决方法：检查是否定义变量，如果是掌控板的变量，则检查代码是否完整或者重刷固件。

![](https://qiniu.makeymonkey.com/1620612941482image.png?imageView2/2/w/800/auto-orient/format/jpg)

## python3.6无法安装，可能是您已安装了python3.6或你的操作系统存在缺陷。请查看解决办法

解决方法： [https://www.labplus.cn/posts/609894744d982b612f5dfd7f](https://www.labplus.cn/posts/609894744d982b612f5dfd7f)

## OSError: SSID invalid / failed to scan this wifi

wifi名称或密码错误

解决方法：检查下WIFI名称密码是否正确，检查掌控板所连接的WIFI是否是2.4GHz，掌控板不支持连接5GHz的WIFI

## AttributeError: 'Pin' object has no attribute 'is\_pressed'

解决方法：固件版本过低，刷入最新固件

## TypeError: function takes 'X' positional arguments but 'XX' were given

函数所填写的参数数量与函数所需要的参数数量不一致

解决方法：很多图形化代码鼠标悬停会有函数以及参数的详解，可以通过这种方式查看参数数目，或者在[文档](https://mpython.readthedocs.io/zh/master/index.html)中搜索

## SyntaxError: invalid syntax

python语法错误

两种情况会出现这个问题：

烧录代码时有数据丢失导致代码缺失不完整

解决方法：重新刷入代码

---

代码语法错误

解决方法：具体看抛出错误的地方，例如：

if语句内判断两者相等大多数情况应该是用“==”而不是“=”

## RemoteException: could not enter raw repl

未能连接上AI摄像头

解决方法：检查掌控板电量是否足够、线路是否接错、代码中引脚是否写错，若都没问题，重刷AI摄像头固件

## IndexError: list index out of range

列表下标索引越界，选择列表某一项的时候不能大于列表长度

解决方法：查看自己的列表长度，选择列表下标索引时要小于列表长度

## ImportError: no module named 'smartcamera'

使用AI摄像头时没有导入smartcamera库

解决方法：硬件模式下，删除左边扩展内的AI摄像头，并在重新加载选择刷入驱动库

延伸错误：ImportError: no module named 'XXX'

表示没有XXX库

使用硬件编程遇到时：

解决方法：下载最新软件刷入最新固件

使用python编程遇到时：

解决方法：

通过左上的 python库管理 安装来安装“XXX”库

![](https://qiniu.makeymonkey.com/1622537548288image.png?imageView2/2/w/800/auto-orient/format/jpg)

---

若1无效，卸载并重装所使用图形化模块的扩展

![](https://qiniu.makeymonkey.com/1622537622021image.png?imageView2/2/w/800/auto-orient/format/jpg)

## OSError: Timeout!,check your wifi password and keep your network unblocked

连接超时

解决方法：检查wifi名称和密码有没有填错

## TypeError: can't convert float to int

不能将float类型替换成int类型

解决方法：根据报错提示转成相应的类型

## MemoryError: memory allocation failed

超出内存

解决方法：

1. 按下掌控板单板背部B键下方的白色按键重启来释放内存
2. 如1不能解决请删减程序代码

## 在使用图形化代码“播放音符列表”时会导致掌控板一直重启

![](https://qiniu.makeymonkey.com/1623314411688image.png?imageView2/2/w/800/auto-orient/format/jpg)

解决方法：初始化列表内只允许放音符，不允许放音调，改用音符即可解决

![](https://qiniu.makeymonkey.com/1623314450854image.png?imageView2/2/w/800/auto-orient/format/jpg)

## 程序缩进问题

解决方法：找到在报错里的main.py那里提示的行数，把对应的图形化代码删除重新添加

## TypeError: extra keyword arguments given

给出了额外的关键字参数

解决方法：

1. 如果是自定义函数，检查是否填写传入了对应数量的参数
2. 如果是非自定义函数，检查报错里main.py出错行对应的函数，在[mpython函数帮助文档](https://mpython.readthedocs.io/zh/master/index.html)内搜索对应函数，查看参数数量是否一致

## 使用小方舟时，缺少nplus的某个库

解决方法：重刷固件

刷完固件后，查看掌控板文件的nplus文件夹内应有下面的四个文件

![](https://qiniu.makeymonkey.com/1631242646550image.png?imageView2/2/w/800/auto-orient/format/jpg)

## Windows OS 安装驱动时，安装失败

![](https://qiniu.makeymonkey.com/1631515753162image.png?imageView2/2/w/800/auto-orient/format/jpg)

解决方法：下载通用兼容版驱动并根据电脑系统选择安装32位或64位

[点击下载通用驱动](http://steamaker.oss-cn-shenzhen.aliyuncs.com/%E8%AE%BA%E5%9D%9B%E5%86%85%E7%9B%B8%E5%85%B3%E4%B8%8B%E8%BD%BD/CP210x_Universal_Windows_Driver.zip)

## 使用录音识别，掌控板显示\ {'state': False, 'err': 'error code 11201, reason licc failed'}\

公共接口使用上限

解决方法：在讯飞开放平台注册个人账号后找到自己的apiKey，使用如下代码来使用个人接口API

![](https://qiniu.makeymonkey.com/1632714944398image.png?imageView2/2/w/800/auto-orient/format/jpg)

## OSError: Timeout,ntp server not response.

授时服务器超时

解决方法：在代码中切换授时服务器

![](https://qiniu.makeymonkey.com/1636947141971image.png?imageView2/2/w/800/auto-orient/format/jpg)
