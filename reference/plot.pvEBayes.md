# Plotting method for a pvEBayes object

This function defines the S3 `plot` method for objects of class
`pvEBayes`.

## Usage

``` r
# S3 method for class 'pvEBayes'
plot(x, type = "eyeplot", ...)
```

## Arguments

- x:

  a `pvEBayes` object, which is the output of the function
  [pvEBayes](https://yihaotancn.github.io/pvEBayes/reference/pvEBayes.md)
  or
  [pvEBayes_tune](https://yihaotancn.github.io/pvEBayes/reference/pvEBayes_tune.md).

- type:

  character string determining the type of plot to show. Available
  choices are `"eyeplot"` which calls
  [eyeplot_pvEBayes](https://yihaotancn.github.io/pvEBayes/reference/eyeplot_pvEBayes.md)
  and `"heatmap"` which calls
  [heatmap_pvEBayes](https://yihaotancn.github.io/pvEBayes/reference/heatmap_pvEBayes.md).

- ...:

  additional arguments passed to heatmap_pvEBayes or eyeplot_pvEBayes.

## Value

A [ggplot](https://ggplot2.tidyverse.org/reference/ggplot.html) object.

## Examples

``` r

obj <- pvEBayes(statin2025_44, model = "general-gamma", alpha = 0.5)
#> ℹ Fitting general-gamma model...
#> ✔ Fitting general-gamma model... [300ms]
#> 
#> ℹ Generating 1000 posterior draws...
#> ✔ Generating 1000 posterior draws... [36ms]
#> 
#> Object of class 'pvEBayes'
#> 
#> General-gamma model with hyperparameter alpha = 0.5.
#> Estimated prior is a mixture of 18 gamma distributions.
#> 
#> Running time of the general-gamma model fitting: 0.3075 seconds.
#> Optimizer convergence: successful.
#> Running time for posterior draws 
#> (1000 signal strength posterior draws per AE-drug pair):0.0434 seconds.
#> 
#> Extract estimated prior parameters, discovered signals
#> and signal strength posterior draws using `summary()`.
plot(obj, type = "eyeplot")

```
