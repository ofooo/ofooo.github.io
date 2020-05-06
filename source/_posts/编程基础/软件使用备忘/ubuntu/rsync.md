---
title: rsync
toc: true
tags: 'shell, rsync, bash'
categories:
  - 编程基础
  - 软件使用备忘
  - ubuntu
date: 2020-05-06 15:35:46
---





复制文件夹的常用参数  -avz




rsync 原地址结尾处是否加 / 会影响结果：

```bash
rsync -r test/ test2
# test文件夹 复制成了 test2文件夹

$ rsync -r test test2
# test文件夹  复制到了 test2/test 里面
```




cp不受原地址结尾的影响，但受目标路径的影响

```bash
cp -r test/   test2 
cp test test2 -r
# 如果test2存在，则复制到test2/test
# 否则复制到 test2
```









## 参考资料
> - []()
> - []()
