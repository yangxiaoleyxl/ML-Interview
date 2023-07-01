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

$$
WOE_i = ln(( \frac{Bad_i +0.5}{Good_i + 0.5}) / (\frac{Bad_T}{Good_T} )    
$$ 

在实践中，我们还需**跨数据集检验WOE分箱的单调性**。如果在训练集上保持单调，但在验证集和测试集上**发生翻转而不单调**，那么说明分箱并不合理，需要再次调整

IV 叫信息值，是与WOE密切相关的一个指标，常用来评估变量的预测能力。因而可用来快速筛选变量。
- <font color="red"> IV measures the strength of that relationship </font>  

### 2.WOE和IV的计算
WOE 计算公式
$$
WOE_{i} = ln( \frac{Bad_i}{Bad_T}) - ln( \frac{Good_i}{Good_T} )  

$$   
可以理解为：**WOE = ln (第i个分箱的坏人数 / 总坏人数) - ln (第i个分箱的好人数 / 总好人数)**  

更进一步，可以理解为：**每个分箱里的坏人分布相对于好人分布之间的差异性**   

#### 从贝叶斯的角度看 WOE 
如果搜集到的数据与先验认知的差距不大，我们就认为这个数据中得到的证据价值不大，反之则认为带来的信息越多。因此，WOE用以衡量**对先验认识修正的增量**，这就是WOE被取名为“证据权重”的原因   

$$
\frac{ P(Y=Bad|X) }{ P(Y=Good|X) } = \frac{ P(X|Y=Bad) }{ P(X|Y=Good) } \frac{P(Y=Bad)}{P(Y=Good)} 
$$
两边取对数 In 

$$
ln[\frac{ P(Y=Bad|X) }{ P(Y=Good|X) }] = ln[\frac{ P(X|Y=Bad) }{ P(X|Y=Good) }] + ln[\frac{P(Y=Bad)}{P(Y=Good)}]  
$$ 
进一步有，
$$
ln[\frac{ Bad }{ Good }] = WOE + ln[ \frac{Bad_T}{Good_T} ]  
$$ 

$ln[\frac{ P(Y=Bad|X) }{ P(Y=Good|X) }]$ 是后验，$ ln[\frac{ P(X|Y=Bad) }{ P(X|Y=Good) }]$ 是观测数据更新的信息，即WOE, $ ln[\frac{P(Y=Bad)}{P(Y=Good)}] $ 是先验项 

IV计算公式
$$
IV_i = (Bad_i/Bad_T - Good_i/Good_T) \times WOE_i
$$  

$$
IV = \sum_{i=1}^{n} IV_i 
$$  
IV 是 WOE 的加权和

