---
published: true
title:  "Relationship between Mutual Information and Kullback-Leibler divergence "
date:   2017-02-22 00:00:00 +0100
author_profile: true
mathjax: true
categories:
  - Information Theory
tags:
  - Mutual Information
  - KL divergence
---


Mutual information between two random variables $$X$$ and $$Y$$ can be expressed mathematically (by definition) as the Kullback-Leibler divergence between the joint distribution of both variables $$P(X,Y)$$ and the distribution $$P(X)·P(Y)$$.

$$I(X,Y) = KL(P(X,Y) | P(X)·P(Y))$$

Mutual information definition is written normally as a function of the entropy $$I(X,Y) = H(X) - H(X|Y)$$ but I find more intuitive the first formulation. One can be derived from the other just by mathematical manipulation.
In the case where both variables are independent, $$P(X,Y)$$ is equal to $$P(X)P(Y)$$ and the KL divergence between both distributions is 0. 
Intuitively we can say that knowing about one variable gives no information about the other.
In the case where both variables are not independent,  knowing about one of  the variables gives information about the other. 
In this case $$P(X,Y)$$ and $$P(X)·P(Y)$$ will differ and the mutual information would be different from zero.

