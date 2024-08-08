# TI3001C

## R-install

```bash
sudo apt install r-base
```

## Basic Commands

This document comprises basic commands to handle in place variables and elementary data structures.

### 1. Operators

Display message

```r
print("Hi there")
```

Declare array

```r
x <- 1:6
```

Perform operation

```r
y <- x^2
```

Display arrays

```r
print(x)
print(y)
```

Matrix operations

```r
z <- x+y
```

Reshape into matrix

```r
z <- matrix(z, nrow = 3)
print(z)
```

Several wise operators on matrix and transpose

```r
z <- 2*t(z)-2
print(z)
```

### 2. Data structures

Create data frame
```r
DF <- data.frame(z, row.names = c("A","B"))
print(DF)
attributes(DF)
```

Rename columns
```r
names(DF) <- c("A","B","C")
print(DF)
```
Retrieve column
```r
DF$C
```
Other ways of accessing
```r
DF["C"]

DF[3]
```
Modify values
```r
attributes(DF)$row.names <- c("first","second")
print(DF)
```
### 3. Functions

Declaration
```r
f <- function(x,y){
  z <- 2*x + 3*y
  return(z)
}

f(2,3)
```


Map arrays
```r
f(1:2,2:3)
f(c(1,2,3),c(4,5,6))
f(0:3,4)

infix operation
```r
'%sumsq%' <- function(x,y){x ^ 2 + y ^ 2}
1:3 %sumsq% -(1:3)
```

lambda
```r
sapply(0:5, \(i) i ^ 2 )
```

Nested operations on preloaded data
```r
mtcars
```

Nested without vert operator
```r
nrow(subset(mtcars, cyl == 4))
```

Nested with vert opeator
```r
mtcars |> subset(cyl == 4) |> nrow()
```
