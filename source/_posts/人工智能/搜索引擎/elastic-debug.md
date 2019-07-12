---
title: elastic-debug
toc: true
date: 2019-06-27 11:20:54
tags:
categories:
---



### 搜索结果的 _score都是None

因为使用了自定义的排序, 例如使用时间戳排序, 这时elastic会省略_socre.

如果你希望排序并查看分数, 可以使用 track_scores 参数.

[参考](https://www.elastic.co/guide/en/elasticsearch/guide/current/_sorting.html )

[stackoverflow](https://stackoverflow.com/questions/41301691/getting-score-null-in-elastic-search)





### 无法写入数据: cluster_block_exception [FORBIDDEN/12/index read-only / allow delete (api)];

因为ES默认监控硬盘使用空间超过95%时会自动设置为自读状态.

解决方案:

1. 清理磁盘空间

2. 配置阈值

   ```bash
   PUT _cluster/settings
   {
     "transient": {
       "cluster.routing.allocation.disk.watermark.low": "100gb",
       "cluster.routing.allocation.disk.watermark.high": "50gb",
       "cluster.routing.allocation.disk.watermark.flood_stage": "10gb",
       "cluster.info.update.interval": "1m"
     }
   }
   ```

   





## 参考资料
> - []()
> - []()
