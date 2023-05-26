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
## 前言
基于ctfshow的web入门所做的整理，希望能够学到一些皮毛。
## web1（信息泄露篇）

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

![image-20230522153806872](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522153806872.png)

svn的也贴贴

.svn目录通常包含以下文件和目录：

> entries：此文件记录了当前目录和其子目录中每个文件和目录的元数据信息，包括文件名、类型、版本号等。

> format：此文件记录了.svn目录的格式版本号。

> wc.db：此文件是一个SQLite数据库，存储了SVN管理的项目的版本历史和其他元数据信息。

> pristine目录：此目录存储了SVN管理的项目的每个文件的原始版本，用于支持SVN的版本比较和合并操作。

> tmp目录：此目录存储了SVN的临时文件和缓存文件。

![image-20230522155626141](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522155626141.png)

对应我直接写入字典，比较舒服。

![image-20230522155842945](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522155842945.png)

## web9

![image-20230522224126893](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522224126893.png)

![image-20230522224415836](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522224415836.png)

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522224525501.png" alt="image-20230522224525501" style="zoom:50%;" />

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522224608292.png" alt="image-20230522224608292" style="zoom:50%;" />

来分析一下原因，这里我直接跟着b站教程走的，利用wsl的ubuntu

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522225052912.png" alt="image-20230522225052912" style="zoom:67%;" />

现在我要把当中aaa改成一个aba，未保存直接关闭。

​                                        <img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522225153134.png" alt="image-20230522225153134" style="zoom:80%;" /> 

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522225352334.png" alt="image-20230522225352334" style="zoom: 33%;" />

重新打开，1.php还在，使用ls -al查看所有文件

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522225947658.png" alt="image-20230522225947658" style="zoom:50%;" />

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522230121322.png" alt="image-20230522230121322" style="zoom:50%;" />

.1.php.swp为交换文件，是在vim非正常退出的情况下产生的，它会存储在atp服务器里面，作为一个非解析内容作为二进制下载，这种情况下我们可能能拿到它的源码。

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522230852158.png" alt="image-20230522230852158" style="zoom: 33%;" />

## web10

![image-20230522231352584](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522231352584.png)

在application里面的cookie，解个码

![image-20230522231448939](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522231448939.png)

![image-20230522231641090](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522231641090.png)

## web11（域名失效）

## web12

![image-20230522231959279](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522231959279.png)

![image-20230522232524689](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522232524689.png)

用我的字典扫出来一个robots.txt，disallow一个admin，我们输入进去看看

![image-20230522232741704](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522232741704.png)

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522232852118.png" alt="image-20230522232852118" style="zoom:50%;" />

密码在网站最下面，用户名为root

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522233005889.png" alt="image-20230522233005889" style="zoom:50%;" />

![image-20230522233053731](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522233053731.png)

## web13

![image-20230522233332617](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522233332617.png)

文档 = document

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522233704700.png" alt="image-20230522233704700" style="zoom:50%;" />

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522233756257.png" alt="image-20230522233756257" style="zoom:50%;" />

![image-20230522233813414](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522233813414.png)

## web14

![image-20230522233900989](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522233900989.png)

嗅觉敏锐，ctrl+u ctrl+f editor

![image-20230522234202458](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230522234202458.png)

编辑器漏洞利用，文件上传，这是一个漏洞攻击的考量方式。

web浏览器目录一般都在/var/www底下的html

![image-20230523222526445](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230523222526445.png)

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230523222621874.png" alt="image-20230523222621874" style="zoom: 33%;" />

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230523223029368.png" alt="image-20230523223029368" style="zoom:33%;" />

![image-20230523223102006](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230523223102006.png)

那个nothing here有点“此地无银三百两”的滋味了。

![image-20230523223342357](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230523223342357.png)

![image-20230523223423555](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230523223423555.png)

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230523223713020.png" alt="image-20230523223713020" style="zoom:50%;" />

估计是了，放在url下看看。

![image-20230523223826852](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230523223826852.png)

错误原因是使用了绝对路径。由最开始找到editor那里的路径，从根目录往后试试相对路径，也就是nothinghere那里。结果正确。

![image-20230523223949445](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230523223949445.png)

## web15

![image-20230523224145585](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230523224145585.png)

网页底部找到一个邮箱，我是要找这个qq号吗？

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230523224554802.png" alt="image-20230523224554802" style="zoom:50%;" />

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230523225058255.png" alt="image-20230523225058255" style="zoom: 33%;" />

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/3bc0cd43199cd43307ca84dcb8dfdb6.jpg" alt="3bc0cd43199cd43307ca84dcb8dfdb6" style="zoom:50%;" />

