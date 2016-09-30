---
layout: post
title: "Preliminary comments on Jaynes's Probability Theory: The Logic of Science"
---

$$\newcommand{\P}{\mathbf P}$$

E.T. Jaynes was a physicist at Washington University in St. Louis. He died in
1998, but his book *Probability Theory: The Logic of Science* was posthumously
published in 2003 from his unfinished manuscript. The book is not so much about
probability theory as a mathematician would understand the term, but instead is
an introduction to Bayesian statistical inference. Moreover, Jaynes takes an
unusual starting point for his theory, completely discarding traditional
measure-theoretic probability theory, and instead basing his inferential
procedures on the notion of probability theory as an extended logic.

To illustrate this difference, consider the common introductory problem in
probability (which Jaynes also uses) that begins with colored balls in an urn.
Suppose there are 2 red balls and 3 white, and we are to reach into the urn and
pull out a ball. If I were a traditional probabilist, I might create a sample
space consisting of the five items $$\{R_1,R_2,W_1,W_2,W_3\}$$, corresponding
to the outcome that we drew the first red ball, the second red ball, the first
white ball, and so on. Then I would assign probabilities to each outcome: in
the absence of any additional information, it seems the reasonable thing to do
is to assign equal probability to each outcome, and thus each one is assigned
the probability $$\frac 1 5$$. Then if I were to ask myself, "What is the
probability I will draw a red ball?", I would proceed by letting $$C$$ be the
random variable into the space $$\{R, W\}$$ that maps each $$R_i$$ to $$R$$ and
each $$W_i$$ to $$W$$. The probability that I will draw a red ball is
$$\P[C=R]=\P[C^{-1}(R)]=\P[R_1]+\P[R_2] = \frac 2 5$$. Of course in practice we
wouldn't need to do everything quite so explicitly for such a simple problem,
but that's the underlying process.

In contrast, Jaynes assigns probabilities directly to propositions. Thus, he
might assign the probability $$\frac 1 5$$ to each of the propositions *I drew
the first red ball*, *I drew the second red ball*, and so on. Then, based on
certain quantitative rules for probabilistic reasoning Jaynes introduces in
Chapter 2, he concludes that the probability of the proposition *I drew a red
ball* is the sum of the probability of the propositions *I drew the $$i$$th red
ball* for $$i=1,2$$, or $$2 5$$. In this way Jaynes (claims to) circumvent the
entire measure theoretic apparatus of probability theory.

I like a lot of things about this book, and in fact found its perspective
enlightening. I might write a later blog post about that. However, this post
will focus on several things I do not like. Jaynes has a lot of complaints with
modern mathematics. He doesn't think mathematics is in a "healthy state." This
is all a lot of nonsense, based on misunderstandings that were resolved within
mathematics over a century ago, and well understood by essentially every
mathematician today.

# Limits

