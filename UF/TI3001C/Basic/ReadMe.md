# TI3001C

[![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1i68U5C2lWpBsw2cs_vWew3qNNv9IKlio)

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

### 4. Plots

Inline display plots

```r
x <- 1:6
y <- x ^ 2

print(x)
print(y)

plot(x,y)
```
Linear regresion model
```r
Model <- lm(y ~ x)
```
Summary
```r
summary(Model)
```
Layout
```r
par(mfrow = c(2,2))
```
Display
```r
plot(Model)
```
### 5. Packages
```r
install.packages("caTools")

library(caTools)

jet.colors <-
    colorRampPalette(
        c("green", "pink", "#007FFF", "cyan", "#7FFF7F",
          "white", "#FF7F00", "red", "#7F0000"))

dx <- 1500 # define width
dy <- 1400 # define height

C  <-
    complex(
            real = rep(seq(-2.2, 1.0, length.out = dx), each = dy),
            imag = rep(seq(-1.2, 1.2, length.out = dy), times = dx)
            )

# reshape as matrix of complex numbers
C <- matrix(C, dy, dx)

# initialize output 3D array
X <- array(0, c(dy, dx, 20))

Z <- 0

# loop with 20 iterations
for (k in 1:20) {

  # the central difference equation
  Z <- Z^2 + C

  # capture the results
  X[, , k] <- exp(-abs(Z))
}

write.gif(
    X,
    "Mandelbrot.gif",
    col = jet.colors,
    delay = 100)
    
```    
