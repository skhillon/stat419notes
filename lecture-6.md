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

