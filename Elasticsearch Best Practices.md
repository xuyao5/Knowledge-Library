# Elasticsearch Best Practices

## 1. 基本约定

###### 本手册为平安信用卡架构组编制的Elasticsearch(下简称ES)最佳实践手册，由于ES不同版本之间有一定差异，故本手册以ES 7.6.x版本为例进行说明

## 2. 基本原则

### 2.1 Mapping规范

###### 原则上，禁止ES进行动态映射，因为动态映射会不准确

###### 有意思的类型

| **Datatype** | **Point** |
| ------------ | --------- |
| Text 和 Keyword | 是否分词 |
| Nested | join查询 |
| Range | 加快搜索 |
| Date | 日期格式 |

###### 更好的es mapping管理：Dynamic templates

### 2.2 ID

###### 在数据库应用中，有逻辑主键和业务主键的区别，但是在es中，强烈要求每个document的id为业务主键
###### es中的一些底层操作依赖id的version对比，如果使用无意义的id(如：seq)，则会损失很多高性能API

### 2.3 时区

###### 在es内部，date被转为UTC，并被存储为一个长整型数字，代表从1970年1月1号0点到现在的毫秒数。Elasticsearch默认为UTC时间，即零时区，查询时若不指定时区，则默认以0时区查询，和我们所在的东八区差8小时

### 2.4 Java Client

###### 只推荐Java High Level REST Client

### 2.5 Search Explain

###### "explain" : true

### 2.6 同步

###### 不推荐asynchronous用法，推荐使用同步+java CompletableFuture

### 2.7 带Proxy的ES架构

### 2.8 ES SQL/Template选择

### 2.9 聚合

### 2.10 写入开放查询关闭

### 2.11 锁

###### 原则上

## 3 数据导入场景

### 3.1 文件导入

### 3.2 消息导入

### 3.3 接口导入

### 3.4 混合导入

## 4 数据更新场景

## 5 数据查询场景

### 5.1 单条查询

### 5.2 批量查询

### 5.3 分页查询

### 5.4 去重查询

## 6 数据清理场景

## 7 结构变更场景

## 8 性能调优

## 9 常见坑

#### 地址表

| **COLUMN**       | **TYPE**              | **NULL** | **KEY** | **NOTE** |
| ---------------- | --------------------- | -------- | ------- | -------- |
| ID               | unsigned bigint(20,0) | NOT NULL | PK      | 物理主键 |



