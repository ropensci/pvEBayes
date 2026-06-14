# Fit a general-gamma, GPS, K-gamma, KM or efron model for a contingency table.

This function fits a non-parametric empirical Bayes model to an AE-drug
contingency table using one of several empirical Bayes approaches with
specified hyperparameter, if is required. Supported models include the
"general-gamma", "GPS", "K-gamma", "KM", and "efron".

## Usage

``` r
pvEBayes(
  contin_table,
  model = c("general-gamma", "K-gamma", "GPS", "KM", "efron"),
  alpha = NULL,
  K = NULL,
  p = NULL,
  c0 = NULL,
  maxi = NULL,
  tol_ecm = 1e-04,
  rtol_efron = 1e-10,
  rtol_KM = 1e-06,
  km_optimizer = c("ECOS", "CLARABEL", "SCS"),
  n_posterior_draws = 1000,
  E = NULL,
  message = TRUE,
  ...
)
```

## Arguments

- contin_table:

  an IxJ contingency table showing pairwise counts of adverse events for
  I AEs (along the rows) and J drugs (along the columns).

- model:

  the model to fit. Available models are "general-gamma", "K-gamma",
  "GPS", "KM" and "efron". Default to "general-gamma". Note that the
  input for model is case-sensitive.

- alpha:

  numeric between 0 and 1. The hyperparameter of "general-gamma" model.
  It is needed if "general-gamma" model is used. Small 'alpha'
  encourages shrinkage on mixture weights of the estimated prior
  distribution. See Tan et al. (2025) for further details.

- K:

  a integer greater than or equal to 2 indicating the number of mixture
  components in the prior distribution. It is needed if "K-gamma" model
  is used. When K is unknown, please consider its extension
  "general-gamma" instead. See Tan et al. (2025) for further details.

- p:

  a integer greater than or equal to 2. It is needed if "efron" mode is
  used. Larger p leads to smoother estimated prior distribution. See
  Narasimhan and Efron (2020) for detail.

- c0:

  numeric and greater than 0. It is needed if "efron" mode is used.
  Large c0 encourage estimated prior distribution shrink toward discrete
  uniform. See Narasimhan and Efron (2020) for detail.

- maxi:

  a upper limit of iteration for the ECM algorithm.

- tol_ecm:

  a tolerance parameter used for the ECM stopping rule, defined as the
  absolute change in the joint marginal likelihood between two
  consecutive iterations. It is used when 'GPS', 'K-gamma' or
  'general-gamma' model is fitted. Default to be 1e-4.

- rtol_efron:

  a tolerance parameter used when 'efron' model is fitted. Default to
  1e-10. See 'stats::nlminb' for detail.

- rtol_KM:

  a tolerance parameter used when 'KM' model is fitted. Default to be
  1e-6. See 'CVXR::solve' for detail.

