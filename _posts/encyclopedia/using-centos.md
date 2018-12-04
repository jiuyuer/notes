---
title: 使用 CentOS7 心得
tags:
  - CentOS7
  - Linux
categories:
  - 百科全书
date: 2018-12-04 11:20:39
---

最近在阿里云上购置了一个云服务，系统是 CentOS7 的，对于不懂 Linux 的菜鸟来说，买了之后也是一脸蒙逼，简直无从下手。
幸好有强大的搜索引擎，折腾了两天，总算有些收获。

## 收获一：使用 MAC 终端登录

登录阿里云，拿到外网的 ip 地址，然后打开 MAC 终端，输入

```bash
ssh root@xx.xxx.xxx.xxx
```

没错，就这么简单，然后我们就可以在服务器上愉快的玩耍了。

## 收获二：文件上传下载

scp [了解一下](https://www.cnblogs.com/webnote/p/5877920.html)

### 上传文件到服务器

```bash
scp -r test.txt root@xx.xxx.xxx.xxx:~
```

### 从服务器下载文件

```bash
scp -r root@xx.xxx.xxx.xxx:~/test.txt ~/Desktop/
```

## 收获三：在 CentOS7 上安装 Node.js

这个也折腾了好久，网上的教程也挺多的，但是本人遇到的几个坑说明一下

- 源码安装，推荐但是并不是最有效率的，因为下载过来的源码需要经过解压，编译（很花费时间，而且需要安装 gcc 来作为编译软件），安装
- 使用已编译版本安装，这是我目前使用的方法，好处不用说了，坏处是版本固定，安装完之后，需要将 node 和 npm 配置成全局环境

## 收获四：在 CentOS7 上安装 mongodb

### 1、下载安装包

```bash
# 版本自己选择
curl -O https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-3.2.12.tgz
```

### 2、解压

```bash
tar -zxvf mongodb-linux-x86_64-3.2.12.tgz
```

### 3、移动到指定位置

```bash
mv  mongodb-linux-x86_64-3.2.12/ /usr/local/mongodb
```

### 4、在/usr/local/mongodb 下创建文件夹

```bash
mkdir -p /data/db
mkdir  /logs
```

### 5、启动

在/usr/local/mongodb/bin 下

```bash
 ./mongod
```

PS:

```bash
  # 使用命令启动mongodb数据库
cd /usr/local/mongodb/bin
./mongod -dbpath=/usr/local/mongodb/data -logpath=/usr/local/mongodb/logs/mongodb.log -logappend -port=27017 -fork
  #  常用的启动参数：
  #  --dbpath：指定存储数据的文件夹
  #  --logpath：指定日志存储文件
  #  --logappend：日志以增加方式产生
  #  --port指定端口，如果不写的话，默认是27017
```

### 6、关闭

```bash
/mongod --shutdown
```

## 收获五：在 CentOS7 上安装 redis

其实跟安装 mongodb 大同小异，搜一下网上一大堆

## 收获六：后台启动 node 服务，关闭 ssh 时，不会断开

> 有两种方法
>
> - 利用 forever 在 Linux 上实现 Node.js 项目自启动
> - nohup

对于 Linux 高手来说不算什么，所以，这只是 Linux 菜鸟的日常记录（无辜笑脸）
<br>
