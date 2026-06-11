# Obtain posterior probability of being a signal

Obtain posterior probability of being a signal

## Usage

``` r
get_posterior_prob(obj, cutoff_signal = 1.001)
```

## Arguments

- obj:

  a `pvEBayes` object, which is the output of the function
  [pvEBayes](https://yihaotancn.github.io/pvEBayes/reference/pvEBayes.md)
  or
  [pvEBayes_tune](https://yihaotancn.github.io/pvEBayes/reference/pvEBayes_tune.md).

- cutoff_signal:

  numeric. Threshold for signal detection. An AE-drug combination is
  classified as a detected signal if its 5th posterior percentile
  exceeds this threshold.

## Value

a matrix

## Examples

``` r

fit <- pvEBayes(
  contin_table = statin2025_44, model = "general-gamma",
  alpha = 0.3, n_posterior_draws = 1000
)
#> ℹ Fitting general-gamma model...
#> ✔ Fitting general-gamma model... [128ms]
#> 
#> ℹ Generating 1000 posterior draws...
#> ✔ Generating 1000 posterior draws... [29ms]
#> 
#> Object of class 'pvEBayes'
#> 
#> General-gamma model with hyperparameter alpha = 0.3.
#> Estimated prior is a mixture of 18 gamma distributions.
#> 
#> Running time of the general-gamma model fitting: 0.1337 seconds.
#> Optimizer convergence: successful.
#> Running time for posterior draws 
#> (1000 signal strength posterior draws per AE-drug pair):0.0339 seconds.
#> 
#> Extract estimated prior parameters, discovered signals
#> and signal strength posterior draws using `summary()`.

posterior_probs <- get_posterior_prob(fit,
cutoff_signal = 1.001)
```
