---
layout : post
title: "Shelter Animal Outcomes"
author: "ooDoo"
date: 2017-04-11
categories : kaggle
cover : /assets/article_images/title/instacode_sizedown.png
---

#0. SETTING



#1. DATA IMPORT

{% highlight r %}
train <- read_csv("train.csv")
test <- read_csv("test.csv")
#sample_submission <- read_csv("sample_submission.csv")
#head(sample_submission)
#rm(sample_submission)
{% endhighlight %}

##1) DATA CHECK 

{% highlight r %}
# train
head(train)
names(train)
{% endhighlight %}



{% highlight text %}
##  [1] "AnimalID"       "Name"           "DateTime"       "OutcomeType"   
##  [5] "OutcomeSubtype" "AnimalType"     "SexuponOutcome" "AgeuponOutcome"
##  [9] "Breed"          "Color"
{% endhighlight %}



{% highlight r %}
# test
head(test)
names(test)
{% endhighlight %}



{% highlight text %}
## [1] "ID"             "Name"           "DateTime"       "AnimalType"    
## [5] "SexuponOutcome" "AgeuponOutcome" "Breed"          "Color"
{% endhighlight %}
- target variables is only "OutcomeType" 

##2) DATA EXPLORATION

{% highlight r %}
# Check Object variable
unique(train$OutcomeType)
{% endhighlight %}



{% highlight text %}
## [1] "Return_to_owner" "Euthanasia"      "Adoption"        "Transfer"       
## [5] "Died"
{% endhighlight %}



{% highlight r %}
unique(train$OutcomeSubtype)
{% endhighlight %}



{% highlight text %}
##  [1] NA                    "Suffering"           "Foster"             
##  [4] "Partner"             "Offsite"             "SCRP"               
##  [7] "Aggressive"          "Behavior"            "Rabies Risk"        
## [10] "Medical"             "In Kennel"           "In Foster"          
## [13] "Barn"                "Court/Investigation" "Enroute"            
## [16] "At Vet"              "In Surgery"
{% endhighlight %}



{% highlight r %}
# Check what is "Transfer"
unique(train$OutcomeSubtype[train$OutcomeType == "Transfer"])
{% endhighlight %}



{% highlight text %}
## [1] "Partner" "SCRP"    "Barn"    NA
{% endhighlight %}



{% highlight r %}
train%>%
    filter(OutcomeType == "Transfer") %>%
    select(OutcomeSubtype) %>%
    group_by(OutcomeSubtype)%>%
    summarise(count = n())
{% endhighlight %}


{% highlight r %}
# Check the others
unique(train$AnimalType)
{% endhighlight %}



{% highlight text %}
## [1] "Dog" "Cat"
{% endhighlight %}



{% highlight r %}
unique(train$SexuponOutcome) # Sex and whether Neutered or not
{% endhighlight %}



{% highlight text %}
## [1] "Neutered Male" "Spayed Female" "Intact Male"   "Intact Female"
## [5] "Unknown"       NA
{% endhighlight %}



{% highlight r %}
table(train$SexuponOutcome)  # don't count number using "length" function. it counts 1 more number, since name row
{% endhighlight %}



{% highlight text %}
## 
## Intact Female   Intact Male Neutered Male Spayed Female       Unknown 
##          3511          3525          9779          8820          1093
{% endhighlight %}



{% highlight r %}
unique(train$AgeuponOutcome) # it needs to set the same measure to month 
{% endhighlight %}



{% highlight text %}
##  [1] "1 year"    "2 years"   "3 weeks"   "1 month"   "5 months" 
##  [6] "4 years"   "3 months"  "2 weeks"   "2 months"  "10 months"
## [11] "6 months"  "5 years"   "7 years"   "3 years"   "4 months" 
## [16] "12 years"  "9 years"   "6 years"   "1 weeks"   "11 years" 
## [21] "4 weeks"   "7 months"  "8 years"   "11 months" "4 days"   
## [26] "9 months"  "8 months"  "15 years"  "10 years"  "1 week"   
## [31] "0 years"   "14 years"  "3 days"    "6 days"    "5 days"   
## [36] "5 weeks"   "2 days"    "16 years"  "1 day"     "13 years" 
## [41] NA          "17 years"  "18 years"  "19 years"  "20 years"
{% endhighlight %}



