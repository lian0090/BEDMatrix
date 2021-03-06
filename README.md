BEDMatrix
=========

[![Travis-CI Build Status](https://travis-ci.org/QuantGen/BEDMatrix.svg?branch=master)](https://travis-ci.org/QuantGen/BEDMatrix)

The BEDMatrix package provides a wrapper around [binary PED files](http://pngu.mgh.harvard.edu/~purcell/plink/data.shtml#bed) (so-called BED files) that behaves just like a regular R matrix, but retrieves genotypes on demand without loading the entire BED file into memory. The goal is to support huge PED files, and to save time on initially reading in PED files into the R environment.


Installation
------------

The package is not available on CRAN yet. In the meantime, it can be installed using the [devtools](https://github.com/hadley/devtools) package directly from GitHub.

1. Install devtools: `install.packages('devtools')`
2. Load devtools: `library(devtools)`
3. Download BEDMatrix: `install_github('QuantGen/BEDMatrix')`


Usage
-----

1. Load the library: `library(BEDMatrix)`
2. Create a new BEDMatrix object by passing in the path to the binary PED file (`path`): `m <- BEDMatrix('plink.bed')`. The `BEDMatrix` constructor will try to parse a FAM and MAP file of the same name as the BED file to determine the number and names of individuals and the number and names of SNPs. If either one of those files are not present, it is necessary to provide the number of individuals (`n`) and the number of SNPs (`p`) explicitly as parameters of the function: `m <- BEDMatrix(path = 'plink.bed', n = 100, p = 10000)`
3. Extract information from the BEDMatrix as if it were a regular matrix, e.g. `m[, 3]`
4. Report any missing functionality or bugs: https://github.com/QuantGen/BEDMatrix/issues/new :)


Example
-------

This example uses a very simple BED file that is bundled with the R package. It was generated from the PLINK files in the [`inst/extdata` folder](https://github.com/QuantGen/BEDMatrix/tree/master/inst/extdata).
```r
# Get path to example BED file
path <- system.file('extdata', 'example.bed', package = 'BEDMatrix')

# Wrap example BED file in matrix
m <- BEDMatrix(path)

# Print matrix
m[]
```


How to create a BED file from a PED file using PLINK
----------------------------------------------------

```
plink --file myfile --make-bed
```
