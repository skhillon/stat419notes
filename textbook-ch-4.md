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

