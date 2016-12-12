---
layout: post
title: "Notes on Coding Neural Networks"
modified: 2016-11-8
categories: blog
excerpt:
tags: []
date: 2016-11-8
---

### Existing Neural Network Libraries
There're many brilliant open source libraries for neural networks and deep learning. Some of them try to wrap every function they provide into an uniform interface (e.g. caffe and tensorflow), such well encapsulated libraries might be easy to use but difficult to change. As the rapid development of deep learning, it is a common need for people in the field to experiment new ideas beyond those encapsulated interfaces, and I often find that the very interface I need is just the source code.

[Keras](https://github.com/fchollet/keras) does a great job on that, as stated as one of their guiding principles, it was developed with a focus on enabling fast experimentation. *Being able to go from idea to result with the least possible delay is key to doing good research.* Before I found keras, I wrote a library myself for such purpose, followings are some implementation notes. It mostly talks about feedforward neural networks (FFNNs), but the idea should be applicable to recurrent networks as well.

### Same Network for Training and Test?
Is the same network used for both training and test? If it were in the last century, the answer might be yes. But no. 
For instance, recently developed layers such as batch normalization behave differently at training and test time, and sometimes people only need some intermediate result as feature representations for other tasks at test time. 
Here're a few examples of different architectures in training and test, [Deep Learning Face Attributes in the Wild](http://www.cv-foundation.org/openaccess/content_iccv_2015/papers/Liu_Deep_Learning_Face_ICCV_2015_paper.pdf), [FractalNet: Ultra-Deep Neural Networks without Residuals](https://arxiv.org/abs/1605.07648), [Auto-Encoding Variational Bayes](https://arxiv.org/abs/1312.6114).

So layer behaviors can be different, network architectures can be different, 
the only thing that connects training and test is (a subset of) the parameters. 
In terms of coding, we totally should decouple the training and test networks as two different functions,
that is to say, the training specifies how to search for the parameters, the test specifies how to use the parameters.

### Implementing a Neural Network Library
The neural network library I wrote follows the following key points, hopefully it would help sorting out the related concepts in terms of implementation.  

- The notion of a network breaks down into two types of functions, one is for optimizing an objective function w.r.t some parameters through an optimizer (training), the other computes the output for some input given the parameters (test).
- A function is defined by stacking up layers.
- A layer can have its parameter, input and output, it may behave differently for training, test or else. 
- Parameters can be shared between layers and functions.

### Variational Autoencoder Example

![samples generated](https://raw.githubusercontent.com/dontloo/dontloo.github.io/master/images/vae.png)

Here are some code snippets of implementing a variational autoencoder using my own library, hopefully it would illustrate how the it works in more detail.

```python
# preparing data
im_pro_fn = intnet.data.get_im_pro_fn(color_space="L", scale=True, flatten=True)  # load image as grayscale
train_ds = intnet.data.CategoricalData(train_lst, "lazy", process_data_fn=im_pro_fn, x_dtype=floatX)
test_ds = intnet.data.CategoricalData(test_lst, "lazy", process_data_fn=im_pro_fn, x_dtype=floatX)

# encoder
l_x = lay.Input((batch_sze, row*column), floatX)
l_h = lay.Activation(lay.FullyConnected(l_x, 256), "relu")
l_z_mean = lay.FullyConnected(l_h, 2)
l_z_log_var = lay.FullyConnected(l_h, 2)
# sampling
l_z = lay.GaussSample(l_z_mean, l_z_log_var)
# decoder
l_h_dec = lay.Activation(lay.FullyConnected(l_z, 256), "relu")
l_x_dec = lay.Activation(lay.FullyConnected(l_h_dec, row*column), "sigmoid")
# loss
l_xent = lay.BinaryXent(l_x_dec, l_x)
l_kl = lay.KL(l_z_mean, l_z_log_var)
l_loss = lay.Merge([l_xent, l_kl], "sum")

# an ffnn for training is essentially a function to be optimized, defined by the loss and related layers
net = intnet.ffnn.FFNNOptimize(l_loss)
# an optimizer instance has its own (shared) parameters that need to be updated every iteration
lr = intnet.com.AdaptParam('linear', 2e-3, 2e-5)
momentum = intnet.com.AdaptParam('fixed', 0.9)
opt = intnet.optimize.get_optimizer("adam", lr, momentum)
# compile the function
train_fn = net.opt_fn([l_x], [l_loss, l_xent, l_kl], opt)

# initialize
net.init_param("Glorot_heuristic")
# train
train_steps = 3e4
for i, x, y in intnet.data.EpochBatchLauncher(train_ds, batch_sze, train_steps, shuffle=True):  # launch the data 
    opt.update_learning_params(i, train_steps)  # update the parameters of the optimizer
    loss, xent, kl = train_fn(x)
    if (i + 1)%100 == 0:
        print("Iter %d: Loss %g" % (i + 1, loss)), xent, kl

# decoder network only
l_z_in = lay.Input((None, 2), floatX)
l_h_dec.pred.pred = l_z_in
decoder_fn = intnet.ffnn.ffnn_fn(l_z_in, l_x_dec)

# generate points in the latent space
grid_num = 15
grids = norm.ppf(np.linspace(0.04, 0.96, grid_num))
points = np.zeros((grid_num ** 2, 2), dtype=floatX)
for x in range(grid_num):
    for y in range(grid_num):
        points[x * grid_num + y, :] = [grids[x], grids[y]]
# decode
x_gen = decoder_fn(points)
# plot
big_im = np.zeros((row * grid_num, column * grid_num))
for x in range(grid_num):
    for y in range(grid_num):
        big_im[x*row:(x+1)*row, y*column:(y+1)*column] = x_gen[x * grid_num + y].reshape(row, column)
plt.imshow(big_im, cmap='Greys_r')
plt.axis('off')
plt.show()
```