![image-20230523225747714](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230523225747714.png)

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230523225832834.png" alt="image-20230523225832834" style="zoom:50%;" />

犯傻了，上面用户名是admin，因为是后台登录（汗）😂😂😂

![image-20230523230154560](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230523230154560.png)

## web16

![image-20230523230427144](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230523230427144.png)

先看看概念喵~~~~

![image-20230523230536808](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230523230536808.png)

*探针的主要用途是帮助开发人员了解服务器的配置和运行环境，以便他们能够更好地调试和优化应用程序。探针可以提供有关 PHP 版本、扩展模块、配置选项、请求信息、环境变量等信息。 ---from ouluhumen*

使用tz.php打开看看。

![image-20230523230932992](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230523230932992.png)

*phpinfo 函数会生成一个包含了 PHP 配置信息的 HTML 页面，其中包含了 PHP 版本、编译选项、加载的扩展模块、环境变量、请求信息等等。通过查看 phpinfo 页面，你可以了解 PHP 的配置和运行环境的详细信息，帮助你诊断和解决 PHP 应用程序的问题 --from ouluhumen*

点击phpinfo跳入，或者url后输入act=phpinfo

![image-20230523232148678](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230523232148678.png)

![image-20230523231340399](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230523231340399.png)

## web17

![image-20230523232336819](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230523232336819.png)

backup.sql是存备份文件的地方，url后输入即可下载

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230523233325611.png" alt="image-20230523233325611" style="zoom:50%;" />

看看我的workbench里，找到了。

![image-20230523233451882](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230523233451882.png)

## web18

![image-20230523233753920](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230523233753920.png)

超你马的比😊😊😊😊😊

ctrl+u看一下源代码，看一下js

![image-20230523234150215](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230523234150215.png)

![image-20230523234303470](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230523234303470.png)

下面那条放我全新的hackbar里，应该是unicode编码，所以可以使用alert方式，这里另种

![image-20230523235352088](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230523235352088.png)

![image-20230523234801119](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230523234801119.png)

![image-20230523235050351](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230523235050351.png)

使用unicode解码得出一个网址，110.php

![image-20230523235130814](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230523235130814.png)

![image-20230523234122327](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230523234122327.png)

## web19

![image-20230523235833211](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230523235833211.png)

这个下面是注释，是用户和密码。

![image-20230523235928306](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230523235928306.png)

![image-20230524000047880](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230524000047880.png)

大意了

![image-20230524000242136](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230524000242136.png)

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230524000444610.png" alt="image-20230524000444610" style="zoom:50%;" />

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230524000535099.png" alt="image-20230524000535099" style="zoom:50%;" />

好叭！得结合一下题目，这里用到的是AES。iv为初始向量，选择CBC模式

![image-20230524001301828](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230524001301828.png)

![image-20230524001139955](image-20230524001139955.png)

![image-20230524001423893](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230524001423893.png)

## web20

![image-20230524002010393](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230524002010393.png)

被脱裤了（？）通过/db/db.mdb下载文件，使用notepad得到答案

![image-20230524003220067](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230524003220067.png)

![image-20230524003330039](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230524003330039.png)

至此信息泄露到此

## web21（爆破篇）

![image-20230524003504591](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230524003504591.png)

哈哈！开始爆破咯！听着好帅！😊😊😊😊😊这一板块使用到很多burpsuite，建议搭配firefox，可以自定义端口。

![image-20230524003705312](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230524003705312.png)

抓个包看看

![image-20230524004237403](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230524004237403.png)

