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

x <- 1:6

Perform operation

y <- x^2

Display arrays

print(x)
print(y)

Matrix operations

z <- x+y

Reshape into matrix

z <- matrix(z, nrow = 3)
print(z)

Several wise operators on matrix and transpose

z <- 2*t(z)-2
print(z)

## 2. Data structures

Create data frame

DF <- data.frame(z, row.names = c("A","B"))
print(DF)
attributes(DF)

Rename columns

names(DF) <- c("A","B","C")
print(DF)

Retrieve column

DF$C

Other ways of accessing

DF["C"]

DF[3]

Modify values

attributes(DF)$row.names <- c("first","second")
print(DF)

## 3. Functions

Declaration

f <- function(x,y){
  z <- 2*x + 3*y
  return(z)
}

f(2,3)

