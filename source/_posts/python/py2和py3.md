---
title: py2_and_py3
toc: true
tags:
  - 兼容性
  - python版本
categories:
  - 编程基础
  - python
date: 2019-03-17 08:39:15
---



## 感受: 实际上还是不好用～～～能用3就用3～～～



## **_future__**

python3出来的时候，python的设计者们当然也考虑过代码之间的兼容问题。许多为为兼容性设计的功能可以通过__future__这个包来导入。例如：

```python
# 使用python3的print函数，禁用python2的print语句。
from __future__ import print_function

# 导入该特征，代码中的文本变量默认是Unicode（如果不导入python2的文本变量默认是str）
# python2   str.decode('utf8') -->  Unicode
from __future__ import unicode_literals

# 参见PEP 328 -- Imports: Multi-Line and Absolute/Relative
from __future__ import absolute_import

# 像python3一样，int除以int得float，而不像Python2那样是整除
from __future__ import division
```

### six

| 字符串类型 | 文本          | 字节            |
| ---------- | ------------- | --------------- |
| python2    | unicode       | str             |
| python3    | str           | bytes           |
| six        | six.text_type | six.binary_type |

```python  
# python2
if isinstance(xxx, unicode):
    pass
    
# 兼容python2和python3
import six
if isinstance(xxx, six.text_type):
   pass

## 使用input代替raw_input
from six.moves import input
```

#### 判断版本写不同的内容

if sys.version>'3':

	pass

## 参考资料
> - []()
> - []()
