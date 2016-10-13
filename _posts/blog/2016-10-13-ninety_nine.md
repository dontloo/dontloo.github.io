---
layout: post
title: "Recipe for 99%+ Accuracy Face Recognition"
modified:
categories: blog
excerpt:
tags: []
date: 2016-10-13
modified: 2016-10-13
---

### Intro
The title is exaggerated, actually by "99%+ accuracy face recognition" I mean "99+% accuracy on the LFW (Labeled Faces in the Wild) dataset". 
This recipe contains every big idea you need to know to reproduce the results, and it depends on public data sets only.

### Preliminaries
We'll use two publicly avaiable data sets for training [CASIA WebFace](http://www.cbsr.ia.ac.cn/english/CASIA-WebFace-Database.html) 
and [MS-Celeb-1M](https://www.microsoft.com/en-us/research/project/ms-celeb-1m-challenge-recognizing-one-million-celebrities-real-world/). 
We'll need a face detector, a face aligner and a deep learning library, there are many open source projects of those online.

### Method
CASIA WebFace contains 500k images of 10k people, the data set is relatively clean. 
With CASIA WebFace data only we can train a network that has about 97%+ accuracy on LFW, as reported in their paper. 
Actually if add some recent techniques (batch normalization, the residual architecture, image augmentation, ADAM) to their network, the performance can be raised up to 98%+.

MS-Celeb-1M contains of 10m images of 100k people, which is rather noisy that I believe is not suitable for training directly. 
But there's a trait of the data set that we can take advantage of, which is, a proportion of these 100k people are rather clean, only we don't know exactly who they are.

With the 98%+ network trained on CASIA WebFace we can do something to clean the MS-Celeb-1M data set.  

- Extracted the features of all the images using the network. 
- Choose a measure to estimate the discrepancy of the images under the same person based on the features (e.g. the trace of the covariance matrix). 
- Sort the 100k people people by this measure, and the first quarter (or 30k) of the list should be relatively clean.
- Keep the (about 3m) images of these 30k people for training and discard the rest.

Following same network architecture, we can get a 98.5%+ network with the 3m images. 
Combining the results of the networks trained on the two data sets will give 99%+ accuracy on LFW.  

### Notes
- Use both aligned and unaligned images for training.
- Test time augmentation: original + flipped.
- I used the aligned LFW images provided by CASIA WebFace for validation, so I gave the CASIA WebFace network a higher weight (1.3) when combining models.
- I didn't merge the two training sets into one becuase there are many overlaps.
- The actual process may not be so easy as it sounds in this blog.


