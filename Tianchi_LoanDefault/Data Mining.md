### Data Mining  
以实际数据挖掘竞赛为例，总结一般的数据挖掘流程与路径
#### 1. EDA 
数据探索性分析是分析原始数据集的第一步，常用的代码段包括：
- 第一阶段
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

# nan可视化, 查看 缺失特征 和 缺失率
missing = df.isnull().sum()/len(df)
missing = missing[missing > 0]
missing.sort_values(inplace=True)
missing.plot.bar()

# 查看缺失率大于 X % 的维度
def nan_ratio_gt(x):
    have_null_fea_dict = (df.isnull().sum()/len(df)).to_dict()
    fea_null_moreThanHalf = {}
    for key,value in have_null_fea_dict.items():
        if value > x:
            fea_null_moreThanHalf[key] = value  
    return fea_null_moreThanHalf 
    
# 查看只有单数值的属性, nunique() 函数
one_value_fea = [col for col in df.columns if df[col].nunique() <= 1]  

``` 

- 第二阶段
    - 特征一般都由 **类别型特征** 和 **数值型特征**组成，其中数值型特征又分为 **连续数值型** 和 **离散数值型** 特征  
    - 类别型特征同时分为 有序 和 无序，例如：等级"A","B","C"可能有序，也可能无序，但学位"学士"，"硕士"，"博士"本身就包含顺序关系，如果认为地位相同，可能会丢失信息 
    - 数值型特征本是可以直接入模的，但往往风控人员要对其做分箱，转化为WOE编码进而做标准评分卡等操作
```python  
# 提取 数值型 和 类别型 特征 
numerical_fea = list(df.select_dtypes(exclude=['object']).columns)
category_fea = list(filter(lambda x: x not in numerical_fea,list(df.columns))) 

# 划分 连续数值型 和 离散数值型 特征 
def get_numerical_serial_fea(data,feas):
    numerical_serial_fea = []
    numerical_noserial_fea = []
    for fea in feas:
        temp = data[fea].nunique()
        if temp <= 10:
            numerical_noserial_fea.append(fea)
            continue
        numerical_serial_fea.append(fea)
    return numerical_serial_fea,numerical_noserial_fea
numerical_serial_fea,numerical_noserial_fea = get_numerical_serial_fea(df, numerical_fea) 

# 对于 离散数值型  和  类别型， 都可用 value_counts() 去探查不同数值上的分布情况 
df['subGrade'].value_counts() 


# 对于连续数值型， 每个数字特征得分布可视化
f = pd.melt(df, value_vars=numerical_serial_fea)
g = sns.FacetGrid(f, col="variable",  col_wrap=2, sharex=False, sharey=False) 
g = g.map(sns.distplot, "value")    



```  

