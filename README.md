# Task 2 数据分析
## 2.1 EDA 目标
EDA的价值主要在于熟悉数据集，了解数据集，对数据集进行验证来确定所获得数据集可以用于接下来的机器学习或者深度学习使用。

当了解了数据集之后我们下一步就是要去了解变量间的相互关系以及变量与预测值之间的存在关系。

引导数据科学从业者进行数据处理以及特征工程的步骤,使数据集的结构和特征集让接下来的预测问题更加可靠。

## 2.2 内容介绍
1.载入各种数据科学以及可视化库:
数据科学库 pandas、numpy、scipy；
可视化库 matplotlib、seabon；

2.载入数据：
载入训练集和测试集；
简略观察数据(head()+shape)；

3.数据总览:
通过describe()来熟悉数据的相关统计量
通过info()来熟悉数据类型

4.判断数据缺失和异常
查看每列的存在nan情况
异常值检测

5.了解预测值的分布
总体分布概况
查看skewness and kurtosis
查看预测值的具体频数

## 2.3 代码示例
### 2.3.1 载入各种数据科学与可视化库
```python
import warnings
warnings.filterwarnings('ignore')
import missingno as msno
import pandas as pd
from pandas import DataFrame
import matplotlib.pyplot as plt 
import seaborn as sns
import numpy as np
```
### 2.3.2 载入训练集和测试集
导入训练集train.csv
```python
import pandas as pd
from pandas import DataFrame, Series
import matplotlib.pyplot as plt
Train_data = pd.read_csv('./train.csv')
```
导入测试集testA.csv
```python
import pandas as pd
from pandas import DataFrame, Series
import matplotlib.pyplot as plt 
Test_data = pd.read_csv('./testA.csv')
```
观察train首尾数据
```python
Train_data.head().append(Train_data.tail())
```
观察train数据集的行列信息
```python
Train_data.shape
```
观察testA首尾数据
```python
Test_data.head().append(Test_data.tail())
```
观察testA数据集的行列信
```python
Test_data.shape
```
