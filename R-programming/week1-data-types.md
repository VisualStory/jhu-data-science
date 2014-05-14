Week 1: Data Types
======

### Contents

* Data Types
  * [atomic classes](#classes): numeric, logical, character, integer, complex
  * [vectors](#vectors), [lists](#lists)
  * [factors](#factors)
  * [missing values](#missing-values)
  * [data frames](#data-frames)
  * [names](#names)

### Classes

* Five basic classes of objects:
  * character
  * numeric (real numbers) = Double
  * integer = Int
  * complex
  * logical (True/False) = Boolean

* Two basic object
  * vector: contain objects of the same class
  * list: contain objects of difference classes

* Numbers (numeric)
   * integer with `L` suffix
   * `Inf` represent infinity: `1 / 0` is `Inf`, `1 / Inf` is 0
   * `NaN` represents undefined value: `0 / 0` is `NaN`

* Attributes
  * names, dimnames
  * dimansions: matrices, arrays
  * class
  * length
  * other user-defined attributes/metadata
  * can be accessed using `attribute()`

* Entering Input


```r
msg <- "hello"  ## assignment
```


* Evaluation


```r
x <- 5  ## nothing printed
x  ## auto-printing occurs
```

```
## [1] 5
```

```r
print(x)  ## explicit printing
```

```
## [1] 5
```


* Printing


```r
x <- 1:10  ## the : operator is used to create integer sequences
x
```

```
##  [1]  1  2  3  4  5  6  7  8  9 10
```


### Vectors

* Creating Vectors of objects using the `c()` (stands for concatenate) function


```r
x <- c(0.5, 0.6)  ## numeric
x <- c(TRUE, FALSE)  ## logical
x <- c(T, F)  ## logical
x <- c("a", "b", "c")  ## character
x <- 0:10  ## integer
x <- c(1 + (0+0i), 2 + (0+4i))  ## complex
```


* Creating Vectors of objects using the `vector()` function with class defined as first parameter and length as second parameter


```r
x <- vector("numeric", length = 10)
x
```

```
##  [1] 0 0 0 0 0 0 0 0 0 0
```


* Mixing Objects: coercion happens to change less common object to more common object


```r
y <- c(1.7, "a")  ## character
y <- c(TRUE, 2)  ## numeric
y <- c("a", TRUE)  ## character
```


* Explicit Coercion by using `as.*`


```r
x <- 0:6
class(x)
```

```
## [1] "integer"
```

```r
as.numeric(x)
```

```
## [1] 0 1 2 3 4 5 6
```

```r
as.logical(x)
```

```
## [1] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
```

```r
as.character(x)
```

```
## [1] "0" "1" "2" "3" "4" "5" "6"
```


* Explicit Coercion with nonsensical coercion


```r
x <- c("a", "b", "c")
as.numeric(x)  ## get warning
```

```
## Warning: NAs introduced by coercion
```

```
## [1] NA NA NA
```

```r
as.logical(x)
```

```
## [1] NA NA NA
```

```r
as.complex(x)
```

```
## Warning: NAs introduced by coercion
```

```
## [1] NA NA NA
```


### Matrices

* Matrices: vectors with a _dimension_ attribute. The _dimension_ attribute is itself an integer vector of length 2 `(nrow, ncol)`


```r
m <- matrix(nrow = 2, ncol = 3)
m
```

```
##      [,1] [,2] [,3]
## [1,]   NA   NA   NA
## [2,]   NA   NA   NA
```

```r
dim(m)
```

```
## [1] 2 3
```

```r
attributes(m)
```

```
## $dim
## [1] 2 3
```


* Matrices are constructed _column-wise_, so entries can be though of starting in the upper-left corner and running down the columns


```r
m <- matrix(1:6, nrow = 2, ncol = 3)
m
```

```
##      [,1] [,2] [,3]
## [1,]    1    3    5
## [2,]    2    4    6
```


* Matrices can be created directly from vectors by adding a dimension attribute


```r
m <- 1:10
m
```

```
##  [1]  1  2  3  4  5  6  7  8  9 10
```

```r
dim(m) <- c(2, 5)
m
```

```
##      [,1] [,2] [,3] [,4] [,5]
## [1,]    1    3    5    7    9
## [2,]    2    4    6    8   10
```


* Matrices can be created by _column-binding_ or _row-binding_ with `cbind()` and `rbind()`


```r
x <- 1:3
y <- 10:12
cbind(x, y)
```

```
##      x  y
## [1,] 1 10
## [2,] 2 11
## [3,] 3 12
```

```r
rbind(x, y)
```

```
##   [,1] [,2] [,3]
## x    1    2    3
## y   10   11   12
```


### Lists

* Lists are a special type of vectors that can contain elements of different classes


```r
x <- list(1, "a", TRUE, 1 + (0+4i))
x  ## with double brackets
```

```
## [[1]]
## [1] 1
## 
## [[2]]
## [1] "a"
## 
## [[3]]
## [1] TRUE
## 
## [[4]]
## [1] 1+4i
```


### Factors

* Factors are used to represent categorical data, can be ordered or unordered. 
  * Factors are treated specially by modelling function like `lm()` and `glm()`
  * Using factors with labels is better than using integers becuase factors are self-describing; having a variable that has values "Male" and "Female" is better than a variable that has values 1 and 2
  

```r
x <- factor(c("yes", "yes", "no", "yes", "no"))
x
```

```
## [1] yes yes no  yes no 
## Levels: no yes
```

```r
table(x)
```

```
## x
##  no yes 
##   2   3
```

```r
unclass(x)
```

```
## [1] 2 2 1 2 1
## attr(,"levels")
## [1] "no"  "yes"
```


* Factors can set the order of levels using `levels` argument to `factor()`.


```r
x <- factor(c("yes", "yes", "no", "yes", "no"), levels = c("yes", "no"))
x
```

```
## [1] yes yes no  yes no 
## Levels: yes no
```


### Missing Values

* Missing Values are denoted by NA or NaN (mathematical operations) for underfined mathematical operations.
  * `is.na()` is used to test objects if they are `NA`
  * `is.nan()` is used to test for `NaN`
  * `NA` values have a class, so there are integer NA, character NA, etc.
  * A `NaN` value is also `NA` but the converse is not true


```r
x <- c(1, 2, NA, 10, 3)
is.na(x)
```

```
## [1] FALSE FALSE  TRUE FALSE FALSE
```

```r
is.nan(x)
```

```
## [1] FALSE FALSE FALSE FALSE FALSE
```

```r
x <- c(1, 2, NaN, NA, 4)
is.na(x)
```

```
## [1] FALSE FALSE  TRUE  TRUE FALSE
```

```r
is.nan(x)
```

```
## [1] FALSE FALSE  TRUE FALSE FALSE
```


### Data Frames

* Data Frames are used to store tabular data
  * They are represented as a special type of list where every element of the list has to have the same length
  * Each element of the list can be thought of as a column and the length of each element of the list is the number of rows
  * Unlike matrices, data frames can store different class of objects in each column (just like lists), matrices must have every element be the same class
  * Data frames also have a special attribute called row.names
  * Data frames are usually created by calling `read.table()` or `read.csv()`
  * Can be converted to a matrix by calling `data.matrix()`


```r
x <- data.frame(foo = 1:4, bar = c(T, T, F, F))
x
```

```
##   foo   bar
## 1   1  TRUE
## 2   2  TRUE
## 3   3 FALSE
## 4   4 FALSE
```

```r
nrow(x)
```

```
## [1] 4
```

```r
ncol(x)
```

```
## [1] 2
```


### Names

* Names are for R objects, which is very useful for writing reable code and self-describing objects


```r
x <- 1:3
names(x)
```

```
## NULL
```

```r
names(x) <- c("foo", "bar", "norf")
x
```

```
##  foo  bar norf 
##    1    2    3
```

```r
names(x)
```

```
## [1] "foo"  "bar"  "norf"
```


* Names for lists


```r
x <- list(a = 1, b = 2, c = 3)
x
```

```
## $a
## [1] 1
## 
## $b
## [1] 2
## 
## $c
## [1] 3
```


* Names for matrices


```r
m <- matrix(1:4, nrow = 2, ncol = 2)
dimnames(m) <- list(c("a", "b"), c("c", "d"))
```

