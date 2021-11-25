---
layout: post
title: Probability distribution
tags: statistics
mathjax: true
description: 
---

## Introduction

A probability distribution is a mathematical description of the probabilities of events, subsets of the sample space. The sample space, often denoted by \\(\Omega\\), is the set of all possible outcomes of a random phenomenon being observed.

To define probability distributions for the specific case of discrete random variable, it is sufficient to specify a probability mass function \\(p\\) assigning a probability to each possible outcome: for example, when trowing a fair die, each of the six values 1 to 6 has the probability 1/6. 

In contrast, when a random variable takes values from a continuum then typically, any individual outcome has probability zero and only events that include infinitely many outcomes, such as intervals, can have positive probability. For example consider the _exact_ time a runner crosses the finish line assuming _infinity_ precision. The probability that it crosses the line at _exactly_ 10 seconds is zero, as it most likely have some non-zero decimal digits.

Continuous probability distributions can be described in several ways. The PDF describes infinitesimal probability of any given value, and the probability  that the outcome lies in a given internal can be computed by integrating the probability density function over such interval. An alternative description of the distribution is by means of the CDF which describes the probability that the random variable is no larger than a given value. The CDF is the area under the PDF from \\(-\infty\\) to \\(x\\), as described in the figure bellow.

<br/>
<div class="card center-image" style="max-width: 40rem;">
  <img src="{{site.baseurl}}/assets/images/fig1_PF.png" class="card-img-top" alt="...">
  <div class="card-body">
    <p class="card-text">On the left is the probability density function. On the right is the cumulative distribution function, which is the area under the probability density curve.</p>
  </div>
</div>
<br/>

## References

- [Wikipedia](https://en.wikipedia.org/wiki/Probability_distribution){:target="_blank"}