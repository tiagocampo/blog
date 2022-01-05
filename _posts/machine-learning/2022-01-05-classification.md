---
layout: post
title: Classification
tags: sklearn python machine-learning theory
mathjax: true
description: In this blog post we discuss classification
---

* Do not remove this line (it will not be displayed)
{:toc}

---

# Decision Trees

Decision Trees are non-parametric supervised learning method used for classification and regression. The goal is to create a model that predicts the value of a target variable by learning simple decision rules inferred from the data features. A tree can be seen as a piecewise constant approximation.

Some advantages of decision trees are:

- Simple to understand and interpret since they can be visualized.
- Requires little data preparation.
- The cost of using the tree is logarithmic in the number of data points used to train the tree.
- Able to handle both numerical and categorical data, but sklearn does not implement categorical variables.
- Able to handle multi-output problems.
- Uses a white box model. If a given situation is observable in a model, the explanation for the condition is easily explained by boolean logic. 
- Possible to validate a model using statistical tests.
- Performs well even if is assumptions are somewhat violated by the true model from which the data were generated.

The disadvantages of decision trees include:

- Decision-tree learners can create over-complex trees that do not generalize the data well, overfitting. Mechanisms such as pruning, setting the minimum number od samples required at leaf node or setting maximum depth of the tree are necessary to avoid this problem.
- Decision trees can b unstable because of small variations in the data might result in a completely different tree being generated.
- Predictions of decision trees are neither smooth nor continuous, but piecewise constant approximations. Therefore they are not good in extrapolations.
- The problem of learning an optimal decision tree is known to be NP-complete. Practical decision tree learning algorithms are based on heuristic algorithms.
- Some concepts cannot be learned by decision trees. Ex.: XOR, parity, etc
- Decision tree learners create biased trees if some classes dominate.

`DecisionTreeClassifier` is a class capable of performing multi-class classification on a dataset.

```python
from sklearn.tree import DecisionTreeClassifier
classifier = DecisionTreeClassifier(criterion = 'entropy', random_state = 0)
classifier.fit(X_train, y_train)
```

The classifier takes several parameters which can be optimized. 

# Ensemble methods

The goal of ensemble methods is to combine the predictions of several base estimators built with a given learning algorithm in order to improve generalization / robustness over a single estimator.

Two families of ensemble methods are usually distinguished:
- In averaging methods, the driving principle is to build several estimators independently and then to average their predictions. On average, the combined estimator is usually better than any of the single base estimator because its variance is reduced.
- By contrast, in boosting methods, base estimators are built sequentially and on tries to reduce the bias of the combined estimator. The motivation is to combine several weak models to produce a powerful ensemble.

## Bagging meta-estimator

In ensemble algorithms, bagging methods from a class of algorithms which build several instances of a black-box estimator on random subsets of the original training set and then aggregate their individual predictions to form a final prediction. These methods are used as a way to reduce the variance of a base estimator (e.g., a decision tree), by introducing randomization into its construction procedure and then making an ensemble out of it. In many cases, bagging methods constitute a very simple way to improve with respect to a single model, without making it necessary to adapt the underlying base algorithm. As they provide a way to reduce overfitting, bagging methods work best with strong and complex models (e.g., fully developed decision trees), in contrast with boosting methods which usually work best with weak models (e.g., shallow decision trees).

In scikit-learn, bagging methods are offered as a unified `BaggingClassifier` meta-estimator, taking as input a user-specified base estimator along with parameters specifying the strategy to draw random subsets. In particular, `max_samples` and `max_features` control the size of the subsets (in terms of samples and features), while `bootstrap` and `bootstrap_features` control whether samples and features are drawn with or without replacement. When using a subset of the available samples the generalization accuracy can be estimated with the out-of-bag samples by setting `oob_score=True`. As an example, the snippet below illustrates how to instantiate a bagging ensemble of KNeighborsClassifier base estimators, each built on random subsets of 50% of the samples and 50% of the features.

