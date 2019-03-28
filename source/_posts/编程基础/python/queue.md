---
title: Queue 队列模块相关
toc: true
categories:
  - 编程基础
  - python
date: 2019-03-25 08:13:50
tags:
---



|       |      |
| ----- | ---- |
| heap  | 堆   |
| stack | 栈   |
| queue | 队列 |
|       |      |

堆的逻辑结构就是完全二叉树，并且二叉树中父节点的值小于等于该节点的所有子节点的值。

特征：heap[k] <= heap[2k+1] 并且 heap[k] <= heap[2k+2] （其中 k 为索引，从 0 开始计数）

## heapq  堆队列

### 基本操作

```python
import heapq 
heap = []
#向堆中插入元素，heapq会维护列表heap中的元素保持堆的性质 
heapq.heappush(heap, item) 

#heapq把列表x转换成堆 O(n)复杂度
heapq.heapify(x)       # 最小堆
heapq._heapify_max(x)  # 最大堆

#从可迭代的迭代器中返回最大的n个数，可以指定比较的key 
heapq.nlargest(n, iterable[, key]) 

#从可迭代的迭代器中返回最小的n个数，可以指定比较的key 
heapq.nsmallest(n, iterable[, key]) 

#从堆中删除元素，返回值是堆中最小或者最大的元素 
heapq.heappop(heap)



heapq.heappushpop(heap, item)：向 heap 中加入 item 元素，并返回 heap 中最小元素。
heapq.heapreplace(heap,item): python3中heappushpop的更高效版。
```

### 原理

使用的比较函数：lt, gt, cmp

内置数据类型和自定义类型，默认使用 **__lt__** （小于比较函数）进行比较

元组类型默认使用 cmp 比较 （先比较第1列，相同再比较第2列，以此类推……）

### 代码示范

```python
import heapq
h = []
# 默认是最小堆
heapq.heappush(h, (5, 'write code'))
heapq.heappush(h, (7, 'release product'))
heapq.heappush(h, (1, 'write spec'))
heapq.heappush(h, (3, 'create tests'))
min_item = heapq.heappop(h)  # (1, 'write spec')

```

## PriorityQueue 优先队列

> queue库是线程安全的

```python
#向队列中添加元素
Queue.put(item[, block[, timeout]])
#从队列中获取元素
Queue.get([block[, timeout]])
#队列判空
Queue.empty()
#队列大小
Queue.qsize()


try:
    import Queue as Q #python version < 3.0
except ImportError:
    import queue as Q #python3.*
q = Q.PriorityQueue()
q.put(19)
q.put(1)
q.put(5)
while not q.empty():
    print(q.get())
```







## 参考资料
> - []()
> - []()
