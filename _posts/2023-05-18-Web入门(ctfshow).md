---
layout:     post
title:      Web入门（ctfshow）
subtitle:   起点
date:       2023-5-18
author:     Rainsblue.chan
header-img: ![3](../../../wallpaper/3.jpg)
catalog:   true
tags:
    - Web
typora-copy-images-to: ./
---
# 前言
基于ctfshow的web入门所做的整理，希望能够学到一些皮毛。
## web1

F12打开开发者工具查看，也可以使用 ctrl + u 查看网页源代码。

![image-20230518161306727](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230518161306727.png)

![image-20230518162256283](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230518162256283.png)

## web2

查看给出的提示

![image-20230518162321752](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230518162321752.png)

我们看看是什么情况，搜索著名博主ouluhumen的博客☞☞[ouluhumen老师](https://ouluhumen.github.io/2023/04/30/Ctfshow-Web%E5%85%A5%E9%97%A81-20%E9%A2%98/)

![image-20230518162404797](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230518162404797.png)

![image-20230518162640582](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230518162640582.png)

现在我们总结一下

查看源代码：ctrl + u = view-source：url

开发者工具：F12 = 右上角元素 = ctrl + shift + i

## web3

这里的抓包应该是指回显

![image-20230518162937492](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230518162937492.png)

## web4

![image-20230518163022729](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230518163022729.png)

这个robots.txt应该就是和爬虫有关，像是个规则，告诉你哪个可以爬，哪个不能爬。

![屏幕截图 2023-05-18 141630](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202023-05-18%20141630.png)

这里对应的，直接在url后面输入这个不允许输入的文件。

![屏幕截图 2023-05-18 141716](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202023-05-18%20141716.png)

## web5

![image-20230522132459095](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522132459095.png)

phps源码泄露是什么，先看主页，输入index.php

![image-20230522132742693](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522132742693.png)

再在后面加入一个s，结果如下，它可以下载，打开能看见flag，这里打开的方式推荐使用notepad。

![image-20230522132934381](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522132934381.png)

![image-20230522133452645](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522133452645.png)

为什么phps可以下载源码，这个是和http服务器的解析有关系。

*文件就是php的源代码文件,通常用于提供给用户(访问者)查看php代码,因为用户无法直接通过Web浏览器看到php文件的内容,所以需要用phps文件代替。*

看到有一个方法是dirsearch（很久以前大概自己弄过，专门用来扫漏洞的），也可以确定这个名字，也有以flag，login为开头的，这里记一下。

#### dirsearch.py

这个刚刚看见的，归结的感觉很多了👉[web信息泄露相关内容](https://www.cnblogs.com/wysngblogs/p/15940304.html)

如果你的windows上装了git或者cygwin，你就可以像我这样安装，当然直接下载一个py文件然后cmd里用也是一样的。

`git clone https://github.com/maurosoria/dirsearch`

![image-20230522135250649](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522135250649.png)

这一篇把下载可能会遇到的问题说了，这是链接👉👉[dirsearch安装问题](https://blog.csdn.net/wuxinweii/article/details/126914934)

`pip install -r requirements.txt -i http://pypi.douban.com/simple/ --trusted-host pypi.douban.com`（这一串是问题核心，下面是一个示例）

![image-20230522141555559](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522141555559.png)

看看使用dirsearch后会产生什么影响。

![image-20230522141904206](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522141904206.png)

整个跑也能找，但是太太太慢了，可以考虑对应的做字典，时间会省不少

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522133817668.png" alt="image-20230522133817668" style="zoom: 67%;" />

[Diresearch 默认字典位置与自定义字典使用方法](https://blog.csdn.net/qq_46145027/article/details/122174063)

[【渗透神器】信息收集-目录爆破Dirsearch篇](https://zhuanlan.zhihu.com/p/483702332)

![image-20230522143442495](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522143442495.png)

一下子就出来了，大概3秒。这里**-w**就是指定字典路径。

## web6

![image-20230522134306246](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522134306246.png)

url后输入www.zip，即可下载源码压缩包

![image-20230522145814644](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522145814644.png)

![image-20230522145859807](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522145859807.png)

解压包里两个文件，一个是php，一个就是flag文件

![image-20230522145930786](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522145930786.png)

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522150129830.png" alt="image-20230522150129830" style="zoom:67%;" />

![image-20230522150351756](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522150351756.png)

这当中两者flag不同的原因是解压的文件是之前www服务器中的，在这个靶场重新构建时会重新写入，所以输入url出现的flag是对的

## web7









