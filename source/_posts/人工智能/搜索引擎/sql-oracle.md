---
title: oracle的SQL基础
toc: true
categories:
  - 人工智能
  - 搜索引擎
date: 2019-08-22 18:27:03
tags:
---

.

## 查看全局信息

### 查看所有表

```sql
 select table_name from user_tables;       -- 查看当前用户拥有的表
 select table_name from all_tables;           -- 查看所有用户的表
 select table_name from dba_tables;        -- 查看所有用户的表包括系统表
```

### 查看所有表字段

```sql
select * from user_tab_columns where TABLE_NAME='某表名称'；     
--查看当前用户下某表所有字段

select * from all_tab_columns where TABLE_NAME='某表名称'；     
select * from dba_tab_columns where TABLE_NAME='某表名称'；
```

> user_tab_columns：
> table_name,column_name,data_type,data_length,data_precision,data_scale,nullable,column_id等
> all_tab_columns ，dba_tab_columns比user_tab_columns多了一个ower

### 查看表注释和字段注释

```sql
select * from user_tab_comments       --查看当前用户下所有表注释
select * from user_col_comments where TABLE_NAME='某表名称'；    
 --查看当前用户下某表所有字段注释
```

> **user_tab_comments**：
> table_name,table_type,comments
> **user_col_comments**：
> table_name,column_name,comments



## 表内常用SQL

```sql
-- 单行注释
/*  多行注释  */

-- 普通语句
select * from db.tablename where field is not null

-- and/or  
SELECT * FROM Websites WHERE country='CN' AND (alexa > 50 or name is null) ;

-- oracle没有limit, 可以用rownum 
 where rownum<=5;
 
--/* 统计数据  */
select sum(1) from db.tablename

-- 聚合xxx字段的所有值
select xxx from db.tablename group by xxx, 'yy yy', zzz

-- 排序 desc=降序  asc=升序
order by xxx1 desc;
-- 
```



## 参考资料
> - []()
> - []()
