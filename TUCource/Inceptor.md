## KS指标深入理解
- [1.特征预处理与转换](#1特征预处理与转换)
- [2.特征预提取与衍生](#2特征预提取与衍生)
- [3.特征选择与降维](#3特征选择与降维)
- [4.特征衍生](#4特征衍生)

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

为什么选择KS指标呢？——**KS指标倾向于从概率角度衡量正负样本分布之间的差异**。正是因为正负样本之间的模糊性和连续性，所以KS也是一条连续曲线。但最终为什么取一个最大值，主要原因是提取KS曲线中的一个显著特征，从而便于相互比较  

### 3.从几何角度解释KS与ROC的关系 
更加直观展示KS和ROC曲线的关系，我们将添加以下辅助线:
- 辅助曲线：TPR（图8左上）、FPR（图8右下）。
- 辅助直线：取得max_ks时的cum_bad_rate，取得max_ks时的cum_good_rate，蓝线为max_ks。灰线BR为ROC曲线在R点的切线，且与对角线OD平行

### 4.特征衍生
- 特征层级和主键：确定特征对象主键KeyID，例如确定需要衍生的特征是客户级、账户级、卡片级还是交易级 
- 多张表与多级表：多张表是指同一实体层属性特征存储在多个表里，多级表是指实体主表附属多个子表。对于多级表，在特征衍生时需要逐级向上级聚合 

例如，电商购物数据表包括客户层、订单层、订单详情层共三级表，一个客户有多张订单，一个订单有多个商品。在进行特征衍生时，订单详情层就需要聚合到订单层，订单层再进一步聚合到客户层，形成多层级的特征。多张订单形成流水时间序列，对于时间序列特征提取已经有很多成熟的方法 