---
knit: "bookdown::render_book"
title: "Handling Strings with R"
author: "Gaston Sanchez"
description: "This book aims to provide a panoramic perspective of the wide array of string manipulations that you can perform with R. If you are new to R, or lack experience working with character data, this book will help you get started with the basics of handling strings. Likewise, if you are already familiar with R, you will find material that shows you how to do more advanced string and text processing operations."
date: "2018-04-07"
output: bookdown::gitbook
bibliography: [book.bib]
biblio-style: apalike
link-citations: yes
always_allow_html: yes
url: 'http\://gastonsanchez.com/r4strings/'
github-repo: gastonstat/r4strings
site: bookdown::bookdown_site
documentclass: book
---


# Preface {-}


<img src="images/cover.png" width="300" height="375" alt="Cover image" />


This book aims to provide a panoramic perspective of the wide array of 
string manipulations that you can perform with R. If you are new to R, or 
lack experience working with character data, this book will help you get 
started with the basics of handling strings. Likewise, if you are already
familiar with R, you will find material that shows you how to do more 
advanced string and text processing operations.

Despite the fact that R may not be as rich and diverse as other scripting 
languages when it comes to string manipulation, it can take you very far if 
you know how. Sadly, documentation on how to manipulate strings and text data 
in R is very scarce. This work is my two cents to increase the number of 
available resources about this indispensable topic for any data scientist.


<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.



<!--chapter:end:index.rmd-->


# Introduction {#intro}

At its heart, computing involves working with numbers. That's the main reason 
why computers were invented: to facilitate mathematical operations around
numbers; from basic arithmetic to more complex operations (e.g. trigonometry, 
algebra, calculus, etc.) Nowadays, however, we use computers to work with 
data that are not just numbers. We use them to write a variety of documents, 
we use them to create and edit images and videos, to manipulate sound, among 
many other tasks. Learning to manipulate those data types is fundamental to 
programming.

Today, there is a considerable amount of information and data in the form 
of text. Look at any website: pretty much the contents are text and images, 
with some videos here and there, and maybe some tables and/or a list of numbers. 

Likewise, most of the times you are going to be working with text files: 
script files, reports, data files, source code files, etc. 
All the  R script files that you use are essentially plain text files. 
I bet you have a csv file or any other field delimited format 
(or even in HTML, XML, JSON, etc), with some fields containing characters. 
In all of these cases what you are working with is essentially 
a bunch of characters.

At the end of the day all the data that is passed to the computer is converted 
to binary format (zeros and ones) so computers can process it. But no one can
deny the fact that a lot of what we do with computers is working with text and 
character strings. 

And then inside R you also have text. Things like row
names and column names of matrices, data frames, tables, and any other 
rectangular data structure. Lists and vectors may also contain names. 
And what about the text in graphics? Things like titles, subtitles, 
axis labels, legends, colors, displayed text in a plot, etc.
Text is omnipresent: whether you are we are surrounded by it.


## About this book

This book aims to help you get started with handling strings in R. It provides 
an overview of several resources that you can use for string manipulation. It 
covers useful functions, general topics, common operations, and other tricks.

This book is NOT about textual data analysis, linguistic analysis, text mining, 
or natural language processing (NLP). For those purposes, I highly recommend 
taking a look at the CRAN Task View on Natural Language Processing (NLP):

