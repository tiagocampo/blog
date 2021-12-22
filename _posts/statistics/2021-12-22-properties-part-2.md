---
layout: post
title: Distributions' properties part 2
tags: statistics machine-learning
mathjax: true
description: Here we discuss about variance, covariance, standard deviation and quantiles
---

* Do not remove this line (it will not be displayed)
{:toc}

---

# Variance

A variance is the expectation of the squared deviation of a random variable from its population mean or sample mean. Variance is a measure of dispersion, meaning it is a measure of how far a set of numbers is spread out from their average value. 

## Definition

The variance of a random variable \\(X\\) is the expected value of the squared deviation from the mean of \\(X\\), $$\mu = E\left[X\right]$$:

$$\textrm{Var}\left(X\right) = E\left[\left(X-\mu\right)\right].$$

The variance can also be thought of as the covariance of a random variable with itself:

$$\textrm{Var} = \textrm{Cor}\left(X,X\right).$$

The expression for the variance can be expanded as follows:

$$\begin{align*}
\textrm{Var}\left(X\right) & =E\left[\left(X-E\left[X\right]\right)^{2}\right]\\
 & =E\left[X^{2}-2XE\left[X\right]+E\left[X\right]^{2}\right]\\
 & =E\left[X^{2}\right]-2E\left[X\right]E\left[X\right]+E\left[X\right]^{2}\\
 & =E\left[X^{2}\right]-E\left[X\right]^{2}
\end{align*}$$

In other words, the variance of \\(X\\) is equal to the mean of the square of \\(X\\) minus the square of the mean of \\(X\\). This equation should not be used for computations using floating point arithmetic, because it suffers from catastrophic cancellation if the two components of the equation are similar in magnitude.

### Discrete random varible

If the generator of random variable \\(X\\) is discrete with probability mass function \\( x_1 \mapsto p_1, x_2 \mapsto p_2, \cdots, x_n \mapsto p_n \\), then

$$\textrm{Var}\left(X\right) \sum_{i=1}^{n}p_i \cdot \left(x_i-\mu\right)^2,$$

where \\(\mu\\) is the expected value. That is,

$$\mu = \sum_{i=1}^n p_i x_i.$$

(When such a discrete weighted variance is specified by weights whose sum is not 1, then on divides by the sum of the weights.)

The Variance of a collection of \\(n\\) equally likely values can be written as

$$\textrm{Var}\left(X\right) = \frac{1}{n}\sum_{i=1}^n \left(x_i-\mu\right)^2$$ 

where \\(\mu\\) is the average value, that is,

$$\mu = \frac{1}{n}\sum_{i=1}^n x_i.$$

The variance of a set of \\(n\\) equally likely values can be equivalently expressed, without directly referring to the mean, in terms of squared deviations of all points from each other:

$$\textrm{Var}\left(X\right) = \frac{1}{n^2}\sum_{i=1}^n\sum_{j=1}^n\frac{1}{2}\left(x_i-x_j\right)^2=\frac{1}{n^2} \sum_{i} \sum_{j \gt i} \left(x_i-x_j\right)^2.$$

### Absolutely continuous random variable

If the random variable \\(X\\) has a probability density function \\(f\left(x\right)\\), and \\(F\left(X\right)\\) is the corresponding cumulative distribution function, then

$$\begin{align*}
\textrm{Var}\left(X\right)=\sigma^{2} & =\int_{\mathbb{R}}\left(x-\mu\right)^{2}f\left(x\right)\textrm{d}x\\
 & =\int_{\mathbb{R}}x^{2}f\left(x\right)\textrm{d}x-2\mu\int_{\mathbb{R}}xf\left(x\right)\textrm{d}x+\mu^{2}\int_{\mathbb{R}}f\left(x\right)\textrm{d}x\\
 & =\int_{\mathbb{R}}x^{2}\textrm{d}F\left(x\right)-2\mu\int_{\mathbb{R}}x\textrm{d}F\left(x\right)+\mu^{2}\int_{\mathbb{R}}\textrm{d}F\left(x\right)\\
 & =\int_{\mathbb{R}}x^{2}\textrm{d}F\left(x\right)-2\mu\cdot\mu+\mu^{2}\cdot1\\
 & =\int_{\mathbb{R}}x^{2}\textrm{d}F\left(x\right)-\mu^{2}
