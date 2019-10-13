---
title: debug：pytorch_梯度出现NaN
toc: true
tags:
  - pytorch
  - NaN
categories:
  - 人工智能
  - pytorch
date: 2019-05-22 19:00:45
---

计算

梯度出现NaN



## 梯度出现异常值：NaN

### 定位方法：

使用如下代码设置，在出现NaN异常时程序会报错，便于定位错误代码

```python
import torch
# 正向传播时：开启自动求导的异常侦测
torch.autograd.set_detect_anomaly(True)

# 反向传播时：在求导时开启侦测
with torch.autograd.detect_anomaly():
	loss.backward()
```

### 原因：

很多网友提到，pytorch的求标准差的函数STD可能有问题。如果使用了类似会调用STD函数的各种Norm层就可能导致NAN问题。

### [官方文档参考](https://pytorch.org/docs/stable/autograd.html#torch.autograd.detect_anomaly)