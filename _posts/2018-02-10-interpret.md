---
published: true
title:  "A deep learning interpretable classifier for diabetic retinopathy disease grading"
date:   2018-02-10 21:33:00 +0100
author_profile: true
mathjax: false
categories:
  - Deep Learning
tags:
  - Classification
  - Diabetic Retinopathy
  - Interpretation
---

# Introduction

In this blog entry I would like to show you a step by step sample evaluation of the classifier published in arxiv.org paper  [A Deep Learning Interpretable Classifier for Diabetic Retinopathy Disease Grading](https://arxiv.org/abs/1712.08107) and submitted for peer review to a Journal.

We show the steps for finding this last pixel explanations map:

![Input  map]({{ site.url }}/assets/images/2018-02-10-interpret/retina-animated.gif)


# The model

The model used is described in the referenced paper. It uses a 640x640 RGB retina color image for predicting the probability of having diabetic retinopathy (DR). The disease is graded in 5 different classes: class 0 meaning no apparent DR, class 1 mild non-proliferative DR (NPDR), class 2 NPDR, class 3 severe NPDR and class 4 Proliferative DR. It is a feedforward fully convolutional neural network of 17 layers. Every convolutional layer has three elements: the convolution, a batch-normalization and a ReLU activation function. All the convolutional layers use 3x3 convolution except the last one that acts as classification layer (layer 15), that uses a 2x2 convolution with no padding. Layer 16 is a linear layer and the output layer (17) is a softmax.

# Retine Image

Here below we show the retina image that we will evaluate in this sample study.

![Retina]({{ site.url }}/assets/images/2018-02-10-interpret/retina.png)

# Classification

For this image the model outputs the next scores previous to the softmax layer:

| Class | Scores |
|:-----:|:------:|
| 0     | -316.3 |
| 1     | -221.5 |
| 2     | -113.2 |
| 3     | +13.1  |
| 4     | +94.5  |

The prediction of the model is class 4.

# Generation of score maps

Now it's time to apply the score propagation algorithm explained in the paper in order to obtain the input score maps. In order to get them, we have to propagate back the output scores layer by layer. In each one, two score map tensors are generated: one that depends on the solely on the inputs and another one that is constant and does not depend on any other variable but the own properties of the proper layer. Here below we show the score maps for every layer until reaching the input space.

# Layer 16 - Last layer feature scores

The first layer after the output is the last layer feature space. It is formed by 64 nodes, each one having its own activation. Here below we present the five different feature vector scores calculated as the multiplication of the weights connecting the different output layers with the feature vectors by its activation. 

![Features C0]({{ site.url }}/assets/images/2018-02-10-interpret/features-c0.png)
![Features C1]({{ site.url }}/assets/images/2018-02-10-interpret/features-c1.png)
![Features C2]({{ site.url }}/assets/images/2018-02-10-interpret/features-c2.png)
![Features C3]({{ site.url }}/assets/images/2018-02-10-interpret/features-c3.png)
![Features C4]({{ site.url }}/assets/images/2018-02-10-interpret/features-c4.png)
 
# Going through the average pooling

Average pooling score propagation is straighforward. Just applying a weighted average over the scores, being the weights the input values, is enough to back propagate the score.

# Layer 15

This is the classification layer. In this model we used a 2x2 convolution of 64 filters with no padding and stride 1. Propagating back the scores, as explained in the paper we obtain two tensors: one independent of the layer inputs, named constant that depend only on the inherent properties of the layer, and another one input dependant. For visualization purposes only, this tensors can be summed up in order to be visualized because all of them represent part of the total score of the image. Every node of the network is encodes the information of particular receptive field that is part of the total image, having some superposition between them. The paper uses a gaussian prior for combine the nodes together and to transpost back every map to input space. Summing up the contribution of every filter and transporting back to the input space both tensors we obtain the next layer maps (first one being the input dependent and the second one the constant):

![Layer 15 feature map]({{ site.url }}/assets/images/2018-02-10-interpret/rf637.png)

![Layer 15 constant feature map]({{ site.url }}/assets/images/2018-02-10-interpret/rf637k.png)

# Layer 14

The nodes of this layer have a receptive field of 509x509 pixels. Following the same procedure we get the next feature maps:

![Layer 14 feature map]({{ site.url }}/assets/images/2018-02-10-interpret/rf509.png)

![Layer 14 constant feature map]({{ site.url }}/assets/images/2018-02-10-interpret/rf509k.png)

# Layer 13

The nodes of this layer have a receptive field of 381x381 pixels. Following the same procedure we get the next feature maps:

![Layer 13 feature map]({{ site.url }}/assets/images/2018-02-10-interpret/rf381.png)

![Layer 13 constant feature map]({{ site.url }}/assets/images/2018-02-10-interpret/rf381k.png)

# Layer 12

The nodes of this layer have a receptive field of 253x253 pixels. Following the same procedure we get the next feature maps:

![Layer 14 feature map]({{ site.url }}/assets/images/2018-02-10-interpret/rf253.png)

![Layer 14 constant feature map]({{ site.url }}/assets/images/2018-02-10-interpret/rf253k.png)

# Layer 11

The nodes of this layer have a receptive field of 189x189 pixels. Following the same procedure we get the next feature maps:

![Layer 11 feature map]({{ site.url }}/assets/images/2018-02-10-interpret/rf189.png)

![Layer 11 constant feature map]({{ site.url }}/assets/images/2018-02-10-interpret/rf189k.png)

# Layer 10

The nodes of this layer have a receptive field of 125x125 pixels. Following the same procedure we get the next feature maps:

![Layer 10 feature map]({{ site.url }}/assets/images/2018-02-10-interpret/rf125.png)

![Layer 10 constant feature map]({{ site.url }}/assets/images/2018-02-10-interpret/rf125k.png)

# Layer 9

The nodes of this layer have a receptive field of 93x93 pixels. Following the same procedure we get the next feature maps:

![Layer 9 feature map]({{ site.url }}/assets/images/2018-02-10-interpret/rf93.png)

![Layer 9 constant feature map]({{ site.url }}/assets/images/2018-02-10-interpret/rf93k.png)

# Layer 8

The nodes of this layer have a receptive field of 61x61 pixels. Following the same procedure we get the next feature maps:

![Layer 8 feature map]({{ site.url }}/assets/images/2018-02-10-interpret/rf61.png)
![Layer 8 constant feature map]({{ site.url }}/assets/images/2018-02-10-interpret/rf61k.png)

# Layer 7

The nodes of this layer have a receptive field of 45x45 pixels. Following the same procedure we get the next feature maps:

![Layer 7 feature map]({{ site.url }}/assets/images/2018-02-10-interpret/rf45.png)
![Layer 7 constant feature map]({{ site.url }}/assets/images/2018-02-10-interpret/rf45k.png)

# Layer 6

The nodes of this layer have a receptive field of 29x29 pixels. Following the same procedure we get the next feature maps:

![Layer 6 feature map]({{ site.url }}/assets/images/2018-02-10-interpret/rf29.png)
![Layer 6 constant feature map]({{ site.url }}/assets/images/2018-02-10-interpret/rf29k.png)

# Layer 5

The nodes of this layer have a receptive field of 21x21 pixels. Following the same procedure we get the next feature maps:

![Layer 5 feature map]({{ site.url }}/assets/images/2018-02-10-interpret/rf21.png)

![Layer 5 constant feature map]({{ site.url }}/assets/images/2018-02-10-interpret/rf21k.png)

# Layer 4

The nodes of this layer have a receptive field of 13x13 pixels. Following the same procedure we get the next feature maps:

![Layer 4 feature map]({{ site.url }}/assets/images/2018-02-10-interpret/rf13.png)
![Layer 4 constant feature map]({{ site.url }}/assets/images/2018-02-10-interpret/rf13k.png)

# Layer 3

The nodes of this layer have a receptive field of 9x9 pixels. Following the same procedure we get the next feature maps:

![Layer 3 feature map]({{ site.url }}/assets/images/2018-02-10-interpret/rf9.png)
![Layer 3 constant feature map]({{ site.url }}/assets/images/2018-02-10-interpret/rf9k.png)

# Layer 2

The nodes of this layer have a receptive field of 5x5 pixels. Following the same procedure we get the next feature maps:

![Layer 2 feature map]({{ site.url }}/assets/images/2018-02-10-interpret/rf5.png)
![Layer 2 constant feature map]({{ site.url }}/assets/images/2018-02-10-interpret/rf5k.png)

# Layer 1

The nodes of this layer have a receptive field of 3x3 pixels. Following the same procedure we get the next feature maps:

![Layer 1 feature map]({{ site.url }}/assets/images/2018-02-10-interpret/rf3.png)
![Layer 1 constant feature map]({{ site.url }}/assets/images/2018-02-10-interpret/rf3k.png)

# Input

Finally we reached the input space. Here we obtain 5 maps, one for each class. The final maps have two contributions: the most important one that is the one that comes from the previous layer, that is the part that depend on the inputs and the sum of all the constant contributions of each precedent layers. Summing up them we get the next input space score maps.

![Input  map]({{ site.url }}/assets/images/2018-02-10-interpret/input-total.png)


# Explanations

Considering that this image has been classified as class 4, in order to evaluate the reasons behind such a conclusion we can visualize the score maps in different ways. Fow example we can plot the pixels that have a positive contribution to the score that are above 2 standard deviations of the distribution of scores of all pixels. Here below we show the generated binary map:

![Input binary map grater than 2 stdev]({{ site.url }}/assets/images/2018-02-10-interpret/retina-big-scores-2std.png)

In this way is possible for an expert to study the pixels that the model considered more important and compare them with its own experience.

Here we show the input image with the same resolution to better identify the points:

![Retina big]({{ site.url }}/assets/images/2018-02-10-interpret/retina-big.png)

We can play generating different ways to improve the way of better understand the results. For example, combining in a unique animated GIF both images:

![Input  map]({{ site.url }}/assets/images/2018-02-10-interpret/retina-animated.gif)

# Contact

<jorditg@tinet.org>



