---
published: true
title:  "On Lasso model regularization"
date:   2015-10-13 00:00:00 +0100
author_profile: true
mathjax: true
categories:
  - Data Science
tags:
  - Regularization
---

Lasso regularization is also known as L1-regularization. This regularizer is more aggresive that the more usual L2-regularizer also known as Rigde regularization. 

Both methods are derived from adding to the chosen cost function an additional term, that penalizes the parameter values, forcing them to be as small as possible.

In Ridge regression the original cost function $$ \mathcal{C_{orig}} $$ is modified according to the next equation: 
$$ \mathcal{C_{reg}} = \mathcal{C_{orig}} + \lambda \sum_{i=1}^N \omega_i^2 $$


In Lasso regression the original cost function becomes:
$$ \mathcal{C_{reg}} = \mathcal{C_{orig}} + \lambda \sum_{i=1}^N \mid \omega_i \mid $$

The main characteristic of Lasso is that the parameters that are not important for the prediction are set to zero by the optimizer. The main difference with Ridge is that this last one, due to the fact that squaring a lower than 1 parameter makes it smaller, have a milder effect in removing superflous parameters.

Sometimes is important to find a equilibrated solution between simplicity and performance. 
In such cases normally is a good idea to first fit a complex model and afterwards use a Lasso regularizer to reduce the complexity and get only the important parameters.

