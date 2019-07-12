---
title: tornado
toc: true
categories:
  - 编程基础
  - python
date: 2019-06-12 09:46:09
tags:
---

















### 监控文件改动, 自动重载服务

```python
# 设置 debug=True  或 autoreload=True 会监控所有.py文件, 在改动后自动重载tornado服务
app = tornado.web.Application(handlers, debug=True)

# 添加监控文件列表
tornado.autoreload.watch(filename: str) 


```







## 参考资料
> - []()
> - []()
