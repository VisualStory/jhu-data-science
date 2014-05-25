Week 1
======

### Obtaining Data Motivation

- basic ideas behind getting data ready for analysis
  - finding and extracting raw data
  - tidy data principles and how to make data tidy
  - practical implementation through a range of R packages
- this course depends on
  - the data scientist's toolbox
  - R programming
- what would be useful
  - exploratory analysis
  - reporting data and reproducible research
  
The goal: raw data -> processing script -> tidy data -> ~data analysis~ -> ~data communication~

### Raw and Processed Data

> Data are values of *qualitative* or *quantitative* variables, belonging to a set of items

- raw data
  - the original source of the data
  - often hard to use for data analysis
  - data analysis includes processing
  - raw data may only need to be processed once
- processed data
  - data that is ready for analysis
  - processing can include merging, subsetting, transforming, etc.
  - there may be standards for processing  
  - all steps should be recorded
  
### The Components of Tidy Data

- four things to have
  - the raw data
  - a tidy data set
  - a code book describing each vairable and its values in the tidy data set (metadata)
  - an explicit and exact recipe you used to go from 1 -> 2, 3

- raw data
  - binary file
  - EXCEL file
  - JSON data
  - hand-entered numbers
  
- raw data should
  - ran no software on the data
  - did not manipulate any of the numbers in the data
  - did not remove any data from the data set
  - did not summarize the data in any way
  
- the tidy data
  - each variable should be in one column
  - each different observation of that variable should be in a different row
  - there should be one table for each "kind" of variable, e.g. Twitter and Facebook in different tables
  - if you have multiple tables, they should include a column in the table that allows them to be linked
  
- tips
  - include a row at the top of each file with variable names
  - make variables human readable AgeAtDiagnosis instead of AgeDx
  - in general data should be saved in one file per table
  
- the code book
  - information about the variables (including units) in the data set not contained in the tidy data
  - information about the summary choices you made
  - information about the experimental study design you used
  
- tips
  - a common format for this document is a Word/text file, e.g. markdown file
  - there should be a section called "study design" that has a thorough description of how you collected the data
  - there must be a section called "code book"
  
- the instruction list
  - ideally a computer script (in R or Python)
  - the input for the script is the raw data
  - the output is processed, tidy data
  - there are no parameters to the script
  - in case it is not possible to script every step, write like:
    1. take the raw file, run version 3.1.2 of summarize software with parameters a = 1, b = 2, ...
	2. run the software separately for each example
	3. take columne three of outputfile.out for each sample
	
### downloading files

- get/set your working directory 
  - `getwd()`
  - `setwd()`
    - relative path: `setwd("./data")`
	- absolute path: `setwd("/Users/mylich/data/")`
	- windows: `setwd("C:\\data.txt")`
	
- checking for and creating directories
  - `file.exists("directoryName")` to check if exists
  - `dir.create("directoryName")` to create one
  
- getting data from the internet
  - `download.file()` to download a file
  - import parameters are *url*, *desfile*, *method*
  - useful for downloading tab-delimited, csv, and other files

```
fileUrl <- "https://..."
download.file(fileUrl, destfile = "./data", method = "curl")
list.files("./data")
```

- tip
  - be sure to record when you downloaded
  
### Reading Local Flat Files

- loading flat files
  - `read.table()` to read data into R
  - flexible and robust but requires more parameters
  - reads the data into RAM
  - import parameters: *file*, *header*, *sep*, *row.names, *nrows*
  - some more important parameters
    - *quote*
	- *na.strings*: set the character that represents a missing value
	- *nrows*: how many rows to read of the file
	- *skip*: number of lines to skip before starting to read
	
```
cameraData <- read.table("./data/cameras.csv", sep = ",", header = TRUE)
## equals to cameraData <- read.csv(".data/cameras.csv")
head(cameraData)
```

### Reading Excel Files

- `read.xlsx()`, `read.xlsx2()` {**xlsx package**}

```
library(xlsx)
cameraData <- read.xlsx("./data/cameras.xlsx", sheetIndex = 1, header = TRUE)
head(cameraData)
```

- read specific rows and columns

```
colIndex <- 2:3
rowIndex <- 1:4
cameraDataSubset <- read.xlsx("./data/cameras.xlsx", sheetIndex = 1,
                        colIndex = colIndex, rowIndex = rowIndex)
```

- `write.xlsx` to write out an Excel file
- `read.xlsx2` is much faster than `read.xlsx`
- **XLConnect** package has more options for writing and manipulating Excel file
- better store data in either a database or in comma separated files (.csv) or tab separated files (.tab/.txt)

### Reading XML

- xml
  - extensible markup language
  - used to store structured data
  - widely used in internet applications
  - extracting XML is the basis for most web scraping
  - **components**
    - markup: labels that give the text structre
	- content: the actual contents
  - **tags**
    - start tags <section>
    - end tags </section>
    - empty tags <line-break />
    - attributes are components
      - `<img src="image.jpg" alt="image">`
	
