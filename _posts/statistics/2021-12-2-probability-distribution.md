---
layout: post
title: Probability distribution
tags: statistics machinelearning
mathjax: true
description: A probability distribution is a mathematical description of the probabilities of events, subsets of the sample space. The sample space is the set of all possible outcomes of a random phenomenon being observed.
---

## Introduction

A probability distribution is a mathematical description of the probabilities of events, subsets of the sample space. The sample space, often denoted by \\(\Omega\\), is the set of all possible outcomes of a random phenomenon being observed.

To define probability distributions for the specific case of discrete random variable, it is sufficient to specify a probability mass function \\(p\\) assigning a probability to each possible outcome: for example, when trowing a fair die, each of the six values 1 to 6 has the probability 1/6. 

In contrast, when a random variable takes values from a continuum then typically, any individual outcome has probability zero and only events that include infinitely many outcomes, such as intervals, can have positive probability. For example consider the _exact_ time a runner crosses the finish line assuming _infinity_ precision. The probability that it crosses the line at _exactly_ 10 seconds is zero, as it most likely have some non-zero decimal digits.

Continuous probability distributions can be described in several ways. The PDF describes infinitesimal probability of any given value, and the probability  that the outcome lies in a given interval can be computed by integrating the probability density function over such interval. An alternative description of the distribution is by means of the CDF which describes the probability that the random variable is no larger than a given value. The CDF is the area under the PDF from \\(-\infty\\) to \\(x\\), as described in the figure bellow.

<br/>
<div class="card center-image" style="max-width: 40rem;">
  <img src="{{site.baseurl}}/assets/images/fig1_PD.png" class="card-img-top" alt="...">
  <div class="card-body">
    <p class="card-text">On the left is the probability density function. On the right is the cumulative distribution function, which is the area under the probability density curve.</p>
  </div>
</div>
<br/>

## Discrete probability distribution

A discrete probability distribution is the probability distribution of a random variable that can take only a countable number of values. In the case where the range of values is countably infinite, these values have to decline to zero fast enough for the probabilities to add up to 1.

Well-known discrete probability distributions used in statistical modeling include the Poisson distribution, the Bernoulli distribution, the binomial distribution, the geometric distribution, and the negative binomial distribution. Additionally, the discrete uniform distribution is commonly used in computer programs that make equal-probability random selection between a number of choices.

When a sample (a set of observations) is drawn from a large population, the sample points have an empirical distribution that is discrete, and which provides information about the population distribution.

<br/>
<div class="card center-image" style="max-width: 40rem;">
  <img src="{{site.baseurl}}/assets/images/fig2_PD.svg" class="card-img-top" alt="...">
  <div class="card-body">
    <p class="card-text">The probability mass function of a discrete probability distribution. The probabilities of the singletons {1}, {3}, and {7} are respectively 0.2, 0.5, 0.3. A set not containing any of these points has probability zero.</p>
  </div>
</div>
<br/>

### Cumulative distribution function

Equivalently to the above, a discrete random variable can be defined as a random variable whose cumulative distribution function (CDF) increases only by jump discontinuities - that is, its CDF increases only where it jumps to a higher value, and is constant between those jumps. As seen in the figure below. Note however that the points where the CDF jumps may form a dense set of the real numbers. The points where jumps occur are precisely the values which the random variable may take. 

<br/>
<div class="card center-image" style="max-width: 40rem;">
  <img src="{{site.baseurl}}/assets/images/fig3_PD.svg" class="card-img-top" alt="...">
  <div class="card-body">
    <p class="card-text">The CDF of a discrete probability distribution</p>
  </div>
</div>
<br/>

## Continuous probability distribution

A continuous probability distribution is a probability distribution whose support is an uncountable set, such as an interval in the real line. They are uniquely characterized by a CDF that can be used to calculate the probability for each subset of the support. There are many examples of continuous probability distributions: normal, uniform, chi-squared, and others.

A random variable \\( X \\) has a continuous probability distribution if there is a function $$ f:\mathbb{R}\rightarrow\left[0,\infty\right]  $$ such that for each interval \\(I\subset\mathbb{R}\\) the probability of \\(X\\) belonging to \\(I\\) is given by the integral of \\(f\\) over \\(I\\). For example, \\(I=\left[a,b\right]\\), then we would have

$$P\left[a\leq X\leq b\right]=\int_{a}^{b}f\left(x\right)\textrm{d}x$$

In particular, the probability for \\(X\\) to take any single value (\a\\) is zero. 
### Cumulative distribution function

A variable that satisfies the above is called a continuous random variable. Its CDF is defined as

$$F\left(X\right)=P\left[-\infty\leq X\leq x\right]=\int_{\infty}^{x}f\left(x\right)\textrm{d}x$$

which has, among other properties, the property that \\(F\left(X\right)\\) is non-decreasing as shown in the figure below.

<br/>
<div class="card center-image" style="max-width: 40rem;">
  <img src="{{site.baseurl}}/assets/images/fig4_PD.svg" class="card-img-top" alt="...">
  <div class="card-body">
    <p class="card-text">The CDF of a continuous probability distribution</p>
  </div>
</div>
<br/>


## References

- [Wikipedia](https://en.wikipedia.org/wiki/Probability_distribution){:target="_blank"}