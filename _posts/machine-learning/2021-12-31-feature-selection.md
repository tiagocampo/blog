---
layout: post
title: Feature selection
tags: sklearn python machine-learning theory
mathjax: false
description: In this blog post we discuss about feature selection
---

* Do not remove this line (it will not be displayed)
{:toc}

---

# Introduction

There are 5 ways of building models

- All-in
- Backward elimination
- Forward selection
- Bidirectional elimination
- Score comparison

The first 4 are grouped into a category named _stepwise regression_.


## All-in

Just use all the features given to you. 

## Backward elimination

1. select a significance level to stay in the model (e.g. SL = 0.05)
2. fit the full model with all possible predictor
3. consider the predictor with the highest p-value. If p > sl, go to step 4, otherwise go to fin.
4. remove the predictor
5. fit model without this variable. Do it until all variables are less then SL.

## Forward elimination

1. select a significance level to enter the model (e.g. SL = 0.05)
2. fit all simple regression models **y ~ x_n**. Select the one with the lowest p-value
3. keep this variable and fit all possible models with one extra predictor added to the one(s) you already have
4. consider the predictor with the lowest p-value. if p < sl, go to step 3, otherwise keep the previous model as the one.

## Bidirectional elimination

1. select a significance level to enter and to stay in the model. e.g.: slenter = 0.05, slstay = 0.05
2. perform the next step of forward selection (new variables must have: p < slenter to enter)
3. perform all steps of backward elimination (old variables must have p < slstay to stay)
4. no new variables can enter and no old variables can exit. Done

## Score comparison

1. select a criterion of goodness of fit (e.g. Akaike criterion)
2. construct all possible regression models: 2^N -1 total combinations
3. select the one with the best criterion

# sklearn feature selection

Please visit https://scikit-learn.org/stable/modules/feature_selection.html to see what is available.


# References

- [Machine Learning A-Z™: Hands-On Python & R In Data Science](https://www.udemy.com/course/machinelearning/learn/lecture/5772052#content){:target="_blank"}
