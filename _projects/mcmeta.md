---
layout: page
title: Beyond SGD - An Exploration of Metadynamics Inspired Methods for Deep Learning, A Work in Progress
description: Exploring how we can potentially apply metadynamics inspired methods to accelerate deep learning training 
img: assets/img/mcmeta/metad.jpg
importance: 1
date: 2026-06-20
#category: work
related_publications: false
---

# Adam still reigns supreme

It's not exactly a secret that [Adam](https://arxiv.org/abs/1412.6980) is defacto the industry and academic standard for optimisation, whenever you're playing with neural networks of some kind.

In some ways, this is wonderful. It means we have out of the box baselines which we know just works. It's incredibly useful to for testing other things, because we can always compare it back to Adam. This is also great for debugging models, as it means we can be reasonably certain that if our model isn't training, it's probably not the optimiser's fault. Adam is a very solid block in the foundation of deep learning.

However, Adam is old, really old. The original ArXiv link dates back to 2014. That's 12 years ago at the time of writing. To put things in perspective, when Adam was first released, Theano was the only deep learning framework in Python. TensorFlow didn't exist. Even Keras wasn't released yet. Plenty of people were still writing frameworks in C++ even. Since then the deep learning field has been a battle royale of frameworks, models, and methodologies. We rarely see anything survive for even a few years without getting completely dominated by something else. Yet, Adam somehow has survived all of this.

# Second order methods haven't caught on

There's been a lot of efforts to try and replace Adam over the years. A lot of them have been second order methods, which makes sense. Second order methods are well used in many other areas of computational science and machine learning. Methods like L-BFGS or Levenberg-Marquardt are very popular in many other areas of optimisation. So it make sense to try it in deep learning as well.

However, they just don't seem to work well for deep learning. Depending on who you ask, there's a lot of different reasons for this. The first and most obvious issue is that all second order methods are approximations. This is because the number of elements in the Hessian is the square of the number of parameters. As such, every second order method only computes an approximation of the true Hessian, typically only estimating the diagonal elements. This has the added benefit of not needing the solve for the inverse of the Hessian, which is clearly intractable for deep learning.

I did personally implement and mess with methods like Levenberg-Marquardt around 2015-2016. My empirical observation back then was that second order methods have a tendency to get stuck. Whilst both first and second order methods assume convexity at some level, first order methods are more capable of handling non-convexity. Back in 2015, from my empirical experiments I noticed second order methods very much struggled to overcome these saddle points and local minima.

It's also worth pointing out that minibatch optimisation is stochastic. We don't know the true function we're optimising, we only have a noisy estimate of it. This is another possible reason why second order methods don't work well. They rely on us getting second order information. I can't prove it, but my gut intuition is that this second order information is just too noisy over each minibatch. It throws off the optimisation process. The beauty of first order optimisation when you pick a good learning rate is that it can handle the noise well. In fact, some say that first order methods take advantage of the noise to deal with saddle points and local minima. Most second order methods have no equivalent answer to this, and they just get stuck.

