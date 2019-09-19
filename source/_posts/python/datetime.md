---
title: datetime
toc: true
categories:
  - python
date: 2019-08-31 15:25:52
tags:
---

.

## time 模块

```python
 time.time()
---> time_stamp(秒级时间戳)

time.localtime(time_stamp=None)
time_stamp ---> time.struct_time

time.strftime('%Y-%m-%d %H:%M:%S', struct_time)
struct_time ---> str_time
```

### 文本转时间戳

```python
a1 = "2019-5-10 23:40:00"
# 先转换为时间数组
timeArray = time.strptime(a1, "%Y-%m-%d %H:%M:%S")
 
# 转换为时间戳
timeStamp = int(time.mktime(timeArray))
```





## datetime 模块







## 参考资料
> - []()
> - []()
