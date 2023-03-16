
<!-- README.md is generated from README.Rmd. Please edit that file -->

# ChatGPT coding assistant for RStudio

<center>
<img width="300" height="400" src="man/figures/chatgpt_meme.jpeg">
<p>
Meme by Programming Jokes I IT Humor & Memes
</p>
</center>

## Installation

You can install the development version of {chatgpt} from
[GitHub](https://github.com/jcrodriguez1989/chatgpt) with:

``` r
# install.packages("remotes")
remotes::install_github("jcrodriguez1989/chatgpt")
```

## Requirements

You need to setup your ChatGPT API key in R.

First you will need to obtain your ChatGPT API key. You can create an
API key by accessing [OpenAI API
page](https://beta.openai.com/account/api-keys) -don’t miss their
article about [Best Practices for API Key
Safety](https://help.openai.com/en/articles/5112595-best-practices-for-api-key-safety)-.

Then you have to assign your API key for usage in R, this can be done
just for the actual session, by doing:

``` r
Sys.setenv(OPENAI_API_KEY = "XX-XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX")
```

Or you can do it persistent (session-wide), by assigning it in your
`.Renviron` file. For it, execute `usethis::edit_r_environ()`, and in
that file write a line at the end your API key as

``` r
OPENAI_API_KEY=XX-XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
```

## Features

The {chatgpt} R package provides a set of features to assist in R
coding. Current existing addins:

- **Ask ChatGPT:** Opens an interactive chat session with ChatGPT
- **Comment selected code:** Comment the selected code
- **Create unit tests:** Create testthat unit tests for the selected
  code
- **Create variable name:** Create a name for a variable that would be
  assigned the result of this code
- **Document code (in roxygen2 format):** Document a function
  definition, in roxygen2 format
- **Explain selected code:** Explain the selected code
- **Find issues in the selected code:** Find issues in the selected code
- **Optimize selected code:** Optimize the selected code
- **Refactor selected code:** Refactor the selected code

**Note:** When no code is selected, it will use the whole file’s code.

## Code Examples

#### `ask_chatgpt`

``` r
> cat(ask_chatgpt("What do you think about R language?"))

*** ChatGPT input:

What do you think about R language?
As an AI language model, I don't have opinions or preferences. However, I can say that R is an incredibly powerful tool for statistical computing and graphics. It is widely used in data analysis, data visualization, and research fields. It has a large and active community, which means that you can easily find help or additional functionalities for your project. Additionally, R's open-source nature allows you to use it for free, and it runs on all major operating systems.
```

#### `comment_code`

``` r
> cat(comment_code("for (i in 1:10) {\n  print(i ** 2)\n}"))

*** ChatGPT input:

Add inline comments to the following R code: "for (i in 1:10) {
  print(i ** 2)
}"
# This is a for loop that will iterate over values 1 to 10.
for (i in 1:10) { 
  # Print the square of each value of i.
  print(i ** 2) 
}
```

#### `create_unit_tests`

``` r
> cat(create_unit_tests("squared_numbers <- function(numbers) {\n  numbers ^ 2\n}"))

*** ChatGPT input:

Create a full testthat file, with test cases for the following R code: "squared_numbers <- function(numbers) {
  numbers ^ 2
}"
Sure! Here is a full testthat file with test cases for the given R code:
```

library(testthat)

squared_numbers \<- function(numbers) { numbers ^ 2 }

test_that(“squared_numbers function works correctly”, {

\# Test case 1: checks if input of 0 returns 0
expect_equal(squared_numbers(0), 0)

\# Test case 2: checks if input of negative numbers returns positive
squares expect_equal(squared_numbers(-5), 25)
expect_equal(squared_numbers(-11), 121)

\# Test case 3: checks if input of positive numbers returns correct
squares expect_equal(squared_numbers(3), 9)
expect_equal(squared_numbers(10), 100)

\# Test case 4: checks if input of decimal numbers returns correct
squares expect_equal(squared_numbers(0.5), 0.25)
expect_equal(squared_numbers(2.25), 5.0625)

})


    In this testthat file, we have defined a function called `squared_numbers` which takes in a vector of numbers and returns their squares. We then have four test cases which

#### `create_variable_name`

``` r
> cat(create_variable_name("sapply(1:10, function(i) i ** 2)"))

*** ChatGPT input:

Give a good variable name to the result of the following R code: "sapply(1:10, function(i) i ** 2)"
The result of the given R code is a vector that contains the square of numbers from 1 to 10. A good variable name for this vector could be "squares_one_to_ten".
```

#### `document_code`

``` r
> cat(document_code("square_numbers <- function(numbers) numbers ** 2"))

*** ChatGPT input:

Document, in roxygen2 format, this R function: "square_numbers <- function(numbers) numbers ** 2"
```

\#’ Square numbers \#’ \#’ This function takes in a numeric vector and
returns a \#’ new vector with each element squared. \#’ \#’ @param
numbers A numeric vector. \#’ \#’ @return A numeric vector with each
element squared. \#’ \#’ @examples \#’ square_numbers(c(1,2,3)) \#’ \#
Output: 1 4 9 \#’ \#’ square_numbers(c(-1,-2,-3)) \#’ \# Output: 1 4 9
\#’ \#’ square_numbers(4.5) \#’ \# Output: 20.25 \#’ \#’
square_numbers(NULL) \#’ \# Output: NULL \#’ \#’ @export square_numbers
\<- function(numbers) { numbers \*\* 2 }

#### `explain_code`

``` r
> cat(explain_code("for (i in 1:10) {\n  print(i ** 2)\n}"))

*** ChatGPT input:

Explain the following R code: "for (i in 1:10) {
  print(i ** 2)
}"
This R code uses a for loop to print the natural numbers 1 to 10, each squared. 

The `for()` loop iterates through a sequence of values, which in this case is `1:10`. This means that the loop will run 10 times, with the variable `i` taking on values from 1 to 10.

Inside the loop, the code uses the `print()` function to output the value of `i` squared, which is calculated using the exponentiation operator `**`.

Therefore, the output of this code will be the following sequence of numbers: 1, 4, 9, 16, 25, 36, 49, 64, 81, and 100.
```

#### `find_issues_in_code`

``` r
> cat(find_issues_in_code("i <- 0\nwhile (i < 0) {\n  i <- i - 1\n}"))

*** ChatGPT input:

Find issues or bugs in the following R code: "i <- 0
while (i < 0) {
  i <- i - 1
}"
The code creates an infinite loop because the condition in the `while` statement is always false. The value of `i` is initialized to 0, and the condition is to continue the loop when `i` is less than 0. Therefore, the loop will never be executed. 

To fix this, the condition in the `while` statement should be changed to `i > 0` if the intention is to decrement `i` to negative values.
```

#### `optimize_code`

``` r
> cat(optimize_code("i <- 10\nwhile (i > 0) {\n  i <- i - 1\n  print(i)\n}"))

*** ChatGPT input:

Optimize the following R code: "i <- 10
while (i > 0) {
  i <- i - 1
  print(i)
}"
Here is an optimized version of the code:

```{r}
for(i in 9:0) {
  print(i)
}
```

This code uses a `for` loop instead of a `while` loop, which simplifies
the code and avoids the need to manually decrement `i`. We also start
the loop at 9 instead of 10 to avoid the need for an initial decrement.



    #### `refactor_code`

    ``` r
    > cat(refactor_code("i <- 10\nwhile (i > 0) {\n  i <- i - 1\n  print(i)\n}"))

    *** ChatGPT input:

    Refactor the following R code, returning valid R code: "i <- 10
    while (i > 0) {
      i <- i - 1
      print(i)
    }"
    Refactored R code:

i \<- 10 while (i \> 0) { print(i) i \<- i - 1 }


    This code will count down from 10 and print the values of i at each iteration.

## Use Code from Clipboard

You can copy a code snippet to clipboard and use {chatgpt} functions
without supplying the `code` argument.

``` r
clipr::write_clip("summarise_data <- function(data) {
  summary_stats <- summary(data)
  return(summary_stats)
}",
allow_non_interactive = TRUE)

expl <- chatgpt::explain_code()
```

\*\*\* ChatGPT input:

Explain the following R code: “summarise_data \<- function(data) {
summary_stats \<- summary(data) return(summary_stats) }”

``` r

cat(expl)
```

The given code defines an R function named “summarise_data” that accepts
a single argument “data”. Inside the function, the “summary()” function
is called on the “data” argument to generate a statistical summary of
the data. The computed summary statistics are stored in a variable named
“summary_stats”. Finally, the function returns the summary statistics by
returning the “summary_stats” variable.

Therefore, this function can be used to summarize any given data by
calling the function with the data as an argument.

## Additional Parameters

### Disable Console Messages

If you want {chatgpt} not to show messages in console, please set the
environment variable `OPENAI_VERBOSE=FALSE`.

### Addin Changes in Place

If you want {chatgpt} addins to take place in the editor -i.e., replace
the selected code with the result of the addin execution- then you sould
set the environment variable `OPENAI_ADDIN_REPLACE=TRUE`.

### Change the language of ChatGPT responses

To change the language that ChatGPT responds in, the
`OPENAI_RETURN_LANGUAGE` environment variable must be changed. E.g.,

``` r
Sys.setenv("OPENAI_RETURN_LANGUAGE" = "Español")
cat(chatgpt::explain_code("for (i in 1:10) {\n  print(i ** 2)\n}"))
#> 
#> *** ChatGPT input:
#> 
#> Explain the following R code: "for (i in 1:10) {
#>   print(i ** 2)
#> }"
#> Este código está usando un bucle `for` para iterar a través de un vector de números del 1 al 10 (`1:10`), y en cada iteración, está imprimiendo el cuadrado de cada número (`i ** 2`). La variable `i` es el valor actual de la iteración, que comienza en 1 y finaliza en 10. Por lo tanto, este código imprimirá los cuadrados de los números del 1 al 10.
```

### ChatGPT Model Tweaks

ChatGPT model parameters can be tweaked by using environment variables.

The following environment variables variables can be set to tweak the
behavior, as documented in
<https://beta.openai.com/docs/api-reference/completions/create> .

- `OPENAI_MODEL`; defaults to `"gpt-3.5-turbo"`
- `OPENAI_MAX_TOKENS`; defaults to `256`
- `OPENAI_TEMPERATURE`; defaults to `1`
- `OPENAI_TOP_P`; defaults to `1`
- `OPENAI_FREQUENCY_PENALTY`; defaults to `0`
- `OPENAI_PRESENCE_PENALTY`; defaults to `0`
