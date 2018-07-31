---
published: true
title: "Bellman Equation Derivation"
date:   2018-07-19 00:00:00 +0100
author_profile: true
mathjax: true
categories:
  - Deep Learning
tags:
  - Reinforcement Learning
---

Using math equations as magic has never been my way. For deep concept understanding, a key point is to first understand all the prior information related with the new concept that you are trying to catch.

In Reinforcement Learning, a important equation is the *Bellman Equation*. In [this video](https://www.youtube.com/watch?v=us8JoyjD0Oo) Constantin Bürgi presents a very clear derivation of the equation transforming the original *infinite horizon problem* into a *dynamic programming* one.

## Original problem 

We want to solve the next infinite horizon optimization problem:

$$ \max \sum_{t=0}^{\inf} \beta^t u(C_t) $$

under the constrain $$ k_{t+1} + C_t = (1 + r) k_t$$

being:

* $$ k_t $$ capital invested in t+1
* $$ C_t $$ capital consumption in t
* $$ k_{t+1} $$ capital invested in t
* $$ r $$ interest rate

By definition $$C_t$$ can also be expressed by $$ C_t = (1+r)k_t - k_{t+1}  $$

The infinite horizon problem, akas $$ L_0 $$ can be expressed by:

$$ \mathcal{L_0} = max \sum_{t=0}^{\inf} \beta^t u((1+r) k_t - k_{t+1}) $0

Leavind a part the first element, t=0, $$L_1$$ can be expressed as:

$$ \mathcal{L_1} = max \sum_{t=1}^{\inf} \beta^t u((1+r) k_t - k_{t+1}) $$

Now we can express $$L_0$$ as the sum of an expression plus $$L_1$$:

$$ L_0 = max( u((1+r)k_0 + k_1) + \mathcal{L_1}) $$

$$ \mathcal{L_0} $$ is a function that depends only on the value of $$k_0$$, for its part, $$ \mathcal{L_1} $$ depends
solely of $$ k_1$$.

$$ \mathcal{L(k_0)} = max ( u ((1+r)k_0 - k_1) + \beta \mathcal{L(k_1)} $$

## Bellman equation or value function

Changing the name of variables $$ V = L $$, $$ k_0 = k $$, $$ k_1 = k' $$ we obtain the expression of the Bellman Equation:

$$ V(k) = max_{k'} ( u [(1+r)k - k'] + \beta V(k'))$$
