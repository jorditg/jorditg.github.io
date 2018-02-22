---
published: true
title: "Visualizing feature extraction disentangling"
date:   2018-02-20 00:00:00 +0100
author_profile: true
mathjax: true
categories:
  - Deep Learning
tags:
  - Classification
---

Image classification uses models based on deep learning convolutional network architectures. These parametric models are composed by a set of layers with differentiated functions. We can consider mainly two differentiated functions: *feature extraction* layers and *classification* layers. 

**Feature extraction** takes place as a first step, extracting simple localized features that are combined together building features of features each layer acting over a greater receptive field. Every layer increments the complexity of the combination between features of different locations, enhancing the disentanglement of the important features that will be in posterior layers used for classification.

**Classification** takes place using the extracted features from previous layers. In this phase, an important part of the total receptive field has been achieved and here normally a set of fully connected layers or convolutions of small size combine together the features to get even better features for solving that particular cassification task. After the last classification layer and previous to the last linear layer connecting with the output softmax layer, in an ideal classifier, the important information has been completely disentangled and that now lies in a linear manifold that allows a perfect separation between classes.

This is obviously not always the case. Limitations in the capacity of the model, having not enough training data available, havng not properly enough tagged the training data, etc. can limit the possibilities of the final classification.

Classification results can be measured with a lot of different indexes or even with a combination of different ones in order to have a quantitatively measure of the performance. But as a data scientist is also good having tools that can help visualizing more intuitively and qualitatively if the separation is taking place correctly or not in order to see f a particular classifier is wrking fine, or comparing against different classifiers to compare the strenghts os each of them. In this way is possible to detect ways of improving the results using strategies of model ensembling or to discard such models that we see are not performing well in a particuar problem.

![t-sne]({{ site.url }}/assets/images/2018-02-21-visualizing-feature-extraction-disentangling/tsne2d.png)

In the image above we present the two dimensional t-SNE visualization of the last layer features used for a 5 class image medical image classification problem. t-SNE is a stochastic non-linear way of visualizing multidimensional data. As we can see in the image we can clearly identify those classesthat are correctly separated from those one that are mixed. The visualization allows also the identification of possible misclassification cases, that can be studied (for example requesting a reevaluation) in order to identify if the missclasification is due to a model limitation or due to a tagging error. 

We identify a clear good separation between classes 0, 2 and 4. Class 1 is not well separated and is mixed with classes 0 and 2. There is some mixing between classes 2, 3 and 4, but in some way we identify the separation between them although some superposition is present. In case of class 1 clearly another type of classification and a revision of the tagged information must be addressed.
