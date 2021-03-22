## 3.1 学习目标
学习时间序列数据的特征预处理方法

学习时间序列特征处理工具 Tsfresh（TimeSeries Fresh）的使用
## 3.2 内容介绍
数据预处理

时间序列数据格式处理

加入时间步特征time

特征工程

时间序列特征构造

特征筛选

使用 tsfresh 进行时间序列特征处理
```python
import pandas as pd
import numpy as np
import tsfresh as tsf
from tsfresh import extract_features, select_features
from tsfresh.utilities.dataframe_functions import impute
```

```python
# 数据读取
data_train = pd.read_csv("train.csv")
data_test_A = pd.read_csv("testA.csv")

print(data_train.shape)
print(data_test_A.shape)
```

```python
(100000, 3)
(20000, 2)
```

```python
data_train.head().append(data_train.tail())
```

```python
### 3.3.2 数据预处理
# 对心电特征进行行转列处理，同时为每个心电信号加入时间步特征time
train_heartbeat_df = data_train["heartbeat_signals"].str.split(",", expand=True).stack()
train_heartbeat_df = train_heartbeat_df.reset_index()
train_heartbeat_df = train_heartbeat_df.set_index("level_0")
train_heartbeat_df.index.name = None
train_heartbeat_df.rename(columns={"level_1":"time", 0:"heartbeat_signals"}, inplace=True)
train_heartbeat_df["heartbeat_signals"] = train_heartbeat_df["heartbeat_signals"].astype(float)

train_heartbeat_df
```

```python
# 将处理后的心电特征加入到训练数据中，同时将训练数据label列单独存储
data_train_label = data_train["label"]
data_train = data_train.drop("label", axis=1)
data_train = data_train.drop("heartbeat_signals", axis=1)
data_train = data_train.join(train_heartbeat_df)

data_train
```

```python
data_train[data_train["id"]==1]
```

### 3.3.3 使用 tsfresh 进行时间序列特征处理

1.特征抽取
**Tsfresh（TimeSeries Fresh）**是一个Python第三方工具包。 它可以自动计算大量的时间序列数据的特征。此外，该包还包含了特征重要性评估、特征选择的方法，因此，不管是基于时序数据的分类问题还是回归问题，tsfresh都会是特征提取一个不错的选择。

2. 特征选择
train_features中包含了heartbeat_signals的779种常见的时间序列特征（所有这些特征的解释可以去看官方文档），这其中有的特征可能为NaN值（产生原因为当前数据不支持此类特征的计算），使用以下方式去除NaN值：

```python
from tsfresh.utilities.dataframe_functions import impute

# 去除抽取特征中的NaN值
impute(train_features)
```
