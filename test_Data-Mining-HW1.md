Data Mining HW1
================
Wen-Hsin Chang
2021/1/29

## Q1 Data visualization:gas prices

\#The theories

1)  Gas stations charge more if they lack direct competition in sight
    (boxplot).

![](test_Data-Mining-HW1_files/figure-gfm/unnamed-chunk-1-1.png)<!-- -->

The theory seems to be unsupported by the data. Specifically, the box
plot shows that gas station without competitors sets higher price.

2)  The richer the area, the higher the gas price (scatter plot).

![](test_Data-Mining-HW1_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

The theory seems to be supported by the data. Specifically, the scatter
plot shows that richer areas has higher price.

3)  Shell charges more than other brands (bar plot).

![](test_Data-Mining-HW1_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

The theory seems to be supported by the data, but to a lesser degree.
Specifically, the bar plot shows that Shell charges slightly more than
other brands.

4)  Gas stations at stoplights charge more (faceted histogram).

![](test_Data-Mining-HW1_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

The theory seems to be supported by the data. Specifically, the faceted
histogram shows that Gas stations at stoplights charge more. We can use
the skewness of the distribution to help our assessment.

5)  Gas stations with direct highway access charge more (your choice of
    plot).

![](test_Data-Mining-HW1_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

The theory seems to be supported by the data. Specifically, the box plot
shows that Gas stations with direct highway access charge more.

## Q2 Data visualization:a bike share network

1)  Plot A: a line graph showing average bike rentals (Avg.Rentals)
    versus hour of the day (hr).

![](test_Data-Mining-HW1_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->
The average rental spikes at around 8 am and 5pm, which makes intuitive
sense because people may commute by rental bike to avoid traffic jams.

2)  Plot B:a faceted line graph showing average bike rentals versus hour
    of the day, faceted according to whether it is a working day

![](test_Data-Mining-HW1_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

On a typical working day, bike rental spikes at around 8 am and 5 pm but
on a typical weekend, bike rental spikes in the afternoon.

c.)Plot C: a faceted bar plot showing average ridership during the 8 AM
hour by weather situation code (weathersit), faceted according to
whether it is a working day or not

![](test_Data-Mining-HW1_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

Bike rental spikes (vs plunges) when the weather is good (vs bad). The
theory holds for both working day and weekend.

## Q3 Data visualization:Flights at ABIA

1)  What is the best time of day to fly to minimize delays (I do not
    care about arriving early) ? Does this change by airline?

![](test_Data-Mining-HW1_files/figure-gfm/unnamed-chunk-11-1.png)<!-- -->

Based on the result above, on average, 18-24 pm is more likely to
encounter arrival delay (worst time to fly), and 0-6 am is less likely
to encounter arrival delay (best time to fly).

![](test_Data-Mining-HW1_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->
Although 18-24 pm is more likely to encounter arrival delay, the result
changes by airline. For instance, airline“9E” is more likely to delay at
0-6 am, and airline “UA” is more likely to delay at 12-18 pm.

B.)What is the best time of year to fly to minimize delays? Does this
change by destination?

![](test_Data-Mining-HW1_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->
Based on the result above, the best time of the year to fly seems to be
May and the worst time to fly seems to be December, but the result
varies by destination.

![](test_Data-Mining-HW1_files/figure-gfm/unnamed-chunk-14-1.png)<!-- -->
For instance, the best time to fly to “AUS” airport seems to be October,
and the best time to fly to “EWR” seems to be January.

C.)What are the bad airports to fly?

![](test_Data-Mining-HW1_files/figure-gfm/unnamed-chunk-15-1.png)<!-- -->

I focus on some of the most popular airport and find that, based on the
result above, “EWR” and “SFO” are two of the airports that delay the
most. The result makes intuitive sense since New York and San Francisco
are two of the most popular destinations in the US.

## Q4 K-nearest neighbots

\#Trim Level filter:350

``` r
trim_350=sclass%>%filter(trim==350)
```

\#train/test split (0.1/0.9)

``` r
# Make a train-test split
trim_350_split =  initial_split(trim_350, prop=0.9)
trim_350_train = training(trim_350_split)
trim_350_test  = testing(trim_350_split)
```

KNN with K = 2

``` r
# KNN with K = 2
knn2 = knnreg(price ~ mileage, data=trim_350_train , k=2)
rmse(knn2, trim_350_test)
```

    ## [1] 12107.98

KNN with K = 5

``` r
# KNN with K =5
knn5 = knnreg(price ~ mileage, data=trim_350_train , k=5)
rmse(knn5, trim_350_test)
```

    ## [1] 10569.19

KNN with K = 10

``` r
# KNN with K =10
knn10 = knnreg(price ~ mileage, data=trim_350_train , k=10)
rmse(knn10, trim_350_test)
```

    ## [1] 10173.71

\#RMSE versus K

![](test_Data-Mining-HW1_files/figure-gfm/unnamed-chunk-22-1.png)<!-- -->
 \#Optimal at K=17…

![](test_Data-Mining-HW1_files/figure-gfm/unnamed-chunk-23-1.png)<!-- -->

\#Trim Level filter:65AMG

``` r
trim_65AMG=sclass%>%filter(trim=='65 AMG')
```

\#train/test split (0.1/0.9)

``` r
# Make a train-test split
trim_65AMG_split =  initial_split(trim_65AMG, prop=0.9)
trim_65AMG_train = training(trim_65AMG_split)
trim_65AMG_test  = testing(trim_65AMG_split)
```

KNN with K = 2

``` r
# KNN with K = 2
knn2 = knnreg(price ~ mileage, data=trim_65AMG_train , k=2)
rmse(knn2, trim_65AMG_test)
```

    ## [1] 20142.91

KNN with K = 5

``` r
# KNN with K = 5
knn5 = knnreg(price ~ mileage, data=trim_65AMG_train , k=5)
rmse(knn5, trim_65AMG_test)
```

    ## [1] 18438.58

KNN with K = 10

``` r
# KNN with K =10
knn10 = knnreg(price ~ mileage, data=trim_65AMG_train , k=10)
rmse(knn10, trim_65AMG_test)
```

    ## [1] 14327.71

\#RMSE versus K

![](test_Data-Mining-HW1_files/figure-gfm/unnamed-chunk-29-1.png)<!-- -->
 \#Optimal at K=6

![](test_Data-Mining-HW1_files/figure-gfm/unnamed-chunk-30-1.png)<!-- -->
According to my train-test split(0.1/0/9) 350 yield slightly greater
value of K, but since the sample is not very big, it depends on the
random process that R assign the train/test split. I think the reason
that two trim has different values of K is mainly because 65 AMG has
smaller data size, and its mileage information varies less.
