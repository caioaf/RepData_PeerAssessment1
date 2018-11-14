Peer-graded Assignment: Course Project 1
========================================

It is now possible to collect a large amount of data about personal
movement using activity monitoring devices such as a Fitbit, Nike
Fuelband, or Jawbone Up. These type of devices are part of the
“quantified self” movement – a group of enthusiasts who take
measurements about themselves regularly to improve their health, to find
patterns in their behavior, or because they are tech geeks. But these
data remain under-utilized both because the raw data are hard to obtain
and there is a lack of statistical methods and software for processing
and interpreting the data.

This assignment makes use of data from a personal activity monitoring
device.

Observations
------------

-   I've hide all library loads from HTML/Markdown report for reading
    purposes
-   

Analysis
========

Loading and preprocessing the data
----------------------------------

### Load the Data

    rawData <- read.csv("activity.csv")

### Process/transform the data (if necessary) into a format suitable for your analysis

Creating variable without NA steps

    # Using dplyr library
    data <- rawData %>% filter(!is.na(steps))

What is mean total number of steps taken per day?
-------------------------------------------------

For this part of the assignment, I will ignore the missing values in the
dataset.

### Calculate the total number of steps taken per day

    totalSteps <- aggregate(data$steps, list(date = data$date), sum)
    print(totalSteps)

    ##          date     x
    ## 1  2012-10-02   126
    ## 2  2012-10-03 11352
    ## 3  2012-10-04 12116
    ## 4  2012-10-05 13294
    ## 5  2012-10-06 15420
    ## 6  2012-10-07 11015
    ## 7  2012-10-09 12811
    ## 8  2012-10-10  9900
    ## 9  2012-10-11 10304
    ## 10 2012-10-12 17382
    ## 11 2012-10-13 12426
    ## 12 2012-10-14 15098
    ## 13 2012-10-15 10139
    ## 14 2012-10-16 15084
    ## 15 2012-10-17 13452
    ## 16 2012-10-18 10056
    ## 17 2012-10-19 11829
    ## 18 2012-10-20 10395
    ## 19 2012-10-21  8821
    ## 20 2012-10-22 13460
    ## 21 2012-10-23  8918
    ## 22 2012-10-24  8355
    ## 23 2012-10-25  2492
    ## 24 2012-10-26  6778
    ## 25 2012-10-27 10119
    ## 26 2012-10-28 11458
    ## 27 2012-10-29  5018
    ## 28 2012-10-30  9819
    ## 29 2012-10-31 15414
    ## 30 2012-11-02 10600
    ## 31 2012-11-03 10571
    ## 32 2012-11-05 10439
    ## 33 2012-11-06  8334
    ## 34 2012-11-07 12883
    ## 35 2012-11-08  3219
    ## 36 2012-11-11 12608
    ## 37 2012-11-12 10765
    ## 38 2012-11-13  7336
    ## 39 2012-11-15    41
    ## 40 2012-11-16  5441
    ## 41 2012-11-17 14339
    ## 42 2012-11-18 15110
    ## 43 2012-11-19  8841
    ## 44 2012-11-20  4472
    ## 45 2012-11-21 12787
    ## 46 2012-11-22 20427
    ## 47 2012-11-23 21194
    ## 48 2012-11-24 14478
    ## 49 2012-11-25 11834
    ## 50 2012-11-26 11162
    ## 51 2012-11-27 13646
    ## 52 2012-11-28 10183
    ## 53 2012-11-29  7047

### Make a histogram of the total number of steps taken each day

    histogram <- ggplot(data = totalSteps, aes(totalSteps$x)) + geom_histogram() + labs(x = "Steps per day", title = "Histogram for steps") + scale_y_continuous(breaks = (1:5)*2)
    print(histogram)

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](PA1_template_files/figure-markdown_strict/histogram-1.png)

