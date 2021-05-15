---
layout: article
title: 听起来像回归算法的逻辑斯特回归(Logistic Regression)
tags: Logistic-Regression 《机器学习》周志华
mathjax: true
key: 2020-08-20-logistic-regression
---

首先，要明确的一点就是Logistic Regression是**分！类！算！法！**。这个一定要记住，它就是很特殊的存在。

### 引出

使用线性模型进行回归学习这一方面，相信大家应该有一个比较清晰的概念，这里就不赘述了。但是，如何将线性模型应用在**分类**问题上呢？

$$ y = g^{-1}(\omega^Tx + b) $$

答案就蕴含在”广义线性模型“中，即公式(1)，其中函数$$g(\cdot)$$代表“联系函数”（单调可微）。严谨而言，就是寻找一个单调可谓函数$$g$$将分类任务的真实标记$$y$$与线性回归模型的预测值联系起来。

我们该怎么将它们联系在一起呢？首先，我们知道线性回归模型的预测值为$$z = \omega^Tx + b$$，而对于二分类任务而言，其对应的分类结果为$$y \in \{0, 1\}$$。所以，就可以使用很常用的“单位阶跃函数”来将预测值$$z$$转换为$$0/1$$值，如公式(2)所示。

$$
\begin{equation}
y = 
\left\{
        \begin{array}{lr}
        0, & z < 0 \\
        0.5, & z = 0\\
        1, &  z > 0 
        \end{array}
\right.
\end{equation}
$$

但是，请注意一点：单位阶跃函数并不连续，所以不能拿来直接用。因此，我们将视角转向了一个与阶跃函数近似且保持了连续性、单调可微的一种Sigmoid函数——**对数几率函数**（logistic function）。

$$
\begin {split}
y &= {1 \over 1 + e^{-z}} \\
  &= {1 \over 1 + e^{-\omega^Tx + b}}
\end {split}
$$


### 解构对数几率函数

本部分的内容，主要是来源于周志华教授的《机器学习》上的关于这一内容的章节。但是我用自己的视角对其进行阐述，便于理解。

对数几率函数，又可以称为逻辑斯特函数，是我们用来解决分类任务的模型。所以这里采用分类的角度对模型进行解读。

首先，我们可以通过简单的变换将对数几率函数转化为以下这种形式：

$$\ln {y \over 1 - y} = \omega^Tx + b$$

若将$$y$$视为样本$$x$$为正例的概率，则$$1-y$$代表$$x$$为负例的概率。所以在此基础上，将$$y \over 1-y$$定义为**几率**（odds），也就是就是$$x$$有多大的相对概率是作为正例存在的。对几率取对数得出的结果是对数几率$$\ln {y \over 1-y}$$。

这也就是对数几率函数名字的由来，整个过程就是**通过线性回归模型的预测结果来逼近真实标记的对数几率**。

这种方法共有三个优点：

- 直接对分类可能性进行建模，无需事先假设数据分布（避免假设分布不准确所带来的问题）；
- 不仅能够预测“类别”，也可以得到近似概率预测（对许多需利用概率辅助决策的任务很有用）；
- 求解的目标函数是任意阶可导的凸函数，现有的许多数值优化算法都可直接用于求取最优解。

<!-- ### 求解

$$ y = {1 \over 1 + e^{-\omega^Tx + b}} $$

这个公式中已知的变量是$$x$$（输入样本）、$$y$$（真实的输出标记） -->



