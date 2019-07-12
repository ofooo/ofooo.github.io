---
title: python源码转UML图
toc: true
categories:
  - 编程基础
  - python
date: 2019-05-25 19:08:46
tags:
---





### 用conda制作模块

## 安装

```bash
# 需要安装的软件：
## Graphviz：贝尔实验室开源的图形绘制工具包
## Pyreverse：用来分析Python代码和类关系的工具，包含在Pylint中
sudo apt install graphviz
pip install pylint
```

## 调用

```bash
pyreverse -o png -ASmy xxx.py
# xxx.py 要解析的源代码文件
# -o png 指定输出图片格式。  默认的dot格式。
# -o tail.png 也可以携带tail 输出文件名= classes.tail.png
# -A, --all-ancestors   展示项目中的所有祖先类
# -a Ｎ                 展示项目中的Ｎ代祖先类
# -S, --all-associated  以递归方式显示所有关联的关联类
# -m, --module-names=[yn] 在表示类中包含模块名称
#　      用法　　　-m y　　或者　　-my
# -k, --only-classnames 类框中不显示属性和方法;这会禁用-f值

```