### Calculate and report the mean and median of the total number of steps taken per day

    meanSteps <- aggregate(data$steps, list(date = data$date), mean)
    print(meanSteps)

    ##          date          x
    ## 1  2012-10-02  0.4375000
    ## 2  2012-10-03 39.4166667
    ## 3  2012-10-04 42.0694444
    ## 4  2012-10-05 46.1597222
    ## 5  2012-10-06 53.5416667
    ## 6  2012-10-07 38.2465278
    ## 7  2012-10-09 44.4826389
    ## 8  2012-10-10 34.3750000
    ## 9  2012-10-11 35.7777778
    ## 10 2012-10-12 60.3541667
    ## 11 2012-10-13 43.1458333
    ## 12 2012-10-14 52.4236111
    ## 13 2012-10-15 35.2048611
    ## 14 2012-10-16 52.3750000
    ## 15 2012-10-17 46.7083333
    ## 16 2012-10-18 34.9166667
    ## 17 2012-10-19 41.0729167
    ## 18 2012-10-20 36.0937500
    ## 19 2012-10-21 30.6284722
    ## 20 2012-10-22 46.7361111
    ## 21 2012-10-23 30.9652778
    ## 22 2012-10-24 29.0104167
    ## 23 2012-10-25  8.6527778
    ## 24 2012-10-26 23.5347222
    ## 25 2012-10-27 35.1354167
    ## 26 2012-10-28 39.7847222
    ## 27 2012-10-29 17.4236111
    ## 28 2012-10-30 34.0937500
    ## 29 2012-10-31 53.5208333
    ## 30 2012-11-02 36.8055556
    ## 31 2012-11-03 36.7048611
    ## 32 2012-11-05 36.2465278
    ## 33 2012-11-06 28.9375000
    ## 34 2012-11-07 44.7326389
    ## 35 2012-11-08 11.1770833
    ## 36 2012-11-11 43.7777778
    ## 37 2012-11-12 37.3784722
    ## 38 2012-11-13 25.4722222
    ## 39 2012-11-15  0.1423611
    ## 40 2012-11-16 18.8923611
    ## 41 2012-11-17 49.7881944
    ## 42 2012-11-18 52.4652778
    ## 43 2012-11-19 30.6979167
    ## 44 2012-11-20 15.5277778
    ## 45 2012-11-21 44.3993056
    ## 46 2012-11-22 70.9270833
    ## 47 2012-11-23 73.5902778
    ## 48 2012-11-24 50.2708333
    ## 49 2012-11-25 41.0902778
    ## 50 2012-11-26 38.7569444
    ## 51 2012-11-27 47.3819444
    ## 52 2012-11-28 35.3576389
    ## 53 2012-11-29 24.4687500

    medianSteps <- aggregate(data$steps, list(date = data$date), median)
    print(medianSteps)

    ##          date x
    ## 1  2012-10-02 0
    ## 2  2012-10-03 0
    ## 3  2012-10-04 0
    ## 4  2012-10-05 0
    ## 5  2012-10-06 0
    ## 6  2012-10-07 0
    ## 7  2012-10-09 0
    ## 8  2012-10-10 0
    ## 9  2012-10-11 0
    ## 10 2012-10-12 0
    ## 11 2012-10-13 0
    ## 12 2012-10-14 0
    ## 13 2012-10-15 0
    ## 14 2012-10-16 0
    ## 15 2012-10-17 0
    ## 16 2012-10-18 0
    ## 17 2012-10-19 0
    ## 18 2012-10-20 0
    ## 19 2012-10-21 0
    ## 20 2012-10-22 0
    ## 21 2012-10-23 0
    ## 22 2012-10-24 0
    ## 23 2012-10-25 0
    ## 24 2012-10-26 0
    ## 25 2012-10-27 0
    ## 26 2012-10-28 0
    ## 27 2012-10-29 0
    ## 28 2012-10-30 0
    ## 29 2012-10-31 0
    ## 30 2012-11-02 0
    ## 31 2012-11-03 0
    ## 32 2012-11-05 0
    ## 33 2012-11-06 0
    ## 34 2012-11-07 0
    ## 35 2012-11-08 0
    ## 36 2012-11-11 0
    ## 37 2012-11-12 0
    ## 38 2012-11-13 0
    ## 39 2012-11-15 0
    ## 40 2012-11-16 0
    ## 41 2012-11-17 0
    ## 42 2012-11-18 0
    ## 43 2012-11-19 0
    ## 44 2012-11-20 0
    ## 45 2012-11-21 0
    ## 46 2012-11-22 0
    ## 47 2012-11-23 0
    ## 48 2012-11-24 0
    ## 49 2012-11-25 0
    ## 50 2012-11-26 0
    ## 51 2012-11-27 0
    ## 52 2012-11-28 0
    ## 53 2012-11-29 0

What is the average daily activity pattern?
-------------------------------------------

### Make a time series plot of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all days (y-axis)

    timeSeriesData <- aggregate(data$steps, list(interval = data$interval), mean)
    timeSeries <- ggplot(data = timeSeriesData, aes(x = interval, y = x)) + geom_line() + labs(x = "5-minute interval", y = "Average Steps", title = "Average steps time series")
    print(timeSeries)

