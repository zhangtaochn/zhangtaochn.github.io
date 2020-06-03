---
layout:     post
title:      "基于smote算法的非平衡数据分类算法设计"
subtitle:   "Higher accuracy, higher recall rate"
date:       2018-12-19 15:05:34 +0800
author:     "ZHANG Tao"
header-img: "img/post-2018-12-19-svm-header.png"
tags:
- python
- svm
- decision tree
- machine learning
- smote
- PCA
- data classification
---

## 报告摘要：

面对非平衡的实验数据，通过数据的预处理，设计相应的调节数据平衡的算法，提高对于少类样本的召回率和准确率。本文主要采用PCA降维结合smote算法生成更多的少类样本数据，之后通过决策树、神经网络等多种分类算法模型对于数据进行分类，通过对于各算法模型精确度的对比分析，确定最优算法模型。

## 实验前期分析：

通过对于数据的人工观察可以可知，实验数据共有10个特征，最后1列为数据的标签（1/-1），且label为1的数量占比很少，约占总数据的5.6%，可以认为这是一个unbalanced数据集，且进一步发现，第3到第10列特征数据的变化不明显，基本全为-1或接近-1。故猜想部分维度对于结果影响很小，可以先进行降维处理。故先使用了PCA分析，确定各维度的方差和主成分占比。结果如下：

![图1 特征主成分分析](/img/post-2018-12-19-smote-PCA.png)

<center>图1 特征主成分分析</center>
通过PCA分析可知，第一个维度占主成分比例93.6%，其余特征的重要性几乎可以忽略不计，故为了数据可视化的便利和尽量保留有效信息，此处保留两个特征，以下是通过PCA降维之后并通过smote生成少类样本之后的数据可视化结果。

![图2 PCA+Smote 处理后的训练集](/img/post-2018-12-19-smote-PCA_smote.png)

<center>图2 PCA+Smote 处理后的训练集</center>
如果直接取前两个维度，不经过降维处理，直接进行了可视化分析，结果如下：

![图3 取前两个特征维度训练集数据可视化结果](/img/post-2018-12-19-smote-PCA_smote_2column.png)

<center>图3 取前两个特征维度训练集数据可视化结果</center>
![图4 取前两个特征维度测试集数据可视化结果](/img/post-2018-12-19-smote-PCA_smote_2column_test.png)

<center>图4 取前两个特征维度测试集数据可视化结果</center>
通过可视化结果大致分析，数据应该是为**两个高斯分布且互有重叠的散点图**数据集。测试数据的可视化结果分布与训练集非常相似，只是点的散点的数量不同。

## 算法模型设计：

实验主要应用BP神经网络实现对于数据的分类，神经网络结构为2-X-2结构，X为隐藏层神经元，学习率初始设置为0.05，及其迭代次数等均为实验当中不断调节的参数之一。决策树算法为对比算法模型。

## 实验过程：

### 实验思路：

对于各种算法模型先尝试使用最简单的不降维进行分类，之后采用PCA与smote结合，进行降维和数据平衡，并使用多种分类模型，如此可以通过实验结果观察模型改进的效果。

#### 实验一：不降维直接进行BP神经网络分类（算法代码文件 BPNN.py）

首先进行了不降维直接通过BPNN算法进行二分类，结果如图。 

![图5 BPNN结果](/img/post-2018-12-19-smote-BPNN.png)

<center>图5 BPNN结果</center>
实际运行结果很差，分析可能是因为数据的非平衡问题。

#### 实验二：数据欠抽取BP神经网络分类 （算法代码文件 BPNN1.py）

之后采用了数据的欠抽取，使正负类样本数基本保持相同比例。网络结构为2-5-2 BP神经网络，为经过多轮调参后结果，学习率0.005，得到训练结果为：

![图6 欠抽取BPNN结果](/img/post-2018-12-19-smote-Under-sampling_BPNN.png)

<center>图6 欠抽取BPNN结果</center>
相比较于实验一有了明显改善。

