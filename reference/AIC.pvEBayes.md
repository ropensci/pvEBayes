# Obtain Akaike Information Criterion (AIC) for a pvEBayes object

This function defines the S3 `AIC` method for objects of class
`pvEBayes`. It extracts the Akaike Information Criterion (AIC) from a
fitted model.

## Usage

``` r
# S3 method for class 'pvEBayes'
AIC(object, ..., k = 2)
```

## Arguments

- object:

  a `pvEBayes` object, which is the output of the function
  [pvEBayes](https://yihaotancn.github.io/pvEBayes/reference/pvEBayes.md)
  or
  [pvEBayes_tune](https://yihaotancn.github.io/pvEBayes/reference/pvEBayes_tune.md).

- ...:

  other input parameters. Currently unused.

- k:

  numeric, the penalty per parameter to be used; the default k = 2 is
  the classical AIC.

## Value

numeric, AIC score for the resulting model.

## Examples

``` r

fit <- pvEBayes(
  contin_table = statin2025_44, model = "general-gamma",
  alpha = 0.3, n_posterior_draws = NULL
)
#> ℹ Fitting general-gamma model...
#> ✔ Fitting general-gamma model... [221ms]
#> 
#> Object of class 'pvEBayes'
#> 
#> General-gamma model with hyperparameter alpha = 0.3.
#> Estimated prior is a mixture of 18 gamma distributions.
#> 
#> Running time of the general-gamma model fitting: 0.2295 seconds.
#> Optimizer convergence: successful.
#> No posterior draws were generated.
#> 
#> Extract estimated prior parameters, discovered signals
#> and signal strength posterior draws using `summary()`.

AIC_score <- AIC(fit)
```
