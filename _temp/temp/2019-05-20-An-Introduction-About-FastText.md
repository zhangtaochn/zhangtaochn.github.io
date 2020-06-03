---
layout:     post
title:      "Data Classification based on SVM"
subtitle:   "Kernel function for nonlinear classification"
date:       2018-12-19 15:05:34
author:     "ZHANG Tao"
header-img: "img/smote.png"
tags:
- python
- svm
- nolinear
- kernel function
- machine learning
- data classification
---

<script type="text/javascript" async src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML"> </script>

### Introduction:

In machine learning, support vector machines (SVMs, also support vector networks[1]) are supervised learning models with associated learning algorithms that analyze data used for classification and regression analysis. Given a set of training examples, each marked as belonging to one or the other of two categories, an SVM training algorithm builds a model that assigns new examples to one category or the other, making it a non-probabilistic binary linear classifier (although methods such as Platt scaling exist to use SVM in a probabilistic classification setting). An SVM model is a representation of the examples as points in space, mapped so that the examples of the separate categories are divided by a clear gap that is as wide as possible. New examples are then mapped into that same space and predicted to belong to a category based on which side of the gap they fall.

Linear SVM:

We consider our training set to be

$$ D=(x_i, Y_i)  x\in R_d, y\in\{-1, 1\} $$

The key idea is that we seek to find a hyperplane ww separating our data - and maximimize the *margin* of this hyperplane to optimize decision-theoretic metrics.

Let κκ be a kernel function on  $$K$$ with $$ K_{ij} = \kappa(x_i, x_j) $$ is positive semidefinite. A key property of such kernel functions is that there exists a map νν such that $$(\nu(x), \nu(y)) = \kappa(x, y)$$. One can think of νν as mapping our input features into a higher dimensional output space.

We can show that for a given feature mapping νν satisfying the previous condition, the Lagrangian for the problem of finding the maximum margin hyperplane takes the form:

$$ \inf _ { z \in \mathbb { R } ^ { n } } \frac { 1 } { 2 } \left| \sum _ { i = 1 } ^ { n } y _ { i } \nu \left( x _ { i } \right) z _ { i } \right| _ { 2 } ^ { 2 } - e ^ { T } z $$

Given a resulting vector of Lagrange multipliers zz, we find that most zz are zero. This comes from the complementary slackness conditions in our optimization problem - either  $$ (x_i, y_i)$$  is on the maximum margin (and so corresponding Lagrange multiplier is nonzero), or it is not on the margin (and so the Lagrange multiplier is zero).

The prediction of a given feature vector xx takes the form

$$ (\omega, \nu(x)) = \sum_{i=1}^{n}z_iy_i(\nu(x_i), \nu_i)  = \sum_{i=i}^{n}z_iy_i\kappa(x_i, x) $$ where we can take the sum over only the non-zero $$ Z_i $$ .This yields a very efficient prediction algorithm - once we have trained our SVM, a large amount of the training data (those samples with zero Lagrangian multipliers) can be removed.

There are more complications (handling the bias term, handling non-separable datasets), but this is the gist of the algorithm.

### Experiment:



### Result:

![img](/img/post-svm/result1.png)

<center>result</center>

![img](/img/post-svm/result2.png)

<center>result</center>

![img](/img/post-svm/result3.png)

<center>concentric_circles</center>

![img](/img/post-svm/result4.png)

<center>concentric_circles result</center>