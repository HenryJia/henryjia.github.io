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

# Second order methods Haven't Caught On

There's been a lot of efforts to try and replace Adam over the years. A lot of them have been second order methods, which makes sense. Second order methods are well used in many other areas of computational science and machine learning. Methods like L-BFGS or Levenberg-Marquardt are very popular in many other areas of optimisation. So it make sense to try it in deep learning as well.

However, they just don't seem to work well for deep learning. Depending on who you ask, there's a lot of different reasons for this. The first and most obvious issue is that all second order methods are approximations. This is because the number of elements in the Hessian is the square of the number of parameters. As such, every second order method only computes an approximation of the true Hessian, typically only estimating the diagonal elements. This has the added benefit of not needing the solve for the inverse of the Hessian, which is clearly intractable for deep learning.

I did personally implement and mess with methods like Levenberg-Marquardt around 2015-2016. My empirical observation back then was that second order methods have a tendency to get stuck. Whilst both first and second order methods assume convexity at some level, first order methods are more capable of handling non-convexity. Back in 2015, from my empirical experiments I noticed second order methods very much struggled to overcome these saddle points and local minima.

It's also worth pointing out that minibatch optimisation is stochastic. We don't know the true function we're optimising, we only have a noisy estimate of it. This is another possible reason why second order methods don't work well. They rely on us getting second order information. I can't prove it, but my gut intuition is that this second order information is just too noisy over each minibatch. It throws off the optimisation process. The beauty of first order optimisation when you pick a good learning rate is that it can handle the noise well. In fact, some say that first order methods take advantage of the noise to deal with saddle points and local minima. Most second order methods have no equivalent answer to this, and they just get stuck.

There are more recent second order methods like [Shampoo](https://arxiv.org/abs/1802.09568), and [SOAP](https://arxiv.org/abs/2409.11321) (not to be confused with Smooth Overlap of Atomic Positions). However, they present multiple issues. For one, they haven't caught on much yet, and are in many ways relatively untested. We don't really know for certain that Shampoo or SOAP works in the wide variety of settings as Adam.

The second is that they're not really second order methods, at least not in any traditional sense. Shampoo doesn't actually compute the Hessian analytically. It estimates the empirical Fisher information matrix, as a proxy for the Hessian. SOAP is based on Shampoo, so it's not a true second order method either.

There's also a bit of an elephant in the room in that SOAP is relatively complex implementation-wise. This is something which often goes underappreciated. Adam is very simple to implement, and it's very easy to understand what's going on under the hood as the equations can be written out in just a few lines. This is likely why it has such staying power. It's simple, and there's relatively few moving parts to go wrong. SOAP is relatively complex. Intuitively, complexity and robustness are inversely correlated.

# Neural Network Optimsation is a Strange Beast

Over the years, newer hypotheses have popped up on neural network optimisation with SGD. A couple of notable ones are the [Lottery Ticket Hypothesis](https://arxiv.org/abs/1803.03635) and the later [Escape Dimension Hypothesis](https://arxiv.org/abs/1803.03635). The escape dimension hypothesis is particularly interesting, as it seems to almost be a sort of corollary to the hypothesis on [intrinsic dimensions](https://arxiv.org/abs/1804.08838).

In short, the intrinssic dimension hypothesis tells us that neural networks have a low intrinsic dimension, provided we are applying the correct inductive biases. You can train a neural network in a small subspace of the full parameter space with limited loss of performance. The escape dimension hypothesis states in effect that the extra dimensions allow us to transform local minima into saddle points, thus allowing us to escape them without having to pay the cost of going over the barrier. In other words, the extra dimensions are kind of like wormholes in the loss landscape. They "shorten" the distance between points in the intrinsic dimension subspace. This also makes sense in the context of the intrinsic dimension hypothesis paper. In that paper, they admit that optimising only in the intrinsic dimension subspace only works well if the problem is relatively simple. They never got it to work on ImageNet. It's quite possible that when the problem gets sufficiently complex, you need the extra dimensions to wormhole your way around the intrinsic dimension subspace.

<div class="row justify-content-center">
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/mcmeta/wormhole_interstellar.gif" title="Interstellar Wormhole Explanation gif" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    A gif of a wormhole being explained from the movie Interstellar, showing how extra dimensions can shorten the distance between two points in a lower dimensional subspace. This is analogous to how the extra dimensions in neural network optimisation can allow us to escape local minima by transforming them into saddle points.
</div>

Something interesting to note though, however, is that these hypotheses share an interesting trait. They start shifting away from the very mathematical theory heavy analysis of optimisation. They shift towards an empirical and intuitive understanding of optimisation. It kind of shows that neural network optimisation might be a very different and strange beast compared to more traditional optimisation problems in mathematics. Here, we don't have good guarrantees of what the optimisation landscape is like. We only have vague intuitions and empirical observations. In some ways, this shifts us away from a mathematical understanding of optimisation, and more towards a more natural science like approach. We have to observe, hypothesise, and test to build our intuitions.

# So, You Want to Find a Unicorn?

Both the intrinsic dimension hypothesis and the escape dimension hypothesis are intuitively very sound. However, they are more descriptive than prescriptive. They tell us what is happening, but they don't really tell us what to do about it. The escape dimension hypothesis tells us that the extra parameters are useful for escaping local minima. But, in practice, those extra parameters take up valuable RAM and TFLOPs. It would be nice if we could take the simple logical conclusion of the escape dimension hypothesis, and just add more parameters. But, that's clearly not a practical solution in this day and age of LLMs, not to mention high hardware costs. So, we need to go further and try and find a way to escape local minimal without paying the optimisation cost of those minima, or by adding more parameters.

#### In other words, we want to find a unicorn

