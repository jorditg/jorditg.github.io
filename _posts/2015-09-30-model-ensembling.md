---
published: true
title:  "On model ensembling"
date:   2015-09-30 00:00:00 +0100
author_profile: true
mathjax: false
categories:
  - Data Science
tags:
  - Ensembling
---

Model ensembling is a way to improve accuracy predictions combining different classifiers trained using different models, data, hyperparameters or parameter initializations.
Every difference introduced in the ensembling increases the diversity and improves the generalization capabilities of the ensembled model.
The drawbacks are the loss of interpretability and the increase in complexity of the evaluation of the ensembled model.

How combine classifiers:

1. Bagging, boosting, random forests
2. Model stacking, model ensembling

# Bagging and Resampling
Are used to reduce variance in mode predictions.
Bagging (**B**oostrap **Agg**regat**ing**) creates numerous repplicants of the original datasetusing random selection with replacement.
Each sampled dataset is used to construct a new model. Posteriously the models are ensembled together.

# Boosting
It takes a set (lots of) weak predictors, weight them and add them up. The combinations of them is a stronger predictor.

# Random Forests
It randomizes the selection of input variables to create a set of individual classification/regression trees and combines the predictions of them.


