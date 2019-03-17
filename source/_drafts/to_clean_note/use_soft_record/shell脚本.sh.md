---
title: shell脚本
tags: []
---

##### 问题：source 无法找到

source是bash的内建命令。不是单独的执行文件。如果用其他shell则会缺少source。

- 使用 bash run.sh 即可。
- 或者在文件开头添加``` #!/bin/bash ```    赋予运行权限``` chmod a+x 文件名 ```，直接运行``` run.sh ```文件。


