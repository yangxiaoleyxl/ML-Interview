## StellarDB Summary
- [1.定义](#1定义) 
- [2.系统架构](#2系统架构) 
- [3.Inceptor SQL](#3inceptor-sql) 
- [4.基本操作](#4基本操作) 

### 1.定义
- 一种企业级分布式图数据库  

### 2.图数据简介
- 图数据
    - 类型（Label）： 用于区分不同的实体
    - 点（Node）：拥有全局唯一的ID, 唯一的类型, 多个标签, 以及一组属性K-V键值
    - 边（Relationship）：每个边都是有向边，拥有全局唯一ID. 每个边有唯一的类型（Label）, 多个标签（Tags）以及一组 K-V 属性值 
- 存储模式
    - 唯一ID的系统字段为 __uid, 类型为 String, 插入数据时需要显示指定
    - 点实体的 entityKey 由点的 __uid 和 label 自动计算而来，类型为 binary
    - 边实体的 entityKey 由边的 __uid 和 Label 以及起点和终点的 entityKey 计算而来
- 数据模式
    - 点模式
    - 相关模式
    - 边模式 
    - 类型模式
    - 指定属性  
    - 变长匹配模式

### 3.创建图 
常见的建图方法：
- 使用 TEoC 建图 `create graph (if not exists) <name> with schema [node schema] [rel_schema] garphproperties:[...]`
- 使用 JSON 建图 
- 根据现有图的 schema 建图 
- 查看已创建的图 