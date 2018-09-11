# 机器学习笔记      第二次课

Author：刘欢 Liu Huan    Date：2018.09.03    Class：Machine Learning

---

## 经验误差与过拟合

### 错误率与误差

* 错误率 error rate：错分样本的占比，即如果在m个样本中有a个分类错误，则 `E = a/m`

* 精度 accuracy：相应的`1 - a/m`称为精度

* 误差 error：把学习器上的实际预测输出与样本的真实输出之间的差异称为“误差”

  * 训练误差 training error 经验误差 empirical error：训练集上的误差
  * 测试误差 test error：测试集上的误差
  * 泛化误差 generalization error：除训练集外的所有样本

  > 注意：我们希望得到泛化误差小的学习器。但由于事先不知道样本特征，我们只能做的努力是把经验误差最小化。

* 过拟合 overfitting：将训练集自身的特点当做了所有未知样本的特性。

  > 优化目标添加正则项
  >
  > 提前结束

* 欠拟合 underfitting：对样本的一般性质尚未学好。

  > 决策树：拓展分支
  >
  > 神经网络：增加训练轮数

* 模型选择 model selection：在现实任务中，对一个问题求解往往有多个算法可以选择；而一个算法因为不同的参数配置，也可以产生不同的模型。

## 评估方法

* 泛化性能、时间开销、存储开销、可解释性等方面的因素进行评估并作出选择。

* 将测试集上的测试误差作为泛化误差的近似。

* 测试集与训练集尽可能互斥。

