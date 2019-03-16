---
title: os、sys
toc: true
date: 2019-02-26 15:00:45
tags:
  - python
  - python基础库
categories:
  - 编程基础
  - python

---



python基础库的用法

库：os、sys



### 常用功能

| 功能             | 代码                        | 参数                                       |
| -------------- | ------------------------- | ---------------------------------------- |
| 判断文件是否存在       | os.path.isfile(path)      |                                          |
| 判断文件或文件夹是否存在   | os.path.exists(path)      |                                          |
| 判断文件权限         | os.access(path, **mode**) | os.F_OK存在  os.R_OK可读 os.W_OK:可写os.X_OK可执行 |
| 判断文件夹存在        | os.path.isdir(dir)        |                                          |
| 得到当前工作目录       | os.getcwd()               |                                          |
| 删除文件           | os.remove()               |                                          |
| 列出目录里的文件夹和文件   | os.listdir(dir)           |                                          |
| 改变工作目录到dirname | os.chdir(dirname)         |                                          |
|                |                           |                                          |

https://www.cnblogs.com/wq242424/p/5803721.html