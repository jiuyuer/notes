---
title: nrm 安装与配置
tags:
  - npm
  - nrm
categories:
  - 技术渣
date: 2021-07-12 16:16:46
---

## 介绍

**nrm**（npm registry manager）是 `npm` 的镜像源管理工具，有时候国外资源太慢，使用这个就可以快速地在 `npm` 源间切换

## 安装

在命令行执行命令，`npm install -g nrm`，全局安装 `nrm`

## 使用

执行命令 `nrm ls` 查看可选的源。

```bush
*npm ---- https://registry.npmjs.org/
cnpm --- http://r.cnpmjs.org/
taobao - http://registry.npm.taobao.org/
eu ----- http://registry.npmjs.eu/
au ----- http://registry.npmjs.org.au/
sl ----- http://npm.strongloop.com/
nj ----- https://registry.nodejitsu.com/
```

其中，带\*的是当前使用的源，上面的输出表明当前源是官方源。

## 切换镜像

如果要切换到 `taobao` 源，执行命令 `nrm use taobao`。

## 增加

你可以增加定制的源，特别适用于添加企业内部的私有源，执行命令 `nrm add <registry> <url>`，其中 `reigstry` 为源名，`url` 为源的路径。

```bush
nrm add registry http://registry.npm.frp.trmap.cn/
```

## 删除

执行命令 `nrm del <registry>` 删除对应的源。

## 测试速度

你还可以通过 `nrm test` 测试相应源的响应时间。

```bush
nrm test npm
```
