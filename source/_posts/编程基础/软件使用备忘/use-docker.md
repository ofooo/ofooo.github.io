---
title: 使用docker
toc: true
categories:
  - 编程基础
  - 软件使用备忘
date: 2019-03-19 14:49:42
tags:
---







## 容器-常用命令

```bash
# 查看容器列表 
## -a 查看全部，否则查看运行中的
docker ps

# 删除容器    -f强制删除
docker rm -f xxx


```

## 镜像-常用命令

```bash
# 查看镜像列表
docker images

# 导出镜像的压缩文件（可以压缩多个镜像，例如xxx和yyy）
docker save xxx:tag yyy:tag2 | gzip > img.tar.gz  

# 镜像重命名
docker tag xxx:tag  xxx2:tag2

# 删除镜像  
## -f强制删除
docker rmi -f xxx:tag

```



## 参考资料
> - []()
> - []()
