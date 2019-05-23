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



