
---
title: 集成学习（以随机森林与adaboosting为例）
date: 2019-08-17
categories: [人工智能, 监督学习]
mathjax: false
---

集成学习著重于在训练集上做文章，将训练集划分为各种子集或权重变换后用较弱的基函數擬合，然後綜合若干個基模型的預測作為最終整體效果

## 集成学习分類

- Booststrap：有放回的抽样方法，是非参数统计中一种重要的估计统计量方差进而进行区间估计的统计方法。
    - 步骤
        - 采用重抽样技术从原始样本中抽取一定数量（自己给定）的样本，此过程允许重复抽样
        - 根据抽出的样本计算统计量T
        - 重复上述N次（一般大于1000），得到统计量T
        - 计算上述N个统计量T的样本方差，得到统计量的方差


- Bagging(Bootstrap Aggregating)：若干個基模型在若干個訓練子集上進行互相獨立的分別訓練，在預測時一次性綜合這些基模型的結果


- Boosting：按迭代順序逐個訓練基模型，在每次訓練後都進行模型測試，然後根據測試結果調整下一輪基模型訓練時所採用的訓練數據，最後預測時仍使用所有子模型的預測得到最終結果

## 随机森林

随机森林在训练过程中对训练集进行随机抽样，分别进行训练后形成若干个小的决策树。分类问题的预测通过这些决策树的投票完成，回归问题的预测通过对基决策树结果求平均完成。基决策树一般采用"较大偏差"、"较小方差"的弱模型，和普通决策树有以下差别：

- 样本裁减：通过随机采样，每个弱模型只训练部分样本数据
- 特征裁减：每个基模型的决策树只选用数据特征中的一部分进行训练和预测，随机抽样保证所有特征都能被部分弱模型学习到
- 小树：由于特征和样本数量有限，每个弱模型决策树都长不高，所以不用担心会过拟合进行剪枝


```python
from sklearn.datasets import load_iris
from sklearn.ensemble import RandomForestClassifier

iris = load_iris()
# Bootstrap: 有放回采样、Out-Bag Estimation: 使用为参与到本身训练的数据集进行评估预测
clf = RandomForestClassifier(n_estimators = 20, bootstrap = True, oob_score = True)

clf.fit(iris.data, iris.target)

clf.oob_score_
```




    0.94666666666666666



## AdaBoost

通过调整训练集中每个样本的权重使得每次迭代在不同的训练集上运行。在第一次迭代时训练集中美个样本会被赋予相同权值，当训练和评估完成后，AdaBoost会更新训练集中的样本，使得在本轮评估中被预测正确的样本权值减少，被预测错误的增加，然后开始第二轮的迭代，如此往复。每个迭代的基模型会逐渐更关注被预测错误的样本，如此提高整体拟合效果。因为每次迭代都用全部样本，故没有oob

AdaBoostClassifier和AdaBoostRegressor都有，即我们的弱分类学习器或者弱回归学习器。理论上可以选择任何一个分类或者回归学习器，不过需要支持样本权重。我们常用的一般是CART决策树或者神经网络MLP。默认是决策树，即AdaBoostClassifier默认使用CART分类树DecisionTreeClassifier，而AdaBoostRegressor默认使用CART回归树DecisionTreeRegressor。另外有一个要注意的点是，如果我们选择的AdaBoostClassifier算法是SAMME.R，则我们的弱分类学习器还需要支持概率预测，也就是在scikit-learn中弱分类学习器对应的预测方法除了predict还需要有predict_proba


```python
from sklearn.datasets import load_iris
from sklearn.ensemble import AdaBoostClassifier

iris = load_iris()

from sklearn.utils import shuffle
X, y = shuffle(iris.data, iris.target)

from sklearn.naive_bayes import GaussianNB
clf = AdaBoostClassifier(GaussianNB())

clf.fit(X[:-20],y[:-20])
clf.score(X[-20:],y[-20:])
```




    1.0



> 参考：

1. [从机器学习到深度学习：基于Scikit-learn与TensorFlow的高效开发实战](http://www.broadview.com.cn/book/5337)
2. [scikit-learn Adaboost类库使用小结](https://www.cnblogs.com/pinard/p/6136914.html)
3. [快速理解bootstrap,bagging,boosting-三个概念](https://blog.csdn.net/wangqi880/article/details/49765673)
