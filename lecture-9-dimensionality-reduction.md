---
description: 'Tuesday, May 14, 2019'
---

# Lecture 9 - Unsupervised Dimensionality Reduction

### Note about Unsupervised Dimensionality Reduction

You can't say "which questions separates male-identifying vs female-identifying students", or stat vs CS students. All she did for the midterm questions was "here's some data, let's see the variance in all the data".

Later, with supervised methods, you **can** ask which variables best separate different classes of students \(stat vs CS, genders, age, whatever\).

## Intro

We observe $$Y_{n \times p}$$ where $$p$$ is the number of attributes you observe and is very large. We might not need all $$p$$ dimensions to tell the whole story. We want to find some smaller set of variables $$k < p$$ that is still going to represent this data well.

### 1. Singular Value Decomposition \(SVD\)

Recall that any matrix $$Y_{n \times p}$$ can be decomposed into 3 separate matrices being multiplied together: $$Y = U_{n \times p}D_{p \times p}V_{p \times p}'$$

Recall that the $$D$$ matrix is a diagonal matrix containing singular values \(square root of eigenvalues, $$\sqrt{\lambda_i}$$\) and 0s everywhere else.

What if you know that $$|Y| = 0$$? This means that not all variables are linearly independent, which implies that some of these variables **can be represented by linear combinations of other variables**. This means that you have redundant variables/attributes/columns that can be "absorbed" into some of the other ones. In terms of singular values, it means that at least some of the eigenvalues are 0.

We further assume that the singular values on the diagonal of $$D$$ are sorted in order of largest \(top left\) to smallest \(bottom right\). If all singular values \(and therefore eigenvalues\) $$\lambda_{k + 1}...\lambda_p = 0$$, then we know that those columns are redundant.

In our data, $$\lambda_i = 0$$ almost never happens, so we treat "very small" values as 0. We ask, what $$k$$ is good enough?

We create a new $$\tilde{Y} = U_{n \times k}^{truncated} D_{k \times k}^{truncated} V_{k \times p}^{truncated}$$ which is a "compressed version" of our data matrix $$Y$$.

In-class example: Given a $$600 \times 600$$ image, we "compress" an image by taking only the important features from each image instead of the full resolution.

### 2. Principal Component Analysis \(PCA\)

A special type of SVD. We take a \(for now, population\) covariance matrix $$\Sigma$$ and we perform SVD on that matrix. Because $$\Sigma$$ is square and non-negative-definite \(as all covariance matrices are\), then we are finding eigenvalues instead of singular values in our decomposition. We assume eigenvalues are already sorted from largest to smallest.

We want to find out **how much variance is explained by each Principle Component \(PC\)**? Each PC is a linear combination of variables. Now, rather than compress and get back our original data, we're using these linear combinations to **quantify** how much is already explained by each PC. We use this information in 2 different ways:

**Use Case 1 - Dimensionality Reduction** -- Explain data with fewer variables. Example: let's say you're trying to quantify the size of a grizzly bear. We have an idea that "Size" is explained by height and weight. We create a scatterplot of the heights vs weights of a bunch of grizzly bears. We want to rank them, but we don't want to rank by only height or only weight; we want a combination. Think of the PC as an **axis passing closest to data** \(best fit line\). Now, we can use this best fit line \(PC score\) to rank them. Bottom left is smallest bear, top right in graph is largest bear. We can create a second PC score perpendicular to the first. In real life, you'll probably find something more nuanced than equal variable weights for height and weight -&gt; size.

**Use Case 2 - Decide which variables are important.** Let's say we're trying to decide which variables are best for predicting if someone will get into Cal Poly or not, we plot GPA on Y and SAT on X axis. We note that the X value matters more, so we create **PC loadings** for these variables that look something like $$Score = 0.8SAT + 0.2GPA$$. Now, even if you don't really care about the score, you have a ratio of importance of multiple variables against each other **\(these must be normalized against each other first!\)**

### Example: \`Principle\_Components.Rmd\`

Note in R output, positive or negative PCA values from `prcomp` does not matter, just use the magnitude. Loadings are given by `pr.out$rotation`, and `pr.out$x` gives you scores \(ex. One score for each PC level \(columns\) for each state \(rows\), more negativity in each PC score indicates a more dangerous state\).

There's another command that gives arrows for each variable and plots the X values in each of those directions \(ex: California seems to be high in the direction of the rape crime\). Least dangerous state looks like North Dakota, most dangerous state looks like Florida. You can also plot the proportion of variance explained, and when it starts to taper off, you can say "ok this seems like good enough", basically the elbow method.



