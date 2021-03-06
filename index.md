+++
title = "Probability Theory"

date = 2020-09-27
lastmod = 2020-09-27
draft = false

tags = ["statistics", "Bayesian"]
summary = "A simple set of unifying principles for statistical inference"
abstract = "A simple set of unifying principles for statistical inference"
authors = ["Vassilis Kehayas"]
hasPlotly = false
doi = "10.5281/zenodo.4052076"
sourceFile = "src/probability-theory.Rmd"

+++



>How could we build a machine which would carry out useful plausible reasoning, following clearly defined principles expressing an idealized common sense? 

(Jaynes 2003) 

The ideal of systematizing the scientific process 
has been a principal pursuit for natural philosophers, 
such as Aristotle, Francis Bacon, Laplace, the Logical Positivists, 
and their successors. 
Aristotelian logic, in particular, 
was concerned with the truth of propositions 
such as “Socrates is an animal”.
The primary tool of Aristotle's system was *deduction*
---drawing conclusions that necessarily follow from an argument.
Much of the later work focused on providing 
the theoretical foundations for *induction*,
[defined by Aristotle](https://plato.stanford.edu/entries/aristotle-logic/)
as "argument from the particular to the universal",
i.e. inferring general conclusions from particular evidence.
Arguably most of modern science is concerned 
with induction rather than deduction.
The question in the opening quote can serve as a pragmatic abstraction of 
the primordial ideal in the setting of inductive inference.
Jaynes's thesis (Jaynes 2003) was that probability theory is
our best answer in the attempt to provide a unifying system
that can serve as a generalization of Aristotelian logic
extended to inferential reasoning.
Based on a reading of Jaynes' book[^1], 
"Probability Theory: The Logic of Science" (Jaynes 2003),
I will produce an exposition of theoretical and practical issues
in light of his arguments on the foundations of probability theory.

## Probability theory as extended logic  

Why should the systemization of inferential reasoning be our goal?
While we may be able to adequately evaluate the relative merit 
of two clearly distinguishable propositions or hypotheses,
we are helpless once the number of hypotheses or the relevant parameters
increases even slightly beyond that.
We need a formalized system
--a mathematical theory--
to help us reason through those more complicated problems
--and a machine to crunch the numbers.
Choosing a machine as the subject that is supposed to execute the reasoning
makes it clear that the goal is to write a computer program
and has the added benefit of avoiding 
the subjective/objective debate regarding prior information: 
the machine would benefit from using all available information, 
no matter what we call it.
Turning the problem into an engineering challenge
makes explicit that the challenge is
to choose the appropriate design principles to achieve our goal
rather than attain a potentially ill-defined truth,
as has been the case for Logical Positivists.
Jaynes defines "plausible reasoning" as a synonym to inference,
i.e. finding the most plausible answer to a question 
based on the available information under uncertainty.
The usage of "common sense" in the opening quote does not imply that 
human reasoning is infallible or always consistent, 
but rather that if our conclusions disagree with some basic desiderata 
we should discard the conclusions and the process that led us to them.

Jaynes posits a set of basic desiderata as a starting point for his reasoning:

I) Degrees of plausibility are represented by real numbers  

This desideratum is deemed necessary as the machine is required to 
associate plausibility assignments with some physical quantity
such as voltage or bits.
It does not appear as objectionable to adopt the convention that
a larger number corresponds to greater plausibility
and that an infinitesimal change of probability corresponds to an
infinitesimal change in plausibility.

II) Qualitative correspondence with common sense

The desideratum of qualitative correspondence with common sense requires
that the direction of change 
must be qualitatively consistent with our intuition.
For example, if our machine acquires new information $C'$ 
that updates the previously held information $C$
in a way that the plausibility of $A$ given $C'$ increases
compared to the plausibility of $A$ given $C$

$$ A|C' > A|C  $$

but the plausibility of $B$ is unchanged

$$  B|AC' = B|AC $$

then we should expect a) that the joint plausibility of $A$ and $B$ 
can only increase and never decrease

$$  AB|C' \geq AB|C $$

and b) a decrease in the plausibility that $A$ is false, $\overline{A}$.

III) Consistent reasoning: 

a) If a conclusion can be reasoned out in more than one way, 
then every possible way must lead to the same result.  
b) The robot always takes into account all of 
the evidence it has relevant to a question. 
It does not arbitrarily ignore some of the information, 
basing its conclusions only on what remains. 
In other words, the robot is entirely non-ideological.  
c) The robot always represents equivalent states of knowledge 
by equivalent plausibility assignments. 
That is, if in two problems the robot's state of knowledge is the same 
(except perhaps for the labelling of the propositions), 
then it must assign the same plausibilities in both.  

