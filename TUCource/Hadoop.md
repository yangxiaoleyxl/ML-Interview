## Hadoop Summary
- [1.Stream管理](#1stream管理)
- [2.StreamJob管理](#2streamjob管理)
- [2.Application管理](#2application管理)

### 1. HDFS Management
- hdfs dfs -put: 上传至HDFS
- hdfs dfs -get: 下载至本地
- hdfs dfs -rm: 删除文件
- hdfs dfs -rmr: 递归删除文件 
- hadoop jar: 运行.jar程序 
- hdfs dfs -ls : 查看目录

### 2.HDFS Delete
- hdfs dfs -rm -r XX：删除文件
- hdfs dfs -rm -r -skipTrash XX: 跳过回收站 
- hdfs dfs -expunge: 清空回收站  

### 3. Practical Operation 
- hdfs dfs -ls -R : 递归的查看所有目录及其下面的文件
- hdfs dfs -chmod 777 PATH: 对 PATH 赋予所有权限
- 对于 csv 文件导入 Hive 的场景
    - 上传文件到 hdfs_path: hdfs dfs -put "XX.csv" hdfs_path 
    - 用 Python 生成 Hive 建表语句，shell脚本 + sql批量装载数据 