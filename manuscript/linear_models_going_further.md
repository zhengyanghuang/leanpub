---
title: "Going further with linear models"
author: "Mike"
date: "02/19/2015"
output: html_document
layout: page
---

## Going Further

The R markdown document for this section is available [here](https://github.com/genomicsclass/labs/tree/master/linear/linear_models_going_further.Rmd).
Linear models can be extended in many directions. Here are some examples of extensions, which you might come across in analyzing data in the life sciences:

#### Robust linear models

In calculating the solution and its estimated error in the standard linear model, we minimize the squared errors. This involves a sum of squares from all the data points, which means that a few *outlier* data points can have a large influence on the solution. In addition, the errors are assumed to have constant variance (called *homoskedasticity*), which might not always hold true (when this is not true, it is called *heteroskedasticity*). Therefore, methods have been developed to generate more *robust* solutions, which behave well in the presence of outliers, or when the distributional assumptions are not met. A number of these are mentioned on the [robust statistics](http://cran.r-project.org/web/views/Robust.html) page on the CRAN website. For more background, there is also a [Wikipedia article](http://en.wikipedia.org/wiki/Robust_regression) with references.

#### Generalized linear models

In the standard linear model, we did not make any assumptions about the distribution of {$$}\mathbf{Y}{/$$}, though in some cases we can gain better estimates if we know that {$$}\mathbf{Y}{/$$} is, for example, restricted to non-negative integers {$$}0,1,2,\dots{/$$}, or restricted to the interval {$$}[0,1]{/$$}. A framework for analyzing such cases is referred to as *generalized linear models*, commonly abbreviated as GLMs. The two key components of the GLM are the *link function* and a probability distribution. The link function {$$}g{/$$} connects our familiar matrix product {$$}\mathbf{X} \boldsymbol{\beta}{/$$} to the {$$}\mathbf{Y}{/$$} values through:

{$$} \textrm{E}(\mathbf{Y}) = g^{-1}( \mathbf{X} \boldsymbol{\beta} ) {/$$}

R includes the function `glm` which fits GLMs and uses a familiar form as `lm`. Additional arguments include `family`, which can be used to specify the distributional assumption for {$$}\mathbf{Y}{/$$}. Some examples of the use of GLMs are shown at the [Quick R](http://www.statmethods.net/advstats/glm.html) website. There are a number of references for GLMs on the [Wikipedia page](http://en.wikipedia.org/wiki/Generalized_linear_model). 

#### Mixed effects linear models

In the standard linear model, we assumed that the matrix {$$}\mathbf{X}{/$$} was *fixed* and not random. For example, we measured the frictional coefficients for each leg pair, and in the push and pull direction. The fact that an observation had a {$$}1{/$$} for a given column in {$$}\mathbf{X}{/$$} was not random, but dictated by the experimental design. However, in the father and son heights example, we did not fix the values of the fathers' heights, but observed these (and likely these were measured with some error). A framework for studying the effect of the randomness for various columns in {$$}X{/$$} is referred to as *mixed effects* models, which implies that some effects are *fixed* and some effects are *random*. One of the most popular packages in R for fitting linear mixed effects models is [lme4](http://lme4.r-forge.r-project.org/) which has an accompanying paper on [Fitting Linear Mixed-Effects Models using lme4](http://arxiv.org/abs/1406.5823). There is also a [Wikipedia page](http://en.wikipedia.org/wiki/Mixed_model) with more references.

#### Bayesian linear models

The approach presented here assumed {$$}\boldsymbol{\beta}{/$$} was a fixed (non-random) parameter.  We presented methodology that estimates this parameter, along with standard errors that quantify uncertainty, in the estimation process. This is referred to as the _frequentist_ approach. An alternative approach is to assume that {$$}\boldsymbol{\beta}{/$$} is random and its distribution quantifies our prior beliefs about what {$$}\boldsymbol{\beta}{/$$} should be. Once we have observed data, then we update our prior beliefs by computing the conditional distribution, referred to as the _posterior_ distribution, of {$$}\boldsymbol{\beta}{/$$} given the data. This is referred to as the _Bayesian_ approach. For example, once we have computed the posterior distribution of {$$}\boldsymbol{\beta}{/$$} we can report the most likely outcome of an interval that occurs with high probability (credible interval). In addition, many models can be connected together in what is referred to as a *hierarchical model*. Note that we provide a brief introduction to Bayesian statistics and hierarchical models in a later chapter. A good reference for Bayesian hierarchical models is [Bayesian Data Analysis](http://www.stat.columbia.edu/~gelman/book/), and some software for computing Bayesian linear models can be found on the [Bayes](http://cran.r-project.org/web/views/Bayesian.html) page on CRAN. Some well known software for computing Bayesian models are [stan](http://mc-stan.org/) and [BUGS](http://www.mrc-bsu.cam.ac.uk/software/bugs/).

#### Penalized linear models

Note that if we include enough parameters in a model we can achieve a residual sum of squares of 0. Penalized linear models introduce a penalty term to the least square equation we minimize. These penalities are typically of the form, {$$}\lambda \sum_{j=1}^p \|\beta_j\|^k{/$$} and they penalize for large absolute values of {$$}\beta{/$$} as well as large numbers of parameters. The motivation for this extra term is to avoid over-fitting. To use these models, we need to pick {$$}\lambda{/$$} which determines how much we penalize. When {$$}k=2{/$$}, this is referred to as *ridge* regression, Tikhonov regularization, or L2 regularization. When {$$}k=1{/$$}, this is referred to as *LASSO* or L1 regularization. A good reference for these penalized linear models is the [Elements of Statistical Learning](http://statweb.stanford.edu/~tibs/ElemStatLearn/) textbook, which is available as a free pdf. Some R packages which implement penalized linear models are the [lm.ridge](https://stat.ethz.ch/R-manual/R-devel/library/MASS/html/lm.ridge.html) function in the MASS package, the [lars](http://cran.r-project.org/web/packages/lars/index.html) package, and the [glmnet](http://cran.r-project.org/web/packages/glmnet/index.html) package.

