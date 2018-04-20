---
published: true
title: "Summary of the most successful Imagenet prediction standardized architectures"
date:   2018-04-20 00:00:00 +0100
author_profile: true
mathjax: false
categories:
  - Deep Learning
tags:
  - Classification, ImageNet
---

Table below shows a summary of the most successful Imagenet prediction standardized architectures sorted by its performance 
for the Imagenet classification task. The more successful network is InceptionResNetV2 but at the cost of having more than
55 million of parameters. Xception has a similar accuracy using less than a half of parameters. MobileNetV2, an architecture
desinged to be used in mobile devices, with nly 3.4 million of parameters has an accuracy similar to the achived with older
architectures as VGG16 and VGG19 that used more than 100 million of parameters.

| Model             | Input size  | Imagenet Top-1 Accuracy | Parameters | Depth | Residual | Publication | Source    | 
|-------------------|-------------|-------------------------|------------|-------|----------|-------------|-----------| 
| InceptionResNetV2 | (299,299,3) | 0,804                   | 55.9M      | 572   | Yes      | 2016-02     | Google    | 
| InceptionV4       | (299,299,3) | 0,802                   | 55.9M      |       | No       | 2016-02     | Google    | 
| Xception          | (299,299,3) | 0,790                   | 22.9M      | 126   | Yes      | 2016-10     | Google    | 
| InceptionV3       | (299,299,3) | 0,788                   | 23.8M      | 159   | No       | 2015-12     | Google    | 
| DenseNet201       | (224,224,3) | 0,770                   | 20.2M      | 201   | Dense    | 2016-08     | Facebook  | 
| ResNet50          | (224,224,3) | 0,759                   | 25.6M      | 168   | Yes      | 2015-12     | Microsoft | 
| DenseNet169       | (224,224,3) | 0,759                   | 14.3M      | 169   | Dense    | 2016-08     | Facebook  | 
| MobileNetV2 (1.4) | (224,224,3) | 0,747                   | 6.9M       |       | Yes      | 2018-01     | Google    | 
| DenseNet121       | (224,224,3) | 0,745                   | 8M         | 121   | Dense    | 2016-08     | Facebook  | 
| VGG19             | (224,224,3) | 0,727                   | 143.7M     | 26    | No       | 2014-09     | Oxford    | 
| MobileNetV2       | (224,224,3) | 0,720                   | 3.4M       |       | Yes      | 2018-01     | Google    | 
| VGG16             | (224,224,3) | 0,715                   | 138.3M     | 23    | No       | 2014-09     | Oxford    | 
| MobileNetV1       | (224,224,3) | 0,706                   | 4.2M       |       | Yes      | 2017-06     | Google    | 
| SqueezeNet        | (227,227,3) | 0,575                   | 1.2M       |       | Yes      | 2016-02     | DeepScale | 
| AlexNet           | (227,227,3) | 0,571                   | 62M        | 8     | No       | 2012-00     | BVLC      | 

This table can be used for comparing against the different architectures. It can help in the decision process of choosing
between the different pretrained networks for transfer learning tasks.
