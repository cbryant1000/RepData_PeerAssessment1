# Reproducible Research: Peer Assessment 1


## Loading and preprocessing the data


```r
library(dplyr)
```

```
## 
## Attaching package: 'dplyr'
## 
## The following object is masked from 'package:stats':
## 
##     filter
## 
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

```r
data <- read.csv("activity.csv",stringsAsFactors=FALSE)
data$date <- as.Date(data$date)
summary(data)
```

```
##      steps             date               interval     
##  Min.   :  0.00   Min.   :2012-10-01   Min.   :   0.0  
##  1st Qu.:  0.00   1st Qu.:2012-10-16   1st Qu.: 588.8  
##  Median :  0.00   Median :2012-10-31   Median :1177.5  
##  Mean   : 37.38   Mean   :2012-10-31   Mean   :1177.5  
##  3rd Qu.: 12.00   3rd Qu.:2012-11-15   3rd Qu.:1766.2  
##  Max.   :806.00   Max.   :2012-11-30   Max.   :2355.0  
##  NA's   :2304
```


## What is mean total number of steps taken per day?


```r
days <- group_by(data, date)
days <- summarise(days, nintervals=n(), avgsteps=mean(steps,na.rm=TRUE), totsteps=nintervals*avgsteps)
plot(days$date, days$totsteps, type="h",xlab="Date",ylab="Total Steps per Day",main="Histogram - Total Number of Steps per Day")
```

![](PA1_template_files/figure-html/unnamed-chunk-2-1.png) 
 
 __Total Number of Steps per Day__  
 __Mean:__ 10766.19  
 __Median:__ 10765  


## What is the average daily activity pattern?


```r
days <- group_by(data, interval)
days <- summarise(days, avgsteps=mean(steps,na.rm=TRUE))
days <- mutate(days, minutes=(interval/100), seconds=(interval - 100*minutes + 60*minutes), index=seconds/5)
plot(days$index, days$avgsteps, type="l", xlab="Interval", ylab="Average Steps", main="Daily Activity - Average Number of Steps")
```

![](PA1_template_files/figure-html/unnamed-chunk-3-1.png) 


## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
