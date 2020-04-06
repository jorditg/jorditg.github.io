---
published: true
title: "How many different versions of a flipped and 90 degrees rotated versions on an image exist?"
date:   2020-04-06 20:00:00 +0100
author_profile: true
mathjax: false
categories:
  - Machine learning
tags:
  - computer vision, test time augmentation, TTA
---


# Motivation

The motivation is to find the number of different versions of the same image that can be obtained from horizontally, vertically flipping and image and rotating it a multiple of 90 degrees.

# Procedure

First of all we design a piece of code to generate different versions of a random generated image. 

We choose to generate a 100x100 image of random values in each point. 

We generate 12 different versions of the original image described in the table below.

| **Tables**          |  **Original** | **Flip Left-Right**|**Flip Up-Down**|
| ------------------- |:-------------:| ------------------:|----------------| 
| **Original**        | Image 0       | Image 4            | Image 8        |
| **Rotated 90º**     | Image 1       | Image 5            | Image 9        |
| **Rotated 180º**    | Image 2       | Image 6            | Image 10       |
| **Rotated 270º**    | Image 3       | Image 7            | Image 11       |


With the code showed below, we generated such 12 different versions of the rendom image and we identify the ones that are the same. In this way, we are able to define how many different versions of the image exist using flip and rot90.

```python
import numpy as np

initial = np.random.randint(255, size=(100,100)) 
initial_r90 = np.rot90(initial, 1)
initial_r180 = np.rot90(initial, 2)
initial_r270 = np.rot90(initial, 3)

flr = np.fliplr(initial) 
flr_r90 = np.rot90(flr, 1)
flr_r180 = np.rot90(flr, 2)
flr_r270 = np.rot90(flr, 3)

fud = np.flipud(initial) 
fud_r90 = np.rot90(fud, 1)
fud_r180 = np.rot90(fud, 2)
fud_r270 = np.rot90(fud, 3)


l = [initial, initial_r90, initial_r180, initial_r270, flr, flr_r90, flr_r180, flr_r270, fud, fud_r90, fud_r180, fud_r270]

for i,val0 in enumerate(l): 
    for j,val1 in enumerate(l): 
        if i != j: 
            if np.array_equal(val0,val1): 
                print(f"Image {i} == Image {j}") 
```

The output of the code above is the next:

```
Image 4   == Image 10
Image 5   == Image 11
Image 6   == Image 8
Image 7   == Image 9
Image 8   == Image 6
Image 9   == Image 7
Image 10  == Image 4
Image 11  == Image 5

```
With this information we are able to enumerate and identify the number of different versions of the original file. 

*Eight* different versions of the image exist. One possible way of generate them is the next:

| **Tables**        | **Original**  | **Flip Left-Right** | **Flip Up-Down** |
| ----------------- |:-------------:| -------------------:|------------------| 
| **Original**      | Image 0       | Image 4             |                  |
| **Rotated 90º**   | Image 1       | Image 5             |                  |
| **Rotated 180º**  | Image 2       | Image 6             |                  |
| **Rotated 270º**  | Image 3       | Image 7             |                  |