\end{align*}$$

or equivalently,

$$\textrm{Var}\left(X\right)=\int_{\mathbb{R}}x^{2}f\left(x\right)\textrm{d}x-\mu^{2}$$

where \\(\mu\\) is the expected value of \\(X\\) given by

$$\mu=\int_{\mathbb{R}}xf\left(x\right)\textrm{d}x=\int_{\mathbb{R}}x\textrm{d}F\left(x\right)$$

### Examples

#### Fair die

A fair six-sided die can be modeled as a discrete random variable, \\(X\\), with outcomes 1 through 6, each with equal probability 1/6. The expected value of \\(X\\) is $$\left(1+2+3+4+5+6\right)/6=7/2$$. Therefore, the variance of \\(X\\) is

$$\begin{align*}
\textrm{Var}\left(X\right) & =\sum_{i=1}^{6}\frac{1}{6}\left(i-\frac{7}{2}\right)\\
 & =\frac{1}{6}\left[\left(-5/2\right)^{2}+\left(-3/2\right)^{2}+\left(-1/2\right)^{2}+\left(1/2\right)^{2}+\left(3/2\right)^{2}+\left(5/2\right)^{2}\right]\\
 & =\frac{35}{12}\approx2.92.
\end{align*}$$

The general formula for the variance of the outcome, \\(X\\), of a \\(n\\)-sided die is

$$\begin{align*}
\textrm{Var}\left(X\right) & =E\left[X^{2}\right]-E\left[X\right]^{2}\\
 & =\frac{1}{n}\sum_{i=1}^{n}i^{2}-\left(\frac{1}{n}\sum_{i=1}^{n}i\right)^{2}\\
 & =\frac{\left(n+1\right)\left(2n+1\right)}{6}-\left(\frac{n+1}{2}\right)^{2}\\
 & =\frac{n^{2}-1}{12}.
\end{align*}$$

#### Exponential distribution

The exponential distribution with parameter \\(\lambda\\) is a continuous distribution whose probability density function is given by

$$f\left(x\right) = \lambda e^{-\lambda x}$$

