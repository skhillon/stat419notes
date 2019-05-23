---
description: By Sarthak Khillon
---

# STAT 419 Notes


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




# Lecture 5 - Thu, Apr 18

#### Testing Covariance Matrices by Determinants

How do you find determinant of 4x4 matrix?

$$A = \left(\begin{array}{cccc} 16 & 0 & 0 & 0 \\ 0 & 1 & 2 & 0 \\ 0 & 3 & 4 & 0 \\ 0 & 0 & 0 & 74 \end{array}\right)$$

$$A$$ is called a _block-diagonal matrix_. There are "squares" down the diagonal line. First block is 16, second block has rows \[1, 2\] and \[3, 4\], and third block is 74.

You can find $$| A | = | a_1 |  | a_2 |  | a_3 | = 16(-2)(74) = -2,368$$

**College Admisssions**

Let's say you had a matrix about applying to college. You have a vector with the following values:

$$\left(\begin{array}{c} GPA \\ SAT \\ ACT \\ RecLetter1 \\ RecLetter2 \end{array} \right)$$

The numerical ones are GPA, SAT, and ACT. The "Holistic" ones are RecLetter1 and RecLetter2 for rec letters.

We want 2 subvectors, $$\overrightarrow{x}$$ and $$\overrightarrow{y}$$. Is it true that rec letters are capturing the same capabilities as numerical? They should all capture the same thing: student quality.

We now have:

$$\left(\begin{array}{c} x_1 \\ x_2 \\ x_3 \\ y_1 \\ y_2 \end{array} \right)$$

There is some true covariance matrix, let's call it $$\Sigma$$, of these variables. The research question you might have is, are these holistic measures independent of these numerical measures? \(by independent in this class, we mean "uncorrelated", or that the true correlation is 0\)

**If correlation is 0 \(under** $$H_0$$ **that these are unrelated\), what does** $$\Sigma$$ **look like?**

$$H0: \Sigma = \left(\begin{array}{c} \sigma{11}^2 & \sigma \\ \sigma & \sigma_{55}^2 \ \end{array} \right) = \Sigma_0$$. Note that this is really a 5x5, we just skipped to the ends.

$$H_a: \Sigma = \left(\begin{array}{c} \Sigma_Y & 0 \\ 0 & \Sigma_X \ \end{array} \right)$$

Under $$H_a$, $| \Sigma | = | \Sigma_x | | \Sigma_y |$$

We've calculated some overall $$S$$, a sample covariance matrix:

$$S = \left(\begin{array}{c} Sy & S{xy} \\ S_{xy} & S_x \ \end{array} \right)$$

What is our test statistic? Should be ratio of determinants: we have $$\frac{| S |}{| S_x | |S_y|}$$, should be close to 1 \(up to your judgement\). It doesn't follow any distribution, bounded between 0 and 1, represents correlation. If you got 0.8, then you could say that they both represent similar things about student performance.

**Are all 5 of these measures independent from each other?**

$$H_0$$ remains the same as before.

$$H_a$$ is still $$\Sigma$$, but is now a diagonal matrix, where diag is variances of each variable. Therefore, determinant is the product of the diagonals, which is the product of all variances \(estimated variances from the data\). We still want this to be close to 1.

We somehow got that GPA is independent from SAT/ACT and they're independent from Rec letters. TODO

**We think variances are all equal, and they are all completely independent.**

$$H_0$$ stays the same.

We make $$H_a$$ a diagonal matrix of the same variance $$\sigma^2$$. So determinant = multiplying them all together. $$ | H_a | = (\sigma^2)^p $$, where $$p$$ is number of elements.

What is the test statistic? This time it's changed. We have $$\frac{| S |}{(S_{pooled}^2)^5}$$

which we still want it to be close to 1.

**Switching things up**

* Drop GPA from the study.
* Our assertion is that numeric variables are independent of rec letters, and that their covariances are the same.

$$H_0: \Sigma = \Sigma_0$$

$$H_a: \Sigma$$ is a block diagonal

$$\Sigma = \left(\begin{array}{c} \Sigma_Y & 0 \\ 0 & \Sigma_X \\ \end{array} \right)$$

And the test statistic is once again $$\frac{| S |}{| S_Y | | S_X |}$$

**Is the mean vector for rec letters the same as the mean vector for test scores?**

* We want to pool covariance matrices. $$H_0: \overrightarrow{\mu_{rec}} = \overrightarrow{\mu_{scores}}$$

Then we have $$M$$

* On exams we're not getting anything on a formula sheet.
* Box's M stat is given to us, the one above.


# Lecture 6 - Tue, Apr 23

### Midterm Info

**Part 1**

* Closed note, just like the written homework.
* We get a formula sheet, which is on Polylearn.
* R Studio

**Part 2**

* Use given desktop computers
* We get to use textbook \(email to self!\)
* We get to use any notes, but you should be able to access them from anywhere \(so email to self/put on Github/Google drive\)

