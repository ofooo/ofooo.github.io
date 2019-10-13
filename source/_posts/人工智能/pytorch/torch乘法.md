---
title: torch中的几种乘法。torch.mm, torch.mul, torch.matmul
toc: true
date: 2019-10-06 20:29:59
tags:
categories: 
- torch.mm
- torch.mul
- torch.matmul
---

.

## 一、点乘

点乘都是broadcast的，可以用torch.mul(a, b)实现，也可以直接用*实现。

```python
>>> a = torch.ones(3,4)
>>> a
tensor([[1., 1., 1., 1.],
        [1., 1., 1., 1.],
        [1., 1., 1., 1.]])
>>> b = torch.Tensor([1,2,3]).reshape((3,1))
>>> b
tensor([[1.],
        [2.],
        [3.]])
>>> torch.mul(a, b)
tensor([[1., 1., 1., 1.],
        [2., 2., 2., 2.],
        [3., 3., 3., 3.]])
```

当a, b维度不一致时，会自动填充到相同维度相点乘。

## 二、矩阵乘

矩阵相乘有torch.mm和torch.matmul两个函数。其中前一个是针对二维矩阵，后一个是高维。当torch.mm用于大于二维时将报错。

```python
>>> a = torch.ones(3,4)
>>> b = torch.ones(4,2)
>>> torch.mm(a, b)
tensor([[4., 4.],
        [4., 4.],
        [4., 4.]])

>>> a = torch.ones(3,4)
>>> b = torch.ones(5,4,2)
>>> torch.matmul(a, b).shape
torch.Size([5, 3, 2])

>>> a = torch.ones(5,4,2)
>>> b = torch.ones(5,2,3)
>>> torch.matmul(a, b).shape
torch.Size([5, 4, 3])

>>> a = torch.ones(5,4,2)
>>> b = torch.ones(5,2,3)
>>> torch.matmul(b, a).shape
报错。
```







## 参考资料
> - [https://blog.csdn.net/weixin_42105432/article/details/100691592](https://blog.csdn.net/weixin_42105432/article/details/100691592)
> - []()
