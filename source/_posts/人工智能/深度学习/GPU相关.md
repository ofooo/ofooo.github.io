---
title: GPU相关
tags: 
  - gpu
categories: 
  - 人工智能
  - 深度学习
---





查看当前GPU使用情况

nvidia-smi

设置使用哪个GPU

CUDA_VISIBLE_DEVICES="1"  

查看CUDA版本

nvcc --version





```bash
# 查看显卡版本
lspci | grep -i nvidia
```

