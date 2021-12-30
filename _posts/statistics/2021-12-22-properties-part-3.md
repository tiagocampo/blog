---
layout: post
title: Distributions' properties part 3
tags: statistics theory machine-learning
mathjax: true
description: Here we define cumulant, skewness and kurtosis
---

* Do not remove this line (it will not be displayed)
{:toc}

---

# Cumulant

The cumulants \\(\kappa_n\\) of a probability distribution are a set of quantiles that provide an alternative to the moments of the distribution.

## Definition

The cumulants of a random variable \\(X\\) are defined using the cumulant-generating function \\(K\left(t\right)\\), which is the natural logarithm of the moment-generating function:

$$ K\left(t\right) = \textrm{ln}E\left[e^{tX}\right] $$

The cumulants \\(\kappa_n\\) are obtained from a power series expansion of the cumulant generating function:

$$K\left(t\right)=\sum_{n=1}^{\infty}\kappa_{n}\frac{t^{n}}{n!}=\kappa_{1}\frac{t}{1!}+\kappa_{2}\frac{t^{2}}{2!}+\cdots=\mu t+\sigma^{2}\frac{t^{2}}{2}+\cdots$$

## The first several cumulants as functions of the moments

All of the higher cumulants are polynomial functions of the central moments, with integer coefficients, but only in degrees 2 and 3 are the cumulants actually central moments.

 - \\(\kappa_1\\) = E(X)
 - \\(\kappa_2\\) = \\(\textrm{var}(X)\\)
 - \\(\kappa_3\\) = \\(E\left[\left(X-E(X)\right)^3\right]\\)
 - etc

# Skewness

Skewness is a measure of the asymmetry of the probability distribution of a real-valued random variable about its mean.

For a unimodal distribution, negative skew commonly indicates that the tail is on the left side of the distribution, and a positive skew indicates that the tail is on the right. In cases where on tail is long but the other tail is fat, skewness does not obey a simple rule.

<br/>
<div class="card center-image" style="max-width: 40rem;">
  <img src="{{site.baseurl}}/assets/images/fig4_PPD.svg" class="card-img-top" alt="...">
  <div class="card-body">
    <p class="card-text">Skewness</p>
  </div>
</div>
<br/>

## Definition

The skewness of a random variable \\(X\\) is the third standardized moment \\(\tilde{\mu}_3\\), defined as:

$$\tilde{\mu}_{3}=E\left[\left(\frac{X-\mu}{\sigma}\right)^{3}\right]=\frac{\mu_{3}}{\sigma^{3}}=\frac{E\left[\left(X-\mu\right)^{3}\right]}{\left(E\left[\left(X-\mu\right)^{2}\right]\right)^{3/2}}=\frac{\kappa_{3}}{\kappa_{2}^{3/2}}$$

where \\(\mu\\) is the mean, \\(\sigma\\) is the standard deviation, \\(E\\) is the expectation operator, \\(\mu_3\\) is the third central moment, and \\(\kappa_t\\) are the \\(t\\)-th cumulants.

# Kurtosis

Kurtosis is a measure of the _tailedness_ of the probability distribution of a real-valued random variable. The kurtosis of any univariate normal distribution is 3. On one hand distributions with kurtosis less than 3 produces fewer extreme outliers than does the normal distributions (uniform distribution is an example). On the other hand, distributions with kurtosis greater than 3 produces more outliers that does the normal distribution (Laplace distribution is an example).

# Definition

The kurtosis is the fourth standardized moment, defined as

$$\textrm{Kurt}\left[X\right]=E\left[\left(\frac{X-\mu}{\sigma}\right)^{4}\right]=\frac{E\left[\left(X-\mu\right)^{4}\right]}{\left(E\left[\left(X-\mu\right)^{2}\right]\right)^{2}}=\frac{\mu_{4}}{\sigma^{4}}$$ 

where \\(\mu_4\\) is the fourth central moment and \\(\sigma\\) is the standard deviation.
 
# References

- [Wikipedia Cumulants](https://en.wikipedia.org/wiki/Cumulant){:target="_blank"}
- [Wikipedia Skewness](https://en.wikipedia.org/wiki/Skewness){:target="_blank"}
- [Wikipedia Kurtosis](https://en.wikipedia.org/wiki/Kurtosis){:target="_blank"}
