---
title: 《hanlp神经网络依存句法分析器》笔记
toc: true
date: 2019-10-08 19:42:54
tags:
categories:
---

.

## 原文链接

[基于神经网络的高性能依存句法分析器](http://www.hankcs.com/nlp/parsing/neural-network-based-dependency-parser.html)

[最大熵依存句法分析器的实现](http://www.hankcs.com/nlp/parsing/to-achieve-the-maximum-entropy-of-the-dependency-parser.html)

https://github.com/hankcs/HanLP/wiki/FAQ

## 摘录

主流的统计句法分析一般分为两大流派——生成式和判决式。

**《生成式》**就是生成一系列句法树，从里面挑选出概率最大的那一棵作为输出。其优点是效果好，但开销大。由于是全局最优，所以可以取得较高的准确率，还可以很方便地处理非投射的句法树。不过也由于搜索的全局性和特征函数的复杂度，模型常常会过拟合，在训练集和测试集上的准确率差别很大。

**《判决式》**一般是基于动作（或称转移）和一个分类器实现的，仿照人类从左到右的阅读顺序，判决式句法分析器不断地读入单词，根据该单词和已构建的句法子树等信息建立分类模型，分类模型输出当前状态下的最佳动作，然后判决式分析器根据最佳动作“拼装”句法树。



## 参考资料
> - []()
> - []()