![](PA1_template_files/figure-markdown_strict/time_series-1.png)

### Which 5-minute interval, on average across all the days in the dataset, contains the maximum number of steps?

    maxStepsInteval <- timeSeriesData %>% filter(x == max(x))
    print(maxStepsInteval)

    ##   interval        x
    ## 1      835 206.1698

Imputing missing values
-----------------------

### Calculate and report the total number of missing values in the dataset (i.e. the total number of rows with NAs)

    # There are no NA values for 'date' or 'interval'
    nrow(rawData %>% filter(is.na(steps)))

    ## [1] 2304

### Devise a strategy for filling in all of the missing values in the dataset. The strategy does not need to be sophisticated. For example, you could use the mean/median for that day, or the mean for that 5-minute interval, etc.

### Create a new dataset that is equal to the original dataset but with the missing data filled in.

    # The 'steps' median value is 0, as found before.
    # My strategy will fill NA values with 0

    newDataset <- rawData
    newDataset$steps[is.na(newDataset$steps)] <- 0
    nrow(newDataset %>% filter(is.na(steps)))

    ## [1] 0

### Make a histogram of the total number of steps taken each day and Calculate and report the mean and median total number of steps taken per day.

    totalSteps2 <- aggregate(newDataset$steps, list(date = newDataset$date), sum)
    histogram2 <- ggplot(data = totalSteps2, aes(totalSteps2$x)) + geom_histogram() + labs(x = "Steps per day", title = "Histogram for steps") + scale_y_continuous(breaks = (1:5)*2)
    print(histogram2)

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](PA1_template_files/figure-markdown_strict/histogram_mean_median_steps-1.png)

    meanSteps2 <- aggregate(newDataset$steps, list(date = newDataset$date), mean)
    print(meanSteps2)

    ##          date          x
    ## 1  2012-10-01  0.0000000
    ## 2  2012-10-02  0.4375000
    ## 3  2012-10-03 39.4166667
    ## 4  2012-10-04 42.0694444
    ## 5  2012-10-05 46.1597222
    ## 6  2012-10-06 53.5416667
    ## 7  2012-10-07 38.2465278
    ## 8  2012-10-08  0.0000000
    ## 9  2012-10-09 44.4826389
    ## 10 2012-10-10 34.3750000
    ## 11 2012-10-11 35.7777778
    ## 12 2012-10-12 60.3541667
    ## 13 2012-10-13 43.1458333
    ## 14 2012-10-14 52.4236111
    ## 15 2012-10-15 35.2048611
    ## 16 2012-10-16 52.3750000
    ## 17 2012-10-17 46.7083333
    ## 18 2012-10-18 34.9166667
    ## 19 2012-10-19 41.0729167
    ## 20 2012-10-20 36.0937500
    ## 21 2012-10-21 30.6284722
    ## 22 2012-10-22 46.7361111
    ## 23 2012-10-23 30.9652778
    ## 24 2012-10-24 29.0104167
    ## 25 2012-10-25  8.6527778
    ## 26 2012-10-26 23.5347222
    ## 27 2012-10-27 35.1354167
    ## 28 2012-10-28 39.7847222
    ## 29 2012-10-29 17.4236111
    ## 30 2012-10-30 34.0937500
    ## 31 2012-10-31 53.5208333
    ## 32 2012-11-01  0.0000000
    ## 33 2012-11-02 36.8055556
    ## 34 2012-11-03 36.7048611
    ## 35 2012-11-04  0.0000000
    ## 36 2012-11-05 36.2465278
    ## 37 2012-11-06 28.9375000
    ## 38 2012-11-07 44.7326389
    ## 39 2012-11-08 11.1770833
    ## 40 2012-11-09  0.0000000
    ## 41 2012-11-10  0.0000000
    ## 42 2012-11-11 43.7777778
    ## 43 2012-11-12 37.3784722
    ## 44 2012-11-13 25.4722222
    ## 45 2012-11-14  0.0000000
    ## 46 2012-11-15  0.1423611
    ## 47 2012-11-16 18.8923611
    ## 48 2012-11-17 49.7881944
    ## 49 2012-11-18 52.4652778
    ## 50 2012-11-19 30.6979167
    ## 51 2012-11-20 15.5277778
    ## 52 2012-11-21 44.3993056
    ## 53 2012-11-22 70.9270833
    ## 54 2012-11-23 73.5902778
    ## 55 2012-11-24 50.2708333
    ## 56 2012-11-25 41.0902778
    ## 57 2012-11-26 38.7569444
    ## 58 2012-11-27 47.3819444
    ## 59 2012-11-28 35.3576389
    ## 60 2012-11-29 24.4687500
    ## 61 2012-11-30  0.0000000

    medianSteps2 <- aggregate(newDataset$steps, list(date = newDataset$date), median)
    print(medianSteps2)

    ##          date x
    ## 1  2012-10-01 0
    ## 2  2012-10-02 0
    ## 3  2012-10-03 0
    ## 4  2012-10-04 0
    ## 5  2012-10-05 0
    ## 6  2012-10-06 0
    ## 7  2012-10-07 0
    ## 8  2012-10-08 0
    ## 9  2012-10-09 0
    ## 10 2012-10-10 0
    ## 11 2012-10-11 0
    ## 12 2012-10-12 0
    ## 13 2012-10-13 0
    ## 14 2012-10-14 0
    ## 15 2012-10-15 0
    ## 16 2012-10-16 0
    ## 17 2012-10-17 0
    ## 18 2012-10-18 0
    ## 19 2012-10-19 0
    ## 20 2012-10-20 0
    ## 21 2012-10-21 0
    ## 22 2012-10-22 0
    ## 23 2012-10-23 0
    ## 24 2012-10-24 0
    ## 25 2012-10-25 0
    ## 26 2012-10-26 0
    ## 27 2012-10-27 0
    ## 28 2012-10-28 0
    ## 29 2012-10-29 0
    ## 30 2012-10-30 0
    ## 31 2012-10-31 0
    ## 32 2012-11-01 0
    ## 33 2012-11-02 0
    ## 34 2012-11-03 0
    ## 35 2012-11-04 0
    ## 36 2012-11-05 0
    ## 37 2012-11-06 0
    ## 38 2012-11-07 0
    ## 39 2012-11-08 0
    ## 40 2012-11-09 0
    ## 41 2012-11-10 0
    ## 42 2012-11-11 0
    ## 43 2012-11-12 0
    ## 44 2012-11-13 0
    ## 45 2012-11-14 0
    ## 46 2012-11-15 0
    ## 47 2012-11-16 0
    ## 48 2012-11-17 0
    ## 49 2012-11-18 0
    ## 50 2012-11-19 0
    ## 51 2012-11-20 0
    ## 52 2012-11-21 0
    ## 53 2012-11-22 0
    ## 54 2012-11-23 0
    ## 55 2012-11-24 0
    ## 56 2012-11-25 0
    ## 57 2012-11-26 0
    ## 58 2012-11-27 0
    ## 59 2012-11-28 0
    ## 60 2012-11-29 0
    ## 61 2012-11-30 0

    # Q: Do these values differ from the estimates from the first part of the assignment? 
    # A: The histogram shows more values for 0 steps; dates previously missing appear now with mean and median values

    # Q: What is the impact of imputing missing data on the estimates of the total daily number of steps?
    # A: In this case, since I replaced NA with 0, it has no impact

