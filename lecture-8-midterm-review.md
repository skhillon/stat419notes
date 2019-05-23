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

