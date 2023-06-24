## WOE和IV指标的含义
- [1.WOE和IV在业务中的应用价值](#1.WOE和IV在业务中的应用价值)
- [2.WOE和IV的计算](#2.WOE和IV的计算)

### 1.WOE和IV在业务中的应用价值 
WOE 叫证据权重，常见的应用包括：
- 处理缺失值
- 处理异常值
- 业务解释性 
- <font color="red"> WOE describes the relationship between a predictive variable and a binary target variable </font>  

WOE 注意事项：
- 分箱时需要注意样本量充足，保证统计意义。
- 若相邻分箱的WOE值相同，则将其合并为一个分箱。
- 当一个分箱内只有好人或坏人时，可对WOE公式进行修正如下

IV 叫信息值，是与WOE密切相关的一个指标，常用来评估变量的预测能力。因而可用来快速筛选变量。
- <font color="red"> IV measures the strength of that relationship </font> 

### 2.WOE和IV的计算
WOE 计算公式
$$
WOE_{i} = ln( \frac{Bad_i}{Bad_T} - \frac{Good_i}{Good_T} ) 
$$  
可以理解为：**WOE = ln (第i个分箱的坏人数 / 总坏人数) - ln (第i个分箱的好人数 / 总好人数)**  

可以理解为：**每个分箱里的坏人分布相对于好人分布之间的差异性**  

IV计算公式
$$
IV_i = (Bad_i/Bad_T - Good_i/Good_T) \times WOE_i
$$  

$$
IV = \sum_{i=1}^{n} IV_i 
$$  
IV 是 WOE 的加权和

