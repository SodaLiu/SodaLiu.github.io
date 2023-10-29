---
layout:     post
title:      Web（Buuctf）
subtitle:   重启
date:       2000-01-02
author:     Rainsblue.chan
header-img: ![3](../../../wallpaper/3.jpg)
catalog:   true
tags:
    - 经验
---

# Web（Buuctf）

## [极客大挑战 2019]EasySQL

![image-20231029144650080](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/202310291446850.png)

界面如上，一个是用户名，还有一个是密码，正常使用sql注入的方式试一试

万能密码的原理就是

在登陆时，网站需要查询数据库。查询数据库就是执行SQL语句。
用户登录时，后台执行的数据库查询操作（SQL语句）是：
`Select user_id,user_type,email From users Where user_id=’用户名’ And password=’密码’`
由于网站后台在进行数据库查询的时候没有对单引号进行过滤，当输入用户名【admin】和万能密码【2’or’1】时，执行的SQL语句为：
`Select user_id,user_type,email From users Where user_id=’admin’ And password=’2’or’1’`
由于SQL语句中逻辑运算符具有优先级，【=】优先于【and】，【and】优先于【or】，且适用传递性。因此，此SQL语句在后台解析时，分成两句：
`Select user_id,user_type,email From users Where user_id=’admin’ And password=’2’`和`’1’`，两句bool值进行逻辑or运算，恒为TRUE。
SQL语句的查询结果为TRUE，就意味着认证成功，也可以登录到系统中。
输入用户名【admin】，密码【2’or’1】，即可登录成功
![image-20231029145344160](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/202310291453128.png)

## [极客大挑战 2019]Havefun

![image-20231029150245644](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/202310291502269.png)

![image-20231029150157604](https://cdn.jsdelivr.net/gh/rainsbluechan/blogimage@main/img/202310291501309.png)

## [网鼎杯 2020 青龙组]AreUSerialz

