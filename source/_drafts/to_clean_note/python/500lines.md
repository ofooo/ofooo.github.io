---
title: 5oo行项目学python
tags: [python]
---



## 目录

\1. A Template Engine （[http://aosabook.org/en/500L/a-template-engine.html](https://link.zhihu.com/?target=http%3A//aosabook.org/en/500L/a-template-engine.html)）
​    MVC模型中的view层如何解析html中的静态变量和简单的语句，如下：

web中的view层不只是html代码，还有支持其他的代码。比如 {products}是一个变量。 同时view层还支持{if} , {for}, {foreach}等等。django，velocity等是如何解析他们的？
大牛用不到500行代码告诉你，是如何实现的？ （不是替换，替换需要每次请求都需要解析）

\2. Web Spreadsheet （[http://aosabook.org/en/500L/web-spreadsheet.html](https://link.zhihu.com/?target=http%3A//aosabook.org/en/500L/web-spreadsheet.html)）
   web的电子表格如何实现的？ 好像比较简单，但是介绍了 web storage 和 web worker，还是很值得一看的

\3. A Web Crawler [http://aosabook.org/en/500L/a-web-crawler-with-asyncio-coroutines.html](https://link.zhihu.com/?target=http%3A//aosabook.org/en/500L/a-web-crawler-with-asyncio-coroutines.html)
   不多说，几百行代码实现高效的网络爬虫， 高效！

\4. Static Analysis [http://aosabook.org/en/500L/static-analysis.html](https://link.zhihu.com/?target=http%3A//aosabook.org/en/500L/static-analysis.html)
​     成熟的IDE都有代码检查和代码提示，怎么做的？ 看这章

\6. A Simple Object Modle [http://aosabook.org/en/500L/a-simple-object-model.html](https://link.zhihu.com/?target=http%3A//aosabook.org/en/500L/a-simple-object-model.html)
​    Python是面向对象语言，对象，继承，多态，怎么用代码实现的，不到500行代码，实际不到400 行， 666.。。

\7. An Archaeology-Inspired Database [http://aosabook.org/en/500L/an-archaeology-inspired-database.html](https://link.zhihu.com/?target=http%3A//aosabook.org/en/500L/an-archaeology-inspired-database.html)
​    如何用python实现一个数据库，支持 query，index, transaction， 2，3百行代码和对每个函数的讲解。看完你就知道知道数据库原理，太值了

\8. Dog Bed Database [http://aosabook.org/en/500L/dbdb-dog-bed-database.html](https://link.zhihu.com/?target=http%3A//aosabook.org/en/500L/dbdb-dog-bed-database.html)
   类似上一章，不过这次实现的是key-value的非关系型数据库，详细的讲解和2，3百行代码

\10. A Python Interpreter Written in Python [http://aosabook.org/en/500L/a-python-interpreter-written-in-python.html](https://link.zhihu.com/?target=http%3A//aosabook.org/en/500L/a-python-interpreter-written-in-python.html)
​      手把手教你如何实现python解析器。



\12. A Continuous Intergration System [http://aosabook.org/en/500L/a-continuous-integration-system.html](https://link.zhihu.com/?target=http%3A//aosabook.org/en/500L/a-continuous-integration-system.html)
​      CI System是一个专门用来测试新代码的系统，根据代码提交记录，拿到新的代码，测试，生成报告。这不是关键，关键是 如果test失败，它还会 恢复，然后从失败的那个点在跑，相当于把出错环境重现了。。。

13 A Rejection Sampler [http://aosabook.org/en/500L/a-rejection-sampler.html](https://link.zhihu.com/?target=http%3A//aosabook.org/en/500L/a-rejection-sampler.html)
​      不是很懂，和机器学习相关，如何 计算你赢得象棋比赛的概率，天气对飞机的影响等类似的问题

14 A visual programming toolkit [http://aosabook.org/en/500L/blockcode-a-visual-programming-toolkit.html](https://link.zhihu.com/?target=http%3A//aosabook.org/en/500L/blockcode-a-visual-programming-toolkit.html)
​      不太明白

