---
layout: Debugging CUDA device-side assert in PyTorch
title: PyTorch
date: 2019-10-05 12:14:22
tags:
---

## 原文: [Debugging CUDA device-side assert in PyTorch](https://lernapparat.de/debug-device-assert/)

PyTorch的立即执行模型的美丽之处在于您实际上可以调试程序。 但是，有时CUDA执行的异步特性使其变得很难。 这是调试程序的一个小技巧。

当您使用CUDA操作运行PyTorch程序时，该程序通常不等到计算完成，而是继续向GPU抛出指令，直到它实际需要结果为止（例如，使用.item（）或.cpu（）进行评估或打印）。

尽管这是PyTorch程序出色性能的关键，但有一个弊端：当cuda操作失败时，您的程序可能正在执行其他操作(因为异步)。 通常的症状是，在触发错误的指令之后的某个地方，或多或少地出现随机性错误。 通常看起来像这样：

```bash
---------------------------------------------------------------------------
RuntimeError                              Traceback (most recent call last)
<ipython-input-4-3d8a992c81ab> in <module>()
      1 loss = torch.nn.functional.cross_entropy(activations, labels)
      2 average = loss/4
----> 3 print(average.item())

RuntimeError: cuda runtime error (59) : device-side assert triggered at /home/tv/pytorch/pytorch/aten/src/THC/generic/THCStorage.cpp:36

```

好吧，这很难理解，我敢肯定，报错位置是合法的代码。 因此，设备端断言意味着系统只是发现某个地方出了点问题。

这是导致此输出的错误程序：

```bash

import torch
device = torch.device('cuda:0')
activations = torch.randn(4,3, device=device) # usually we get our activations in a more refined way...
labels = torch.arange(4, device=device)
loss = torch.nn.functional.cross_entropy(activations, labels)
average = loss/4
print(average.item())
```

调试中的一种选择是将事物移至CPU。 但通常，我们使用库或复杂的东西就没法这么做。 所以现在怎么办？ 如果我们能获得良好的追溯，我们就能找到并解决问题。

以下是获得良好回溯的方式：您可以在环境变量CUDA_LAUNCH_BLOCKING设置为1的情况下启动程序。这也可以在python代码中解决：在程序的顶部，在导入任何内容（尤其是PyTorch）之前，先插入

```python
import os
os.environ['CUDA_LAUNCH_BLOCKING'] = "1"
```

通过此添加，我们可以获得更好的错误回溯：

```bash
---------------------------------------------------------------------------
RuntimeError                              Traceback (most recent call last)
<ipython-input-4-3d8a992c81ab> in <module>()
----> 1 loss = torch.nn.functional.cross_entropy(activations, labels)
      2 average = loss/4
      3 print(average.item())

/usr/local/lib/python3.6/dist-packages/torch/nn/functional.py in cross_entropy(input, target, weight, size_average, ignore_index, reduce)
   1472         >>> loss.backward()
   1473     """
-> 1474     return nll_loss(log_softmax(input, 1), target, weight, size_average, ignore_index, reduce)
   1475 
   1476 

/usr/local/lib/python3.6/dist-packages/torch/nn/functional.py in nll_loss(input, target, weight, size_average, ignore_index, reduce)
   1362                          .format(input.size(0), target.size(0)))
   1363     if dim == 2:
-> 1364         return torch._C._nn.nll_loss(input, target, weight, size_average, ignore_index, reduce)
   1365     elif dim == 4:
   1366         return torch._C._nn.nll_loss2d(input, target, weight, size_average, ignore_index, reduce)

RuntimeError: cuda runtime error (59) : device-side assert triggered at /home/tv/pytorch/pytorch/aten/src/THCUNN/generic/ClassNLLCriterion.cu:116
```

显然，损失函数的输入不合法。 实际上，我们的激活形状批处理为x 3，因此我们只允许三个类别（0、1、2），但标签的值为3！

这对特殊情况也适用, 如果我们能恢复计算中的非GPU位而不需要完全重启就好了.(The best part is that this also works for nontrivial examples. Now if only we could recover the non-GPU bits of our calculation instead of needing a complete restart...  这句话翻译的不太好, 有建议可以联系我邮箱ofyu@163.com)





```bash


RuntimeError: copy_if failed to synchronize: device-side assert triggered

RuntimeError: CUDA error: device-side assert triggered

THCudaCheck FAIL file=/pytorch/aten/src/THC/THCCachingHostAllocator.cpp line=296 error=59 : device-side assert triggered
*** RuntimeError: cuda runtime error (59) : device-side assert triggered at /pytorch/aten/src/THC/THCCachingHostAllocator.cpp:296

# 本次出错, 是因为词向量的id超出了词向量维度, 还有可能id=-1,或者label超出维度等等
```

