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

## web7、8

![image-20230522150631112](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522150631112.png)

![image-20230522151029959](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522151029959.png)

两题题目相同。我们从“版本控制和生产环境”入手，因为我什么都不懂，所以就直接搜着看看能有什么发现。显示结果最多的wp表示与git和svn有关系，因为最近搞的博客，所以对于git还是有印象，它是分布式系统，像更新博客，就是一份在自己的本地仓库进行修改，然后pull到github的远程仓库，这就是分布式方便的地方。这个操作其实就是“不部署到生产环境”，而是在本地上部署操作，然后直接同步到生产环境。

![image-20230522151801406](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522151801406.png)

![image-20230522152356484](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522152356484.png)

版本控制最主要的功能就是追踪文件的变更。它将什么时候、什么人更改了文件的什么内容等信息忠实地了记录下来。每一次文件的改变，文件的版本号都将增加。除了记录版本变更外，版本控制的另一个重要功能是并行开发。[版本控制的概念，点击去往百度喵！](https://baike.baidu.com/item/%E7%89%88%E6%9C%AC%E6%8E%A7%E5%88%B6/3311252?fr=aladdin)*主打一个同步，一直用在软件更新上*

git与svn的区别也可以自己去搜，我觉得最核心的区别就是分布与集中。在这里，.git是git仓库所使用的目录，包含所有跟踪信息。这里ouluhhumen老师有整理，我就直接贴在下面了。

.git目录中包含了以下主要内容：

> HEAD文件：指向当前所在的分支或提交。

> config文件：存储了Git仓库的配置信息，例如用户名、邮箱、远程仓库等。

> hooks目录：包含了Git钩子脚本，用于在特定的Git操作时触发自定义脚本。

> objects目录：存储了Git仓库中所有的对象，包括提交、分支、标签等。

> refs目录：包含了所有的引用，例如分支、标签等。

> index文件：存储了当前工作目录中所有文件的状态信息，包括文件名、文件状态、文件指针等。

> logs目录：存储了Git仓库中所有引用的更新日志，用于记录所有提交和分支的变更历史。

![image-20230522153806872](image-20230522153806872.png)

svn的也贴贴

.svn目录通常包含以下文件和目录：

> entries：此文件记录了当前目录和其子目录中每个文件和目录的元数据信息，包括文件名、类型、版本号等。

> format：此文件记录了.svn目录的格式版本号。

> wc.db：此文件是一个SQLite数据库，存储了SVN管理的项目的版本历史和其他元数据信息。

> pristine目录：此目录存储了SVN管理的项目的每个文件的原始版本，用于支持SVN的版本比较和合并操作。

> tmp目录：此目录存储了SVN的临时文件和缓存文件。

![image-20230522155626141](image-20230522155626141.png)

对应我直接写入字典，比较舒服。

![image-20230522155842945](image-20230522155842945.png)









