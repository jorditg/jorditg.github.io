---
published: true
title: "On the type of questions that Data Science tries to answer"
date:   2015-09-21 00:00:00 +0100
author_profile: true
mathjax: false
categories:
  - Data Science
tags:
  - Categories
---

Data Scientist use its analysis tools for different purposes. 

Problems can be classified in different categories according to the result that we want ot achieve:

1. **Descriptive**: In this case the goal is the description of data. Usually it is not generalizable without further analysis. 
2. **Exploratory**: Here the goal is to discover new connections. Plots are very important in these studies. Dimensionality reduction techniques are also applied for visualization of multidimensional data. In any case, it is important to remember that **correlation does not necessarily imply causation**.
3. **Inferential**: The goal here is the estimation of variables of a population using a sample of the population. The challenge in such problems is to be able to get good samples that are **representative** of the population. This is not trivial. When this is not done in the right way, important biases in the variables inferred from the study can be very relevant.
4. **Predictive**: Here the data scientist uses data of some objects to predict the behaviour of another. Keep in mind that **NOT NECESSARILY** *X predicts Y* means that *X causes Y*.
5. **Causal**: Here the Data Scientist uses randomized studies to find causation between variables.
6. **Mechanistic**: When Physical and Engineering Sciences are involved.

Remember that **Prediction is not Inference**. Both are important. 

Prediction normally is more challenging that inference.

