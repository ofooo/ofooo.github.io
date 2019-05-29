---
title: 使用Adblock广告屏蔽插件
toc: true
categories:
  - 编程基础
  - 软件使用备忘
date: 2019-05-27 21:49:42
tags:
---



## 

## 插件图标：

![1558947803597](use-Adblock/1558947803597.png)

## 屏蔽规则



```bash
# 隐藏元素：host--网站域名  class_name--类名  id_name--id名
host##.class_name    
host###id_name  

# 属性选择符
##div[title*="adv"]  隐藏 title 属性包含 adv 字符的 div 元素
##table[width="80%"] 隐藏 width 属性值为 80% 的表格元素
##div[title^="adv"][title$="ert"] 隐藏 titile 属性以 adv 开始并且以 ert 结束的 div 元素
```

## 我的自定义配置文件：

```bash
sohu.com###right-side-bar
sohu.com###float-btn
sohu.com##.groom-read
```



## 参考资料
> - [https://adblockplus.org/filters](https://adblockplus.org/filters)
> - []()