Jaynes displays a considerable amount of anxiety about limits and infinite
sets. I'm not sure if he would have described himself as
a [finitist](https://en.wikipedia.org/wiki/Finitism), but his statements
certainly resemble that philosophy. His worries resemble those of 19th century
mathematicians, and seem completely anachronistic today. To a modern
mathematician, there is a simple and precise definition of the term *limit*,
which has been extensively tested and found to capture exactly the features one
wants limits to have. In taking a limit operation, a mathematician simply
ensures that the result follows from the definition.[^1]

[^1]:
    Actually, the situation in general is more complicated. What exactly
a limit means depends on the space under consideration, and it may take work to
determine which space is appropriate to use. However, this is a complete
nonissue in the mathematically simple problems Jaynes consider.

For Jaynes, there appears to be no definition of a limit and no precise way to
ensure that one's limiting procedures are acceptable. Instead, when one must
take a limit, one must use ad hoc methods to arrive at the result, and
carefully check that one's results correspond with intuition.

In section 15.2, Jaynes illustrates that one cannot sum an infinite series by
arbitrarily rearranging and cancelling terms the way one naively might expect.
He gives the impression that this is a phenomenon not understood by modern
mathematicians, who are frequently making errors due to taking limits
incorrectly. This is of course absurd. Every student of mathematics who has
understood his elementary real analysis class knows that this is not a valid
way to sum series, because it does not follow from the definition of a limit.
There is no need to follow Jaynes's vague dictum, "Apply the ordinary processes
of arithmetic and analysis only to expressions with a finite number $$n$$ of
terms." There is only a need to understand what a limit actually is.

At the end of section 15.7, Jaynes described what is elsewhere called Borel's
paradox. Let $$(\theta, \phi)$$ be longitudinal and latitudinal coordinates on
the unit sphere. Given the uniform distribution on the unit sphere, the
conditional density of $$\theta$$ given a fixed $$\phi$$ is uniform (as one
would expect), while the conditional density of $$\phi$$ given a fixed
$$\theta$$ varies with $$\phi$$ (which is perhaps counterintuitive). Actually,
with a little thought this is not so counterintuitive after all. The key is to
notice that while the density on the sphere is uniform, the random variable
$$\phi$$ is *not*. If we pick a random point on the sphere, we are more likely
to pick a point near the equator than near the north poles. Given that fact,
*of course* we shouldn't expect $$\phi$$ to be uniformly distributed after
conditioning: it wasn't uniformly distributed to begin with.

Jaynes asserts that Borel's paradox arises because one must define the limiting
operation used before calculating a conditional probability. Actually,
shockingly, he says one cannot even define 'great circle' without defining the
limiting operation used to produce it. Jaynes has missed the point in
spectacular fashion. Great circles are easily defined and that is not at issue
here. Instead, one must clearly and precisely define conditional probabilities
(which Jaynes never does), and then consistently apply that definition in each
case. Jaynes's preference for ad hockery over clear definitions has gotten him
into trouble.

# Cox's Theorem

This book brought the so-called Cox's Theorem to my attention. In Jaynes's
description (which occupies parts of Chapters 1 and 2), this theorem asserts
that if we wish our probabilistic reasoning to follow certain intuitively
obvious rules, we have no choice but to follow all the rules of probability
theory as described in the book.

The problem, as is often the case with non-mathematician writers writing
mathematical works, is that Jaynes never clearly states the theorem.
I understand that many casual readers of mathematics are turned off by the
Theorem-proof format that mathematicians often use. It can be boring or
intimidating or otherwise a turnoff. But its great advantages are

1. it encourages the writer to precisely state his claim and its proof, in one
place;

2. it allows the reader to easily identify the important statements and their
proofs.

Instead, Jaynes states a very vague, rough version of the theorem, but feels
free to introduce extra hypotheses throughout his proof. I still don't actually
know exactly what the theorem says (someday I will read Cox's work to find
out).

# Bogus nondifferentiable functions

In the appendix B.5.3, Jaynes discusses nondifferentiable functions. His
thesis in this section is hard to discern, but he seems to make the following
points:

1. nondifferentiable functions are useless, and mathematicians are foolish for
spending so much time on them;

2. the delta function is very useful, and mathematicians are foolish
for not utilizing it;

This is inane for a variety of reasons. Most obviously, mathematicians use the
delta function extensively and have developed the theory of distributions (or
generalized functions) around it.

Beyond that, points 1 and 2 are very obviously in conflict. The delta function
is the ultimate representative example of why functions that were formerly
considered badly behaved are important. In fact, the delta function is so badly
behaved that it's not actually even a function! Moreover, even if you don't
think you have any use for (say) Weierstrass's example of a continuous, nowhere
differentiable function, it turns out that in order to construct a reasonable
mathematical theory that includes the delta function, you *have* to include all
continuous functions, and a lot more besides. See any book on distributions.

At the end of this section, Jaynes writes

> Note, therefore, that we stamp out this plague too, simply by defining the term
> 'function' in the way appropriate to our subject. The definition of
> a mathematical concept that is 'appropriate' to some field is the one that
> allows its theorems to have the greatest range of validity and useful
> applications, without the need for a long list of exceptions, special cases,
> and other anomalies. In our work the term 'function' includes good functions
> and well-behaved limits of sequences of good functions; but not
> nondifferentiable functions. We do not deny the existence of other definitions
> which do include nondifferentiable functions, any more than we deny the
> existence of fluorescent purple hair dye in England; in both case, we simply
> have no use for them.

At this point I have to wonder if Jaynes ever read a work by a mathematician
written later than 1920, because all modern mathematicians are very clear about
which functions their theory applies to, and feel free to ignore classes of
functions. The differences between what mathematicians do and what Jaynes
proposes are

1. mathematicians tend to carry around a label referring to the class of
functions under discussion; a mathematical work might consistently refer to
'analytic functions', rather than just saying at the outset 'in this work all
functions are analytic.' In practice this is a much better approach; how is
a casual reader turning to the middle of your book supposed to know that when
you say 'function' you mean 'analytic function'? Besides, what if the author
needs to occasionally refer to non-analytic functions?

2. mathematicians actually give clear definitions. Jaynes seems to believe that
he can just say 'good function' and the reader will somehow know which
functions he considers good. He also thinks he can say 'well-behaved limits',
and the reader will know what he means. This is bizarre, since he includes the
delta function but excludes continuous nondifferentiable functions, when by any
reasonable definition the latter are much more well-behaved.

# Measure theory

In section B.7, Jaynes discusses the Hausdorff sphere paradox. This is the
theorem that there are three congruent subsets $$X,Y,Z$$ of the sphere such
that their union nearly covers the sphere, and such that each of $$X,Y,Z$$ is
also congruent to $$X \cup Y$$. Jaynes says, "We are... puzzled by how
mathematicians can accept and publish such results; why do they not see in this
a blatant contradiction which invalidates the reasoning they are using?"

Apparently Jaynes's reasoning goes like this: subsets of the sphere are like
pieces of an orange peel. Since I can't divide an orange peel up into pieces
$$X,Y,Z$$ that have the characteristics of those subsets in the Hausdorff
sphere paradox, there must be something wrong with the mathematical framework
that produced the Hausdorff sphere paradox. The point that Jaynes has missed is
this: arbitrary subsets of the sphere are not good mathematical objects for
modeling pieces of an orange peel. Instead, *measurable* subsets of the sphere
are what one should use for modeling pieces of an orange peel. Measurable
subsets don't exhibit this behavior.

Here's an analogy. Imagine you are teaching calculus. A student comes to you and says,

"I need to make a mathematical model of the motion of this train along its
track. What mathematical object can I use for this purpose?"

You say, "Ah, you want the functions $$\mathbb R \to \mathbb R$$. The
independent variable is time, and the dependent variable is the position of the
train on the track."

Student: "Okay, great. Hey, wait a minute though! There are functions that
behave in crazy ways! Discontinuous functions and all kinds of weird stuff. My
train doesn't jump around like that! Isn't this an indication that something is
wrong with mathematics?"

You: "No, nothing is wrong with mathematics. By all means you can use only the
continuous funcions if that's all you need, but the other functions are still
there for those who need them."

Similarly, the fact that there exist nonmeasurable sets is not an obstacle to
modeling phenomena like orange peels.

# Conclusion

There's plenty more wrong with Jaynes's view of mathematics and mathematicians,
but this seems sufficient for this blog post. It's really unfortunate that such
an interesting work is marred by these inane, ill-informed digressions about
the nature of mathematics.
