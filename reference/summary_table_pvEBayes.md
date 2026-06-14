# Obtain a summary table for a pvEBayes object

Obtain a summary table for a pvEBayes object

## Usage

``` r
summary_table_pvEBayes(x, cutoff_signal = 1.001)
```

## Arguments

- x:

  a `pvEBayes` object, which is the output of the function
  [pvEBayes](https://yihaotancn.github.io/pvEBayes/reference/pvEBayes.md)
  or
  [pvEBayes_tune](https://yihaotancn.github.io/pvEBayes/reference/pvEBayes_tune.md).

- cutoff_signal:

  numeric. Threshold for signal detection. An AE-drug combination is
  classified as a detected signal if its 5th posterior percentile
  exceeds this threshold.

## Value

a data.table that summarizes reporting count (N), expected null value
(E), posterior probability of being a signal (post_prob), posterior
signal strength median (q50), 5-th and 95-th posterior signal strength
percentile (q05 and q95) for each AE-drug combination.

## Examples

``` r

fit <- pvEBayes(
  contin_table = statin2025_44, model = "general-gamma",
  alpha = 0.5, n_posterior_draws = 100
)
#> ℹ Fitting general-gamma model...
#> ✔ Fitting general-gamma model... [302ms]
#> 
#> ℹ Generating 100 posterior draws...
#> ✔ Generating 100 posterior draws... [12ms]
#> 
#> Object of class 'pvEBayes'
#> 
#> General-gamma model with hyperparameter alpha = 0.5.
#> Estimated prior is a mixture of 18 gamma distributions.
#> 
#> Running time of the general-gamma model fitting: 0.3094 seconds.
#> Optimizer convergence: successful.
#> Running time for posterior draws 
#> (100 signal strength posterior draws per AE-drug pair):0.0194 seconds.
#> 
#> Extract estimated prior parameters, discovered signals
#> and signal strength posterior draws using `summary()`.

summary_table_pvEBayes(fit)
#>                       AE         drug     N      E post_prob         q05
#>                   <char>       <char> <int>  <num>     <num>       <num>
#>   1: Acute Kidney Injury Atorvastatin  1132 532.74      1.00  2.09757345
#>   2: Acute Kidney Injury  Fluvastatin    23  50.91      0.00  0.43512416
#>   3: Acute Kidney Injury   Lovastatin    23   4.97      1.00  2.77198273
#>   4: Acute Kidney Injury  Pravastatin   153  74.39      1.00  2.09348794
#>   5: Acute Kidney Injury Rosuvastatin  1141 424.95      1.00  2.72939141
#>  ---                                                                    
#> 311:   Tendon Discomfort   Lovastatin     0   0.01      0.64  0.10845630
#> 312:   Tendon Discomfort  Pravastatin     0   0.08      0.55  0.01690626
#> 313:   Tendon Discomfort Rosuvastatin    10   0.45      1.00 14.25872304
#> 314:   Tendon Discomfort  Simvastatin     0   0.31      0.38  0.01710343
#> 315:   Tendon Discomfort  Other_drugs   205 205.00      0.52  0.98466684
#>             q50       q95
#>           <num>     <num>
#>   1:  2.1181526  2.138051
#>   2:  0.4445578  0.457355
#>   3:  3.8887922  6.281840
#>   4:  2.1168997  2.134092
#>   5:  2.7482400  2.769797
#>  ---                     
#> 311:  1.0123821 23.202877
#> 312:  1.0053909  7.507397
#> 313: 23.2037083 23.207676
#> 314:  0.9950147  3.877769
#> 315:  1.0015560  1.016113
```