Are there differences in activity patterns between weekdays and weekends?
-------------------------------------------------------------------------

### Create a new factor variable in the dataset with two levels – “weekday” and “weekend” indicating whether a given date is a weekday or weekend day.

    # Will ignore missing values for this step

    weekDataset <- data
    weekDataset$weekday <- ifelse(weekdays(as.Date(weekDataset$date)) %in% c("Saturday", "Sunday"), "weekend", "weekday")

### Make a panel plot containing a time series plot of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all weekday days or weekend days (y-axis).

    weekdayDataset <- weekDataset %>% filter(weekday == "weekday")
    timeSeriesData2 <- aggregate(weekdayDataset$steps, list(interval = weekdayDataset$interval), mean)
    timeSeries2 <- ggplot(data = timeSeriesData2, aes(x = interval, y = x)) + geom_line() + labs(x = "5-minute interval", y = "Average Steps", title = "Average steps time series - Weekdays")
    print(timeSeries2)

![](PA1_template_files/figure-markdown_strict/weekdays_plot-1.png)

    weekendDataset <- weekDataset %>% filter(weekday != "weekday")
    timeSeriesData3 <- aggregate(weekendDataset$steps, list(interval = weekendDataset$interval), mean)
    timeSeries3 <- ggplot(data = timeSeriesData3, aes(x = interval, y = x)) + geom_line() + labs(x = "5-minute interval", y = "Average Steps", title = "Average steps time series - Weekends")
    print(timeSeries3)

![](PA1_template_files/figure-markdown_strict/weekdays_plot-2.png)
