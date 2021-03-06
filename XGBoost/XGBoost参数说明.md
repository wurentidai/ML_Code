 - booster [default=gbtree]

有两中模型可以选择gbtree和gblinear。gbtree使用基于树的模型进行提升计算，gblinear使用线性模型进行提升计算。缺省值为gbtree。



- silent [default=0]

取0时表示打印出运行时信息，取1时表示以缄默方式运行，不打印运行时信息。缺省值为0。



- nthread

XGBoost运行时的线程数。缺省值是当前系统可以获得的最大线程数。



- num_pbuffer

预测缓冲区大小，通常设置为训练实例的数目。缓冲用于保存最后一步提升的预测结果，无需人为设置。



- num_feature

Boosting过程中用到的特征维数，设置为特征个数。XGBoost会自动设置，无需人为设置。



- eta [default=0.3] 

为了防止过拟合，更新过程中用到的收缩步长。在每次提升计算之后，算法会直接获得新特征的权重。 eta通过缩减特征的权重使提升计算过程更加保守。缺省值为0.3 。
取值范围为：[0,1]



- gamma [default=0] 

minimum loss reduction required to make a further partition on a leaf node of the tree. the larger, the more conservative the algorithm will be. 
取值范围为：[0,∞]



- max_depth [default=6] 

数的最大深度。缺省值为6。
取值范围为：[1,∞]

 

- min_child_weight [default=1] 

孩子节点中最小的样本权重和。如果一个叶子节点的样本权重和小于min_child_weight则拆分过程结束。在现行回归模型中，这个参数是指建立每个模型所需要的最小样本数。该成熟越大算法越conservative。
取值范围为：[0,∞]



- max_delta_step [default=0] 

我们允许每个树的权重被估计的值。如果它的值被设置为0，意味着没有约束；如果它被设置为一个正值，它能够使得更新的步骤更加保守。通常这个参数是没有必要的，但是如果在逻辑回归中类极其不平衡这时候他有可能会起到帮助作用。把它范围设置为1-10之间也许能控制更新。 
取值范围为：[0,∞]



- subsample [default=1] 

用于训练模型的子样本占整个样本集合的比例。如果设置为0.5则意味着XGBoost将随机的从整个样本集合中随机的抽取出50%的子样本建立树模型，这能够防止过拟合。 
取值范围为：(0,1]



- colsample_bytree [default=1] 

在建立树时对特征采样的比例。缺省值为1。
取值范围为：(0,1]



- lambda [default=0] 

L2 正则的惩罚系数

- alpha [default=0] 

L1 正则的惩罚系数

- lambda_bias 

在偏置上的L2正则。缺省值为0（在L1上没有偏置项的正则，因为L1时偏置不重要）。


- objective [ default=reg:linear ] 

定义学习任务及相应的学习目标，可选的目标函数如下：

“reg:linear” —— 线性回归。

“reg:logistic”—— 逻辑回归。

“binary:logistic”—— 二分类的逻辑回归问题，输出为概率。

“binary:logitraw”—— 二分类的逻辑回归问题，输出的结果为wTx。

“count:poisson”—— 计数问题的poisson回归，输出结果为poisson分布。在poisson回归中，max_delta_step的缺省值为0.7。(used to safeguard optimization)

“multi:softmax” –让XGBoost采用softmax目标函数处理多分类问题，同时需要设置参数num_class（类别个数）

“multi:softprob” –和softmax一样，但是输出的是ndata * nclass的向量，可以将该向量reshape成ndata行nclass列的矩阵。没行数据表示样本所属于每个类别的概率。

“rank:pairwise” –set XGBoost to do ranking task by minimizing the pairwise loss。



- base_score [ default=0.5 ]

所有实例的初始化预测分数，全局偏置；为了足够的迭代次数，改变这个值将不会有太大的影响。




eval_metric [ default according to objective ]

校验数据所需要的评价指标，不同的目标函数将会有缺省的评价指标（rmse for regression, and error for classification, mean average precision for ranking）。

用户可以添加多种评价指标，对于Python用户要以list传递参数对给程序，而不是map参数list参数不会覆盖’eval_metric’。

可供的选择如下:

“rmse”: root mean square error

“logloss”: negative log-likelihood

“error”: Binary classification error rate. It is calculated as #(wrong cases)/#(all cases). For the predictions, the evaluation will regard the instances with prediction value larger than 0.5 as positive instances, and the others as negative instances.

“merror”: Multiclass classification error rate. 

“mlogloss”: Multiclass logloss.

“auc”: Area under the curve for ranking evaluation.

“ndcg”:Normalized Discounted Cumulative Gain

“map”:Mean average precision

“ndcg@n”,”map@n”: n can be assigned as an integer to cut   off the top positions in the lists for evaluation.

“ndcg-“,”map-“,”ndcg@n-“,”map@n-“: In XGBoost, NDCG andMAP will evaluate the score of a list without any positive   samples as 1. By adding “-” in the evaluation metric XGBoostwill evaluate these score as 0 to be consistent under some    conditions. training repeatively



- seed [ default=0 ]

随机数的种子。缺省值为0。