{% highlight r %}
table(train$AgeuponOutcome) # it needs to set the same measure to month 
{% endhighlight %}



{% highlight text %}
## 
##   0 years     1 day   1 month    1 week   1 weeks    1 year 10 months 
##        22        66      1281       146       171      3969       457 
##  10 years 11 months  11 years  12 years  13 years  14 years  15 years 
##       446       166       126       234       143        97        85 
##  16 years  17 years  18 years  19 years    2 days  2 months   2 weeks 
##        36        17        10         3        99      3397       529 
##   2 years  20 years    3 days  3 months   3 weeks   3 years    4 days 
##      3742         2       109      1277       659      1823        50 
##  4 months   4 weeks   4 years    5 days  5 months   5 weeks   5 years 
##       888       334      1071        24       652        11       992 
##    6 days  6 months   6 years  7 months   7 years  8 months   8 years 
##        50       588       670       288       531       402       536 
##  9 months   9 years 
##       224       288
{% endhighlight %}



{% highlight r %}
length(unique(train$Breed)) # the number of breed is 1380
{% endhighlight %}



{% highlight text %}
## [1] 1380
{% endhighlight %}



{% highlight r %}
length(unique(train$Color)) # the number of color is 366
{% endhighlight %}



{% highlight text %}
## [1] 366
{% endhighlight %}



{% highlight r %}
head(train)
#View(train)
#View(test)
{% endhighlight %}
*in AgeupounOutcome it needs to set the same measure to day*
*in color and Breed, it needs to classfy higer levels*



#2. FEATURE HANDLING
##1) AGE_STR EXTRACT

{% highlight r %}
Str_Function <- function(x){
    ifelse(str_split(x, "[ ]")[[1]][2] == "day" | str_split(x, "[ ]")[[1]][2] == "days", as.numeric(str_split(x, "[ ]")[[1]][1]),
        ifelse(str_split(x, "[ ]")[[1]][2] == "week" | str_split(x, "[ ]")[[1]][2] == "weeks", as.numeric(str_split(x, "[ ]")[[1]][1]) * 7,
            ifelse(str_split(x, "[ ]")[[1]][2] == "month" | str_split(x, "[ ]")[[1]][2] == "months", as.numeric(str_split(x, "[ ]")[[1]][1]) * 30,
                ifelse(str_split(x, "[ ]")[[1]][2] == "year" | str_split(x, "[ ]")[[1]][2] == "years", as.numeric(str_split(x, "[ ]")[[1]][1]) * 365,
                    ifelse(x == "0 years", 350, NA)))))
    }
{% endhighlight %}

###(1) APPLY STR_FUCTION

{% highlight r %}
# apply Str_Fuction to train
train$AGE <- NULL
train$AGE <- sapply(train$AgeuponOutcome, FUN = Str_Function)
table(is.na(train$AGE))
{% endhighlight %}



{% highlight text %}
## 
## FALSE  TRUE 
## 26711    18
{% endhighlight %}



{% highlight r %}
# apply Str_Fuction to test
test$AGE <- NULL
test$AGE <- sapply(test$AgeuponOutcome, FUN = Str_Function)
{% endhighlight %}
*but there is still 84 NAs in "Ageuponoutcom" variable*

###(2) INTERPOLATE INFORMATION

{% highlight r %}
# Check NA's feature
## Train
train%>%
    dplyr::select(-c(AnimalID, DateTime)) %>%
    filter(is.na(AGE) == TRUE)

## TEST
test%>%
    filter(is.na(AGE) == TRUE)
{% endhighlight %}
*: NA of AGE's feature*
 - 2016.02
 - almost is cat and transfer


{% highlight r %}
# Check distribution
train%>%
    mutate(Income_Year = year(DateTime),
    Income_Month = month(DateTime),
    Income_Day = day(DateTime))%>%
    filter(Income_Year == 2016 & Income_Month == 2,
           Breed == "Domestic Shorthair Mix",
           is.na(AGE) == FALSE,
           AnimalType == "Cat") %>%    
    ggplot(aes(x = OutcomeType, y = AGE, color = OutcomeType)) +
    geom_boxplot() +
    geom_point()
{% endhighlight %}

