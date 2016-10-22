---
layout: post
title: "Notes on Joint Bayesian Verification"
modified:
categories: blog
excerpt:
tags: []
date: 2015-12-21
modified: 2015-12-21
---

The following gives the detailed derivatation of the formulars in the paper 
[Bayesian Face Revisited: A Joint Formulation](https://www.microsoft.com/en-us/research/publication/bayesian-face-revisited-a-joint-formulation/).

###Eq.4
\\[r(x_1,x_2)=\log\frac{p(x_1,x_2|H_I)}{p(x_1,x_2|H_E)}=x_1^TAx_1+x_2^TAx_2-2x_1^TGx_2\\]
where
\\[A=(S_\mu+S_\epsilon)^{-1}-(F+G)\\]
