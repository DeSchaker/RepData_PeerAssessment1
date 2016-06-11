# Reproducible Research: Peer Assessment 1


## Loading and preprocessing the data

First we read in the data from the activity.csv file, that was downloaded from the [course website](https://d396qusza40orc.cloudfront.net/repdata%2Fdata%2Factivity.zip).



```r
setwd("~/R/projecten/Coursera/RepData_PeerAssessment1")
df_act <- read.csv("activity.csv",na.strings = "NA")
```

Next we convert the date column from string to date

```r
df_act$date <- as.Date(as.character(df_act$date))
```

## What is mean total number of steps taken per day?
This part consists of the following steps:

1. Calculate the total number of steps taken per day

```r
df_stepsday <- aggregate(steps ~ date, data=df_act, FUN=sum, na.rm=TRUE )
```
2. Make a histogram of the total number of steps taken each day

```r
hist(df_stepsday$steps,breaks=10,col="purple",xlab="steps taken",main="Steps taken per day")
```

![](PA1_template_files/figure-html/unnamed-chunk-4-1.png)<!-- -->

3. Calculate and report the mean and median of the total number of steps taken per day

```r
mean(df_stepsday$steps)
```

```
## [1] 10766.19
```

```r
median(df_stepsday$steps)
```

```
## [1] 10765
```

## What is the average daily activity pattern?
First we calculate the mean steps per interval across the days and put the results in the vector mean_steps, next we make a time plot with the names and values of this vector. Finally we calculate which interval contains the maximum number of average steps.


```r
mean_steps <- tapply(df_act$steps,INDEX=df_act$interval,FUN=mean,na.rm=TRUE)
plot(names(mean_steps),mean_steps,type="l",xlab="5 minute interval",ylab="mean steps",
     main="average daily activity pattern")
```

![](PA1_template_files/figure-html/unnamed-chunk-6-1.png)<!-- -->

```r
print(paste("Interval with maximum number of average steps:", names(which.max(mean_steps))))
```

```
## [1] "Interval with maximum number of average steps: 835"
```



## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