![plot of chunk unnamed-chunk-9](/assets/R_kaggle/2017-04-11-Shelter-Animal-Outcomes-ooDoo/unnamed-chunk-9-1.png)

{% highlight r %}
# Check dietail value for interpolation
train%>%
    mutate(Income_Year = year(DateTime),
    Income_Month = month(DateTime),
    Income_Day = day(DateTime))%>%
    filter(Income_Year == 2016 & Income_Month == 2,
           Breed == "Domestic Shorthair Mix",
           is.na(AGE) == FALSE,
           AnimalType == "Cat") %>%    
    group_by(OutcomeType)%>%
    summarise(Mid = median(AGE))
    #summarise(Mean = mean(AGE)) 
{% endhighlight %}
*i'm gonna using median, since there is a huge outlier in train case.*

###(3) AGE INTERPOLATE

{% highlight r %}
# train
train$AGE[is.na(train$AGE) == "TRUE"] <- 730 
table(is.na(train$AGE))
{% endhighlight %}



{% highlight text %}
## 
## FALSE 
## 26729
{% endhighlight %}



{% highlight r %}
# test
test$AGE[is.na(test$AGE) == "TRUE"] <- 730 
table(is.na(test$AGE))
{% endhighlight %}



{% highlight text %}
## 
## FALSE 
## 11456
{% endhighlight %}



{% highlight r %}
unique(train$SexuponOutcome)
{% endhighlight %}



{% highlight text %}
## [1] "Neutered Male" "Spayed Female" "Intact Male"   "Intact Female"
## [5] "Unknown"       NA
{% endhighlight %}

##2) FEATURE EXTRACT

{% highlight r %}
FeatureExtract <- function(data){
    data%>%
        # Date Varible
        mutate(Income_Year = year(DateTime),
               Income_Month = as.factor(month(DateTime)),
               Income_Day = day(DateTime)) %>%
        # Change AGE variable as numeric 
        mutate(AGE = as.numeric(AGE))%>%
        # Name and SexuponOutcome Dummy
        mutate(Name = ifelse(is.na(Name)== FALSE , "N_O", "N_X"),
               Neutered_Dummy = ifelse(SexuponOutcome == "Neutered Male" | SexuponOutcome == "Spayed Female", 1 , 0))%>%
        
        # drop the unnecessary column
        select(-c(DateTime, AgeuponOutcome))
}
{% endhighlight %}

{% highlight r %}
# Apply
train_1 <- FeatureExtract(train)
train_1%>%
    select(-c(AnimalID, OutcomeSubtype)) -> train_1
test_1 <- FeatureExtract(test)
{% endhighlight %}

###(1) BREED_PURE

{% highlight r %}
# Breed_Str_Function
Breed_Str_Function <- function(data){
    ifelse(grepl('Mix', data) == TRUE, "Mix",
        ifelse(grepl("/", data) == TRUE,"with", "Pure"))
}
{% endhighlight %}


{% highlight r %}
# apply
train_1$Breed_Pure <- NULL
train_1$Breed_Pure <- sapply(train_1$Breed, FUN = Breed_Str_Function)

test_1$Breed_Pure <- NULL
test_1$Breed_Pure <- sapply(test_1$Breed, FUN = Breed_Str_Function)
{% endhighlight %}


###(2) COLOR_SIMPLE

{% highlight r %}
# Color_Str_Function
Color_Str_Function <- function(data){
    str_split(data, "[/]")[[1]][1]
}
{% endhighlight %}


{% highlight r %}
# apply
train_1$Color_simple <- NULL
train_1$Color_simple <- sapply(train_1$Color, FUN = Color_Str_Function)

test_1$Color_simple <- NULL
test_1$Color_simple <- sapply(test_1$Color, FUN = Color_Str_Function)
{% endhighlight %}



{% highlight r %}
train_1%>%
    group_by(Color)%>%
    summarise(count = n()) %>%
    arrange(desc(count), Color)

