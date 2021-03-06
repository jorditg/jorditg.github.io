---
published: true
title: "Bagging, Boosting and Decision Trees Based Predictors"
date:   2018-06-04 00:00:00 +0100
author_profile: true
mathjax: false
categories:
  - Machine learning
tags:
  - Trees
---

# Bagging vs Boosting

Error sources are noise, bias and variance. Model ensembles are a very effective way of reducing prediction errors. Bagging and Boosting are two ways of combining classifiers. They are able to convert a weak classifier into a very powerful one, just averaging multiple individual weak predictors.

## Bagging

The combination of multiple predictors decreases variance, increasing stability. Bagging uses a base learner algorithm (fe., classification trees), ie. a weak learner, for creating a pool of N weak predictors. Every predictor is generated by a different sample genereted by random sampling with replacement from the original dataset. In bagging every sample has the same probability of being chosen from the original dataset. The nature of the algorithm makes Bagging an easy paralelizable algorithm.

## Boosting

Boosting is very similar to Bagging with a significant difference: boosting uses a weighting strategy in sampling and in the combination of predictors. In Boosting the predictors generation process is sequential. Boosting increases the weights of misclassified data to emphasize the most difficult cases. Boosting also assigns weights to predictors giving more importance to best predictors. Due to this weighting strategy with predictors, Boosting is able not only to reduce variance but also to reduce bias. In counterpart, Boosting can overfit training data, problem that is not present in bagging predictors.

# Random Forest

* Uses Bagging for combining multiple decision trees, ie. weak predictors.
* This models reduce variance but not bias.
* They don't overfit.
* Uses a pool of weak learners (trees) each one of them trained using a different sampling with repetition of the original dataset. In every sample the number of samples is equal to the number of elements of the dataset. Some of them (probabilistically 1/3 of all) will be repeated samples.
* Features used for every individual predictor are also chosen by sampling.
* Classification results are calculated by mean (or majority vote) of the results given by every predictor.
* It has a missing values handling algorithm.
* It only handles numerical data. Categorical data has to be previously converted to numeric.

# GBM

* Uses boosting for combining multiple decison trees.
* These models are able to reduce not only variance but also bias.
* A potential problem is overfitting.
* Uses a pool of weak learners using a sampling with repetition of a weighted version of the original dataset. Weights are tuned every learning step, that's why the tree generation is done in a serialized way. The points more difficult to classify are those that receive higher weights, ie. its probability of being chosen from the sampling is higher.
* Features used for every individual predictor are also chosen by sampling.
* Classification results are calculated by a weighted sum of predictors. Strong predictors having higher weights than weaker ones.
* Tree construction is stopped when a tree split results in a loss of evaluation function.
* It has a missing values handling algorithm.
* It only handles numerical data. Categorical data has to be previously converted to numeric.

# XGBoost
* Boosting with overfitting control using decision trees.
* Allows L1 and L2 regularization to control overfitting
* Although tree generation is serial due to its boosting nature, it has some improvements in parallelization of some parts of the algorithm.
* Trees are completely unfolded and a posteriori pruned. In this way it avoids cases where a first split produces a loss of performance but a posteriori splits result in higher global gains.
* Allows customization of objective and evaluation functions.
* Missing values handling.
* Parameter tuning is the key for the best performance.
* Performance depends heavily on hyperparameter optimization.
* It only handles numerical data. Categorical data has to be previously converted to numeric.

# Catboost
* Categorical data managing + Bosting using decision trees.
* It can handle categorical data, taking advantadge from this fact for improving performance against other previous implementations.
* Performance not so dependant of hyperparameter optimization.
* It can perform better than XGBoost when used (and only) in combination with categorical data.