### MANOVA

* We're making fun of SB

$$H0: \mu{CP} = \mu_{SB} = \mu{CSU B} $$

$$Ha: \mu{CP} \ne \mu{SB} \ne ... $$ not all equal.

### MANOVA Slides

#### Bivariate Model

**\(References "Same data, reordered" slide from MANOVA slides\)**

$$H_0: y{ij} \sim \mu + \varepsilon_{ij}$$, where $$i$$ is person and $$j$$ is score and $$\mu$$ is overall mean

We don't want any SB data to go into our Poly prediction, so for alternative:

$$H_a: y_ij \sim \mu_j + \varepsilon{ij} $$, where $$\mu_j$$ is the school's mean.

**Error Estimate**

$$H_0$$: Guess $$\mu = \bar{y}$$

$$\hat{\varepsilon} = \frac{1}{n-1} \sum_{i,j} (y_{ij} - \bar{y.j})^2$$

where the dot $$.$$ is overall.

$$H_a$$: Guess $$\mu_j = \bar{y_j} $$

$$\hat{\varepsilon_A} = \frac{1}{n-1} \sum_{j = 1} (y_i1 - \bar{y_i1})^2 + (y_i2 - \bar{y_i2})^2 + ...$$

Alternate will be smaller because based on the graph \(from slides, see Iris\), we will never get more variance when we consider individual group means \(TODO: why?\).

We're asking, did we reduce the variance enough in the model such that $$ \hat{\varepsilon_A} < \hat{\varepsilon_0} $$? Can we use the more complicated model?

#### Multivariate Model

We just make the $$ \mu $$s into vectors now

$$H0: \vec{\mu{CP}} = \vec{\mu{SB}} = \vec{\mu{CSU B}} $$

$$Ha: \vec{\mu{CP}} \ne \vec{\mu{SB}} \ne ... $$ not all equal.

**Error Estimate**

Individual student came from some overall mean, and each student brought their own error. We have a single mean per student $$\mu$$ \(not a vector!\) from $$n$$ students with 2 variables \(SAT and ACT\) such that:

$$ H_0: Y^{(n \times 2)} = \mu + E^{(n \times 2)} $$

For alternative, we know data is double indexed, so now the means are specific to the group. We're gonna call this error $$H$$ just to differentiate between null and alternate error estimates.

$$ H_a: Y^{(n \times 2)} = \vec{\mu_j} + H^{(n \times 2)} $$

Now if we want to estimate E, then for every person, we can average out how much difference there was between them and the overall mean \(TODO: same as centering?\) \(these equations are given on the computer\):

There's two ways for our guesses to miss. We might have missed the group mean vs the overall mean, or each group could have a lot of noise.

$$ \hat{E} = \sum (y_{.j} - \bar{y})( ... TODO)$$

**Takeaway**:

$$H_0: \hat{\varepsilon} = H + E$$

$$H_a: \hat{\varepsilon} = E $$

* Specifying model null and alternate \(see stuff under Multivariate Model header\)
* We will be given H and E matrices.

  * $$H$$ is error from not keeping track of the groups \(overall error/variance\)
  * $$E$$ is error from natural noise in data \(within groups\).
  * Question: is there enough error/wiggle room within the groups \($$H$$\) compared to the natural noise in the data \($$E$$\) for us to justify using the model?

**In-class exercise: Using** `MANOVA_Demo.rmd` **to create a test statistic: do we believe means are equal across all 3 schools?**

**TODO: Clear up the null hypothesis so that the result that H matters makes sense**

$$H_0: \hat{\varepsilon} = H + E$$, means are equal and $$H$$ matters.

$$H_a: \hat{\varepsilon} = E $$

Test statistic: if this is close to 1, then we don't need $$H$$ because it's so small that it doesn't significantly contribute to total error. Else, \(say $$H$$ and $$E$$ have approximately same determinants\), then we'd have something like $$\frac{det}{det + det} \approx 0.5$$, which is not close to 1 so we would fail to reject the null and conclude that we need $$H$$.

Test statistic $$ = \frac{|E|}{|H| + |E|} $$, but actually you add them together before taking determinant \(for "math reasons"\), so we have:

$$Test statistic = \frac{|E|}{|H + E|}$$

$$ det(E) = (37486 \times 1309) - 3775^2 = 34,818,549 $$

$$ \| H + E \| = \(\(2210409 + 37486\) \* \(85 + 1309\)\) - \(11216 + 3775\)^2 = 2,908,835,549 $$

$$\Lambda = \frac{|E|}{|H + E|} = \frac{34,818,549}{2,908,835,549} = 0.012 < 1$$

Therefore, since test statistic is small, we fail to reject the null and conclude that $H$ is important.

We just derived something called "Wilk's Lambda"!

====

We could have also used Pillai's Trace:

$$V = trace[(H + E)^{-1}E]$$

In code: `V <- sum(diag(solve(H + E) %*% E))`

Under $$H_0$$, trace = 2.

====

Hotelling-Lawley: Last one which combines the ideas. Sees if $$H$$ is "big enough".

$$U = trace(E^{-1}H)$$

Not very interpretable, but it does reduce to $$T^2 \times junk$$ which we don't really care about.


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


# Lecture 8 - Midterm Review

### General Exam Structure

* She posted only calculations on Polylearn, these notes are her explaining it.
* Can use R as your calculator on the computers.
* Looks a lot like HW and DA. Calculations and stuff isn't that important, analysis is more important. WHY is more important. Real World conclusions!
* Best way to study is to make up your own exam questions. She's gonna integrate one of the questions we submit onto the exam.

### Question 1a

Some dealerships will price cars differently, not necessarily independent \(based on dealership preferences, might price in related way\)

Divide all covariances by constituent standard deviations \(she used R but you should be able to do this by hand\)

Off diagonals show a slightly positive relationship. Toyota cars are probably related, and negative relationships between Toyota and Ford Fusion. Both hybrids? Anyway, positive relationship between first 2 and negative with 3rd.

$$ \frac{3.1}{ \sqrt{7.1 \times 6.4}} $$

### Question 1b

We're talking about a linear combination.

$$2y_1 + 4y_2 + 0y_3$$

$$a = (2 4 0)^T$$

$$\mu_{a'y} = a'\mu_y$$

$$\sigma_{a'y}^2 = a\Sigma_ya$$

She did this in R, but be able to do by hand.

### Question 1\(c, hypothetical\)

Distribution of how much Gates would spend?

Univariate normal: $$ \$ spent \sim N(142, \sqrt{177}) $$

### Question 1\(d, hypothetical\)

Probability that Gates spends more than $150K?

Get Z score: $$Z = \frac{150-142}{\sqrt{177}}=0.6 $$, get area above that on a normal curve.



### Question 2a

Fitness abilities are probably related for a given person.

$$H_0: \vec{\mu_L} = \vec{\mu_H}$$ -- \(Mean vector of low blood pressures and high blood pressures are equal.\)

$$H_a: \vec{\mu_L} \ne \vec{\mu_H}$$ --...not the same...

We do not reject the null \(that they have different fitness abilities\). We're given an F stat and p-value, so we fail to reject the null. Real world conclusion: We do not have sufficient evidence to say that blood pressure has an effect on fitness level.

### Question 2b

**MVN?**

* Maybe, but there's only 10 subjects PER GROUP \(Low group and High group\), so we can't just assume multivariate normality based on Central Limit Theorem.
* Also, we must have equal covariances because hotelling uses pooled sample covariance matrix and that relies on the assumption that we have equal covariances.
  * **TODO: WORKAROUND**: Not use pooled. `hotelling` package doesn't do that though.
  * Recall $$ S_{\bar{p}} = \frac{S_1}{n_1} + \frac{S_2}{n_2} $$
* People are all independent from each other \(assuming no family members\).

### Question 3a

* Recall sample total variances \($$ \sum diag(S) $$\) and sample generalized variances \($$ | S |$$\) from HW1
* Total variance: Similar, little more uncertainty in the uptake rate in the chilled sitaution.
* Generalized variance: Maybe relationship between concentration and rate of uptake is not the same between chilled and unchilled. Little more overall uncertainty in the chilled case.

### Question 3b

_This question is phrased as it would be on the midterm!_

$$H_0: \vec{\mu}_{chilled} = \vec{\mu}_{non-chilled}$$

$$H_a: \vec{\mu}_{chilled} \ne \vec{\mu}_{non-chilled}$$

$$\bar{d} = \bar{y_1} - \bar{y_2}$$

Calculate as non-pooled, this question is ambiguous but the midterm will be more clear.

$$S_{\bar{p}} = \frac{S_1}{n_1} + \frac{S_2}{n_2}$$

We care about our $$T^2$$ statistic and how variable it is:

$$T^2 = \bar{d}'(S_{\bar{d}}^-1)\bar{d} = 10.3$$

10.3 &gt; critical value of 6.29 \(we need to know if above or below\), so we reject the null hypothesis. Conclusion: The mean vectors between chilled and non-chilled are not equal, so **we have found evidence at the** $$\alpha = 0.05$$ **level that chilled environments affect** $$CO_2$$ **concentration and uptake**.

### Question 4a

Do they all have the same HWY MPG, engine size, and horsepower?

$$H0: \vec{\mu}{sports} = \vec{\mu}{SUV} = \vec{\mu}{wagon}$$ 

$$H_a$$: At least one mean is different

\(Extra: give a model and a null hypothesis in terms of the model\).

Model:

$$y = \mu + \alpha_j + \epsilon_{ij}$$

Recall in English, $$y_{ij}$$ is car $$i$$ of type $$j$$.

$$H_0: \forall_j \alpha_j = 0$$

Using Wilks' Lambda:

$$\Lambda = \frac{| E |}{| E + H|}$$

which we expect to be 1 under the null. Actual value is 0.2849... which is **not** close enough to 1 \(not greater than given critical value of 0.90\). Therefore, we reject the null hypothesis and **conclude that the three cars do NOT have the same Highway MPG, Engine Size, and Horsepower.**

Using Pillai, you should be able to explain what you expect under the null.

### Question 4b

**What were the assumptions?**

* MVN -- Sample sizes are pretty high, so yes.
* Homogenous \(equal\) covariance matrices -- Just by eyeballing, determinants are not the same.

### Question 4c

$$H0: \Sigma_S = \Sigma_W = \Sigma{SUV}$$

$$H_a$$: Not all equal.

Test statistic: Box's M Test. We have 3 populations.

$$M = \frac{(4.98 \times 10^4)^{46/2}(2.1 \times 10^4)^{58/2}(3.17 \times 10^4)^{38/2}}{(4.53 \times 10^4)^{(46+58+33)/2}} = 1.1 \times 10^-11$$

M value is very small, so we reject null because this is a ratio, and if it's not close to 1 then it implies that the individual matrices don't equal the Pooled version. This means we can't really trust the results of Wilks' Lambda and the outputs of the other tests because our basic assumptions are not valid.

### Question 5a

Are video games related at all to health?

$$H_0: \Sigma = \Sigma_0 $$ \(means this is unknown, and our best guess about it is the sample version\) 

$$H_a: \Sigma = diag(\sigma_n^2) $$ with 0s everywhere else.

Therefore we're testing if $$ | \Sigma | = \sigma1^2 | \Sigma{23} | $$

Test statistic:

$$u = \frac{|S|}{S_1^2 |S_{W, BP}} = 0.99$$

Note that $$S_1^2$$ is the variance of the first variable \(value is 8.31, top left in matrix\).

We reject the null hypothesis and conclude that gaming is independent of Blood Pressure and Weight.

### Homework Review, part II

#### Question 1

$$y_{ijk} = \mu + \alpha_j + \beta_k + \Gamma_{jk} + \epsilon_{ijk}$$

where $$y$$ is the observation of those 4 measurements \(4x1 vector\), $$i$$ is the individual plant, $$j$$ is the variety, and $$k$$ is the date.

**3 Null Hypotheses to test**: 

1\) $$H_0: \alpha_j = 0, \Lambda = 0.9 -> p = 0.27$$ so fail to reject. 

2\) $$H_0: \beta_k = 0, \Lambda = 0.034 -> p = 0$$ so reject. 

