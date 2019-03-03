### lightGbm直方图优化

不同于xgboost在寻找分裂点的时候遍历所有样本每个特征的每个取值,ligtm通过将连续特征进行离散化也就是将连续特征分桶，将某个区间的值映射成某个数字.统计每个bin中的一阶导和二阶导。对所有特征构建直方图。然后 遍历所有特征的每个bin，使用和xgboost相同的评分函数来寻找最优的分割点.
同时树的树的生长策略和xgboost的也不同。一般的gbdt树生成策略都是按层生长，就是对同一层的每个叶子节点都进行分裂。但是这种分裂方式，某些节点分裂的信息增益很低，这种一般是没必要分裂的。
ligtm树生成策略是带有深度限制的按叶子生成。就是对同一层的所有节点，只对分裂后信息增益最大的那个进行分裂。但是这样后造成树的深度过深，容易过拟合，所以可以对树的深度进行限制来减少过拟合.