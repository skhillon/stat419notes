# Lecture 4 - Tue, Apr 16

Tuesday, Apr 16

Review: Pooled covariance matrix of $$d$$: $$C = \frac{(n_1 - 1)C_1 + (n_2 - 1)C_2}{n_1 + n_2 - 2}$$

Covariance estimate for mean dif: $$S_\bar{d} = (\frac{1}{n_1} + \frac{1}{n_2})C$$

$$C^{-1}(\frac{n_1 + n_2}{n_1n_2})^{-1} \to (\frac{n_1 + n_2}{n_1n_2})C^{-1}$$

$$T_2 = \bar{d}^{-1} S_\bar{d}^{-1}\bar{d} = (\frac{n_1 + n_2}{n_1n_2})C^{-1}$$

#### Checking Multivariate Normality \(MVN\)

1. Individual Variables
* Histograms
* Q-Q plots.
* What is a Q-Q plot? AKA Normal Quantile Plot.
* If a histogram is normal, how many standard deviations do we have to go below the mean before there's 16% of the data? Should be 1 standard deviation. Mark where that happens.
* We can keep finding checkpoints where a certain percentage of data is captured.
* We look at what should happen on a standard normal and what happens with my data. On a standard normal, 0 standard deviations from mean should have half the data below, but our data showed 67%. At Z-scores of 1 and 2, we see values of 71 and 75.
* How much do these values fall on a nice normal distribution? Plot X being normal values, Y being our actual values. Q-Q plot shows a linear plot, how well your values fit the line is how normal your data is.
* Recall 324, top left chart!
* Shapiro-Wilk: Basically tests quantiles from Q-Q plot. Gives you something better than eyeballing a plot for linearity.
2. MVN: Looking at Quantiles for variance and "Kirtosis" \(don't worry about it\).

* Command shows output of a bunch of tests, don't worry about any that aren't in these notes.
* Central Limit Theorem trumps all, sample size \($$n$$ &gt; 15\) is large enough to treat as normal.
* Sometimes $$|\Sigma| \ne 0$$ happens

#### Hypothesis Test for Sugar Percentage

$$H_0: \mu{ResSug} = 0.8\mu_{pH}$$

$$\overrightarrow{\mu} = \left(\begin{array}{c} \mu{ResSug} \\ \mu{pH} \\ \end{array} \right)$$

Note that if you change the order where $$pH$$ is first \(as was the case in the R code for Lab 3 before changing it\), you need to switch $$-0.8$$ to be first \(on top\).

$$\mathbf{a}\overrightarrow{\mu}$$ where $$ \mathbf{a} = \left( \begin{array}{c} 1 \\ 0.8 \\ \end{array} \right)$$

$$\mathbf{w} = \mathbf{a'y}$$

$$\mathbf{W} = \mathbf{Ya}$$

#### Hypothesis Test for Generalized Variance

$$H_0: \Sigma_g = \Sigma_b (= \Sigma_p)$$

$$\frac{| \Sigma_g |}{| \Sigma_b |} = 1$$

This shows that the ratio of determinants to see if covariance matrices are equal: $$\frac{ \sqrt{|\Sigma_g||\Sigma_b| }}{|\Sigma_p|} = 1$$

The following should be close to 1: $$\mu = \frac{|S_g|^{\frac{1}{2}(n_1 - 1)}|S_b|^{\frac{1}{2}(n_1 - 1)}}{|S_p^2|^{(n_1 + n_2 - 2)}}$$

#### Individual T-Tests

Our tests are on vectors, but we don't really know which ones are driving the differences. We can run individual t tests using individual calls to `t.test`.

_Question: Why not just start here? If one of them is different then we don't have to bother with the matrix stuff, right?_

Answer: We're looking at relationships between variables. pH and residual sugar of the same wine are linked. In the Hotelling test, we accounted for that relationship to test the vectors all at once. That's why getting to `S_dbar` was such a pain because we care about the covariances.

Note that individual tests can be significant whereas the multivariate tests can be not significant, or vice-versa. The relationship matters, so you have to run both depending on what you want.



