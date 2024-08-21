# ReadData

[![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1ZFYTuu7nQM0px2rvzIISxG1_pcy0t27H)

## Load dataset from OneDrive

```r
system("wget https://tecmx-my.sharepoint.com/:x:/g/personal/rleyv_tec_mx/EYHOAX28ve1Kq20EbiCRi7sBcSK_dOq5MR_gmup_2nL9NA?Download=1 -O titanic.csv")
```

## Elementary Analysis

Load dataset into a DataFrame

```r
DF = read.csv("DF.csv")
head(DF)
```

Data types

```r
DF$Survived=as.factor(DF$Survived)
DF$Sex=as.factor(DF$Sex)
sapply(DF, class)

```

Dataset summary

```r
summary(DF)
```

Display number of NaN elements

```r
print("Not a number elements")
sum(is.na(DF))
```

Droput NaN elements

```r
print("Filter out NaN")
DF = DF[rowSums(is.na(DF))<=0,]
```

Retrieve columns by filter

```r
print("Retrieve columns")
survivedlist=DF[DF$Survived == 1,]
notsurvivedlist=DF[DF$Survived == 0,]
survivedlist
notsurvivedlist
```

## Plots

Pie Chart
```r
Survived <- table(DF$Survived)
lbls <- paste(names(Survived), "\n", Survived, sep="")
pie(Survived, labels = lbls, main="Pie Chart of Survived column data\n (with sample sizes)")

```

Scatter Plots
```r
plot(DF$Age, DF$Fare, xlab = "Age", ylab = "Fare")
hist(DF$Fare)
```

Histograms
```r
print("Histograms")
hist(survivedlist$Age, xlab="gender",	ylab="frequency")
```

Bar Plots
```r
barplot(table(notsurvivedlist$Sex), xlab="gender", ylab="frequency")
```

Density Plots
```r
Fare <- density(table(DF$Fare))
plot(Fare, type="n",main="Fare charged from Passengers")
polygon(Fare, col="lightgray",border="gray")
```

Box Plots
```r
boxplot(DF$Fare, main="Fare charged from passengers")
```

   