- km_optimizer:

  a character vector specifying the optimizer(s) in CVXR used to fit the
  KM model. Supported values are `"ECOS"`, `"CLARABEL"`, and `"SCS"`.
  Note that the input for km_optimizer is case-sensitive. If multiple
  optimizers are supplied, they are tried sequentially and the first
  successfully fitted result is returned. Defaults to c("ECOS",
  "CLARABEL", "SCS")`. See `CVXR::psolve\` for detail.

- n_posterior_draws:

  a number of posterior draws for each AE-drug combination.

- E:

  A matrix of expected counts under the null model for the SRS frequency
  table. If `NULL` (default), the expected counts are estimated from the
  SRS data using 'estimate_null_expected_count()'.

- message:

  logical, indicating whether to print fitting information. Default to
  be TRUE.

- ...:

  additional parameters to be passed to optimizer for 'KM' model. See
  'CVXR::solve' for detail.

## Value

The function returns an S3 object of class `pvEBayes` containing the
estimated model parameters as well as posterior draws for each AE-drug
combination if the number of posterior draws is specified.

The `convergence` component is an integer code: `0` indicates successful
convergence of the optimizer, while `1` indicates that the optimizer did
not converge.

## Details

This function implements the ECM algorithm proposed by Tan et al.
(2025), providing a stable and efficient implementation of Gamma-Poisson
Shrinker(GPS), K-gamma and "general-gamma" methods for signal estimation
and signal detection in Spontaneous Reporting System (SRS) data table.

Method "GPS" is proposed by DuMouchel (1999) and it is a parametric
empirical Bayes model with a two gamma mixture prior distribution.

Methods "K-gamma" and "general-gamma" are non-parametric empirical Bayes
models, introduced by Tan et al. (2025). The number of mixture
components "K" needs to be prespecified when fitting a "K-gamma" model.
When the number of mixture components is unknown, we recommend using the
"general-gamma" model instead. For "general-gamma", the mixture weights
are regularized by a Dirichlet hyper prior with hyperparameter \\0 \leq
\alpha \< 1\\ that controls the shrinkage strength. As "alpha"
approaches 0, less non-empty mixture components exist in the fitted
model. When \\\alpha = 0\\, the Dirichlet distribution is an improper
prior still offering a reasonable posterior inference that represents
the strongest shrinkage of the "general-gamma" model.

Parameter estimation for the "KM" model is formulated as a convex
optimization problem. The objective function and constraints are
modified from the REBayes package (see 'REBayes::KWDual()'). Parameter
estimation is performed using the open-source convex optimization
package CVXR.

The implementation of the "efron" model in this package is adapted from
the deconvolveR package, developed by Bradley Efron and Balasubramanian
Narasimhan. The original implementation in deconvolveR does not support
an exposure or offset parameter in the Poisson model, which corresponds
to the expected null value (\\E\_{ij}\\) for each AE-drug combination.
To address this, we modified the relevant code to allow for the
inclusion of \\E\_{ij}\\ in the Poisson likelihood. In addition, we
implemented a method for estimating the degrees of freedom, enabling
AIC- or BIC-based hyperparameter selection for the "efron" model (Tan et
al. 2025). See
[`pvEBayes_tune`](https://yihaotancn.github.io/pvEBayes/reference/pvEBayes_tune.md)
for details.

## References

DuMouchel W. Bayesian data mining in large frequency tables, with an
application to the FDA spontaneous reporting system. *The American
Statistician.* 1999; 1;53(3):177-90.  

Tan Y, Markatou M and Chakraborty S. Flexible Empirical Bayesian
Approaches to Pharmacovigilance for Simultaneous Signal Detection and
Signal Strength Estimation in Spontaneous Reporting Systems Data.
*Statistics in Medicine.* 2025; 44: 18-19,
https://doi.org/10.1002/sim.70195.

Narasimhan B, Efron B. deconvolveR: A G-modeling program for
deconvolution and empirical Bayes estimation. *Journal of Statistical
Software*. 2020; 2;94:1-20.

Koenker R, Gu J. REBayes: an R package for empirical Bayes mixture
methods. *Journal of Statistical Software*. 2017; 4;82:1-26.

Fu, A, Narasimhan, B, Boyd, S. CVXR: An R Package for Disciplined Convex
Optimization. *Journal of Statistical Software*. 2020; 94;14:1-34.

## Examples

``` r

set.seed(1)

# fit general-gamma model with a specified alpha
fit <- pvEBayes(
  contin_table = statin2025_44,
  model = "general-gamma",
  alpha = 0.3,
  n_posterior_draws = 1000
)
#> ℹ Fitting general-gamma model...
#> ✔ Fitting general-gamma model... [171ms]
#> 
#> ℹ Generating 1000 posterior draws...
#> ✔ Generating 1000 posterior draws... [28ms]
#> 
#> Object of class 'pvEBayes'
#> 
#> General-gamma model with hyperparameter alpha = 0.3.
#> Estimated prior is a mixture of 18 gamma distributions.
#> 
#> Running time of the general-gamma model fitting: 0.1822 seconds.
#> Optimizer convergence: successful.
#> Running time for posterior draws 
#> (1000 signal strength posterior draws per AE-drug pair):0.0336 seconds.
#> 
#> Extract estimated prior parameters, discovered signals
#> and signal strength posterior draws using `summary()`.

