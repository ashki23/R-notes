# A gentle introduction to R
*[Ashkan Mirzaee](https://ashki23.github.io/index.html) - December 2019*

[R](https://www.r-project.org/) is a free software environment for statistical computing and graphics. To use R we might use [RStudio](https://www.rstudio.com/), the most popular R IDE, or directly use R in a terminal. In both cases, we need to first download and install R from R webpage or from your favorite package manager (`apt`, `yum`, and etc.). In this article we will cover some fundamental syntax in R including operators, control flow commands, defining functions, reading and writing files, and installing and importing packages. 

You may find more about plotting and programming in R at:

- [Basic graphics in R](https://ashki23.github.io/r_plots.html)
- [Helpful functions in R](https://ashki23.github.io/r_functions.html)
- [R Tutorial](http://www.cyclismo.org/tutorial/R/index.html)
- [Programming with R](http://swcarpentry.github.io/r-novice-inflammation/)
- [R for Reproducible Scientific Analysis](http://swcarpentry.github.io/r-novice-gapminder/)

---

## Operators
R operators include:

- Arithmetic: `+`, `-`, `*`, `/`, `^`, `% any arithmetic operarors %`
- Negation: `!`
- Indexing: `[`, `[[`
- Sequence operator: `:`
- Component/slot extraction: `$`, `@`
- Logical (and/or): `&`, `&&`, `|`, `||`
- Membership: `%in%`
- Assignment: `=`, `<-`, `->`
- Ordering and comparison: `<`, `>`, `<=`, `>=`, `==`, `!=`

For example:
```r
a = 8
b = 3
n = 2
a %/% b  # Intiger division
## 2 

a %% a   # Remainder
## 0

a ^ n    # nth power 
## 64

a ^ 1/n  # nth root
## 4

A = matrix(c(1,2,3,4), ncol = 2)
A
##      [,1] [,2]
## [1,]    1    3
## [2,]    2    4

A %*% A  # Matrix multiplication
##      [,1] [,2]
## [1,]    7   15
## [2,]   10   22
```

## Data structures
There are four major data structures in R:

- Vectors: `c`
- Matrices: `matrix`
- Data frames: `data.frame`
- Lists: `list`

**Vectors** are generating by `c` command which combines values into a vector. Vectors are **subscriptable** and **mutable** objects that can be **concatenated**. We can call them by using `vector[index]`. Vectors keeps all array with a same type.

`matrix` creates a **matrix** from the given set of values. Matrices are **subscriptable** and **mutable** objects and we can use `matrix[row,col]` to call columns and rows. Matrices keeps all array with a same type and they cannot be concatenated.

`data.frame` creates **data frames**, store each column separately as a different variable with different observations (n obs. of m variables). When we read a csv file it saves as a dataframe. Data frames are  **subscriptable** objects and we can use `data.frame[row,col]` or `data.frame[col]` to call columns and rows and `data.frame$col_name` can be used to call certain column by their names. They also can **concatenate**.

R **list** is the object which contains elements of different types – like strings, numbers, vectors, matrices, functions and another list inside it. It also could contains different number of objects at each row. For example if we have a loop that do not generate same amount of results at each iteration then we can store them in a list format. Lists are **subscriptable** and we can use `list$name` or `list[index]` to call components (rows) and `list$name[index_2]` or `list[[index]][index_2]` to call members of each component (row). They also can **concatenate**.

```r
# Vectors
c(1:3,7) # all int 
## [1] 1 2 3 7

1:3 # sequnces are vector
## [1] 1 2 3

seq(1,3) # sequnces are vector
## [1] 1 2 3

c(1:3,'a',7) # all str
## [1] "1" "2" "3" "a" "7"

letter = c('a','b','c','d')
letter[1] # first element
## [1] "a"

letter[1:3] # elements 1 to 3
## [1] "a" "b" "c"

letter[4] = 'z' # mutable

letter
## [1] "a" "b" "c" "z"

c(letter, 'cat') # concatenate
## [1] "a"   "b"   "c"   "z"   "cat"

append(letter, 'append')
## [1] "a"   "b"   "c"   "z"   "append"

# Matrices
mm = matrix(c(1:8), 2, 4)
mm
##      [,1] [,2] [,3] [,4]
## [1,]    1    3    5    7
## [2,]    2    4    6    8

mm[1,2] # row 1 col 2
## [1] 3

mm[2,4] = 100 # mutable
mm
##      [,1] [,2] [,3] [,4]
## [1,]    1    3    5    7
## [2,]    2    4    6  100

## Cannot concatenate
## mm[,5] = c(101,102) # error 

matrix(c('a',1, 'b'), 1)
##      [,1] [,2] [,3]
## [1,] "a"  "1"  "b"

## Dataframes
df = data.frame(col1 = 1:3, col2 = letters[1:3], col3 = 31:33)
df
##   col1 col2 col3
## 1    1    a   31
## 2    2    b   32
## 3    3    c   33

df$col1 # column col1
## [1] 1 2 3

df[,1] # column 1
## [1] 1 2 3

df[1,] # row 1
##   col1 col2 col3
## 1    1    a   31

df[1,1] # row 1 and col 1
## [1] 1

df[1,1] = 100 # mutable
df
##   col1 col2 col3
## 1  100    a   31
## 2    2    b   32
## 3    3    c   33

df$col3[3] = 500 # mutable
df
##   col1 col2 col3
## 1  100    a   31
## 2    2    b   32
## 3    3    c  500

df$col4 = c(103,102,101) # concatenate
df
##   col1 col2 col3 col4
## 1  100    a   31  103
## 2    2    b   32  102
## 3    3    c  500  101

## Lists
ls = list(x = 11:15, y = 1:7)
ls
## $x
## [1] 11 12 13 14 15
## 
## $y
## [1] 1 2 3 4 5 6 7

ls$x
## [1] 11 12 13 14 15

ls[1]
## $x
## [1] 11 12 13 14 15

ls[[2]][7] # or ls$y[7]
## [1] 7

ls[[2]][8] = 80 # concatenate or ls$y[8] = 80
ls
## $x
## [1] 11 12 13 14 15
## 
## $y
## [1]  1  2  3  4  5  6  7 80

ls$z = "this is a new component"
ls
## $x
## [1] 11 12 13 14 15
## 
## $y
## [1]  1  2  3  4  5  6  7 80
## 
## $z
## [1] "this is a new component"

empty_list = vector("list", 2) # make an empty list
names(empty_list) <- paste("list", 1:2, sep = "_") # rename the list
empty_list
## $list_1
## NULL
## 
## $list_2
## NULL
```

Note that not only we can select by indexing the objects, but also we can **remove** entries. For instance:
```r
letter # remove 4th element
## [1] "a" "b" "c" "z"

letter[-4] 
## [1] "a" "b" "c"

mm
##      [,1] [,2] [,3] [,4]
## [1,]    1    3    5    7
## [2,]    2    4    6  100

mm[,c(-2,-3)] # remove column 2,3
##      [,1] [,2]
## [1,]    1    7
## [2,]    2  100

df
##   col1 col2 col3 col4
## 1  100    a   31  103
## 2    2    b   32  102
## 3    3    c  500  101

df = df[,-4] # remove 4th col
df
##   col1 col2 col3
## 1  100    a   31
## 2    2    b   32
## 3    3    c  500

ls
## $x
## [1] 11 12 13 14 15
## 
## $y
## [1]  1  2  3  4  5  6  7 80
## 
## $z
## [1] "this is a new component"

ls[-1] # remove 1st component (x)
## [1] 1 2 3 4 5 6 7
```

And since most of R data structures are **subscriptable**, we can easily **filter** them as well. For example:
```r
df
##   col1 col2 col3
## 1  100    a   31
## 2    2    b   32
## 3    3    c  500

## Let's select rows when:
df[df$col1 < 100,] # col1 < 100
##   col1 col2 col3
## 2    2    b   32
## 3    3    c  500

df[df$col3 %in% c(31,32),] # col3 is 31 or 32
##   col1 col2 col3
## 1  100    a   31
## 2    2    b   32

df[!df$col3 %in% c(31,32),] # col3 is not 31 nor 32
##   col1 col2 col3
## 3    3    c  500

df[df$col1 > 10 & df$col3 > 30, ] # col1 > 10 and col3 > 30 
##   col1 col2 col3
## 1  100    a   31

df[df$col1 > 10 | df$col3 > 40, ] # col1 > 10 or col3 > 30 
##   col1 col2 col3
## 1  100    a   31
## 3    3    c  500

## Let's order based col1
df[order(df$col1),]
##   col1 col2 col3
## 2    2    b   32
## 3    3    c  500
## 1  100    a   31

## Let's find which elemnts in col3 are > 31
which(df$col3 > 31)
## [1] 2 3

## Let's find percentage of col3 > 31
length(which(df$col3 > 31))/nrow(df)
## [1] 0.6666667

## Change col1 to 0,1 such that
df$col1[df$col1 < 100] = 0
df$col1[df$col1 >= 100] = 1
df
##   col1 col2 col3
## 1    1    a   31
## 2    0    b   32
## 3    0    c  500

```

## Control flow tools
These statements allow us to control flow of the R script. The most common control statements include:

  - if, else
  - for
  - while 
  - break 
  - return 
  - repeat 

The following are some simple examples of using these statements in R.

```r
n = 10
if (n == 7) {
  print("n is equal 7")
} else if (n > 7) {
  print("n is greater than 7")
} else {
  print("n is smaller than 7")
}
## [1] "n is greater than 7"

n = 7  
while (n < 10) {
  print(n)
  n = n + 1 
}
## [1] 7
## [1] 8
## [1] 9

mysum = 0
for (i in c(10,20,30)) {
  mysum = mysum + i
}
print(mysum)
## [1] 60

mysum = 0
for (i in 1:100) { 
  mysum = mysum + i
  if (mysum > 25) {
    break
  }
}
print(mysum)
## [1] 28

a = 1:2
b = 1:2
for (i in a) {
  stopifnot(all.equal(a,b)) # if all are not TRUE then stop  
  cat("'a' and 'b' both are equal to: ", i,"\n")
}
## 'a' and 'b' both are equal to:  1 
## 'a' and 'b' both are equal to:  2
```

## Defining functions
By using `function` command we can define our own functions in R. For instance, lets define function $\Delta = b^2 - 4ac$ and find the solution for `a = 2`, `b = 3` and `c = 4`: 

```r
# Delta
delta = function(a, b, c) {
  b^2 - 4*a*c
}
delta(a = 2, b = 3, c = 4)
## [1] -23
```

Some other examples:
```r
# Norm
norm = function(x) sqrt(x %*% x)
norm(1:4)
##          [,1]
## [1,] 5.477226

# Square
square = function(x) return (x * x)
square(2)
## [1] 4

# Factorial
fact_iter = function(n) {
  p = 1
  for (i in 1:n) {
     p = p * i # Not recursive 
  }  
  return(p)
} 
fact_iter(8)
## [1] 40320

# Recersive function that compute n!
fact_rec = function(n) { 
  if (n == 1) 
    return(1)
  else 
    return(n * fact_rec(n - 1)) # Recursive function
}
fact_rec(8)
## [1] 40320

# Recersive function that compute a * b
mult = function(a, b) {
  if (b == 1) {
  return(a)
  } else {
    return(a + mult(a, b-1)) # Recursive function
  }
}
mult(6, 5)
## [1] 30

# Recersive function that compute matrix power
matrix.power = function(p, n) { 
  if (n == 1) 
    return(p)
  else 
    return(p %*% matrix.power(p, n-1)) # Recursive function
}
matrix.power(matrix(c(4,2,2,4), 2, 2), 3)
##      [,1] [,2]
## [1,]  112  104
## [2,]  104  112

# Matrix symmetric test
sym = function(a) {
  if (is.matrix(a) == TRUE) {
    if (identical(a, t(a)) == TRUE) {
      return("Matrix is symmetric")
    } else return("Matrix is not symmetric")
  } else return("Entry is not a Matrix")
}
sym(matrix(c(4,2,2,4), 2, 2))
## [1] "Matrix is symmetric"
```

## Reading and writing
In R we can use `read. ` and `write. ` to read and write the file types that we want.

```r
gpa = data.frame(name = c("Ashki", "Ari", "Dori", "Pishi"), gpa = c(3.4,3.7,3.9,3.5))

# write
write.table(gpa, file = "~/Documents/gpa.txt", sep = " ", row.names = FALSE, col.names = TRUE)

# add
write.table(data.frame(name = "Ellie", gpa = 3.3), file = "~/Documents/gpa.txt", append = TRUE, sep = " ", row.names = FALSE, col.names = FALSE)

# read
read.table("~/Documents/gpa.txt", header = T)

# csv
write.csv(gpa, file = "~/Documents/gpa.csv", row.names = FALSE)
read.csv("~/Documents/gpa.csv") # header is TRUE by default
```

## Packages
Packages are very important component of R. RStudio is a great IDE for R that provides some basic libraries. But based on your requirements you may need to install and import other packages. We can use `install.packages("package name")` and `library("package name")` functions to install and import packages in RStudio. Knowing packages in R is a very important topic, some of packages that I am using are include:

- Documentation: rmarkdown, kintr, kableExtra
- Web application: shiny
- Plot: ggplot2
- GIS: sf, maps, leaflet
- Bayesian analysis: R2OpenBUGS (need openBUGS)
- Panel regression: plm, splm
- Statistical learning: 
  - LDA and QDA: MASS
  - k-nearest neighbors (KNN): class
  - Bootstrapping: boot
  - Ridge and LASSO: glmnet
  - Principal components regression (PCR) and Partial Least Squares (PLS): pls
  - Spline: splines
  - Generalized additive models (GAM): gam
  - Gradient Boosting Machines (GBM): gbm
  - tree, Random forest and bagging: tree, randomForest
  - Support Vector Machine (SVM): e1071

---
Copyright 2018-2019, [Ashkan Mirzaee](https://ashki23.github.io/index.html) | Content is available under [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/) | Sourcecode licensed under [GPL-3.0](https://www.gnu.org/licenses/gpl-3.0.en.html)
