---
layout: post
title: Distributions' properties part 1
tags: statistics machinelearning
mathjax: true
description: Here we discuss and compare expected value (or mean), median and mode
---

* Do not remove this line (it will not be displayed)
{:toc}

---

# Introductin

There are some quantities that are often used to described _macro_ characteristics of probabilities distributions. Such properties will be discussed bellow.

## Expected value (or mean)

The expected value of a random variable \\(X\\), often denoted as \\(E(X)\\), is a generalization of the weighted average, and is intuitively the arithmetic mean of a large number of independent realizations of \\(X\\). The expected value is also known as the expectation, mean, average or first moment.

### Discrete case

Let \\(X\\) be a discrete random variable with a finite number of finite outcomes $$x_1, x_2, \cdots,x_k$$ occurring with probabilities $$p_1,p_2,\cdots,p_k$$ respectively. The expectation of \\(X\\) is defined as

$$E\left(X\right)=\sum_{i=1}^{k}x_{i}p_{i}=x_{1}p_{1}+x_{2}p_{2}+\cdots+x_{k}p_{k}$$

Since $$p_1+p_2+\cdots+p_k=1$$, the expected values is the weighted sum of the \\(x_i\\) values, with the probabilities \\(p_i\\) as weights.

### Absolutely continuous case

If \\(X\\) is a random variable with a probability density function of \\(f\left(x\right)\\), then the expected value is defined as

$$E\left(X\right)=\int xf\left(x\right)\textrm{d}x$$

### Examples

#### Roll of dice

Let \\(X\\) represent the outcome of a roll of a fair six-sided die. The possible values for \\(X\\) are 1, 2, 3, 4, 5 and 6, all of which are equally likely to occur with a probability of \\(\frac{1}{6}\\). The expectation of \\(X\\) is

$$E\left(X\right)=1\cdot\frac{1}{6}+2\cdot\frac{1}{6}+3\cdot\frac{1}{6}+4\cdot\frac{1}{6}+5\cdot\frac{1}{6}+6\cdot\frac{1}{6}=3.5$$

If one rolls the die \\(n\\) times and computes the average (arithmetic mean) of the results, then as \\(n\\) grows, the average will almost surely converge to the expected value, a fact known as the strong law of large numbers. See in the figure bellow an illustration of the convergence cited above.

<br/>
<div class="card center-image" style="max-width: 40rem;">
  <img src="{{site.baseurl}}/assets/images/fig1_PPD.svg" class="card-img-top" alt="...">
  <div class="card-body">
    <p class="card-text">An illustration of the convergence of sequence averages of rolls of a die to the expected value of 3.5 as the number of rolls (trials) grows.</p>
  </div>
</div>
<br/>

#### Roulette game

