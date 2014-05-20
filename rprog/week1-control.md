Control Structures
==================

- `if` and `else`
- `for`
- `while`
- `repeat`
- `break`
- `next`
- `return`

#### `if` and `else`

```
if(<condition1>) {
  ## do something
} else if(<condition2) {
  ## do something different
} else {
  ## do something else
}
```

#### `for`

```
for (i in 1:4) {
  print(i)
}
```

```
x <- c("a", "b", "c", "d")
for (i in 1:4) {
  print(x[i])
}
for(i in seq_along(x)) {
  print(x[i])
}
for (letter in x) {
  print(letter)
}
for (i in 1:4) print(x[i])
```

#### nested for loops

```
x <- matrix(1:6, 2, 3)
for (i in seq_len(nrow(x))) {
  for (j in seq_len(ncol(x))) {
    print(x[i, j])
  }
}
```

#### while

```
count <- 0
while (count < 4) {
  print(count)
  count <- count + 1
}
```

> be careful of inifinite loops!

#### repeat

```
x0 <- 1
tol <- 1e-8
repeat {
  x1 <- computeEstimate()
  if(abs(x1 - x0) < tol) {
    break
  } else {
    x0 <- x1
  }
}
```

> common in optimization equations, no garantee to stop if not converge. Better use a `for` loop to set a hard limit on the number of iterations

#### `next` and `return`

```
for (i in 1:100) {
  if (i <= 20) {
    ## skip the first 20 iterations
    next
  }
  ## do something here
}
```
