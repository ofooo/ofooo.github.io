---
title: pytorch报错
tags: [深度学习, GPU, pytorch]
---



eq() received an invalid combination of arguments - got (type), but expected one of:(float other)

**net-Module内部的 self.type 不能被覆盖。    不能self.type=net() 这样～～～**



RuntimeError: multi-target not supported at /pytorch/torch/lib/THNN/generic/ClassNLLCriterion.c:22

**CrossEntropyLoss(y, truey)应该：    y二维(n, 分类数)  truey一维(n)** 



RuntimeError: invalid argument 1: input is not contiguous at /pytorch/torch/lib/TH/generic/THTensor.c:231

**对象不是连续的（在显存或内存里）     input.contiguous() 即可**



RuntimeError: save_for_backward can only save input or output tensors, but argument 0 doesn't satisfy this condition

**函数需要需要反向传播时，输入必须是Variable，不能是tensor**



ValueError: Expected more than 1 value per channel when training

在训练时，期望多余1个值（例如nn.BatchNorm1d必须输入batch>1的数据）

可以用model.eval()   来进入预测模式，避免此问题










