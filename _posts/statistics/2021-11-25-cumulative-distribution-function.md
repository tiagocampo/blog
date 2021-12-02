---
layout: post
title: Cumulative distribution function
tags: statistics machinelearning
mathjax: true
description: The cumulative distribution function (CFD) of a real-valued random variable X, evaluated at x, is the probability that X will take a value less than or equal to x.
---

## Definition

The cumulative distribution function (CFD) of a real-valued random variable \\(X\\), evaluated at \\(x\\), is the probability that \\(X\\) will take a value less than or equal to \\(x\\).

The CFD of a real-valued random variable \\(X\\) is the function given by:

$$ F_{X}\left(x\right)=P\left(X\leq x\right) $$

where the right-hand side represents the probability that the random variable \\(X\\) takes on a value less than or equal to \\(x\\). The probability that \\(X\\) lies in the semi-close internal \\( \left[0,180\right) \\), where \\(a \ lt b\\), is therefore

$$ P\left(a \lt X \le b\right)=F_{X}\left(b\right)-F_{X}\left(a\right) $$

The probability density function of a continuous random variable can be determined from the cumulative distribution function by differentiating the CFD

$$f\left(x\right)=\frac{\textrm{d}}{\textrm{dx}}F\left(x\right)$$

as long as the derivative exists.

The CFD of a continuous random variable \\(X\\) can be expressed as the integral of its probability density function \\(f_X\\) as follows:

$$F_{X}\left(x\right)=\int_{-\infty}^{x}f_{X}\left(t\right)\textrm{d}t$$


## Examples

Suppose \\(X\\) is uniformly distributed in the unit interval \\( \left[0,1 \right] \\). Then the CFD of (\\X\\) is given by

$$F_{X}\left(x\right)=\begin{cases}
0: & x<0\\
x: & 0\le x\le1\\
1: & x>1
\end{cases}$$

Suppose instead that \\(X\\) takes only the discrete values 0 and 1, with equal probability. Then the CFD of \\(X\\) is given by

$$F_{X}\left(x\right)=\begin{cases}
0: & x<0\\
\frac{1}{2}: & 0\le x<1\\
1: & x>1
\end{cases}$$

<br/><br/>
<div class="card center-image" style="max-width: 20rem;">
  <img src="{{site.baseurl}}/assets/images/fig1_CDF.svg" class="card-img-top" alt="...">
  <div class="card-body">
    <p class="card-text">From top to bottom, the CFD of a discrete probability distribution and of a continuous probability distribution.</p>
  </div>
</div>


## References

- [Khan Academy](https://www.youtube.com/c/khanacademy){:target="_blank"}
- [Wikipedia](https://en.wikipedia.org/wiki/Cumulative_distribution_function){:target="_blank"}