[这一篇文章可以看看，点击食用，讲的是OAuth框架](https://zhuanlan.zhihu.com/p/409073486)

看最下面的Authorization，这个字段放的是**鉴权信息**，主要包括两部分：

1.鉴权类型

最主要的鉴权方式是Basic和Bearer，表示使用的基本身份认证或持有人身份认证

Basic base64编码（username：password）

**eg.Authorization: Basic YWRtaW46ZnVjaw==**

![image-20230524123818983](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230524123818983.png)

![image-20230524145803977](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230524145803977.png)

![image-20230524150424116](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230524150424116.png)

哈哈，just kidding，但是他确实是这样的。而对于Bearer鉴权，凭证则是犹如OAuth服务器颁发的一个token，就是访问令牌，格式为**Bearer access_token**，这里token就是持有人身份认证。可以复制proxy到Intruder，也可以用ctrl+i

![image-20230524151518574](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230524151518574.png)

![image-20230524151322461](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230524151322461.png)

在最后的==后点击Add$按钮，我们选择字典爆破，点击payloads

![image-20230524152653607](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230524152653607.png)

![image-20230524151810786](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230524151810786.png)

我们要爆破的是密码，选择的是前缀为**admin：**，然后已知的是它是Authorization里的一部分，所以是经过Base64加密的，这里选择的时候可以写一下。

![image-20230524151949874](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230524151949874.png)

![image-20230524152028188](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230524152028188.png)

这里符号不需要加密，否则爆不出来力（悲）

![image-20230524152208121](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230524152208121.png)

![image-20230524153447831](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230524153447831.png)

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230524154547080.png" alt="image-20230524154547080" style="zoom:50%;" />

爆破！😊😊😊😊😊

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230524153613169.png" alt="image-20230524153613169" style="zoom:50%;" />

![image-20230524153649601](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230524153649601.png)

这个我楞了一下，ok就好了，这个免费版还是能用的，我打算搞一手破解版，有哥们跟我说那个速度快。很快啊，哥们搞到手了。

![image-20230525094250195](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230525094250195.png)

[指路👉👉👉BurpSuite专业版下载](https://blog.csdn.net/qq_37776764/article/details/130037000)

艰难的😢😢😢😢😢

![image-20230525104825744](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230525104825744.png)

![image-20230525105106986](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230525105106986.png)

![image-20230525105235006](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230525105235006.png)

也可以，上面多打了一个v

![image-20230525105907501](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230525105907501.png)

## web22

![image-20230525110006287](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230525110006287.png)

这个域名失效了，但是能在靶场网页上看见

## web23

![image-20230525110322218](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230525110322218.png)

> 在 Web 开发中，`?token=` 是一种常见的 URL 参数格式，用于向服务器传递数据。当浏览器请求一个 URL 时，可以在 URL 后面添加一个问号 `?`，然后在问号后面添加参数，参数的格式为 `key=value`，多个参数之间使用 `&` 连接。
>
> 比如，一个包含token参数的url可能长这样
>
> eg.https://example.com/path/to/resource?token=abc123

是一段php代码，所以这里的方式就是要传token的参。

![image-20230525110414296](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230525110414296.png)

![image-20230525110501476](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230525110501476.png)

这段代码是一段 PHP 代码，用于检查传递给它的 URL 参数 "token"。如果满足特定条件，则会输出一个叫做 $flag 的变量的值。

代码中包含了一个叫做 "flag.php" 的文件，可能是存储了一些敏感信息的文件。

在检查 "token" 参数时，它会将其进行 MD5 哈希处理，并检查哈希值的特定位置上的字符是否相等。如果相等，它会计算出这些特定位置上字符的总和并将其除以哈希值第一个字符的值。如果结果等于哈希值第 31 个字符的值，则代码会输出 $flag 的值。

如果 "token" 参数不存在，代码将会输出自身的源代码。同时，它禁用了错误报告功能，这意味着任何错误都不会被显示出来，这使得攻击者更难以找到漏洞。

**所以要做的就是制作出一个token令牌，使得它的哈希满足上述规则**

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230525112830183.png" alt="image-20230525112830183" style="zoom:33%;" />

*只是一种方式，本人没有用这种方式实现，用比较蠢的又比较爽的*

![image-20230525122030020](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230525122030020.png)

直接扫也行，出来一个422和1202，两个都是对的，哈哈😊😊😊![image-20230525122401560](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230525122401560.png)

![image-20230525122527098](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230525122527098.png)

#### 另外的思路（sublime+php）

![image-20230525172859821](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230525172859821.png)

*如果您在`echo`语句中使用`\n`时没有将其放在双引号中，PHP将不会将其解释为换行符，而是将其视为普通的文本。因此，如果您尝试使用`echo $i \n;`而不是`echo "$i \n";`，PHP会在尝试解析`\n`之前将其视为`$i`的一部分，这将导致语法错误。因此，为了在`echo`语句中使用特殊字符，您需要将它们放在双引号中。*

## web24

![image-20230525214449582](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230525214449582.png)

拿到题目我们能看见两段。我们分为A、B段来分别分析。

A段为php代码。

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230525214712315.png" alt="image-20230525214712315" style="zoom:50%;" />

这是一段 PHP 代码，它包含一个名为 "flag.php" 的文件，并检查 GET 请求中是否存在名为 "r" 的参数。如果存在，它将变量 "$r" 的值设置为 "r" 参数的值，使用 "mt_srand()" 函数生成一个随机数，并使用 "intval()" 检查 "$r" 的值是否等于生成的随机数。如果两个值相等，则输出flag。

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230525223839665.png" alt="image-20230525223839665" style="zoom: 33%;" />

如果 GET 请求中不存在 "r" 参数，则使用 "highlight_file()" 函数突出显示当前文件的源代码，并使用 "system('cat /proc/version')" 命令打印出 Linux 内核版本的输出。

"cat /proc/version" 命令显示服务器上正在运行的 Linux 内核版本的信息。这些信息对攻击者来说可能很有用，可以用于寻找系统的漏洞。

值得注意的是，"error_reporting(0)" 函数用于关闭错误报告，这可能会使在出现问题时调试代码变得更加困难。

B段就是else分支下打印出的Linux内核版本的输出。

![image-20230525221233659](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230525221233659.png)

我的第一个想法当然还是最简单的爆破，毕竟不用动脑子，还有就是利用php写个脚本跑跑，我先试试第一种。

![image-20230525225055507](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230525225055507.png)

![image-20230525225122808](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230525225122808.png)

![image-20230525225159694](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230525225159694.png)

完蛋，跑了一万个没结果，还是想想实际的...

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230525225849301.png" alt="image-20230525225849301" style="zoom: 33%;" />

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230525230656870.png" alt="image-20230525230656870" style="zoom:50%;" />

`mt_srand()` 函数返回的是布尔值，而不是生成的随机数。因此，在代码中，变量 `$i` 将被赋值为 `true` 或 `false`，而不是生成的随机数。可以这么说，mt_srand是随机数序列，种子相同，随机数序列生成也就相同。

但是将这个数值放入后也没有成功，发现是php版本的问题，我使用的应该是7.3.4？这里用小皮面板调一下版本号，非常的方便，非常的新鲜。慢慢调，慢慢试。

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230525233240135.png" alt="image-20230525233240135" style="zoom:50%;" />

php7.09nts是这个，5.3.29也不对，我待会得想想如何得到网站的php版本。

![image-20230525233350582](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230525233350582.png)

啊？怎么回事呢？我一开始找到的就是这个？怎么没进去？我本来一开始就赢了呜呜呜😢😢😢😢😢

![image-20230525233849680](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230525233849680.png)

我现在气死了！！！啊！！！！！！我要！！报仇！查他的版本号！操他妈的！

点击F12，查看网络模块，刷新一下网页或者**ctrl+R**跳出来下面的包，查看响应头，X-Powered-By或者Server就是版本，显示为7.3.x（都是7.3的版本），以后记住喵！

![image-20230525234214533](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230525234214533.png)

## web25

![image-20230526084512674](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526084512674.png)

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526084804942.png" alt="image-20230526084804942" style="zoom:50%;" />

还是分析它看看。

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526085335019.png" alt="image-20230526085335019" style="zoom:50%;" />

这里我想随便先传一个r的参数，看会不会回显一个rand，结果是可以的。

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526085451048.png" alt="image-20230526085451048" style="zoom:50%;" />

一个负值，我直接加1试试。即**1999098941**。

![image-20230526085829107](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526085829107.png)

似乎又大了？接着调整几次范围。

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526090355865.png" alt="image-20230526090355865" style="zoom:50%;" />

![image-20230526090503948](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526090503948.png)

941没有回显，非常奇怪！别的都有！下面这个能验证我的想法。

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526090541245.png" alt="image-20230526090541245" style="zoom:50%;" />

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526090639930.png" alt="image-20230526090639930" style="zoom:50%;" />

下一步就是token，那么就是url处要多一个传参**&?token=**，这里我先爆一下，但是无果，找教程说还是要爆种子，有工具的。叫做**php_mt_seed**。由于中间中断了一次，所以又是一个重新的随机，这里只是一个演示。

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526095553541.png" alt="image-20230526095553541" style="zoom:50%;" />

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526154400862.png" alt="image-20230526154400862" style="zoom:50%;" />

[PHP伪随机数漏洞，以及php_mt_seed脚本的使用](https://blog.csdn.net/qq_58784379/article/details/121715072)

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526205109586.png" alt="image-20230526205109586" style="zoom:50%;" />

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526205915250.png" alt="image-20230526205915250" style="zoom:50%;" />

注意php版本，**7.3**

![image-20230526210502114](image-20230526210502114.png)

![image-20230526210607617](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526210607617.png)

缩小范围，只有11和14满足了。试了一下11，直接成功。

![image-20230526210715971](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526210715971.png)

## web26

![image-20230526163228033](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526163228033.png)

![image-20230526163616499](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526163616499.png)

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526163721777.png" alt="image-20230526163721777" style="zoom:50%;" />

![image-20230526163828715](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526163828715.png)

![image-20230526164417956](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526164417956.png)

因为直接什么都不输也能连到数据库，所以抓包看回显也行

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526164810546.png" alt="image-20230526164810546" style="zoom:50%;" />

## web27

![image-20230526164911054](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526164911054.png)

？？？？？

![image-20230526165210740](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526165210740.png)

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526165324789.png" alt="image-20230526165324789" style="zoom: 50%;" />

这当中有一些问题打断了我，详见我的博客[经验第六篇](https://rainsbluechan.github.io/2023/05/18/%E7%BB%8F%E9%AA%8C%E9%9B%86/)

![image-20230526212916120](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526212916120.png)

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526213305368.png" alt="image-20230526213305368" style="zoom:50%;" />

有些晕。试了好几次，回显都因为这个弹出页面改成了get，花了一些时间找，终于发现一个

#### 小技巧（查看http history）

![image-20230526225044278](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526225044278.png)

![image-20230526225341699](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526225341699.png)

找的是年月日，那么做一个对应的字典应该很方便。

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526230023388.png" alt="image-20230526230023388" style="zoom: 33%;" />

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526230258609.png" alt="image-20230526230258609" style="zoom: 50%;" />

![image-20230526230720514](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526230720514.png)

艰难

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526231030153.png" alt="image-20230526231030153" style="zoom:50%;" />

## web28

![image-20230526231150576](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526231150576.png)

![image-20230526231517795](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526231517795.png)

作为爆破篇的最后一题，这看着确实很怪，尤其是这个url...

我老实说我真没看懂，我得去找找wp了。

![image-20230526231928845](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526231928845.png)

提示是index.php，剩下是在两个数字里爆破。

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526234335765.png" alt="image-20230526234335765" style="zoom:50%;" />

这里加一个index.php，作为主页输出

![image-20230527001444247](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230527001444247.png)

要对两个变量进行爆破，也就是100x100的数量。选择Clusterbomb。

![image-20230527000707440](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230527000707440.png)

这样就会出现两个包

![image-20230527000821166](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230527000821166.png)

![image-20230527002335333](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230527002335333.png)

## web29

## web30

## 番外篇

#### 爆破（polarctf）

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526185658706.png" alt="image-20230526185658706" style="zoom: 50%;" />

![image-20230526185804379](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526185804379.png)

天，那不是和那个差不多？传个pass的参数。

![image-20230526194126517](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526194126517.png)

![image-20230526191742800](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230526191742800.png)

#### 传说之下（雾）

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230527002503276.png" alt="image-20230527002503276" style="zoom:50%;" />

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230527002801059.png" alt="image-20230527002801059" style="zoom:50%;" />

哈哈，还真放的传说之下的音乐！

不管怎么说我还是得看看源码有什么东西。写了个注释

![image-20230527002913774](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230527002913774.png)

它的计分是通过javascript实现的，一般来说会放在game.js中，一看真有。

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230527003728003.png" alt="image-20230527003728003" style="zoom:50%;" />

![image-20230527003331560](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230527003331560.png)

有没有办法让他的计分跳到2077呢？就把变量增大就行。

看了一个方法是在比赛途中改变量的，这里试一下。真对的。点击👉👉[zsy](http://zhangshiyu.com/post/49546.html)

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230527004640736.png" alt="image-20230527004640736" style="zoom: 33%;" />

控制台成功打出flag。

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230527004717676.png" alt="image-20230527004717676" style="zoom:50%;" />

[CTFshow-菜狗杯-传说之下（雾）-easyPytHon_P](https://blog.csdn.net/qq_31415417/article/details/129069722)

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230527005436805.png" alt="image-20230527005436805" style="zoom:50%;" />

<img src="image-20230527005102834.png" alt="image-20230527005102834" style="zoom: 33%;" />

<img src="https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/image-20230527005151599.png" alt="image-20230527005151599" style="zoom:33%;" />



















































