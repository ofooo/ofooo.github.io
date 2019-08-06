---
title: elastic-search插件
toc: true
categories:
  - 人工智能
  - 搜索引擎
date: 2019-08-01 16:37:07
tags:
---









## 命令 elasticsearch-plugin

```bash
elasticsearch-plugin list     #查看已经安装的插件
elasticsearch-plugin install     #安装插件
elasticsearch-plugin remove     #卸载插件


```

## IK分词器

### 配置 IK分词器的词典

配置文件路径

```bash
{$elasticsearch_dir}/config/analysis-ik/IKAnalyzer.cfg.xml
```

配置内容

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE properties SYSTEM "http://java.sun.com/dtd/properties.dtd">
<properties>
	<comment>IK Analyzer 扩展配置</comment>
	<!--用户词典,  注意是相对于ik插件所在目录的相对路径, 而且即便写绝对路径也会被拼接 -->
    <!--dict/date  绝对路径为  {$elasticsearch_dir}/config/analysis-ik/dict/date.dic   -->
	<entry key="ext_dict">dict/date.dic;dict/ext.dic</entry>
</properties>
```

词库文件

文本文件, 一行一个词汇



## 参考资料

> - []()
> - []()
