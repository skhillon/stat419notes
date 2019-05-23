# Textbook Ch 6 - PCA

## 6.1 - Definition of Principal Components

* Principal Component Analysis \(PCA\) takes $$p$$ variables $$X_1, X_2, ..., X_p$$and finds uncorrelated combinations of these variables.
* This creates indices $$Z_1, Z_2, ..., Z_p$$that are uncorrelated and sorted in order of their importance in terms of variation in data. In other words, $$Var(Z_1) \ge Var(Z_2) \ge ... \ge Var(Z_p)$$. They are uncorrelated because we want variables to measure different dimensions of the data.
* Z indices are **principal components**
* We want variances of principal components \($$Z_i$$s\) to be low for most of the indices. That means the few that have high variance can adequately cover most of the variation in the data set, so you only need those. The fewer that have high variance, the fewer variables you need to keep since your dataset has a lot of redundant variables.
* If original variables are uncorrelated, then PCA does nothing. This is only useful when original variables are very highly correlated \(positively or negatively\).

## 6.2 - Procedure for a PCA

### General Idea

* We start with the full dataset containing $$n$$ observations \(rows\) of $$p$$ variables \(columns\).
* The first principal component is a linear combination of all the variables:

$$Z_1 = a_{11}X_1 + a_{12}X_2 + ... + a_{1p}X_p = \vec{a}'\vec{X}$$

* We want to find coefficients \(values of $$a_i$$\) that maximize $$Var(Z_i)$$ WHERE $$\sum{a_{ip}} = 1$$. If we didn't have this condition, all $$a_{ip}$$ values could simply be $$\infty$$.
* Remember that all $$Z_i$$ must be uncorrelated with all other $$Z_i$$s

### Covariance Matrices

* A PCA involves finding the eigenvalues of a sample covariance matrix $$C$$ \(or in homework, $$S$$\)
* The eigenvalues of the matrix $$C$$ are the variances of the principal components. Recall that the eigenvalues are calculated by $$det(C - \lambda I)$$, also denoted as $$| C - \lambda I |$$
* This results in $$p$$ eigenvalues, where each $$\lambda_1, \lambda_2, ...\lambda_p \ge 0$$. We assume they are already in decreasing order, so each $$\lambda_i$$ corresponds to the $$i$$th Principal Component $$Z_i$$ such that $$Var(Z_i) = \lambda_i$$. Remember the $$a_{ip}$$ must sum to 1.
* Important property is that sum of eigenvalues = sum of diagonals \(trace\). Since the trace is variances, the takeaway here is that the principal components account for all the variation in the original data.

### How to Calculate them

* Standardize all variables to have means of 0 and variances of 1. This means diagonals is now all 1s. This gets you a correlation matrix.
* Translate the correlation matrix into a covariance matrix.
* Find the eigenvalues $$\lambda_i$$ and the corresponding eigenvectors $$\vec{a_i}$$ such that the sum of squares of coefficients = 1. This gets you the variance and coefficients of the Principal Component $$Z_i$$, respectively.
* Discard any components that only account for a small proportion of overall variation. For example, you might set a threshold to delete the bottom 10%.

