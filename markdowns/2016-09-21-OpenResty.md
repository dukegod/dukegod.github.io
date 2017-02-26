---
title: openResty
date: 2016-09-21
tags: [Nginx, openResty]
---

全能的web服务器openResty，相关的安装以及配置。

<!-- more -->

```
# 第一步

brew install pcre openssl

# 第二步

// 1）下载openResty源码，直接到 http://openresty.org/ 下载打包好的。
// 2）直接去github下来，运行make，自动下载依赖包，


# 第三布
// ngx_openresty-1.9.7.1 进入你的项目中

安装需要指定安装目录 prefix

cd ngx_openresty-1.9.7.1

./configure

配置的时候可以指定相关的路径。--with-prefix

./configure \ \
--with-cc-opt="-I/usr/local/Cellar/openssl/1.0.2h_1/include/ -I/usr/local/Cellar/pcre/8.39/include/" \ \
--with-ld-opt="-L/usr/local/Cellar/openssl/1.0.2h_1/lib/ -L/usr/local/Cellar/pcre/8.39/lib/" \ \
-j8

# error 处理

ERROR: failed to run command: sh ./configure --prefix=/usr/local/openresty/nginx \...

// 运行

./configure --with-openssl=/usr/local/Cellar/openssl/1.0.2h_1

```



  >  最新Mac OSX 10.11.1 下安装 openresty 有一点小小的麻烦，记录一下：
    第一步根据官网安装需要的依赖：
    ```bash
    brew install pcre openssl
    ```
    其实最后我们会发现这样安装的openssl并没有什么用。
    configure 过程中会遇到 openssl找不到的错误，需要手动指定openssl 源码包。
    ```bash
    wget https://www.openssl.org/source/openssl-1.0.2e.tar.gz
    tar -xzvf openssl-1.0.2e.tar.gz
    ```
    链接的时候会发现找不到pcre的动态库，需要手动置顶prce的动态库。
    最终成功configure和make的命令如下：
    ```
    ./configure --prefix=/opt/openresty --with-openssl=../openssl-1.0.2e --with-cc-opt='-I/usr/local/Cellar/pcre/8.37/include/' --with-ld-opt='-L/usr/local/Cellar/pcre/8.37/lib' -j5
    make -j4
    sudo make install
    ```


### openReasty后 启动，关闭，重启操作

安装 openReasty后,不启动默认的nginx服务，启动openReasty自带的服务

安装的目录： /usr/local/openresty/nginx

```
// start

sudo ./sbin/nginx

// stop

sudo ./sbin/nginx -s stop

```

nginx相关的操作必须在管理员权限下进行。

```
// 相关的配置 conf
cd /usr/local/openresty/nginx/

usr/local/openresty/nginx/sbin/nginx

usr/local/openresty/nginx/sbin/nginx -s reload
ps -ef | grep nginx
kill -9

# 关闭
usr/local/openresty/nginx/sbin/nginx -s stop

```

里面有各种配置，日志

##### 设置环境变量

```
# OpenResty nginx
export PATH="/usr/local/openresty/nginx/sbin:$PATH"
alias ngxr="/usr/local/openresty/nginx/sbin/nginx -s reload"
alias ngxps="ps -ef | grep nginx"

#  启动
nginx -p ~/openresty-test

curl http://localhost:6699 -i
```

### LuaRocks

[LuaRocks](http://blog.csdn.net/wentianyao/article/details/50556520)

安装在/usr/local中，包在lib中

LuaRocks 是 Lua 模块的安装和部署工具，类似于 Ruby 的 gem，Python 的 egg 和 Perl 的 cpan，它可以很方便的安装第三方 Lua 模块，而且你不需要关心模块之间的依赖关系，一条命令就可以很轻松地把模块安装部署好


### 参考

[最佳实践](https://moonbingbing.gitbooks.io/openresty-best-practices/content/)
[极客学院](http://wiki.jikexueyuan.com/project/openresty/)
[常见的报错](http://homeway.me/2015/07/10/rebuild-osx-environment/)
[openResty](http://www.cnblogs.com/youn/p/5682376.html)
