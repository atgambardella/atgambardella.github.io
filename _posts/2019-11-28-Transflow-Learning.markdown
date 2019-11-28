---
layout: post
title:  "Transflow Learning"
date:   2019-11-28 07:51:23 +0000
categories: jekyll update
---

Generative models are one of the most exciting fields in AI currently, and you can do a lot of cool things with them, such as turning zebras into horses, or painting an image in the style of Van Gogh.


<div class="imgcap">
<img src="/assets/transflow/cyclegan.png">
<div class="thecap">Turning zebras into horses with <a href='https://arxiv.org/abs/1703.10593'>CycleGAN</a></div>
</div>

Today I'm going to talk about work that I've personally done along these lines. The method I'll describe is called <a href='put arxiv link here'>Transflow Learning</a>, and has a wide range of applications, from classifying handwritten digits, to making your waifu real. I'll briefly explain how it works and then get to the results.

<div class="imgcap">
<img src="/assets/transflow/cherrypicked.png">
<div class="thecap">Turning an anime character into a real person with Transflow Learning.</div>
</div>

## Generative Models

There are many types of generative models, but in this post I'm going to talk about a specific category known as "flow models." Flow models are generally the weakest of all generative models in terms of their ability to create realistic images, but come with an attractive property: invertibility.

What does invertibility mean in this context? It means we can give our generative model (which, like almost all things in modern AI, is a neural network) an output (in this case, an image) and receive back an input. But our model just creates realistic images out of thin air. What kind of input would it even take?

To understand that we need to step back and understand how neural networks process inputs. Neural networks generally get an output by putting the input through a series of learned, non-linear transformations. These transformations usually take the form $f(x) = g(W*x)$  

<div class="imgcap">
<img src="/assets/transflow/magnitude.gif">
<div class="thecap">'Smoothly' transforming a woman into my waifu. Note that the images are hilariously misaligned.</div>
</div>
