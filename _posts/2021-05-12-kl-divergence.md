---
layout: post
title: An Intro to Kullback-Leibler and Jensen-Shannon Divergence
published: true
---

KL divergence is used to measure the **divergence** between two probability distributions of a random variable. Divergence is the distance between two probability distributions on a statistical manifold. Divergence is not symmetric (divergence from probability distribution q to p <img src = "https://latex.codecogs.com/gif.latex?%5Cneq"> that from p to q) and need not satisfy the triangle inequality (sum of length of 2 sides of a triange >= other side) [[1]](https://en.wikipedia.org/wiki/Divergence_(statistics)). 

The entropy for a probability distribution is:

<img src = "https://latex.codecogs.com/gif.latex?H%20%3D%20-%5Csum_%7Bi%3D1%7D%5E%7BN%7D%20p%28x_i%29%5Ccdot%20log%20p%28x_i%29">

Entropy tells us the minimum number of bits it would take for us to encode a the information in a dataset. It gives us the lower bound of # bits (using log base-2 for bits, or log base-e for nats) needed to encode a given distribution. KL divergence is used to quantify how much information is lost when we use a parametrised distribution as a substitution to our original distribution of values [[2]](https://www.countbayesie.com/blog/2017/5/9/kullback-leibler-divergence-explained). The KL divergence between two probability distributions q and p is presented with the following notation:

<img src ="https://latex.codecogs.com/gif.latex?KL%28p%5Cleft%20%7C%20%5Cright%20%7Cq%29%20%3D%20%5Csum_%7Bi%3D1%7D%5E%7BN%7D%20p%28x_i%29%5Ccdot%20log%20%5Cfrac%7Bq%28x_i%29%7D%7Bp%28x_i%29%7D">

When P(q) is large, and P(p) is small, there is a large divergence. When the P(p) is large and P(q) is small, the divergence is relatively smaller. When both distributions are identical, the score is 0 and when they differ, the score is >0.

This can be used for discrete and continuous distributions (integral would be used instead of the sum of probabilities).

Jensen-Shannon Divergence:

When using the base-2 log, JS divergence provides a smoothed and normalized version of KL divergence. It results in scores between 0 and 1, where a score of 0 means the two distributions are identical, and a score closer to 0 means the distributions are different. It is calculated as follows:

<img src="https://latex.codecogs.com/gif.latex?JS%28p%5Cleft%20%7C%20%5Cright%20%7Cq%29%20%3D%20%5Cfrac%7B1%7D%7B2%7D%20KL%28p%20%5Cleft%20%7C%20%5Cright%20%7Cm%29%20&plus;%20%5Cfrac%7B1%7D%7B2%7D%20KL%28q%20%5Cleft%20%7C%20%5Cright%20%7Cm%29">

where `m` is calculated as follows:

<img src = "https://latex.codecogs.com/gif.latex?m%20%3D%20%5Cfrac%7B1%7D%7B2%7D%20%28q&plus;p%29">

JS distance is the square root of this score. The distance and divergence calculations are symmetrical, i.e. 
<img src = "https://latex.codecogs.com/gif.latex?JS%28p%5Cleft%20%7C%20%5Cright%20%7Cq%29%20%3D%3D%20JS%28q%5Cleft%20%7C%20%5Cright%20%7Cp%29">
