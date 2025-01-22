# The_evolution_of_youR_code

This is an addition to my presentation "The evolution of youR code: From 
copy-paste to functions to a package" in our R-club (January 2025).

## Prerequisites

- devtools
- roxygen2
- testthat

## Example for the course

**Task:** Filter a vector of quality scores

Quality Score in Sequencing: 

    Sequencing quality scores measure the probability that a base is called
    incorrectly.

```{R}
# Filter low-quality reads
filter_reads <- function(quality_scores, threshold = 20) {
  quality_scores[quality_scores >= threshold]
}
```

## Steps to your own R-package

1. Use `devtools` to create the package structure.

```
library(devtools)
create_package("Rclubbing")
```

The 'create_package()' call creates the needed directory structure, whereas the 
parent directory is named like you desired package name (*i.e.* Rclubbing). Within 
the directory you find a directory named R where you can put in your functions. 

2. Put your filter function into an .R-file in the `R/` directory (*i.e.* 
filter.R)

3. Add the roxygen2 comments above each function.

You need to document your function with the roxygen2 style. Each row that begins
with #' is used by roxygen2 to write your documentation. The keyword export is
important, as this indicates that the function can be used when the package is
installed. ChatGPT can be a really good assistant here to provide you quite 
good roxygen2 templates for your individual functions. **But**  be careful and 
re-read and modify the template.

```
#' Filter Reads by Quality
#'
#' Filters out sequencing reads with quality scores below a given threshold.
#'
#' @param quality_scores A numeric vector of quality scores.
#' @param threshold Minimum quality score to keep (default: 20).
#' @return A numeric vector of quality scores above the threshold.
#' @export
filter_reads <- function(quality_scores, threshold = 20) {
  quality_scores[quality_scores >= threshold & !is.na(quality_scores)]
}
```

 4. Create the documentation using devtools

```
library(devtools)
document()
```

This function calls roxygen2 and creates the documentation of your package.

5. Build the package and load it for testing:

```
build()
load_all()
```

Thiese calls build your package and load all the functions with the export 
keyword. Know you can run and test your functions in your current environment.
The package is not installed and hence not globally available.

6. Install the package

Navigate to your package directory and run the following code:

```
library(devtools)
install()
```

Now your package is installed and can be globally accessed.

7. Setup a test frame framework

```
library(devtools) use_testthat()
```