3\) $$H_0: \Gamma_{jk} = 0, \Lambda = 0.94 -> p = 0.51$$ so fail to reject.

**Sowing date affects the mean of 4 growth measures. We do not have evidence to show that variety matters, or that variety modifies the effect of sowing date \(interaction term\).**

#### Question 2

Are the assumptions met?

We did not find evidence of homogeniety of covariance matrices, so we cannot verify our evidence.


# Textbook Ch 4



## Chapter 4 - Tests of Significance with Multivariate Data

### 4.1 - Simultaneous tests on several variables

* If we collect data for several variables with the same units, then we can always examine variables one at a time.
  * _TODO: What do they mean here by sample units?_
  * _TODO: I also don't get this sentence_ : If sample units are in 2 groups, then a difference between means for 2 groups can be tested separately for each variable.
  * Repeated individual significance tests each have errors -&gt; multiply errors together.
    * Probability of false positive in at least one accumulates as num tests increases.
    * Instead, we want 1 test that uses all info together.
      * Ex\) $$H_0$$: Means of all variables are same for 2 multivariate population, and if $$p < 0.05$$ then we take it as $$H_a$$: Means differ for at least 1 variable.

### 4.2 - Comparison of mean values for 2 samples: The single-variable case

* Recall data in Table 1.1 on body measurements of 49 female sparrows. 
  * A sample when testing Darwin's theory of Natural Selection.
  * Birds 1-21 survived, 22-49 died.
  * Features included $$X_1$$ = total length, $$X_2$$ = alar extent, $$X_3$$ = length of beak & head, $$X_4$$ = length of humerus, and $$X_5$$ = length of keel of sternum
    * All features in millimeters.
* Take $$X_1$$, total length
  * Was mean length the same for survivors and non-survivors?
  * We create a sample of 21 survivors and 28 non-survivors, assuming random samples from much larger populations of survivors and non-survivors.
  * Are the 2 means **significantly** different?
    * Is the observed difference of the 2 means so large that it is unlikely to have happened by chance if the **population** means were otherwise equal?
  * To do this, we perform a **t-test**.

#### t-tests \(unofficial header\)

