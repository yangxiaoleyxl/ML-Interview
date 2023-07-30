### Data Mining  
以实际数据挖掘竞赛为例，总结一般的数据挖掘流程与路径
#### 1. EDA 
数据探索性分析是分析原始数据集的第一步，常用的代码段包括
```python  
import pandas as pd 
# 查看各维度的基本信心
df.info()   

# 查看各维度的基本情况，min, max, std, mean，percentile 等
df.describe()  

# 查看头尾的3行
df.head(3).append(df.tail(3)) 

# 查看缺失值 df.isnull().any().sum()
print(f'There are {data_train.isnull().any().sum()} columns in train dataset with missing values.') 

# 


```