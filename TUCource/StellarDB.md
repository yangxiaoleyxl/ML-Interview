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
- 使用 TEoC 建图 `create graph (if not exists) <name> with schema [node schema] [rel_schema] graphproperties:[...]`
- 使用 JSON 建图 `create graph <name> with file schema <path> `
- 根据现有图的 schema 建图 `create graph <copy_graph> with schema from graph my_graph`
- 查看已创建的图 `show graph(s)`  


### 4.批量数据导入
- 支持的格式：Text, ORC, CSV 以及 Parquet. 批量数据导入 要在`analysis` 模式运行，可通过 `config crux.execution.mode analysis` 切换
- `bulk upsert/create/delete` 导入数据, 例句 `select * from source_db.e bulk upsert [:YY {__uid:uid, prop1:str, prop2:name}] ` 
- `load node into graph graph_name from source_db with file schema "hdfs://home/load.json" ` 根据位于hdfs://home/的json文件，将 source_db 库下的 v 表数据批量导入点 

### 5.图算法
- 通过创建视图来加速图算法的执行, 创建视图语句 `create query temporary view GRAPH_VIEM_NAME as (v) [e] with GRAPH_AIGO(@GRAPH_VIEW_NAME, VIEW_STORE_PATH, CONFIG_MAP, PROPS) ; ` 
- 算法
    - 基本度量
        - 直径
        - 半径
        - 度
        - K-core 
        - 三角计数 
        - 局部聚集系数
        - 平均聚集系数
    - 中心性算法
        - PageRank
        - Presonalized PageRank 
        - ArticleRank 
        - Weighted PageRank 
        - 特征向量中心性 
        - 介度中心性
        - 接近中心性
        - 调和中心性
    - 路径搜寻
    - 社区发现
    - 相似度
    - 链路预测