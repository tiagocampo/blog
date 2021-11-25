---
layout: post
title: Probability density function
tags: statistics
mathjax: true
description: A probability density function (PDF) is a function whose value at any given sample (or point) in the sample space can be interpreted as providing a _relative likelihood_ that the value of the random variable would be close to that sample. In other words, while the _absolute likelihood_ for a continuous random variable to take on any particular value is 0, the value of the PDF at two different samples can be used to infer how much  likely it is that the random variable would be close to one sample compared to the other sample.
---

## Definition

A probability density function (PDF) is a function whose value at any given sample (or point) in the sample space can be interpreted as providing a _relative likelihood_ that the value of the random variable would be close to that sample. In other words, while the _absolute likelihood_ for a continuous random variable to take on any particular value is 0, the value of the PDF at two different samples can be used to infer how much likely it is that the random variable would be close to one sample compared to the other sample.

In a more precise sense, the PDF is used to specify the probability of the random variable falling within a particular range of values, as opposed to taking on any one value. This probability is given by the integral of this variable's PDF over that range. The probability density function is nonnegative everywhere, and its integral over the entire space is equal to 1. 

A PDF is most commonly associated with absolutely continuous univariate distributions. A random variable \\(X\\) has density \\(\f_X\), where \\(f_X\\) is a non-negative integrable function, if:

$$\textrm{Pr}\left[a\le X\le b\right]=\int_{a}^{b}f_{X}\left(x\right)\textrm{d}x$$

Hence, if \\(F_X\\) is the CDM of \\(X\\), then

$$F_{X}=\int_{-\infty}^{x}f_{X}\left(u\right)\textrm{d}u$$

and (if \\(f_X\\) is continuous at x)

$$f_{X}\left(x\right)=\frac{\textrm{d}}{\textrm{d}x}F_{X}\left(x\right)$$

Intuitively, one can think of \\(f_X\left(x\right)\textrm{d}x\\) as being the probability of \\(X\\) falling within the infinitesimal interval \\(\left[x,x+\textrm{d}x\right]\\).
## References

- [Khan Academy](https://www.youtube.com/c/khanacademy){:target="_blank"}
- [Wikipedia](https://en.wikipedia.org/wiki/Probability_density_function){:target="_blank"}