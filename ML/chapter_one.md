# 机器学习笔记     第一次课

Author：刘欢 Liu Huan    Date：2018.09.03    Class：Machine Learning

---

## 基本术语--数据：

* 机器学习：以计算为手段（学习算法）利用经验（计算机系统内数据）改善系统自身性能（数据模型）。

  - 最常用定义：计算机系统能够利用经验提高自身的性能。
  - 可操作定义：机器学习的本质是一个基于经验数据的函数估计问题。
  - 统计学定义：提取重要模式、趋势，并理解数据，即从数据中学习。

  ![](https://ws4.sinaimg.cn/large/0069RVTdly1fuwn6iq81hj30br084wf4.jpg)

* 数据集 data set：记录的集合。

* 记录：一个事件或对象的描述。称为一个**“示例”(instance)**或**“样本(sample)”**。

* 特征 feature 属性 attribute：事物或对象在某方面的表现或性质的事项。

* 属性值 attribute value：属性的取值。

* 属性空间 attribute space 样本空间 sample space 输入空间：属性张成的空间。

* 特征向量 feature vector：也可称一个示例为特征向量。

* 一般的，令 D = {**x<sub>1</sub>**,**x<sub>2</sub>**,…,**x<sub>m</sub>**} 表示包含了m个示例的数据集，每个示例由d个属性描述，每个示例是 **x<sub>i</sub>** = (x<sub>i1</sub>;x<sub>i2</sub>;…x<sub>id</sub>) 是d维样本空间 $$\chi$$  中的一个向量，**x<sub>i</sub>** $$ \in\chi$$ ，其中 x<sub>ij</sub> 是 **x<sub>i</sub>** 在第 j 个属性上的取值。d 称为样本 **x<sub>i</sub>** 的维度(dimensionality)。
* 学习 learning 训练 training：从数据中学得模型的过程，这个过程通过某种学习算法来完成。

* 训练数据 training data：训练过程中使用的数据。

* 训练样本 training sample：其中的每一个样本称为一个训练样本。

* 训练集 training set：训练样本组成的集合。

* 标记 label：关于训练样本“结果”的信息。

* 样例 example：拥有了标记信息的示例。

  > 一般的用（**x<sub>i</sub>**, y<sub>i</sub>) 表示第 i 个样例，其中 y<sub>i</sub> $$\in $$ $$\mathcal{Y}$$ 是示例的 **x<sub>i</sub>**的标记，$$\mathcal{Y}$$ 是所有标记的集合。

* 标记空间 label space 输出空间：所有标记的集合。

## 基本术语--任务：

* 假设 hypothesis：学得模型对于了关于数据的某种潜在的规律。

* 真相 事实 ground-truth：这种潜在规律本身。

* 学习过程就是为了找出或者逼近真相。

* 学习器 learner：学习算法在给定数据与参数空间上的实例化。

* 分类 classification： 若预测的是离散值，此类学习任务称为分类。

  * 二分类：两个预测值
  * 多分类：多个预测值、

  > 二分类 binary classification：只涉及**两个**类别的分类任务。一个称为正类(positive class)，一个称为反类(negative class)。
  >
  > 多分类 multi-class classification：涉及**三个及以上**的类别的分类任务。

* 回归 regression：若预测的是连续值，此类学习任务称为回归。

  > 例如：瓜的成熟度（0.9、0.8）

* 聚类 clustering：对给定训练集，将其分为几组，每组称为一个“簇”(cluster)；这些簇可能对应着一些潜在概念划分。通常这些概念我们事先不知道且训练样本通常不带有标记信息。

* 有无标记信息分类：

  * 监督学习 supervised learning：分类、回归
  * 无监督学习 unsupervised learning：聚类
  * 半监督学习：两者结合

* 泛化 generalization：学得模型适用于新样本的能力。机器学习的目标是让学到的模型能很好的适用于“新样本”，而不是训练集合。

* 独立同分布 i.i.d：通常假设样本空间符合一个未知的分布。我们获得的每个样本都是独立的从这个分布上采样获得的。一般来说训练集越多，得到的模型泛化能力越强。

* 预测任务目的：就是要通过对训练集的学习，期望得到一个从输入空间到输出空间的**映射**。

## 假设空间

* 我们可以把学习看做是一个在所有假设组成的空间中进行搜索的过程，搜索目标是找到与训练集“匹配”(fit)的假设。
* 版本空间 version space：现实问题中，面临的假设空间可能非常巨大，而供学习的训练集有限。搜索过程中可能存在多个假设与训练集一致，我们把这些假设组成的集合称为“版本空间”。

![](https://ws3.sinaimg.cn/large/006tNbRwly1fuxf1356ssj30bu06r3yx.jpg)

## 归纳偏好

* 归纳偏好：当有多个假设成立时，算法的启发式或“价值观”。

* 奥卡姆剃刀：当有多个假设与观察一致时，选择最简答的那个。

* 没有免费的午餐定理：一个算法A如果在某些问题上比另一个算法B好，那么必然存在另一些问题，B比A好。

  > 脱离实际问题，空谈某个算法好没有意义。
  >
  > 实际问题中，并非所有问题出现的可能性都相同。

![](https://ws2.sinaimg.cn/large/006tNbRwly1fuxf1u72huj30ks07xdh0.jpg)