* 拆分测试集与训练集：

  * 留出法 hold-out ：直接将数据集$$D$$划分为两个互斥的集合

    > 从采样(sampling)的角度：保留原类别比例，即数据划分尽可能保持数据一致性（分层采样）
    >
    > 为了保证选取特定类别的数据具有随机性，一般若干次随机划分、重复实验评估对误差取评估
    >
    > 训练/测试样本比例为2:1~4:1

  * 交叉验证法 cross validation：将数据集分层采样(保持数据分布一致)划分为k个大小相似的互斥子集，每次用k-1个子集的并集作为训练集，余下的子集作为测试集，最后返回k个测试结果的均值。k通常取10。

    > 通常把交叉验证法称为“$$k$$ 折交叉验证法”。

    ![](https://ws1.sinaimg.cn/large/0069RVTdly1fv3eelr5pbj30nq0actai.jpg)

  * 留一法 Leave-One-Out，简称LOO：令k取数据集样本数

    > 不受随机样本划分的影响
    >
    > 结果往往比较准确
    >
    > 数据集较大时，计算开销过大

  * 自助法 bootstrapping：以“自助采样法”为基础，有放回抽取。

    * 给定包含$$m$$个数据的数据集$$D$$，我们对他进行采样产生数据集$$D$$ ‘ ：每次随机从$$D$$挑选一个样本，将其拷贝放入$$D$$ ‘ ，然后再将该样本放回初始数据集$$D$$中，使得该样本在下次采样仍然有机会被采集到；这个过程重复执行$$m$$次后，我们就得到了包含$$m$$个样本的数据集$$D$$ ’。

    * 很明显，有一部分样本会在$$D$$ ‘ 中出现多次，有些则不会出现。样本在$$m$$次采样中始终不会被采集到的概率为：

      $$\lim\limits_{m \to \infty}(1 - \frac{1}{m})^m \to \frac{1}{e} \approx 0.368$$

      即通过自助采样，初始数据集$$D$$中约有$$36.8\%$$的样本没出现在采样数据集中。所以我们把$$D$$ ’ 作为训练集，$$D \backslash D$$用作测试集。这样实际评估的模型与期望评估的模型都使用$$m$$个训练样本，而我们仍有数据总量约三分之一的没在训练集出现的样本用于测试。这样的测试结果，亦称“包外估计”(out-of-bagestimate)

    > 在数据集较小时、难以有效划分训练/测试集时很有用
    >
    > 能从初始数据集中集中产生多个不同的训练集
    >
    > 改变了数据集初始的分布，引入了误差。因此，在数据量足够时，交叉验证法与留出法更常用

### 调参与验证集

* 参数 parameter：

  * 超参数：数目在10个以内；是算法的参数；人工设定。
  * 模型参数：数目可能很多 ；是模型的参数；通过学习来产生多个候选值。

* 调参 parameter tuning：对学习算法的参数进行设置。需要给定范围与变化步长。

* 引入新概念：验证集 validation set：模型评估与选择中用于评估测试的数据集。

  ![](https://ws4.sinaimg.cn/large/0069RVTdly1fv3j0pv1edj30ei08ejrx.jpg)

## 性能度量

* 性能度量 performance measure：是衡量模型泛化能力的评价标准，决定于任务需求。

  * 回归任务最常用的性能度量是“均方误差”（mean squared error，简称MSE）

    $$E(f;D)=\frac{1}{m} \sum\limits_{i=1}^m(f(\vec{x_i})-y_i)^2$$

    更一般的，对于数据分布$$\mathcal{D}$$和概率密度函数$$p(.)$$，均方误差可以描述为

    $$E(f;\mathcal{D})=\int\nolimits_{x \sim \mathcal{D}} (f(\vec{x}-y)^2p(\vec{x}))$$

  * 分类任务，错误率与精度是最常用的性能度量

    * 错误率 error rate

      ![](https://ws4.sinaimg.cn/large/0069RVTdly1fv3myhfqo6j30af02lglq.jpg)

    * 精度 accuracy

      ![](https://ws1.sinaimg.cn/large/0069RVTdly1fv3myu3v1vj30do0473yv.jpg)

  * 信息检索与WEB搜索场景下，查准率与查全率

    对于二分类问题，可根据其真实类别与学习器预测类别的组合划分为**真正例**(true positive，TP)、**假正例**(false positive，FP)、**真反例**(true negative，TN)、**假反例**(false negative，FN)。

  > 查准率 precision：P = TP/(TP + FP)  预测出来的正例中正确的比率。
  >
  > 查全率 recall：P = TP/(TP + FN)  正例被预测出来的比率
  >
  > 查准率与查全率是一对矛盾的度量。一般来说一方数值较高时，另一方较低。通常在一些简单任务中才可能让查全率与查准率都很高。

  * 统计真实标记和预测结果的组合可以得到 “混淆矩阵”

    ![](https://ws1.sinaimg.cn/large/0069RVTdly1fv3n2skgoyj30o405otag.jpg)

* P-R曲线

  * 若一个学习算法的PR曲线被另一个学习算法的曲线完全“包住”，则可以断定后者的性能优于前者。

  * 若两个学习算法的PR曲线发生交叉，则难以判断孰优孰劣，只能在具体的查准率和查全率条件下进行比较。

    * 可通过比较P-R曲线下的面积
    * 利用平衡点（即P=R时的取值）
    * 利用F1度量

    ![](https://ws4.sinaimg.cn/large/0069RVTdly1fv3n8atzprj30gb0cwdia.jpg)

  * F1度量：

    ![](https://ws3.sinaimg.cn/large/0069RVTdly1fv3nkhb6gnj30gk02zmxj.jpg)

  * 比F1更一般的形式$$F_ \beta$$:

    ![](https://ws3.sinaimg.cn/large/0069RVTdly1fv3nk43rhvj30a603dglw.jpg)

    * $$\beta = 1$$：标准F1
    * $$\beta > 1$$：偏重查全率 逃犯信息检索
    * $$\beta < 1$$：偏重查准率 商品推荐系统

    > 当我们有多个混淆矩阵时，我们希望在n个二分类混淆矩阵上综合考虑查准率与查全率。
    >
    > * 宏：先在各个矩阵上分别计算出查准率与查全率，然后再计算平均值。得到**宏查准率**(macro-P)、**宏查全率**(macro-R)，以及相应的**宏F1**(macro-F1):
    >
    >   ![](https://ws3.sinaimg.cn/large/0069RVTdly1fv3nz9hok0j30lz0b9wff.jpg)
    >
    > * 微：先将混淆矩阵的对应元素进行平均，基于平均值计算**微查准率**(micro-P)、**微查全率**(micro-R)，以及相应的**微F1**(micro-F1):
    >
    >   ![](https://ws2.sinaimg.cn/large/0069RVTdly1fv3o2f4oqkj30kw0bd754.jpg)

* ROC 受试者工作特征：

  * 真正例率：TPR = TP/(TP+FN)
  * 假正例率：FPR = FP/(TN+FP)

  类似P-R曲线，根据学习器的预测结果对样例排序，并逐个作为正例进行预测，以“假正例率”为横轴，“真正例率”为纵轴可得到ROC曲线，全称“受试者工作特征”。

  ROC图的绘制：给定$$m^+$$个正例和$$m^-$$个负例，根据学习器预测结果对样例进行排序，将分类阈值设为每个样例的预测值，当前标记点的坐标为$$(x,y)$$，当前若为真，则对应标记点的坐标为$$(x,y+\frac{1}{m^+})$$；当前若为假正例，则对应标记点的坐标为$$(x+\frac{1}{m^-},y)$$，然后用线段连接相邻点。
  * 若某个学习器的ROC曲线被另一个学习器的曲线“包住”，则后者性能优于前者。

  * 否则根据曲线交叉，可以根据ROC曲线下的面积大小进行比较，即AUC值

    >AUC可估算为：
    >
    >![](https://ws1.sinaimg.cn/large/0069RVTdly1fv3qoo94w3j30et031mxj.jpg)
    >
    >AUC衡量了样本预测的排序质量。

    ![](https://ws1.sinaimg.cn/large/0069RVTdly1fv3qmv36emj30dc0dmmz1.jpg)

* 代价敏感错误率

  现实任务中不同类型错误所造成的后果很可能不同，为了权衡不同类型错误所造成的不同损失，可为错误赋予“非均等代价”。

  以二分类为例，可根据领域知识设定“代价矩阵”，如下表所示，其中$$cost_{ij}$$表示将第$$i$$类样本的代价。损失程度越大，$$cost_{01}$$与$$cost_{10}$$值的差别越大。

  ![](https://ws2.sinaimg.cn/large/006tNbRwly1fv4aqp5eh2j30m305ot9a.jpg)

  在非均等代价下，不再最小化错误次数，而是最小化“总体代价”，则“代价敏感”错误率相应为：

  ![](https://ws3.sinaimg.cn/large/006tNbRwly1fv4atsgmflj30mg02rmy6.jpg)

* 代价曲线：在非均等代价下，ROC曲线不能直接反应出学习器的期望总体代价，而“代价曲线可以。

  * 代价曲线的横轴是取值为[0,1]的正例概率代价：

    ![](https://ws1.sinaimg.cn/large/006tNbRwly1fv4bwity28j30e602qq3a.jpg)

  * 纵轴是取值为[0,1]的归一化代价：

    ![](https://ws1.sinaimg.cn/large/006tNbRwly1fv4bxihxwij30hk038gmb.jpg)

  * 代价曲线绘制：

    ![](https://ws1.sinaimg.cn/large/006tNbRwly1fv4c2p7k3kj30ex0b0go1.jpg)

## 比较检验

正在写。

## 偏差与方差

正在写。