---
layout: single
title: Exploring zeroth order optimizers, single neuron
date: 2026-01-06
---

I've been experimenting with zeroth-order optimizers, like Evolution Strategies (ES), for some time now, specifically for training certain types of neural networks and for RL ([https://github.com/lucidrains/x-evolution](https://github.com/lucidrains/x-evolution)).

Inspired by [https://kindxiaoming.github.io/blog/2026/single-relu-neuron-copy/](https://kindxiaoming.github.io/blog/2026/single-relu-neuron-copy/).  Using the same single ReLU Neuron with one hidden layer with 1D input:

$$f(x; w_1, b_1, w_2, b_2) = w_2\sigma(w_1 x + b_1) + b_2, \quad \sigma(x) = \text{ReLU}(x) = \max(0, x)$$

Starting with the same initializations in Ziming Liu's post ($w_1 = w_2 = 1$ ), we see that ES has a hard time learning even this simple system. Looking at the weight evolution:

![Weight evolution over training iterations showing ES struggling to converge](/../assets/images/image1.png)

No annealing is done. If anyone knows some initializations/hyperparams that would result in successful convergence in the uniform noise sampling case (not Gaussian), I would greatly appreciate it.

![Loss landscape visualization showing narrow troughs and oval shapes](/../assets/images/image3.png)

Looking at the loss landscape, the narrow troughs and oval like shapes, as well as the oscillations of the final bias suggests that CMA-ES ([https://lilianweng.github.io/posts/2019-09-05-evolution-strategies/](https://lilianweng.github.io/posts/2019-09-05-evolution-strategies/)) might be able to deal with this, and indeed it does (using the balanced initialization):

![CMA-ES successfully converging with balanced initialization](/../assets/images/image2.png)

Still, like the original blog post, initializing with a large negative $b_2$, like gradient descent (Adam), also leads to a linear regression solution local minima fixing the rest of the hyperparams. Though the $\|b_2\|$ transition appears different ($\|b_2\|$ was initialized to -5 here). Also since the biases are zero, the $w_1 \cdot w_2 = 1$ symmetry is all valid (if it can get the weights near there). Gradient descent seems to avoid these solutions better.

![Training dynamics with large negative bias initialization showing local minima](/../assets/images/image4.png)
