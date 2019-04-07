---
title: argparse命令行参数模块
toc: true
tags:
  - python
  - argparse
  - 命令行参数
categories:
  - 编程基础
  - python
date: 2019-04-05 22:54:57
---



## 基础用法：必须参数

```bash
# 导入命令行解析的库文件
import argparse    

# pkg是一个必须的位置参数(因为前面没有横杠，所以是位置参数。因为没有默认值，所以是必须参数)
parse.add_argument('pkg',help='help')

# 命令行执行 --help时，会查看的说明
parse = argparse.ArgumentParser(description="test!!")  

```

## 可选参数

```bash
# nargs是默认值，有默认值的参数是可选参数
parse.add_argument('keyoukewu',help='xx'，nargs='?')  

# 前缀是‘-’的参数名是缩写，前缀是‘--’的参数名是全称
parse.add_argument('-a','--abc',help='xx',nargs='?')
print(args.abc)
print(args.a) # 是错误的：因为解析的时候必须用全称


```



## 参考资料
> - []()
> - []()
