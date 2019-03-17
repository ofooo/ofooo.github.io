**每个logger输出时**

​	每个handler输出符合logger.level和handler.level的日志

​	还把日志传给logger.parent处理(logger.parent默认=root logger)



```python
# lib python3.6   logging __init__.py 调用parent循环体
def callHandlers(self, record):
    c = self
            found = 0
            while c:
                for hdlr in c.handlers:
                    found = found + 1
                    if record.levelno >= hdlr.level:
                        hdlr.handle(record)
                if not c.propagate:
                    c = None    #break out
                else:
                    c = c.parent
```




#### 典型的日志记录的步骤是这样的：

1.创建logger
2.创建handler
3.定义formatter
4.给handler添加formatter
5.给logger添加handler

**logger可看做是记录人，对于每个日志，他需要有一套规则，比如记录的格式（formatter），等级（level）等等，这个规则就是handler。使用logger.addHandler(handler)添加多个规则，就可以让一个logger记录多个日志。**


```python
# 模块级函数
import logging
logging.getLogger([name])  # 返回一个logger对象，如果没有指定名字将返回root logger
    logging.debug()、logging.info()、logging.warning()、logging.error()、logging.critical()  # 使用root logger写入对应级别的日志
logging.basicConfig()  # 用默认Formatter为日志系统建立一个StreamHandler，设置基础配置并加到root logger中
```


### Logger对象
```python
lg = logging.getLogger('asd')	# 获取一个logger对象
lg.setLevel('DEBUG')	# 把logger最低显示等级设置成 DEBUG
lg.info('asdsad')	# 使用info等级写入一条日志
```

#### Formatter格式配置

| %(name)s            | Logger的名字                                |
| ------------------- | ---------------------------------------- |
| %(levelno)s         | 数字形式的日志级别                                |
| %(levelname)s       | 文本形式的日志级别                                |
| %(pathname)s        | 调用日志输出函数的模块的完整路径名，可能没有                   |
| %(filename)s        | 调用日志输出函数的模块的文件名                          |
| %(module)s          | 调用日志输出函数的模块名                             |
| %(funcName)s        | 调用日志输出函数的函数名                             |
| %(lineno)d          | 调用日志输出函数的语句所在的代码行                        |
| %(created)f         | 当前时间，用UNIX标准的表示时间的浮 点数表示                 |
| %(relativeCreated)d | 输出日志信息时的，自Logger创建以 来的毫秒数                |
| %(asctime)s         | 字符串形式的当前时间。默认格式是 “2003-07-08 16:49:45,896”。逗号后面的是毫秒 |
| %(thread)d          | 线程ID。可能没有                                |
| %(threadName)s      | 线程名。可能没有                                 |
| %(process)d         | 进程ID。可能没有                                |
| %(message)s         | 用户输出的消息                                  |
|                     |                                          |



. logging是线程安全的，但不是多进程安全的。也就是说多进程间不会有IO阻塞

2. 多进程使用logging建议是每个进程单独一个log文件，不会阻塞，会写乱。。



如果你非要多进程还要写到一个文件，那么有两种解决方案

1. 所有进程log到SocketHandler，然后有个专门的进程监听Socket写入文件，相当于日志聚合

2. 使用multiprocessing的Lock类，把写日志变成阻塞的