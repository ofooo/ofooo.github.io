---
title: 安装python
toc: true
categories:
  - 编程基础
  - python
  - 虚拟环境
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




## 用conda制作模块

有时安装不上某个模块，可以尝试用conda安装。conda安装不上时，可以尝试去anaconda.org查询是否有这个模块是否在某个源

```bash
conda install -c 某个源 模块名
conda install -c conda-forge jsonnet
```





## conda创建虚拟环境

**conda创建虚拟环境，jupyter可以使用。 这个过程jupyter貌似不用重启，刷新页面即可。**

```bash
# 1、创建环境
conda create -n py36 python=3.6

# 2、进入环境
source activate py36

# 3、然后添加kernel
# 错误命令: 如果当前虚拟环境不是root用户的，而仅用有user权限。则sudo安装的kernel位置不会是当前虚拟环境的位置。
sudo python -m ipykernel install --name py36 
# 正确命令: 仅安装到当前用户，这个位置正确。如果提示没有权限，则给要写入的文件夹权限。
python -m ipykernel install --user --name py36 

# 如果提示没有ipykernel，使用:python -m pip install ipykernel

# 4、退出虚拟环境
source deactivate

#　5、删除虚拟环境
conda remove -n 环境名称 --all
```



### 删除kernel

先找到配置文件kernel.json

sudo find / -name "kernel.json"

判断倒数第一行是我的配置，所以删除/usr/local/share/jupyter/kernels/py36/的话即是删除了这个kernel。

/usr/local/share/jupyter/kernels/py36/kernel.json

/home/fish/.local/share/jupyter/kernels/py27



### 用virtualenv安装虚拟环境

```bash
# 安装virtualenv
pip install virtualenv

# 列出所有环境
lsvirtualenv

# 创建环境
virtualenv venvname
# 创建环境，以  /usr/bin/python3  为python程序
virtualenv -p /usr/bin/python3 venvname

# 激活环境
activate venvname
# 退出环境
deactivate
# 删除环境
rmvirtualenv venvname　
```