---
layout: post
mathjax: true
title:  "Transflow Learning"
date:   2019-11-28 07:51:23 +0000
categories: jekyll update

---

Generative models are one of the most exciting fields in AI currently. In their raw form they just create images similar to that found in some dataset, but you can also do a lot of cool things with them, such as turning zebras into horses, or painting an image in the style of Van Gogh.


<div class="imgcap">
<img src="/assets/transflow/cyclegan.png">
<div class="thecap">Turning zebras into horses with <a href='https://arxiv.org/abs/1703.10593'>CycleGAN</a>.</div>
</div>

Today I'm going to talk about work that I've personally done along these lines. The method I'll describe is called <a href='put arxiv link here'>Transflow Learning</a>, and has a wide range of applications, from classifying handwritten digits, to making your waifu real. I'll briefly explain how it works and then get to the results.

<div class="imgcap">
<img src="/assets/transflow/cherrypicked.png">
<div class="thecap">Turning an anime character into a real person with Transflow Learning.</div>
</div>

## Generative Models

There are many types of generative models, but in this post I'm going to talk about a specific category known as "flow models." Flow models are generally the weakest of all generative models in terms of their ability to create realistic images, but come with an attractive property: invertibility.

What does invertibility mean in this context? It means we can give our generative model (which, like almost all things in modern AI, is a neural network) an output (in this case, an image) and receive back an input. But generative models just create realistic images out of thin air. What kind of input would it even take?

To understand that we need to step back and understand how neural networks process inputs. Neural networks generally get an output by putting the input through a series of learned, non-linear transformations. These transformations usually take the form $f(x) = g(W * x)$ where $x$ is our input, $W$ is a learned, real-valued weight matrix, and $g$ some non-linearity like the <a href='https://en.wikipedia.org/wiki/Sigmoid_function'>sigmoid function</a>. The most important thing to note here is that all of our functions are <i>deterministic</i>, that is, no random number generation is invoked at any point in the process. This means that for some given input, we will always get the same output.

This is an issue because we want to be able to create any and all arbitrary images with our generative model. Can we come up with a way to induce randomness?

It turns out that the easiest way to do this is to give it a randomly sampled vector $z$ as input, both during training and test time, and that crucially the distributions from which we sample these $z$ stay fixed throughout the whole process. After all, if during training we showed our model how to turn $z$ in a certain range into an image, and then during test time showed it a $z$ far out of this range, we have no idea what our model would do.

So with an invertible generative model, we can provide our network with an image, and then get back the random $z$ that would have produced this image. Neat.

## Properties of Generative Models

Training generative models in this way, with a randomly sampled $z$, often induces very desirable effects into "$z$ space," which is known as the "latent space". One of these desirable effects is the ability to interpolate images, as seen below.

<div class="imgcap">
<img src="/assets/transflow/magnitude.gif">
<div class="thecap">'Smoothly' transforming a woman into my waifu. Note that the image is hilariously misaligned with the dataset on which the flow model was originally trained.</div>
</div>

Here I show an interpolation using a flow model trained on human faces. During training the $z$ were sampled from a multivariate (multi-dimensional) normal distribution and here I'm interpolating from the center of that distribution, the 0 vector, to an image I selected myself. I am only able to do this because I am using a flow model, which is invertible, and therefore I know the $z$ corresponding to the image of this anime character.

The ability to interpolate smoothly in the latent space of a generative model means that $z$ which are close to each other correspond to images close to each other, which is another really nice property to have. From the gif above we can see that this even applies for images which are pretty far outside of the training distribution. This is going to come in handy for the next section.

## Transflow Learning

Remember when I said we needed to keep the distribution from which we sampled $z$ fixed or else <i>terrible things might happen</i>? This is true to a degree, but what if we also want terrible things to happen? What if we want to sample from a distribution that isn't the same as the one on which we originally trained? As it turns out, we can do that, and we can do that shockingly well.

The method I'm going to handwavingly describe here is known as <a href='put arxiv link here'>Transflow Learning</a>, so named because it <i>tranfers knowledge</i> from a trained <i>flow model</i> (or really any invertible generative model) to new data. The general idea is that if we can find some $z$ corresponding to data that we want new samples to look like, we can find the normal distribution in between our original distribution (from which we could sample arbitrary human faces) and our data, to get the human faces that look like our data.

<div class="imgcap">
<img src="/assets/transflow/gaussians.png">
<div class="thecap">Given our original flow model (cool colors) and new data (green) we can find a new normal distribution (hot colors) which gives samples in between the distribution on which we originally trained our model, and our new data.</div>
</div>


