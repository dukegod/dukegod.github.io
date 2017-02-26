---
title: node中使用mysql数据库
date: 2016-12-02
tags: [Node,Mysql]
---

很早以前就应该做这个总结了，一直没有时间，一直拖到现在才开始真正的着手处理这件事情。  
mysql的一些操作就不做出说明了，看看相关的书籍就可以了。  

本文主要说明下，安装，链接，简单运用。

<!-- more -->

### 安装

使用brew就可以了，自行谷歌具体的安装问题。

安装node，更不用说明了。自行谷歌吧。

### 连接数据库

中间件使用 [mysql](https://github.com/mysqljs/mysql)

### 客户端

推荐 sequel Pro

### 常见的错误信息总结

+ [重新开机启动不了mysql数据库](http://stackoverflow.com/questions/5527676/warning-the-user-local-mysql-data-directory-is-not-owned-by-the-mysql-user/35259654#35259654)

+ [可能已经打开，需要关闭一些进程](http://stackoverflow.com/questions/15450091/for-a-newbie-error-2002-hy000-cant-connect-to-local-mysql-server-through-so)

+ [修改密码过期：如下](http://www.lai18.com/content/8651784.html)

```
最近安装mySQL5.7.9，发现安装完后会自动生成一个随机密码，然后用sql工具登录，发现这个密码已经过期了，不能登录。

终于解决好了，这里分享下处理步骤：

1.先关闭mysql服务；

2.进入终端，输入指令：cd /usr/local/mysql/bin/，进入安装目录；

3.输入指令：sudo su，切换到root用户；

4.输入指令：./mysqld_safe --skip-grant-tables &，禁止mysql验证功能。此时mysql服务会自动重启了；
5. 用工具（比如Sequal Pro）登录mySQL。配置的时候，只配用户名为root，密码不配。
6. 登录进去以后，数据库选择mysql，修改user表下用户名为root的那条记录，将password_expired设为N。这样随机密码就有效了，可以用密码登录了。

如果希望修改root密码，则在登录mysql后，执行下面两条sql即可：

update mysql.user set authentication_string=password('123456') where user='root' and Host = 'localhost';

flush privileges;
```