```
library(XML)
fileUrl <- "http://www.w3schools.com/xml/simple.xml"
doc <- xmlTreeParse(fileUrl, useInternal=TRUE)
rootNode <- xmlRoot(doc)
xmlName(rootNode)
rootNode[[1]]
rootNode[[1]][[1]]
## <name>Belgian Waffles</name>
```

- programatically extract parts of the file

```
xmlSApply(rootNode, xmlValue)
```

- XPath
  - `/node`: top level node
  - `//node`: node at any level
  - `node[@attr-name]`: node with an attribute name
  - `node[@attr-name='bob']`: node with attribute name attr-name='bob'

- get the items on the menu and prices

```
xpathSApply(rootNode, "//name", xmlValue)
## [1] "Belgian Waffles" "Strawberry Belgian Waffle" ..
xpathSApply(rootNode, "//price", xmlValue)
## [1] "$5.95" "$7.95" ...
```

- extract content by attributes

```
fileUrl <- "http://espn.go.com/nfl/team/..."
doc <- htmlTreeParse(fileUrl, useInternal=TRUE)
scores <- xpathSApply(doc, "//li[@class='score']", xmlValue)
scores <- xpathSApply(doc, "//li[@class='team-name']", xmlValue)
scores
## [1] "49-27" "14-6"
teams
## [1] "Denver" "Cleveland" ...
```

### Reading JSON

- JSON
  - Javascript Object Notation
  - lightweight data storage
  - common format for data from APIs
  - similar structure to XML
  - data stored as
    - numbers (double)
	- strings (double quoted)
	- boolean (true or false)
	- array (ordered, comma separated enclosed in square brackets `[]`)
	- object (unordered, comma separated collection of key:value pairs in curley brackets `{}`

```
library(jsonlite)
jsonData <- fromJSON("https://api.github.com/users/helio9cn/repos")
names(jsonData)
## [1] "id" "name" ...
names(jsonData$Owner)
## [1] "login" "id" ...
jsonData$ower$login
## [1] "helio9cn" "helio9cn" ...
```

- writing data frames to JSON

```
myjson <- toJSON(iris, pretty=TRUE)
cat(myjson)
```

- convert back to JSON

```
iris2 <- fromJSON(myson)
head(iris2)
##   Sepal.Length ...
## 1 5.1 ...
```

### the **data.table** package

- **data.table**
  - inherits from data.frame
  - written in C
  - much faster at subsetting, group and updating

```
library(data.table)
DF = data.frame(x=rnome(9),y=rep(c("a","b","c'),each=3),znorm(9))
head(DF,3)
##   x      y z
## 1 0.4159 a -0.05855
DT = data.table(x=rnome(9),y=rep(c("a","b","c'),each=3),znorm(9))
head(DT,3)
tables()
##      NAME NROW MB COLS  KEY
## [1,] DT   0    1  x,y,z
## Total: 1MB
```

- subsetting rows

```
DT[2,]
DT[DT$y="a",]
DT[c(2,3)] ## based on rows
```

- column subsetting in data.table

```
{
  x = 1
  y = 2
}
k = {print(10); 5}
```

- calculate values for variables with expressions

```
DT[,list(mean(x),sum(z))]
##    V1   V2
## 1: 0.05 0.06
DT[,table(y)]
DT[,w:=z^2]
##    x        y z       w
## 1: -0.27721 a 0.25300 0.0064009
```

- multiple operations

```
DT[,m: {tmp<- (x + z); log2(tmp + 5)}]
##    x y z w m
```

- `plyr` like operations

```
DT[,a:x>0]
DT[,b:= mean(x+w),by=a ## group by a = TRUE or FALSE
```

- special variables
  - `.N`

```
set.seed(123);
DT <- data.table(x=sample(letters[1:3], 1E5, TRUE))
DT[, .N, by=x]
```

- keys

```
DT <- data.table(x=rep(c("a","b","c'),each=100(, y=rnorm(300))
setkey(DT, x)
DT['a']
```

- joins

```
DT1 <- data.talbe(x=c('a','a','b','dt1'), y=1:4)
DT1 <- data.talbe(x=c('a','a','dt2'), z=5:7)
setkey(DT1, x); setkey(DT2, x)
merge(DT1, DT2)
##    x y z
## 1: a 1 5
```

- fast reading

```
big_df <- data.frame(x=rnorm(1E6), y=rnorm(1E6))
file <- tempfile()
write.table(big_df, file=file, row.names=FALSE, col.names=TRUE, sep="\t", quote=FALSE)
system.time(fread(file)) ## fread is much faster
## user system elapsed
## 0.312 0.0155 0.326
system.time(read.table(file, header=TRUE, set="\t"))
## user system elapsed
## 5.702 0.048 5.755
```

