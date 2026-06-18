---
layout: about
title: About
permalink: /
subtitle: Machine Learning, Computational Chemistry, Additive & Subtractive Manufacturing, Flutemaking

profile:
  align: right
  image: prof_pic.jpg
  image_circular: false # crops the image to make it circular
  #more_info: 

selected_papers: false # includes a list of papers marked as "selected={true}"
social: true # includes social icons at the bottom of the page

announcements:
  enabled: false # includes a list of news items
  scrollable: true # adds a vertical scroll bar if there are more than 3 news items
  limit: 5 # leave blank to include all the news in the `_news` folder

latest_posts:
  enabled: false
  scrollable: true # adds a vertical scroll bar if there are more than 3 new posts items
  limit: 3 # leave blank to include all the blog posts
---

Hey there, I'm Henry. My current research is in predicting blood brain barrier (BBB) permeability to drug-like molecules at the University of Warwick. I previously worked in the ML industry for about 7 years, including at MidJourney and Leap Motion/UltraLeap.

My main focus is on combining machine learning with molecular dynamics simulations to create efficient methods of predicting BBB permeability for novel molecules. Molecular dynamics simulations are transparent and validated with physics, but they're computationally expensive. Machine learning gets blackboxy sometimes, but it's accurate and fast. My work is on integrating them so you can get the best of both worlds.

Although my research is focused on predicting BBB permeability, I expect these methods are highly applicable in other areas of absorbtion, distribution, metabolism and excretion (ADMET) prediction. But, I am just one guy, so maybe I'll get to work with one of you wonderful readers on that in the future.

I also have a strong pet interest in porting the ideas I come across in computational chemistry back into machine learning. I think a lot of the enhanced sampling methods used in molecular dynamics might be able to radically alter the standard SGD based methods everyone's been using for the last decade and a half.

Aside from my current work, I've had a long and storied journey in machine learning, and since you're here, I presume you want to read about it.

#### 1999 - 2010
I was born in China in 1999. I lived there till I was about 8, when I moved to the UK. When I was about 10, around 2009 and 2010, I started to read books on C programming. To be frank with you, I don't remember why. For whatever reason, 10 year old me decided that C/C++ was the thing to do instead of going outside. C/C++ stayed with me, and I continued to learn it for the next half a decade. For the longest time, C/C++ was my weapon of choice.

#### 2014 - 2015
I started getting into GUIs. I think like every kid who touched code, I wanted to make video games. So I started messing around with wxWidgets and Qt. I never made any games, funnily enough. I did briefly contribute to the open source 0AD game, which is based on Age of Empires. But, I mostly built other things with Qt. I ended up making a full Microsoft Excel clone of all things. Not exactly the most exciting project, but 15 year old me got a tad obsessed with it. I was a weird kid, what can I say?

#### January 2015 - March 2015
I started hearing about this strange thing called "machine learning". I had no idea what it was, but I saw the Andrew Ng course on Coursera and thought I should give it a go. After all, how hard could it be? It's hard to understate how good Andrew Ng's course was. ML stuck with me. I ended up also doing the legendary MIT 18.06 Linear Algebra course, along with Professor Jim Fowlers Calculus courses to supplement the maths side.

#### March 2015 - September 2015
I started working on machine learning projects of my own. At the time, Keras was just released, and definitely wasn't well known. Tensorflow wouldn't be released until late 2015. Theano existed, but wasn't exactly popular. Everyone was building their own frameworks. So, I decided to build my own as well. I bought myself a NVidia GTX 960 4GB GPU, taught myself how to write and optimise CUDA C, and built my own deep learning framework in it from scratch. I called it "CUBLAS-ML" as it was mainly using NVidia's CUBLAS library to do all the linear algebra. Funnily enough, I think I did it in CUDA C because I was afraid of having to learn Python. A tad ironic in hindsight given how easy Python is to learn, but hey ho, I think I ended up with somewhat unique experience into high performance computation on GPUs which still serve me well to this day.

#### September 2015 - June 2022
I met David Holz. At the time, he was the CTO of Leap Motion. He decided to hire me as a machine learning engineer. I worked with him at Leap Motion (later rebranded to Ultraleap) for the next 6 years. We did a lot in this time. I integrated my CUDA C deep learning framework into the Leap Motion team's framework, as theirs was in C++ and not CUDA accelerated. My framework didn't survive long though. ML frameworks were developing at an ungodly pace. By late 2015 we all finally switched to Python as TensorFlow came out along with tf.Keras. We built a lot of cool stuff. We built, then rebuilt our in house machine learning infrastructure. We played around with early GANs for synthetic data generation to make our existing simulators more realistic. We tried deformable convolutions. We even tried early neural SLAM using LSTMs with CNNs. We also worked on machine learning with forward kinematics models.

#### June 2022 - December 2022
I think it was about a year before this, David left Ultraleap to start MidJourney. I ended up leaving about a year later to join him. We did some interesting things in that time. MidJourney was in its early stages, so I worked on the early diffusion models with U-Net based architectures and CLIP embeddings. We didn't have much infrastructure at the time, but I was unable to stick around to build it, as I wanted to start a PhD.

#### December 2022 - September 2026
I started my PhD at the University of Warwick. My motivation was mixed one. I'd spent a lot of time doing just machine learning, and I felt like I was rabbitholing myself somewhat. ML was and remains what I'm good at, but I think I wanted more. I was also somewhat burned out by the 7 long years of working in industry. I know a PhD isn't exactly the usual prescribed treatment for burnout. But, I wasn't the kind of person who can just sit around doing nothing. I needed something interesting to work on, and I've long had the idea of shifting into computational medicine. So I wound up doing a PhD on predicting BBB permeability. The rest is history, and the start of my bio tells you all about that.

During my PhD, I also got to play around with a lot of side projects. I briefly also worked as a research fellow in utilising Bayesian Optimisation for multi-objective small molecule design. Due to circumstances beyond our control we didn't manage to get a paper out, but I might revisit some of those ideas in the near future. Some of those ideas seem especially good since we now have very good foundation models for small molecules now.

I played around a lot with additive and subtractive manufacturing. I built my own 3D printers using the Voron designs. With my own printers, I 3D printed a working violin, which you can see in my profile picture. I got access to a lathe and mill thanks to the Birmingham Makerspace. I ended up getting into flutemaking. I found a set of formulas for calculating flute tunings. This led me to calculating, designing and fabricating a series of Irish flutes. I gave these mostly to friends who were professional musicians, who seemed to judge them as on par with very expensive professional instruments. I also dabbled around with the ESP Internet of things Development Framework for programming ESP based microcontrollers in C with RTOS.

I'm now heading towards the end of my PhD, and I'm eager to see what happens next. I want to continue with drug discovery and computational medicine. I also want to steal the ideas I've picked up from computational chemistry and statistical mechanics, and see how they work in ML. I have more than a few ideas of things to play with in this area. With any mount of luck, I look forward to working with you, dear reader, on some of them in the future.