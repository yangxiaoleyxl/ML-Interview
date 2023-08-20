## Decision Tree
### 决策树
决策树是一种基本的分类与回归方法。这里主要讨论决策树用于分类。

决策树模型是描述对样本进行分类的树形结构。树由结点和有向边组成：

- 内部结点表示一个特征或者属性。
- 叶子结点表示一个分类。
- 有向边代表了一个划分规则。
- 决策树从根结点到子结点的的有向边代表了一条路径。决策树的路径是互斥并且是完备的。

用决策树分类时，对样本的某个特征进行测试，根据测试结果将样本分配到树的子结点上。此时每个子结点对应该特征的一个取值。

递归地对样本测试，直到该样本被划分叶结点。最后将样本分配为叶结点所属的类。

决策树的优点：
- 可读性强，
- 分类速度快。

决策树学习通常包括3个步骤：
- 特征选择。
- 决策树生成。
- 决策树剪枝。  

### 梯度提升树 GBDT 
- Boosting Tree 是以决策树为基本学习器的加法模型 
- 对于分类问题, 使用二叉分类树; 对于回归问题, 使用二叉回归树
- Boosting Tree 采用前向分步算法
    - 初始化提升树, $f_0(x)=0$ 
    - 第 m 步的模型: $f_m{x} = f_{m-1}(x) + h_m(x, \theta)$ 
    - 经验风险极小化确定第m个决策树参数, $\Theta_m = argmin_{\Theta_m} \sum_{i=1}^{N} L(y_i, f_m(x)) $, 此处为引入正则化, XGBoost中引入 
- 回归问题通常使用**平方误差损失函数**, 分类问题通常使用**指数损失函数**

### GBT 
- 当损失函数为平方或指数损失函数时，每一步优化都很简单，但为一般函数时，每一步优化不易，因此提出梯度提升算法
- GBT利用**损失函数的负梯度在当前模型的值作为残差的近似值，从而拟合一个回归树** 
$$ 
L(y, f_m(x)) = L(y, f_{m-1}(x) + h_m(x;\Theta) ) = L(y, f_{m-1}{x}) + \frac{ \partial L(y, f_{m-1}(x)) }{ \partial f_{m-1}(x) } h_{m}(x;\Theta) 
$$
故有 
$$ 
\delta L = \frac{ \partial L(y, f_{m-1}(x)) }{ \partial f_{m-1}(x) } h_{m}(x;\Theta) 
$$ 

### RF vs GBDT  
从模型的框架上，
- GBDT 是 boosting 模型
- RF 是 bagging 模型 

从偏差分解的角度上,
- GBT采用弱分类器（此种分类器是**高偏差，低方差**），GBDT综合了这些分类器，**每一步降低了偏差**，但保持了方差
- RF采用完全成长的子决策树（低偏差，高方差）。RF要求子树之间尽量无关，故综合之后可以降低方差 

### XGBOOST 
- xgboost与GBDT一样,使用前向分步方法，xgboost的改进在于使用**结构风险最小化**来确定下一个决策树的参数 $\Theta_{m}$ 
$$ 
\Theta_{m} = argmin \sum_{i=1}^{N}L(y_i, f_m(x)) + \Omega(h_m(x))
$$ 
$\Omega(h_m(x))$ 是正则化项
以损失函数为目标函数，对其进行二阶泰勒展开，GBDT只用了一阶泰勒展开，这是**GBDT与XGBOOST**的重要区别 

XGBOOST的缺点：
- 由于是基于预排序的决策树算法，因此空间消耗量大，
- 需要保存数据的特征，还保存了特征排序的结果（为后续快速分割，保存排序后的索引），需要消耗训练数据两倍以上的内存
- 时间开销也较大，遍历每一个分割点时，都要进行分裂增益计算，消耗代价大
- Cache 优化不友好。在预排序后，特征对梯度的访问是一种随机访问，并且不同的特征访问的顺序不一样，无法对cache进行优化。同时，在每一层长树的时候，需要随机访问一个行索引到叶子索引的数组，并且不同特征访问的顺序也不一样，也会造成较大的cache miss


### LightGBM  
#### LightGBM的思想 
- 若减少训练样本数量, 或减少样本的训练特征数量，则可以大幅度提高训练速度
- LGB的两个策略
    - GOSS:基于梯度的采样。**用于减少样本数量** 
    - EFB:基于互斥特征的特征捆绑。**用于减少样本特征的数量** 

LGB 是针对 XGBOOST 的上述缺陷做出了7点优化：
- 基于 Histogram 的决策树算法
- 单边梯度采样 Gradient-based One-Side Sampling（GOSS）: 使用GOSS可以减少大量只具有小梯度的数据实例, 这样在计算信息增益的时候只利用剩下的具有高梯度的数据就可以了。相比XGBoost遍历所有特征值节省了不少时间和空间上的开销
- 互斥特征捆绑 Exclusive Feature Bundling (EFB)：使用EFB可以将许多互斥的特征绑定为一个特征，这样达到了降维的目的 
- 带深度限制的 Leaf-wise 的叶子生长策略：大多数 GBDT 工具支持 level-wise, 但按层生长的策略不加区分地对待同一层的叶子。实际上很多叶子的分裂增益较低，没必要进行搜索和分裂
- 直接支持类别特征 
- 支持高效并行 
- Cache命中率优化   

lightGBM参数优化一般技巧：
- 日常的调参顺序
    - max_depth、num_leaves
    - min_data_in_leaf、min_child_weight
    - bagging_fraction、 feature_fraction、bagging_freq
    - reg_lambda、reg_alpha
    - min_split_gain 

面临过拟合时，可能需要对以下参数进行调优：
- 使用更小的 `max_bin` 
- 使用更小的 `num_leaves` 
- 使用 `min_data_in_leaf` 和 `min_sum_hessian_in_leaf` 
- 通过设置 `bagging_fraction` 和 `bagging_freq` 使用 `bagging_freq`
通过设置 `feature_fraction` 使用特征子采样 
- 使用更大的训练数据 
- 尝试 `lambdal1`、`lambdal2` 和 `min_gain_to_split` 进行正则化 
- 尝试 `max_depths` 以避免树的深度增长  






