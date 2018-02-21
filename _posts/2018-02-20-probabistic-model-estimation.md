---
published: true
title: "f-GAN a generalization of GANs to all f-divergences"
date:   2018-02-20 00:00:00 +0100
author_profile: true
mathjax: true
categories:
  - Deep Learning
tags:
  - Probabilistic models
  - Probability distribution distance
---

In this blog intro I want to write some notes about the paper [f-GAN: Training Generative Neural Samplers using Variational Divergence Minimization](https://papers.nips.cc/paper/6066-f-gan-training-generative-neural-samplers-using-variational-divergence-minimization.pdf) and the fantastic presentation of the [NIPS 2016 Workshop on Adversarial Training](https://www.youtube.com/watch?v=kQ1eEXgGsCU) that I had the great honor to attend in person on December 2016.

A **probabilistic model** is a formalized representation of an event or a phenomenon in a way that instead of giving a unique answer for an event as a deterministic model does, it gives as a solution a probability distribution. It is used to modelize stochastic processes where the events doesn't have a deterministic solution. This models are used to mimic as uch as possible the behaviour of real world probability distributions. 

Real world probability distributions can be approximated with real data adquisition of the event or phenomena that we are studying. As we don't now, if they exist, what are the principles that rule the world, we can only approximate the true dstributions collecting samples from the environment and modellizing models to mimic its behaviour.

# Estimation of probabilistic models

Having a real distribution $$ Q $$, we can use a parametric model $$ P $$ to approximate $$ Q $$. For measuring how far is our model from correctly predicting the true distribution, we need a measure of the difference between the results reported by the model and the vaues of the true dstribution. Firstly, as both models are stochastic, they don't report a unique value for each input but a probability distribution. We have to define a way of comparing probability distributions. One way of doing this is making an abstraction of the term distance and broaden its scope defining the so called **distance between probability distributions**. Secondly, we can do some assumptions on $$ P $$ to ease the process of approximation, i.e., that $$ P $$ has a tractable sampling, in order to compare the samples of our model with the true samples; that $$ P $$ has a tractable parameter gradient with respect to sample, in order to allow the usage of optimization techniques for learning; and finally that $$ P $$ had a tractable likelihood function, that is that for every instance of the class you can calculate the log-likelihood point-wise.


# Probabilistic models

Depending on the construction procedure we differentiate between the next probabilistic models:

* Graphical models (GMs)
* Variational autoencoders (VAEs)
* Generative Adversarial Networks (GANs)

**Graphical models** are models built using as a main representation a graphical structure that abstracts out the contitional independence relationships between variables.

**Variational autoencoders** is a generative model. It uses a **encoder network** to encode the true distribution into a small feature space and after that uses a decoder network to reconstruct the original sample from the encoded representation. It uses neural networks as a way to represent information in a compressed manner an to learn important features required for generating a true distribution.

**Generative Adversarial Networks** use also a combination of two neural networks to create a generative model that tries to mimic a true distribution. The first network called *generator*, generates a model sample from a random vector using a deterministic transformation. A second neural network called *discriminator* receives randomly chosen samples from the true distribution and from the model distribution and is trained for differentiating between them. Both networks are trained in a adversarial manner, the generator to generate images as close as possible to the true distribution and the discrinator to detect the samples coming from the generator. GANs are a likelihood free model because it has a non-tractable likelihood although probably existing.

# Abstraction of the concept of distance between probability distributions

Different approaches exist to define the distance between probability distributions. We can differentiate mainly between three different approaches:

1. Integral probability metrics
2. Scoring rules
3. f-divergences

## Integral probability metrics

Addressed the firt time in the publications of [Müller et al., 1997](https://www.jstor.org/stable/1428011?seq=1#page_scan_tab_contents) and [Sriperumbudur et al., 2010](http://www.jmlr.org/papers/volume11/sriperumbudur10a/sriperumbudur10a.pdf). The key point f this methods is that both distributions appear in expectation form, alowing then to approximate such expectation using samples. Wasserstein distance is derived fro this methods, successfully used afterwards as a distance in [Wasserstein-GANs](https://arxiv.org/abs/1701.07875).

## Scoring rules
[Gneiting & Raftery, 2007](https://www.stat.washington.edu/raftery/Research/PDF/Gneiting2007jasa.pdf) proposed the approach of using a score for evaluation of the fitness of one distributon to another. The point is the optimization of the score. The maximum (minimum) score is achieved when both distributions are the same.

## f-divergences

Addressed by [Ali & Silvey, 1966](https://www.jstor.org/stable/2984279) for the first time. P and Q distributions are required in the form of density function. f-divrgences are a generalization of the Kullback-Leiber Divergence. An expectation of the distribution Q is multiplied by a convex function of the likelihood ratio between P and Q. Generally is not directly applicable because normally we don't have the distribution of data.

In [Nguyen, 2010](http://ieeexplore.ieee.org/document/5605355/), [Reid & Williamson, 2011](http://www.jmlr.org/papers/volume12/reid11a/reid11a.pdf) and in [Goodfellow et al., 2014](https://arxiv.org/abs/1406.2661) methods where developed for using f-divergences in problems where P is is distribution form and Q in expectation form and finally where both distributions are in expectation form. This allowed the usage of such metrics in problems where only samples of both distributions are available.

## Generative Adversarial Networks (GANs)

A neural network parametrized model $$P_{\theta}$$ called **generator** and another neural network $$ D_{\omega} $$ called **discriminator** are trained jointly using the next loss function:

$$
	\begin{equation}
		\displaystyle\min_{\theta} \displaystyle\max_{\omega} \mathbb{E}_{x \sim Q} [ log D_{\omega} (x) ] + \mathbb{E}_{x \sim P_{\theta}} [ log (1 - D_{\omega} (x)) ] 
	\end{equation}
$$

The discriminator parameters $$\omega$$ are changed for maximizing the probability of discrimination between the samples coming from the two distributions. Generator is trained for minimazing the probability of discrimination of its samples from the ones coming from the true distribution.

Goodfellow proved that optimizing GAN using such cost function is the same as minimizing the Jensen-Shanon divergence, that is one type of *f-divergence*.

We will try to generalize the objective function given above to be used with any type of f-divergence.

# f-divergences

In probability theory, an ƒ-divergence is a function $$D_f (P  || Q)$$ that measures the difference between two probability distributions P and Q. 

It helps the intuition to think of the divergence as an average, weighted by the function f, of the odds ratio given by P and Q.

## Definition

$$
\begin{equation}
D_f(Q || P) = \int_{\mathscr{X}} p(x) f ( \frac{q(x)}{p(x)} ) dx
\end{equation}
$$

where $$f$$ is a convex, so called *generator function* accomplishing the condition that $$f(1) = 0$$.

This distance is always greater than zero and is only equal to zero when both distributions are equal over all the domain $$ \mathscr(X) $$

| Name                     | $$ D_f(P || Q) $$                 | Generator $$ f(u) $$ |
|:-------------------------|:--------------------------------------------------|:-------------------------------|
|Total variation           | $$\frac{1}{2}\int \mid p(x)-q(x)\mid dx$$         | $$\frac{1}{2}\mid u-1 \mid$$   |
| Kullback-Leibler         | $$\int p(x) \log \frac{p(x)}{q(x)}dx $$            | $$ u log u $$                 |
| Reverse Kulback-Leibler  | $$\int q(x) \log \frac{q(x)}{p(x)}dx $$            | $$ - log u $$                 |
| Pearson $$\chi^2$$       | $$\int \frac{(q(x)-p(x))^2}{p(x)}dx$$             | $$ (u-1)^2 $$                  |
| Neyman $$\chi^2$$        | $$\int \frac{(p(x)-q(x))^2}{q(x)}dx$$             | $$ \frac{(1-u)^2}{u} $$        | 
| Squared Hellinger        | $$\int (\sqrt{p(x)}-\sqrt{q(x)})^2 dx$$           | $$ (\sqrt{u}-1)^2 $$           |
| Jeffrey                  | $$\int (p(x) - q(x))\log (\frac{p(x)}{q(x)})dx)$$ | $$ (u-1) \log u $$             |
| Jensen-Shannon           | $$\frac{1}{2}\int p(x) \log \frac{2p(x)}{p(x)+q(x)} + q(x) \log \frac{2q(x)}{p(x)+q(x)} dx$$ | $$-(u+1)\log \frac{1+u}{2} + u \log u$$ |
| Jensen-Shannon weighted  | $$\int p(x) \pi \log \frac{p(x)}{\pi p(x)+(1-\pi)q(x)} + (1-\pi)q(x) \log \frac{q(x)}{\pi p(x)+ (1-\pi) q(x)} dx$$ | $$\pi u \log u + (1 - \pi + \pi u) \log (1 - \pi + \pi u)$$ |
| GAN                      | $$\int p(x) \log \frac{2p(x)}{p(x)+q(x)} + q(x) \log \frac{2q(x)}{p(x)+q(x)} dx$$ - \log 4| $$u \log u - (u+1) \log (u+1)$$ |
| $$\alpha$$-divergence    | $$ \frac{1}{\alpha (\alpha - 1)} \int (p(x) [(\frac{q(x)}{p(x)})^{\alpha} - 1] - \alpha (q(x) - p(x)))dx $$ | $$ \frac{1}{\alpha (\alpha - 1)} ( u^{\alpha} - 1 - \alpha(u-1)) $$ |

# Estimation of f-divergences from samples

Nguyen et al., 2010 derive a general variational method to estimate f-divergences given only samples from P and Q. From convex analysis: every convex function $$f$$ has a *Fenchel conjugate $$f^*$$* so that $$ f(u) = \displaystyle\sup_{t \in dom_{f^*}} \{ tu - f^* (t) \} $$, ie., any convex function can be represented as point-wise maximum of linear functions. Being $$ f^*(t) $$ the intercept with the y axis for every point t.

$$
\begin{equation}
D_f(Q || P) = \int_{\mathscr{X}} p(x) f ( \frac{q(x)}{p(x)} ) dx \ge \displaystyle\sup_{T \in \mathscr{T}} ( \int_{\mathscr{x}} q(x)T(x)dx - int_{\mathscr{X}}p(x)f^*(T(x))dx) = \sup_{T \in \mathscr{T}}( \mathbb{E}_{x \sim Q}[T(x)] -  \mathbb{E}_{x \sim P}[f^*(T(x))])
\end{equation}
$$

The expressions has been converted into expectations, and now can be used in a sample based algorithm.

A caveat that has to be taken into account is that $$ f^* $$ for some divergences is only defined in a restricted domain. In those cases, the function has to be mapped into the defined domain previously to use the objective function.

## GAN discriminator-variational function correspondence

Comparing this expression with the GAN objective, we see that $$ T(x) = log(D_{\omega}(x) $$. GAN minimizes Jensen-Shanon divergence, a spetial case of f-GAN.



