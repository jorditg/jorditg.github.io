---
published: true
title: "Cross Validation alternatives for model selection"
date:   2018-06-10 00:00:00 +0100
author_profile: true
mathjax: false
categories:
  - Machine learning
tags:
  - Cross validation
---

# Hold Out method
Splitting original training dataset using random sampling without repetition into 2 subsets. The first called *training set* is used for fitting the model/s, the secon one, called *valitation set* is used for hyper-parameter optimization and for model selection not only between hyper-parameters sets but also between different types of models. As a rule of thumb, training set use to have between 50% to 70% of the data and validation set between 50% to 30%.

# K-fold cross validation
The original training set is splitted in K folds of the same size using random sampling without repetition. The model/s are trained K times, each one of them using as training set K-1 folds and 1 (the not used one) as a validation set. Prediction error is the average of the K individual errors. Error variance can be used as a measure of the stability of the model. The advantadge of this method is that it matters less how the data is divided, ie. the model is less prone of having selection bias. After choosing the best model hyper-parameters and/or model a retrain with the whole dataset is recommended.

# Leave one out CV
It is a type of K-fold cross validation where we hold out only one sample each time. It is a good way to validate but requires a high computation time.

# Bootstrap methods
It randomly draws datasets from the original sample. Each sample size is equal to the original training size. Each model/s with its particular hyper-parameters is fitted using the bootstrapped samples. The model/s are examined with the out-of-bag data, ie. data not selected in each bootstrap.


