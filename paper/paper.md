---
title: 'gmm_diag and gmm_full: Multi-Threaded C++ Implementations of Gaussian Mixture Models and Expectation-Maximisation'
tags:
  - modelling
  - statistics
  - numerics
authors:
 - name: Conrad Sanderson
   orcid: 0000-0002-0049-4501
   affiliation: 1, 2, 4
 - name: Ryan Curtin
   orcid: 0000-0002-9903-8214
   affiliation: 3, 4
affiliations:
  - name: Data61, CSIRO, Australia
    index: 1
  - name: University of Queensland, Australia
    index: 2
  - name: Symantec Corporation, USA
    index: 3
  - name: Arroyo Consortium
    index: 4
date: 2 August 2016
bibliography: paper.bib
---

# Summary

Modelling multivariate data through a convex mixture of Gaussians,
also known as a Gaussian mixture model (GMM),
has many uses in fields such as signal processing,
statistics, econometrics, pattern recognition, and machine learning [@Bishop_2006].
Each Gaussian component in a GMM is described with a weight, mean vector (centroid), and covariance matrix.

*gmm_diag* and *gmm_full* are C++ classes which provide multi-threaded (parallelised) implementations of GMMs
and the associated Expectation-Maximisation (EM) training algorithm [@Moon96,@McLachlan_2008].
The *gmm_diag* class is specifically tailored for diagonal covariance matrices
(all entries outside the main diagonal in each covariance matrix are assumed to be zero),
while the *gmm_full* class is tailored for full covariance matrices.
The *gmm_diag* class is typically much faster to train and use than the *gmm_full* class,
at the potential cost of some reduction in modelling accuracy.

The interface for the *gmm_diag* and *gmm_full* classes
allows the user full control over the parameters for GMM fitting,
as well as easy and flexible access to the trained model.
Specifically, the two classes contain functions for likelihood evaluation,
vector quantisation, histogram generation, data synthesis, and parameter modification,
in addition to training (learning) the GMM parameters via the EM algorithm.
The classes use several techniques to improve numerical stability
and promote convergence of EM based training,
such as keeping as much as possible of the internal computations in the log domain,
and ensuring the covariance matrices stay positive-definite.

To achieve multi-threading, the EM training algorithm has been reformulated into a MapReduce-like framework [@MapReduce_2004]
and implemented with the aid of OpenMP pragma directives [@OpenMP_2007].
As such, the EM algorithm runs much quicker on multi-core machines when OpenMP is enabled during compilation
(for example, using the -fopenmp option in GCC and clang compilers).

The *gmm_diag* and *gmm_full* classes are included in version 7.960 of the Armadillo C++ library [@Armadillo_2016],
with the underlying mathematical details described in [@Arxiv_1707_09094].
The documentation for the classes is available online^[http://arma.sourceforge.net/docs.html#gmm_diag].

# References
