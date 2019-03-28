---
title: 使用docker
toc: true
categories:
  - 编程基础
  - 软件使用备忘
date: 2019-03-19 14:49:42
tags:
---



## 配置

### 



### 服务设置

刚安装完成后，需要重启机器，才能启动服务

```
# Ubuntu
sudo service docker start  # 启动服务

# manjaro
sudo systemctl start docker   # 启动服务
sudo systemctl status docker  # 查看服务状态
systemctl enable docker       # 开机启动
```

### 设置信任本地仓库

```bash
# 1. 在/etc/default/docker添加：
-- insecure-registry 127.0.0.1:5000
# 2. 再重启docker 服务
```



## 容器-常用命令

```bash
# 查看容器列表 
## -a 查看全部，否则查看运行中的
docker ps

# 删除容器    -f强制删除
docker rm -f xxx


```

### 容器自启动设置

```bash
docker run --restart=on-failure:10 xxx
docker run --restart=always xxx
```

- no   容器退出时不要自动重启。这个是默认值。
- on-failure[:max-retries]     只在容器以非0状态码退出时重启。可选的，可以退出docker daemon尝试重启容器的次数。在每次重启容器之前，重启延迟比上次增加一倍，从100毫秒开始，来防止影响服务器。这意味着daemon将等待100ms,然后200ms，直到超过on-failure限制，或执行docker stop或docker rm -f 。如果容器重启成功[容器启动后并运行至少10秒]，然后delay重置为默认的100ms。
  ms, 400, 800, 1600等等，直到超过on-failure限制，或执行docker stop或docker rm -f
- always     不管退出状态码是什么始终重启容器。当指定always时，docker daemon将无限次数地重启容器。容器也会在daemon启动时尝试重启，不管容器当时的状态如何。(和unless-stopped 参数值效果一样)

  



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