* Let there be a single variable $$X$$ and 2 random samples of values from 2 different populations.
* Let $$X_{i1}$$ denote values of $$X$$ in the first sample for $$i = 1,2,...,n_1$$
* Let $$X_{i2}$$denote values of $$X$$ in the second sample for $$i = 1,2,...,n_2$$

Then the mean for some other $$j$$th sample is:

$$\bar{x_j} = \sum_{i = 1}^{n_j} \frac{x_{ij}}{n}$$

and the variance is:

$$s_j^2 = \sum_{i = 1}^{n_j} \frac{(x_{ij} - \bar{x_j})^2}{(n_j - 1)}$$

* We assume $$X$$ is normally distributed in both samples and has the same variance within each sample.
* We test whether 2 sample means are **significantly different** using t-statistic:

$$t = \frac{(\bar{x_1} - \bar{x_2})}{s \times \sqrt{(\frac{1}{n_1} + \frac{1}{n_2})}}$$

* We then test if this is significantly different than 0 \(no difference\) in comparison with the t-distribution with appropriate degrees of freedom \(df\):

$$ df = n_1 + n_2 - 2 $$

The **pooled estimate of variance from the 2 samples** is given by:

$$s^2 = \frac{(n_1 - 1)s_1^2 + (n_2 - 1)s_2^2}{df}$$

* If we assume normality \(which is fine for $$ n > 15 $$ or so\) then this is robust.
  * We also don't have to worry too much about equal population variances if their ratio is between 0.4 and 2.5. 
  * Helps if sample sizes are equal.
* If they're normal but population variances may be drastically unequal, then we can use Welch's t-test:

$$t = \frac{(\bar{x_1} - \bar{x_2})}{\sqrt{(\frac{s_1^2}{n_1} + \frac{s_2^2}{n_2})}}$$

which we compare to the t distribution:

$$v = \frac{(w_1 + w_2)^2}{(\frac{w_1^2}{(n_1 - 1)} + \frac{w_2^2}{(n_2 - 1)})}$$

where

$$w_1 = \frac{s_1^2}{n_1}$$ and $$w_2 = \frac{s_2^2}{n_2}$$

But usually use the first ones, this one you probably won't need.

### 4.3 - Comparison of mean values for 2 samples: The multivariate case

* We can do the t-test in the previous section for each of the 5 measurements in the table, separately, to figure out which ones differ significantly between survivors and non-survivors.
  * What if a **multivariate relationship between the variables** was the predicting factor?
* We need a multivariate test to handle this: **Hotelling's** $$T^2$$**-test**. It's a generalization of the square of the original t-statistic.
  * In a general case, there are $$p$$ variables $$X_1, X_2, ..., X_p$$ being considered, and 2 samples with sizes $$n_1$$ and $$n_2$$.
  * There are also 2 sample mean vectors, $$\bar{x_1}$$ and $$\bar{x_2}$$ and 2 sample covariance matrices $$C_1$$ and $$C_2$$ being calculated as before.
    * TODO: Q: isn't there only 1 sample mean vector with 2 elements?

Assuming that population covariance matrices equal each other $$(\Sigma_1 = \Sigma_2)$$, we obtain a pooled estimate of the covariance matrix:

$$C = \frac{(n_1 - 1)C_1 + (n_2 - 1)C_2}{n_1 + n_2 - 2}$$

Hotelling's $$T^2$$ statistic is then defined as:

$$T^2 = \frac{n_1 n_2(\bar{x_1} - \bar{x_2})'C^{-1}(\bar{x_1} - \bar{x_2})} {(n_1 + n+2)}$$

* **Significantly large** $$T^2$$ **values mean that the population mean vectors are different**
* How do we find significance? Turn it into an F distribution, $$F \sim (p, n_1 + n_2 - p - 1)$$
* We can also rewrite Hotelling's statistic in a form similar to compute:

$$T^2 = \frac{(n_1 n_2)}{(n_1 + n_2)} \sum_{i = 1}^p \sum_{k = 1}^p (\bar{X_{1i}} - \bar{X_{2i}}) c^{ik} (\bar{X_{1k}} - \bar{X_{2k}})$$

where $$ \bar{X_{ji}} $$ is the mean of variable $$ X_i $$ in the $$j$$th sample, and $$ c^{ik} $$ is the element in the $$i$$th row and $$k$$th column of the inverse matrix $$ C^{-1} $$.

Remember that to compare 2 samples using Hotelling's statistic, both samples are assumed to come from multivariate normal distributions with equal covariance matrices, with moderate deviation allowed in multivariate normality and population covariance matrix equality.

**Example 4.1 Not replicated, Handwrite**

### 4.4 - Multivariate vs Univariate Tests

* It is possible to have insignificant univariate tests \(t-tests\), but significant multivariate \(Hotelling's $$T^2$$ tests\), and vice versa.
  * Significant multivariate happens from accumulations of evidence from individual variables in the overall test, i.e., multiple factors **together** are significant, but individually mean nothing.
  * Significant univarite but not multivariate happens when one significant result is swamped by other insignificant results in the group.
* Type I error is false positive \(null hypothesis is true even though we rejected\).
  * In univariate, we test at 5% level, so 95% chance of nonsignificant result.
  * If we do $$p$$ independent trials, then probability of at least 1 significant result is $$ 1 - 0.95^p $$, which keeps increasing with $$p$$ and may become unacceptably large. For example, $$p = 3$$ yields 0.23.
  * In multivariate data, variables are not usually independent, so the formula above isn't entirely accurate. Still, the more tests, the higher probability of a single false positive.
* To avoid increasing probability of Type I error, we use a multivariate test like Hotelling's $$T^2$$ test. Providing assumptions hold, 5% level of significance does not increase with $$p$$ variables involved.
* If you still need to use univariate tests, you can perform a Bonferroni adjustment. Not covering cuz we didn't do this in lecture, basically you just increase your $$\alpha$$ proportionally to $$p$$ to make up for the number of variables: $$ \frac{(100\alpha)}{p}\%$$
  * Probably just use a multivariate test.



### 4.5 - Comparison of Variation for 2 Samples: The Single-Variable Case

* With 1 variable, you can compare 2 samples using an F-test.
  * Review:
  * 1\) Get variances of both samples: $$s_1^2$$ and $$s_2^2$$. 
  * 2\) Compare ratio of first / second to F distribution: $$ F \sim F(n_1 - 1, n_2 - 2) $$
* Drawback of F-test is that it's sensitive to non-normality, so you might get a false positive significance due to the fact that the variables aren't normally distributed rather than the fact that their variances are unequal.
* More robust version is Levene's test. See example 4.2 \(not replicated here\).

### 4.6 - Comparison of Variation for 2 samples: The Multivariate Case

* Usually use **Box's M-test** to compare variation in 2 or more multivariate samples. See section 4.8 for more.
  * Sensitive to assumption that samples are from multivariate normal distributions.
  * False positive might be due to nonnormality rather than unequal population covariance matrices \($$\Sigma$$\)
* Van Valen's test:

$$d_{ij} = \sqrt{\Sigma_{k = 1}^p (x_{ijk} - \bar{x}_{jk})^2}$$

where $$ x_{ijk} $$ _is the value of variable_ $$X_k$$ _for the_ $$i$$_th individual in sample_ $$j$$_, and_ $$\bar{x}_{jk}$$ is the mean of the same variable in the sample. **Note that each variable should be standardized to** $$\mu = 0$$ **and** $$\sigma^2 = 1$$.

For a more robust test, we can replace $$\bar{x}_{jk}$$ _with_ $$ M_{jk} $$, which is the median for variable $$X_k$$ for the $$i$$th individual in sample $$j$$.

### 4.7 - Comparison of Means for Several Samples

There are 4 statistics used to test $$H_0$$: All samples come from populations with the same mean vector.

#### 1 - Wilks' Lambda Statistic

In short, we calculate $$\Lambda$$. If it is small, then the samples do not come from populations with the same mean vector. The calculation is: $$\Lambda = \frac{| W | }{| T |}$$

where:

* $$| x |$$ is a determinant
* $$W$$ is the within-sample Sum of Squares and Cross-product matrix \(TODO: ???\)
* $$T$$ is the total sum of squares and cross products matrix.

What are $$W$$ and $$T$$?

* We have $$j$$ samples \(tables\)
* Each sample has $$i$$ individuals \(rows\)
* Each individual has $$k$$ variables \(columns\)

So,

* $$x_{ijk}$$ is the value of the variable $$X_k$$ for the $$i$$th individual in the $$j$$th sample.
* $$\bar{x}_k$$ is the overall mean of $$X_k$$ across all samples.

Assuming $$m$$ total samples, each with its own size $$n_j$$, the elements in row $$r$$ and column $$c$$ of the $$\textbf{T}$$ matrix are:

$$t_{rc} = \Sigma_{j = 1}^m \Sigma_{i = 1}^{n_j} (x_{ijr} - \bar{x}_r)(x_{ijc} - \bar{x}_c)$$

The elements in row $$r$$ and column $$c$$ of the $$\textbf{W}$$ matrix are:

$$w_{rc} = \Sigma_{j = 1}^m \Sigma_{i = 1}^{n_j} (x_{ijr} - \bar{x}_{jr})(x_{ijc} - \bar{x}_{jc})$$

Note the difference in what's being subtracted right before parentheses \(TODO: Explain\). The other equations here don't really match up with what we learned.

### 4.8 - Comparison of Variation for Several Samples \(MANOVA Primer\)

Use Box's M-test to compare variation in several samples. The M-statistic is given by the equation:

