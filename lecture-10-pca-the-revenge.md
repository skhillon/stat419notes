---
description: 'Thursday, May 16, 2019'
---

# Lecture 10 - PCA: The Revenge

Recall that a PC is a linear combination of variables that has the largest variance.

Suppose you have some vector $$\vec{a}$$. We're going to take this and multiply it by our data: $$z = \vec{a}\vec{y}$$. The variance is $$var(z) = \vec{a}'\Sigma_y\vec{a}$$. What $$\vec{a}$$ maximizes the variance? Not a trick question, it's $$(\infty, \infty)'$$.

But that's not useful. We want to stay within our data, so we scale it. We want to find an $$\vec{a}$$ that maximizes $$\lambda$$ such that:

$$ \lambda = \frac{\vec{a}'S_y\vec{a}}{\vec{a}'\vec{a}} $$

We can rearrange terms to get the following equation:

$$\vec{a}'(I\lambda - S_y)\vec{a} = 0$$

Note the part in parentheses. Recall that solving $$| I\lambda - S_y | = 0$$ finds the eigenvalues of the covariance matrix by solving for $$\lambda$$. We want the best $$\vec{a}$$ that blows up the variance $$\lambda$$ without blowing up itself.

In the equation solving for 0 above \[$$\vec{a}'(I\lambda - S_y)\vec{a} = 0$$\], there will be multiple solutions; in fact, there will be $$p$$ solutions matching $$p$$ variables. We sort the variables from largest to smallest and denote them as $$a_1, ..., a_p$$ and $$\lambda_1, ..., \lambda_p$$. $$a_i$$ are your Principal Components, and $$\lambda_i$$ are the relative variance that you're trying to maximize. Lastly, your Principle Component Scores are $$z_1 = a_1'\vec{y}, z_2 = a_2'\vec{y}, ..., z_p = a_p'\vec{y}$$.

**NOTE**: Why are we doing this? We're trying to find a linear combination that spreads the data as much as possible. Why? Depends on your research question, but in general you want to differentiate "good" from "bad" scores as much as possible so that it's clear.

**NOTE**: On homework, note that "first PC" just the "best ranking method"

Lastly, we said PCA was unsupervised; you're trying to score all your students. The natural next  question is, can we decide what's the most important linear combination if we have some extra information, e.g. supervised method? Yes, this is called Linear Discriminant Analysis.

### Linear Discriminant Analysis \(LDA\)

NOTE: This is NOT Latent something else, LDA is usually used to reference the other one.

This is a supervised method; we know which population each observation came from. We want to know: what linear combination $$\vec{a}'\vec{y}$$ best separates your populations? \(Ex: What weightings of survey answers will best differentiate between favorite students?\)

**The best linear combination is the one that provides the most evidence of a difference.** For example:

$$H_0: \vec{a}'\vec{\mu_1} = \vec{a}'\vec{\mu_2}$$ \(Does applying these principle components make them equal? We want to reject\).

$$H_a: \vec{a}'\vec{\mu_1} \ne \vec{a}'\vec{\mu_2}$$

We also observe $$Y_1, Y_2$$ and we observe $$\Sigma_1 = \Sigma_2$$. This will be an ordinary t test because the linear combination $$\vec{a}'\vec{y}$$ results in a scalar.

The evidence of what you observe is the difference $$\vec{a}'\bar{y_1} - \vec{a}'\bar{y_2}$$. Under the null, you would expect a difference of $$0$$ if they're equal. We find the pooled covariance matrix $$S_p$$ as follows:

$$(\frac{1}{n_1} + \frac{1}{n_2})S_p = S_\bar{d}$$

$$S_z = \vec{a}'S_p\vec{a}$$ where $$z = \vec{a}'y_1 - \vec{a}'y_2$$

The t statistic \(want to maximize magnitude to find the most evidence!\) is then:

$$t = \frac{\vec{a}'\bar{y_1} - \vec{a}'\bar{y_2}}{\sqrt{\vec{a}'S_p\vec{a}(\frac{1}{n_1} + \frac{1}{n_2})}}$$

We find the most evidence when we maximize the following \(square t statistic from above, take out sample sizes since those are constants\):

$$\frac{(\vec{a}'\bar{y_1} - \vec{a}'\bar{y_2})}{\vec{a}'S_p\vec{a}}$$

If you think about what's actually happening here \(divide out the pooled covaraince that has been adjusted\), note that dividing by a matrix implies some sort of inverse. Skipping all the math, you end up with this:

$$\vec{a} = S_{p_{(p \times p)}}^{-1}(\bar{y_1} - \bar{y_2})_{(p \times 1)}$$

This equation will give you the coefficients \(Principal Components\) that will maximize your difference.

Punchline: $$\vec{a}'\bar{y_1} - \vec{a}'\bar{y_2} = (\bar{y_1} - \bar{y_2})'S_p^{-1}(\bar{y_1} - \bar{y_2})$$

What is the right half of the equation? **Hotelling's T-Squared \(without sample size\)**!

$$\vec{a}'\bar{y_1} - \vec{a}'\bar{y_2} = T^2(\frac{1}{n_1} + \frac{1}{n_2})^{-1}$$

\*\*The $$T^2$$ test is _exactly_ finding a linear combination to best separate the populations and then testing to see if the populations were separated enough for statistical significance.\*\*

#### Small Adjustment

Suppose you have 3 populations, and you need to find 2 linear populations that best separate the 3 populations. We then use Hotelling-Lawley.

\*\*Note that coefficients of a linear discriminant are $$S_p$$, and you may be asked to calculate that on an exam.\*\*

### Why Find Linear Discriminants?

With PCA you want to find the variable that best describes the data. With LDA, you can ask:

1. Which coefficients tell you the relative importance of variables in distinguishing between individual populations?
2. From that, find the least important \(redundant\) variables and drop them --&gt; Dimensionality Reduction.

#### Testing for Redundant Variables

Let's say we think we don't need the last few variables to differentiate between populations in the data \(our main goal in this whole thing\). We test:

$$H_0: \vec{a}'\bar{\mu_1} = \vec{a}'\bar{\mu_2}$$

$$H_a: \vec{a}'\bar{\mu_1} \ne \vec{a}'\bar{\mu_2}$$

We basically do a full-vs-reduced test, where the reduced is filled with $$0$$s to keep vectors the same:

Full: $$\vec{a} = (a_1, a_2, ..., a_p)$$

Reduced: $$\vec{a} = (a_1, a_2, ..., 0, 0, 0)$$