#### 实验三：PCA-Smote处理后BP神经网络分类（算法代码 BPNN_PCA_smote.py）

采用了PCA-Smote对于数据预处理，训练集数据处理后可视化结果为：

![图7 训练集PCA-smote处理后结果](/img/post-2018-12-19-smote-PCA_smote_trainset.png)

<center>图7 训练集PCA-smote处理后结果</center>
测试集经过了PCA处理，得到可视化结果：

![图8 测试集PCA-smote处理后结果](/img/post-2018-12-19-smote-PCA_smote_testset.png)

<center>图8 测试集PCA-smote处理后结果</center>
可以明显发现，测试集也是一个非平衡的数据集，与训练集分布相似。

通过PCA降维和smote生成少类样本之后利用BP神经网络运行结果如图9：

![图9 BPNN_PCA_smote结果](/img/post-2018-12-19-smote-BPNN_PCA_smote.png)

<center>图9 BPNN_PCA_smote 结果</center>
运行结果正常，提高了少类样本的召回率。

#### 实验四：不进行数据平衡处理的决策树算法（算法代码 Decision_tree.py）

利用决策树算法得到的结果，并且经过调节最大树深度等参数没有明显结果，分析决策树算法对于非平衡数据敏感。

![图10 决策树算法分类结果](/img/post-2018-12-19-smote-decision_tree.png)

<center>图10 决策树算法分类结果</center>
决策树对于非平衡数据敏感，难以得到有效结果。

#### 数据平衡处理的决策树算法（算法代码 Decision_tree_balanced.py）

采用了数据的平衡处理，并且调节树深度，最大深度为1/2/3时结果基本一致。

![图 11数据平衡处理决策树算法结果](/img/post-2018-12-19-smote-decision_tree_balanced.png)

<center>图 11数据平衡处理决策树算法结果</center>
能够有效将正类样本区分，基本达到实验要求。

#### 实验六：利用以上五个实验当中三个有效实验算法模型共同预测（算法代码 total_predict.py）

![图12 多算法混合预测结果](/img/post-2018-12-19-smote-multiple_algorithms.png)

<center>图12 多算法混合预测结果</center>
## 实验结论：

采用了precision recall f1-score 指标对于算法模型结果进行评价。

<center> 表1 算法模型结果评价指数表 </center>
![表1 算法模型结果评价指数表](/img/post-2018-12-19-smote-table1.png)

两种算法模型的比较上，都对于非平衡数据集很敏感。在训练的效率上BP神经网络相比较决策树算法需要花费更多的时间，在测试阶段，两种算法速度都很快。

神经网络有更多的参数可供不断调节，能够寻找最优的结果，但这既是一个优点也是一个缺点，也意味着需要花更多的时间用于参数的调节选择上。

从结果看，最终的测试结果，神经网络和决策树结果基本一致，通过不同算法得到了一致的结果也印证了实验结果的有效性。

## 代码文件:

<a href="https://github.com/zhangtaochn/Data-Classification-Based-on-Smote-Algorithms" target="_blank">github：实验相关代码及其报告</a>

<center> 表2 代码文件列表 </center>
| 文件                      | 文件说明                                                 |
| ------------------------- | -------------------------------------------------------- |
| BPNN_1.py                 | 欠抽取BP神经网络算法代码                                 |
| BPNN.py                   | 不经过数据非平衡处理的BP神经网络代码                     |
| BPNN_PCA_smote.py         | 采用了PCA降维smote生成少类数据之后的BP神经网络算法       |
| Decision_tree.py          | 不经过数据非平衡处理的决策树算法                         |
| Decision_tree_balanced.py | 采用了数据平衡处理之后的决策树算法                       |
| Smote_pca.py              | 用于对于数据降维和生成少类样本的模块，以供其他算法调用。 |
| Total_predict.py          | 结合三种有效算法模型的投票预测算法代码                   |
| \result                   | 存放各算法模型运行的测试结果                             |

BP神经网络为自行编写的算法，对比算法决策树为调用sklearn包。