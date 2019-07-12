---
title: python常用代码
toc: true
categories:
  - python
date: 2019-04-10 22:46:50
tags:
---





## 计数器对象 class collections.Counter

```python
c = Counter()   # 创建
c.most_common(3)  # 返回频次前3的二维数组，降序排列。不加参数则返回全部。 [(word, count)]
```







## 向上取整

```python
(分子 + 分母 - 1) // 分母
```



## tqdm进度条

```python
from tqdm import tqdm
gen_tqdm = tqdm(gener, total=len(gener))
for i in gen_tqdm:
    # 实时修改进度条上的描述文本
    gen_tqdm.set_description(description, refresh=False)
```



## 交换变量

### 快捷写法：最多支持4个变量互换

```python
a, b, c = 1,2,3
a,b,c = c,a,b
# 结果： a=3   b=1   c=2
```

### 如果交换内容涉及：对象及其属性，需要考虑先后顺序

```python
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None
        
# 正确的交换     
node = ListNode(1) ; node.next = 2
node.next, node = node.val, node.next
# 结果： node=2

        
# 错误的交换     
node = ListNode(1) ; node.next = 2
node, node.next = node.next, node.val
# 结果报错信息：
# AttributeError: 'int' object has no attribute 'next'
# node = node.next (2)
# node.next = node.val  int没有next属性

```

### 原因

- 交换的不是变量，而是变量的地址。地址变化是有顺序的，并不是同时完成的。
- 如果没有涉及到对象及其属性，地址变化不会影响取值过程，所以不会报错。所以看起来像是一句代码同时完成了一样。
- python解释得出的执行码中有4个指令：ROT_TWO /ROT_THREE/ROT_FOUR  所以交换赋值语句最多支持4个变量







## 参考资料

> - []()
> - []()

