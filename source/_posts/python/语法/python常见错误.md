---
title: python常见错误
toc: true
categories:
  - python
  - 语法
date: 2019-04-15 08:46:54
tags:
---



.



### "(或) or "的剪枝流程导致bug

```python
# 如果fun()==True 则foo()不会被执行
result = fun() or foo()
```





### 用系统内置函数作为变量名

比如下面的一些语句，会使你失去系统内置的功能：

```python
# 把内置类型或函数作为变量复制，导致原有功能失效
set = {1, 2, 3}
print = 'Hello'
```

### 将.py文件命名为内置模块的名称

常常被覆盖的模块名有：abc、match、turtle等。比如，为了计算一个公式的值，把源代码文件命名为math.py，内容如下：

```python
import math
print(math.sqrt(2)*2)
# 报错
Traceback (most recent call last):
File "/Users/chenbin/Documents/homework/math.py", line 1, in <module>
import math
File "/Users/chenbin/Documents/homework/math.py", line 2, in <module>
print(math.sqrt(2)*2)
AttributeError: module 'math' has no attribute 'sqrt'
```

### 以为input函数是万能的

初学者经常会以为input函数可以随心所欲得到想要的那种类型数值，特别是整数，比如：

```python
n = input("请输入年龄：")
print("明年你就", n + 1, "岁了！")
```

结果出错，因为python3中的input函数返回的是字符串，必须要套一层int()才能得到整数。

### 可变类型的连续赋初值

初学者觉得a=b=c=1这样赋初值特别cool，然后：

```python
# 初始化了3个空列表，但这其实是幻觉
# 因为它们仨指向了同一个可变类型的列表容器对象
a=b=c=[] 
# 给a添加了一个元素
a.append(123)  
# 其实a,b,c指向的是同一个列表，结果a,b,c都是[123]
```

记住，只有不可变类型的对象可以这么赋初值，或者你确实需要几个指向同一个可变对象的变量（这几乎不会出现）。

## 参考资料
> - []()
> - []()
