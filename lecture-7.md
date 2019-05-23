# Lecture 7 - Thu, Apr 25

_Note: She put up practice midterm questions and she's going to be typing up notes on a flight sometime this weekend._

### 3 FAQs

**1 - Pooling**

* There's some true covariance matrices which we don't know \($$\sigma_1$$ and $$\sigma_2$$\) which we want to estimate.
* If we believe the two covariance matrices are equal \(pooled\), then our best guess is that they're both equal to $$S_p$$
* If we believe they are not equal, then we guess $$S_1, S_2$$
* Use Box's M test to determine whether or not to pool \(see if the two sigmas are equal\).

$$\Sigma_{\bar{d}} = \Sigma_{\bar{y_1}} + \Sigma_{\bar{y_2}} = \frac{\Sigma_1}{n_1} + \frac{\Sigma_2}{n_2}$$ \(adjusting for sample size by dividing\).

What's our best guess about $$ \Sigma_{\bar{d}} $$ ?

If pooling, then:

$$S_{\bar{d}} = \frac{S_p}{n_1} + \frac{S_p}{n_2} = (\frac{1}{n_1} + \frac{1}{n_2})S_p$$

Else if not pooling, then:

$$S_{\bar{d}} = \frac{S_1}{n_1} + \frac{S_2}{n_2}$$

**2 - Null/Alternate Hypotheses**

* Based on research question
* "Is there evidence that..." \(ex: "...all variables are independent?" or "...cov matrices are not equal?" based on Box's M test\)
* Ex: $$ H_0: \Sigma $$ or $$ \Sigma_1 = \Sigma_2 $$ \(based on pooling?\)
* Ex: $$ H_a: \Sigma = diag(\sigma^2) $$

**3 - Test statistic to p-value**

* We have a bunch of test statistics: $$T^2, \Lambda, V, U, M, u$$
* All of these turn into a p-value, which is how we make our final conclusion.
* The intermediate step \(not very important, will be given to you in R output\):
* Compare to F distribution: $$T^2, \Lambda, V, U $$
* Compare to $$ \chi^2 $$ distribution: $$M, u$$
* Know how to conclude based on hypotheses and **be able to discuss these, what it means**

### Review/Clarify MANOVA

* MANOVA only works if pooled \(that $$\Sigma$$ matrices are equal\)
* If we want to test for quality of all 3 covariance matrices, we can just add another to the top and change $$p$$ on the bottom to 3.

### New: Two-way MANOVA

* Let's say, in addition to collecting ACT and SAT from these 3 schools, we also want to collect whether that student is in-state or out-of-state.

#### Review: How would you test the following null hypotheses?

Can we say that...

**1\)** $$H_0: \frac{SAT}{68} = ACT$$ **?**

Guess: Compare means same

Ans:

* $$H_0: \vec{a}'\vec{\mu} = 0$$
* t-test of linear combination of means: $$ \vec{a} = (1/68, -1)$$where first is SAT/68 and second is ACT.

**2\)** $$H_0:$$ **SAT is independent of ACT? \(lazy notation\)**

Guess: Calculate a Correlation statistic

Ans: Test statistic is Ratio of determinants and $$ S = diag(S_1^2, S_2^2) $$

**3\)** $$H_0$$**: Same test scores for in-state vs out-of-state students?**

Guess: Mean in-state same as mean out-of-state

Ans: Calculate $$T^2$$ statistic \(can still do that with 2 groups\), same assumptions as num 4.

**4\)** $$H_0$$**: Same test scores across all 3 schools?**

Guess: Compare 3 means

Ans: MANOVA test statistics guessing equality of mean vectors across 3 populations.

Assumptions:

1. That you can pool \(equal covariance matrices\)

2. Random samples \(truly independent samples\)

3. Multivariate Normality \(hope Central Limit Theorem applies and move on\)

**5\)** $$H_0$$**: Test scores same regardless of school and in/out-of-state status?**

Guess: Compare in-state from all schools vs out-of-state from all schools.

Ans: 2-way MANOVA

$$H_0: \mu_1 $$ \(TODO: ???\)

Use $$i$$ for student, $$j$$ for school, and $$k$$ for categorical \(0 for in-state, 1 for out-of-state\)

You say there's one mean + some random noise: $$ \vec{y_{ijk}} = \vec{\mu} + \varepsilon_{ijk} $$.

$$H_A$$ and $$H_B$$ for categorical variable $$A$$ and categorical variable $$B$$. This is **not** null vs alternative. A is in-state, B is out-of-state.

Sources of error:

1. $$H_A$$: There may be different means between schools.
2. $$H_B$$: There could be error because we didn't account for different in- vs out-of-state means \(TODO??\)
3. $$H_{AB}$$: Maybe in- vs out-of-state matters differently for each school. Maybe out-of-state students who choose to go to CSU Bakersfield are weird, but going out-of-state to UCSB is normal so there's not much difference between in- and out-of-state students at UCSB. We're looking at different **subgroupings** across all of these subgroups. Equation for this doesn't matter.
4. Noise \($$E$$\): Even after accounting for all of this, there's still some unexplained error which you just have to live with.

#### Our model is now

Our model \(before removing unnecessary adjustments\) is now:

$$\vec{y_{ijk}} = \vec{\mu} + \vec{\alpha_j} + \vec{B_c} + \vec{\gamma_{jk}} + \vec{E_{ijk}}$$

where:

$$\vec{\mu}$$ is the overall mean.

$$\vec{\alpha_j}$$ is the adjustment you need to make for each school \(if Cal Poly regularly gets 200 higher than others then $$\alpha_j = 200$$ for Cal Poly\). Source of error 1.

$$\vec{B_c}$$ is the adjustment for in- vs out-of-state. \(source of error 2\)

$$\vec{\gamma_{jk}}$$ is a "tweak" for interactions between school \(source of error 3\)

and $$\vec{E_{ijk}}$$ is the leftover random noise \(source of error 4\)

We want to compare model with $$\vec{H_{AB}} vs \vec{E}$$. We test this using Wilk's test:

$$\Lambda = \frac{| \vec{E} |}{| \vec{E} + \vec{H_{AB}} |}$$

We also test: should we have to keep $$ \vec{\alpha_j} $$ in the model? \(another $$H_0$$, where we test $$\vec{H_A} vs \vec{E}$$\):

$$\Lambda = \frac{| \vec{E} |}{| \vec{E} + \vec{H_{A}} |}$$

And additionally: should we have to keep $$ \vec{\alpha_j} $$ in the model? \(another $$H_0$$ where we test $$\vec{H_B} vs \vec{E}$$\):

$$\Lambda = \frac{| \vec{E} |}{| \vec{E} + \vec{H_{B}} |}$$

Looking at Wilks, we have to keep the factor for schools \($$\vec{\alpha_j}$$\), but we don't have to keep track of in- vs out-of-state or any interaction terms, so our final model is:

$$\vec{y_{ijk}} = \vec{\mu} + \vec{\alpha_j} + \vec{E_{ijk}}$$

