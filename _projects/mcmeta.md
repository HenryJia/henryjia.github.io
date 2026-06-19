---
layout: page
title: Beyond SGD - An Exploration of Metadynamics Inspired Methods for Deep Learning, A Work in Progress
description: Exploring how we can potentially apply metadynamics inspired methods to accelerate deep learning training 
img: assets/img/mcmeta/metad.jpg
importance: 1
#category: work
related_publications: false
---

# Adam still reigns supreme

It's not exactly a secret that [Adam](https://arxiv.org/abs/1412.6980) is defacto the industry and academic standard for optimisation, whenever you're playing with neural networks of some kind.

In some ways, this is wonderful. It means we have out of the box baselines which we know just works. It's incredibly useful to for testing other things, because we can always compare it back to Adam. This is also incredibly useful for debugging models, as it means we can be reasonably certain that if our model isn't training, it's probably not the optimiser's fault. Adam is a very solid block in the foundation of deep learning.

However, Adam is old, really old. The original ArXiv link dates back to 2014. That's 12 years ago at the time of writing. To put things in perspective, when Adam was first released, Theano was the only deep learning framework in Python. TensorFlow didn't exist. Even Keras wasn't released yet. Plenty of people were still writing frameworks in C++ even. Since then the deep learning field has been a battle royale of frameworks, models, and methodologies. We rarely see anything survive for even a few years without getting completely dominated by something else. Yet, Adam somehow has survived all of this.

# Second order methods still suck

There's been a lot of efforts to try and replace Adam over the years. A lot of them have been second order methods, which makes sense. Second order methods are well used in many other areas of computational science and machine learning. Methods like L-BFGS or Levenberg-Marquardt are very popular in many other areas of optimisation. So it make sense to try it in deep learning as well.

However, they just don't seem to work well for deep learning. Depending on who you ask, there's a lot of different reasons for this. My empirical observation from writing second order methods by hand in C way back in 2015 is that second order methods are almost "too good".

Whilst both first and second order methods assume convexity at some level, first order methods are more capable of handling non-convexity. Back in 2015, from my empirical experiments I noticed second order methods tend to get stuck, even with relatively simple neural networks.

It's also worth pointing out that minibatch optimisation is stochastic. We don't know the true function we're optimising, we only have a noisy estimate of it. This is another possible reason why second order methods don't work well. They rely on us getting second order information. I can't prove it, but my gut intuition is that this second order information is just too noisy over each minibatch. It throws off the optimisation process. The beauty of first order optimisation when you pick a good learning rate is that it can handle the noise well. In fact, some say that first order methods take advantage of the noise to deal with saddle points and local minima. Second order methods have no equivalent answer to this, and they just get stuck.

# Optimisation is a black box

