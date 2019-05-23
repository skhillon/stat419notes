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

