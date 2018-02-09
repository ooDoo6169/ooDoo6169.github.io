---
layout : post
title: "Data-Handling"
author: "ooDoo"
date: 2018-01-08
categories : study
cover : /assets/article_images/title/IMG_8493.JPG
---



#1. apply
: `apply` 함수는 데이터의 행 또는 열에 동일한 연산을 가하기 위해 사용한다. 여기서 확인하고자 하는 `apply`, `sappy`, `lapply ` 3가지로 각각의 목적과 용법은 아래 표와 같다

함수명|목적|용법
-|--|-
`apply`|기본적 apply|`apply(x,행|열,함수)`
`lapply`|산출물 :list형식|`lapply(x,행|열,함수)` 
`sapply`|산출물 :vector형식|`sapply(x,행|열,함수)`

실습 데이터는 *iris*라는 내장 데이터로,추가적인 연구 자료는 [여기](https://www.r-statistics.com/wp-content/uploads/2012/01/source_https.r.txt)에서 구할 수 있다.

{% highlight text %}
##   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
## 1          5.1         3.5          1.4         0.2  setosa
## 2          4.9         3.0          1.4         0.2  setosa
## 3          4.7         3.2          1.3         0.2  setosa
## 4          4.6         3.1          1.5         0.2  setosa
## 5          5.0         3.6          1.4         0.2  setosa
## 6          5.4         3.9          1.7         0.4  setosa
{% endhighlight %}

##1) apply

{% highlight r %}
apply(X = iris[1:20,1:4], MARGIN = 1,FUN =  mean) # MARGIN =1: row 
{% endhighlight %}



{% highlight text %}
##     1     2     3     4     5     6     7     8     9    10    11    12 
## 2.550 2.375 2.350 2.350 2.550 2.850 2.425 2.525 2.225 2.400 2.700 2.500 
##    13    14    15    16    17    18    19    20 
## 2.325 2.125 2.800 3.000 2.750 2.575 2.875 2.675
{% endhighlight %}



{% highlight r %}
apply(X = iris[ ,1:4], MARGIN = 2,FUN =  mean) # MARGIN =2: column
{% endhighlight %}



{% highlight text %}
## Sepal.Length  Sepal.Width Petal.Length  Petal.Width 
##     5.843333     3.057333     3.758000     1.199333
{% endhighlight %}



{% highlight r %}
apply(X = iris[1:20 ,1:4], MARGIN = 2,FUN =  diff)
{% endhighlight %}



{% highlight text %}
##    Sepal.Length Sepal.Width Petal.Length Petal.Width
## 2          -0.2        -0.5          0.0         0.0
## 3          -0.2         0.2         -0.1         0.0
## 4          -0.1        -0.1          0.2         0.0
## 5           0.4         0.5         -0.1         0.0
## 6           0.4         0.3          0.3         0.2
## 7          -0.8        -0.5         -0.3        -0.1
## 8           0.4         0.0          0.1        -0.1
## 9          -0.6        -0.5         -0.1         0.0
## 10          0.5         0.2          0.1        -0.1
## 11          0.5         0.6          0.0         0.1
## 12         -0.6        -0.3          0.1         0.0
## 13          0.0        -0.4         -0.2        -0.1
## 14         -0.5         0.0         -0.3         0.0
## 15          1.5         1.0          0.1         0.1
## 16         -0.1         0.4          0.3         0.2
## 17         -0.3        -0.5         -0.2         0.0
## 18         -0.3        -0.4          0.1        -0.1
## 19          0.6         0.3          0.3         0.0
## 20         -0.6         0.0         -0.2         0.0
{% endhighlight %}
`diff` : Returns suitably lagged and iterated differences. 

##2) lapply
 : 결과물을 dataFram으로 변환 용이

{% highlight r %}
lapply(iris[ ,1:4],mean) 
{% endhighlight %}



{% highlight text %}
## $Sepal.Length
## [1] 5.843333
## 
## $Sepal.Width
## [1] 3.057333
## 
## $Petal.Length
## [1] 3.758
## 
## $Petal.Width
## [1] 1.199333
{% endhighlight %}

##3) sapply

{% highlight r %}
sapply(iris[ ,1:4],mean)
{% endhighlight %}



{% highlight text %}
## Sepal.Length  Sepal.Width Petal.Length  Petal.Width 
##     5.843333     3.057333     3.758000     1.199333
{% endhighlight %}
결과적으로 세가지 기능이 크게 차이가 없으니 편한걸로 사용하면 됨.




#2. which & within
##1) which
: 원하는 조건의 컬럼 혹은 로우만 가져오는 함수

{% highlight text %}
##                    mpg cyl disp  hp drat    wt  qsec vs am gear carb
## Mazda RX4         21.0   6  160 110 3.90 2.620 16.46  0  1    4    4
## Mazda RX4 Wag     21.0   6  160 110 3.90 2.875 17.02  0  1    4    4
## Datsun 710        22.8   4  108  93 3.85 2.320 18.61  1  1    4    1
## Hornet 4 Drive    21.4   6  258 110 3.08 3.215 19.44  1  0    3    1
## Hornet Sportabout 18.7   8  360 175 3.15 3.440 17.02  0  0    3    2
## Valiant           18.1   6  225 105 2.76 3.460 20.22  1  0    3    1
{% endhighlight %}

{% highlight r %}
mtcars[which(mtcars$mpg <= 20 & mtcars$cyl == 6), ]
{% endhighlight %}



{% highlight text %}
##               mpg cyl  disp  hp drat   wt  qsec vs am gear carb
## Valiant      18.1   6 225.0 105 2.76 3.46 20.22  1  0    3    1
## Merc 280     19.2   6 167.6 123 3.92 3.44 18.30  1  0    4    4
## Merc 280C    17.8   6 167.6 123 3.92 3.44 18.90  1  0    4    4
## Ferrari Dino 19.7   6 145.0 175 3.62 2.77 15.50  0  1    5    6
{% endhighlight %}



{% highlight r %}
mtcars[, -which(names(mtcars) == "wt")]
{% endhighlight %}



{% highlight text %}
##                      mpg cyl  disp  hp drat  qsec vs am gear carb
## Mazda RX4           21.0   6 160.0 110 3.90 16.46  0  1    4    4
## Mazda RX4 Wag       21.0   6 160.0 110 3.90 17.02  0  1    4    4
## Datsun 710          22.8   4 108.0  93 3.85 18.61  1  1    4    1
## Hornet 4 Drive      21.4   6 258.0 110 3.08 19.44  1  0    3    1
## Hornet Sportabout   18.7   8 360.0 175 3.15 17.02  0  0    3    2
## Valiant             18.1   6 225.0 105 2.76 20.22  1  0    3    1
## Duster 360          14.3   8 360.0 245 3.21 15.84  0  0    3    4
## Merc 240D           24.4   4 146.7  62 3.69 20.00  1  0    4    2
## Merc 230            22.8   4 140.8  95 3.92 22.90  1  0    4    2
## Merc 280            19.2   6 167.6 123 3.92 18.30  1  0    4    4
## Merc 280C           17.8   6 167.6 123 3.92 18.90  1  0    4    4
## Merc 450SE          16.4   8 275.8 180 3.07 17.40  0  0    3    3
## Merc 450SL          17.3   8 275.8 180 3.07 17.60  0  0    3    3
## Merc 450SLC         15.2   8 275.8 180 3.07 18.00  0  0    3    3
## Cadillac Fleetwood  10.4   8 472.0 205 2.93 17.98  0  0    3    4
## Lincoln Continental 10.4   8 460.0 215 3.00 17.82  0  0    3    4
## Chrysler Imperial   14.7   8 440.0 230 3.23 17.42  0  0    3    4
## Fiat 128            32.4   4  78.7  66 4.08 19.47  1  1    4    1
## Honda Civic         30.4   4  75.7  52 4.93 18.52  1  1    4    2
## Toyota Corolla      33.9   4  71.1  65 4.22 19.90  1  1    4    1
## Toyota Corona       21.5   4 120.1  97 3.70 20.01  1  0    3    1
## Dodge Challenger    15.5   8 318.0 150 2.76 16.87  0  0    3    2
## AMC Javelin         15.2   8 304.0 150 3.15 17.30  0  0    3    2
## Camaro Z28          13.3   8 350.0 245 3.73 15.41  0  0    3    4
## Pontiac Firebird    19.2   8 400.0 175 3.08 17.05  0  0    3    2
## Fiat X1-9           27.3   4  79.0  66 4.08 18.90  1  1    4    1
## Porsche 914-2       26.0   4 120.3  91 4.43 16.70  0  1    5    2
## Lotus Europa        30.4   4  95.1 113 3.77 16.90  1  1    5    2
## Ford Pantera L      15.8   8 351.0 264 4.22 14.50  0  1    5    4
## Ferrari Dino        19.7   6 145.0 175 3.62 15.50  0  1    5    6
## Maserati Bora       15.0   8 301.0 335 3.54 14.60  0  1    5    8
## Volvo 142E          21.4   4 121.0 109 4.11 18.60  1  1    4    2
{% endhighlight %}

##2) within
   (1)mtcars의 mpg의 평균보다 크거나 같은 경우, 작은 경우의 범주형 변수를 추가
   (2) wt 변수를 삭제
 : within 구문을 통해 복제하여 수정/개조, formula를 사용하여 변수를 생성

{% highlight r %}
class_mtcars <- within(mtcars, {     
  mpg_class <- ifelse(mpg >= mean(mpg), "U", "L")
  rm(wt)
})
head(class_mtcars)
{% endhighlight %}



{% highlight text %}
##                    mpg cyl disp  hp drat  qsec vs am gear carb mpg_class
## Mazda RX4         21.0   6  160 110 3.90 16.46  0  1    4    4         U
## Mazda RX4 Wag     21.0   6  160 110 3.90 17.02  0  1    4    4         U
## Datsun 710        22.8   4  108  93 3.85 18.61  1  1    4    1         U
## Hornet 4 Drive    21.4   6  258 110 3.08 19.44  1  0    3    1         U
## Hornet Sportabout 18.7   8  360 175 3.15 17.02  0  0    3    2         L
## Valiant           18.1   6  225 105 2.76 20.22  1  0    3    1         L
{% endhighlight %}



#3. cut
 : 연속형 변수를 쉽게 범주화 할때 사용 

{% highlight r %}
mtcars$disp_class <- NULL
mtcars$disp_class <- cut(mtcars$disp, breaks = 3, labels = c("L","M","H"))
head(mtcars)
{% endhighlight %}



{% highlight text %}
##                    mpg cyl disp  hp drat    wt  qsec vs am gear carb
## Mazda RX4         21.0   6  160 110 3.90 2.620 16.46  0  1    4    4
## Mazda RX4 Wag     21.0   6  160 110 3.90 2.875 17.02  0  1    4    4
## Datsun 710        22.8   4  108  93 3.85 2.320 18.61  1  1    4    1
## Hornet 4 Drive    21.4   6  258 110 3.08 3.215 19.44  1  0    3    1
## Hornet Sportabout 18.7   8  360 175 3.15 3.440 17.02  0  0    3    2
## Valiant           18.1   6  225 105 2.76 3.460 20.22  1  0    3    1
##                   disp_class
## Mazda RX4                  L
## Mazda RX4 Wag              L
## Datsun 710                 L
## Hornet 4 Drive             M
## Hornet Sportabout          H
## Valiant                    M
{% endhighlight %}
 
 
 
#4. strsplit
 : 글자를 쪼개 분석할 때 사용하는 함수로, 자세한 용법은 다른편에서 다시 다루기로 하자.

{% highlight r %}
head(strsplit(rownames(mtcars), split = " "))
{% endhighlight %}



{% highlight text %}
## [[1]]
## [1] "Mazda" "RX4"  
## 
## [[2]]
## [1] "Mazda" "RX4"   "Wag"  
## 
## [[3]]
## [1] "Datsun" "710"   
## 
## [[4]]
## [1] "Hornet" "4"      "Drive" 
## 
## [[5]]
## [1] "Hornet"     "Sportabout"
## 
## [[6]]
## [1] "Valiant"
{% endhighlight %}



{% highlight r %}
mtcars$brand <- sapply(strsplit(rownames(mtcars), split = " "), "[", 1)
head(mtcars)
{% endhighlight %}



{% highlight text %}
##                    mpg cyl disp  hp drat    wt  qsec vs am gear carb
## Mazda RX4         21.0   6  160 110 3.90 2.620 16.46  0  1    4    4
## Mazda RX4 Wag     21.0   6  160 110 3.90 2.875 17.02  0  1    4    4
## Datsun 710        22.8   4  108  93 3.85 2.320 18.61  1  1    4    1
## Hornet 4 Drive    21.4   6  258 110 3.08 3.215 19.44  1  0    3    1
## Hornet Sportabout 18.7   8  360 175 3.15 3.440 17.02  0  0    3    2
## Valiant           18.1   6  225 105 2.76 3.460 20.22  1  0    3    1
##                   disp_class   brand
## Mazda RX4                  L   Mazda
## Mazda RX4 Wag              L   Mazda
## Datsun 710                 L  Datsun
## Hornet 4 Drive             M  Hornet
## Hornet Sportabout          H  Hornet
## Valiant                    M Valiant
{% endhighlight %}

  
  
#5 %in%
: 왼쪽(비교하고자 하는 값)과 오른쪽(비교대상)을 비교해서 해당 인자의 존재 여부에 따라 TRUE/FALSE를 돌려주는 binary operator

{% highlight text %}
##      brand  disp
## 1      Bmw 435.7
## 2  Hyundai 417.2
## 3      kia 403.0
## 4     Merc 415.7
## 5    Chevy 430.7
## 6 Chrysler 424.0
{% endhighlight %}

{% highlight r %}
dataset$brand %in% mtcars$brand
{% endhighlight %}



{% highlight text %}
## [1] FALSE FALSE FALSE  TRUE FALSE  TRUE
{% endhighlight %}



{% highlight r %}
sum(dataset$brand %in% mtcars$brand)
{% endhighlight %}



{% highlight text %}
## [1] 2
{% endhighlight %}



{% highlight r %}
dataset[dataset$brand %in% mtcars$brand,]
{% endhighlight %}



{% highlight text %}
##      brand  disp
## 4     Merc 415.7
## 6 Chrysler 424.0
{% endhighlight %}


#6. dplyr


##1) dplyr: `filter`
 : 모든 컬럼은 존재한채, 조건만 실행

{% highlight r %}
filter(flights, !month <= 5 , !month >= 9) -> flights_2
table(flights$month)
{% endhighlight %}



{% highlight text %}
## 
##     1     2     3     4     5     6     7     8     9    10    11    12 
## 27004 24951 28834 28330 28796 28243 29425 29327 27574 28889 27268 28135
{% endhighlight %}



{% highlight r %}
filter(flights,dep_time >= 1630)
filter(flights, month ==1 , dep_time >= 1630) # if you wanna 2 conditional option, just use ','
{% endhighlight %}

##2) dplyr: `select`
 : 원하는 컬럼을 선택하는 함수

{% highlight r %}
select(flights, dep_time, arr_time) # select "dep_time", "arr_time"  column
select(flights, month:arr_delay) # bring multiple column using ":", also you could bring the column as number
#if you want bring the all column which contain "time" word in the name, time using [contains()]
select(flights, contains('time'))
#also subtract the all column whic contain "time" word, using [-contains()]
select(flights, -contains('time'))
{% endhighlight %}


##3) dplyr: `arrange`
 : row 정렬

{% highlight r %}
arrange(flights, distance)
arrange(flights, desc(distance)) # descent arrangement as "distance" column
arrange(flights, distance, dep_time) # arrnage "distance" column first, and secondly arragne as "dep_time"  
{% endhighlight %}


##4) dplyr: `mutate` 
 : 기존 변수를 토대로 새로운 변수 생성시 사용 !! 중요!! 

{% highlight r %}
# speed = distance / time
flightsSpeed <- mutate(flights, speed = distance /air_time * 60) # the measue of distance is miles per hour, so mulitple 60  
select(flightsSpeed, distance, air_time,speed)
{% endhighlight %}


##5) dplyr: `summarize` 
 : 말그대로 데이터를 조건별로 정리하여 사용하는 함수로, 활용도가 높으니 다양한 방식으로 응용해 볼 것

{% highlight r %}
Population <- data.frame(No = 1:6, Region = rep(c("Europe", "Asia", "N.America"), each = 2),
    Nationality = c("England", "Germany", "Korea", "Japan", "Canada", "USA"),
    Population = c(53.8, 80.7, 50, 126.3, 36.2, 324))
Population
{% endhighlight %}



{% highlight text %}
##   No    Region Nationality Population
## 1  1    Europe     England       53.8
## 2  2    Europe     Germany       80.7
## 3  3      Asia       Korea       50.0
## 4  4      Asia       Japan      126.3
## 5  5 N.America      Canada       36.2
## 6  6 N.America         USA      324.0
{% endhighlight %}

{% highlight r %}
Population%>%
    group_by(Region)%>%
    summarise(Average = mean(Population))
{% endhighlight %}


{% highlight r %}
plot(Population%>%
    group_by(Region)%>%
    summarise(Average = mean(Population)))
{% endhighlight %}

![plot of chunk unnamed-chunk-19](/assets/R_study/2018-01-13-Data-Handling/unnamed-chunk-19-1.png)



















