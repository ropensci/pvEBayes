# Generate posterior draws for each AE-drug combination

This function generates posterior draws from the posterior distribution
of \\\lambda\_{ij}\\ for each AE-drug combination, based on a fitted
empirical Bayes model. The posterior draws can be used to compute
credible intervals, visualize posterior distributions, or support
downstream inference.

## Usage

``` r
posterior_draws(obj, n_posterior_draws = 1000, verbose = TRUE)
```

## Arguments

- obj:

  a `pvEBayes` object, which is the output of the function
  [pvEBayes](https://yihaotancn.github.io/pvEBayes/reference/pvEBayes.md)
  or
  [pvEBayes_tune](https://yihaotancn.github.io/pvEBayes/reference/pvEBayes_tune.md).

- n_posterior_draws:

  number of posterior draws for each AE-drug combination.

- verbose:

  logical. If is TRUE (default), a progress bar is displayed to the
  console.

## Value

The function returns an S3 object of class `pvEBayes` with posterior
draws.

## Examples

``` r

fit <- pvEBayes(
  contin_table = statin2025_44, model = "general-gamma",
  alpha = 0.3, n_posterior_draws = NULL
)
#> ℹ Fitting general-gamma model...
#> ✔ Fitting general-gamma model... [128ms]
#> 
#> Object of class 'pvEBayes'
#> 
#> General-gamma model with hyperparameter alpha = 0.3.
#> Estimated prior is a mixture of 18 gamma distributions.
#> 
#> Running time of the general-gamma model fitting: 0.1331 seconds.
#> Optimizer convergence: successful.
#> No posterior draws were generated.
#> 
#> Extract estimated prior parameters, discovered signals
#> and signal strength posterior draws using `summary()`.

fit_with_draws <- posterior_draws(fit, n_posterior_draws = 1000)
#> ℹ Generating 1000 posterior draws...
#> ✔ Generating 1000 posterior draws... [24ms]
#> 
```
