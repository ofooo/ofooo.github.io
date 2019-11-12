---
title: node和npm使用说明
toc: true
tags:
  - node
  - npm
categories:
  - 编程基础
  - javascript
date: 2019-07-12 08:55:09
---

.


## npm 安装和卸载模块

```bash
# 安装模块, 并将模块名加入到package.json
npm install xxxxxx --save

# 全局安装
npm install xxxxxxxx -g

# 全局卸载
npm uninstall xxxxxxxx -g
```





## npm常用命令

```bash
# 查看已安装模块的版本(-g查看全局,否则查看本地)
npm ls jquery -g

npm view jquery version  #查看jquery的最新的版本
npm view jquery versions  #查看npm服务器上所有的jquery版本信息
npm info jquery          #查看npm服务器上所有的jquery版本信息
```

## 切换国内的源

```bash
# 阿里在国内搭建了镜像服务器:http://npm.taobao.org 
# 需要执行以下命令更改:
sudo npm config set registry https://registry.npm.taobao.org --global
sudo npm config set disturl https://npm.taobao.org/dist --global
# 更改完成 使用 命令   查看本地镜像源
npm config get registry
```





