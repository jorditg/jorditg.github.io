---
published: true
title:  "Covariate shift in Machine Learning inference"
date:   2018-03-09 00:00:00 +0100
author_profile: true
mathjax: false
categories:
  - Machine learning
tags:
  - Covariate shift
---

Machine Learning paradigm gives computer systems the ability to learn from data. These algorithms allow the identification of the more relevant features present in data and the way of combining them to maximize the performance in a particular classification or regression problem. Identifying such a set of important features allow the generalization of the prediction capabilities of designed models. *Feature vectors* are also known as *covariates* in statistical jargon. That's why *covariate shift* could be expressed as *feature vector shift* in machine learning jargon.

Model design in Machine Learning is done using a data set that is splitted in two main parts: a *train set* and a *test set*. Many details could be described in this point, but for the purposes of this entry blog the important point here is that, due to the way of choosing the sets (random selection) we assure that both sets come from the same population and share the same probability distribution.

After the training process we usually want to use the model for inference over different data. This step is not always done in the right way. New data, can share a priori most of the properties of the data used in training, but also it could have distinctive properties not present in the original data that could influence on the classification. Therefore, before applying inference over this new data it is important to check for the existance of distinctive elements affecting the classification/regression performance. If this happen, we say that there is *covariate shift*. Detecting or discarding covariate shift is critical when using models from prediction in similar but different populations.

# Covariate shift detection

## Probability distribution distance testing

One way of testing for the absence of covariate shift is supposing that training and inference populations are different and calculate the distance between both distributions. *Kullback-Leibler divergence* is a way for computing the distance between two distributions. A threshold is defined and the distance is computed using a sample based approximation. In case of being the distance greater than the threshold, covariate shift is present. In case of being the distance lower than the threshold covariate shift can be discarded.

## Non-randomness testing

Another way of detection is testing for the presence of non-randomness on the data. In case that both samples belong to the same distribution, no presence of differences in the data belonging to the same classes should be detected. In case both samples belong to different populations some kind of differentiative structure in the data can be detected. One test used extensively for this purpose is the *Wald-Wolfowitz test*.

## Graphical methods

Dimensionality reduction techniques allow the visualization of high dimensional feature vectors in two dimensional spaces. Visualization in the reduced space allow the qualitative evaluation of differences between both populations if they exist. Manifold Learning techniques (eg: IsoMap, MDS, t-SNE, etc.) are not simple linear projections, allowing different and more powerful results than standard PCA. 
