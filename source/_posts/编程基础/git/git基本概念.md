---
title: git基本概念
toc: true
tags:
  - git
  - gitlab
categories:
  - 编程基础
  - git
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





## Error修复

### Tool open

@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0664 for 'xxx_rsa' are too open.
It is required that your private key files are NOT accessible by others.

文件权限太开放, 被其他人可以读写.

解决方案:  chmod 600 fileName       修改成```--rw------------```