train_1%>%
    group_by(Color_simple)%>%
    summarise(count = n()) %>%
    arrange(desc(count), Color_simple)
{% endhighlight %}



###(3) BREED_SIMPLE

{% highlight r %}
i = unique(train_1$AnimalType)[2]
head(train_1$Breed)
{% endhighlight %}



{% highlight text %}
## [1] "Shetland Sheepdog Mix"             "Domestic Shorthair Mix"           
## [3] "Pit Bull Mix"                      "Domestic Shorthair Mix"           
## [5] "Lhasa Apso/Miniature Poodle"       "Cairn Terrier/Chihuahua Shorthair"
{% endhighlight %}



{% highlight r %}
for(i in unique(train_1$AnimalType)){
    train_1%>%
        filter(AnimalType == i)%>%
        group_by(Breed)%>%
        summarise(count = n())%>%
        arrange(desc(count)) -> k 

    assign(paste0('train_',as.factor(i),'Breed Count'), k)
}
head(`train_CatBreed Count`)
head(`train_DogBreed Count`)
{% endhighlight %}
*We could see that there is too much breed speiecs in dog data*


{% highlight r %}
# BREED_Str_Function
Breed_Str_Function <- function(data){
    str_split(data, "[/]")[[1]][1]
}
{% endhighlight %}


{% highlight r %}
# apply
train_1$Breed_simple <- NULL
train_1$Breed_simple <- sapply(train_1$Breed, FUN = Breed_Str_Function)

test_1$Breed_simple <- NULL
test_1$Breed_simple <- sapply(test_1$Breed, FUN = Breed_Str_Function)
{% endhighlight %}


{% highlight r %}
#result
length(unique(train$Breed))  # before simplify
{% endhighlight %}



{% highlight text %}
## [1] 1380
{% endhighlight %}



{% highlight r %}
length(unique(train_1$Breed_simple)) # after simplify
{% endhighlight %}



{% highlight text %}
## [1] 382
{% endhighlight %}


##3) LIST WISE DELETION

{% highlight r %}
# train
nrow(train_1) # 26,729 row, before to list wise deletion
{% endhighlight %}



{% highlight text %}
## [1] 26729
{% endhighlight %}



{% highlight r %}
nrow(train_1[complete.cases(train_1),]) # 26728 row, after list wise deletion 
{% endhighlight %}



{% highlight text %}
## [1] 26728
{% endhighlight %}



{% highlight r %}
train_1[complete.cases(train_1) == FALSE,]
# train_1 <- train_1[complete.cases(train_1) == TRUE,] # if i could know the relation btwn AGE and Sex as Animaltype, i could guess this NA also.  
                                                       # So i'm gonna do this next paragraph

# test
nrow(test_1)
{% endhighlight %}



{% highlight text %}
## [1] 11456
{% endhighlight %}



{% highlight r %}
nrow(test_1[complete.cases(test_1) == FALSE,]) # there is no more NA in test data
{% endhighlight %}



{% highlight text %}
## [1] 0
{% endhighlight %}

###1) RELATIONSHIP BTWN AGE, SEX AS ANIMALTYPE

{% highlight r %}
train%>%
    filter(is.na(SexuponOutcome) == FALSE,
           AnimalType == "Dog",
           Breed == "Dachshund",
           OutcomeType == "Return_to_owner") %>%
    ggplot(aes(x = SexuponOutcome , y = AGE, fill = SexuponOutcome)) +
    geom_boxplot() +
    geom_point() 
{% endhighlight %}

![plot of chunk unnamed-chunk-23](/assets/R_kaggle/2017-04-11-Shelter-Animal-Outcomes-ooDoo/unnamed-chunk-23-1.png)
*Through above graph, this one's Sex might be "Neutered Male"*

###2) INTERPOLATE SexuponOutcome's NA 

{% highlight r %}
# Interpolation
train_1[!complete.cases(train_1),"SexuponOutcome"]  <- "Neutered Male"
train_1[!complete.cases(train_1),"Sex_Dummy"]  <- 1
# check
train_1[complete.cases(train_1) == FALSE,] # now, there is no more NA !
{% endhighlight %}



#3. VISUALIZAION
##1) OUTCOME
###(1) AS NAME EXISTENCE

