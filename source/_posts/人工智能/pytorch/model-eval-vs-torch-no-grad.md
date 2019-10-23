---
title: model.eval() 和 with torch.no_grad() 对比
toc: true
categories:
  - 人工智能
  - pytorch
date: 2019-10-23 16:23:19
tags:
---





>  两者目标不一样



## model.eval()

eval()将通知所有层当前的使用模式(train/eval),  因为一些特殊的层会有两种工作方式. 

- batchnorm 在train时使用batch的数据归一化, 而在eval时使用统计数据进行归一化
- dropout 在train时正常, 在eval时不会生效





### torch.no_grad()

```pyton3
with torch.no_grad():
	y = model(x)
```

no_grad()会关闭自动梯度引擎, 这会降低内存或显存的使用数量, 并且加快计算速度













## 参考资料
> - [https://discuss.pytorch.org/t/model-eval-vs-with-torch-no-grad/19615](https://discuss.pytorch.org/t/model-eval-vs-with-torch-no-grad/19615)
> - []()
