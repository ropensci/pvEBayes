# A suite of empirical Bayes methods to use in pharmacovigilance.

`pvEBayes` provides a collection of parametric and non-parametric
empirical Bayes methods implementation for pharmacovigilance (including
signal detection and signal estimation) on spontaneous reporting systems
(SRS) data.

An SRS dataset catalogs AE reports on *I* AE rows across *J* drug
columns. Let \\N\_{ij}\\ denote the number of reported cases for the
*i*-th AE and the *j*-th drug, where \\i = 1,..., I\\ and \\j = 1,...,
J\\. We assume that for each AE-drug pair, \\N\_{ij} \sim
\text{Poisson}(\lambda\_{ij} E\_{ij})\\, where \\E\_{ij}\\ is expected
baseline value measuring the expected count of the AE-drug pair when
there is no association between *i*-th AE and *j*-th drug. The parameter
\\\lambda\_{ij} \geq 0\\ represents the relative reporting ratio, the
signal strength, for the \\(i, j)\\-th pair measuring the ratio of the
actual expected count arising due to dependence to the null baseline
expected count. Current disproportionality analysis mainly focuses on
*signal detection* which seeks to determine whether the observation
\\N\_{ij}\\ is substantially greater than the corresponding null
baseline \\E\_{ij}\\. Under the Poisson model, that is to say, its
signal strength \\\lambda\_{ij}\\ is significantly greater than 1.

In addition to *signal detection*, Tan et al. (*Stat. in Med.*, 2025)
broaden the role of disproportionality to *signal estimation*. The use
of the flexible non-parametric empirical Bayes models enables more
nuanced empirical Bayes posterior inference (parameter estimation and
uncertainty quantification) on signal strength parameter \\\\
\lambda\_{ij} \\\\. This allows researchers to distinguish AE-drug pairs
that would appear similar under a binary signal detection framework. For
example, the AE-drug pairs with signal strengths of 1.5 and 4.0 could
both be significantly greater than 1 and detected as a signal. Such
differences in signal strength may have distinct implications in medical
and clinical contexts.

The methods included in `pvEBayes` differ by their assumptions on the
prior distribution. Implemented methods include the Gamma-Poisson
Shrinker (GPS), Koenker-Mizera (KM) method, Efron’s nonparametric
empirical Bayes approach, the K-gamma model, and the general-gamma
model.

The GPS model uses two gamma mixture prior by assuming the
signal/non-signal structure in SRS data. However, in real-world setting,
signal strengths \\(\lambda\_{ij})\\ are often heterogeneous and thus
follows a multi-modal distribution, making it difficult to assume a
parametric prior. Non-parametric empirical Bayes models (KM, Efron,
K-gamma and general-gamma) address this challenge by utilizing a
flexible prior with general mixture form and estimating the prior
distribution in a data-driven way.

`pvEBayes` offers the first implemention of the bi-level Expectation
Conditional Maximization (ECM) algorithm proposed by Tan et al. (2025)
for efficient parameter estimation in gamma mixture prior based models:
GPS K-gamma and general-gamma.

The KM method has an existing implementation in the `REBayes` package,
but it relies on Mosek, a commercial convex optimization solver, which
may limit accessibility due to licensing issue. `pvEBayes` provides a
alternative fully open-source implementation of the KM method using
`CVXR`.

Efron’s method also has a general nonparametric empirical Bayes
implementation in the `deconvolveR` package; however, that
implementation does not support an exposure or offset parameter in the
Poisson model, which corresponds to the expected null value \\E\_{ij}\\.
In `pvEBayes`, the implementation of the Efron's method is adapted and
modified from `deconvolveR` to support \\E\_{ij}\\ in Poisson model.

For a detailed introduction to `pvEBayes`, see Tan et al. (*arxiv*,
2025) and package Vignette.

## References

Tan Y, Markatou M and Chakraborty S. Flexible Empirical Bayesian
Approaches to Pharmacovigilance for Simultaneous Signal Detection and
Signal Strength Estimation in Spontaneous Reporting Systems Data.
*Statistics in Medicine.* 2025; 44: 18-19,
https://doi.org/10.1002/sim.70195.

Tan Y, Markatou M and Chakraborty S. pvEBayes: An R Package for
Empirical Bayes Methods in Pharmacovigilance. *arXiv*:2512.01057
(stat.AP). https://doi.org/10.48550/arXiv.2512.01057

Koenker R, Mizera I. Convex Optimization, Shape Constraints, Compound
Decisions, and Empirical Bayes Rules. *Journal of the American
Statistical Association* 2014; 109(506): 674–685,
https://doi.org/10.1080/01621459.2013.869224

Efron B. Empirical Bayes Deconvolution Estimates. *Biometrika* 2016;
103(1); 1-20, https://doi.org/10.1093/biomet/asv068

DuMouchel W. Bayesian data mining in large frequency tables, with an
application to the FDA spontaneous reporting system. *The American
Statistician.* 1999; 1;53(3):177-90.

## See also

Useful links:

- <https://github.com/ropensci/pvEBayes>

- Report bugs at <https://github.com/ropensci/pvEBayes/issues>

## Author

Yihao Tan, Marianthi Markatou, Saptarshi Chakraborty and Raktim
Mukhopadhyay.

Maintainer: Yihao Tan <yihaotan@buffalo.edu>
