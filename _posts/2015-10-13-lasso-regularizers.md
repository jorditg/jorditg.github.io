---
layout: post
title:  "On Lasso model regularization"
date:   2015-10-13 00:00:00 +0100
categories: data_science
---

Lasso regularization is also known as L1-regularization. This regularizer is more aggresive that the more usual L2-regularizer.
Those parameters that are not important for the prediction are easily set to zero with this regularizer. 
Sometimes is important to find a equilibrated solution between simplicity and performance. 
In such cases normally is a good idea to first fit a complex model and afterwards use a Lasso regularizer to reduce the complexity and only get the important parameters.

