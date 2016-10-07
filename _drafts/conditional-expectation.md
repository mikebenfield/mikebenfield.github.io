---
layout: post
title: "Conditioning on an event of probability 0, Part 1"
---

$$\newcommand{\P}{\mathbf P}$$
$$\newcommand{\E}{\mathbf E}$$

# Introduction

Suppose we are given a probability space $$\Omega$$ and events $$A$$ and
$$B$$. The *conditional probability* of $$A$$ given $$B$$ is written
$$\P[A|B]$$ and, in elementary probability theory, is defined as

$$\begin{equation}
  \P[A|B] = \frac{\P[A \cap B]}{\P[B]} .
\end{equation}$$

For example, if $$\Omega$$ consists of the results $$\{1,2,3,4,5,6\}$$ of the
roll of a fair die, $$B$$ is the event that an even number was rolled, and
$$A$$ is the event that a 2 was rolled, we have $$\P[A]= \frac 1 6$$, while
$$\P[A|B] = \frac 1 3$$, coinciding with our intuition.

But what about the case when $$\P[B] = 0$$? Recall that an event being of
probability 0 does not mean that it is impossible. As a simple example, suppose
that the random variable $$X$$ is distributed uniformly on $$[0,1]$$. Then for
any fixed value $$a \in [0,1]$$, we have $$\P[X=a] = 0$$, but of course it's
not *impossible* that $$X=a$$. Since $$\P[B]$$ appears in the denominator of
our definition given above, this definition cannot be used for a case when
$$\P[B]=0$$. Nevertheless, in many cases there seem to be intuitively clear
values to assign $$\P[A | B]$$, and it seems to a recurring question among
students of elementary probability theory whether such a probability is valid
and how to compute it.

# An example we won't be looking at

Typically the difficulty in conditioning on probability $$0$$ events is
illustrated with the [Borel-Kolmogorov
paradox](https://en.wikipedia.org/wiki/Borel–Kolmogorov_paradox). This is an
interesting and historically important example and by all means you should
investigate it if you're interested. It's not the example we will be focuing on
here for two reasons:

1. The sample space is the sphere, and the geometry of the sphere makes the
phenomenon at hand difficult to visualize.

2. It's not clear what conclusion we should reach. Do the conditional
probabilities really differ? Or is the fact that they differ an indication that
our method of calculation was wrong, and we should do something else instead?
Or maybe we should conclude that conditioning on an event of probability
0 really is invalid?

# An attempt to compute 
In our example we will focus on the conditional *expectation* of a random
variable, in elementary probability theory defined as

$$\E[X | B] = \frac{\int_B X \, d\P}{\P[B]} . $$

The conditional expectation is simpler for our purposes and will lead into our
later discussion of regular conditional probability.

# The answer and how to deal with it

To skip straight to the answer, no, in general it is not permissible to give
a value to $$P[A | B]$$ when $$P[B] = 0$$. If you need to compute such
a conditional probability, there are two things you can do:

1. You have modelled your data using the probability distribution $$P[\cdot]$$.
The distribution itself doesn't have enough information to capture $$P[\cdot
| B]$$, but maybe *you* have enough information and can extend your
model to give values to probabilities conditioned on $$B$$.

2. If $$B$$ is given as the level set of a random variable (i.e., $$B= \{X
= x\}$$ for some random variable $$X$$), then you may consider using the
*regular conditional probability*. This is a concept that we will describe
later in this series of posts, but it will require some preliminary work.


 So what goes
wrong? Why can't there be some way 

# The Borel-Kolmogorov paradox

 This is an
example in which points are sampled from a sphere, uniformly with respect to
surface area. Let $$\lambda$$ be the longitude function on the sphere, and
$$\phi$$ be the latitude. Then $$\lambda=0$$ and $$\phi=0$$ are both great
circles on the sphere, and one would naturally expect the conditional density
to be uniform on each great circle. However, upon calculating the conditional
density in what appears to be the natural way, one finds that the density for
$$\phi=0$$ is uniform, but that for $$\lambda=0$$ is not.

This is a fine and historically important example, but it's not the one I will
be focusing on for two reasons:


# A simple example

Let $$\Omega$$ be the upper half of the unit disk in the plane; that is,
$$\Omega = \{(x,y) \in \mathbb R^2 : 0 \le y; x^2+y^2 \le 1 \}$$.

XXX picture of Omega.

Sample points from $$\Omega$$ uniformly with respect to area, and let $$(X,Y)$$
be random variables representing the $$x$$ and $$y$$ coordinates of the sampled
points. That is, $$(X,Y)$$ has the uniform density $$\frac 1 \pi$$ on
$$\Omega$$.

Let $$W = X^2+Y^2$$. We are going to attempt to calculate the conditional
expectation $$\E[Y|W=\frac 1 2]$$ in the way that seems intuitively clear to
most people. (Just conditional *expectation* for now. Conditional probability
will wait until a later post in this series.)

XXX picture of W.

Since $$(X,Y)$$ is sampled uniformly with respect to area, it seems natural to
assume that the conditional probability $$\P[(X,Y) \in U | W=\frac 1 2]$$ has
uniform density with respect to arc length. This is the assumption that makes
the Borel-Kolmogorov paradox seem paradoxical.

Let $$\gamma$$ be the half circle determined by the condition $$W=\frac 1 2$$.
Then we calculate

$$\E\left[Y \Big| W=\frac 1 2\right] = \frac{\int_\gamma y \, ds}
{\text{length of } \gamma} = \frac{\sqrt 2}{\pi} \approx 0.450 . $$

So it appears that the average value of $$Y$$ when $$W=\frac 1 2$$ is about
$$0.45$$. Let's introduce a new random value $$Z = 2X$$. Then $$W
= \frac{Z^2}{4} + Y^2$$. Let's call the image of $$\Omega$$ in the $$ZY$$ plane
$$\Omega'$$. Then $$\Omega'$$ is half of an elliptical disk rather than
a circular disk, and the curve $$W=\frac 1 2$$ is a half-ellipse:

XXX image of Omega' with $$W$$

The important thing to note is that $$(Z, Y)$$ is sampled from $$\Omega'$$
uniformly with respect to area, just as $$(X, Y)$$ is sampled from $$\Omega$$
uniformly with respect to area.

Now we'll attempt to do the same calculation as above, but this time we'll use
the coordinates $$(Z,Y)$$. Let $$\gamma'$$ be the curve determined by
$$W=\frac 1 2$$ in the $$ZY$$ plane, and we find

$$\E\left[Y \Big| W=\frac 1 2\right] = \frac{\int_{\gamma'} y \, ds}
{\text{length of } \gamma'} \approx 0.484 . $$

(This required a numerical integration since these integrals cannot be computed
in elementary terms.)

Clearly we obtain two different answers depending on which coordinates we use.
The problem is that there are changes of coordinates which preserve the
property of being a uniform distribution, but which do not preserve average
values of functions along curves.

To put it another way, the probability distribution itself does not contain
enough information to determine the expectation conditioned on an event of
probability 0.

# Another way of looking at the problem

Suppose you could not see the probability distribution $$\P[\cdot]$$ on
$$\Omega$$ explicitly, but you could sample points from it. How would you
estimate $$\E[X|B]$$? You would sample many points from $$\Omega$$, collect the
points $$\{p_i\}_{i=1}^n$$ that were in the event $$B$$, and then calculate

$$\frac{\sum_{i=1}^n X(p_i)}{n} . $$

The problem is that if $$B$$ has probability 0, then even if we sample
infinitely many points, the probability that any of our points are in $$B$$ is
still 0, so there is no way to perform the necessary calculation.

