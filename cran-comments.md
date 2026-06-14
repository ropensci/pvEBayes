# pvEBayes 0.3.0

## Resubmission

This is a re-submission to update the changes made during the rOpenSci peer review.

## Changelog

- improved the documentation and vignette.

- included two opioid-related datasets

- expanded and improved the unit tests.

- fixed bugs.

- improved message output.

## Test environment:

- local Windows 10 install, R version 4.5.0 (2025-04-11 ucrt)

- macos-latest (release), windows-latest (release), ubuntu-latest (devel),
ubuntu-latest (release) and ubuntu-latest (oldrel-1) through GitHub actions.

## R CMD check results

There were no ERRORs or WARNINGs in any platforms.



# pvEBayes 0.2.2

## Resubmission

This is a re-submission to update the CVXR interface for compatibility with 
CVXR (>= 1.8.1).

## Changelog

- update the CVXR interface for compatibility with CVXR (>= 1.8.1).

- utilize multiple CVXR-provided optimizers during KM model fitting, ensuring 
numerical stability.

## Test environment:

- local Windows 10 install, R version 4.5.0 (2025-04-11 ucrt)

- macos-latest (release), windows-latest (release), ubuntu-latest (devel),
ubuntu-latest (release) and ubuntu-latest (oldrel-1) through GitHub actions.

## R CMD check results

There were no ERRORs or WARNINGs in any platforms.

## Why pkgcheck is failing in GitHub action?

The new version of CVXR added dependency on clarabel that introduced a 
version 4 Cargo lockfile that strictly requires Rust version 1.78.0 or newer to 
compile. However, the rOpenSci pkgcheck action runs inside a strict r2u Ubuntu 
container that forces the use of the older default system Rust version 1.75.

# pvEBayes 0.1.2

## Resubmission

This is a re-submission correcting issue possibly caused the error reported from
MKL test.

## Changelog

- fixed one bug that was causing eyeplot testing example to fail 

## Test environment:

- local Windows 10 install, R version 4.5.0 (2025-04-11 ucrt)

- local Ubuntu release 24.04, R version 4.2.0 (2022-04-22)

- online win-builder (devel, release, and old release)

- online mac-builder

## R CMD check results

There were no ERRORs or WARNINGs in any platforms, and no NOTES on local Windows,
online mac-builder and online win-builder (release, old-release, devel).

There was a NOTE on Ubuntu 24.04 on the compilation flags:

```
❯ checking compilation flags used ... NOTE
  Compilation used the following non-portable flag(s):
    ‘-march=skylake-avx512’
```