{% highlight r %}
train_1%>%
    group_by(Name, OutcomeType)%>%
    summarise(count = n()) %>%
    arrange(OutcomeType) %>% 
    ggplot(aes(x = reorder(OutcomeType, count), y = count, fill = Name)) +
    geom_col(position = "dodge")
{% endhighlight %}

![plot of chunk unnamed-chunk-25](/assets/R_kaggle/2017-04-11-Shelter-Animal-Outcomes-ooDoo/unnamed-chunk-25-1.png)

{% highlight r %}
train_1%>%
    mutate(OutcomeType_2 = ifelse(OutcomeType == "Died" | OutcomeType == "Euthanasia", "Bad", "Good")) %>%
    group_by(Name, OutcomeType, OutcomeType_2)%>%
    summarise(count = n()) %>%
    arrange(OutcomeType) %>% 
    ggplot(aes(x = reorder(OutcomeType_2, count), y = count, fill = Name)) +
    geom_col(position = "dodge")
{% endhighlight %}

![plot of chunk unnamed-chunk-25](/assets/R_kaggle/2017-04-11-Shelter-Animal-Outcomes-ooDoo/unnamed-chunk-25-2.png)
*we could see that if animal has name, her pct of transfer or return to owener is increased.*

###(2) AS SEX

{% highlight r %}
table((train_1$SexuponOutcome))
{% endhighlight %}



{% highlight text %}
## 
## Intact Female   Intact Male Neutered Male Spayed Female       Unknown 
##          3511          3525          9780          8820          1093
{% endhighlight %}


{% highlight r %}
for(i in 1:length(unique(train_1$SexuponOutcome))){
train_1%>%
    filter(SexuponOutcome == unique(train_1$SexuponOutcome)[i])%>%
    group_by(OutcomeType)%>%
    summarise(count = n()) %>%
    ggplot(aes(x = OutcomeType, y = count,  fill = OutcomeType)) +
    geom_col(position = "dodge") +
    ggtitle(unique(train_1$SexuponOutcome)[i]) +
    geom_text(aes(label = count)) +
    theme(legend.position="none", 
          axis.text.x = element_text(angle = 90, face = "italic", vjust = 1 ,hjust = 1),
          plot.title = element_text(face = "bold.italic", hjust = 0.5)) -> k
   
     assign(paste0("VIS_",i), k)
}
{% endhighlight %}


{% highlight r %}
library(gridExtra)
grid.arrange(VIS_1,VIS_2, ncol = 2) # neutralization
{% endhighlight %}

![plot of chunk unnamed-chunk-28](/assets/R_kaggle/2017-04-11-Shelter-Animal-Outcomes-ooDoo/unnamed-chunk-28-1.png)

{% highlight r %}
grid.arrange(VIS_3,VIS_4, ncol = 2) # not neutralization
{% endhighlight %}

![plot of chunk unnamed-chunk-28](/assets/R_kaggle/2017-04-11-Shelter-Animal-Outcomes-ooDoo/unnamed-chunk-28-2.png)

{% highlight r %}
VIS_5 # i think, unknown also has some meaning.
{% endhighlight %}

![plot of chunk unnamed-chunk-28](/assets/R_kaggle/2017-04-11-Shelter-Animal-Outcomes-ooDoo/unnamed-chunk-28-3.png)
*i've made a dummy variable of sexuponoutcome*

###(3) AS CAT OR DOG

{% highlight r %}
train_1%>%
    group_by(OutcomeType, AnimalType)%>%
    summarise(count = n())%>%
    ggplot(aes(x = OutcomeType, y = count , fill = AnimalType)) +
    geom_col(position = "dodge") +
    geom_text(aes(label = count), position = position_dodge(width = 1)) # using position dodge and width, i could make text on each col
{% endhighlight %}

![plot of chunk unnamed-chunk-29](/assets/R_kaggle/2017-04-11-Shelter-Animal-Outcomes-ooDoo/unnamed-chunk-29-1.png)


###(4) AS BREED
 :finding whether purebred or not

