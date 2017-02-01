---
layout: post
title: "Metrics for classifiers: the wrong approach"
---

# Introduction

Suppose we have two binary classifiers and want to compare their predictive
performance. The simplest approach may be to evaluate the *accuracy* of each
classifier. Much ink has been spilled about the flaws in this approach, but I
believe most of the alternatives commonly used in the machine learning community
are not much better. Instead, I advocate testing *predictors*, not classifiers,
using a metric like the *Brier score*.

# The difficulty

To evaluate the accuracy of a classifier, we have a test set $$\mathcal X$$, and
for each classifier we evaluate

$$\frac{1}{|\mathcal X|} \sum_{x\in\mathcal X} [p(x) = c(x)] . $$

Here $$p(x)$$ is the class predicted by the classifier and $$c(x)$$ is the
actual class. For a proposition $$P$$, $$[P]=1$$ if $$P$$ is true, and $$[P]=0$$
otherwise.

Thus the accuracy is the probability of correctly classifying a randomly chosen
data point.

One of the problems people sometimes point to with accuracy is that it doesn't
take into account the fact that the distribution of the classes may be different
in the real data compared to the training or test data. I don't take this
complaint seriously. If your training data is not distributed more or less like
your real data, or at least if you don't have some idea how the real data
differs from the training data, your problem is hopeless to begin with.

A more substantive complaint is that scoring by accuracy doesn't take into
account the fact that different problems may have different loss functions. For
some problems, a false positive and a false negative may be equally bad (and for
such a problem accuracy is actually a perfectly good metric!), but for other
problems, they may not. Imagine a preliminary medical test for a serious illness
in which a positive result means the patient goes for more extensive and more
accurate testing, while a negative result means the patient goes home and never
gets tested again. In this scenario, a false negative may be much worse than a
false positive. If the illness is rare, a classifier may simply *always* predict
negative, earning a high accuracy score and yet being absolutely worthless!

Several alternative metrics have been proposed to address this problem. Most of
them, in my opinion, miss the
mark. The [ROC](https://en.wikipedia.org/wiki/Receiver_operating_characteristic)
curve has a better idea, and the related AUC metric reduces it to a single
number. However, in my opinion this metric overcomplicates the issue and is
difficult to interpret. Indeed, as far as I know there are no theoretical
guarantees that a better predictor (in the sense I discuss below) will get a
better AUC score.

# A better idea

The reason why we have these difficulties evaluating a classifier is that
classifying actually consists of two steps: prediction (estimating the
probability that our data point falls into each class), and classication proper
(using the estimated probability and our loss function to pick a class). The
second step is easy: just pick whichever class gives us the lowest expected loss
based on our estimated probability. But the second step is also the one which
varies from problem to problem, and which causes all the difficulties in
evaluating classifiers.

Instead of evaluating the *classifier*, we should be evaluating the underlying
*predictor*. If the algorithm does a good job of estimating the probability for
each class, then we can easily translate that into good classifications given a
loss function. Fortunately, a metric to evaluate predictors has already been
developed. Actually, it was developed over sixty years ago by the weather
forecasting community. It's
the [Brier score](https://en.wikipedia.org/wiki/Brier_score). In the Brier
score, we evaluate a predictor on a test set $$\mathcal X$$ by

$$\frac{1}{|\mathcal X|} \sum_{x\in\mathcal X} (f(x) - o(x))^2 . $$

Here $$f(x)$$ is the predicted probability of $$x$$ being of a desired class
$$C$$, while $$o(x)$$ is 1 if $$x$$ is indeed of class $$C$$ and 0
otherwise. Thus an algorithm will get a better (that is, lower) Brier score by
giving a high probability to the outcomes that actually appear in the test set,
and it can expect to achieve the best possible score by predicting the correct
probabilities (in the terminology of decision theory, it is
a
[proper scoring rule](https://en.wikipedia.org/wiki/Scoring_rule#Proper_scoring_rules)).

Conveniently, the Brier score is already available
in
[sklearn](https://www.google.com/search?client=safari&rls=en&q=sklearn+brier+score&ie=UTF-8&oe=UTF-8). Give
it a try.