on the interval $$(\left[0,\infty \right)$$. It mean can be show to be

$$E\left[X\right]=\int_0^\infty \lambda x e^{-\lambda x} \textrm{d}x=\frac{1}{\lambda}$$

Using integration by parts and making use of the expected value already calculated, we have:

$$\begin{align*}
E\left[X^{2}\right] & =\int_{0}^{\infty}\lambda xe^{-\lambda x}\textrm{d}x\\
 & =\left[-x^{2}e^{-\lambda x}\right]_{0}^{\infty}+\int_{0}^{\infty}2xe^{-\lambda x}\textrm{d}x\\
 & =0+\frac{2}{\lambda}E\left[X\right]\\
 & =\frac{2}{\lambda^{2}}
\end{align*}$$

Thus, the variance of \\(X\\) is given by

$$\textrm{Var}\left(X\right)=E\left[X^{2}\right]-E\left[X\right]^{2}=\frac{2}{\lambda^{2}}-\left(\frac{1}{\lambda}\right)^{2}=\frac{1}{\lambda^{2}}$$

## Some properties

### Sum of uncorrelated variables (Bienaymé formula)

One reason for the use of the variance in preference to other measures of dispersion is that the variance of the sum (or the difference) of uncorrelated random variables is the sum of their variances:

$$\textrm{Var}\left(\sum_{i=1}^{n}X_{i}\right)=\sum_{i=1}^{n}\textrm{Var}\left(X_{i}\right)$$

### Sum of correlated variables

In general, the variance of the sum of \\(n\\) variables is the sum of their covariances:

$$\textrm{Var}\left(\sum_{i=1}^{n}X_{i}\right)=\sum_{i=1}^{n}\textrm{Cov}\left(X_{i},X_{j}\right)=\sum_{i=1}^{n}\textrm{Var}\left(X_{i}\right)+2\sum_{1\le i<j\leq n}\textrm{Cov}\left(X_{i},X_{j}\right)$$

## Population variance and sample variance

Real-world observations such as the measurements of yesterday's rain throughout the day typically cannot be complete sets of all possible observations that could be made. As such, the variance calculated from the finite set will in general not match the variance that would have been calculated from the full population of possibles observations. This means that one estimates the mean and variance from a limited set of observations by using an estimator equation. The estimator is a function of the sample of n observations drawn without observational bias from the whole population of potential observations. In this example that sample would be the set of actual measurements of yesterday's rainfall from available rain gauges within the geography of interest.

The simplest estimators for population mean and population variance are simply the mean and variance of the sample, the sample mean and (uncorrected) sample variance – these are consistent estimators (they converge to the correct value as the number of samples increases), but can be improved in two ways.

Firstly, if the true population mean is unknown, then the sample variance (which uses the sample mean in place of the true mean) is a biased estimator: it underestimates the variance by a factor of (n − 1) / n; correcting by this factor (dividing by n − 1 instead of n) is called Bessel's correction. The resulting estimator is unbiased, and is called the (corrected) sample variance or unbiased sample variance. For example, when n = 1 the variance of a single observation about the sample mean (itself) is obviously zero regardless of the population variance. If the mean is determined in some other way than from the same samples used to estimate the variance then this bias does not arise and the variance can safely be estimated as that of the samples about the (independently known) mean.

Secondly, the sample variance does not generally minimize mean squared error between sample variance and population variance. Correcting for bias often makes this worse: one can always choose a scale factor that performs better than the corrected sample variance, though the optimal scale factor depends on the excess kurtosis of the population, and introduces bias. This always consists of scaling down the unbiased estimator (dividing by a number larger than n − 1), and is a simple example of a shrinkage estimator: one "shrinks" the unbiased estimator towards zero. For the normal distribution, dividing by n + 1 (instead of n − 1 or n) minimizes mean squared error. The resulting estimator is biased, however, and is known as the biased sample variation.

The sample variance is computed as an average of squared deviations about the (sample) mean, by dividing by n. However, using values other than n improves the estimator in various ways. Four common values for the denominator are n, n − 1, n + 1, and n − 1.5: n is the simplest (population variance of the sample), n − 1 eliminates bias, n + 1 minimizes mean squared error for the normal distribution, and n − 1.5 mostly eliminates bias in unbiased estimation of standard deviation for the normal distribution. 

# Covariance

Covariance is a measure of the joint variability of two random variables. The sign of the covariance shows the tendency in the linear relationship between the variables. The magnitude of the covariance, however, being not normalized, carries less meaning. Moreover, the normalized version of the covariance, the correlation coefficient, shows by its magnitude the strength of the linear relation.

## Definition

For two jointly distributed real-valued random variables, \\(X\\) and \\(Y\\) with finite second moments, the covariance is defined as the expected value (or mean) of the product of their deviations from their individual expected values:

$$\textrm{cov}\left(X,Y\right)=E\left[\left(X-E\left[X\right]\right)\left(Y-E\left[Y\right]\right)\right]$$

The covariance is also sometimes denoted as \\(\sigma_{XY}\\) or \\(\sigma\left(X,Y\right)\\), in analogy to variance. By using the linearity property of expectations, the above expression can be simplified to:

$$\begin{align*}
\textrm{cov}\left(X,Y\right) & =E\left[\left(X-E\left[X\right]\right)\left(Y-E\left[Y\right]\right)\right]\\
 & =E\left[XY-XE\left[Y\right]-E\left[X\right]Y+E\left[X\right]E\left[Y\right]\right]\\
 & =E\left[XY\right]+E\left[X\right]E\left[Y\right]
\end{align*}$$

but this equation is susceptible to the catastrophic cancellation.
## Covariance with itself

The variance is a special case of the covariance in which the two variables are identical:

$$\textrm{cov}\left(X,X\right)=\textrm{var}\left(X\right)\equiv\sigma^{2}\left(X\right)\equiv\sigma_{X}^{2}$$


# Standard deviation

The standard deviation is a measure of the amount of variation or dispersion of a set of values. A low standard deviation indicates that the values tend to be close to the mean (expected value) of the set, while a high standard deviation indicates that the values are spread out over a wider range.

## Definition

The standard deviation is the square root of variance

## Examples

### Population standard deviation of grades of eight students

Suppose that the entire population of interest is eight students in a particular class. The marks of a class of eight students are the following eight values: 2, 4, 4, 4, 5, 5, 7, 9.

These eight data points have the mean (average) of 5:

$$ \mu = \frac{2+4+4+4+5+5+7+9}{8} = \frac{40}{8} = 5 $$

First calculate the deviations of each data point from the mean, as square the result of each:

$$\left(2-5\right)^{2}=9,\ \left(4-5\right)^{2}=1,\cdots,\left(9-5\right)^{2}=16$$

The variance is the mean of these values:

$$\sigma^{2}=\frac{9+1+1+1+0+0+4+16}{8}=\frac{32}{8}=4$$

and the population standard deviation is equal to the square root of the variance:

$$\sigma=\sqrt{4}=2$$

# Quantile

Quantiles are cut points dividing the range of a probability distribution into continuous intervals with equal probabilities, or dividing the observations in a sample in the same way.

\\(q\\)-quantiles are values that partition a finite set of values in \\(q\\) subsets of (nearly) equal sizes. There are \\(q\\)-1 of the \\(q\\)-quantiles, one for each integer \\(k\\) satisfying $$0 < k < q$$. In some cases the value of a quantile may not be uniquely determined, as can be the case for the median (2-quantile) of a uniform probability distribution on a set of even size.

## Specialized quantiles

Some \\(q\\)-quantiles have special names:

    - The only 2-quantile is calle median
    - The 3-quantiles are called tertiles or terciles \\(rightarrow T\\)
    - The 4-quantiles are called quartiles (rightarrow Q\\)
    - etc.

## Quantiles of a population

As in the computation of, for example, standard deviation, the estimation of a quantile depends upon whether one is operating with a statistical population or with a sample drawn from it. For a population, of discrete values or for a continuous population density, the \\(k\\)-th \\(q\\)-quantile is the data value where the cumulative distribution function crosses \\(\frac{k}{q}\\). That is, \\(x\\) is a \\(k\\)-th \\(q\\)-quantile for a variable \\(X\\) if

$$ \textrm{Pr}\left[X < x\right] \leq \frac{k}{q}$$
 
For a finite population of \\(N\\) equally probable values indexed \\(1,\cdots,N\\)from lowest to highest, the \\(k\\)-th \\(q\\)-quantile of this population can equivalently be computed via the value of $$I_P = N \frac{k}{q}$$ rounding up to the next integer.

# References

- [Wikipedia Variance](https://en.wikipedia.org/wiki/Variance){:target="_blank"}
- [Wikipedia Covariance](https://en.wikipedia.org/wiki/Covariance){:target="_blank"}
- [Wikipedia Standard Deviation](https://en.wikipedia.org/wiki/Standard_deviation){:target="_blank"}
- [Wikipedia Quantile](https://en.wikipedia.org/wiki/Quantile){:target="_blank"}

