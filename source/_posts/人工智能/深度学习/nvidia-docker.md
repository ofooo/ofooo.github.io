---
title: nvidia_docker
toc: true
categories:
  - 人工智能
  - 深度学习
date: 2019-06-14 09:54:32
tags:
---





## nvidia-docker简介

Docker容器与平台无关, 但也与硬件无关.这有一个问题, 当使用专门的硬件,如NVIDIA显卡时, 需要内核模块和用户级别的库来操作. 因此docker本身并不支持容器内的NVIDIA显卡.

NVIDIA提供了 nvidia-docker:

1. 驱动无关的CUDA镜像
2. 一个docker命令行包装, 在启动时将驱动程序的用户模式组件和GPU设备装入容器



## 安装nvidia-docker

```bash





```

### 使用镜像

镜像仓库https://hub.docker.com/r/nvidia/cuda

```bash
CUDA镜像的三种风格:
base: 基础镜像
runtime: 扩展于base, 增加了CUDA toolkit 共享库
devel: 扩展于runtime, 增加了debugging工具/编译器工具链/头文件和静态库


# 选择版本后, 拉取nvidia/cuda镜像
nvidia-docker pull nvidia/cuda:10.0-cudnn7-devel-ubuntu18.04
# 查看拉取镜像的版本
nvidia-docker run --rm -ti 镜像名称 nvcc --version
```

### 安装pytorch

获取安装文件https://pytorch.org/get-started/locally/

```bash
根据上面的版本, 选择1.1, linux, python3.7
```









## 参考资料
> - []()
> - []()
