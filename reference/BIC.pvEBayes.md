# Obtain Bayesian Information Criterion (BIC) for a pvEBayes object

This function defines the S3 `BIC` method for objects of class
`pvEBayes`. It extracts the Bayesian Information Criterion (BIC) from a
fitted model.

## Usage

``` r
# S3 method for class 'pvEBayes'
BIC(object, ...)
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

numeric, BIC score for the resulting model.

## Examples

``` r

fit <- pvEBayes(
  contin_table = statin2025_44, model = "general-gamma",
  alpha = 0.3, n_posterior_draws = NULL
)
#> ℹ Fitting general-gamma model...
#> ✔ Fitting general-gamma model... [224ms]
#> 
#> Object of class 'pvEBayes'
#> 
#> General-gamma model with hyperparameter alpha = 0.3.
#> Estimated prior is a mixture of 18 gamma distributions.
#> 
#> Running time of the general-gamma model fitting: 0.2411 seconds.
#> Optimizer convergence: successful.
#> No posterior draws were generated.
#> 
#> Extract estimated prior parameters, discovered signals
#> and signal strength posterior draws using `summary()`.

BIC_score <- BIC(fit)
```