```python
from sklearn.ensemble import BaggingClassifier
from sklearn.neighbors import KNeighborsClassifier
bagging = BaggingClassifier(KNeighborsClassifier(),
...                             max_samples=0.5, max_features=0.5)
```

## Random forests 

The `sklearn.ensemble` module includes two averaging algorithms based on randomized decision trees: The RandomForest algorithm and the Extra-Trees method. Both algorithms are perturb-and-combine techniques specifically designed for trees. This means a diverse set of classifiers is created by introducing randomness in the classifier construction. The prediction of the ensemble is given as the averaged prediction of the individual classifiers.

```python
from sklearn.ensemble import RandomForestClassifier
classifier = RandomForestClassifier(n_estimators = 10, criterion = 'entropy', random_state = 0)
classifier.fit(X_train, y_train)
```

In random forests, each tree in the ensemble is built from a sample drawn with replacement (i.e., a bootstrap sample) from the training set. Furthermore, when splitting each node during the construction of a tree, the best split is found either from all input features or a random subset of size `max_features`.

The purpose of these two sources of randomness is to decrease the variance of the forest estimator. Indeed, individual decision trees typically exhibit high variance and tend to overfit. The injected randomness in forests yield decision trees with somewhat decoupled prediction errors. By taking an average of those predictions, some errors can cancel out. Random forests achieve a reduced variance by combining diverse trees, sometimes at the cost of a slight increase in bias. In practice the variance reduction is often significant hence yielding an overall better model.

## AdaBoost

The core principle of AdaBoost is to fit a sequence of weak learners (i.e., models that are only slightly better than random guessing, such as small decision trees) in repeatedly modified versions of the data. The predictions from all of them are then combined through a weighted majority vote (or sum) to produce the final prediction. The data modifications at each so-called boosting iteration consist of applying weights \\(\omega_1, \omega_2, \cdots, \omega_N\\) to each of the training samples. Initially, those weights are all set to $$\omega_i = 1/N$$, so that the first step simply trains a weak learner on the original data. For each successive iteration, the sample weights are individually modified and the learning algorithm is reapplied to the reweighted data. At a given step, those training examples that were incorrectly predicted by the boosted model induced at the previous step have their weights increased, whereas the weights are decreased for those that were predicted correctly. As iterations proceed, examples that are difficult to predict receive ever-increasing influence. Each subsequent weak learner is thereby forced to concentrate on the examples that are missed by the previous ones in the sequence.

```python
from sklearn.model_selection import cross_val_score
from sklearn.datasets import load_iris
from sklearn.ensemble import AdaBoostClassifier

X, y = load_iris(return_X_y=True)
clf = AdaBoostClassifier(n_estimators=100)
scores = cross_val_score(clf, X, y, cv=5)
scores.mean()
0.9...
```

The number of weak learners is controlled by the parameter `n_estimators`. The `learning_rate` parameter controls the contribution of the weak learners in the final combination. By default, weak learners are decision stumps. Different weak learners can be specified through the `base_estimator` parameter. The main parameters to tune to obtain good results are `n_estimators` and the complexity of the base estimators (e.g., its depth `max_depth` or minimum required number of samples to consider a split `min_samples_split`).

## Gradient tree boosting

Gradient Tree Boosting or Gradient Boosted Decision Trees (GBDT) is a generalization of boosting to arbitrary differentiable loss functions. GBDT is an accurate and effective off-the-shelf procedure that can be used for both regression and classification problems in a variety of areas including Web search ranking and ecology.

`GradientBoostingClassifier` supports both binary and multi-class classification. The following example shows how to fit a gradient boosting classifier with 100 decision stumps as weak learners:

```python
from sklearn.datasets import make_hastie_10_2
from sklearn.ensemble import GradientBoostingClassifier

X, y = make_hastie_10_2(random_state=0)
X_train, X_test = X[:2000], X[2000:]
y_train, y_test = y[:2000], y[2000:]

clf = GradientBoostingClassifier(n_estimators=100, learning_rate=1.0,
...     max_depth=1, random_state=0).fit(X_train, y_train)
clf.score(X_test, y_test)
0.913...
```
The number of weak learners (i.e. regression trees) is controlled by the parameter `n_estimators`; The size of each tree can be controlled either by setting the tree depth via `max_depth` or by setting the number of leaf nodes via `max_leaf_nodes`. The `learning_rate` is a hyper-parameter in the range (0.0, 1.0] that controls overfitting via shrinkage.

