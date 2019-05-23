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