It is perhaps surprising at first that the above-stated conditions
uniquely identify a single set of mathematical operations that obey them
[but see Halpern (1999)].

Two rules follow based on those desiderata from 
[Cox's functional equations](https://en.wikipedia.org/wiki/Cox's_theorem):

1) The product rule:

If $A$ and $B$ are two statements,
we seek to calculate the plausibility of their conjunction, $AB$,
given that $C$ is true, $p(AB|C)$.
If $B$ is true given $C$,
then $B|C$ is true.
For both $A$ and $B$ to be true given that $B|C$ is true
then $A|BC$ also needs to be true.
Putting everything together,
the plausibility of $AB|C$ must be equal the plausibility of both
$A|BC$ and $B|C$

$$ p(AB|C) = p(A|BC)p(B|C) $$
But since we could just as well swap the labels of the statements
$A$ and $B$,
based on desideratum III the following relationship 
should also hold equivalently:

$$ p(AB|C) = p(B|AC)p(A|C) $$
The product rule combines our results:

$$ p(AB|C) = p(A|BC)p(B|C) = p(B|AC)p(A|C) $$ 

2) The sum rule
$$ p(A|B) + p(\overline{A}|B) = 1 $$

merely extends the basic Aristotelian postulate according to which
if $A$ is true, then not-$A$, or $\overline{A}$, must be false, and reversely.

>Aristotelian deductive logic is the limiting form of our rules for plausible reasoning, as the robot becomes more and more certain of its conclusions.

(Jaynes 2003)

## Discussion  

