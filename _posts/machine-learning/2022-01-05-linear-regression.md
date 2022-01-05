---
layout: post
title: Linar Regression
tags: sklearn python machine-learning theory
mathjax: true
description: In this blog post we discuss linear regression
---

* Do not remove this line (it will not be displayed)
{:toc}

---

# Linear Regression

Linear regression assumptions is that the target value is expected to be a linear combination of the features. In mathematical notation, if \\(\hat{y}\\) is the predicted value

$$\hat{y}\left(\omega,x\right) = \omega_0 + \omega_1 x_1 + \cdots + \omega_p x_p$$

Across the module, we designate the vector $$ \omega = \left(\omega_1, \cdots, \omega_p \right)$$ as `coef_` and \\(\omega_0\\) as `intercept_`.

## Ordinary least squares

`LinearRegression` fits a linear model with coefficients $$ \omega = \left(\omega_1, \cdots, \omega_p \right)$$ to minimize the residual sum of squares between the observed targets in the dataset, and the targets predicted by the linear approximation. Mathematically, without going into too much detail, it solves a problem of the form:

$$ \min\left\Vert X\omega-y\right\Vert _{2}^{2} $$

**Usage**

```python
from sklearn.linear_model import LinearRegression
reg = LinearRegression()
reg.fit(X,y)
```

## Ridge regression (L2 regularization)

`Ridge` regression addresses some of the problems with Ordinary least squares by imposing penalty on the size of the coefficients. The ridge coefficients minimize a penalized residual sum of squares:

$$ \min\left\Vert X\omega-y\right\Vert _{2}^{2} + \alpha \left\Vert \omega \right\Vert _{2}^{2} $$

The complexity parameter \\(\alpha \geq 0 \\) controls the amount of shrinkage: the larger the value of \\(\alpha\\), the greater the amount of shrinkage and thus the coefficients become more robust to collinearity.

**Usage**

```python
from sklearn.linear_model import Ridge
reg = Ridge(alpha=0.5)
reg.fit(X,y)
```

`RidgeCV` implements ridge regression with built-in cross-validation of the alpha parameter. The object works in the same way as `GridSearchCV` except that it defaults to Leave-One-Out-Cross-Validation

**Usage**
```python
import numpy as np
from sklearn import linear_model
reg = linear_model.RidgeCV(alphas=np.logspace(-6, 6, 13))
reg.fit([[0, 0], [0, 0], [1, 1]], [0, .1, 1])
RidgeCV(alphas=array([1.e-06, 1.e-05, 1.e-04, 1.e-03, 1.e-02, 1.e-01, 1.e+00, 1.e+01,
      1.e+02, 1.e+03, 1.e+04, 1.e+05, 1.e+06]))
reg.alpha_
0.01
```

Specifying the value of the `cv` attribute will trigger the use of cross-validation.

## Lasso (L1 regularization)

`Lasso` is a linear model that estimates sparse coefficients. It is useful in some contexts due to its tendency to prefer solutions with fewer non-zero coefficients, effectively reducing the number of features upon which the given solution is dependent.

Mathematically, it consists of a linear model with an added regularization term.

$$ \min \frac{1}{2n_{\textrm{samples}}} \left\Vert X\omega-y\right\Vert _{2}^{2} + \alpha \left\Vert \omega \right\Vert _{1} $$

**Usage**

```python
from sklearn import linear_model
reg = linear_model.Lasso(alpha=0.1)
reg.fit([[0, 0], [1, 1]], [0, 1])
Lasso(alpha=0.1)
reg.predict([[1, 1]])
array([0.8])
```

sklearn also exposes objects that set the Lasso \\(\alpha\\) parameter by cross-validation: `LassoCV` and `LassoLarsCV`

## Elastic-Net

`Elastic-Net` is a linear regression model trained with both \\(l_1\\) and \\(l_2\\)-norm regularization of the coefficients. This combination allows for learning a sparse model where few of the weights are non-zero like Lasso, while still maintaining the regularization properties of Ridge. 

Elastic-net is useful when there are multiple features that are correlated with one another. LAsso is likely to pick one of these at random, while elastic-net is likely to pick both.

To objective function to minimize is in this case

$$ \min \frac{1}{2n_{\textrm{samples}}} \left\Vert X\omega-y\right\Vert _{2}^{2} + \alpha \rho \left\Vert \omega \right\Vert _{1} + \frac{\alpha\left(1-\rho\right)}{2}\left\Vert \omega \right\Vert _{2}^2$$

`ElasticNetCV` can be used to set the parameters \\(\alpha\\) and `l1_ratio` \\(\rho\\) by cross-validation.

## Generalized Linear Regression

Generalized Linear Models (GLM) extend linear models in two ways. First, the predicted value \\(\hat{y}\\) is linked to a linear combination of the input variables \\(X\\) via an inverse link function \\(h\\) as

$$ \hat{y}\left(\omega,X\right)=h\left(X\omega\right)$$

Secondly, the squared loss function is replaced by the unit deviance \\(d\\) of a distribution in the exponential family (or more precisely, a reproductive exponential dispersion model (EDM)).

The minimization problem becomes

$$ \min \frac{1}{2n_{\textrm{samples}}}\sum_i d\left(y_i,\hat{y}_i\right) + \frac{\alpha}{2}\left\Vert \omega \right\Vert _{2}$$

where \\(\alpha\\) is the L2 regularization penalty. When sample weights are provides, the average becomes a weighted average.

The choice of the distribution depends on the problem at hand:

- If the target value \\(y\\) are counts (non-negative integer valued) or relative frequencies (non-negative), you might use a Poisson deviance with log-link
- If the target values are positive valued and skewed, you might try a Gamma deviance with log-link
- If the target values seem to be heavier tailed than a Gamma distribution, you might try an Inverse Gaussian deviance.

Examples of use cases include:

- Agriculture / weather modeling: number of rain events per year (Poisson), amount of rainfall per event (Gamma), total rainfall per year (Tweedie / Compound Poisson Gamma).
- Risk modeling / insurance policy pricing: number of claim events / policyholder per year (Poisson), cost per event (Gamma), total cost per policyholder per year (Compound Poisson Gamma).
- Predictive maintenance: number of production interruption events per year (Poisson), duration of interruption (Gamma), total interruption time per year (Compound Poisson Gamma)

**Usage**

`TweedieRegressor` implements a generalized linear model for the Tweedie distribution, that allows to model any of the above mentioned distributions using the appropriate `power` parameter. In particular:

- `power = 0`: Normal distribution. Specific estimators such as `Ridge`, `ElasticNet` are generally more appropriate in this case.
- `power = 1`: Poisson distribution. `PoissonRegressor` is exposed for convenience. However, it is strictly equilatent to `TweedieRegressor(power=1, link= 'log')`.
- `power = 2`: Gamma distribution. `GammaRegressor` is exposed for convenience. However, it is strictly equivalent to `TweedieRegressor(power=2, link= 'log')`.
- `power = 3`: Inverse Gaussian distribution.

```python
from sklearn.linear_model import TweedieRegressor
reg = TweedieRegressor(power=1, alpha=0.5, link='log')
reg.fit([[0, 0], [0, 1], [2, 2]], [0, 1, 2])
TweedieRegressor(alpha=0.5, link='log', power=1)
reg.coef_
array([0.2463..., 0.4337...])
reg.intercept_
-0.7638...
```

The feature matrix \\(X\\) should be standardized before fitting. This ensures that the penalty treats features equally.



# References

- [Supervised learning](https://scikit-learn.org/stable/supervised_learning.html){:target="_blank"}