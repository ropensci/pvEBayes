# Print method for a pvEBayes object

This function defines the S3 `print` method for objects of class
`pvEBayes`. It displays a concise description of the fitted model.

## Usage

``` r
# S3 method for class 'pvEBayes'
print(x, ...)
```

## Arguments

- x:

  a `pvEBayes` object, which is the output of the function
  [pvEBayes](https://yihaotancn.github.io/pvEBayes/reference/pvEBayes.md)
  or
  [pvEBayes_tune](https://yihaotancn.github.io/pvEBayes/reference/pvEBayes_tune.md).

- ...:

  other input parameters. Currently unused.

## Value

Invisibly returns the input `pvEBayes` object.

## Examples

``` r

obj <- pvEBayes(
  contin_table = statin2025_44, model = "general-gamma",
  alpha = 0.5, n_posterior_draws = 10000
)
#> ℹ Fitting general-gamma model...
#> ✔ Fitting general-gamma model... [325ms]
#> 
#> ℹ Generating 10000 posterior draws...
#> ✔ Generating 10000 posterior draws... [477ms]
#> 
#> Object of class 'pvEBayes'
#> 
#> General-gamma model with hyperparameter alpha = 0.5.
#> Estimated prior is a mixture of 18 gamma distributions.
#> 
#> Running time of the general-gamma model fitting: 0.3325 seconds.
#> Optimizer convergence: successful.
#> Running time for posterior draws 
#> (10000 signal strength posterior draws per AE-drug pair):0.4842 seconds.
#> 
#> Extract estimated prior parameters, discovered signals
#> and signal strength posterior draws using `summary()`.

print(obj)
#> Object of class 'pvEBayes'
#> 
#> General-gamma model with hyperparameter alpha = 0.5.
#> Estimated prior is a mixture of 18 gamma distributions.
#> 
#> Running time of the general-gamma model fitting: 0.3325 seconds.
#> Optimizer convergence: successful.
#> Running time for posterior draws 
#> (10000 signal strength posterior draws per AE-drug pair):0.4842 seconds.
#> 
#> Extract estimated prior parameters, discovered signals
#> and signal strength posterior draws using `summary()`.
```
