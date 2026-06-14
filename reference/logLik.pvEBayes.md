# Extract log marginal likelihood for a pvEBayes object

This function defines the S3 `logLik` method for objects of class
`pvEBayes`. It extracts the log marginal likelihood from a fitted model.

## Usage

``` r
# S3 method for class 'pvEBayes'
logLik(object, ...)
```

## Arguments

- object:

  a `pvEBayes` object, which is the output of the function
  [pvEBayes](https://yihaotancn.github.io/pvEBayes/reference/pvEBayes.md)
  or
  [pvEBayes_tune](https://yihaotancn.github.io/pvEBayes/reference/pvEBayes_tune.md).

- ...:

  other input parameters. Currently unused.

## Value

returns log marginal likelihood of a pvEBayes object.

## Examples

``` r

fit <- pvEBayes(
  contin_table = statin2025_44, model = "general-gamma",
  alpha = 0.3, n_posterior_draws = NULL
)
#> ℹ Fitting general-gamma model...
#> ✔ Fitting general-gamma model... [218ms]
#> 
#> Object of class 'pvEBayes'
#> 
#> General-gamma model with hyperparameter alpha = 0.3.
#> Estimated prior is a mixture of 18 gamma distributions.
#> 
#> Running time of the general-gamma model fitting: 0.2259 seconds.
#> Optimizer convergence: successful.
#> No posterior draws were generated.
#> 
#> Extract estimated prior parameters, discovered signals
#> and signal strength posterior draws using `summary()`.

logLik(fit)
#> [1] -1845.437
```
