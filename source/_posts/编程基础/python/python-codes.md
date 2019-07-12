---
title: python常用代码
toc: true
categories:
  - 编程基础
  - python
date: 2019-04-10 22:46:50
tags:
---





### 计数器对象 class collections.Counter

```python
c = Counter()   # 创建
c.most_common(3)  # 返回频次前3的二维数组，降序排列。不加参数则返回全部。 [(word, count)]
```







### 向上取整

```python
(分子 + 分母 - 1) // 分母
```



### tqdm进度条

```python
from tqdm import tqdm
gen_tqdm = tqdm(gener, total=len(gener))
for i in gen_tqdm:
    # 实时修改进度条上的描述文本
    gen_tqdm.set_description(description, refresh=False)
```



## 参考资料

> - []()
> - []()

