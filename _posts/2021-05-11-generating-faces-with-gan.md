---
layout: post
title: GANs in Keras/Tensorflow2.0
published: true
---
<img src = "https://raw.githubusercontent.com/kopalgarg/GAN-keras/main/output/train-49.png">

GANs are composed of 2 NNs: discriminator and generator. Each have a different set of inputs and outputs. 

Generator NN: useful when builiding a face generating NN. Input is a random seed [12, 2, 42, 28,...,] and the output is a random face image. Random seed is a vector (n-dimensional array). The range of seed values should be in the same range of values that were used to train the NN. 
Input: x is random seeds
Output: random faces 

Discriminator NN: discriminates between real and fake input images (3D Tensor - height, width, color), and gives a prediction values between 0 to 1 (0 = Fake image, 1 = Real image). E.g. .97 is a 97% probability that the input image is a real face.
Input: random fake faces from the generator NN output and a batch of real images from the training set (50-50)
Output: prediction/probabilities, <img src = "https://latex.codecogs.com/gif.latex?%5Chat%7By%7D">

Since its an adverserial NN, the discriminator NN and generator NN are working against each other. The generator is updating its weights with an objective of fooling the discriminator. Two interesting points: 1) the generator never sees the training set, and 2) we always have `y` =1 as we aspire for the generator NN to fool the discriminator NN into thinking the fake face images are real so we want the predictions, <img src = "https://latex.codecogs.com/gif.latex?%5Chat%7By%7D"> to be as close to 1 as possible. 

CNN is used when dealing with images, LSTM or RNNs for time-series / sequential data.

A simple implementation is found [here](https://github.com/kopalgarg/GAN-keras)

The higher the resolution of images, the more memory and training time are required. For Google Colab, 128x128 res is the highest we can use because of memory restrictions.

Training set used: [Kaggle faces data new](https://www.kaggle.com/gasgallo/faces-data-new)

The loss function should allow the generator and discriminator to be trained in an adverserial way. We require 2 separate loss functions since we are training 2 separate NNs independently in 2 separate passes. This also requires 2 separate updates to the gradients.

When one's gradients are applied to decrease its loss, only its weights should update. It won't produce good results (and it wouldn't be fair) to adversarially damage the weights of the other NN to help the first NN.

A backprop method will be used to simultaneously affect the weights of both generator and discriminator to lower the loss it was assigned to lower

Discriminator training set: `x` contains 50-50 generated (or fake) and real images. Real images are randomly sampled from the training set, and fake images are randomly generated from random seeds. Here y contains a value of `1` for real images and 0 for generated images.

Generator training set:` x` contains random seeds to generate fake images and `y` is always 1 (because we want the generator to fool the discriminator into thinking the images are real, and to output a predicted probability of 1 so we want `y` to be 1 and <img src = "https://latex.codecogs.com/gif.latex?%5Chat%7By%7D"> to be as close as possible )
