---
title: decorator装饰器
toc: true
tags:
  - python
  - decorator
  - 装饰器
categories:
  - python
  - 语法
date: 2019-03-17 08:38:37
---



## 最简单的模板是这样的

```python
def outer(func):
    def inner():
        print 'before'
        func()
        print 'after'
        # return r
    return inner

@outer
def F1():
    print 'test'
```

## 函数带多个参数，装饰器对应修改以适合多种情况

```python
def ftfunc(func):
    def timef(*s,**gs):
        print "[%s] %s() called" % (ctime(),func.__name__)
        return func(*s,**gs)
    return timef

@ftfunc
def foo(*s,**gs):
    print(s)
    print(gs)
```

## 函数带多个参数，装饰器也带多个参数

```python
def decrator(*dargs, **dkargs):
    def wrapper(func):
        def _wrapper(*args, **kargs):
            print "decrator param:", dargs, dkargs
            print "function param:", args, kargs
            return func(*args, **kargs)
        return _wrapper
    return wrapper

@decrator(1, a=2)
def foo(x, y=0):
    print "foo", x, y
```

## 函数带多个参数，装饰器能转换参数类型

```python
def validate(**vkargs):
    def decorator(func):
        def wrapper(**kargs):
            for key in vkargs:
                # 根据vkargs中的参数的类型对kargs的参数进行类型转换
                kargs[key] = vkargs[key](kargs[key])
            return func(**kargs)
        return wrapper
    return decorator


@validate(x=int, y=float, z=float)
def move(x, y, z):
    print "move %d (%0.2f, %0.2f)"%(x, y, z)
```

## 参考资料
> - []()
> - []()
