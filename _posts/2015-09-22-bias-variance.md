---
published: true
title:  "Prediction error: bias vs variance"
date:   2015-09-22 00:00:00 +0100
author_profile: true
mathjax: false
categories:
  - Data Science
tags:
  - Bias
  - Variance
---

Sometimes prediction error sources are not well understood. 
These two important concepts are easily understood after visualizing them:

![Bias vs Variance]({{ site.url }}/assets/images/2015-09-22-bias-variance/bias_variance.png)

**Bias** is the difference between the expected average prediction and the real value.

**Variance** measures the variability of the model prediction for a given data point.

A low bias - high variance model would give predictions where its expected average is near the true value, but its individual predictions are highly dispersed around the true value.

A high bias - low variance model would give predictions far from the true value but with small variability between the predictions.

A high bias - high variance model would give predictions far from the true value and with high variability between them.

Finally a low bias - low variance model would be the best one having close to the true value predictions and with low variability between individual predictions.

