---
layout : post
title: "Data_Merge"
author: "ooDoo"
date: 2018-01-26
categories : study
cover : /assets/instacode_sizedown.png
---





# 1. cbind / rbind

## 1) rbind (row + bind = `rbind`)
 : 행 결합 (위 + 아래) : rbind(A, B)  
 두 데이터의 *컬럼*이 동일해야 함

{% highlight r %}
df_1 <- data.frame(id = c("1", "2" ,"3" ,"4"), 
                   name = c("A", "B", "C", "D"))

df_2 <- data.frame(id = c("5", "6", "7"), 
                   name = c("E", "F", "G"))

df <- rbind(df_1, df_2)
# combine 2 data by row
df
{% endhighlight %}



{% highlight text %}
##   id name
## 1  1    A
## 2  2    B
## 3  3    C
## 4  4    D
## 5  5    E
## 6  6    F
## 7  7    G
{% endhighlight %}


## 2) cbind (column + bind = `cbind`)
 : 열 결합 (왼쪽 열 + 오른쪽 열) : cbind(A, B)
 두 데이터의 *행*이 동일해야 함. 

{% highlight r %}
df_1 <- data.frame(id = c("1", "2" ,"3" ,"4"), 
                   name = c("Apple", "Bob", "Charlie", "Damn"))

df_2 <- data.frame(gender = c("M", "F", "M", "M"), 
                   money = c("100,000", "2,000", "50,000","100" ))


df <- cbind(df_1, df_2)
# combine 2 data by column
df
{% endhighlight %}



{% highlight text %}
##   id    name gender   money
## 1  1   Apple      M 100,000
## 2  2     Bob      F   2,000
## 3  3 Charlie      M  50,000
## 4  4    Damn      M     100
{% endhighlight %}



# 2. merge
 : 두 데이터의 열을 결합할 때 단순히 옆으로만 붙이는 것이 아니라,
  각각의 *key*값에 맞춰서 데이터를 조합해서 붙이는 방식 
  두 데이터에 *key*를 맞춰줄 수 있는 동일한 *column*이 있어야 함

{% highlight r %}
df_1 <- data.frame(id = c("1", "2" ,"3" ,"4"), 
                   name = c("Apple", "Bob", "Charlie", "Damn"))

df_2 <- data.frame(id = c("1", "4" ,"2" ,"3"),
                   gender = c("M", "F", "M", "M"), 
                   money = c("100,000", "2,000", "50,000","100" ))


df <- merge(df_1, df_2)
df
{% endhighlight %}



{% highlight text %}
##   id    name gender   money
## 1  1   Apple      M 100,000
## 2  2     Bob      M  50,000
## 3  3 Charlie      M     100
## 4  4    Damn      F   2,000
{% endhighlight %}

 그러나 아래 데이터와 같이 서로 데이터를 결합할 경우 손실되는 값들이 발생할때, 원하는 데이터의 일부를 살리기 위해 `join`함수를 사용해야 한다.

{% highlight r %}
df_1 <- data.frame(id = c("1", "2" ,"3" ,"4","7","8"), 
                   name = c("Apple", "Bob", "Charlie", "Damn", "Emily","Foodding"))

df_2 <- data.frame(id = c("1", "4" ,"2" ,"6" ,"3", "5"),
                   gender = c("M", "F", "M", "M", "F", "F"), 
                   money = c("100,000", "2,000", "5,000","100", "70"," 900" ))


df <- merge(df_1, df_2)

df
{% endhighlight %}



{% highlight text %}
##   id    name gender   money
## 1  1   Apple      M 100,000
## 2  2     Bob      M   5,000
## 3  3 Charlie      F      70
## 4  4    Damn      F   2,000
{% endhighlight %}


