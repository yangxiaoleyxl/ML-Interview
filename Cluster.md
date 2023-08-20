### Clustering 
#### Clustering 的度量指标 
#### 外部指标 
- Jaccard系数
- FM指数
- Rand指数 
- ARI指数 
#### 内部指标 
- DB指数
- Dunn指数  
#### 距离度量
- `Minkowski distance` 
- `Value Difference Metric`(VDM) 

### 原型聚类 
常见的原型聚类：
- k-means
- Learning Vector Quantization
- Mixture of Gaussian

#### K-means 
算法步骤如下：
- 从样本中随机初始化 K 个簇心 
- 不断迭代至算法收敛或到达迭代次数上限:
    - 计算每个样本到 K 个簇心的距离，将其 **划分到最近簇心的簇中**
    - 以簇中样本的均值更新簇心 
    - 若簇心不再变化(算法收敛),结束迭代，否则继续更新簇心 
