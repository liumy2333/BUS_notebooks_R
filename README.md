# BUSpaRse notebooks

This repository has example notebooks that demonstrate how to go from fastq files to sparse matrices for scRNA-seq data from start to end. To run the notebooks, please install [kallisto](https://pachterlab.github.io/kallisto/starting), [bustools](https://github.com/BUStools/bustools), and the [BUSpaRse](https://github.com/BUStools/BUSpaRse) R package. 

## Installation of BUSpaRse
You can install BUSpaRse with:

``` r
if (!require(devtools)) install.packages("devtools")
devtools::install_github("BUStools/BUSpaRse")
```

This is work in progress. The package will be available on Bioconductor shortly.

### Installation note for MacOS
In case you encounter this error during installation:

```
clang: error: unsupported option '-fopenmp'
```

This is what to do to resolve it:

This package contains compiled code, and a compiler that supports OpenMP is required to compile this package. However, the default clang that comes with MacOS does not support OpenMP. MacOS users using R 3.5 should download and install Clang 6.0 and gfortran 6.1 compilers from [this webpage from CRAN](https://cran.r-project.org/bin/macosx/tools/), which has OpenMP enabled. R 3.5 no longer works with Clang 4, which was used for R 3.4.

Then, if the file `~/.R/Makevars` does not exist, in the terminal, go to your home directory by `cd`, use `mkdir .R` to create the `.R` directory, and type `vim Makevars` to create and start editing the file. If it already exists, then type `vim Makevars` to edit it.

Alternatively, if you are uncomfortable with the command line, this can be done in RStudio. First use `file.exists("~/.R/Makevars")` to check if `~/.R/Makevars` exists. Then use `dir.exists("~/.R")` to check that if the `~/.R` directory exists. If it does not, then use `dir.create("~/.R")` to create the directory. Then use `file.create("~/.R/Makevars")` to create that file. Then navigate to that file in the Files pane in RStudio, open that file in RStudio, and edit it.

Add the following to the `~/.R/Makevars` file:

```
CC=/usr/local/clang6/bin/clang
SHLIB_CXXLD=/usr/local/clang6/bin/clang++
CXX= /usr/local/clang6/bin/clang++  -Wall
CXX1X= /usr/local/clang6/bin/clang++
CXX98= /usr/local/clang6/bin/clang++
CXX11= /usr/local/clang6/bin/clang++
CXX14= /usr/local/clang6/bin/clang++
CXX17= /usr/local/clang6/bin/clang++
LDFLAGS=-L/usr/local/clang6/lib

```

Above is the default path where this Clang 6.0 is installed. Please change it if Clang 6.0 is installed in a custom path. This will tell R to use the Clang 6.0 from CRAN that has OpenMP enabled. Then restart the R session and reinstall this package.

## Notebooks

1. [10x v2 chemistry - 1k 1:1 Mixture of Fresh Frozen Human (HEK293T) and Mouse (NIH3T3) Cells](https://bustools.github.io/BUS_notebooks_R/10xv2.html)
2. [10x v3 chemistry - 1k 1:1 Mixture of Fresh Frozen Human (HEK293T) and Mouse (NIH3T3) Cells](https://bustools.github.io/BUS_notebooks_R/10xv3.html)

Notebooks for Drop-seq and CEL-seq2 are coming soom.