$$M = \frac{\Pi_{i = 1}^m | C_i | ^ {\frac{1}{2}(n_i - 1)}} {| C | ^ {\frac{1}{2} (n - m)}}$$

where

* $$n_i$$ is the size of the $$i$$th sample
* $$C_i$$ is the sample covariance for the $$i$$th sample \(see section 2.7\)
* $$C$$ is the pooled covariance matrix given by:

$$C = \frac{\Sigma_{i = 1}^m (n_i - 1) C_i}{(n - m)}$$

#### Significant M-values

Large values of M mean that samples are **not from populations with the same covariance matrix**. We test with some equations that I don't think we need to know.


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


# Lecture 11 - MANOVA + LDA Part II

Recall if we have 2 groups, we perform Hotelling's $$T^2$$, and if we have 3+ groups, we do MANOVA.

### MANOVA **Part II**

Recall we are comparing $$E$$ vs $$H$$, and the important matrix is $$E^{-1}H$$ which we want to maximize because that means that E is large compared to H.

We find the eigenvalues of $$E^{-1}H$$: $$\lambda_1, \lambda_2, ..., \lambda_p$$ and that these are ordered from largest to smallest. How big, in terms of those eigenvalues, is $$E^{-1}H$$?

We find that $$| E^{-1}H | = \prod \lambda_i$$

Therefore, Wilk's Lambda can be written as: $$\Lambda = \frac{| E + H |}{| E |} = \prod_{i = 1}^p \frac{1}{1 + \lambda_i}$$

#### How do we decide how many variables to keep?

We use a "truncated" Wilk's Lambda.

If we only want to keep the first $$k \le p$$ variables, then we also only have to keep the first $$k$$ eigenvectors:

$$\Lambda_k =  \prod_{i = 1}^k \frac{1}{1 + \lambda_i}$$

We no longer need $$H$$ and $$E$$; all we need are eigenvalues. 

In 2 populations, we found an $$\vec{a}$$ that maximizes $$T^2$$.

In 3+ populations, we find $$\vec{a_1}, \vec{a_2}, ..., \vec{a_p}$$ that maximizes $$\Lambda$$, or equivalently, the ratio$$\frac{\vec{a}'H\vec{a}}{\vec{a}'E\vec{a}}$$. This is solved by solving for $$\vec{a}$$ in the following equation:

$$(E^{-1}H - \lambda I)_{\vec{a}} = 0$$

The lambdas tell you, relatively speaking, how important each discriminant function $$\vec{a_1}, \vec{a_2}, ..., \vec{a_p}$$ is. 

#### Take-Away

