---
layout: single
title: Exploring zeroth order optimizers, single neuron
date: 2026-01-06
---

I've been experimenting with zeroth-order optimizers, like Evolution Strategies (ES), for some time now, specifically for training certain types of neural networks and for RL ([https://github.com/lucidrains/x-evolution](https://github.com/lucidrains/x-evolution)).

Inspired by [https://kindxiaoming.github.io/blog/2026/single-relu-neuron-copy/](https://kindxiaoming.github.io/blog/2026/single-relu-neuron-copy/). Starting with the same initializations in xioming's post, we see that ES has a hard time learning even this simple system. Looking at the weight evolution:

![](/../assets/images/image1.png)

No annealing is done. If anyone knows some initializations/hyperparams that would result in successful convergence in the uniform noise sampling case (not Gaussian), I would greatly appreciate it.

![](/../assets/images/image3.png)

Looking at the loss landscape, the narrow troughs and oval like shapes, as well as the oscillations of the final bias suggests that CMA-ES ([https://lilianweng.github.io/posts/2019-09-05-evolution-strategies/](https://lilianweng.github.io/posts/2019-09-05-evolution-strategies/)) might be able to deal with this, and indeed it does (using the balanced initialization):

![](/../assets/images/image2.png)

Still, like the original blog post, initializing with a large negative b2, like gradient descent (Adam), also leads to a linear regression solution local minima fixing the rest of the hyperparams. Though the |b2| transition appears different (|b2| was initialized to -5 here). Also since the biases are zero, the w1*w2 = 1 symmetry is all valid (if it can get the weights near there). Gradient descent seems to avoid these solutions better.

![](/../assets/images/image4.png)