# Logistic Regression

Despite its name it is a linear model for classification rather than regression. Logistic regression is implemented in `LogisticRegression`. This implementation can fit binary, One-vs-Rest, or multinomial logistic regression with optional \\(l_1\\), \\(l_2\\) or ElasticNet regularization.

As an optimization problem, binary class \\(l_2\\) penalized logistic regression minimizes the following cost function:

$$\min_{w,c}\frac{1}{2}\omega^{T}\omega+C\sum_{i=1}^{n}\log\left(\exp\left(-y_{i}\left(X_{i}^{T}\omega+c\right)\right)+1\right)$$

Similarly, for \\(l_1\\) regularization

$$\min_{w,c}\left\Vert \omega_{1}\right\Vert +C\sum_{i=1}^{n}\log\left(\exp\left(-y_{i}\left(X_{i}^{T}\omega+c\right)\right)+1\right)$$

And for ElasticNet

$$\min_{w,c}\frac{1-\rho}{2}\omega^{T}\omega+\rho\left\Vert \omega_{1}\right\Vert +C\sum_{i=1}^{n}\log\left(\exp\left(-y_{i}\left(X_{i}^{T}\omega+c\right)\right)+1\right)$$

```python
from sklearn.linear_model import LogisticRegression
classifier = LogisticRegression(random_state = 0)
classifier.fit(X_train, y_train)
```

There are a lot of parameters which can be tunned.

# Nearest Neighbors

`sklearn.neighbors` provides functionality for unsupervised and supervided neighbors-based learning methods. 

The principle behind nearest neighbor methods is to find a predefined number of training samples closest in distance to the new point, and predict the label from these. The number of samples can be user-defined (k-nearst neighbor learning), or vary based on the local density of points (radius-based neighbor learning). The distance can, in general, be any metric measure: standard Euclidean distance is the most common choice. Neighbors-based methods are known as _non-generalizing_ machine learning methods, since they simply "remember" all of its training data.

Neighbors-based classification is a type of _instance-based learning_: it does not attempt to construct a general internal model, but simply stores instances of the training data. Classification is computed from a simple majority vote of the nearest neighbors of each point: a query point is assigned the data class which has the most representatives within the nearest neighbors of the point.

scikit-learn implements two different nearest neighbors classifiers: `KNeighborsClassifier` implements learning based on the \\(k\\) nearest neighbors of each query point, where \\(k\\) is an integer value specified by the user.`RadiusNeighborsClassifier` implements learning based on the number of neighbors within a fixed radius \\(r\\) of each training point, where \\(r\\) is a floating-point value specified by the user.

The \\(k\\)-neighbors classification in `KNeighborsClassifier` is the most commonly used technique. The optimal choice of the value \\(k\\) is highly data-dependent: in general a larger \\(k\\) suppresses the effects of noise, but makes the classification boundaries less distinct.

In cases where the data is not uniformly sampled, radius-based neighbors classification in `RadiusNeighborsClassifier` can be a better choice. The user specifies a fixed radius \\(r\\), such that points in sparser neighborhoods use fewer nearest neighbors for the classification. For high-dimensional parameter spaces, this method becomes less effective due to the so-called “curse of dimensionality”.

The basic nearest neighbors classification uses uniform weights: that is, the value assigned to a query point is computed from a simple majority vote of the nearest neighbors. Under some circumstances, it is better to weight the neighbors such that nearer neighbors contribute more to the fit. This can be accomplished through the `weights` keyword. The default value, `weights = 'uniform'`, assigns uniform weights to each neighbor. `weights = 'distance'` assigns weights proportional to the inverse of the distance from the query point. Alternatively, a user-defined function of the distance can be supplied to compute the weights.

