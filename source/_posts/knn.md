---
title: KNN学习
---



# KNN

自己写代码实现一个最简单的knn算法，不使用机器学习库。

## knn概述

&#8195;k-近邻算法是一种基本分类与回归方法；它是是监督学习中分类方法的一种，属于懒散学习法（惰性学习方法）。

&#8195;给定一个训练集D和一个测试对象z,该测试对象是一个由属性值和一个未知的类别标签组成的向量，该算法需要计算z和每个训练对象之间的距离（或相似度），这样就可以确定最近邻的列表。然后将最近邻中实例数量占优的类别赋给z。（主要思想是如果一个样本在特征空间中的k个最近的样本中的大多数都属于某个类别，则该样本属于这个类别，并具有这个类别上的特性 ）。

## 代码实现
```python
import sklearn
from sklearn.neighbors import KNeighborsClassifier
import numpy as np
import matplotlib.pyplot as plt
from math import sqrt

#模拟数据
X_raw = [[14.23,5.64],
         [13.2,4.38],
        [13.16,5.68],
        [14.37,4.80],
        [13.24,4.32],
        [12.07,2.76],
        [12.43,3.94],
        [11.79,3.  ],
        [12.37,2.12],
         [12.04,2.6]]
y_raw = [0,0,0,0,0,1,1,1,1,1] 
x_test = np.array([13.8,4.1])
X_train = np.array(X_raw)
y_train = np.array(y_raw)

#绘制图像
plt.style.use('ggplot')
plt.figure(figsize=(10,6))
X_0, X_1 = X_train[y_train == 0], X_train[y_train == 1]
plt.scatter(X_0[:,0],X_0[:,1],color="r")
plt.scatter(X_1[:,0],X_1[:,1],color="b")
plt.scatter(x_test[0],x_test[1],color="g")

```

![20190620162916272_10651](/knn/20190620162916272_10651.png)

&#8195;&#8195;红色的为标记为0的数据集；蓝色的为标记为1的数据集，绿色的为测试点。

```python

distance = [sqrt(np.sum((x - x_test)**2))for x in X_train]
sort = np.argsort(distance)
K = 3
#找到距离测试点最近的K个点，并打印他们的类型
topK = [y_train[i] for i in sort[:K]]
print("topK:",topK)
from collections import Counter
votes = Counter(topK)
print("answer:",votes.most_common(1)[0][0])

```

&#8195;可以得到结果 topK: [0, 0, 0] &#8195;answer: 0
&#8195;从图中我们可以清楚的看到测试点应该为红色类型，也就是属于标记为0的类别，与我们的结果相符合。

&#8195;我们也可以使用sklearn中的函数实现一下，比较一下结果：
```python
kNN_classifier=KNeighborsClassifier(n_neighbors=3)
kNN_classifier.fit(X_train,y_train)
x_test = x_test.reshape(1,-1)
print(kNN_classifier.predict(x_test)[0])
```
&#8195;可以看到结果是0。