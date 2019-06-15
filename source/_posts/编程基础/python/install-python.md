---
title: 安装python
toc: true
categories:
  - 编程基础
  - python
date: 2019-04-17 08:55:46
tags:
---







## 在ubuntu中安装python3.6

```bash
sudo apt update \
    && apt install -y software-properties-common \
    && add-apt-repository -y ppa:jonathonf/python-3.6 \
    && apt update \
    && apt install -y python3.6 \  
    && update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.6 100 \ 
    && update-alternatives --install /usr/bin/python python /usr/bin/python3.6 100 \ 
    && apt install -y python3-pip \

```

update-alternatives是Ubuntu中管理软件版本的工具

如果不设置名称, 则默认的python3实际是3.5 这时候安装python3-pip时会针对python3.5安装

update-alternatives用法说明:

```bash
# 查看python3这个名称对应了什么软件
update-alternatives --display python3 


# 把软件路径设置到某个链接和某个名称
update-alternatives --install <链接> <名称> <路径> <优先级>
链接是类似/usr/bin/python3 这样的软链接路径
名称是类似python3 这样的软件名称
路径是指软件的实际位置
优先级数字越大越优先
```




### 用conda制作模块

有时安装不上某个模块，可以尝试用conda安装。conda安装不上时，可以尝试去anaconda.org查询是否有这个模块是否在某个源

```bash
conda install -c 某个源 模块名
conda install -c conda-forge jsonnet
```
