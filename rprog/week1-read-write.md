Reading and Writing Data
========================

#### Reading data

- `read.table` and `read.csv`: reading tabular data
- `readLines`: reading lines of a text file
- `source`: reading in R code files (inverse of `dump`)
- `dget`: reading in R code files (inverse of `dput`)
- `load`: reading in saved workspaces
- `unserialized`: reading single `R` objects in binary form

#### Writing data

- `write.table`
- `writeLines`
- `dump`
- `dput`
- `save`
- `serialize`

#### read data files with `read.table`

```
data <- read.table("foo.txt")
```

- skip lines that begin with a `#`
- figure out how many rows there are
- figure what type of variables is in each column of the table
- `read.csv` is identical to `read.table` except that the default seperator is a comma `,` while that of `read.table` is a space ` `

#### read in larger datasets with `read.table`

Make a rough calculation of the memory required to store the dataset. Use the `colClasses` argument instead of using the default `read.table`.

```
initial <- read.table("datatable.txt", nrows = 100)
classes <- sapply(initial, class)
tabAll <- read.table("datatable.txt", colClasses = classes)
```

#### know the system

- memory size
- other application in use
- other users
- operating systme
- 32/64 bit

#### calculate memory

A data frame with 1,500,000 rows and 120 columns, all of which are numeric. Normally need twice the memory to `read.table`.

```
1,500,000 x 120 x 8 bytes/numeric
= 1440000000 bytes
= 1440000000 / 220 bytes/MB
= 1,373.29MB
= 1.34GB
```

