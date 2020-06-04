---
title: snakeviz_cprofile_性能分析
toc: true
tags:
  - python
  - snakeviz
  - cprofile
  - 性能分析
  - 运行速度分析
categories:
  - python
  - 工具
date: 2020-06-04 10:42:12
---



## cProfile

cProfile是标准库内建的分析工具的其中一个，另外两个是hotshot和profile

- cProfile：基于lsprof的用C语言实现的扩展应用，运行开销比较合理，适合分析运行时间较长的程序，推荐使用这个模块；
- profile：纯Python实现的性能分析模块，接口和cProfile一致。但在分析程序时增加了很大的运行开销。不过，如果你想扩展profiler的功能，可以通过继承这个模块实现；
-  hotshot：一个试验性的C模块，减少了性能分析时的运行开销，但是需要更长的数据后处理的次数。目前这个模块不再被维护，有可能在新版本中被弃用



### python代码中使用

```python
import cProfile

# 直接把分析结果打印到控制台
cProfile.run("test()")
# 把分析结果保存到文件中
cProfile.run("test()", filename="result.out")
# 增加排序方式
cProfile.run("test()", filename="result.out", sort="cumulative")

# 注意 test必须是从程序入口为起点的对象路径（如果想执行code/test.py fn()   则要run('code.test.fn()')
```

### shell中调用

```bash
# 直接把分析结果打印到控制台
python -m cProfile test.py
# 把分析结果保存到文件中
python -m cProfile -o result.out test.py
# 增加排序方式
python -m cProfile -o result.out -s cumulative test.py
```





## snakeviz

snakeviz是第三方工具，用于可视化cProfile输出的性能分析文件

```bash
# 安装
pip install snakeviz

# 可视化
snakeviz $profile文件路径
```







## 参考资料
> - []()
> - []()
