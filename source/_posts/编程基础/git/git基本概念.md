---
title: git基本概念
toc: true
tags:
  - git
  - gitlab
categories:
  - 编程基础
  - 软件使用备忘
date: 2019-05-17 19:05:30
---





## 概念

![img](git基本概念/v2-3bc9d5f2c49a713c776e69676d7d56c5_hd.jpg)

remote  远程仓库

repository   本地仓库

index/stage   暂存区

workspace     工作区



## 查看日志

```bash
# 如果恢复老版本, 想查看之前的新版本ID可以使用reflog
git reflog
```



## 恢复文件到暂存区的版本

```bash
git checkout -- $filename
# 如果未add到暂存区的内容会被丢弃
# 这个命令也可以恢复在工作区删除的文件(删除操作未add)
```