![4가지 join 함수](http://cfile4.uf.tistory.com/image/2464D13755B602E72AFAF0)


## 1) Inner join 

{% highlight r %}
df_1 <- data.frame(id = c("1", "2" ,"3" ,"4","7","8"), 
                   name = c("Apple", "Bob", "Charlie", "Damn", "Emily","Foodding"))

df_2 <- data.frame(id = c("1", "4" ,"2" ,"6" ,"3", "5"),
                   gender = c("M", "F", "M", "M", "F", "F"), 
                   money = c("100,000", "2,000", "5,000","100", "70"," 900" ))

df <- merge(x = df_1, y = df_2,
            by = "id")
df
{% endhighlight %}



{% highlight text %}
##   id    name gender   money
## 1  1   Apple      M 100,000
## 2  2     Bob      M   5,000
## 3  3 Charlie      F      70
## 4  4    Damn      F   2,000
{% endhighlight %}

## 2) Outer join

{% highlight r %}
df_1 <- data.frame(id = c(1, 2 ,3 ,4,7,8), 
                   name = c("Apple", "Bob", "Charlie", "Damn", "Emily","Foodding"))

df_2 <- data.frame(id = c(1, 4 ,2 ,6 ,3, 5),
                   gender = c("M", "F", "M", "M", "F", "F"), 
                   money = c("100,000", "2,000", "5,000","100", "70"," 900" ))

df <- merge(x = df_1, y = df_2,
            by = "id", sort = T,
            all = TRUE)
df
{% endhighlight %}



{% highlight text %}
##   id     name gender   money
## 1  1    Apple      M 100,000
## 2  2      Bob      M   5,000
## 3  3  Charlie      F      70
## 4  4     Damn      F   2,000
## 5  5     <NA>      F     900
## 6  6     <NA>      M     100
## 7  7    Emily   <NA>    <NA>
## 8  8 Foodding   <NA>    <NA>
{% endhighlight %}

## 3) Left Outer join

{% highlight r %}
df_1 <- data.frame(id = c(1, 2 ,3 ,4,7,8), 
                   name = c("Apple", "Bob", "Charlie", "Damn", "Emily","Foodding"))

df_2 <- data.frame(id = c(1, 4 ,2 ,6 ,3, 5),
                   gender = c("M", "F", "M", "M", "F", "F"), 
                   money = c("100,000", "2,000", "5,000","100", "70"," 900" ))

df <- merge(x = df_1, y = df_2,
            by = "id", sort = T,
            all.x = TRUE)
df
{% endhighlight %}



{% highlight text %}
##   id     name gender   money
## 1  1    Apple      M 100,000
## 2  2      Bob      M   5,000
## 3  3  Charlie      F      70
## 4  4     Damn      F   2,000
## 5  7    Emily   <NA>    <NA>
## 6  8 Foodding   <NA>    <NA>
{% endhighlight %}

## 4) Right Outer join

{% highlight r %}
df_1 <- data.frame(id = c(1, 2 ,3 ,4,7,8), 
                   name = c("Apple", "Bob", "Charlie", "Damn", "Emily","Foodding"))

df_2 <- data.frame(id = c(1, 4 ,2 ,6 ,3, 5),
                   gender = c("M", "F", "M", "M", "F", "F"), 
                   money = c("100,000", "2,000", "5,000","100", "70"," 900" ))

df <- merge(x = df_1, y = df_2,
            by = "id", sort = T,
            all.y = TRUE)
df
{% endhighlight %}



{% highlight text %}
##   id    name gender   money
## 1  1   Apple      M 100,000
## 2  2     Bob      M   5,000
## 3  3 Charlie      F      70
## 4  4    Damn      F   2,000
## 5  5    <NA>      F     900
## 6  6    <NA>      M     100
{% endhighlight %}

# 3. reshape by `reshape2`function
:우리가 보기에 편한 WIDE LAYOUT을 컴퓨터에게 편한(시각화가 가능한) LONG LAYOUT으로 변환 


함수명|목적
:---:|:---:
`WIDE LAYOUT`|하나의 행에 여러개의 정보가 들어 있음
`LONG LAYOUT`|하나의 행에 하나의 정보만 들어가 있음





{% highlight r %}
# Wide Layout 
students_wide <- data.frame(student = c("A", "B"),
    korean = c(80, 68),
    math = c(72, 94),
    english = c(77, 82))
students_wide
{% endhighlight %}



{% highlight text %}
##   student korean math english
## 1       A     80   72      77
## 2       B     68   94      82
{% endhighlight %}

 

{% highlight r %}
# Long Layout
students_long <- data.frame(student = rep(c("A", "B")),
    subject = rep(c("korean", "math", "english"), each = 2),
    score = c(80, 68, 72, 94, 77, 82))
students_long
{% endhighlight %}



{% highlight text %}
##   student subject score
## 1       A  korean    80
## 2       B  korean    68
## 3       A    math    72
## 4       B    math    94
## 5       A english    77
## 6       B english    82
{% endhighlight %}




## 1) melt 
: Wide Layout --> Long Layout
*다양한 변수들을 한번에 그래프로 그려내려 할때 유용하게 사용.*

{% highlight r %}
molten_airq <- melt(airquality,
        id.vars = c("Month", "Day"),         # it also take 2 id variables
        variable.name = "climate_variable",  # categories column 
        value.name = "climate_value")        # value column
head(molten_airq)
{% endhighlight %}



{% highlight text %}
##   Month Day climate_variable climate_value
## 1     5   1            Ozone            41
## 2     5   2            Ozone            36
## 3     5   3            Ozone            12
## 4     5   4            Ozone            18
## 5     5   5            Ozone            NA
## 6     5   6            Ozone            28
{% endhighlight %}


## 2) dcast

{% highlight r %}
wide_airq <- dcast(molten_airq, Month+Day ~ climate_variable)  # using '+', we can dcast 2 id variables
head(wide_airq)
{% endhighlight %}



{% highlight text %}
##   Month Day Ozone Solar.R Wind Temp
## 1     5   1    41     190  7.4   67
## 2     5   2    36     118  8.0   72
## 3     5   3    12     149 12.6   74
## 4     5   4    18     313 11.5   62
## 5     5   5    NA      NA 14.3   56
## 6     5   6    28      NA 14.9   66
{% endhighlight %}

