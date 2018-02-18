---
published: true
title: "Prior & Posterior: two concepts not always well understood"
date:   2018-02-18 00:00:00 +0100
author_profile: true
mathjax: true
categories:
  - Bayesian Statistics
tags:
  - Probability
  - Prior
  - Posterior
---

Intuitions are the best way to get into the concepts, also in math. Prior and Posterior are two commonly used concepts in Bayesian Statistics. For the profan sometimes the specialized jargon can be confusing. This was my case until I found the equation that connected them. The two concepts are just another way to name two of the elements of the **Bayes Theorem**:

$$
P(X \mid Y) = \frac{P(Y \mid X) P(X)}{P(Y)}
$$

being:

* $$ P(Y \mid X) $$ the **Likelihood**
* $$ P(Y) $$ the **Evidence**
* $$ P(X \mid Y) $$ the **Posterior**
* $$ P(X) $$ the **Prior**

If X and Y events are related, i.e., they are not independent, knowing about one of both events changes the probability occurrence of the other.

The **Prior**, $$ P(X) $$, refers to the probability of event X before knowing about Y.
The **Posterior**, $$ P(X \mid Y) $$, refers to the probability of event X after knowing about Y. 

