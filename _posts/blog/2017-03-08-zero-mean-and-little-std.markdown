---
layout: post
title: " Why do we need the MEAN to be near ZERO and stddev to be small?"
permalink: /blog/technology/Why-do-we-need-the-MEAN-to-be-near-ZERO-and-stddev-to-be-small
author: "Gao Minquan"
date: 2017-03-08 14:47:40"
use_math: true
categories: Machine Learning
---

Notice: *this article is a craft*

When we build a machine leanring model, as we know, we need to scale the normalize the train data. What we want to is that let the MEAN(average) of the train data to be ZERO, and standard deviation to be as small as possible. 

But, Why? 

In this Article, I will show the reason that why need the MEAN to be ZERO and stddeve to be small. 

### 1. Algebra Explaination. 

To keep the question simple, we assume the train set is one dimension. means, $x \in R^1 $, and we assume the hypothesis function is a linear function $f(x) = kx + b$. 

Therefore, we could define the error function or loss function by L2 distence:

$$loss(k, b) = \sum_{i=1}^{n}(kx_i+b-y_i)^2$$

`In order to keep the partial less simple, we often add the `$\frac{1}{2} $` before `$\sum$

Therefore, we get: 

$$ \frac{\partial{loss}}{\partial{k}} = 2\sum_{i=1}^{n}(kx_i+b-y_i)x_i \thicksim O(\sum(x_i)^2) $$

> If we add  $\frac{1}{2}$ before $\sum$, we will get $\frac{\partial{loss}}{\partial{k}} = \sum_{i=1}^{n}(kx_i+b-y_i)x_i$)$

**However, because we usually use the bath-mini gradient descent approach, not the full-batch gradient descent appraoch, we could know that the $\frac{\partial{loss}}{\partial{k}} \nsim O(\sum_{i=1}^{n}((x_i)^2))$, and in order to get the right K or b, we need the train over and over again(we call it one epoch). **

But, 

$\frac{\partial{loss}}{\partial{k}} \sim O(\sum_{i\in mini-batch}(x_i)^2)$

**In a simple word. We juse use a little train data when each train epoch. **

In flollowing, I will approve why the large mean of X set and the large stddve of X set are bad for trainning.

$\because$  very large mean of $<x_1, x_2, x_3, \dots x_n>, x \in mini-batch-train-set$ 

$\therefore \frac{\partial{loss}}{\partial{k}}$ is very large

and we define the learning rate to be $\alpha$

Therefore, $\delta{k} = \alpha \frac{\partial{loss}}{\partial{k}}$

$\therefore \delta k$ is very large

**Now, we assume at some time, we get the $\hat{k} = 5.3 $, and the right $ k=5.0 $, but if the $\delta{k}$ is too large, such as 15, then after iteration, we get the $\hat{k} = -9.7$, which let we get the right $k$ much more furthure.**

**In a simple word, we need keep $\delta{k}$ to be small or keep $\hat{k}$ consistent ahead to the right $k$**, but if we get the very large $\delta{k}$, the **convergence** will be very slow, or even *not convergent*.

> So, if the Trainset has the very large mean, whatever the mean is very large positive or very large negative, because every iteration the $\delta{k} = \alpha \frac{\partial{loss}}{\partial{k}}$, the convergence will become *much slow* or even *impossible*.

#### Why Small Stddve? 

*(What's the large stddve? Such as {101, -1, 123, -34}; What's the small stddve? Such as {101, 100, 122, ...}*

As the same reason,  if the standard deviation of $x_1, x_2, \dots, x_m $ is very large. 

the $$\delta{k}$$

will change very *rapidly*. 

This also makes the convergence of $\hat{k}$ is be *slowly* or *impossible.*

#### Conslusion

The reason why we should make the **mean** and **stddve** to be small and near to zero is that we should keep the convergence be quickly and consistent. 


#### Practice

If we have the train data set $ \vec{x_1} = <101, 101>, y_1 = 1, \vec{x_2} = <101, 99>, y_2=0$, what should we transform to keep the mean and std small?

> Hint: trying to divide the number by mean or substrct by some number. 

##### Practice Solution:  One possible result could be [1, 1], [1, -1], a more normal approach is 
    
    X = (X - X.mean())/(X.max()-X.min())
    
you could try it by yourself, and check the new X's mean and std.

### 2. Geometry Explaination Approach.
