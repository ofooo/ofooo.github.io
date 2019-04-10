---
title: python常用代码
toc: true
categories:
  - 编程基础
  - python
date: 2019-04-10 22:46:50
tags:
---







### tqdm进度条

```python
from tqdm import Tqdm
gen_tqdm = Tqdm(gener, total=len(gener))
for i in gen_tqdm:
    # 实时修改进度条上的描述文本
    gen_tqdm.set_description(description, refresh=False)
```



## 参考资料

> - []()
> - []()