The matrix $$| E^{-1}H |$$ ****is important because you're trying to maximize $$\frac{\vec{a}'H\vec{a}}{\vec{a}'E\vec{a}}$$ ****as much as possible. We can do that through matrix decomposition of ****$$(E^{-1}H - \lambda I)_{\vec{a}} = 0$$**.**

### **LDA Part II**

Reasons why we do LDA:

1. We want to decide which variables matter for distinguishing groups \(are "_descriptive_"\)
2. "Predictive": Some unknown observation comes along, and we have to guess which population it came from \("_classification_"\)

In LDA, we're trying to come up with some scoring, or ruling, for how we're going to classify a new observation.

#### Classification

Is supervised, or at least semi-supervised. How do we use LDA for classification?

1. Find discriminant function\(s\) for known data \(training set\).
2. Find all scores from those functions for the training set.
3. Create a rule: choose a cutoff to differentiate between our populations.
4. Take all unknown data, score those, and use cutoffs to classify them.

#### Notes while going over \`Classification\_Code.Rmd\`:

* **Step 1:** Discriminant function is difference of means times inverse of covariance matrix.
  * $$\vec{a} = (\vec{\bar{y_1}} - \vec{\bar{y_2}}) S_p^{-1}$$
  * Note that the values are on different scales. If we're using LDA for goal \#1 \(see which variables matter\), then you definitely have to standardize.
  * **Step 2:** However, our goal is \#2 \(classification\). We drop the response variable \(`t(as.matrix(wine[, -12]))`\) and then multiply that by our discriminant function to get our discriminant score.
* We don't really know what these scores mean, and we don't care; we just want to know the scores **relative to each other.** We do this by plotting.
  * She set cutoff to halfway point. This seems like SVM...
* **Step 3**: How do we choose a proper cutoff?
  * Avoid overfitting: perfectly categorizing known samples is not impressive!
    * Deal with this using cross-validation.
  * If we have different sample sizes, then we can use that to weight our predictions.
    * Ex: our training data has more bad wines than good, so without any other information, if asked, you should guess that the wine is bad.
    * Furthermore, good wines might have a small range of scores \(-750 to -720\) whereas bad wines much have a much larger range \(-750 to -800\)
  * Risk analysis: cost of misclassification.
    * If you enter a wine into a competition and pay a $5000 entry fee, then the cost of misclassifying a bad wine as good is $5000.
    * On the other hand, misclassifying a good wine as bad costs you nothing, because you just won't enter it into the competition.

#### Fisher's Rule for choosing cutoff

Deals with proportions \(continuing with bad and good wines example\).

$$p_G = \frac{n_G}{n_{tot}}$$ and $$p_B = \frac{n_B}{n{tot}}$$ are "probability estimates"

Also "costs" of misclassification:

$$C_{12}$$ is the cost of misclassifying a category 1 observation as category 2. In the code, 1 is "good wines" and 2 is "bad wines".

Fisher's rule says we take the halfway point and then add an adjustment. The total equation is:

$$Cutoff = \frac{score}{2} + log(\frac{p_1C_{21}}{p_2C_{12}})$$

#### Continuing with Rmd, Step 4

We classify unknown wines and plot. We know "above is good" and "bad is below" by looking at the original plot.

Note that LDA function always standardizes and chooses cutoff as 0 if you don't provide an adjustment.




# Lecture 12 - Thu, May 23

### Continuing with `Classification Code.Rmd`

#### "What about PCA"?

* You can see that ellipses are not very different on Y axis, but they are on the X axis.
* The plot basically shows we can't do a very good job with only these 2 variables. We use PCA to spread wines out as much as we can \(unsupervised learning\) using some other pair of variables.
* Plotting first 2 PCs separates them drastically. We can just use unsupervised PCA clustering to classify new wines.

#### Calculate PC scores, how would you predict their quality using the first 2 PCs?

* To find PC scores, multiply the unknown wines \(minus their scores colum\) with the PCA rotation, column 1 or 2 based on which PC score you want to calculate.
  * `pc1 = as.matrix(unknown_wines[, -12] %*% my_pca$rotation[, 1])`

### Classification with PCA

* What do we gain with PCA? Dimension reduction, yes. But computers are fast, so why do we care?
  * Ans: Think of it as "de-noising" the data.
  * The observations we have come from some meaningful and also un-meaningful linear combinations. Un-meaningful linear combinations are random noise.
  * Goal of PCA is to say, "the first few PCs capture something real about the world", and "the last few PCs capture the noise/leftover error". We would like to use only the real information.
  * So, instead of overfitting what we're doing based on 11 dimensions that have a lot of noise, we narrow it down to only the important variables that say something meaninful about the world.

#### Steps

1. Create a PC decomposition from known data \(training set\).
2. Find PC scores for known data.
3. Find scores for unknown data.
4. For each unknown point, find which population is "closest". 

#### How do we find "closest" population? In other words, how do we calculate distance?

There are a variety of ways that we should known for this class:

* **Centroid distance**: Find geometric center of each group \(**centroid**\) and then calculate Euclidean distance from each point to each centroid. Classify to population with minimum distance.
  * Downsides: What if centroids are very close to each other based on each cluster's geometric mean? Also, the mean is not resistant to outliers.
* **K-Nearest Neighbors \(KNN\)**: See which $$k$$ wines look most like this unknown wine \(read: are closest via Euclidean distance\), and classify it as whichever is the majority group of all of its $$k$$ nearest known points.
  * Downsides: 
    * Don't use an even $$k$$ to avoid ties. 
    * Also, sensitive to population differences: if there's a lot more bad wines than good wines, the chances of you just having a majority of bad wines is higher regardless of where you actually are.
  * Lastly, how do you choose a $$k$$? Here are some options:
    * Try many $$k$$s and do cross-validation \(beyond the scope of 419\).
    * Try many $$k$$s and if all of them say the same result \(e.g. "bad wine" for most of your $$k$$s\) then you can be comfortable classifying as "bad wine".
    * Choose a distance \(radius around point\). Use however many neighbors are in that radius, and use that number of $$k$$. If there's no neighbors in radius, then that's a bad radius. Usually only meaningful if the space is interpretable to you in some way.
    * **For the homework, just pick a good value and move on**.

### PCA\_Clustering\_Classification.R

* There are a few Federalist papers with unknown authors. 
* We have 200 stop-words. For each federalist paper, there is a measurement of the percentage of the document which is stop-words.
* Looking at the first 4 PCs: Each PC is a linear combination of words with their frequencies. None of the 4 do a very good job of separating authors except PC1 paired with PC2. Plot confirms this.
* Next, classifying and predicting unknown documents, looks like James Madison authored most of these unknown documents \(based on, visually, which ellipse they're in and also their nearest neighbors\).
* Performing KNN with all 200 dimensions and $$k$$ says that most of them were authored by James Madison. Changing to $$k = 10$$ assigned a few more to Hamilton.
* We don't need all 200 words, so let's use the 2 PCs we have instead. Now we look at the closest point in 2 dimensions instead of 200. Results are similar.
* **In real life, most of them were written by James Madison and the 2 that are conflicted were probably co-authored, which is why they are so "on-the-border".**


