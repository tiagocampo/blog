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

When the image of \\(X\\) is countable, the random variable is called a **discrete random variable** and its distribution is a discrete probability distribution, i.e., can be described by a probability mass function that assigns a probability to each value in the image of \\(X\\). If the image is uncountably infinite then \\(X\\) is called a **continuous random variable** and its distribution can be described by a probability density function, which assigns probabilities to intervals.

Any random variable can ne described by its **cumulative distribution function**, which describes the probability that the random variable will be less than or equal to a certain value.

## References

- [Khan Academy](https://www.youtube.com/watch?v=dOr0NKyD31Q&list=PLU5aQXLWR3_xDN0M2ZeZ_zHIia0e42_3O){:target="_blank"}
- [Wikipedia](https://en.wikipedia.org/wiki/Random_variable){:target="_blank"}
   