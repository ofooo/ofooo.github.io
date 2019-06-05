---
title: pytorch常用代码
toc: true
categories:
  - 人工智能
  - 深度学习
date: 2019-06-05 09:35:55
tags:
---





pytorch版本: 1.1.0



## 张量

```bash
# 通用注释: x表示其他张量     
# size0,size1表示张量维度, 数量不固定
# data 表示张量的数组值(python数组类型)

zeros = torch.zeros(
	size0, size1, dtype=x.dtype, device=x.device, requires_grad=True)

zeros = torch.zeros(data, dtype=torch.long) # 指定具体地数据类型

x = torch.rand(size0, size1)	# 默认 torch.float32
x = torch.rand(size0, size1, dtype=torch.float)
x = torch.rand(size=[size0, size1], dtype=torch.float)

x = torch.randint(low=1, high=100, size=[12, 2], dtype=torch.long)
x = torch.LongTensor(size0, size1)	# 在pycharm中有错误提示

```











## 参考资料
> - []()
> - []()