Accepting these seemingly unobjectionable corollaries 
leads to the adoption of 
[Bayesian inference](http://www.scholarpedia.org/article/Bayesian_statistics)

$$ p(H | E) = \frac{p(E | H) p(H)}{p(E)} $$
where $p(H|E)$ is called the *posterior distribution*,
the probability of the hypothesis $H$ given the evidence $E$,
$p(H)$ is the *prior probability*,
the probability of the hypothesis before observing the data,
and $p(E)$ is the normalizing factor when multiple hypotheses are considered,
for example when considering two competing hypotheses $H_1$ and $H_2$,
$p(E) = p(E|H_1)p(H_1) + p(E|H_2)p(H_2)$.

For those trained initially within the frequentist framework,
working under the Bayesian framework leads to questions
regarding the choice of priors 
and a re-evaluation of the concept of uncertainty.
Bayesian inference comes with some benefits in estimating relatively complex
models that are not as easy to fit within the frequentist framework
in a general way and
a simplification of their interpretation, as well as some drawbacks, 
mostly revolving around computational cost.
We will briefly discuss those issues in the following sections.

### Bayesian and frequentist inference  

#### Conceptual juxtaposition  

The ultimate goal of the frequentist approach is to
estimate how likely are the data we observed, $y$,
given a set of fixed parameters, $\theta$,
designated as $p(y|\theta)$.
It, thus, considers that the uncertainty in the data is irreducible, 
or aleatoric.
Data distributions are chosen based on imaginary projections
to future samples generated from the same process.
The proximal goal has traditionally been 
to minimise the model's prediction error
on future samples.

The Bayesian approach is designed to estimate
how likely a hypothesis $H$ is,
given the data $D$ we observed, $p(H|D)$.
Hence, it takes the observed data as definite,
measurement errors and all,
and considers that the final source of uncertainty is epistemic,
arising due to lack of information.
Since often our hypotheses are defined
to encompass a range of values,
probability distributions are assigned over a model's parameters.
The goal is to update our beliefs
to new ones that are more consistent with the observed data.

The tension between the two approaches on the nature of uncertainty
delineates a philosophical issue that cannot be easily resolved.
One the one hand, uncertainty can always be reduced 
to progressively lower levels of description,
but on the other, 
it is an open question whether it can be completely eliminated.
For example, the exact position an arrow is going to land on
can be difficult to determine
---that is why archery is an interesting sport to some.
But, in principle, if we had information about all the relevant parameters,
down to a complete description of the wind patterns and the gravitational field,
we should be able to precisely predict the arrow's final position.
Ultimately, it boils down to the question of whether
the universe is deterministic, which must involve 
some discussion around the state of quantum physics
that still appears to remain unresolved.
 
#### Practical considerations  

In practice, though, it rarely is relevant for most experimenters
to invoke levels of description that involve quantum physics.
The choice of analytical framework is most often made
based on the particular goals of the scientific question at hand.
In situations where the models specified are relatively simple
and the samples considered are large enough,
it is sufficient to adopt the frequentist approach
to get an accurate answer fast.
However, in many actual scientific problems
the underlying models are, or should be,
complicated to such a degree that the frequentist approach does not provide
satisfactorily powerful tools
that are as easy to implement in a general way.
Furthermore, if the question the experimenter asks is 
“What have I learned from the data regarding my hypothesis 
after seeing the data?", 
it cannot be reasonably answered 
unless the available information about the hypothesis 
before seeing the data is also specified.

##### The choice of priors  

Even people who accept the conclusions 
of the logical analysis presented in the opening section 
regard the choice of the prior probability as a thorny issue. 
One objection often raised is that the prior can only be subjectively chosen,
something seen as going against 
the goal of objectivity pursued in scientific practice.
However, whereas the choice of the prior probability is in one sense subjective,
as it is relative to the information available to the agent doing the reasoning,
it is also objective in the sense that 
any agent that has access to the same information 
must choose the same prior probability.
There remains the practical issue of translating our prior beliefs into 
specific values of prior probabilities.
An effective way to choose priors 
is to inspect prior predictive distributions,
which provide a way to examine the range and likely values
of responses our priors would produce
before seeing any data:

$$ p(y, \theta) = p(y|\theta)p(\theta) $$
where $p(\theta)$ is our prior distribution
and $p(y|\theta)$ is the sampling distribution.
If the prior predictive distribution generates values
that are beyond what we would consider reasonable before seeing the data,
we must adjust our priors accordingly.
Of course, this method of prior elicitation 
can only narrow down the range of parameter values 
---the exact parameter values are often impossible to define
unless we have specific information 
from previous studies or other expert knowledge.
In cases where the sample size is adequately large
or the prior is not so specific that its influence dominates that of the data,
the choice of values within that reasonable range
will make little difference in the result.
If, however, the choice of the prior makes a difference to the results,
it is arguably a useful feature of the analytical framework 
to be able to report it so that people can evaluate its reasonableness.

The alternative of using frequentist inference,
which is equivalent to assuming a uniform prior[^2],
is rarely a defensible approach 
since there is always some additional information available:
the coefficient of your experimental variable 
is *a priori* unlikely to take values equal to $- \infty$, 
the Avogadro constant, and everything in between with equal plausibility.
Using uniform priors often leads to practical problems,
such as edge effects at the parameter space boundaries
and an inability to converge in the presence 
of collinearity among the predictors.
To be sure, there are ways to circumvent those problems in some cases
under the frequentist framework.
For instance, both of those problems
can be addressed by regularization approaches.
But it is easy to show (Hastie, Tibshirani, & Friedman 2017, p. 91) 
that these are in turn
equivalent to choosing appropriate priors under the Bayesian framework.
The difference is that the choice of the equivalent Bayesian priors
can be carried out in a more principled way 
and that priors can help avoid issues of "double dipping",
i.e. using the data twice, 
once to optimize the hyperparameters of the frequentist regularization 
and to then later produce inferences based on them,
something that undermines their predictive ability[^3].

##### Paedagogical value  

An important factor based on which someone may prefer the Bayesian approach
is that it appears to more closely match
the way that scientists tend to think
as is evident by the observation that it is very often the case
that frequentist $p$-values are misinterpreted
as Bayesian posterior probabilities
---as if answering the question 
"*How likely is my hypothesis given the observed data?*"---
or otherwise misinterpret them (Lecoutre, Lecoutre, & Poitevineau 2001; McShane & Gal 2017).
The opposite misunderstanding is much more rarely observed.

Another practical advantage that Bayesian inference has
over frequentist statistics is that through its simple unifying principles
the Bayesian analyst is enabled to 
more easily combine different analytical techniques
compared to the seemingly unrelated methods
of the frequentist framework
(e.g. regularization, multiple imputation, robust statistics, meta-analysis, "mixed models")[^4].
As a consequence, the Bayesian can come closer to fitting 
[the model that the data deserve](https://betanalpha.github.io/assets/case_studies/modeling_and_inference.html)
instead of being restricted by feasibility constraints.
The impetus towards adherence to simple unifying principles 
under the Bayesian framework 
raises opportunities to make more principled modelling choices.
In contrast, within the frequentist framework,
one often faces challenges that cannot all be addressed at the same time
and can become inconspicuous as a consequence
or, worse, be swept under the rug.

Based on the discussion so far,
[one is left wondering whether Bayesian methods should be considered
as the default method for statistical inference](http://babieslearninglanguage.blogspot.com/2018/02/mixed-effects-models-is-it-time-to-go.html),
especially in cases where the research question can be framed
as a [hierarchical/mixed-effects/varying intercept and/or slope model estimation problem]({{< ref "/post/glmm-examples/index.md" >}}).
I would argue that they probably should
unless the model is simple, 
you have little to no prior information, 
and enough data are available
---unless you find the Bayesian interpretation of posterior probabilities 
useful in those case as well and computational cost is not a major concern.
With the advent of user-friendly, yet powerful software packages such as [`brms`](https://cran.r-project.org/web/packages/brms/index.html)
and the continuous increase in computational power
there is little reason for those convinced by argumentation
along similar lines to those followed in this blog post to hold back.
I will explore the super-powers `brms` can give you 
in separate blog posts to follow.

##### Obstacles for the adoption of Bayesian inference and limitations  

Although Bayesian inference had a head start with the work of
Bayes and Laplace, among others,
progress stalled,
in large part because problems 
beyond the most simple cases where analytically intractable.
A breakthrough that lead to increased adoption of Bayesian inference
was the development of sampling methods such as
[Markov-chain Monte Carlo](https://en.wikipedia.org/wiki/Markov_chain_Monte_Carlo) (MCMC)
that required intensive computer simulations.
More refined algorithms (Hoffman & Gelman 2011) are now in wide use
but those too require lengthier computation times
as compared to approximate frequentist inference,
although of comparable orders of magnitude for simple models.
Perhaps variational (Bayesian) inference methods 
will be more used in the future 
as they usually run faster compared to sampling methods,
although their results are also approximate.
[Within-chain parallelization](https://github.com/paul-buerkner/brms/issues/892)
is another promising approach for speeding up computation of certain models.

##### Mixed approaches

Jaynes' often polemic tone is not widespread nowadays, 
and that's probably for the better.
Many mix-and-match approaches are currently widely used,
such as multiple imputation,
regularization, which can be seen as one way to incorporate priors
within the frequentist framework,
and mixed-effects (otherwise called multi-level or hierarchical) models
in frequentist inference.

In summary, probability theory as extended logic,
or simply Bayesian inference as it is often called,
is a far-reaching theory that extends binary logic
to problems of inference under uncertainty
based on apparently defensible desiderata.

[^1]: Mostly the first two chapters where he unfolds the foundations of Probability Theory as logic. The rest of the book merely extends and further explains the corollaries of those first two chapters.

[^2]: Even if useful to understand some differences between the Bayesian and the frequentist frameworks, this statement is simplifying some of the underlying conceptual differences which we discussed above.

[^3]: Similar points can be made regarding other frequentist tools such as [equivalence tests](https://doingbayesiandataanalysis.blogspot.com/2017/02/equivalence-testing-two-one-sided-test.html) and the perils of practices such as [repeated sampling](https://statmodeling.stat.columbia.edu/2014/02/13/stopping-rules-bayesian-analysis/), which both are of lesser concern for Bayesian inference.

[^4]: Even if the frequentist framework is based on [Kolmogorov's axioms](https://en.wikipedia.org/wiki/Probability_axioms), when it comes to inference the different sub-schools of thought (the [Likelihood school](https://en.wikipedia.org/wiki/Likelihoodist_statistics), [Fisherian significance testing framework, or the Neymar-Pearson's hypothesis testing framework](https://en.wikipedia.org/wiki/Foundations_of_statistics)) can lead to incongruent conceptualizations.


## References  

Halpern, J.Y., 1999. A Counterexample to Theorems of Cox and Fine. Journal of AI research 10, 67–85.

Hastie, T., Tibshirani, R., Friedman, J.H., 2017. The elements of statistical learning: data mining, inference, and prediction.

Hoffman, M.D., Gelman, A., 2011. The No-U-Turn Sampler: Adaptively Setting Path Lengths in Hamiltonian Monte Carlo. arXiv:1111.4246 [cs, stat].

Jaynes, E.T., 2003. Probability Theory: The Logic of Science. Cambridge University Press.

Lecoutre, B., Lecoutre, M.-P., Poitevineau, J., 2001. Uses, Abuses and Misuses of Significance Tests in the Scientific Community: Won’t the Bayesian Choice Be Unavoidable? International Statistical Review / Revue Internationale de Statistique 69, 399–417. https://doi.org/10.2307/1403453

McShane, B.B., Gal, D., 2017. Statistical Significance and the Dichotomization of Evidence. Journal of the American Statistical Association 112, 885–895. https://doi.org/10.1080/01621459.2017.1289846


