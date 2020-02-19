---
title: kmeans
date: 2019-07-02 16:38:51
description: 使用sklearn的kmeans对iris数据集进行分类。
---



# Kmeans

说明：这里使用sklearn的kmeans对iris数据集进行分类。

## Kmeans概括

​	k均值聚类算法（k-means clustering algorithm）是一种迭代求解的[聚类分析](https://baike.baidu.com/item/聚类分析/3450227)算法，其步骤是随机选取K个对象作为初始的聚类中心，然后计算每个对象与各个种子聚类中心之间的距离，把每个对象分配给距离它最近的聚类中心。聚类中心以及分配给它们的对象就代表一个聚类。每分配一个样本，聚类的聚类中心会根据聚类中现有的对象被重新计算。这个过程将不断重复直到满足某个终止条件。终止条件可以是没有（或最小数目）对象被重新分配给不同的聚类，没有（或最小数目）聚类中心再发生变化，误差平方和局部最小。

## 练习

> ```python
> from sklearn import datasets
> from sklearn.cluster import KMeans
> from sklearn.preprocessing import Normalizer
> import matplotlib.pyplot as plt
> 
> iris = datasets.load_iris()
> #归一化数据
> iris.data = Normalizer().fit_transform(iris.data)
> 
> X = iris.data[:,[0,3]]
> Y = iris.target
> 
> '''plt.scatter(X[Y==0,0],X[Y==0,1],color = "r")
> plt.scatter(X[Y==1,0],X[Y==1,1],color = "b")
> plt.scatter(X[Y==2,0],X[Y==2,1],color = "y")
> '''
> figure1 = plt.figure()
> plt.scatter(X[:,0],X[:,1],c=Y)#c的作用是对Y中不同的数字用不用的颜色标记，和上面的注释效果相同
> 
> #我们已知了为三类不同的花瓣
> model = KMeans(n_clusters = 3)
> model.fit(iris.data)
> Y_ = model.predict(iris.data)
> 
> figure2 = plt.figure()
> plt.scatter(X[:,0],X[:,1],c=Y_)
> plt.title("predict")
> ```
>
> ![1562057195839](http://q5xxri682.bkt.clouddn.com/1562057195839.png)
>
> 这是使用原始数据绘制的散点图，不同类型的花使用不同类型的点进行标记。下面绘制使用kmeans聚类算法计算出来的族。
>
> ![1562057369139](http://q5xxri682.bkt.clouddn.com/1562057369139.png)
>
> ​	从结果的绘制图形看来，在这里使用kmeans算法的准确度还是蛮高的。