```python
from sklearn.neighbors import KNeighborsClassifier
classifier = KNeighborsClassifier(n_neighbors = 10, metric = 'minkowski', p = 2)
classifier.fit(X_train, y_train)
```

# Naive Bayes

Baive Bayes methods are a set of supervised learning algorithms based on applying Bayes`s theorem with the "naive" assumption of conditional independence between every pair of features given the value of the class variable. Bayes' theorem states the following relationship, given class variable \\(y\\) and dependent feature vector \\(x_1, \cdots, x_n\\):

$$P\left(y|x_{1},\cdots,x_{n}\right)=\frac{P\left(y\right)P\left(x_{1},\cdots,x_{n}|y\right)}{P\left(x_{1},\cdots,x_{n}\right)}$$

Using the naive conditional independence assumption that

$$P\left(x_{i}|y,x_{1},\cdots,x_{i-1},x_{i+1},\cdots,x_{n}\right)=P\left(x_{i}|y\right)$$

for all \\(i\\), this relationship is simplified to

$$P\left(y|x_{1},\cdots,x_{n}\right)=\frac{P\left(y\right)\prod_{i=1}^{n}P\left(x_{i}|y\right)}{P\left(x_{1},\cdots,x_{n}\right)}$$

Since \\(P\left(x_{1},\cdots,x_{n}\right)\\) is constant given the input, we can use the following classification rule:

$$\begin{align*}
P\left(y|x_{1},\cdots,x_{n}\right) & \propto P\left(y\right)\prod_{i=1}^{n}P\left(x_{i}|y\right)\\
 & \Downarrow\\
\hat{y} & =\arg\max_{y}P\left(y\right)\prod_{i=1}^{n}P\left(x_{i}|y\right)
\end{align*}$$

and we can use Maximum A Posteriori estimation to estimate 
\\(P\left(y\right)\\) and \\( P\left(x_{i}|y\right) \\); the former is then the relative frequency of class \\(y\\) in the training set.

The different naive Bayes classifiers differ mainly by the assumption they make regarding the distribution of 
\\( P\left(x_{i}|y\right) \\).

### Gaussian Naive Bayes

`GaussianNB` implements the Gaussian naive Bayes algorithm for classification. The likelihood of the features is assumed to be Gaussian:

$$P\left(x_{i}|y\right)=\frac{1}{\sqrt{2\pi\sigma_{y}^{2}}}\exp\left(-\frac{\left(x_{i}-\mu_{y}\right)^{2}}{2\sigma_{y}^{2}}\right)$$

The parameters \\(\sigma_y\\) and \\(\mu_y\\) are estimated using maximum likelihood.

### Bernoulli Naive Bayes

`BernoulliNB` implements the naive Bayes training and classification algorithms for data that is distribute according to multivariate Bernoulli distributions, i.e., there may be multiple features but each one is assumed to be binary-valued variable. Therefore, this class requires samples to be represented as binary-valued feature vectors/

The decision rule for Bernoulli naive Bayes is based on

$$P\left(x_{i}|y\right)=P\left(i|y\right)x_{i}+\left(1-P\left(i|y\right)\right)\left(1-x_{i}\right)$$

which differs from multinomial NB’s rule in that it explicitly penalizes the non-occurrence of a feature \\(i\\) that is an indicator for class \\(y\\), where the multinomial variant would simply ignore a non-occurring feature.

# Support Vector Machines

`SVC`, `NuSVC` and `LinearSVC` are classes capable of performing binary and multi-class classification on a dataset.

`SVC` and `NuSVC` are similar but accept slightly different sets of parameters, `LinearSVC` is a fast implementation of SVC for the case of a linear kernel.

```python
from sklearn.svm import SVC
classifier = SVC(kernel = 'linear', random_state = 0)
classifier.fit(X_train, y_train)
```

```python
from sklearn.svm import SVC
classifier = SVC(kernel = 'rbf', random_state = 0)
classifier.fit(X_train, y_train)
```

There are a lot of parameters that can be tuned.

# References

- [Supervised learning](https://scikit-learn.org/stable/supervised_learning.html){:target="_blank"}