# fit K-gamma model with K = 3
fit_Kgamma <- pvEBayes(
  contin_table = statin2025_44, model = "K-gamma",
  K = 3, n_posterior_draws = 1000
)
#> ℹ Fitting K-gamma model...
#> ✔ Fitting K-gamma model... [20ms]
#> 
#> ℹ Generating 1000 posterior draws...
#> ✔ Generating 1000 posterior draws... [26ms]
#> 
#> Object of class 'pvEBayes'
#> 
#> K-gamma model with number of gamma mixture components K = 3.
#> 
#> Running time of the K-gamma model fitting: 0.025 seconds.
#> Optimizer convergence: successful.
#> Running time for posterior draws 
#> (1000 signal strength posterior draws per AE-drug pair):0.0314 seconds.
#> 
#> Extract estimated prior parameters, discovered signals
#> and signal strength posterior draws using `summary()`.


# fit Efron model with specified hyperparameters
# p = 40, c0 = 0.05

fit_efron <- pvEBayes(
  contin_table = statin2025_44,
  model = "efron",
  p = 40,
  c0 = 0.05,
  n_posterior_draws = 1000
)
#> ℹ Fitting efron model...
#> ✔ Fitting efron model... [328ms]
#> 
#> ℹ Generating 1000 posterior draws...
#> ✔ Generating 1000 posterior draws... [30ms]
#> 
#> Object of class 'pvEBayes'
#> 
#> efron model is fitted with hyperparameters (p = 40, c0 = 0.05).
#> 
#> Running time of the efron model fitting: 0.3363 seconds.
#> Optimizer convergence: successful.
#> Running time for posterior draws 
#> (1000 signal strength posterior draws per AE-drug pair):0.0376 seconds.
#> 
#> Extract estimated prior parameters, discovered signals
#> and signal strength posterior draws using `summary()`.

# fit GPS model and comapre with 'openEBGM'


fit_gps <- pvEBayes(statin2025_44, model = "GPS")
#> ℹ Fitting GPS model...
#> ✔ Fitting GPS model... [24ms]
#> 
#> ℹ Generating 1000 posterior draws...
#> ✔ Generating 1000 posterior draws... [31ms]
#> 
#> Object of class 'pvEBayes'
#> 
#> GPS (2-gamma) model is fitted
#> 
#> Running time of the GPS model fitting: 0.0319 seconds.
#> Optimizer convergence: successful.
#> Running time for posterior draws 
#> (1000 signal strength posterior draws per AE-drug pair):0.036 seconds.
#> 
#> Extract estimated prior parameters, discovered signals
#> and signal strength posterior draws using `summary()`.

if (FALSE) { # \dontrun{

## Optional comparison with openEBGM (only if installed)

## tol_ecm is the absolute tolerance for ECM stopping rule.
## It is set to ensure comparability to `openEBGM`.

fit_gps <- pvEBayes(statin2025_44, model = "GPS", tol_ecm = 1e-2)

if (requireNamespace("openEBGM", quietly = TRUE)) {
  E <- estimate_null_expected_count(statin2025_44)
  statin2025_44_stacked <- as.data.frame(as.table(statin2025_44))
  statin2025_44_stacked$E <- as.vector(E)
  colnames(statin2025_44_stacked) <- c("var1", "var2", "N", "E")
  statin2025_44_stacked_squash <- openEBGM::autoSquash(statin2025_44_stacked)

  hyper_estimates <- openEBGM::hyperEM(statin2025_44_stacked_squash,
    theta_init = c(2, 1, 2, 2, 0.2),
    method = "nlminb",
    N_star = NULL,
    zeroes = TRUE,
    param_upper = Inf,
    LL_tol = 1e-2,
    max_iter = 10000
  )
}

theta_hat <- hyper_estimates$estimates
qn <- openEBGM::Qn(theta_hat,
  N = statin2025_44_stacked$N,
  E = statin2025_44_stacked$E
)

statin2025_44_stacked$q05 <- openEBGM::quantBisect(5,
  theta_hat = theta_hat,
  N = statin2025_44_stacked$N,
  E = statin2025_44_stacked$E,
  qn = qn
)

## obtain the detected signal provided by openEBGM
statin2025_44_stacked %>%
  subset(q05 > 1.001)

## detected signal from pvEBayes presented in the same way as openEBGM
fit_gps %>%
  summary(return = "posterior draws") %>%
  apply(c(2, 3), quantile, prob = 0.05) %>%
  as.table() %>%
  as.data.frame() %>%
  subset(Freq > 1.001)
} # }
```
