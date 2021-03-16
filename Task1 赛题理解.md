# Datawhale 零基础入门数据挖掘-Task1 赛题理解

## 1.1学习目标
理解赛题数据和目标，清楚评分体系。

完成相应报名，下载数据和结果提交打卡（可提交示例结果），熟悉比赛流程

## 1.2赛题概况

比赛要求参赛选手根据给定的数据集，建立模型，预测不同的心跳信号。赛题以预测心电图心跳信号类别为任务，数据集报名后可见并可下载，该该数据来自某平台心电图数据记录，总数据量超过20万，主要为1列心跳信号序列数据，其中每个样本的信号序列采样频次一致，长度相等。为了保证比赛的公平性，将会从中抽取10万条作为训练集，2万条作为测试集A，2万条作为测试集B，同时会对心跳信号类别（label）信息进行脱敏。
## 1.3 数据概况
train.csv

id 为心跳信号分配的唯一标识
heartbeat_signals 心跳信号序列(数据之间采用“,”进行分隔)
label 心跳信号类别（0、1、2、3）

testA.csv

id 心跳信号分配的唯一标识
heartbeat_signals 心跳信号序列(数据之间采用“,”进行分隔)

## 1.4 预测指标
多分类算法常见的评估指标如下：

1、混淆矩阵（Confuse Matrix）

（1）若一个实例是正类，并且被预测为正类，即为真正类TP(True Positive )

（2）若一个实例是正类，但是被预测为负类，即为假负类FN(False Negative )

（3）若一个实例是负类，但是被预测为正类，即为假正类FP(False Positive )

（4）若一个实例是负类，并且被预测为负类，即为真负类TN(True Negative ）

第一个字母T/F，表示预测的正确与否；第二个字母P/N，表示预测的结果为正例或者负例。如TP就表示预测对了，预测的结果是正例，那它的意思就是把正例预测为了正例。

2.准确率（Accuracy） 

准确率是常用的一个评价指标，但是不适合样本不均衡的情况，医疗数据大部分都是样本不均衡数据。 

$$ Accuracy=\frac{Correct}{Total}\ Accuracy = \frac{TP + TN}{TP + TN + FP + FN} $$ 

3、精确率（Precision）也叫查准率简写为P

精确率(Precision)是针对预测结果而言的，其含义是在被所有预测为正的样本中实际为正样本的概率在被所有预测为正的样本中实际为正样本的概率，精确率和准确率看上去有些类似，但是是两个完全不同的概念。精确率代表对正样本结果中的预测准确程度，准确率则代表整体的预测准确程度，包括正样本和负样本。 $$ Precision = \frac{TP}{TP + FP} $$ 4.召回率（Recall） 也叫查全率 简写为R

召回率(Recall)是针对原样本而言的，其含义是在实际为正的样本中被预测为正样本的概率。 

$$ Recall = \frac{TP}{TP + FN} $$

5.宏查准率（macro-P）

计算每个样本的精确率然后求平均值 

$$ {macroP=\frac{{1}}{{n}}{\mathop{ \sum }\limits_{{1}}^{{n}}{p\mathop{{}}\nolimits_{{i}}}}} $$ 

6.宏查全率（macro-R）

计算每个样本的召回率然后求平均值 

$$ {macroR=\frac{{1}}{{n}}{\mathop{ \sum }\limits_{{1}}^{{n}}{R\mathop{{}}\nolimits_{{i}}}}} $$ 7.宏F1（macro-F1） $$ {macroF1=\frac{{2 \times macroP \times macroR}}{{macroP+macroR}}} $$ 与上面的宏不同，微查准查全，先将多个混淆矩阵的TP,FP,TN,FN对应位置求平均，然后按照P和R的公式求得micro-P和micro-R，最后根据micro-P和micro-R求得micro-F1

8.微查准率（micro-P） 

$$ {microP=\frac{{\overline{TP}}}{{\overline{TP} \times \overline{FP}}}} $$ 

9.微查全率（micro-R） 

$$ {microR=\frac{{\overline{TP}}}{{\overline{TP} \times \overline{FN}}}} $$ 

10.微F1（micro-F1） 

$$ {microF1=\frac{{2 \times microP\times microR }}{{microP+microR}}} $$