There are more recent second order methods like [Shampoo](https://arxiv.org/abs/1802.09568), and [SOAP](https://arxiv.org/abs/2409.11321) (not to be confused with Smooth Overlap of Atomic Positions). However, they present multiple issues. For one, they haven't caught on much yet, and are in many ways relatively untested. We don't really know for certain that Shampoo or SOAP works in the wide variety of settings as Adam.

The second is that they're not really second order methods, at least not in any traditional sense. Shampoo doesn't actually compute the Hessian analytically. It estimates the empirical Fisher information matrix, as a proxy for the Hessian. SOAP is based on Shampoo, so it's not a true second order method either.

There's also a bit of an elephant in the room in that SOAP is relatively complex implementation-wise. This is something which often goes underappreciated. Adam is very simple to implement, and it's very easy to understand what's going on under the hood as the equations can be written out in just a few lines. This is likely why it has such staying power. It's simple, and there's relatively few moving parts to go wrong. SOAP is relatively complex. Intuitively, complexity and robustness are inversely correlated.

# Neural network optimsation is a strange beast

Over the years, newer hypotheses have popped up on neural network optimisation with SGD. A couple of notable ones are the [Lottery Ticket Hypothesis](https://arxiv.org/abs/1803.03635) and the later [Escape Dimension Hypothesis](https://flavio-martinelli.github.io/blog/2026/lottery/). The escape dimension hypothesis is particularly interesting, as it seems to almost be a sort of corollary to the hypothesis on [intrinsic dimensions](https://arxiv.org/abs/1804.08838).

In short, the intrinsic dimension hypothesis tells us that neural networks have a low intrinsic dimension, provided we are applying the correct inductive biases. You can train a neural network in a small subspace of the full parameter space with limited loss of performance. The escape dimension hypothesis states in effect that the extra dimensions allow us to transform local minima into saddle points, thus allowing us to escape them without having to pay the cost of going over the barrier. In other words, the extra dimensions are kind of like wormholes in the loss landscape. They "shorten" the distance between points in the intrinsic dimension subspace. This also makes sense in the context of the intrinsic dimension hypothesis paper. In that paper, they admit that optimising only in the intrinsic dimension subspace only works well if the problem is relatively simple. They never got it to work on ImageNet. It's quite possible that when the problem gets sufficiently complex, you need the extra dimensions to wormhole your way around the intrinsic dimension subspace.

<div class="row justify-content-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/mcmeta/wormhole_interstellar.gif" title="Interstellar Wormhole Explanation gif" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    A gif of a wormhole being explained from the movie Interstellar, showing how extra dimensions can shorten the distance between two points in a lower dimensional subspace. This is analogous to how the extra dimensions in neural network optimisation can allow us to escape local minima by transforming them into saddle points.
</div>

Something to note though, however, is that these hypotheses share an interesting trait. They start shifting away from the very mathematical theory heavy analysis of optimisation. They shift towards an empirical and intuitive understanding of optimisation, with mathematics used as the language to describe it. It kind of shows that neural network optimisation might be a very different and strange beast compared to more traditional optimisation problems in mathematics. Here, we don't have good guarrantees of what the optimisation landscape is like. We only have vague intuitions and empirical observations. In some ways, this shifts us away from a mathematical understanding of optimisation, and more towards a more natural science like approach. We have to observe, hypothesise, and test to build our intuitions.

# So, you want to find a unicorn?

Both the intrinsic dimension hypothesis and the escape dimension hypothesis are intuitively very sound. However, they are more descriptive than prescriptive. They tell us what is happening, but they don't really tell us what to do about it. The escape dimension hypothesis tells us that the extra parameters are useful for escaping local minima. But, in practice, those extra parameters take up valuable RAM and TFLOPs. It would be nice if we could take the simple logical conclusion of the escape dimension hypothesis, and just add more parameters. But, that's clearly not a practical solution in this day and age of LLMs, not to mention high hardware costs. So, we need to go further and try and find a way to escape local minimal without paying the optimisation cost of those minima, or by adding more parameters. Oh, and this method needs to be simple and robust enough to be widely adopted. This is a tall order to say the least.

But, there is a valuable old saying in engineering "Any idiot can build a bridge, but only an engineer can build one that just about stands." The point of ML research and engineering isn't to scale things endlessly. Any idiot who can write Python can figure that out if they had unlimited compute. The point of ML is to find the most efficient way of doing things. However, we are running up against old questions in ML optimisation which are yet to be solved. What we're looking for really is a unicorn. That being said, unless we want to be stuck trying to solve problems by building ever larger computational hammers, we need to find that unicorn.

# What on earth is metadynamics?

Generally, it's regarded as bad engineering practice to reinvent the wheel. So naturally, I checked to see if anyone else had the idea of using metadynamics to aid deep learning optimisation. To my surprised, there were quite literally zero papers on this, at least that I could find. There's papers on people applying deep learning to help with metadynamics in molecular dynamics, but nothing on the other way around.

This is quite surprising, given how many papers get tossed at ArXiv every day, probably never to be read. Someone in this infinite monkeys with typewriters should've run into this idea. It's especially surprsing given metadynamics isn't even new. The original paper was in 2002, almost quarter of a century ago. well tempered metadynamics was published in 2008. These are not groundbreaking ideas, at least in computational chemistry. So it's very unusual that no one has publicly thought of this before, at least not on ArXiv. Maybe there are random people out there who have put it on their webpages like mine here, but I couldn't find them.

Metadynamics at its core is actually a very simple idea, which is what drew me to it. Imagine we are in an energy landscape. Naturally, physical systems tend towards the lowest local energy state. This is essentially the same as gradient descent. However, in molecular dynamics, we want to explore beyond the local minima, and ideally the whole energy landscape. So, we add a little bit of extra energy to the system at the current state at regular intervals. We can do this by adding a small Gaussian function centred at the current state. This is like filling up the local minima with a little bit of sand, so that the system can escape it and explore other areas of the energy landscape. Over time, we can build up a picture of the energy landscape by looking at where we've added these Gaussian functions.

<div class="row justify-content-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/mcmeta/metad.jpg" title="Metadynamics Illustration" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    An illustration of metadynamics with a 1D energy landscape, provided by [CompChems](https://www.compchems.com/an-introduction-to-enhanced-sampling-and-metadynamics). Here the black line is our true energy landscape, and the red shows our Gaussian functions being added, which allows us to escape local minima and explore the whole energy landscape.
</div>

Metadynamics is a very powerful method in molecular dynamics, speaking from experience of using it for the last few years. But applying it to deep learning means we have to make a lot of adjustments, and treat it more as loose inspiration. Deep learning is a different beast and runs into a number of issues we don't have in molecular dynamics.

# Nothing's easy in deep learning

The first and biggest issue with applying metadynamics is dimensionality. In molecular dynamics, we typically have a handful of dimensions, maybe up to 8 if we're feeling brave. In deep learning, our parameter space is anywhere between millions to billions of dimensions, a lot of which may not do anything useful. We clearly can't apply metadynamics naively to the whole parameter space.

To work around this, we use our input data as a "lens" to view the parameter space. We apply metadynamics to a hidden layer of the model instead. However, this hidden layer is still very high dimensional, which means we can't apply metadynamics naively to the whole hidden layer. We need some way of reducing dimensionality.

An interesting paper I came across recently is the [MiCA paper](https://arxiv.org/abs/2604.01694). MiCA in short proposes finetuning models by appling minor component analysis to the weight space, to fine tune only in the minor component subspace. Intuitively, this is very interesting. It's essentially doing LoRA in the sort of "dead space" of the weight space that doesn't do very much.

We take a page out of their book and do something similar. We apply minor component analysis to the activations of a hidden layer, and apply metadynamics in the minor component subspace instead. This allows us to try and force the model to explore the "dead space" of the activations, which should map to the "dead space" of the weight space, with any amount of luck. Hopefully, this should allow the model to do more exploration in regions which don't directly affect the loss. Maybe this will accelerate training by exploring saddle points and local minima more effectively.

The second big issue, the one which I've yet to figure out how to solve fully, is the hyperparameters. Metadynamics introduces a whole new set of hyperparameters. We have the height and width of the Gaussian functions, and how often we add them along with how high to scale them. These hyperparameters are very important for the performance of metadynamics. If we add the Gaussians too often, or if they're too high, we might end up adding too much energy to the system, which can lead to divergence. If we don't add them often enough, or if they're too low, we might not add enough energy to actually be useful.

Finding the right hyperparameters for metadynamics is comparatively straightforward in molecular dynamics. Because we're in a physical system with actual units for time, energy, and distance, we can use our understanding of the system to make educated guesses about the hyperparameters. In deep learning, we don't have this luxury. We don't have a physical system with units that we can use to guide our choice of hyperparameters. There are no physical real world units for us to measure distance in the hidden layer latent space by. The loss function isn't a physical energy with real world units either. As such, we are limited to trial and error in practice. This is somewhat painful, but I don't see a good way around it yet.

The third issue is that metadynamics, when applied naively, requires O(t) memory, where t is the number of timesteps. This is because we need to store all the Gaussian functions we've added to the system. In molecular dynamics, this isn't a big deal, as we typically only run simulations for a few nanoseconds, which is a relatively small number of timesteps. In deep learning, we can easily run for millions of timesteps, which means we can't store all the Gaussian functions.

To work around this, we use a ring buffer to store the Gaussians. This naturally means that our memory requirements are now fixed at the beginning of training regardless of how long we train for.

# Implementation strategy

So, to test things out, we need a sufficiently hard problem. As shown in the intrinsic dimensions hypothesis paper linked earlier, simple problems like MNIST can be optimised in a very low dimensional subspace. We need something more complex than that.

Since we're in the era of generative models, and computer vision was my old background, we'll test things out using flow matching.

We'll take the NVidia SANA architecture as our base architecture as this is easily adapted via HuggingFace's diffusers library. We'll cut the model size down somewhat to fit within a tight computational budget so I can run it on consumer grade NVidia GPUs. We'll train it on the PD12M + MS COCO dataset, as this gives us around 12-13M images to train on. PD12M has good synthetic captions for text conditioning, but they're a bit "artificial" in many ways. The COCO dataset also has human captions, which should make the model respond better to humanistic captions. To convert the text to embeddings, we'll use Gemma3-270M. It's not powerful, but it is very computationally cheap, and good enough for our purposes.

For the flow matching methodology, we'll use the standard rectified/optimal transport flow matching method. It's simple and highly effective. We'll also use the [REPA](https://arxiv.org/abs/2410.06940) method to help accelerate training, as it's pretty easy to implement

To apply the metadynamics, we'll perform minor component analysis by tracking the exponential moving average of the mean and covariance of the activations of a hidden layer. Specifically, we'll use the 8th hidden layer as it's sort of in the middle, and will have a decent representation whilst not directly breaking the model too much hopefully. We can obtain the minor components simply by mean centering the activations, then computing an eigendecomposition of the covariance matrix, taking the smallest 8 smallest eigenvalues and their corresponding eigenvectors, and projecting the activations onto those eigenvectors. Then we can apply metadynamics in this minor component subspace.

Note that we also store the mean and eigenvectors used in the projection along with the Gaussian functions in the ring buffer. This is because the minor component subspace might change a lot over time. There's no guarantee that this change will also be continuous because of the eigendecomposition step. So we store the mean and eigenvectors, and always compute distances in the original minor component subspace the Gaussian was logged in.

# Does it actually work?

Short answer, not yet. Things are still being trained and this is a work in progress. You'll have to check back at another time to see results.