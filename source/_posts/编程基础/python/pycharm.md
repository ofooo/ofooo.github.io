---
title: 配置和使用 pycharm
toc: true
categories:
  - 编程基础
  - python
date: 2019-03-17 08:55:57
tags:
---



## 配置

### 常用代码片段配置

****

>  配置路径   Setting--->Editor--->Live Templates--->加号按钮

```python
# ~err
error = '\n'.join(traceback.format_exception(*sys.exc_info()))

# ~root
def root(*f, relative_root='../../../'):
    # relative_root 当前代码目录相对root的相对路径
    for t in f:
        if t[:1] == '/':
            print('Warning: root()包含绝对路径 参数={}'.format(f))
            break
    code_dir = os.path.dirname(os.path.realpath(__file__))
    long_path = os.path.join(code_dir, relative_root, *f)
    return long_path
```

### 快捷键配置

```bash
Keymap---方案设置成NetBeans

# Code格式化代码   设置成  Ctrl+Alt+L
Reformat
# 当前行往上挪一行  设置成 Alt+Up
Move Line Up
# 当前行往上挪一行  设置成 Alt+Down
Move Line Down

# 优化导入代码   默认快捷键 Ctrl+Shift+I
Optimize Imports

```

### 跳转到上个光标所在位置

​	打开 View---toolbar   有左右箭头按钮。悬停可以查看快捷键

![toolbar](/home/fish/.config/Typora/typora-user-images/1553590786370.png)

### 插件

File---Setting---Plugins

数据库插件：

​	搜索datebase

​		安装 Database Navigator

​		安装Mongo Plugin

​	



## 参考资料

> - []()
> - []()