Suppose random variable \\(X\\) represents the (monetary) outcome of a $1 bet on a single number. If the bet wins (which happens with probability $$\frac{1}{38}$$, the payoff is $35; otherwise the player loses the bet. The expected profit from such a bet will be

$$E\left(\textrm{gain from \$1 bet}\right)=-\$1\cdot\frac{37}{38}+\$35\cdot\frac{1}{38}=-\$\frac{1}{19}$$

That is, the bet of $1 standsto lose \\(-$\frac{1}{19}\\), so its expected value is \\(-$\frac{1}{19}\\).

#### Countably infinite case

Let \\(X\\) be a non-negative random variable with a countable set of outcomes \\(x_1,x_2,\cdots\\), occurring wth probabilities \\(p_1,p_2,\cdots\\), respectively. Analogous to the discrete case, the expected value of \\( X \\) is then defined as the series

$$E\left(X\right)=\sum_{i=1}^{\infty}x_{i}p_{i}$$

Note that since \\(x_i p_i \geq 0\\), the infinite sum is well-defines and does not depend on the order in which it is computed. Unlike the finite case, the expectation here can be equal to infinity, if the infinite sum above increases without bonds.

The genera case is more complex and it will be not discussed here.


## Median

The **median** is the value separating the higher half from the lower half of a data sample, a population ar a probability distribution. For a data set, it may be thought of as _the middle_ value. The basic feature of the median in describing data compared to the mean is that it is not skewed by a small proportion of extremely large or small values, and therefore provides a better representation of a _typical_ value.

### Finite data set of numbers

If the data set has an odd number of observation, the middle one is selected. For example 1, 3, 3, **6**, 7, 8, 9 has a median of _6_.

If the data set has an even number of observation, there is no distinct middle value and the median is usually defined to be the arithmetic mean of the two middle values. For example 1, 2, 3, **4**, **5**, 6, 8, 9 has a median value of 4.5, that is (4+5)/2. 

### Probability distributions

For any real-valued probability distribution with cumulative distribution function \\(F\\), a median is defined as any real number \\(m\\) that satisfies the inequalities $$\int_{\left(-\infty,m\right]}\textrm{d}F\left(X\right)\geq\frac{1}{2}$$ and $$\int_{\left[m,\infty\right)}\textrm{d}F\left(X\right)\geq\frac{1}{2}$$

## Mode

The **mode** is the value that appears most often in a set of data values. If \\(X\\) is a discrete random variable, the mode is the value \\(x\\) at which the probability mass function takes its maximum value. In other words, it is the value that is most likely to be sampled.

The mode is not necessarily unique to a given distribution, since the probability mass function may take the same maximum value at several points \\(x_1,x_2\\), etc. The most extreme case occurs in uniform distributions, where all values occur equally frequently.

When the probability density function of a continuous distribution has multiple maxima it is common to refer to all of the local maxima as modes of the distribution.

### Mode of a sample

For example, the mode of the sample 1, 3, 6, 6, 6, 7, 7, 12, 12, 17 is **6**. Given the list of data 1, 1, 2, 4, 4 its mode is not unique. 

For a sample from a continuous distribution the concept is unusable in its raw form, since no two values will be exactly the same, so each value will occur precisely once. In order to estimate the mode of the underlying distribution, the usual practice is to discretize the data by assigning frequency values to intervals of equal distance, as for making a histogram. The mode is then the value where the histogram reaches its peak.

# Comparison of mean, median and mode

| Type | Description | Example | Result |
| --------------------- | --------------------- | --------------------- | --------------------- |
| Arithmetic mean | sum of values divided by number of values | (1+2+2+3+4+7+9)/7 | 4 |
| Median | middle value separating the greater and lesses halves | 1, 2, 2, **3**, 4 ,7, 9| 3 |
| Mode | most frequent value | 1, **2**, **2**, 3, 4, 7, 9 | 2 |

<br/>
<div class="card center-image" style="max-width: 40rem;">
  <img src="{{site.baseurl}}/assets/images/fig2_PPD.svg" class="card-img-top" alt="...">
  <div class="card-body">
    <p class="card-text">Geometric visualisation of the mode, median and mean of an arbitrary probability density function.</p>
  </div>
</div>
<br/>

# Example for a skewed distribution

A well-known class of distributions that can be arbitrarily skewed is given by the log-normal distribution. It is obtained by transforming a random variable \\(X\\) having a normal distribution into random variable $$Y = e^X$$. Then the logarithm of random variable \\(Y\\) is normally distributed, hence the name. 

When \\(X\\) has standard deviation $$\sigma = 0.25$$, the distribution of \\(Y\\) is weakly skewed

$$\begin{cases}
\textrm{mean} & e^{\mu+\sigma^{2}/2}\approx1.032\\
\textrm{mode} & e^{\mu-\sigma^{2}}\approx0.939\\
\textrm{median} & e^{\mu}\approx1
\end{cases}$$

When \\(X\\) has large standard deviation, $$\sigma = 1$$, the distribution of \\(Y\\) is strongly skewed

$$\begin{cases}
\textrm{mean} & e^{\mu+\sigma^{2}/2}\approx1.649\\
\textrm{mode} & e^{\mu-\sigma^{2}}\approx0.368\\
\textrm{median} & e^{\mu}\approx1
\end{cases}$$

We can see better in the figure below, assuming $$\mu = 0$$

<br/>
<div class="card center-image" style="max-width: 40rem;">
  <img src="{{site.baseurl}}/assets/images/fig3_PPD.svg" class="card-img-top" alt="...">
  <div class="card-body">
    <p class="card-text">Comparison of mean, median and mode of two log-normal distributions with different skewness.</p>
  </div>
</div>
<br/>

# References

- [Wikipedia Expected Value](https://en.wikipedia.org/wiki/Expected_value){:target="_blank"}
- [Wikipedia Median](https://en.wikipedia.org/wiki/Median){:target="_blank"}
- [Wikipedia Mode](https://en.wikipedia.org/wiki/Mode_(statistics)){:target="_blank"}