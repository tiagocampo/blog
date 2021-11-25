---
layout: post
title: Random Variables
categories: statistics
mathjax: true
description: A random variable is a variable whose values depend on outcomes of a random phenomenon. Instead of a so called _normal_ variable, the random variable's possible values might represent the possible outcomes of a yet-to-be-performed experiment, or of a past experiment whose already-existing value is uncertain.
---
## Definition

A random variable is a variable whose values depend on outcomes of a random phenomenon. Instead of a so called _normal_ variable, the random variable's possible values might represent the possible outcomes of a yet-to-be-performed experiment, or of a past experiment whose already-existing value is uncertain. They may also conceptually represent either the results of an _objectively_ random process (such as rolling a die) or the _subjective_ randomness that results from incomplete knowledge of a quantity.

As a function, a random variable is required to be measurable, which allows for probabilities to be assigned to sets of its potential values. It is common that the outcomes depend on some physical variables that are not predictable, as in the case of tossing a coin.

Random variable can be discrete or continuous.
    - Discrete random variables take any of a specified finite or countable list of values. 
    - Continuous random variables take any numerical value in an interval or collection of intervals (having an uncountable range), via a probability density function.

### Mathematical definition

A random variable \\( X \\) is a measurable function \\( X : \Omega \rightarrow E\\) from a set of possible outcomes \\(\Omega\\) to a measurable space \\(E\\).

The probability that \\(X\\) takes on a value in a measurable set \\(S \subseteq E\\) is written as $$P\left(X\in S\right)=P\left(\left\{ \omega\in\Omega\mid X\left(\omega\right)\in S\right\} \right)$$

When the image of \\(X\\) is countable, the random variable is called a **discrete random variable** and its distribution is a discrete probability distribution, i.e., can be described by a probability mass function that assigns a probability to each value in the image of \\(X\\). If the image is unaccountably infinite then \\(X\\) is called a **continuous random variable** and its distribution can be described by a probability density function, which assigns probabilities to intervals.

Any random variable can ne described by its **cumulative distribution function**, which describes the probability that the random variable will be less than or equal to a certain value.

## Distribution functions

If a random variable \\( X : \Omega \rightarrow \mathbb{R} \\) is given, we can ask questions like "How likely is it that the value of \\( X = 2\\)?". This is the same as the probability of the event \\( \{ \omega:X\left(\omega\right)=2\} \\) which is often written as \\(P\left(X=2\right)\\) or \\(p_X(2)\\).

Recording all these probabilities of output ranges of a real-valued random variable \\(X\\) yields the probability distribution of \\(X\\). The probability distribution "forgets" about the particular probability space used to define \\(X\\) and only records the probabilities of various values of \\(X\\). Such a probability distribution can always be captures by its cumulative distribution function

$$ F_{X}\left(x\right)=P\left(X\leq x\right) $$

and sometimes also using a probability density function, \\(p_X\\). 


## Examples

### Discrete random variables

#### Coin toss

The possible outcomes for one coin toss can be described by the sample space $$\Omega=\left\{ \textrm{heads,tails}\right\}$$. We can introduce a real-valued random variabl \\(Y\\) that model a $1 payoff for a successful bet on heads as follows:

$$Y\left(\omega\right)=\begin{cases}
1, & if\ \omega=\textrm{heads},\\
0, & if\ \omega=\textrm{tails},
\end{cases}$$

If the coin is fair, \\(Y\\) has a probability mass function \\(f_Y\\) given by:

$$f_{Y}\left(y\right)=\begin{cases}
\frac{1}{2}, & if\ y=1,\\
\frac{1}{2}, & if\ y=0,
\end{cases}$$

### Continuous random variable

Formally, a continuous random variable is a random variable whose cumulative distribution function is continuous everywhere, which no gaps, which would correspond to numbers which have a finite probability of occurring. Instead, continuous random variable almost never take an exact prescribed value \\(c\\) (formally, \\( \forall_{C}\in\mathbb{R}:\textrm{Pr}\left(X=c\right)=0 \\)) but here is a positive probability that its value will lie in particular intervals which can be arbitrarily small.

An example would be one based on a spinner that can choose a horizontal direction. By mapping the sample space to a random variable which takes real number values, lets say, bt mapping a direction to a bearing in degrees clockwise from North, then the random variable takes values which are in the interval \\( \left[0,360\right) \\), with all parts of the range being _equally likely_. Any real number has probability zero of being selected, but a positive probability can be assigned to any range o values. For example the probability of choosing a number in \\( \left[0,180\right) \\) is \\( \frac{1}{2} \\). Instead of speaking of a probability mass function, we say that the probability _density_ of \\(X\\) is 1/360.


## References

- [Khan Academy](https://www.youtube.com/c/khanacademy){:target="_blank"}
- [Wikipedia](https://en.wikipedia.org/wiki/Random_variable){:target="_blank"}
   