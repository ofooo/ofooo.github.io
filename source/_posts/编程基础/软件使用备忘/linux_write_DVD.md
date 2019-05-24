---
title: linux刻录光盘
toc: true
categories:
  - 编程基础
  - 软件使用备忘
date: 2019-04-02 15:26:08
tags:
---

## ubuntu--Brasero

1. 在Ubuntu软件商店安装brasero
2. 光驱插入光盘
3. 打开brasero
4. 选择：数据项目(A)：创建一个视频DVD或SVCD
5. 点击添加按钮，加入文件夹或文件
6. 给光盘命名（默认是日期文本）
7. 显示进度条，等待刻录完成

## 注意：带很多代码和数据文件的文件夹，要先压缩再刻盘。 不然有可能刻盘失败。  光盘也不能用了。。。。

## 大小：4000M比较靠谱（存储空间比真实文件更大）

sudo tar cjf - police_model |split -b 4000m - police.v9.







参考资料

> - []()
> - []()