{% highlight r %}
train_1%>%
    group_by(OutcomeType, Breed_Pure) %>%
    summarise(count = n()) %>%
    group_by(Breed_Pure) %>%
    mutate(count_sum = sum(count),
           ratio = count / count_sum) %>%
    ggplot(aes(x = OutcomeType, y = ratio, fill = factor(Breed_Pure))) +
    geom_col(position = "dodge") +
    geom_text(aes(label = round(ratio,digits = 2)), stat = ,position = position_dodge(width = 1))
{% endhighlight %}

![plot of chunk unnamed-chunk-30](/assets/R_kaggle/2017-04-11-Shelter-Animal-Outcomes-ooDoo/unnamed-chunk-30-1.png)
*sample count btwn mix and pure is too difference => So i use the each ratio value*


###(5) AS COLOR

{% highlight r %}
# original color 
for(i in 1:length(unique(train_1$OutcomeType))){
    train_1%>%
    filter(OutcomeType == unique(OutcomeType)[i]) %>%
    group_by(Color)%>%
    summarise(count = n()) %>%
    ggplot(aes(x = Color, y = count, fill = Color)) +
    geom_col() +
    ggtitle(unique(train_1$OutcomeType)[i]) +
    theme(legend.position="none", 
          axis.text.x = element_text(angle = 90, face = "italic", vjust = 1 ,hjust = 1),
          plot.title = element_text(face = "bold.italic", hjust = 0.5)) -> k
    print(k)
}
{% endhighlight %}

![plot of chunk unnamed-chunk-31](/assets/R_kaggle/2017-04-11-Shelter-Animal-Outcomes-ooDoo/unnamed-chunk-31-1.png)![plot of chunk unnamed-chunk-31](/assets/R_kaggle/2017-04-11-Shelter-Animal-Outcomes-ooDoo/unnamed-chunk-31-2.png)![plot of chunk unnamed-chunk-31](/assets/R_kaggle/2017-04-11-Shelter-Animal-Outcomes-ooDoo/unnamed-chunk-31-3.png)![plot of chunk unnamed-chunk-31](/assets/R_kaggle/2017-04-11-Shelter-Animal-Outcomes-ooDoo/unnamed-chunk-31-4.png)![plot of chunk unnamed-chunk-31](/assets/R_kaggle/2017-04-11-Shelter-Animal-Outcomes-ooDoo/unnamed-chunk-31-5.png)


{% highlight r %}
# simple color
for(i in 1:length(unique(train_1$OutcomeType))){
    train_1%>%
    filter(OutcomeType == unique(OutcomeType)[i]) %>%
    group_by(Color_simple)%>%
    summarise(count = n()) %>%
    ggplot(aes(x = Color_simple, y = count, fill = Color_simple)) +
    geom_col() +
    ggtitle(unique(train_1$OutcomeType)[i]) +
    theme(legend.position="none", 
          axis.text.x = element_text(angle = 90, face = "italic", vjust = 1 ,hjust = 1),
          plot.title = element_text(face = "bold.italic", hjust = 0.5)) -> k
    print(k)
}
{% endhighlight %}

![plot of chunk unnamed-chunk-32](/assets/R_kaggle/2017-04-11-Shelter-Animal-Outcomes-ooDoo/unnamed-chunk-32-1.png)![plot of chunk unnamed-chunk-32](/assets/R_kaggle/2017-04-11-Shelter-Animal-Outcomes-ooDoo/unnamed-chunk-32-2.png)![plot of chunk unnamed-chunk-32](/assets/R_kaggle/2017-04-11-Shelter-Animal-Outcomes-ooDoo/unnamed-chunk-32-3.png)![plot of chunk unnamed-chunk-32](/assets/R_kaggle/2017-04-11-Shelter-Animal-Outcomes-ooDoo/unnamed-chunk-32-4.png)![plot of chunk unnamed-chunk-32](/assets/R_kaggle/2017-04-11-Shelter-Animal-Outcomes-ooDoo/unnamed-chunk-32-5.png)

#4. DIVIDING CAT & DOG




#5. MODELING
##1) ONE HOT ENCODING

{% highlight r %}
# data
train_1
#train_shelter_mat <- model.matrix(OutcomeType ~ +. , train_1)
{% endhighlight %}






























