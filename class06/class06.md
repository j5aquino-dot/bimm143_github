# Class06: R Functions
Jervic Aquino (PID:A17756721)
2026-01-23

- [Background](#background)
- [A first function](#a-first-function)
- [A second function](#a-second-function)
- [A new cool function](#a-new-cool-function)

## Background

Function are at the heart of using R. Everything we do involves calling
using functions (from data input, analysis to results output).

All functions in R have at least three things:

1.  A **name**: the thing we use to call the function
2.  One or more input **arguments** that are comma separated
3.  The **body**: lines of code between curly brackets { } that does the
    work of the function

## A first function

Let’s write a function that adds some numbers:

``` r
add <- function(x) {
  x + 1
}
```

Let’s try it out:

``` r
add(100)
```

    [1] 101

Will this work?

``` r
add(c(100, 200, 300))
```

    [1] 101 201 301

Modify to be more useful and add more than just 1

``` r
add <- function(x, y=1) {
  x + y
}
```

``` r
add(100, 10)
```

    [1] 110

Will this still work?

``` r
add(100)
```

    [1] 101

No, because there is no y-component. We have to set y equal to value if
adding only one argument or component in the created function.

How to argue:

``` r
plot(1:10, col="blue", typ="b")
```

![](class06_files/figure-commonmark/unnamed-chunk-7-1.png)

``` r
log(10, base=10)
```

    [1] 1

> **N.B.** Input arguments can be either **required** or **optional**.
> The latter have a fall-back default that is specified in the function
> code with an equals sign.

``` r
#add(100, 200, 300)
```

## A second function

All functions in R look like this

    name <- function(arg) {
      body
    }

The `sample()` function in R generates random numbers from the range of
numbers given. It randomly picks items from the vector inputted.

``` r
sample(1:10, size=4)
```

    [1]  5 10  3  8

> Q. Return 12 numbers picked randomly from the input 1:10

``` r
sample(1:10, size=12, replace=TRUE)
```

     [1] 10 10  9  3  5  2  4  6  2  3  4  9

> Q. Write the code to generate a random 12 nucleotide long DNA sequence

``` r
sample(c("a", "c", "g", "t"), size=12, replace=TRUE)
```

     [1] "c" "c" "t" "c" "t" "a" "a" "t" "t" "t" "t" "c"

Another way to write the code:

``` r
bases <- c("A", "T", "G", "C")
sample(bases, size=12, replace=TRUE)
```

     [1] "G" "A" "C" "T" "A" "G" "C" "T" "G" "C" "C" "T"

> Q. Write a first version function called `generate_dna()` that
> generates a user specified length `n`, random DNA sequence

``` r
n <- sample(c(4:30), size=1)
generate_dna <- sample(bases, size = n, replace = TRUE)
generate_dna
```

     [1] "A" "A" "A" "C" "G" "A" "C" "T" "A" "T" "C" "C" "A" "C" "G"

``` r
generate_dna <- function(n=6) {
  bases <- c("A", "T", "G", "C") 
  sample(bases, size=n, replace=TRUE)
}
```

``` r
generate_dna(100)
```

      [1] "T" "C" "T" "T" "T" "T" "G" "G" "T" "A" "A" "T" "C" "A" "T" "A" "G" "A"
     [19] "C" "A" "T" "T" "T" "C" "T" "G" "A" "A" "G" "A" "C" "A" "G" "G" "T" "A"
     [37] "G" "G" "G" "C" "A" "T" "G" "T" "T" "T" "A" "C" "A" "C" "A" "C" "T" "G"
     [55] "A" "T" "G" "C" "A" "T" "A" "G" "A" "C" "G" "C" "C" "A" "T" "G" "A" "C"
     [73] "T" "T" "C" "A" "T" "A" "T" "C" "G" "C" "C" "G" "A" "C" "A" "A" "T" "T"
     [91] "C" "C" "G" "C" "A" "C" "G" "C" "T" "C"

> Q. Modify your function to return a FASTA-like sequence so rather than
> \[10\] “G” “C” “A” “A” “T” we want “GCAAT”

``` r
generate_dna <- function(n=6) {
  bases <- c("A", "T", "G", "C") 
  sequence <- sample(bases, size=n, replace=TRUE)
  sequence <- paste(sequence, collapse="")
  return(sequence)
}
```

``` r
generate_dna(10)
```

    [1] "ACAAATGTGC"

> Q. Give the user an option to return FASTA format output sequence or
> standard multi-element vector format

``` r
generate_dna <- function(n=6, fasta=TRUE) {
  bases <- c("A", "T", "G", "C") 
  sequence <- sample(bases, size=n, replace=TRUE)
  
  if(fasta) {
  sequence <- paste(sequence, collapse="")
  cat("Hello...")
  } else {
    cat("is it me you're looking for...")
  }
  
  return(sequence)
}  
```

``` r
generate_dna(10)
```

    Hello...

    [1] "AAATCTGTCA"

``` r
generate_dna(10, fasta = FALSE)
```

    is it me you're looking for...

     [1] "G" "C" "C" "G" "G" "C" "A" "T" "G" "A"

## A new cool function

> Q. Write a function called `generate_protein()` that generates a user
> specific length protein sequence in FASTA format

``` r
generate_protein <- function(n) {
  aa <- sample(c("A","R","N","D","C","Q","E","G","H",
        "I","L","K","M","F","P","S","T","W","Y","V"), size=n, replace=TRUE)
  protein <- paste(aa, collapse="")
  return(protein)
}
```

``` r
generate_protein(10)
```

    [1] "YPWSQVPEIG"

> Q. Use your new `generate_protein()` function to generate sequences
> between length 6 and 12 amino acids in length and check if any of
> these are unique in nature (i.e. found in the NR database at NCBI)

``` r
generate_protein <- function(n) {
  aa <- sample(c("A","R","N","D","C","Q","E","G","H",
        "I","L","K","M","F","P","S","T","W","Y","V"), size=n, replace=TRUE)
  protein <- paste(aa, collapse="")
  return(protein)
}
```

``` r
generate_protein(6)
```

    [1] "RPFCMN"

``` r
generate_protein(7)
```

    [1] "GPIYWCY"

``` r
generate_protein(8)
```

    [1] "EGGIRWFL"

``` r
generate_protein(9)
```

    [1] "AIVSHRKSI"

``` r
generate_protein(10)
```

    [1] "KVPGMAFVSG"

``` r
generate_protein(11)
```

    [1] "TVCIYDGDWQG"

``` r
generate_protein(12)
```

    [1] "FYCALHSHCTKP"

Or we could do a `for()` loop:

``` r
for(i in 6:12) {
  cat(">", i, sep="", "\n" )
  cat(generate_protein(i), "\n")
}
```

    >6
    RASTWG 
    >7
    TSSMVRM 
    >8
    KIFINRKF 
    >9
    IKHWIFVQA 
    >10
    GVKFPCGIIT 
    >11
    GWQDYNYTGSK 
    >12
    CTNKHCDRFIPP 
