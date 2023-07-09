## Inceptor Summary
- [1.定义](#1定义)
- [2.系统架构](#2系统架构)
- [3.Inceptor SQL](#3inceptor-sql)
- [4.基本操作](#4基本操作)

### 1.定义
- Inceptor 是一款用于 **数据仓库** 和 **大数据分析** 的大数据平台软件 
- 基于Hadoop的数据仓库产品 
- 分布式通用 SQL 殷勤
- 基于 Hadoop 和 Spark 技术打造 

### 2.系统架构 
- 客户端：
    - CLI 
    - ODBC/JDBC 
    - Web UI ：HUE Apache Hadoop UI 系统，自研的 BI 分析工具
    - Waterdrop : 配套的数据开发工具 
- Inceptor:
    - Inceptor Server
        - Connector
        - SQL Compiler 
        - PL/SQL Compiler 
        - Transaction Manager 
        - Spark 
    - MetaStore 
        - TxSQL 
- Hadoop Cluster  

### 3.Inceptor SQL 
- 平台表设计
    - TEXT 
    - ORC
    - ORC Transaction 
    - Holodesk 
    - ES 
    - Hyperbase 
    - CSV 
- 数据类型
    - 不常见的类型
        - ARRAY 
        - MAP 
        - STRUCT 

### 4.基本操作
- 建库
    - CREATE DATABASE IF NOT EXISTS   [COMMENT]  [WITH DBPROPERTIES] 
    - DROP DATABASE [IF EXISTS] 
    - ALTER DATABASE   SET DBPROPERTIES  
- 建表 
    - CREATE [TEMPORARY] [EXTERNAL] TABLE [IF NOT EXISTS] [PARTITION BY] [CLUSTER BY ... INTO <> BUCKETS] [LOCATION]  
    - CREATE TABLE 创建内表 
    - CREATE EXTERNAL TABLE 创建外表 
    - <font color="red"> 创建外表时，一定要指定数据存储位置 </font> 
    - <font color="red"> 删除外表时，只删除元数据，表中数据保留 </font> 
    - <font color="red"> 删除内表时，同时删除数据和元数据 </font>  
    - 临时表 

        - 临时表仅当前 Sesion 可见，Session 结束后立即删除，且不支持 <font color="red"> 分区 </font> 
```sql 
CREATE TEMPORARY TABEL <>
```
        - CREATE TABLE <> LIKE <> 通过已存在的表或者视图来创建内表，只复制 Schema, 不复制数据
```sql 
CREATE TABLE <> LIKE <>
```
        - 使用查询结果创建内表，即复制 Schema, 又复制数据   
```sql 
CREATE TABLE <> AS SELECT <> 
```  
    - 删除表
        - 对于内表，删除数据和元数据；对于外表，只删除元数据 
    - 清空表
        - 删除数据，但不删元数据，该操作只用于内表


