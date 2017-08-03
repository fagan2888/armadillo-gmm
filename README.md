# gmm_diag and gmm_full: C++ classes for multi-threaded Gaussian mixture models and Expectation-Maximisation

The *gmm_diag* and *gmm_full* classes provide multi-threaded (parallelised) implementations
of Gaussian mixture models (GMMs) and the associated Expectation-Maximisation (EM) training algorithm.

The *gmm_diag* class is specifically tailored for diagonal covariance matrices
(all entries outside the main diagonal in each covariance matrix are assumed to be zero),
while the *gmm_full* class is tailored for full covariance matrices.
The *gmm_diag* class is typically much faster to train and use than the *gmm_full* class,
at the potential cost of some reduction in modelling accuracy.

The interface for the *gmm_diag* and *gmm_full* classes allows the user full control over the parameters for GMM fitting,
as well as easy and flexible access to the trained model.
Specifically, the two classes contain functions for likelihood evaluation,
vector quantisation, histogram generation, data synthesis, and parameter modification,
in addition to training (learning) the GMM parameters via the EM algorithm.
The classes use several techniques to improve numerical stability
and promote convergence of EM based training,
such as keeping as much as possible of the internal computations in the log domain,
and ensuring the covariance matrices stay positive-definite.

To achieve multi-threading, the EM training algorithm has been reformulated into a MapReduce-like framework 
and implemented with the aid of OpenMP pragma directives.
As such, the EM algorithm runs much quicker on multi-core machines when OpenMP is enabled during compilation
(for example, using the ```-fopenmp``` option in GCC and clang compilers).

The *gmm_diag* and *gmm_full* classes are included in version 7.960 of the Armadillo C++ library.
For installation of the Armadillo library, please see the `armadillo_readme.txt` file.

Documentation for the *gmm_diag* and *gmm_full* classes is available online: [http://arma.sourceforge.net/docs.html#gmm_diag](http://arma.sourceforge.net/docs.html#gmm_diag).
