# Helpful functions in R

[R](https://www.r-project.org/) is a powerful tool for statistical learning, data analysis and graphics that includes numerous built-in functions. R is a very self explanatory environment in terms of documentation. We can learn about any R commands only by using `help(command)`. As a prerequisite, first review the following article:

- [A gentle introduction to R](https://ashki23.github.io/r-intro.html)

The following are also more resources to learn R programming:

- [R Tutorial](http://www.cyclismo.org/tutorial/R/index.html)
- [Programming with R](http://swcarpentry.github.io/r-novice-inflammation/)
- [R for Reproducible Scientific Analysis](http://swcarpentry.github.io/r-novice-gapminder/)
- [Basic graphics in R](https://ashki23.github.io/r-plots.html)

In this article, we will learn about some fundamental functions for data structures, date and time data, data mining, control flow and defining new functions.

---

## Date and time
There are several functions to work with date and time classes, following are some examples of these functions.  

```r
Sys.time()
## [1] "2020-02-12 21:47:43 CST"

d = Sys.Date()
d
## [1] "2020-02-12"

weekdays(d)
## [1] "Wednesday"

months(d)
## [1] "February"

quarters(d)
## [1] "Q1"

format(Sys.time(), "%d")
## [1] "12"

format(Sys.time(), "%m")
## [1] "02"

format(Sys.time(), "%Y")
## [1] "2020"

timestamp()
## ##------ Wed Feb 12 21:47:43 2020 ------##

format(Sys.time(), "%a %b %d %Y %X") # To see more options for format enter `help(strftime)`
## [1] "Wed Feb 12 2020 21:47:43"

format(Sys.time(), "%Y-%m-%d")
## [1] "2020-02-12"

format(Sys.time(), "%H:%M:%S")
## [1] "21:47:43"

weeks = seq(Sys.Date(), length.out = 3, by = "1 week") # Next three weeks
weeks
## [1] "2020-02-12" "2020-02-19" "2020-02-26"

difftime(weeks[2], weeks[1], units = "auto")
## Time difference of 7 days

# Date-time conversion
strftime(Sys.time(), format = "%a %d %b %Y %H:%M:%S") # convert time-date objects to character
## [1] "Wed 12 Feb 2020 21:47:43"

strptime("20/2/06 11:16:16.683", format = "%d/%m/%y %H:%M:%OS") # convert character to time-date objects
## [1] "2006-02-20 11:16:16 CST"
```

`ts` function can be used to create a vector or matrix of **time-series** objects.

```r
ts(1:12, start = c(1956, 3), frequency = 12) # for season: frequency = 4
##      Jan Feb Mar Apr May Jun Jul Aug Sep Oct Nov Dec
## 1956           1   2   3   4   5   6   7   8   9  10
## 1957  11  12
```

## Differentiation and integration
R base system supports both differentiation and integration, for instance:
```r
## Derivative
f = expression(x^2+3*x)
ff = D(f, "x")
ff
## 2 * x + 3

x = 2 
eval(ff) # to find the answer for x = 2 
## [1] 7

D(ff, "x") # to find the second derivate
## [1] 2

## Integrate
f = function(x) x^2+3*x
integrate(f, lower = 0, upper = 1)
## 1.833333 with absolute error < 2e-14
```

## Matrix operations
The most common matrix operations include:

- Dimensions of a matrix: `dim()`
- Diagonal of a matrix: `diag()`
- Identity matrix: `diag(number)`
- Matrix symmetric test: `isSymmetric()`
- Matrix multiplication: `%*%`
- Test matrices for exact equality: `identical(,)`
- Matrix transpose: `t()`
- Determinant of a matrix: `det()`
- Inverse of a matrix: `solve()`
- Solve a system of equations: `solve()`
- QR Decomposition of a Matrix: `qr()`
- Spectral Decomposition of a Matrix: `eigen()`

The following are some examples of above functions.

```r
M = matrix(c(4,4,-2,2,6,2,2,8,4), 3, 3)
N = matrix(c(3,2,1,0,1,-2,4,5,6), 3, 3)
b = matrix(c(0,0,1))

dim(M)
## [1] 3 3

diag(M)
## [1] 4 6 4

diag(3)
##      [,1] [,2] [,3]
## [1,]    1    0    0
## [2,]    0    1    0
## [3,]    0    0    1

isSymmetric(M)
## [1] FALSE

M %*% N
##      [,1] [,2] [,3]
## [1,]   18   -2   38
## [2,]   32  -10   94
## [3,]    2   -6   26

identical(M, N)
## [1] FALSE

t(M)
##      [,1] [,2] [,3]
## [1,]    4    4   -2
## [2,]    2    6    2
## [3,]    2    8    4

det(M)
## [1] 8

qr(M)
## $qr
##            [,1]       [,2]       [,3]
## [1,] -6.0000000 -4.6666667 -5.3333333
## [2,]  0.6666667 -4.7140452 -7.4481914
## [3,] -0.3333333  0.7071068  0.2828427
## 
## $rank
## [1] 3
## 
## $qraux
## [1] 1.6666667 1.7071068 0.2828427
## 
## $pivot
## [1] 1 2 3
## 
## attr(,"class")
## [1] "qr"

solve(M) # Inverse of M
##      [,1] [,2] [,3]
## [1,]  1.0 -0.5  0.5
## [2,] -4.0  2.5 -3.0
## [3,]  2.5 -1.5  2.0

solve(M,b) # Solve a system
##      [,1]
## [1,]  0.5
## [2,] -3.0
## [3,]  2.0

eigen(M)
## eigen() decomposition
## $values
## [1] 9.4185507 4.3878731 0.1935761
## 
## $vectors
##           [,1]       [,2]       [,3]
## [1,] 0.3994272 -0.6725085  0.1632537
## [2,] 0.8980978 -0.5844552 -0.8354557
## [3,] 0.1840605  0.4540313  0.5247494
```

## Computational functions
R provides an abundance of computational functions. The following are some examples of these functions. 

```r
# Cumulative sums, products
cumsum(1:5)
## [1]  1  3  6 10 15

cumprod(1:5)
## [1]   1   2   6  24 120

set.seed(23)
mydata = data.frame(sample = sample(1:100, 5), random = rnorm(5))
mydata
##   sample     random
## 1     29  2.7075823
## 2     28  0.5284939
## 3     72 -0.4823752
## 4     43 -1.0835666
## 5     45  0.2366887

# Which min/max
which.min(mydata$sample)
## [1] 2

which.max(mydata$sample)
## [1] 3

# Apply
apply(mydata , 2, quantile) # Calculate quantile
##      sample     random
## 0%       28 -1.0835666
## 25%      29 -0.4823752
## 50%      43  0.2366887
## 75%      45  0.5284939
## 100%     72  2.7075823

apply(mydata, 2, mean) # Calculate mean
##     sample     random 
## 43.4000000  0.3813646

colMeans(mydata)
##     sample     random 
## 43.4000000  0.3813646

scale(mydata) # scale(x) = (x - mean(x)) / sd(x)
##           sample     random
## [1,] -0.80967904  1.6104335
## [2,] -0.86590675  0.1018572
## [3,]  1.60811253 -0.5979645
## [4,] -0.02249108 -1.0141675
## [5,]  0.08996434 -0.1001587
## attr(,"scaled:center")
##     sample     random 
## 43.4000000  0.3813646 
## attr(,"scaled:scale")
##    sample    random 
## 17.784825  1.444467
```

## Summary statistics
`aggregate` function splits the data into subsets, computes summary statistics for each, and returns the result in a convenient form. `table` uses the cross-classifying factors to build a contingency table of the counts at each combination of factor levels.

```r
head(warpbreaks)
##   breaks wool tension
## 1     26    A       L
## 2     30    A       L
## 3     54    A       L
## 4     25    A       L
## 5     70    A       L
## 6     52    A       L

aggregate(breaks ~ wool + tension, data = warpbreaks, mean)
##   wool tension   breaks
## 1    A       L 44.55556
## 2    B       L 28.22222
## 3    A       M 24.00000
## 4    B       M 28.77778
## 5    A       H 24.55556
## 6    B       H 18.77778

head(airquality)
##   Ozone Solar.R Wind Temp Month Day
## 1    41     190  7.4   67     5   1
## 2    36     118  8.0   72     5   2
## 3    12     149 12.6   74     5   3
## 4    18     313 11.5   62     5   4
## 5    NA      NA 14.3   56     5   5
## 6    28      NA 14.9   66     5   6

aggregate(cbind(Ozone, Temp) ~ Month, data = airquality, mean)
##   Month    Ozone     Temp
## 1     5 23.61538 66.73077
## 2     6 29.44444 78.22222
## 3     7 59.11538 83.88462
## 4     8 59.96154 83.96154
## 5     9 31.44828 76.89655

# Finding frequency
letter = c('d','b','c','d','a','d','a', 'c')
fr = data.frame(table(letter))
fr
##   letter Freq
## 1      a    2
## 2      b    1
## 3      c    2
## 4      d    3

fr[order(fr$Freq, decreasing = TRUE),]
##   letter Freq
## 4      d    3
## 1      a    2
## 3      c    2
## 2      b    1

# Correlation matrix
cor(mtcars[,1:3])
##             mpg        cyl       disp
## mpg   1.0000000 -0.8521620 -0.8475514
## cyl  -0.8521620  1.0000000  0.9020329
## disp -0.8475514  0.9020329  1.0000000

# Symbolic coding correlation matrix
symnum(cor(mtcars))
##      m cy ds h dr w q v a g cr
## mpg  1                        
## cyl  + 1                      
## disp + *  1                   
## hp   , +  ,  1                
## drat , ,  ,  . 1              
## wt   + ,  +  , ,  1           
## qsec . .  .  ,      1         
## vs   , +  ,  , .  . , 1       
## am   . .  .    ,  ,     1     
## gear . .  .    ,  .     , 1   
## carb . .  .  ,    . , .     1 
## attr(,"legend")
## [1] 0 ' ' 0.3 '.' 0.6 ',' 0.8 '+' 0.9 '*' 0.95 'B' 1
```

## Split and merge data
`split` function divides the data into a list of defined groups. `merge` function merge two data frames by common columns or row names. `merge` is similar to `JOIN` in SQL:

- Inner join: `merge(x, y, by)`
- Left join: `merge(x, y, by, all.x = T)`
- Right join: `merge(x, y, by, all.y = T)`
- Outer join: `merge(x, y, by, all = T)`

```r
data = expand.grid(meat = c("grade-1","grade-2","grade-3"), food = c("burger", "steak", "pizza"))
data$value = round(rnorm(nrow(data)), 2)
data
##      meat   food value
## 1 grade-1 burger  0.33
## 2 grade-2 burger -0.60
## 3 grade-3 burger  0.85
## 4 grade-1  steak  0.92
## 5 grade-2  steak  1.19
## 6 grade-3  steak  0.77
## 7 grade-1  pizza -0.60
## 8 grade-2  pizza -0.39
## 9 grade-3  pizza  0.88

data_by_food = split(data, data$food)
data_by_food
## $burger
##      meat   food value
## 1 grade-1 burger  0.33
## 2 grade-2 burger -0.60
## 3 grade-3 burger  0.85
## 
## $steak
##      meat  food value
## 4 grade-1 steak  0.92
## 5 grade-2 steak  1.19
## 6 grade-3 steak  0.77
## 
## $pizza
##      meat  food value
## 7 grade-1 pizza -0.60
## 8 grade-2 pizza -0.39
## 9 grade-3 pizza  0.88

class(data_by_food)
## [1] "list"

x = data.frame(ID = 1:6, Product = c(rep("TV", 3), rep("Mobile", 3)))
x
##   ID Product
## 1  1      TV
## 2  2      TV
## 3  3      TV
## 4  4  Mobile
## 5  5  Mobile
## 6  6  Mobile

y = data.frame(ID = c(2,4,6), Made_in = c(rep("Japan", 2), rep("China", 1)))
y
##   ID Made_in
## 1  2   Japan
## 2  4   Japan
## 3  6   China

merge(x, y, by = "ID") # Inner join
##   ID Product Made_in
## 1  2      TV   Japan
## 2  4  Mobile   Japan
## 3  6  Mobile   China

merge(x, y, by = "ID", all = TRUE) # Full outer join
##   ID Product Made_in
## 1  1      TV    <NA>
## 2  2      TV   Japan
## 3  3      TV    <NA>
## 4  4  Mobile   Japan
## 5  5  Mobile    <NA>
## 6  6  Mobile   China
```

## Regular expressions 
[Regular expressions](https://en.wikipedia.org/wiki/Regular_expression) (regex) are a simple way to find patterns in text. The most common functions implementing regex in R are in the **global regular expression print** (`grep`) family. For more information see `help("regex")` and `help(grep)`. Learn more about regex functions in R at [D-RUG](https://d-rug.github.io/blog/2015/regex.fick). Following are some simple examples. 

```r
sub("a", "#", "abcdfa") # Substitution: substitue first "a" in the expression "abcdfa" with "#" 
## [1] "#bcdfa"

gsub("a", "#", "abcdfa") # General substitution: substitue all "a" in the expression "abcdfa" with "#"  
## [1] "#bcdf#"

substr("abcdef", 1, 3) # substr(x, start, stop)
## [1] "abc"

substr("abcdef", 1, regexpr("d","abcdef")[1]) # From first to "d"
## [1] "abcd"

substr("abcdef", nchar("abcdef")+1-3, nchar("abcdef")) # First 3 caracters from right
## [1] "def"

grep("a", c("abc", "def", "cba a", "aa"), value = FALSE) # Shows arrays' number that include "a"
## [1] 1 3 4

grep("a+", c("abc", "def", "cba a", "aa"), value = TRUE) # Shows expressions that include one or more "a"
## [1] "abc"   "cba a" "aa"

grepl("Jojo", "my name is Jojo") # True if "Jojo" is in the text
## [1] TRUE

grepl("^Jojo", "my name is Jojo") # True if "Jojo" is at the begining of the text
## [1] FALSE

grepl("Jojo$", "my name is Jojo") # True if "Jojo" is at the end of the text
## [1] TRUE

grepl("[J-j]ojo", "my name is Jojo") # True if "Jojo" or "jojo" is in the text
## [1] TRUE

pattern = "(\\d{3})[-. )]*(\\d{3})[-. ]*(\\d{4})"

grep(pattern, "888-555-7766", value = TRUE)
## [1] "888-555-7766"

r = regexec(pattern, "888-555-7766")
regmatches("888-555-7766", r)
## [[1]]
## [1] "888-555-7766" "888"          "555"          "7766"

list.files(path = "./files", pattern = "*.pdf$") # List of "pdf" files in a directory
## [1] "Ashkan_Mirzaee_CV_Fall2019.pdf"   "Ashkan_Mirzaee_CV_Spring2020.pdf"
## [3] "CV_01_2019.pdf"
```

---
Copyright 2018-2019, [Ashkan Mirzaee](https://ashki23.github.io/index.html) | Content is available under [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/) | Sourcecode licensed under [GPL-3.0](https://www.gnu.org/licenses/gpl-3.0.en.html)
