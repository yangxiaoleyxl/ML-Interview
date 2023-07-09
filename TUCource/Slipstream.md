## Slipstream Summary
- [1.Stream管理](#1stream管理)
- [2.StreamJob管理](#2streamjob管理)
- [2.Application管理](#2application管理)

### 1.Stream管理
- Create Stream : 创建 Input Stream
- Create Stream AS Select : 创建 Derived Stream  
- Show Streams : 列出所有的 Stream 
- Describe Stream : 查看 Stream 信息 
- Alter Stream : 修改 Input Stream 
- Drop Stream : 删除 Input Stream  

### 2.StreamJob管理 
StreamJob是触发 StreamSQL 执行的Action, 主要存储 StreamJob Level 的配置参数，以及对应的 SQL 
- StreamJob 管理操作
    - Create StreamJob
    - Show StreamJob 
    - Describe StreamJob 
    - Alter StreamJob 
    - Drop StreamJob  

### 3.Application管理 
Application 用于运行时的隔离和权限验证 
- 当业务需要上线时，可以用一个 Prod ID，对应一个Application, 将自己的SQL脚本放在 Application 下运行即可
- 管理操作
    - Create Application 
    - Alter Application 
    - Drop Application 
    - Describe Application 
    - Show Application    

### 4.StreamSQL Window
流应用通常对一个窗口内的数据做多表关联，聚合或者统计 
StreamSQL中的窗口以时间作为划分单位 
- 不指定窗口 : 默认以系统时间为基准
- 指定窗口  
    - 不指定时间字段 ：以系统时间作为切分基准
    - 指定时间字段 ：以时间字段作为切分基准  
- 窗口类型 
    - 滑动窗口 
    - 跳动窗口  
- 窗口切分方式
    - 系统时间切分 
    - 事件时间切分：基于指定时间字段 
    - 事件时间切分：支持 String 类型
    - 自定义时间格式



