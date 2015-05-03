# 龙星-机器学习笔记

## 介绍

什么是机器学习？允许计算机在经验知识的基础上不断演化进步的算法。

- 计算机视觉
- 语音识别
- 自然语言处理
- 搜索
- 推荐
- 其它
	- 无人驾驶
	- 问题回答

机器学习的类型

- 有监督学习：给定$\{x_i,y_i\}$，学习$y=f(x;\theta)$
	- classification
	- regression
	- ranking
	- structured prediction
- 无监督学习：给定$\{x_i\}$，学习$y=f(x;\theta)$
	- clustering

ML的是三个要素：data、model、algorithm

## 线性模型

线性回归模型的统计描述：$Y=\beta_0+\beta_1X+\epsilon$

- 如何估计$\beta_0$和$\beta_1$
- 如何评价模型
- $\beta_0$和$\beta_1$哪个更重要

线性回归模型基础

- 给定$(X_i, Y_i)$，学习$\beta_0$和$\beta_1$，$\如何评价模型
- $\beta_0$epsilon$是噪音
- 定义残差$r_i=Y_i-(\beta_0+\beta_1X)$，目标是要达到最小的残差，即最小化损失函数 $\min\sum\limits_{i=1}^nL(r_i)$
- 常用的损失函数是$L(r_i)=r_i^2$，称为线性最小二乘回归 $[\hat\beta_0,\hat\beta_1]=\arg\min\limits_{\beta_0,\beta_1}\sum\limits_{i=1}^n(Y_i-(\beta_0+\beta_1X_i))^2$
- $\epsilon$必须是均值为0的噪声，因为若均值不为0，那么模型必然可以改进，比如修改$\beta_0$
- 理想的噪声是均值为0的高斯分布
- 最小二乘回归对孤立点很敏感
- 残差$r_i$应该看起来随机，如果不随机，模型需要改进，比如添加非线性特征
- 如果$\epsilon_i$相比高斯分布更加[重尾](http://en.wikipedia.org/wiki/Heavy-tailed_distribution)，那么模型不鲁棒

泛化的线性模型

- 对于模型非线性函数$f_j(X_i)$，泛化的线性模型可以表示为$Y_i=\beta_0+\sum_{j=1}\beta_jf_j(X_i)+\epsilon_i$
- 仍然是一个线性模型，只是使用了非线性的特征，但是对于参数$\beta_j$仍然是线性的
- 只要模型对参数来说仍然是线性的，就可以用线性的学习方法来学习模型
- 通用的线性最小二乘回归：$Y_i=\beta^TX_i+\epsilon_i$
	- 最小化RSS(residue sum-of-squares)
	- 代数解为$\hat\beta=(X^TX)^{-1}X^TY$
	- `似然*先验=后验*事实`

噪声

- 残差是否具有相同的方差
	- 以样本值为X轴，残差为Y轴，看残差是否与样本值无关
	- [Using Plots to Check Model Assumptions](http://www.ma.utexas.edu/users/mks/statmistakes/modelcheckingplots.html) 
- 残差是否满足高斯分布
	- 根据中心极限定理，大量独立的随机变量均值满足正态分布
- 均匀残差的处理
    - 基于[无偏估计](http://en.wikipedia.org/wiki/Unbiased_estimation_of_standard_deviation)，噪声的均方差与残差的关系：$\hat\sigma^2=\frac 1 {n-p}\sum_{i=1}^nr_i^2$，其中$p$是参数的个数
    - 残差比噪声的方差小
    - 模型的参数越多，同样的残差下，模型的噪声均方差越大
    - 同样的数据能够提供的信息是有限的，模型的参数越多，生成模型后从模型得到的信息就越少
    - 过拟合是因为把噪声当成数据学习
- 非均匀残差的处理

Variable Importance