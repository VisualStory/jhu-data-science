Subsetting
==========

- `[`: returns an object of the same class, can be used to select more than one element
- `[[`: used to extract elements of a list or a data frame; it can only be used to extrat a single element and the class of the returned object will not necessarily be a list or data frame
- `$`: used to extract elemetns of a list or data frame by name; semantics are similar to that of `[[`


```r
x <- c("a", "b", "c", "d")
x[1]
```

```
## [1] "a"
```

```r
x[1:4]
```

```
## [1] "a" "b" "c" "d"
```

```r
x[x > "a"]
```

```
## [1] "b" "c" "d"
```

```r
u <- x > "a"
u
```

```
## [1] FALSE  TRUE  TRUE  TRUE
```

```r
x[u]  # select elments that are larger than 'a'
```

```
## [1] "b" "c" "d"
```


#### subsetting a matrix


```r
x <- matrix(1:6, 2, 3)
x[1, 2]  # returns a vector of length 1 rather than a 1x1 matrix
```

```
## [1] 3
```

```r
x[1, 2, drop = FALSE]  # returns a 1x1 matrix
```

```
##      [,1]
## [1,]    3
```

```r

x[, 2]  # omit indices
```

```
## [1] 3 4
```

```r
x[1, ]  # returns a vector
```

```
## [1] 1 3 5
```

```r
x[1, , drop = FALSE]  # returns a matrix
```

```
##      [,1] [,2] [,3]
## [1,]    1    3    5
```


- `drop=FALSE`: returns a matrix rather than a vector

#### subsetting a list


```r
x <- list(foo = 1:4, bar = 0.6)
x[1]  # returns a list containing the sequence
```

```
## $foo
## [1] 1 2 3 4
```

```r
x[[1]]  # returns a sequence
```

```
## [1] 1 2 3 4
```

```r
x$bar  # returns a single value of 'bar'
```

```
## [1] 0.6
```

```r
x[["bar"]]  # same to x$bar
```

```
## [1] 0.6
```

```r
x["bar"]  # return a list with 'bar'
```

```
## $bar
## [1] 0.6
```


- The `[[` operator can be used with computed indices; `$` can only be used with liter names


```r
x <- list(foo = 1:4, bar = 0.6, baz = "hello")
name <- "foo"
x[[name]]  # computed index for 'foo'
```

```
## [1] 1 2 3 4
```

```r
x$name  # element 'name' does not exist
```

```
## NULL
```


- The `[[` can take an integer sequence


```r
x <- list(a = list(10, 12, 14), b = c(3.14, 2.81))
x[[c(1, 3)]]
```

```
## [1] 14
```

```r
x[[1]][[3]]
```

```
## [1] 14
```

```r
x[[c(2, 1)]]  # same as x[[2]][[1]]
```

```
## [1] 3.14
```


#### partial matching


```r
x <- list(aardvark = 1:5)
x$a
```

```
## [1] 1 2 3 4 5
```

```r
x[["a"]]
```

```
## NULL
```

```r
x[["a", exact = FALSE]]  # same as x$a
```

```
## [1] 1 2 3 4 5
```


#### removing `NA` values


```r
x <- c(1, 2, NA, 4, NA, 5)
bad <- is.na(x)  # tell which elements are NA
x[!bad]  #
```

```
## [1] 1 2 4 5
```



```r
x <- c(1, 2, NA, 4, NA, 5)
y <- c("a", "b", NA, "d", NA, NA)
good <- complete.cases(x, y)
good
```

```
## [1]  TRUE  TRUE FALSE  TRUE FALSE FALSE
```

```r
x[good]
```

```
## [1] 1 2 4
```

```r
y[good]
```

```
## [1] "a" "b" "d"
```