[http://cran.r-project.org/web/views/NaturalLanguageProcessing.html](http://cran.r-project.org/web/views/NaturalLanguageProcessing.html)

However, even if you don't plan to do text analysis, text mining, or natural 
language processing, I bet you have some dataset that contains data as 
characters: names of rows, names of columns, dates, monetary quantities, 
longitude and latitude, etc. I'm sure that you have encountered one or more of 
the following cases:

- You want to remove a given character in the names of your variables
- You want to replace a given character in your data
- Maybe you wanted to convert labels to upper case (or lower case)
- You've been struggling with xml (or html) files
- You've been modifying text files in excel changing labels, categories, one cell at a time, or doing one thousand copy-paste operations 


Hopefully after reading this book, you will have the necessary tools in your 
toolbox for dealing with these (and many) other situations that involve 
handling and processing strings in R.


### Structure of the book

The content of the book is divided in five major parts:

1. Getting started with character strings
2. Formatting and printing text and numbers
3. Input and output
4. Basic string manipulations
5. Working with Regular Expressions

If you have minimal or none experience with R, the best place to start is 
[Chapter 2: Characters](#chars). If you are already familiar with the basics
of vectors and character objects, you can quickly skim this chapter, or skip it, 
and then go to another chapter of your interest.

Chapter 2 describes different ways to format text and numbers. These are 
useful tools for when you want to produce output that will either be displayed
on screen, or that will be exported to a file.

The third major component of the book has to do with reading in information from
text files, as well as exporting output to text to files.

The fourth part of the book deals with _basic_ string manipulations. By "basic"
I mean any type of manipulation and transformation that does not require
the use of regular expressions.

The fifth part comprises working with regular expressions. Here you will learn
about the basic concepts around regular expressions (regex), the intricacies 
when working with regex in R, and becoming familiar with the regex functions 
in the R package __stringr__.

Last but not least, the last chapters of the book present a couple of case 
studies and extended practical examples that cover the main topics covered
in the book.


### Main Resources

Documentation on how to manipulate strings and text data in R is very scarce. 
This is mostly because R is not perceived as a scripting language (like Python 
or Java, among others). However, I seriously think that we need to have more 
available resources about this indispensable topic. 

There is not much documentation on how to manipulate character strings and text 
data in R. There are great R books for an enormous variety of statistical 
methods, graphics and data visualization, as well as applications in a wide 
range of fields such as ecology, genetics, psychology, finance, economics, etc. 
But not for manipulating strings and text data. 

Perhaps the main reason for this lack of resources is that R is not considered 
to be qualified as a "scripting" language: R is primarily perceived as a 
language for computing and programming with (mostly numeric) data. Quoting 
[Hadley Wickham](http://journal.r-project.org/archive/2010-2/RJournal_2010-2_Wickham.pdf)

> "R provides a solid set of string operations, but because they have grown 
> organically over time, they can be inconsistent and a little hard to learn. 
> Additionally, they lag behind the string operations in other programming 
> languages, so that some things that are easy to do in languages like Ruby or 
> Python are rather hard to do in R"

Most introductory books about R have small sections that briefly cover string 
manipulation without going further down. That is why I don't have many books 
for recommendation, if anything the book by Phil Spector 
__Data Manipulation with R__. 

If published material is not abundant, we still have the online world. The good 
news is that the web is full of hundreds of references about processing 
character strings. The bad news is that they are very spread and uncategorized. 

For specific topics and tasks, a good place to start with is _Stack Overflow_. 
This is a questions-and-answers site for programmers that has a lot of 
questions related with R. Just look for those questions tagged with `"r"`: 
[http://stackoverflow.com/questions/tagged/r](http://stackoverflow.com/questions/tagged/r). 
There is a good number of posts related with handling characters and text, and 
they can give you a hint on how to solve a particular problem. There is also 
_R-bloggers_, [http://www.r-bloggers.com](http://www.r-bloggers.com), a blog 
aggregator for R enthusiasts in which is also possible to find contributed 
material about processing strings as well as text data analysis.

You can also check the following resources that have to do with string 
manipulations. It is a very short list of resources but I've found them very 
useful:

- __R Wikibook: Programming and Text Processing__
[http://en.wikibooks.org/wiki/R_Programming/Text_Processing](http://en.wikibooks.org/wiki/R_Programming/Text_Processing)
 R wikibook has a section dedicated to text processing that is worth check it out.

- __stringr: modern, consisting string processing__ by Hadley Wickham
[http://journal.r-project.org/archive/2010-2/RJournal_2010-2_Wickham.pdf](http://journal.r-project.org/archive/2010-2/RJournal_2010-2_Wickham.pdf)
Article from the R journal introducing the package `"stringr"` by Hadley Wickham.
 
- __Introduction to String Matching and Modification in R Using Regular Expressions__ by Svetlana Eden
[http://biostat.mc.vanderbilt.edu/wiki/pub/Main/SvetlanaEdenRFiles/regExprTalk.pdf](http://biostat.mc.vanderbilt.edu/wiki/pub/Main/SvetlanaEdenRFiles/regExprTalk.pdf)



### Acknowledgements

This book is a major iteration on a previous ebook that I wrote in 2013:
_Handling and Processing Strings in R_. As you can tell, I've shorten the
title to just __Handling Strings with R__. I've also expanded the content to
include many more examples, code snippets, and material about regular 
expressions.

As always, many thanks to Jessica who patiently accepted my occupying of the
dinning table as my workbench (~~that's over now~~).


### Colophon

The source of the book is available in the github repository:

[https://github.com/gastonstat/r4strings](https://github.com/gastonstat/r4strings).

The book is powered by [https://bookdown.org](https://bookdown.org).

This book was built with:


```
#> R version 3.3.3 (2017-03-06)
#> Platform: x86_64-apple-darwin13.4.0 (64-bit)
#> Running under: OS X Yosemite 10.10.5
#> 
#> locale:
#> [1] en_US.UTF-8/en_US.UTF-8/en_US.UTF-8/C/en_US.UTF-8/en_US.UTF-8
#> 
#> attached base packages:
#> [1] stats     graphics  grDevices utils     datasets  base     
#> 
#> loaded via a namespace (and not attached):
#>  [1] backports_1.1.2 magrittr_1.5    bookdown_0.7    rprojroot_1.3-2
#>  [5] htmltools_0.3.6 tools_3.3.3     rstudioapi_0.7  yaml_2.1.16    
#>  [9] Rcpp_0.12.15    stringi_1.1.6   rmarkdown_1.8   knitr_1.18     
#> [13] methods_3.3.3   stringr_1.2.0   digest_0.6.14   xfun_0.1       
#> [17] evaluate_0.10.1
```




<!--chapter:end:introduction.Rmd-->


# (PART) Characters {-}

# Character Strings in R {#chars}

## Introduction

This chapter introduces you to the basic concepts for creating character
vectors and character strings in R. You will also learn how R treats objects 
containing characters.

In R, a piece of text is represented as a sequence of characters (letters, 
numbers, and symbols). The data type R provides for storing sequences of 
characters is _character_. Formally, the __mode__ of an object that holds 
character strings in R is `"character"`.

You express character strings by surrounding text within double quotes:


```r
"a character string using double quotes"
```

or you can also surround text within single quotes:


```r
'a character string using single quotes'
```

The important thing is that you must match the type of quotes that your are 
using. A starting double quote must have an ending double quote. Likewise, a 
string with an opening single quote must be closed with a single quote. 

Typing characters in R like in above examples is not very useful. Typically, 
you are going to create objects or variables containing some strings. For 
example, you can create a variable `string` that stores some string:


```r
string <- 'do more with less'
string
#> [1] "do more with less"
```

Notice that when you print a character object, R displays it using double 
quotes (regardless of whether the string was created using single or double 
quotes). This allows you to quickly identify when an object contains character 
values.

When writing strings, you can insert single quotes in a string with double 
quotes, and vice versa:


```r
# single quotes within double quotes
ex1 <- "The 'R' project for statistical computing"
```


```r
# double quotes within single quotes
ex2 <- 'The "R" project for statistical computing'
```

However, you cannot directly insert single quotes in a string with single 
quotes, neither you can insert double quotes in a string with double quotes 
(Don't do this!):


```r
ex3 <- "This "is" totally unacceptable"
```


```r
ex4 <- 'This 'is' absolutely wrong'
```

In both cases R will give you an error due to the unexpected presence of 
either a double quote within double quotes, or a single quote within single 
quotes.

If you really want to include a double quote as part of the string, you need 
to _escape_ the double quote using a backslash `\` before it:


```r
"The \"R\" project for statistical computing"
```

We will talk more about escaping characters in the following chapters.


## Common use of strings in R

Perhaps the most common use of character strings in R has to do with:

- names of files and directories
- names of elements in data objects
- text elements displayed in plots and graphs
  
When you read a file, for instance a data table stored in a csv file, 
you typically use the `read.table()` function and friends---e.g. `read.csv()`, 
`read.delim()`. Assuming that the file `dataset.csv` is in your working directory:


```r
dat <- read.csv(file = 'dataset.csv')
```

The main parameter for the function `read.csv()` is `file` which requires a 
character string with the pathname of the file.

Another example of a basic use of characters is when you assign names to the 
elements of some data structure in R. For instance, if you want to name the 
elements of a (numeric) vector, you can use the function `names()` as follows:


```r
num_vec <- 1:5
names(num_vec) <- c('uno', 'dos', 'tres', 'cuatro', 'cinco')
num_vec
```

Likewise, many of the parameters in the plotting functions require some sort 
of input string. Below is a hypothetical example of a scatterplot that includes 
several graphical elements like the main title (`main`), subtitle (`sub`), 
labels for both x-axis and y-axis (`xlab`, `ylab`), the name of the color
(`col`), and the symbol for the point character (`pch`).


```r
plot(x, y, 
     main = 'Main Title', 
     sub = 'Subtitle',
     xlab = 'x-axis label', 
     ylab = 'y-axis label',
     col = 'red', 
     pch = 'x')
```


## Creating Character Strings

Besides the single quotes `''` or double quotes `""`, R provides the function 
`character()` to create character vectors. More specifically, `character()` 
is the function that creates vector objects of type `"character"`. 

When using `character()` you just have to specify the length of the vector. 
The output will be a character vector filled of empty strings:


```r
# character vector with 5 empty strings
char_vector <- character(5)
char_vector
#> [1] "" "" "" "" ""
```

When would you use `character()`? A typical usage case is when you want to 
initialize an _empty_ character vector of a given length. The idea is to 
create an object that you will modify later with some computation.

As with any other vector, once an empty character vector has been created, 
you can add new components to it by simply giving it an index value outside 
its previous range: 


```r
# another example
example <- character(0)
example
#> character(0)

# check its length
length(example)
#> [1] 0

# add first element
example[1] <- "first"
example
#> [1] "first"

# check its length again
length(example)
#> [1] 1
```

You can add more elements without the need to follow a consecutive index range:


```r
example[4] <- "fourth"
example
#> [1] "first"  NA       NA       "fourth"
length(example)
#> [1] 4
```

Notice that the vector `example` went from containing one-element to contain 
four-elements without specifying the second and third elements. R fills this 
gap with missing values `NA`.


### Empty string

The most basic type of string is the __empty string__ produced by 
consecutive quotation marks: `""`. Technically, `""` is a string with 
no characters in it, hence the name "empty string":


```r
# empty string
empty_str <- ""
empty_str
#> [1] ""

# class
class(empty_str)
#> [1] "character"
```


### Empty character vector

Another basic string structure is the __empty character vector__ produced 
by the function `character()` and its argument `length=0`:


```r
# empty character vector
empty_chr <- character(0)
empty_chr
#> character(0)

# class
class(empty_chr)
#> [1] "character"
```

It is important not to confuse the empty character vector `character(0)` 
with the empty string `""`; one of the main differences between them is 
that they have different lengths:


```r
# length of empty string
length(empty_str)
#> [1] 1

# length of empty character vector
length(empty_chr)
#> [1] 0
```

Notice that the empty string `empty_str` has length 1, while the empty 
character vector `empty_chr` has length 0.

Also, `character(0)` occurs when you have a character vector with one or 
more elements, and you attempt to subset the position 0:


```r
string <- c('sun', 'sky', 'clouds')
string
#> [1] "sun"    "sky"    "clouds"
```

If you try to retrieve the element in position 0 you get:


```r
string[0]
#> character(0)
```


### Function `c()`

There is also the generic function `c()` (concatenate or combine) that you 
can use to create character vectors. Simply pass any number of character 
elements separated by commas:


```r
string <- c('sun', 'sky', 'clouds')
string
#> [1] "sun"    "sky"    "clouds"
```

Again, notice that you can use single or double quotes to define the character 
elements inside `c()`


```r
planets <- c("mercury", 'venus', "mars")
planets
#> [1] "mercury" "venus"   "mars"
```



### `is.character()` and `as.character()`

Related to `character()` R provides two related functions: 
`as.character()` and `is.character()`. These two functions are methods for 
coercing objects to type `"character"`, and testing whether an 
R object is of type `"character"`. For instance, let's define two 
objects `a` and `b` as follows:


```r
# define two objects 'a' and 'b'
a <- "test me"
b <- 8 + 9
```

To test if `a` and `b` are of type `"character"` use the function
`is.character()`:


```r
# are 'a' and 'b' characters?
is.character(a)
#> [1] TRUE

is.character(b)
#> [1] FALSE
```

Likewise, you can also use the function `class()` to get the class of an 
object:


```r
# classes of 'a' and 'b'
class(a)
#> [1] "character"
class(b)
#> [1] "numeric"
```

The function `as.character()` is a coercing method. For better or worse, 
R allows you to convert (i.e. coerce) non-character objects into character 
strings with the function `as.character()`:


```r
# converting 'b' as character
b <- as.character(b)
b
#> [1] "17"
```


## Behavior of R objects with character strings

The main, and most basic, type of objects in R are vectors. Vectors must have 
their values _all of the same mode_. This means that any given vector 
must be unambiguously either logical, numeric, complex, character or raw. 
In R we say that vectors are __atomic__ structures, with their elements 
having all the same type or mode. 

So what happens when you mix different types of data in a vector?


```r
# vector with numbers and characters
c(1:5, pi, "text")
#> [1] "1"                "2"                "3"               
#> [4] "4"                "5"                "3.14159265358979"
#> [7] "text"
```

As you can tell, the resulting vector from combining integers `1:5`, the 
number `pi`, and some `"text"` is a vector with all its elements 
treated as character strings. In other words, when you combine mixed data in 
vectors, strings will dominate. This means that the mode of the vector will be 
`"character"`, even if you mix logical values:


```r
# vector with numbers, logicals, and characters
c(1:5, TRUE, pi, "text", FALSE)
#> [1] "1"                "2"                "3"               
#> [4] "4"                "5"                "TRUE"            
#> [7] "3.14159265358979" "text"             "FALSE"
```

In fact, R follows two basic rules of data types coercion. The most strict 
rule is: if a character string is present in a vector, everything else in the 
vector will be converted to character strings. The other coercing rule is: if a 
vector only has logicals and numbers, then logicals will be converted to 
numbers; `TRUE` values become 1, and `FALSE` values become 0.

Keeping these rules in mind will save you from many headaches and frustrating 
moments. Moreover, you can use them in your favor to manipulate data in very 
useful ways.


__Matrices.__
The same behavior of vectors happens when you mix characters and numbers in 
matrices. Again, everything will be treated as characters:


```r
# matrix with numbers and characters
rbind(1:5, letters[1:5])
#>      [,1] [,2] [,3] [,4] [,5]
#> [1,] "1"  "2"  "3"  "4"  "5" 
#> [2,] "a"  "b"  "c"  "d"  "e"
```

__Data frames.__
With data frames, things are a bit different. By default, character strings 
inside a data frame will be converted to factors:


```r
# data frame with numbers and characters
df1 = data.frame(numbers=1:5, letters=letters[1:5])
df1
#>   numbers letters
#> 1       1       a
#> 2       2       b
#> 3       3       c
#> 4       4       d
#> 5       5       e
# examine the data frame structure
str(df1)
#> 'data.frame':	5 obs. of  2 variables:
#>  $ numbers: int  1 2 3 4 5
#>  $ letters: Factor w/ 5 levels "a","b","c","d",..: 1 2 3 4 5
```

To turn-off the `data.frame()`'s default behavior of converting strings 
into factors, use the argument `stringsAsFactors = FALSE`:


```r
# data frame with numbers and characters
df2 <- data.frame(
  numbers = 1:5, 
  letters = letters[1:5], 
  stringsAsFactors = FALSE)

df2
#>   numbers letters
#> 1       1       a
#> 2       2       b
#> 3       3       c
#> 4       4       d
#> 5       5       e
# examine the data frame structure
str(df2)
#> 'data.frame':	5 obs. of  2 variables:
#>  $ numbers: int  1 2 3 4 5
#>  $ letters: chr  "a" "b" "c" "d" ...
```

Even though `df1` and `df2` are identically displayed, their structure is 
different. While `df1$letters` is stored as a `"factor"`, `df2$letters` is 
stored as a `"character"`.

__Lists.__
With lists, you can combine any type of data objects. The type of data in 
each element of the list will maintain its corresponding mode:


```r
# list with elements of different mode
list(1:5, letters[1:5], rnorm(5))
#> [[1]]
#> [1] 1 2 3 4 5
#> 
#> [[2]]
#> [1] "a" "b" "c" "d" "e"
#> 
#> [[3]]
#> [1]  0.49293623 -1.21452992 -0.65625779  0.91992999  0.09828659
```




## The workhorse function `paste()`

The function `paste()` is perhaps one of the most important functions that you
can use to create and build strings. `paste()` takes one or more R objects, 
converts them to `"character"`, and then it concatenates (pastes) them to form 
one or several character strings. Its usage has the following form:

```
paste(..., sep = " ", collapse = NULL)
```

The argument `...` means that it takes any number of objects. The argument 
`sep` is a character string that is used as a separator. The argument 
`collapse` is an optional string to indicate if you want all the terms to be 
collapsed into a single string. Here is a simple example with `paste()`:


```r
# paste
PI <- paste("The life of", pi)

PI
#> [1] "The life of 3.14159265358979"
```

As you can see, the default separator is a blank space (`sep = " "`). But you 
can select another character, for example `sep = "-"`:


```r
# paste
IloveR <- paste("I", "love", "R", sep = "-")

IloveR
#> [1] "I-love-R"
```

If you give `paste()` objects of different length, then it will apply a 
recycling rule. For example, if you paste a single character `"X"` with the
sequence `1:5`, and separator `sep = "."`, this is what you get:


```r
# paste with objects of different lengths
paste("X", 1:5, sep = ".")
#> [1] "X.1" "X.2" "X.3" "X.4" "X.5"
```

To see the effect of the `collapse` argument, let's compare the difference with
collapsing and without it:


```r
# paste with collapsing
paste(1:3, c("!","?","+"), sep = '', collapse = "")
#> [1] "1!2?3+"

# paste without collapsing
paste(1:3, c("!","?","+"), sep = '')
#> [1] "1!" "2?" "3+"
```

One of the potential problems with `paste()` is that it coerces missing values `NA` into the character `"NA"`:


```r
# with missing values NA
evalue <- paste("the value of 'e' is", exp(1), NA)

evalue
#> [1] "the value of 'e' is 2.71828182845905 NA"
```

In addition to `paste()`, there's also the function `paste0()` which is the equivalent of

```
paste(..., sep = "", collapse)
```


```r
# collapsing with paste0
paste0("let's", "collapse", "all", "these", "words")
#> [1] "let'scollapseallthesewords"
```


## Exercises

1. What is the difference between the empty character `""` and the output 
of invoking `character()`?

2. When you combine logical values, numeric values, and character
values in one single vector, what will be the mode of the resulting vector?

3. Using `rep()`, how would you obtain the following character vectors:


```
#> [1] "a" "b" "a" "b" "a" "b" "a" "b"
#> [1] "a" "a" "a" "a" "b" "b" "b" "b"
#> [1] "a" "a" "b" "b" "a" "a" "b" "b"
```

4. Given the following vectors `go`, `bears`, and `bang`:


```r
go <- 'Go'
bears <- 'Bears'
bang <- '!'
```

how would you use `paste()` and `paste0()` to get the following strings:

```
"Go Bears !"
"GoBears!"
"Go Bears!"
"Go-Bears!"
"Go Bears!!!"
"Go Bears! Go Bears! Go Bears!"
```

<!--chapter:end:characters.Rmd-->


# (PART) Formatting {-}

# Formatting Text and Numbers {#formatting}

## Introduction

A common task when working with character strings involves printing and 
displaying them on the screen or on a file. In this chapter you will learn 
about the different functions and options in R to print strings in a 
wide variety of common---and not so common---formats. 


## Printing and formatting

R provides a series of functions for printing strings. Some of the printing 
functions are useful when creating `print` methods for programmed 
objects' classes. Other functions are useful for printing output either in the 
R console or to a given file. In this chapter we will describe the following 
print-related functions:

| Function     | Description          |
|:-------------|:---------------------|
| `print()`    | generic printing     |
| `noquote()`  | print with no quotes |
| `cat()`      | concatenation        |
| `format()`   | special formats      |
| `toString()` | convert to string    |
| `sprintf()`  | C-style printing     |



## Generic printing

The _workhorse_ printing function in R is `print()`. As its 
names indicates, this function prints its argument on the R console:


```r
# text string
my_string <- "programming with data is fun"

print(my_string)
#> [1] "programming with data is fun"
```

To be more precise, `print()` is a generic function, which means that you
should use this function when creating printing methods for programmed classes.

As you can see from the previous example, `print()` displays text in 
quoted form by default. If you want to print character strings with no quotes 
you can set the argument `quote = FALSE` 


```r
# print without quotes
print(my_string, quote = FALSE)
#> [1] programming with data is fun
```


### When to use `print()`?

When you type the name of an obbject in the R console, R calls the corresponding
`print` method associated to the class of the object. If the object is a 
`"data.frame"`, then R will dispatch the method `print.data.frame` and display 
the output on screen accordingly.

Most of the times you don't really need to invoke `print()`. Usually, simply 
typing the name of the object will suffice. So when do you actually call 
`print()`? You use `print()` when your code is inside an __R expression__ 
(i.e. code inside curly braces `{ }`) and you want to see the results of one
or more computational steps. Typical examples that require an explicit call to
`print()` is when you are interested in looking at some value within a loop, 
or a conditional structure.

Consider the following dummy `for` loop. It iterates five times, each 
time adding 1 to the value of the iterator `i`:


```r
for (i in 1:5) {
  i + 1
}
```

The above code works and R executes the additions, but nothing is displayed on 
the console. This is because the command `i + 1` forms part of an R expression,
that is, it is within the braces `{ }`.
To be able to see the actual computations you should call `print()` like so:


```r
for (i in 1:5) {
  print(i + 1)
}
#> [1] 2
#> [1] 3
#> [1] 4
#> [1] 5
#> [1] 6
```


## Concatenate and print with `cat()`

Another very useful function is `cat()` which allows you to concatenate objects 
and print them either on screen or to a file. Its usage has the following 
structure:

```
cat(..., file = "", sep = " ", fill = FALSE, labels = NULL, append = FALSE)
```

The argument `...` implies that `cat()` accepts several types of R objects 
(typically vectors). However, when we pass numeric and/or complex vectors, 
they are automatically converted to character strings by `cat()`. By default, 
the strings are concatenated with a space character as separator. This can be 
modified with the `sep` argument.

If you use `cat()` with only one single string, you get a similar 
(although not identical) result as `noquote()`:


```r
# simply print with 'cat()'
cat(my_string)
#> programming with data is fun
```

As you can see, `cat()` prints its arguments without quotes. In essence, `cat()` 
simply displays its content (on screen or in a file). Compared to `noquote()`, 
`cat()` does not print the numeric line indicator (`[1]` in this case). 

The usefulness of `cat()` is when we have two or more strings that we want 
to concatenate:


```r
# concatenate and print
cat(my_string, "with R")
#> programming with data is fun with R
```

You can use the argument `sep` to indicate a chacracter vector that will be 
included to separate the concatenated elements:


```r
# especifying 'sep'
cat(my_string, "with R", sep=" =) ")
#> programming with data is fun =) with R

# another example
cat(1:10, sep = "-")
#> 1-2-3-4-5-6-7-8-9-10
```

When we pass vectors to `cat()`, each of the elements are treated as though 
they were separate arguments:


```r
# first four months
cat(month.name[1:4], sep = " ")
#> January February March April

# first four months
cat(month.name[1:4], sep = "-")
#> January-February-March-April

# first four months
cat(month.name[1:4], sep = "")
#> JanuaryFebruaryMarchApril
```

The argument `fill` allows us to break long strings; this is achieved when we 
specify the string width with an integer number:


```r
# fill = 30
cat("Loooooooooong strings", "can be displayed", "in a nice format", 
    "by using the 'fill' argument", fill = 30)
#> Loooooooooong strings 
#> can be displayed 
#> in a nice format 
#> by using the 'fill' argument
```

Last but not least, we can specify a file output in `cat()`. For instance, 
let's suppose that we want to save the output in the file `output.txt` 
located in our working directory. This is done by specifying the `file`
argument:


```r
# cat with output in a given file
cat(my_string, "with R", file = "output.txt")
```




## Encoding strings with `format()`

The function `format()` allows you to format an R object for _pretty_ printing. 
Essentially, `format()` treats the elements of a vector as character strings 
using a common format. This is especially useful when printing numbers and 
quantities under different formats.


```r
# default usage
format(13.7)
#> [1] "13.7"

# another example
format(13.12345678)
#> [1] "13.12346"
```


Some useful arguments used in `format()`:

- `width` the (minimum) width of strings produced
- `trim` if set to `TRUE` there is no padding with spaces
- `justify` controls how padding takes place for strings. 
Takes the values `"left", "right", "centre", "none"`


For controling the printing of numbers, use these arguments:

- `digits` The number of digits to the right of the decimal place.
- `scientific` use `TRUE` for scientific notation, `FALSE` for standard notation



```r
# use of 'nsmall'
format(13.7, nsmall = 3)
#> [1] "13.700"

# use of 'digits'
format(c(6.0, 13.1), digits = 2)
#> [1] " 6" "13"

# use of 'digits' and 'nsmall'
format(c(6.0, 13.1), digits = 2, nsmall = 1)
#> [1] " 6.0" "13.1"
```

By default, `format()` pads the strings with spaces so that they all have 
the same length.


```r
# justify options
format(c("A", "BB", "CCC"), width = 5, justify = "centre")
#> [1] "  A  " " BB  " " CCC "

format(c("A", "BB", "CCC"), width = 5, justify = "left")
#> [1] "A    " "BB   " "CCC  "

format(c("A", "BB", "CCC"), width = 5, justify = "right")
#> [1] "    A" "   BB" "  CCC"

format(c("A", "BB", "CCC"), width = 5, justify = "none")
#> [1] "A"   "BB"  "CCC"

# digits
format(1/1:5, digits = 2)
#> [1] "1.00" "0.50" "0.33" "0.25" "0.20"

# use of 'digits', widths and justify
format(format(1/1:5, digits = 2), width = 6, justify = "c")
#> [1] " 1.00 " " 0.50 " " 0.33 " " 0.25 " " 0.20 "
```

For printing large quantities with a sequenced format we can use the arguments 
`big.mark` or `big.interval`. For instance, here is how we can print a number 
with sequences separated by a comma `","`


```r
# big.mark
format(123456789, big.mark = ",")
#> [1] "123,456,789"
```


## Exercises

1. Why do we say that `print()` is not really one function but a _family_ of functions?

2. Mention three differences between `print()` and `cat()`.

3. What happens when you pass a matrix to `cat()`? For instance:


```r
m <- matrix(1:12, nrow = 3, ncol = 4)
cat(m)
```

4. What happens when you pass a data frame object to `cat()`? For instance:


```r
dfr <- data.frame(a = 1, b = 2, c = 3)
cat(dfr)
```

<!--chapter:end:printing.Rmd-->


# C-style Formatting

R comes with the `sprintf()` function that provides string formatting
like in the __C__ language. To be more precise, this function is a wrapper
for the C library function of the same name. In many other programming
languages, this type of printing is known as _printf_ which stands for 
__print formatting__. Simply put, 
`sprintf()` allows you to create strings as output using formatted data.

The function `sprintf()` requires using a special syntax that may look
awkward the first time you use it. Here is one example:


```r
sprintf("I woke up at %s:%s%s a.m.", 8, 0, 5)
#> [1] "I woke up at 8:05 a.m."
```

How does `sprintf()` work? The first argument of this function is a character
vector of one element that contains the text to be formatted. Observe that 
inside the text there are various percent symbols `%` followed by the letter 
`s`. Each `%` is referred to as a __slot__, which is basically a placeholder 
for a variable that will be formatted. The rest of the inputs passed to
`sprintf()` are the values that will be used in each of the slots.

The string in the previous example contains three slots of the same type, `%s`,
and the subsequent arguments are numbers `8`, `0`, and `5`. Each number is used 
as a value for each slot. The letter `s` indicates that the formatted variable
is specified as a _string_.

Most of the times you won't use `sprintf()` like in the example above. 
Instead, what you will pass are variables containing different values:


```r
hour <- 8
mins1 <- 0
mins2 <- 5
sprintf("I woke up at %s:%s%s a.m.", hour, mins1, mins2)
#> [1] "I woke up at 8:05 a.m."
```


## C-style formatting options

The string format `%s` is just one of a larger list of available formatting
options. The following table shows the most common formatting specifications:

| Notation | Description                                       |
|:---------|:--------------------------------------------------|
| `%s`     | a string                                          |
| `%d`     | an integer                                        |
| `%0xd`   | an integer padded with `x` leading zeros          |
| `%f`     | decimal notation with six decimals                |
| `%.xf`   | floating point number with `x` digits after decimal point | 
| `%e`     | compact scientific notation, `e` in the exponent  |
| `%E`     | compact scientific notation, `E` in the exponent  |
| `%g`     | compact decimal or scientific notation (with `e`) |



### Format Slot Syntax

The full syntax for a format slot is defined by:

```
%[parameter][flags][width][.precision][length]type
```

The percent symbol, `%`, as we said, indicates a placeholder or slot.


The `parameter` field is an optional field that can take the value `n$` in which 
`n` is the number of the variable to display, allowing the variables provided 
to be used multiple times, using varying format specifiers or in different 
orders.


```r
sprintf("The second number is %2$d, the first number is %1$d", 2, 1)
#> [1] "The second number is 1, the first number is 2"
```


The `flags` field can be zero or more (in any order) of:

- `-` (minus) Left-align the output of this placeholder.
- `+` (plus) Prepends a plus for positive signed-numeric types.
- `' '` (space) Prepends a space for positive signed-numeric types.
- `0` (zero) When the 'width' option is specified, prepends zeros for numeric types.
- `#` (hash) Alternate form:
    + for `g` and `G` types, trailing zeros are not removed.
    + for `f, F, e, E, g, G` types, the output always contain a decimal point.
    + for `o, x, X` types, the text `0`, `0x`, `0X`, respectively, is 
    prepended to non-zero numbers.
    

The `width` field is an optional field that you use to specify a minimum number
of characters to output, and is typically used to pad fixed-width fields in 
tabulated output, where the fields would otherwise be smaller, although it 
does not cause truncation of oversized fields.


```r
sprintf("%*d", 5, 10)
#> [1] "   10"
```


The `precision` field usually specifies a maximum limit on the output, 
depending on the particular formatting type.


```r
sprintf("%.*s", 3, "abcdef")
#> [1] "abc"
```

The `length` field is also optional, and can be any of:


The most important field is the `type` field.

- `%`: Prints a literal `%` character (this type doesn't accept any flags, 
width, precision, length fields).
- `d, i`: integer value as signed decimal number.
- `f`: double value in normal fixed-point notation.
- `e, E`: double value in standard form.
- `g, G`: double value in either normal or exponential notation.
- `x, X`: unsigned integer as a hexadecimal number. `x` uses lower case, while
`X` uses upper case.
- `o`: unsigned integer in octal notation.
- `s`: null terminated string.
- `a, A`: double value in hexadecimal notation


### Example: basic `sprintf()`

Let's begin with a minimal example to explore the different formatting options
of `sprintf()`. Consider a real fraction like `1/6`; in R the default output 
of this fraction will be:


```r
1 / 6
#> [1] 0.1666667
```

Notice that `1/6` is printed with seven decimal digits. The number `1/6` is 
actually an irrational number and so the computer needs to round it to some 
number of decimal digits. You can modify the default printing format in several 
ways. One option is to display only six decimal digits with the `%f` option:


```r
# print 6 decimals
sprintf('%f', 1/6)
#> [1] "0.166667"
```

But you can also specify a different number of decimal digits, say 3. This can 
be achieved specifying an option of `%.3f`:


```r
# print 3 decimals
sprintf('%.3f', 1/6)
#> [1] "0.167"
```

The table below shows six different outputs for `1/6`

| Notation | Output                   |
|:---------|:-------------------------|
| `%s`    | 0.166666666666667   |
| `%f`    | 0.166667   |
| `%.3f`  | 0.167 |
| `%e`    | 1.666667e-01   |
| `%E`    | 1.666667E-01   |
| `%g`    | 0.166667   |


When would you use `sprintf()`? Everytime you produce output text. Some 
cases include: 

1) exporting output to some file.
2) printing output on console.
3) forming new strings.


### Example: File Names

When working on data analysis projects, it is common to generate different 
files with similar names (e.g. either for creating images, or data files, or 
documents). Imagine that you need to generate the names of 3 data files 
(with .csv extension). All the files have the same prefix name but each of them
has a different number: `data01.csv`, `data02.csv`, and `data03.csv`. 
One naive solution to generate a character vector with these names in R would 
be to write something like this:


```r
file_names <- c('data01.csv', 'data02.csv', 'data03.csv')
```

Instead of writing each file name, you can generate the vector `file_names`
in a more efficient way taking advantage of the vectorized nature of 
`paste0()`:


```r
file_names <- paste0('data0', 1:3, '.csv')

file_names
#> [1] "data01.csv" "data02.csv" "data03.csv"
```

Now imagine that you need to generate 100 file names numbered from 01, 02, 03, 
to 100. You could write a vector with 100 file names but it's going to take 
you a while. A preferable solution is to use `paste0()` like in the approach 
of the previous example. In this case however, you would need to create two 
separate vectors---one with numbers 01 to 09, and another one with numbers 
10 to 100---and then concatenate them in one single vector:


```r
files1 <- paste0('data0', 1:9, '.csv')
files2 <- paste0('data', 10:100, '.csv')
file_names <- c(files1, files2)
```

Instead of using `paste0()` to create two vectors, you can use `sprintf()` 
with the `%0xd` option to indicate that an integer should be padded with `x` 
leading zeros. For instance, the first nine file names can be generated as:


```r
sprintf('data%02d.csv', 1:9)
#> [1] "data01.csv" "data02.csv" "data03.csv" "data04.csv" "data05.csv"
#> [6] "data06.csv" "data07.csv" "data08.csv" "data09.csv"
```

To generate the 100 file names do:


```r
file_names <- sprintf('data%02d.csv', 1:100)
```

The first nine elements in `file_names` will include a leading zero before 
the integer; the following elements will not include the leading zero.


### Example: Fahrenheit to Celsius

This example involves working on a function to convert Fahrenheit degrees
into Celsius degrees. The conversion formula is:

$$
Celsius = (Fahrenheit - 32) \times \frac{5}{9}
$$

You can define a simple function `to_celsius()` that takes one argument,
`temp`, which is a number representing temperature in Fahrenheit degrees. 
This function will return the temperature in Celsius degrees:


```r
to_celsius <- function(temp = 1) {
  (temp - 32) * 5/9
}
```

You can use `to_celsius()` as any other function in R. Say you want to 
know how many Celsius degrees are 95 Fahrenheit degrees:


```r
to_celsius(95)
#> [1] 35
```

To make things more interesting, let's create another function that not only 
computes the temperature conversion but also prints a more informative message, something like: `95 Fahrenheit degrees = 35 Celsius degrees`. 

We'll name this function `fahrenheit2celsius()`:


```r
fahrenheit2celsius <- function(temp = 1) {
  celsius <- to_celsius(temp)
  sprintf('%.2f Fahrenheit degrees = %.2f Celsius degrees', temp, celsius)
}
```

Notice that `fahrenheit2celsius()` makes use of `to_celsius()` to
compute the Celsius degrees. And then `sprintf()` is used with the options
`%.2f` to display the temperatures with two decimal digits. Try it out:


```r
fahrenheit2celsius(95)
#> [1] "95.00 Fahrenheit degrees = 35.00 Celsius degrees"
fahrenheit2celsius(50)
#> [1] "50.00 Fahrenheit degrees = 10.00 Celsius degrees"
```


### Example: Car Traveled Distance

Our third example is a little bit more sophisticated. The idea is to construct
an object of class `"car"` that contains characteristics like the name 
of the car, its make, its year, and its fuel consumption in _city_, 
_highway_ and _combined_.

Let's consider a _Mazda 3_ for this example. One possible way to define
a `"car"` object is to use a list with the following elements:


```r
mazda3 <- list(
  name = 'mazda3', # car name
  make = 'mazda',  # car make
  year = 2015,     # year model
  city = 30,       # fuel consumption in city
  highway = 40,    # fuel consumption in highway
  combined = 33)   # fuel consumption combined (city-and-hwy)
```

So far we have an object `mazda3` that is essentially a list. Because we
want to create a `print()` method for objects of class `"car"` we
need to assign this class to our `mazda3`:


```r
class(mazda3) <- "car"
```

Now that we have our `"car"` object, we can create a `print.car()` function. 
In this way, everytime we type `mazda3`, instead of getting the typical list 
output, we will get a customized display:


```r
print.car <- function(x) {
  cat("Car\n")
  cat(sprintf('name: %s\n', x$name))
  cat(sprintf('make: %s\n', x$make))
  cat(sprintf('year: %s\n', x$year))
  invisible(x)
}
```

Next time you type `mazda3` in your console, R will display these lines:


```r
mazda3
#> Car
#> name: mazda3
#> make: mazda
#> year: 2015
```

It would be nice to have a function `miles()` that allows you to calculate the 
traveled distance for a given amount of gas (in gallons), taking into account 
the type of fuel consumption (e.g. city, highway, combined):


```r
miles <- function(car, fuel = 1, mpg = 'city') {
  stopifnot(class(car) == 'car')
  switch(mpg,
         'city' = car$city * fuel,
         'highway' = car$highway * fuel,
         'combined' = car$combined * fuel,
         car$city * fuel)
}
```


The `miles()` function takes three parameters: `car` is an object of
class `"car"`, `fuel` is the number of gallons, and `mpg` is the
type of fuel consumption (`'city', `highway`, `combined'`). The first
command checks whether the first parameter is an object of class `"car"`.
If it is not, then the function will stop the execution raising an error. 
The second command involves using the function `switch()` to compute the 
traveled miles. It switches to the corresponding consumption depending on the
provided value of `mpg`. Note that the very last switch condition is a
_safety_ condition in case the user mispecifies `mpg`.

Let's say you want to know how many miles the `mazda3` could
travel with 4 gallons of gas depending on the different types of consumption:


```r
miles(mazda3, fuel = 4, 'city')
#> [1] 120
miles(mazda3, fuel = 4, 'highway')
#> [1] 160
miles(mazda3, fuel = 4, 'combined')
#> [1] 132
```

Again, to make things more user friendly, we are going to create a function
`get_distance()` that prints a more informative message about the
traveled distance:


```r
get_distance <- function(car, fuel = 1, mpg = 'city') {
  distance <- miles(car, fuel = fuel, mpg = mpg) 
  cat(sprintf('A %s can travel %s miles\n',
              car$name, distance))
  cat(sprintf('with %s gallons of gas\n', fuel))
  cat(sprintf('using %s consumption', mpg))
}
```

And this is how the output when calling `get_distance` looks like:


```r
get_distance(mazda3, 4, 'city')
#> A mazda3 can travel 120 miles
#> with 4 gallons of gas
#> using city consumption
```


### Example: Coffee Prices

Consider some coffee drinks and their prices. We'll put this information in a 
vector like this:


```r
prices <- c(
  'americano' = 2, 
  'latte' = 2.75, 
  'mocha' = 3.45, 
  'capuccino' = 3.25)
```

What type of vector is `prices`? Is it a character vector? Is it numeric 
vector? Or is it some sort of vector with mix-data? We have seen that vectors 
are _atomic_ structures, meaning that all their elements must be of the
same class. So `prices` is definitely not a vector with mix-data. 
From the code chunk we can observe that each element of the vector is formed 
by a string, followed by the `=` sign, followed by some number. 
This way of defining a vector is not very common in R but it is perfectly 
valid. Each string represents the name of an element, while 
the numbers are the actual elements. Therefore `prices` is in reality 
a numeric vector. You can confirm this by looking at the mode (or data type):


```r
mode(prices)
#> [1] "numeric"
```

Let's say you want to list the names of the coffees and their prices. If you 
just simply try to `print()` the prices, the output will be the entire 
vector `prices`:


```r
print(prices)
#> americano     latte     mocha capuccino 
#>      2.00      2.75      3.45      3.25
```

Alternatively, you can use a for loop to `print()` each individual element of 
the vector `prices`, but again the output is displayed in an awkward fashion:


```r
for (p in seq_along(prices)) {
  print(prices[p])
}
#> americano 
#>         2 
#> latte 
#>  2.75 
#> mocha 
#>  3.45 
#> capuccino 
#>      3.25
```

To list the names of the coffees and their prices, it would be nicer to use
a combination of `paste0()` and `print()`. In addition, you can be
more descriptive adding some auxiliary text such that the output prints
something like: _"americano has a price of $2"_.


```r
for (p in seq_along(prices)) {
  print(paste0(names(prices)[p], ' has price of $', prices[p]))
}
#> [1] "americano has price of $2"
#> [1] "latte has price of $2.75"
#> [1] "mocha has price of $3.45"
#> [1] "capuccino has price of $3.25"
```

Another possible solution consists of combining `print()` and `sprintf()`:


```r
for (p in seq_along(prices)) {
  print(sprintf('%s has price of $%s', names(prices)[p], prices[p]))
}
#> [1] "americano has price of $2"
#> [1] "latte has price of $2.75"
#> [1] "mocha has price of $3.45"
#> [1] "capuccino has price of $3.25"
```

One limitation of `quote()` is that it won't work inside a for loop:


```r
for (p in seq_along(prices)) {
  noquote(sprintf('%s has price of $%s', names(prices)[p], prices[p]))
}
```

If what you want is to print the output wihtout quotes, then you need to 
use `cat()`; just make sure to add a newline character `"\n"`:


```r
for (p in seq_along(prices)) {
  cat(sprintf('%s has price of $%s\n', names(prices)[p], prices[p]))
}
#> americano has price of $2
#> latte has price of $2.75
#> mocha has price of $3.45
#> capuccino has price of $3.25
```


<!--chapter:end:sprintf.Rmd-->


# Input and Output



## Output

Some times you need to export results to a file. Typically this happens when
you want to export a data table to a text file. R provides the functions
`write.table()` and `write.csv()` for these purposes.
These functions let you send a matrix or a data frame to a text file that will
have a tabular format (i.e. rows and columns).


### Concatenating output

You can use `cat()` to concatenate and print information to a file. 

To show you how to use `cat()` let's illustrate a simple example using the data 
frame `mtcars` that comes in R.


```r
# summary statistics of unemp
min(mtcars$mpg)
max(mtcars$mpg)
median(mtcars$mpg)
mean(mtcars$mpg)
sd(mtcars$mpg)
```

The goal is to generate a file `mpg-statistics.txt` with the following 
contents:

```
Miles per Gallon Statistics

Minimum: 10.40
Maximum: 33.90
Median : 19.20
Mean   : 20.09 
Std Dev: 6.02
```

Here is one way to do it. First, let's assign the statistics to different
objects:


```r
# summary statistics of mpg
mpg_min <- min(mtcars$mpg)
mpg_max <- max(mtcars$mpg)
mpg_med <- median(mtcars$mpg)
mpg_avg <- mean(mtcars$mpg)
mpg_sd <- sd(mtcars$mpg)
```

After creating the objects containing the summary statistics, the next step
is to export them to the text file `mpg-statistics.txt` via `cat()`. 
Assuming that the output file is in your working directory, here's how you can
send the set of strings to the text file:


```r
# name of output file
outfile <- "mpg-statistics.txt"

# first line of the file
cat("Miles per Gallon Statistics\n\n", file = outfile)

# subsequent lines appended to the output file
cat("Minimum:", mpg_min, "\n", file = outfile, append = TRUE)
cat("Maximum:", mpg_max, "\n", file = outfile, append = TRUE)
cat("Median :", mpg_med, "\n", file = outfile, append = TRUE)
cat("Mean   :", mpg_avg, "\n", file = outfile, append = TRUE)
cat("Std Dev:", mpg_sd, "\n", file = outfile, append = TRUE)
```

The first line exported to `mpg-statistics.txt` is a string with the title
`"Miles per Gallon Statistics\n\n"`. Observe that we are using two new line
characters `"\n\n"` to add some space between the title and the statistics.
The rest of calls to `cat()` use the argument `append = TRUE` to concatenate
the specified strings to the end of the text file without overriding the 
existing lines.

If you run the code of this example and look at the contents of 
`mpg-statistics.txt`, you will see the following output:

```
Miles per Gallon Statistics

Minimum: 10.4 
Maximum: 33.9 
Median : 19.2 
Mean   : 20.09062 
Std Dev: 6.026948 
```

As you can tell, the displayed values have a different number of decimal 
digits. If you just want to keep two decimal digits, you can use `sprintf()`
and choose the format `"%0.2f"`. Let's re-export the lines:


```r
cat("Miles per Gallon Statistics\n\n", file = outfile)
cat(sprintf('Minimum: %0.2f', mpg_min), "\n", file = outfile, append = TRUE)
cat(sprintf('Maximum: %0.2f', mpg_max), "\n", file = outfile, append = TRUE)
cat(sprintf('Median : %0.2f', mpg_med), "\n", file = outfile, append = TRUE)
cat(sprintf('Mean   : %0.2f', mpg_avg), "\n", file = outfile, append = TRUE)
cat(sprintf('Std Dev: %0.2f', mpg_sd), "\n", file = outfile, append = TRUE)
```

Now the content of `mpg-statistics.txt` should look like this:

```
Miles per Gallon Statistics

Minimum: 10.40 
Maximum: 33.90 
Median : 19.20 
Mean   : 20.09 
Std Dev: 6.03 
```

Here is an exercise for you: How would you avoid writing that many calls to 
`cat()`?


### Sinking output

Another interesting function is `sink()`. This function is very useful when
you want to export R output as is displayed in the R console. For example, 
consider the output from `summary()`


```r
summary(mtcars)
```

You could assign the output of `summary(mtcars)` to an object and then try
`writeLines()` to export the results to a file `mtcars-summary.txt`, but 
you won't keep the same format of R:


```r
mtcars_summary <- summary(mtcars)
writeLines(mtcars_summary, con = "mtcars-summary.txt")
```

To be able to keep the same output display of R, you must use `sink()`. This
function will __divert__ R output to the specified file:


```r
sink(file = "mtcars-statistics.txt")
summary(australia)
sink()
```

__Your turn:__ Use `sink()` to send the output from running a linear 
regression of `mpg` on `disp` with the function `lm()`. Also export the results 
from using `summary()` on the regression object. And/or try running a t-test
between `mpg` and `disp` with `t.test()`.



## Exporting tables

Another interesting tool to export tables in LaTeX or HTML formats is provided
by the R package `"xtable"` and its main function `xtable()`.


```r
library(xtable)

# linear regression
reg <- lm(mpg ~ disp, data = mtcars)

# create xtable and export it
reg_table <- xtable(reg)
```

The object `reg_table` is an object of class `"xtable"`. What you do with this
type of objects is `print()` them to a file.

To print `reg_table` in latex format to a `.tex` file:


```r
print(reg_table, type = "latex", file = "reg-table.tex")
```

To print `reg_table` in html format to an `.html` file:


```r
print(reg_table, type = "html", file = "reg-table.html")
```

<!--chapter:end:input-output.Rmd-->


# (PART) Manipulations {-}

# Basic String Manipulations {#manip}

## Introduction

In this chapter you will learn about the different functions to do what I call
_basic manipulations_. By "basic" I mean transforming and processing strings
in such way that do not require the use of [regular expressions](#intro). More 
advanced manipulations involve defining patterns of text and matching such
patterns. This is the essential idea behind regular expressions, which is 
the content of part 5 in this book.


## Basic Manipulations

Besides creating and printing strings, there are a number of very handy 
functions in R for doing some basic manipulation of strings. In this chapter    
we will review the following functions:

| Function       | Description                      |
|:---------------|:---------------------------------|
| `nchar()`      | number of characters             |
| `tolower()`    | convert to lower case            |
| `toupper()`    | convert to upper case            |
| `casefold()`   | case folding                     |
| `chartr()`     | character translation            |
| `abbreviate()` | abbreviation                     |
| `substring()`  | substrings of a character vector |
| `substr()`     | substrings of a character vector |

 
## Counting characters

One of the main functions for manipulating character strings is `nchar()` 
which counts the number of characters in a string. In other words, `nchar()` 
provides the length of a string:


```r
# how many characters?
nchar(c("How", "many", "characters?"))
#> [1]  3  4 11

# how many characters?
nchar("How many characters?")
#> [1] 20
```

Notice that the white spaces between words in the second example are also 
counted as characters. 

It is important not to confuse `nchar()` with `length()`. While the former 
gives us the __number of characters__, the later only gives the number of 
elements in a vector.


```r
# how many elements?
length(c("How", "many", "characters?"))
#> [1] 3

# how many elements?
length("How many characters?")
#> [1] 1
```


## Casefolding

R comes with three functions for text casefolding. 

1. `tolower()`
2. `toupper()`
3. `casefold()`

The function `tolower()` converts any upper case characters into lower case:


```r
# to lower case
tolower(c("aLL ChaRacterS in LoweR caSe", "ABCDE"))
#> [1] "all characters in lower case" "abcde"
```

The opposite function of `tolower()` is `toupper`. As you may guess, this 
function converts any lower case characters into upper case:


```r
# to upper case
toupper(c("All ChaRacterS in Upper Case", "abcde"))
#> [1] "ALL CHARACTERS IN UPPER CASE" "ABCDE"
```

The third function for case-folding is `casefold()` which is a wrapper for both `tolower()` and `toupper()`. Its uasge has the following form:

```
casefold(x, upper = FALSE)
```

By default, `casefold()` converts all characters to lower case, but you can 
use the argument `upper = TRUE` to indicate the opposite (characters in upper 
case):


```r
# lower case folding
casefold("aLL ChaRacterS in LoweR caSe")
#> [1] "all characters in lower case"

# upper case folding
casefold("All ChaRacterS in Upper Case", upper = TRUE)
#> [1] "ALL CHARACTERS IN UPPER CASE"
```

I've found the case-folding functions to be very helpful when I write functions
that take a character input which may be specified in lower or upper case, or 
perhaps as a mix of both cases. For instance, consider the function 
`temp_convert()` that takes a temperature value in Fahrenheit degress, and
a character string indicating the name of the scale to be converted.


```r
temp_convert <- function(deg = 1, to = "celsius") {
  switch(to,
         "celsius" = (deg - 32) * (5/9),
         "kelvin" = (deg + 459.67) * (5/9),
         "reaumur" = (deg - 32) * (4/9),
         "rankine" = deg + 459.67)
}
```

Here is how you call `temp_convert()` to convert 10 Fahrenheit degrees into 
celsius degrees:


```r
temp_convert(deg = 10, to = "celsius")
#> [1] -12.22222
```

`temp_convert()` works fine when the argument `to = 'celsius'`. But what 
happens if you try `temp_convert(30, 'Celsius')` or 
`temp_convert(30, 'CELSIUS')`?

To have a more flexible function `temp_convert()` you can apply `tolower()`
to the argument `to`, and in this way guarantee that the provided string by
the user is always in lower case:


```r
temp_convert <- function(deg = 1, to = "celsius") {
  switch(tolower(to),
         "celsius" = (deg - 32) * (5/9),
         "kelvin" = (deg + 459.67) * (5/9),
         "reaumur" = (deg - 32) * (4/9),
         "rankine" = deg + 459.67)
}
```

Now all the following three calls are equivalent:


```r
temp_convert(30, 'celsius')
temp_convert(30, 'Celsius')
temp_convert(30, 'CELSIUS')
```



## Translating characters

There's also the function `chartr()` which stands for _character translation_. `chartr()` takes three arguments: an `old` string, a `new` string, and a 
character vector `x`:

```
chartr(old, new, x)
```

The way `chartr()` works is by replacing the characters in `old` that appear 
in `x` by those indicated in `new`. For example, suppose we want to translate 
the letter `"a"` (lower case) with `"A"` (upper case) in the sentence 
`"This is a boring string"`:


```r
# replace 'a' by 'A'
chartr("a", "A", "This is a boring string")
#> [1] "This is A boring string"
```

It is important to note that `old` and `new` must have the same number of 
characters, otherwise you will get a nasty error message like this one:


```r
# incorrect use
chartr("ai", "X", "This is a bad example")
#> Error in chartr("ai", "X", "This is a bad example"): 'old' is longer than 'new'
```

Here's a more interesting example with `old = "aei"` and `new = "\#!?"`. 
This implies that any `'a'` in `'x'` will be replaced by `'\#'`, any `'e'` in 
`'x'` will be replaced by `'?'`, and any `'i'` in `'x'` will be replaced by 
`'?'`:


```r
# multiple replacements
crazy <- c("Here's to the crazy ones", "The misfits", "The rebels")
chartr("aei", "#!?", crazy)
#> [1] "H!r!'s to th! cr#zy on!s" "Th! m?sf?ts"             
#> [3] "Th! r!b!ls"
```


## Abbreviating strings

Another useful function for basic manipulation of character strings is 
`abbreviate()`. Its usage has the following structure:

```
abbreviate(names.org, minlength = 4, dot = FALSE, strict = FALSE,
            method = c("left.keep", "both.sides"))
```

Although there are several arguments, the main parameter is the character 
vector (`names.org`) which will contain the names that we want to abbreviate:


```r
# some color names
some_colors <- colors()[1:4]
some_colors
#> [1] "white"         "aliceblue"     "antiquewhite"  "antiquewhite1"

# abbreviate (default usage)
colors1 <- abbreviate(some_colors)
colors1
#>         white     aliceblue  antiquewhite antiquewhite1 
#>        "whit"        "alcb"        "antq"        "ant1"

# abbreviate with 'minlength'
colors2 <- abbreviate(some_colors, minlength = 5)
colors2
#>         white     aliceblue  antiquewhite antiquewhite1 
#>       "white"       "alcbl"       "antqw"       "antq1"

# abbreviate
colors3 <- abbreviate(some_colors, minlength = 3, method = "both.sides")
colors3
#>         white     aliceblue  antiquewhite antiquewhite1 
#>         "wht"         "alc"         "ant"         "an1"
```


A common use for `abbreviate()` is when plotting names of objects or variables
in a graphic. I will use the built-in data set `mtcars` to show you a simple
example with a scatterplot between variables `mpg` and `disp`


```r
plot(mtcars$mpg, mtcars$disp, type = "n")
text(mtcars$mpg, mtcars$disp, rownames(mtcars))
```

<img src="_main_files/figure-html4/unnamed-chunk-48-1.png" width="70%" style="display: block; margin: auto;" />

The names of the cars are all over the plot. In this situation you may want to
consider using `abbreviate()` to shrink the names of the cars and produce a 
less "crowded" plot:


```r
plot(mtcars$mpg, mtcars$disp, type = "n")
text(mtcars$mpg, mtcars$disp, abbreviate(rownames(mtcars)))
```

<img src="_main_files/figure-html4/unnamed-chunk-49-1.png" width="70%" style="display: block; margin: auto;" />


## Replacing strings

One common operation when working with strings is the extraction and 
replacement of some characters. There a various ways in which characters can
be replaced. If the replacement is based on the positions that characters 
occupy in the string, you can use the functions `substr()` and `substring()`

`substr()` extracts or replaces substrings in a character vector. Its usage has 
the following form:

```
substr(x, start, stop)
```

`x` is a character vector, `start` indicates the first element to be replaced, 
and `stop` indicates the last element to be replaced:


```r
# extract 'bcd'
substr("abcdef", 2, 4)
#> [1] "bcd"

# replace 2nd letter with hash symbol
x <- c("may", "the", "force", "be", "with", "you")
substr(x, 2, 2) <- "#"
x
#> [1] "m#y"   "t#e"   "f#rce" "b#"    "w#th"  "y#u"

# replace 2nd and 3rd letters with happy face
y = c("may", "the", "force", "be", "with", "you")
substr(y, 2, 3) <- ":)"
y
#> [1] "m:)"   "t:)"   "f:)ce" "b:"    "w:)h"  "y:)"

# replacement with recycling
z <- c("may", "the", "force", "be", "with", "you")
substr(z, 2, 3) <- c("#", "```")
z
#> [1] "m#y"   "t``"   "f#rce" "b`"    "w#th"  "y``"
```


Closely related to `substr()` is the function `substring()` which extracts or 
replaces substrings in a character vector. Its usage has the following form:

```
substring(text, first, last = 1000000L)
```

`text` is a character vector, `first` indicates the first element to be 
replaced, and `last` indicates the last element to be replaced:


```r
# same as 'substr'
substring("ABCDEF", 2, 4)
#> [1] "BCD"
substr("ABCDEF", 2, 4)
#> [1] "BCD"

# extract each letter
substring("ABCDEF", 1:6, 1:6)
#> [1] "A" "B" "C" "D" "E" "F"

# multiple replacement with recycling
text6 <- c("more", "emotions", "are", "better", "than", "less")
substring(text6, 1:3) <- c(" ", "zzz")
text6
#> [1] " ore"     "ezzzions" "ar "      "zzzter"   "t an"     "lezz"
```



## Set Operations

R has dedicated functions for performing set operations on two given vectors. 
This implies that we can apply functions such as set union, intersection, 
difference, equality and membership, on `"character"` vectors. 

| Function       | Description    |
|:---------------|:---------------|
| `union()`      | set union      |
| `intersect()`  | intersection   |
| `setdiff()`    | set difference |
| `setequal()`   | equal sets     |
| `identical()`  | exact equality |
| `is.element()` | is element     |
| `%in%()`     | contains       |
| `sort()`       | sorting        |


### Set union with `union()`

Let's start our reviewing of set functions with `union()`. As its name 
indicates, you can use `union()} when you want to obtain the elements of 
the union between two character vectors:


```r
# two character vectors
set1 <- c("some", "random", "words", "some")
set2 <- c("some", "many", "none", "few")

# union of set1 and set2
union(set1, set2)
#> [1] "some"   "random" "words"  "many"   "none"   "few"
```

Notice that `union()` discards any duplicated values in the provided vectors. 
In the previous example the word `"some"` appears twice inside `set1` but it 
appears only once in the union. In fact all the set operation functions will 
discard any duplicated values.


### Set intersection with `intersect()`

Set intersection is performed with the function `intersect()`. You can use this
function when you wish to get those elements that are common to both vectors:


```r
# two character vectors
set3 <- c("some", "random", "few", "words")
set4 <- c("some", "many", "none", "few")

# intersect of set3 and set4
intersect(set3, set4)
#> [1] "some" "few"
```


### Set difference with `setdiff()`

Related to the intersection, you might be interested in getting the difference 
of the elements between two character vectors. This can be done with `setdiff()`:


```r
# two character vectors
set5 <- c("some", "random", "few", "words")
set6 <- c("some", "many", "none", "few")

# difference between set5 and set6
setdiff(set5, set6)
#> [1] "random" "words"
```


### Set equality with `setequal()`

The function `setequal()` allows you to test the equality of two character 
vectors. If the vectors contain the same elements, `setequal()` returns `TRUE` (`FALSE` otherwise)


```r
# three character vectors
set7 <- c("some", "random", "strings")
set8 <- c("some", "many", "none", "few")
set9 <- c("strings", "random", "some")

# set7 == set8?
setequal(set7, set8)
#> [1] FALSE

# set7 == set9?
setequal(set7, set9)
#> [1] TRUE
```


### Exact equality with `identical()`

Sometimes `setequal()` is not always what we want to use. It might be the case 
that you want to test whether two vectors are _exactly equal_ (element by 
element). For instance, testing if `set7` is exactly equal to `set9`. Although 
both vectors contain the same set of elements, they are not exactly the same 
vector. Such test can be performed with the function `identical()`


```r
# set7 identical to set7?
identical(set7, set7)
#> [1] TRUE

# set7 identical to set9?
identical(set7, set9)
#> [1] FALSE
```

If you consult the help documentation of `identical()`, you will see that this 
function is the "safe and reliable way to test two objects for being exactly 
equal".



### Element contained with `is.element()`

If you wish to test if an element is contained in a given set of character 
strings you can do so with `is.element()`:


```r
# three vectors
set10 <- c("some", "stuff", "to", "play", "with")
elem1 <- "play"
elem2 <- "crazy"

# elem1 in set10?
is.element(elem1, set10)
#> [1] TRUE

# elem2 in set10?
is.element(elem2, set10)
#> [1] FALSE
```

Alternatively, you can use the binary operator `%in%` to test if an element 
is contained in a given set. The function `%in%` returns `TRUE` if the first 
operand is contained in the second, and it returns `FALSE` otherwise:


```r
# elem1 in set10?
elem1 %in% set10
#> [1] TRUE

# elem2 in set10?
elem2 %in% set10
#> [1] FALSE
```


### Sorting with `sort()`

The function `sort()` allows you to sort the elements of a vector, either in 
increasing order (by default) or in decreasing order using the argument `decreasing`:


```r
set11 = c("today", "produced", "example", "beautiful", "a", "nicely")

# sort (decreasing order)
sort(set11)
#> [1] "a"         "beautiful" "example"   "nicely"    "produced"  "today"

# sort (increasing order)
sort(set11, decreasing = TRUE)
#> [1] "today"     "produced"  "nicely"    "example"   "beautiful" "a"
```

If you have alpha-numeric strings, `sort()` will put the numbers first when 
sorting in increasing order:


```r
set12 = c("today", "produced", "example", "beautiful", "1", "nicely")

# sort (decreasing order)
sort(set12)
#> [1] "1"         "beautiful" "example"   "nicely"    "produced"  "today"

# sort (increasing order)
sort(set12, decreasing = TRUE)
#> [1] "today"     "produced"  "nicely"    "example"   "beautiful" "1"
```

<!--chapter:end:basic-manipulations.Rmd-->


# Stringr Basics


## Introduction

So far we've seen the various functions R provides to perform basic string 
processing and manipulations of `"character"` data. Most of the times these 
functions are enough and they will allow you to get your job done. However, 
they have some drawbacks. For instance, consider the following example:


```r
# some text vector
text <- c("one", "two", "three", NA, "five")

# how many characters in each string?
nchar(text)
#> [1]  3  3  5 NA  4
```

As you can tell, `nchar()` gives `NA` a value of 2, as if it were a string 
formed by two characters. Perhaps this may be acceptable in some cases, but 
taking into account all the operations in R, it would be better to leave `NA` 
as a missing value, instead of treating it as a string of two characters.

Another awkward example can be found with `paste()`. The default separator is 
a blank space, which more often than not is what you want to use. But that's 
secondary. The really annoying thing is when you want to paste things that 
include zero length arguments (e.g. `NULL`, `character(0)`). How does `paste()` 
behave in those cases? See below:  


```r
# this works fine
paste("University", "of", "California", "Berkeley")
#> [1] "University of California Berkeley"

# this works fine too
paste("University", "of", "California", "Berkeley")
#> [1] "University of California Berkeley"

# this is weird
paste("University", "of", "California", "Berkeley", NULL)
#> [1] "University of California Berkeley "

# this is ugly
paste("University", "of", "California", "Berkeley", NULL, character(0), 
      "Go Bears!")
#> [1] "University of California Berkeley   Go Bears!"
```

Notice the output from the last example (the _ugly_ one). The objects `NULL` 
and `character(0)` have zero length, yet when included inside `paste()` they 
are treated as an empty string `""`. Wouldn't be good if `paste()` removed 
zero length arguments? Sadly, there's nothing we can do to change `nchar()` and 
`paste()`. But fear not. There is a very nice package that solves these 
problems and provides several functions for carrying out consistent string 
processing.



## Package `stringr`

Thanks to Hadley Wickham, we have the package `stringr` that adds more 
functionality to the base functions for handling strings in R. 

[http://cran.r-project.org/web/packages/stringr/index.html](http://cran.r-project.org/web/packages/stringr/index.html)

According to the description of the package:

> "is a set of simple wrappers that make R's string functions more consistent, 
> simpler and easier to use. It does this by ensuring that: function and 
> argument names (and positions) are consistent, all functions deal with NA's 
> and zero length character appropriately, and the output data structures from 
> each function matches the input data structures of other functions."

To install `"stringr"` use the function `install.packages()`. Once installed, 
load it to your current session with `library()`:


```r
# installing 'stringr'
install.packages("stringr")

# load 'stringr'
library(stringr)
```




## Basic String Operations

`"stringr"` provides functions for both 1) basic manipulations and 2) for 
regular expression operations. In this chapter we cover those functions that 
have to do with basic manipulations. 

The following table contains the `stringr` functions for basic string operations:

| Function       | Description                             | Similar to    |
|:---------------|:----------------------------------------|:--------------|
| `str_c()`      | string concatenation                    | `paste()`     |
| `str_length()` | number of characters                    | `nchar()`     |
| `str_sub()`    | extracts substrings                     | `substring()` |
| `str_dup()`    | duplicates characters                   | _none_        |
| `str_trim()`   | removes leading and trailing whitespace | _none_        |
| `str_pad()`    | pads a string                           | _none_        |
| `str_wrap()`   | wraps a string paragraph                | `strwrap()`   |
| `str_trim()`   | trims a string                          | _none_        |


Notice that all functions in `stringr` start with `"str_"` followed by a term 
associated to the task they perform. For example, `str_length()` gives you the 
number (i.e. length) of characters in a string. In addition, some functions are 
designed to provide a better alternative to already existing functions. This is 
the case of `str_length()` which is intended to be a substitute of `nchar()`. 
Other functions, however, don't have a corresponding alternative such as 
`str_dup()` which allows you to duplicate characters.


### Concatenating with `str_c()`

Let's begin with `str_c()`. This function is equivalent to `paste()` but 
instead of using the white space as the default separator, `str_c()` uses the 
empty string `""` which is a more common separator when _pasting_ strings:


```r
# default usage
str_c("May", "The", "Force", "Be", "With", "You")
#> [1] "MayTheForceBeWithYou"

# removing zero length objects
str_c("May", "The", "Force", NULL, "Be", "With", "You", character(0))
#> [1] "MayTheForceBeWithYou"
```

Observe another major difference between `str_c()` and `paste()`: zero length 
arguments like `NULL` and `character(0)` are silently removed by `str_c()`. 

If you want to change the default separator, you can do that as usual by 
specifying the argument `sep`:


```r
# changing separator
str_c("May", "The", "Force", "Be", "With", "You", sep = "_")
#> [1] "May_The_Force_Be_With_You"
```



### Number of characters with `str_length()`

As we've mentioned before, the function `str_length()` is equivalent to 
`nchar()`. Both functions return the number of characters in a string, that is, 
the _length_ of a string (do not confuse it with the `length()` of a vector). 
Compared to `nchar()`, `str_length()` has a more consistent behavior when 
dealing with `NA` values. Instead of giving `NA` a length of 2, `str_length()` 
preserves missing values just as `NA`s.


```r
# some text (NA included)
some_text <- c("one", "two", "three", NA, "five")

# compare 'str_length' with 'nchar'
nchar(some_text)
#> [1]  3  3  5 NA  4
str_length(some_text)
#> [1]  3  3  5 NA  4
```

In addition, `str_length()` has the nice feature that it converts factors to 
characters, something that `nchar()` is not able to handle:


```r
some_factor <- factor(c(1,1,1,2,2,2), labels = c("good", "bad"))
some_factor
#> [1] good good good bad  bad  bad 
#> Levels: good bad

# try 'nchar' on a factor
nchar(some_factor)
#> Error in nchar(some_factor): 'nchar()' requires a character vector

# now compare it with 'str_length'
str_length(some_factor)
#> [1] 4 4 4 3 3 3
```


### Substring with `str_sub()`

To extract substrings from a character vector `stringr` provides `str_sub()` 
which is equivalent to `substring()`. The function `str_sub()` has the 
following usage form:

```
str_sub(string, start = 1L, end = -1L)
```

The three arguments in the function are: a `string` vector, a `start` value 
indicating the position of the first character in substring, and an `end` value 
indicating the position of the last character. Here's a simple example with a 
single string in which characters from 1 to 5 are extracted:


```r
lorem <- "Lorem Ipsum"

# apply 'str_sub'
str_sub(lorem, start = 1, end = 5)
#> [1] "Lorem"

# equivalent to 'substring'
substring(lorem, first = 1, last = 5)
#> [1] "Lorem"

# another example
str_sub("adios", 1:3)
#> [1] "adios" "dios"  "ios"
```

An interesting feature of `str_sub()` is its ability to work with negative 
indices in the `start` and `end` positions. When we use a negative position, `str_sub()` counts backwards from last character: 


```r
resto = c("brasserie", "bistrot", "creperie", "bouchon")

# 'str_sub' with negative positions
str_sub(resto, start = -4, end = -1)
#> [1] "erie" "trot" "erie" "chon"

# compared to substring (useless)
substring(resto, first = -4, last = -1)
#> [1] "" "" "" ""
```

Similar to `substring()`, we can also give `str_sub()` a set of positions which 
will be recycled over the string. But even better, we can give `str_sub()` 
a negative sequence, something that `substring()` ignores:


```r
# extracting sequentially
str_sub(lorem, seq_len(nchar(lorem)))
#>  [1] "Lorem Ipsum" "orem Ipsum"  "rem Ipsum"   "em Ipsum"    "m Ipsum"    
#>  [6] " Ipsum"      "Ipsum"       "psum"        "sum"         "um"         
#> [11] "m"
substring(lorem, seq_len(nchar(lorem)))
#>  [1] "Lorem Ipsum" "orem Ipsum"  "rem Ipsum"   "em Ipsum"    "m Ipsum"    
#>  [6] " Ipsum"      "Ipsum"       "psum"        "sum"         "um"         
#> [11] "m"

# reverse substrings with negative positions
str_sub(lorem, -seq_len(nchar(lorem)))
#>  [1] "m"           "um"          "sum"         "psum"        "Ipsum"      
#>  [6] " Ipsum"      "m Ipsum"     "em Ipsum"    "rem Ipsum"   "orem Ipsum" 
#> [11] "Lorem Ipsum"
substring(lorem, -seq_len(nchar(lorem)))
#>  [1] "Lorem Ipsum" "Lorem Ipsum" "Lorem Ipsum" "Lorem Ipsum" "Lorem Ipsum"
#>  [6] "Lorem Ipsum" "Lorem Ipsum" "Lorem Ipsum" "Lorem Ipsum" "Lorem Ipsum"
#> [11] "Lorem Ipsum"
```

We can use `str_sub()` not only for extracting subtrings but also for replacing
substrings:


```r
# replacing 'Lorem' with 'Nullam'
lorem <- "Lorem Ipsum"
str_sub(lorem, 1, 5) <- "Nullam"
lorem
#> [1] "Nullam Ipsum"

# replacing with negative positions
lorem <- "Lorem Ipsum"
str_sub(lorem, -1) <- "Nullam"
lorem
#> [1] "Lorem IpsuNullam"

# multiple replacements 
lorem <- "Lorem Ipsum"
str_sub(lorem, c(1,7), c(5,8)) <- c("Nullam", "Enim")
lorem
#> [1] "Nullam Ipsum"  "Lorem Enimsum"
```


### Duplication with `str_dup()`

A common operation when handling characters is _duplication_. The problem is 
that R doesn't have a specific function for that purpose. But `stringr` does: `str_dup()` duplicates and concatenates strings within a character vector. 
Its usage requires two arguments:

```
str_dup(string, times)
```

The first input is the `string` that you want to dplicate. The second input, 
`times`, is the number of times to duplicate each string:


```r
# default usage
str_dup("hola", 3)
#> [1] "holaholahola"

# use with differetn 'times'
str_dup("adios", 1:3)
#> [1] "adios"           "adiosadios"      "adiosadiosadios"

# use with a string vector
words <- c("lorem", "ipsum", "dolor", "sit", "amet")
str_dup(words, 2)
#> [1] "loremlorem" "ipsumipsum" "dolordolor" "sitsit"     "ametamet"

str_dup(words, 1:5)
#> [1] "lorem"                "ipsumipsum"           "dolordolordolor"     
#> [4] "sitsitsitsit"         "ametametametametamet"
```


### Padding with `str_pad()`

Another handy function that we can find in `stringr` is `str_pad()` for 
_padding_ a string. Its default usage has the following form:

```
str_pad(string, width, side = "left", pad = " ")
```

The idea of `str_pad()` is to take a string and pad it with leading or trailing 
characters to a specified total `width`. The default padding character is a 
space (`pad = " "`), and consequently the returned string will appear to be 
either left-aligned (`side = "left"`), right-aligned (`side = "right"`), or 
both (`side = "both"`). 

Let's see some examples:


```r
# default usage
str_pad("hola", width = 7)
#> [1] "   hola"

# pad both sides
str_pad("adios", width = 7, side = "both")
#> [1] " adios "

# left padding with '#'
str_pad("hashtag", width = 8, pad = "#")
#> [1] "#hashtag"

# pad both sides with '-'
str_pad("hashtag", width = 9, side = "both", pad = "-")
#> [1] "-hashtag-"
```


### Wrapping with `str_wrap()`

The function `str_wrap()` is equivalent to `strwrap()` which can be used to 
_wrap_ a string to format paragraphs. The idea of wrapping a (long) string is 
to first split it into paragraphs according to the given `width`, and then add 
the specified indentation in each line (first line with `indent`, following 
lines with `exdent`). Its default usage has the following form:

```
str_wrap(string, width = 80, indent = 0, exdent = 0)
```

For instance, consider the following quote (from Douglas Adams) converted into 
a  paragraph:


```r
# quote (by Douglas Adams)
some_quote <- c(
  "I may not have gone",
  "where I intended to go,", 
  "but I think I have ended up",
  "where I needed to be")

# some_quote in a single paragraph
some_quote <- paste(some_quote, collapse = " ")
```

Now, say you want to display the text of `some_quote` within some pre-specified 
column width (e.g. width of 30). You can achieve this by applying `str_wrap()` 
and setting the argument `width = 30`


```r
# display paragraph with width=30
cat(str_wrap(some_quote, width = 30))
#> I may not have gone where I
#> intended to go, but I think I
#> have ended up where I needed
#> to be
```

Besides displaying a (long) paragraph into several lines, you may also wish to 
add some indentation. Here's how you can indent the first line, as well as the 
following lines: 


```r
# display paragraph with first line indentation of 2
cat(str_wrap(some_quote, width = 30, indent = 2), "\n")
#>   I may not have gone where I
#> intended to go, but I think I
#> have ended up where I needed
#> to be

# display paragraph with following lines indentation of 3
cat(str_wrap(some_quote, width = 30, exdent = 3), "\n")
#> I may not have gone where I
#>    intended to go, but I think I
#>    have ended up where I needed
#>    to be
```



### Trimming with `str_trim()`

One of the typical tasks of string processing is that of parsing a text into 
individual words. Usually, you end up with words that have blank spaces, called _whitespaces_, on either end of the word. In this situation, you can use the 
`str_trim()` function to remove any number of whitespaces at the ends of a 
string. Its usage requires only two arguments:

```
str_trim(string, side = "both")
```

The first input is the `string` to be strimmed, and the second input indicates 
the `side` on which the whitespace will be removed.

Consider the following vector of strings, some of which have whitespaces either 
on the left, on the right, or on both sides. Here's what `str_trim()` would do 
to them under different settings of `side`


```r
# text with whitespaces
bad_text <- c("This", " example ", "has several   ", "   whitespaces ")

# remove whitespaces on the left side
str_trim(bad_text, side = "left")
#> [1] "This"           "example "       "has several   " "whitespaces "

# remove whitespaces on the right side
str_trim(bad_text, side = "right")
#> [1] "This"           " example"       "has several"    "   whitespaces"

# remove whitespaces on both sides
str_trim(bad_text, side = "both")
#> [1] "This"        "example"     "has several" "whitespaces"
```


### Word extraction with `word()`

We end this chapter describing the `word()` function that is designed to 
extract words from a sentence:

```
word(string, start = 1L, end = start, sep = fixed(" "))
```

The way in which you use `word()` is by passing it a `string`, together with a 
`start` position of the first word to extract, and an `end` position of the 
last word to extract. By default, the separator `sep` used between words is a 
single space.

Let's see some examples:


```r
# some sentence
change <- c("Be the change", "you want to be")

# extract first word
word(change, 1)
#> [1] "Be"  "you"

# extract second word
word(change, 2)
#> [1] "the"  "want"

# extract last word
word(change, -1)
#> [1] "change" "be"

# extract all but the first words
word(change, 2, -1)
#> [1] "the change" "want to be"
```

`stringr` has more functions but we'll discuss them in the chapters about 
[regular expressions](#regex1).

<!--chapter:end:stringr-basics.Rmd-->


# Basic Manipulation Examples


## Introduction

This chapter provides more elaborated examples than the simple demos presented
so far. The idea is to show you less abstract scenarios and cases where you
could apply the functions and concepts covered so far.


### Example: Names of files

Imagine that you need to generate the names of 10 data `.csv` files. All the 
files have the same prefix name but each of them has a different number: 
`file1.csv`, `file2.csv`, ... , `file10.csv`. 

There are several ways in which you could generate a character vector with 
these names. One naive option is to manually type those names and form a
vector with `c()`


```r
c('file1.csv', 'file2.csv', 'file3.csv')
#> [1] "file1.csv" "file2.csv" "file3.csv"
```

But that's not very efficient. Just think about the time it would take you
to create a vector with 100 files. A better alternative is to use the
vectorized nature of `paste()`


```r
paste('file', 1:10, '.csv', sep = "")
#>  [1] "file1.csv"  "file2.csv"  "file3.csv"  "file4.csv"  "file5.csv" 
#>  [6] "file6.csv"  "file7.csv"  "file8.csv"  "file9.csv"  "file10.csv"
```

Or similarly with `paste0()`


```r
paste0('file', 1:10, '.csv')
#>  [1] "file1.csv"  "file2.csv"  "file3.csv"  "file4.csv"  "file5.csv" 
#>  [6] "file6.csv"  "file7.csv"  "file8.csv"  "file9.csv"  "file10.csv"
```


### Example: Valid Color Names

R comes with the function `colors()` that returns a vector with the names 
(in English) of 657 colors available in R. How would you write a function 
`is_color()` to test if a given name---in English---is a valid R color. 
If the provided name is a valid R color, `is_color()` should return `TRUE`. 
If the provided name is not a valid R color `is_color()` should return `FALSE`.


```r
is_color <- function(x) {
  x %in% colors()
}
```

Lets test it:


```r
is_color('yellow')  # TRUE
#> [1] TRUE

is_color('blu')     # FALSE
#> [1] FALSE

is_color('turkuiose') # FALSE
#> [1] FALSE
```

Another possible way to write `is_color()` is comparing if `any()` element
of `colors()` equals the provided name:


```r
is_color2 <- function(x) {
  any(colors() == x)
}
```

Test it:


```r
is_color2('yellow')  # TRUE
#> [1] TRUE

is_color2('blu')     # FALSE
#> [1] FALSE

is_color2('turkuiose') # FALSE
#> [1] FALSE
```


### Example: Me and You plot

This example is not really about data analysis or something serious, it is 
instead a fun project in which you get to apply what we have covered so far.
The idea is to produce a plot with some text on it. But not any kind of text.
The plot is intended to be a postcard---for Saint Valentine's day.
With this kind of tutorial, you should be able to make youw own plot, print it 
and give it to your significant other.

The idea is to make a chart with your name and the name of your significant 
other, adding a touch of randomness in the location of the text, the sizes, and
the colors.

First we generate the x-y coordinates. We'll use 100 points, and set the 
random seed to 333:


```r
# random seed
set.seed(333)

# x-y coordinates
n <- 100
x <- rnorm(n)
y <- rnorm(n, 1, 2)
```


The first step is to produce a very basic-raw plot (nothing fancy). We use 
`plot()` for this purpose:


```r
plot(x, y)
```

This just produces a scatter diagram with a 100 points on it. The following 
step consists of replacing the dots by some text: your name and the one of your 
significant other. To hide the dots, we set the parameter `type = "n"`, which 
means that we don't want anything to be plotted. To show the text, we use the 
low level plotting function `text()`. We use the same coordinates, but this 
time we specify the displayed `labels`:


```r
plot(x, y, type = "n")
text(x, y, labels = "me & you")
```

Again, this is a very preliminary plot; something basic that allows us to
start getting a feeling of how the chart looks like. The second step is to 
change the background color. One way to do this is by specifying the `bg` 
graphical parameter inside the `par()` function:


```r
# graphical parameters
op <- par(bg = "gray10")
# plot text
plot(x, y, type = "n")
text(x, y, 
     labels = "me & you",
     col = "white")
# reset default parameters
par(op)
```

<img src="_main_files/figure-html4/me-and-you2-1.png" width="70%" style="display: block; margin: auto;" />

`par()` has default settings. Everytime you call `par()` and change 
one of the associated parameters, the subsequent plots will be displayed with
those values. To set parameters in a temporary way, you can assign them to 
an object: i.e. `op`. After the plot is produced, we reset the default 
graphical parameters with the instruction `par(op)`.

We are getting closer to the desired look of the postcard. The final stage is 
to add some color to the text, and change their size. The size of the labels 
will also be random with a uniform distribution.

R provides several ways to specify colors. In this example we will use the
`hsv()` function (i.e. hue-saturation-value). This function requires three
parameters: hue (color), saturation, and value. Hues are specified with a range
from 0 to 1. We generate some random numbers in the interval 0.85 - 0.95 to get
some hues red, pink, fuchsia colors. `hsv()` also takes the optional 
parameters `alpha` to determined the alpha transparency.


```r
# text size
sizes <- runif(n, 0.5, 3)

# text color
hues <- runif(n, 0.85, 0.95)
alphas <- runif(n, 0.1, 1)


op <- par(bg = "gray10", mar = rep(0, 4))
plot(x, y, type = "n", axes = FALSE, 
     xlab = '', ylab = '')
text(x, y, 
     labels = "me & you", 
     font = 3, 
     col = hsv(hues, 1, 1, alphas),
     cex = sizes)
par(op)
```

<img src="_main_files/figure-html4/unnamed-chunk-59-1.png" width="70%" style="display: block; margin: auto;" />

To save the image, call `pdf()`. To give the image the dimensions of a 
standard postcard, you can specify `width = 5` and `height = 3.5`, that is,
5 inches wide and 3.5 inches tall (you can choose other dimensions if you want):


```r
pdf(file = "figure/me-and-you3.pdf", width = 5, height = 3.5)
op <- par(bg = "gray10", 
          mar = rep(0, 4))
plot(x, y, type = "n", axes = FALSE, 
     xlab = '', ylab = '')
text(x, y, 
     labels = "me & you", 
     font = 3, 
     col = hsv(hues, 1, 1, alphas),
     cex = sizes)
par(op)
dev.off()
```

If you save the image in png format, you could also use it as a wallpaper for your
computer:

![A wallpaper chart for your significant other](images/me-you-wallpaper.png)

<!--chapter:end:basic-examples.Rmd-->


# (PART) Regex {-}

# Regular Expressions {#regex1}

## Introduction

So far you have learned some basic and intermediate functions for handling and 
working with text in R. These are very useful functions and they allow you 
to do many interesting things. However, if you truly want to unleash the power 
of strings manipulation, you need to take things to the next level and learn 
about _regular expressions_.


## What are Regular Expressions?

The name "Regular Expression" does not say much. However, regular 
expressions are all about text. Think about how much text is all around 
you in our modern digital world: email, text messages, news articles, blogs, 
computer code, contacts in your address book---all these things are text. 
Regular expressions are a tool that allows us to work with these text by 
describing text patterns.

A __regular expression__ is a special text string for describing a certain 
amount of text. This "certain amount of text" receives the formal name of 
_pattern_. In other words, a regular expression is a set of symbols that 
describes a text pattern. More formally we say that a regular expression is a 
_pattern that describes a set of strings_. In addition to this first 
meaning, the term regular expression can also be used in a slightly different 
but related way: as the formal language of these symbols that needs 
to be interpreted by a regular expression processor.
Because the term "regular expression" is rather long, most people 
use the word __regex__ as a shortcut term. And you will even find the 
plural _regexes_.

It is also worth noting what regular expressions are not. They're not a 
programming language. They may look like some sort of programming language
because they are a formal language with a defined set of rules that gets a 
computer to do what we want it to do. However, there are no variables in regex
and you can't do computations like adding 1 + 1. 


### What are Regular Expressions used for?

We use regular expressions to work with text. Some of its common uses involve
testing if a phone number has the correct number of digits, if a date follows a 
specifc format (e.g. mm/dd/yy), if an email address is in a valid format, or if 
a password has numbers and special characters. You could also use regular 
expressions to search a document for _gray_ spelt either as "gray" or 
"grey". You could search a document and replace all occurrences of "Will", "Bill", 
or "W." with William. Or you could count the number of times in a document 
that the word "analysis" is immediately preceded by the words "data", 
"computer" or "statistical" only in those cases. You could use it to 
convert a comma-delimited file into a tab-delimited file or to find duplicate 
words in a text. 

In each of these cases, you are going to use a regular expression to write up a 
description of what you are looking for using symbols. In the case of a phone 
number, that pattern might be three digits followed by a dash, followed by three 
digits and another dash, followed by four digits. Once you have defined a 
pattern then the regex processor will use our description to return matching 
results, or in the case of the test, to return true or false for whether or not 
it matched.


### A word of caution about regex

If you have never used regular expressions before, their syntax may seem a bit
scary and cryptic. You will see strings formed by a bunch of letters, digits, 
and other punctuation symbols combined in seemingly nonsensical ways. As with
any other topic that has to do with programming and data analysis, learning
the principles of regex and becoming fluent in defining regex patterns takes
time and requires a lot of practice. The more you use them, the better you
will become at defining more complex patterns and getting the most out of them.

Regular Expressions is a wide topic and there are books entirely dedicated to
this subject. The material offered in this book is not extensive and there are
many subtopics that I don't cover here. Despite the initial barriers that you
may encounter when entering the regex world, the pain and frustration of 
learning this tool will payoff in your data science career.


### Regular Expressions in R

Tools for working with regular expressions can be found in virtually all 
scripting languages (e.g. Perl, Python, Java, Ruby, etc). R has some 
functions for working with regular expressions but it does not provide 
the wide range of capabilities that other scripting languages do. Nevertheless, 
they can take you very far with some workarounds (and a bit of patience).

One of the best tools you must have in your toolkit is the R package `"stringr"`
(by Hadley Wickham). It provides functions that have similar behavior to 
those of the base distribution in R. But it also provides many more facilities
for working with regular expressions.


## Regex Basics

The main purpose of working with regular expressions is to describe patterns 
that are used to match against text strings. Simply put, working with regular 
expressions is nothing more than __pattern matching__. The result of a match 
is either successful or not.

The simplest version of pattern matching is to search for one occurrence (or 
all occurrences) of some specific characters in a string. For example, we might 
want to search for the word `"programming"` in a large text document, or we 
might want to search for all occurrences of the string `"apply"` in a series 
of files containing R scripts.

Typically, regular expression patterns consist of a combination of alphanumeric 
characters as well as special characters. A regex pattern can be as simple as a 
single character, or it can be formed by several characters with a more complex 
structure. In all cases we construct regular expressions much in the same form 
in which we construct arithmetic expressions, by using various operators to 
combine smaller expressions. 


## Matching Literal Characters

We're going to start with the simplest match of all: a literal character.
A literal character match is one in which a given character such as the letter
`"R"` matches the letter _R_. This type of match is the most basic 
type of regular expression operation: just matching plain text.

The following examples are extremely basic but they will help you get a 
good understanding of regex.

Consider the following text stored in a character vector `this_book`:


```r
this_book <- 'This book is mine'
```

The first regular expression we are going to work with is `"book"`. 
This pattern is formed by a letter _b_, followed by a letter _o_, followed by 
another letter _o_, followed by a letter _k_. As you may guess, this pattern 
matches the word _book_ in the character vector `this_book`. 
To have a visual representation of the actual pattern that is matched, you
should use the function `str_view()` from the package `"stringr"` 
(you may need to upgrade to a recent version of RStudio):


```r
str_view(this_book, 'book')
```

As you can tell, the pattern `"book"` doesn't match the entire content in
the vector `this_book`; it just matches those four letters.

It may seem really simple but there are a couple of details to be highlighted.
The first is that regex searches are case sensitive by default. This means 
that the pattern `"Book"` would not match _book_ in ``this_book``.


```r
str_view("This Book is mine.", 'book')
```

You can change the matching task so that it is case insensitive but we will
talk about it later.

Let's add more text to `this_book`:


```r
this_book <- 'This book is mine. I wrote this book with bookdown.'
```

Let's use `str_view()` to see what pieces of text are matched in `this_book` 
with the pattern `"book"`:


```r
str_view(this_book, "book")
```

As you can tell, only the first occurrence of _book_ was matched. This is
a common behavior of regular expressions in which they return a match as fast
possible. You can think of this behavior as the "eager principle", that is,
regular expressions are eager and they will give preference to an early match.
This is a minor but important detail and we will come back to this behavior of 
regular expressions.

All the letters and digits in the English alphabet are considered literal 
characters. They are called _literal_ because they match themselves.


```r
str_view <- c("I had 3 quesadillas for lunch", "3")
```

Here is another example:


```r
transport <- c("car", "bike", "boat", "airplane")
```

The first pattern to test is the letter `"a"`:


```r
str_view(transport, "a")
```

When you execute the previous command, you should be able to see that the 
letter `"a"` is highlighted in the words _car_, _boat_ and _airplane_.



## Metacharacters

The next topic that you should learn about regular expressions has to do with 
__metacharacters__. As you just learned, the most basic type of regular 
expressions are the literal characters which are characters that match 
themselves. However, not all characters match themselves. Any character that 
is not a literal character is a metacharacter. This type of characters have a 
special meaning and they allow you to transform literal characters in very 
powerful ways.

Below is the list of metacharacters in _Extended Regular Expressions_ (EREs):

```
.   \   |   (   )   [   ]   {   }   $   -    ^   *   +   ?
```

- the dot `.`
- the backslash `\`
- the bar `|`
- left or opening parenthesis `(`
- right or closing parenthesis `)`
- left or opening bracket `[`
- right or closing bracket `]`
- left or opening brace `{`
- right or closing brace `}`
- the dollar sign `$`
- the dash, hyphen or minus sign `-`
- the caret or hat `^`
- the star or asterisk `*`
- the plus sign `+`
- the question mark `?`

We're going to be working with these characters throughout the rest of the book. 
Simply put, everything else that you need to know about regular expressions 
besides literal characters is how these metacharacters work. The good news is 
that there are only a few metacharacters to learn. The bad news is 
that some metacharacters can have more than one meaning. And learning those 
meanings definitely takes time and requires hours of practice. The meaning of 
the metacharacters greatly depend on the context in which you use them,
how you use them, and where you use them. If it wasn't enough complication, 
it is also the metacharacters that have variation between the different 
regex engines. 
 


### The Wild Metacharacter

The first metacharacter you should learn about is the dot or period `"."`, 
better known as the __wild__ metacharacter. This metacharacter is used to
match __ANY__ character except for a new line.

For example, consider the pattern `"p.n"`, that is, _p wildcard n_. This
pattern will match _pan_, _pen_, and _pin_, but it will not match _prun_ 
or _plan_. The dot only matches one single character. 

Let's see another example using the vector `c("not", "note", "knot", "nut")` 
and the pattern `"n.t"`


```r
not <- c("not", "note", "knot", "nut")

str_view(not, "n.t")
```

the pattern `"n.t"` matches _not_ in the first three elements, and _nut_
in the last element.

If you specify a pattern `"no."`, then just the first three elements
in `not` will be matched. 


```r
str_view(not, "no.")
```

And if you define a pattern `"kn."`, then only the third element is matched.


```r
str_view(not, "kn.")
```

The wild metacharacter is probably the most used metacharacter, and it is 
also the most abused one, being the source of many mistakes. Here is a basic
example with the regular expression formed by `"5.00"`. If you think that this 
pattern will match five with two decimal places after it, you will be 
surprised to find out that it not only matches _5.00_ but also _5100_ and _5-00_. 
Why? Because `"."` is the metacharacter that matches absolutely anything.
You will learn how to fix this mistake in the next section, but it illustrates 
an important fact about regular expressions: the challenge consists of matching 
what you want, but also in matching only what you want. You don't want to 
specify a pattern that is overly permissive. You want to find the thing you're 
looking for, but only that thing. 


### Escaping metacharacters

What if you just want to match the character dot? For example, say you 
have the following vector:


```r
fives <- c("5.00", "5100", "5-00", "5 00")
```

If you try the pattern `"5.00"`, it will match all of the elements in `fives`.


```r
str_view(fives, "5.00")
```

To actually match the dot character, what you need to do is __escape__ the
metacharacter. In most languages, the way to escape a metacharacter is by 
adding a backslash character in front of the metacharacter: `"\."`. 
When you use a backslash in front of a metacharacter you are "escaping" the
character, this means that the character no longer has a special meaning, 
and it will match itself.

However, R is a bit different. Instead of using a backslash you have to use
two backslashes: `"5\\.00"`. This is because the backslash `"\"`, which is
another metacharacter, has a special meaning in R. Therefore, to match just
the element _5.00_ in `fives` in R, you do it like so:


```r
str_view(fives, "5\\.00")
```

<!--chapter:end:regex1.Rmd-->


# Character Sets

In this chapter we will talk about character sets. You will learn about 
a couple of more metacharacters, the opening and closing brackets `[ ]`, that 
will help you define a character set.

These square brackets indicate a character set which will match any one of 
the various characters that are inside the set. Keep in mind that a character 
set will match only one character. The order of the characters inside the set 
does not matter; what matter is just the presence of the characters inside the
brackets. So for example if you have a set defined by `"[AEIOU]"`, that will 
match any one upper case vowel. 


## Defining character sets

Consider the following pattern that includes a character set: `"p[aeiou]n"`, 
and a vector with the words _pan_, _pen_, and _pin_:


```r
pns <- c('pan', 'pen', 'pin', 'pon', 'pun')

str_view(pns, "p[aeiou]n")
```

The set `"p[aeiou]n"` matches all elements in `pns`. Now let's use the same 
set with another vector `pnx`:


```r
pnx <- c('pan', 'pen', 'pin', 'p0n', 'p.n', 'p1n', 'paun')

str_view(pnx, "p[aeiou]n")
```

As you can tell, this time only the first three elements in `pnx` are matched.
Notice also that _paun_ is not matched. This is because the character set
matches only one character, either _a_ or _u_ but not _au_.

If you are interested in matching all capital letters in English, 
you can define a set formed as:

```
[ABCDEFGHIJKLMNOPQRSTUVWXYZ]
```

Likewise, you can define a set with only lower case letters in English:

```
[abcdefghijklmnopqrstuvwxyz]
```

If you are interested in matching any digit, you can also specify a character
set like this:

```
[0123456789]
```



## Character ranges

The previous examples that show character sets containing all the capital 
letters or all lower case letters are very convenient but require a lot of 
typing. __Character ranges__ are going to help you solve that problem, by 
giving you a convenient shortcut based on the dash metacharacter `"-"` to 
indicate a range of characters. A character range consists of a character set
with two characters separated by a dash or minus `"-"` sign.

Let's see how you can reexpress the examples in the previous section as
character ranges. The set of all digits can be expressed as a character range
using the following pattern:

```
[0-9]
```

Likewise, the set of all lower case letters _abcd...xyz_ is compactly 
represented with the character range:

```
[a-z]
```

And the character set of all upper case letters _ABD...XYZ_ is formed by

```
[A-Z]
```

Note that the dash is only a metacharacter when it is inside a character set; 
outside the character set it is just a literal dash.

So how do you use character range? To illustrate the concept of character 
ranges let's create a `basic` vector with some simple strings, and see 
what the different ranges match:


```r
basic <- c('1', 'a', 'A', '&', '-', '^')
```


```r
# digits
str_view(basic, '[0-9]')
```


```r
# lower case letters
str_view(basic, '[a-z]')
```


```r
# upper case letters
str_view(basic, '[A-Z]')
```

Now consider the following vector `triplets`:


```r
triplets <- c('123', 'abc', 'ABC', ':-)')
```

You can use a series of character ranges to match various occurrences of
a certain type of character. For example, to match three consecutive digits
you can define a pattern `"[0-9][0-9][0-9]"`; to match three consecutive
lower case letters you can use the pattern `"[a-z][a-z][a-z]"`; and the
same idea applies to a pattern that matches three consecutive upper case
letters `"[A-Z][A-Z][A-Z]"`. 


```r
str_view(triplets, '[0-9][0-9][0-9]')

str_view(triplets, '[A-Z][A-Z][A-Z]')
```

Observe that the element `":-)"` is not matched by any of the character ranges
that we have seen so far.

Character ranges can be defined in multiple ways. For example, the range 
`"[1-3]"` indicates any one digit 1, 2, or 3. Another range may be defined
as `"[5-9]"` comprising any one digit 5, 6, 7, 8 or 9. The same idea applies
to letters. You can define shorter ranges other than `"[a-z]"`. One example
is `"[a-d]"` which consists of any one lettere _a_, _b_, _c_, and _d_.


## Negative Character Sets

A common situation when working with regular expressions consists of matching
characters that are NOT part of a certain set. This type of matching can be
done using a negative character set: by matching any one character that is not
in the set. To define this type of sets you are going to use the metacharacter
caret `"^"`. If you are using a QWERTY keyboard, the caret symbol should be
located over the key with the number 6.

The caret `"^"` is one of those metacharacters that have more than one meaning
depending on where it appears in a pattern. If you use a caret in the first
position inside a character set, e.g. `[^aeiou]`, it means _negation_. In 
other words, the caret in `[^aeiou]` means "not any one of lower case vowels."

Let's use the `basic` vector previously defined:


```r
basic <- c('1', 'a', 'A', '&', '-', '^')
```

To match those elements that are NOT upper case letters, you define a negative
character range `"[^A-Z]"`:


```r
str_view(basic, '[^A-Z]')
```

It is important that the caret is the first character inside the character 
set, otherwise the set is not a negative one:


```r
str_view(basic, '[A-Z^]')
```

In the example above, the pattern `"[A-Z^]"` means "any one upper case letter 
or the caret character." Which is completely different from the negative set 
`"[^A-Z]"` that negates any one upper case letter.

If you want to match any character except the caret, then you need to use a
character set with two carets: `"[^^]"`. The first caret works as a negative 
operator, the second caret is the caret character itself:


```r
str_view(basic, '[^^]')
```


## Metacharacters inside character sets

Now that you know what character sets are, how to define character ranges, 
and how to specify negative character sets, we need to talk about what 
happens when including metacharacters inside character sets.

Except for the caret in the first position of the character set, any other 
metacharacter inside a character set is already escaped. This implies that
you do not need to escape them using backslashes.

To illustrate the use of metacharacters inside character sets, let's use 
the `pnx` vector:


```r
pnx <- c('pan', 'pen', 'pin', 'p0n', 'p.n', 'p1n', 'paun')
```

The character set formed by `"p[ae.io]n"` includes the dot character. Remember
that, in general, the period is the wildcard metacharacter and it matches 
any type of character. However, the period in this example is inside a 
character set, and because of that, it loses its wildcard behavior.


```r
str_view(pnx, "p[ae.io]n")
```

As you can tell, `"p[ae.io]n"` matches _pan_, _pen_, _pin_ and _p.n_, 
but not _p0n_ or _p1n_ because the dot is the literal dot, not a wildcard 
character anymore.

Not all metacharacters become literal characters when they appear inside a
character set. The exceptions are the closing bracket `]`, the dash `-`,
the caret `^`, and the backslash `\`.

The closing bracket `]` is used to enclose the character set. Thus, if you
want to use a literal right bracket inside a character set you must escape it:
`[aei\\[ou]`. Remember that in R you use double backslash for escaping
purposes. This is also why the backslash `\`, or double backslash in R, 
does not become a literal character. 

Another interesting case has to do with the dash or hyphen `-` character. As 
you know, the dash inside a character set is used to define a range of 
characters: e.g. `[0-9]`, `[x-z]`, and `[K-P]`. As a general rule, if you
want to include a literal dash as part of a range, you should escape it:
`"[a-z\\-]"`. 

Let's modify the `basic` vector by adding an opening and ending brackets:


```r
basic <- c('1', 'a', 'A', '&', '-', '^', '[', ']')
```

How do you match each of the characters that have a special meaning inside a 
character set?


```r
# matching a literal caret
str_view(basic, "[a\\^]")
```


```r
# matching a literal dash
str_view(basic, "[a\\-]")
```


```r
# matching a literal opening bracket
str_view(basic, "[a\\[]")
```


```r
# matching a literal closing bracket
str_view(basic, "[a\\]]")
```

## Character Classes

Closely related with character sets and character ranges, regular expressions
provide another useful construct called __character classes__ which, as their
name indicates, are used to match a certain class of characters. The most
common character classes in most regex engines are:

| Character | Matches                                     | Same as         |
|:----------|:--------------------------------------------|:----------------|
| `\\d`     | any digit                                   | `[0-9]`         |
| `\\D`     | any nondigit                                | `[^0-9]`        |
| `\\w`     | any character considered part of a word     | `[a-zA-Z0-9_]`  |
| `\\W`     | any character not considered part of a word | `[^a-zA-Z0-9_]` |
| `\\s`     | any whitespace character                    | `[\f\n\r\t\v]`  |
| `\\S`     | any nonwhitespace character                 | `[^\f\n\r\t\v]` |


You can think of character classes as another type of metacharacters, or as 
shortcuts for special character sets. 

The following table shows the characters that represent whitespaces:

| Character | Description     |
|:----------|:----------------|
| `\f`      | form feed       |
| `\n`      | line feed       |
| `\r`      | carriage return |
| `\t`      | tab             |
| `\v`      | vertical tab    |

Sometimes you have to deal with nonprinting whitespace characters. In these
situations you probably will end up using the whitespace character class `\\s`.
A common example is when you have to match tab characters, or line breaks. 

The operating system Windows uses `\r\n` as an end-of-line marker. In contrast,
Unix-like operating systems (including Mac OS) use `\n`.

Tab characters `\t` are commonly used as a field-separator for data files. But 
most text editors render them as whitespaces.



## POSIX Character Classes

We finish this chapter with the introduction of another type of character
classes known as __POSIX character classes__. These are yet another class
construct that is supported by the regex engine in R.

| Class        | Description                | Same as         |
|:-------------|:---------------------------|:----------------|
| `[:alnum:]`  | any letter or digit        | `[a-zA-Z0-9]`   |
| `[:alpha:]`  | any letter                 | `[a-zA-Z]`      |
| `[:digit:]`  | any digit                  | `[0-9]`         |
| `[:lower:]`  | any lower case letter      | `[a-z]`         |
| `[:upper:]`  | any upper case letter      | `[A-Z]`         |
| `[:space:]`  | any whitespace inluding space | `[\f\n\r\t\v ]` | 
| `[:punct:]`  | any punctuation symbol     |                 |
| `[:print:]`  | any printable character    |                 |
| `[:graph:]`  | any printable character excluding space |    |
| `[:xdigit:]` | any hexadecimal digit      | `[a-fA-F0-9]`   |
| `[:cntrl:]`  | ASCII control characters   |                 |


Notice that a POSIX character class is formed by an opening bracket `[`, 
followed by a colon `:`, followed by some keyword, followed by another 
colon `:`, and finally a closing bracket `]`.

In order to use them in R, you have to wrap a POSIX class inside a regex
character class. That is, you have to surround a POSIX class with brackets.

Once again, refer to the `pnx` vector to illustrate the use of POSIX classes:


```r
pnx <- c('pan', 'pen', 'pin', 'p0n', 'p.n', 'p1n', 'paun')
```

Let's start with the `[:alpha:]` class, and see what does it match in `pnx`:


```r
str_view(pnx, "[[:alpha:]]")
```

Now let's test it with `[:digit:]`


```r
str_view(pnx, "[[:digit:]]")
```


<!--chapter:end:character-sets.Rmd-->

