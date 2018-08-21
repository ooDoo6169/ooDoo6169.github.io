---
layout : post
title: "PublicData_Competition_trashAnalasys"
author: "ooDoo"
date: "2018-07-18"
categories : kaggle
cover : /assets/article_images/title/instacode_sizedown.png
---

# 0. SETTING


# 1. DATA IMPORT

{% highlight r %}
##0) Disposal
### data number : 3
disposal.local.houseLife <- read.csv("0) Disposal/04_02_2015_<U+653C><U+3E63> „êµãå<U+3E64>_<U+653C><U+3E63>‹œêµ°êµ¬ <U+653C><U+3E64>˜„<U+653C><U+3E64>™©_3. <U+653C><U+3E64>ê¸°ë¬¼ì²˜ë¦¬ì£¼ì²´ë³<U+383C><U+3E34> ì²˜ë¦¬<U+653C><U+3E64>˜„<U+653C><U+3E64>™©_3ê°€.ê°€<U+653C><U+3E63> •<U+653C><U+3E63>ƒ<U+653C><U+3E64>™œ<U+653C><U+3E64>ê¸°ë¬¼.csv")
disposal.local.industrialLife <- read.csv("0) Disposal/04_02_2015_<U+653C><U+3E63> „êµãå<U+3E64>_<U+653C><U+3E63>‹œêµ°êµ¬ <U+653C><U+3E64>˜„<U+653C><U+3E64>™©_3. <U+653C><U+3E64>ê¸°ë¬¼ì²˜ë¦¬ì£¼ì²´ë³<U+383C><U+3E34> ì²˜ë¦¬<U+653C><U+3E64>˜„<U+653C><U+3E64>™©_3<U+653C><U+3E62>‚˜.<U+653C><U+3E63>‚¬<U+653C><U+3E63>—…<U+653C><U+3E63>¥<U+653C><U+3E63>ƒ<U+653C><U+3E64>™œê³„íê¸°ë¬¼.csv")
disposal.local.industrialWaste <- read.csv("0) Disposal/04_02_2015_<U+653C><U+3E63> „êµãå<U+3E64>_<U+653C><U+3E63>‹œêµ°êµ¬ <U+653C><U+3E64>˜„<U+653C><U+3E64>™©_3. <U+653C><U+3E64>ê¸°ë¬¼ì²˜ë¦¬ì£¼ì²´ë³<U+383C><U+3E34> ì²˜ë¦¬<U+653C><U+3E64>˜„<U+653C><U+3E64>™©_3<U+653C><U+3E62>‹¤.<U+653C><U+3E63>‚¬<U+653C><U+3E63>—…<U+653C><U+3E63>¥ë°°ì¶œ<U+653C><U+3E63>‹œ<U+653C><U+3E63>„¤ê³„íê¸°ë¬¼.csv")
disposal.local.constructionWaste <- read.csv("0) Disposal/04_02_2015_<U+653C><U+3E63> „êµãå<U+3E64>_<U+653C><U+3E63>‹œêµ°êµ¬ <U+653C><U+3E64>˜„<U+653C><U+3E64>™©_3. <U+653C><U+3E64>ê¸°ë¬¼ì²˜ë¦¬ì£¼ì²´ë³<U+383C><U+3E34> ì²˜ë¦¬<U+653C><U+3E64>˜„<U+653C><U+3E64>™©_3<U+653C><U+3E62>¼.ê±´ì„¤<U+653C><U+3E64>ê¸°ë¬¼.csv")


##1) Occurence
### data number : 2
occurrence.houseLife <- read.csv("1) Production/04_02_2015_<U+653C><U+3E63> „êµãå<U+3E64>_<U+653C><U+3E63>‹œêµ°êµ¬ <U+653C><U+3E64>˜„<U+653C><U+3E64>™©_2. <U+653C><U+3E64>ê¸°ë¬¼ë°œìƒ ë°<U+383C><U+3E66> ì²˜ë¦¬<U+653C><U+3E64>˜„<U+653C><U+3E64>™©_2ê°€.ê°€<U+653C><U+3E63> •<U+653C><U+3E63>ƒ<U+653C><U+3E64>™œ<U+653C><U+3E64>ê¸°ë¬¼.csv")
occurrence.industrialLife <- read.csv("1) Production/04_02_2015_<U+653C><U+3E63> „êµãå<U+3E64>_<U+653C><U+3E63>‹œêµ°êµ¬ <U+653C><U+3E64>˜„<U+653C><U+3E64>™©_2. <U+653C><U+3E64>ê¸°ë¬¼ë°œìƒ ë°<U+383C><U+3E66> ì²˜ë¦¬<U+653C><U+3E64>˜„<U+653C><U+3E64>™©_2<U+653C><U+3E62>‚˜.<U+653C><U+3E63>‚¬<U+653C><U+3E63>—…<U+653C><U+3E63>¥<U+653C><U+3E63>ƒ<U+653C><U+3E64>™œ<U+653C><U+3E64>ê¸°ë¬¼.csv")
occurrence.industrialWaste <- read.csv("1) Production/04_02_2015_<U+653C><U+3E63> „êµãå<U+3E64>_<U+653C><U+3E63>‹œêµ°êµ¬ <U+653C><U+3E64>˜„<U+653C><U+3E64>™©_2. <U+653C><U+3E64>ê¸°ë¬¼ë°œìƒ ë°<U+383C><U+3E66> ì²˜ë¦¬<U+653C><U+3E64>˜„<U+653C><U+3E64>™©_2<U+653C><U+3E62>‹¤.<U+653C><U+3E63>—…ì¢…ë³„ <U+653C><U+3E63>‚¬<U+653C><U+3E63>—…<U+653C><U+3E63>¥ë°°ì¶œ<U+653C><U+3E63>‹œ<U+653C><U+3E63>„¤ê³„íê¸°ë¬¼.csv")
occurrence.constructionWaste <- read.csv("1) Production/04_02_2015_<U+653C><U+3E63> „êµãå<U+3E64>_<U+653C><U+3E63>‹œêµ°êµ¬ <U+653C><U+3E64>˜„<U+653C><U+3E64>™©_2. <U+653C><U+3E64>ê¸°ë¬¼ë°œìƒ ë°<U+383C><U+3E66> ì²˜ë¦¬<U+653C><U+3E64>˜„<U+653C><U+3E64>™©_2<U+653C><U+3E62>¼.ê±´ì„¤<U+653C><U+3E64>ê¸°ë¬¼.csv")


##2) landfill_incinerate
### data number : 5, 6, 7
landincin.local.land <- read.csv("2) landfill_incinerate/04_02_2015_<U+653C><U+3E63> „êµãå<U+3E64>_<U+653C><U+3E63>‹œêµ°êµ¬ <U+653C><U+3E64>˜„<U+653C><U+3E64>™©_5. <U+653C><U+3E64>ê¸°ë¬¼ ë§¤ë¦½<U+653C><U+3E63>‹œ<U+653C><U+3E63>„¤ <U+653C><U+3E64>˜„<U+653C><U+3E64>™©_5ê°€.ì§€ë°©ìì¹˜ë‹¨ì²<U+623C><U+3E34>.csv")
landincin.own.land <- read.csv("2) landfill_incinerate/04_02_2015_<U+653C><U+3E63> „êµãå<U+3E64>_<U+653C><U+3E63>‹œêµ°êµ¬ <U+653C><U+3E64>˜„<U+653C><U+3E64>™©_5. <U+653C><U+3E64>ê¸°ë¬¼ ë§¤ë¦½<U+653C><U+3E63>‹œ<U+653C><U+3E63>„¤ <U+653C><U+3E64>˜„<U+653C><U+3E64>™©_5<U+653C><U+3E62>‚˜.<U+653C><U+3E63>ê°€ì²˜ë¦¬<U+653C><U+3E63>—…ì²<U+623C><U+3E34>.csv")

landincin.local.incin <- read.csv("2) landfill_incinerate/04_02_2015_<U+653C><U+3E63> „êµãå<U+3E64>_<U+653C><U+3E63>‹œêµ°êµ¬ <U+653C><U+3E64>˜„<U+653C><U+3E64>™©_6. <U+653C><U+3E64>ê¸°ë¬¼<U+653C><U+3E63>†Œê°ì‹œ<U+653C><U+3E63>„¤<U+653C><U+3E64>˜„<U+653C><U+3E64>™©_6ê°€.ì§€ë°©ìì¹˜ë‹¨ì²<U+623C><U+3E34>.csv")
landincin.ownLife.incin <- read.csv("2) landfill_incinerate/04_02_2015_<U+653C><U+3E63> „êµãå<U+3E64>_<U+653C><U+3E63>‹œêµ°êµ¬ <U+653C><U+3E64>˜„<U+653C><U+3E64>™©_6. <U+653C><U+3E64>ê¸°ë¬¼<U+653C><U+3E63>†Œê°ì‹œ<U+653C><U+3E63>„¤<U+653C><U+3E64>˜„<U+653C><U+3E64>™©_6<U+653C><U+3E62>‚˜.<U+653C><U+3E63>ê°€ì²˜ë¦¬<U+653C><U+3E63>—…ì²<U+623C><U+3E34>(<U+653C><U+3E63>ƒ<U+653C><U+3E64>™œ<U+653C><U+3E64>ê¸°ë¬¼ <U+653C><U+3E63>†Œê°ì‹œ<U+653C><U+3E63>„¤).csv")
landincin.ownBusiness.incin <- read.csv("2) landfill_incinerate/04_02_2015_<U+653C><U+3E63> „êµãå<U+3E64>_<U+653C><U+3E63>‹œêµ°êµ¬ <U+653C><U+3E64>˜„<U+653C><U+3E64>™©_6. <U+653C><U+3E64>ê¸°ë¬¼<U+653C><U+3E63>†Œê°ì‹œ<U+653C><U+3E63>„¤<U+653C><U+3E64>˜„<U+653C><U+3E64>™©_6<U+653C><U+3E62>‹¤.<U+653C><U+3E63>ê°€ì²˜ë¦¬<U+653C><U+3E63>—…ì²<U+623C><U+3E34>(<U+653C><U+3E63>‚¬<U+653C><U+3E63>—…<U+653C><U+3E63>¥<U+653C><U+3E64>ê¸°ë¬¼ <U+653C><U+3E63>†Œê°ì‹œ<U+653C><U+3E63>„¤).csv")

landincin.local.etc <- read.csv("2) landfill_incinerate/04_02_2015_<U+653C><U+3E63> „êµãå<U+3E64>_<U+653C><U+3E63>‹œêµ°êµ¬ <U+653C><U+3E64>˜„<U+653C><U+3E64>™©_7. ê¸°í<U+383C><U+3E33>€<U+653C><U+3E63>‹œ<U+653C><U+3E63>„¤<U+653C><U+3E64>˜„<U+653C><U+3E64>™©_7ê°€.ì§€ë°©ìì¹˜ë‹¨ì²<U+623C><U+3E34>.csv")
landincin.own.etc <- read.csv("2) landfill_incinerate/04_02_2015_<U+653C><U+3E63> „êµãå<U+3E64>_<U+653C><U+3E63>‹œêµ°êµ¬ <U+653C><U+3E64>˜„<U+653C><U+3E64>™©_7. ê¸°í<U+383C><U+3E33>€<U+653C><U+3E63>‹œ<U+653C><U+3E63>„¤<U+653C><U+3E64>˜„<U+653C><U+3E64>™©_7<U+653C><U+3E62>‚˜.<U+653C><U+3E63>ê°€ì²˜ë¦¬<U+653C><U+3E63>—…ì²<U+623C><U+3E34>.csv")


##3) collet
### data number : 8
collect.lifeBusiness <- read.csv("3) Collection/04_02_2015_<U+653C><U+3E63> „êµãå<U+3E64>_<U+653C><U+3E63>‹œêµ°êµ¬ <U+653C><U+3E64>˜„<U+653C><U+3E64>™©_8. <U+653C><U+3E64>ê¸°ë¬¼ì²˜ë¦¬<U+653C><U+3E63>—… <U+653C><U+3E64>˜„<U+653C><U+3E64>™©_8ê°€.<U+653C><U+3E63>ˆ˜ì§‘Â·ìš´ë°˜ì—…ì²<U+623C><U+3E34>(<U+653C><U+3E63>ƒ<U+653C><U+3E64>™œ ë°<U+383C><U+3E66> <U+653C><U+3E63>‚¬<U+653C><U+3E63>—…<U+653C><U+3E63>¥<U+653C><U+3E64>ê¸°ë¬¼).csv")
collect.construction <- read.csv("3) Collection/04_02_2015_<U+653C><U+3E63> „êµãå<U+3E64>_<U+653C><U+3E63>‹œêµ°êµ¬ <U+653C><U+3E64>˜„<U+653C><U+3E64>™©_8. <U+653C><U+3E64>ê¸°ë¬¼ì²˜ë¦¬<U+653C><U+3E63>—… <U+653C><U+3E64>˜„<U+653C><U+3E64>™©_8<U+653C><U+3E62>‚˜.<U+653C><U+3E63>ˆ˜ì§‘Â·ìš´ë°˜ì—…ì²<U+623C><U+3E34>(ê±´ì„¤<U+653C><U+3E64>ê¸°ë¬¼).csv")


##4) middle/final/overall
### data number : 8
middle.disposal <- read.csv("4) middle_final_overall/1) Middle/04_02_2015_<U+653C><U+3E63> „êµãå<U+3E64>_<U+653C><U+3E63>‹œêµ°êµ¬ <U+653C><U+3E64>˜„<U+653C><U+3E64>™©_8. <U+653C><U+3E64>ê¸°ë¬¼ì²˜ë¦¬<U+653C><U+3E63>—… <U+653C><U+3E64>˜„<U+653C><U+3E64>™©_8<U+653C><U+3E62>‹¤.ì¤‘ê°„ì²˜ë¶„<U+653C><U+3E63>—…ì²<U+623C><U+3E34>.csv")
middle.recycle <- read.csv("4) middle_final_overall/1) Middle/04_02_2015_<U+653C><U+3E63> „êµãå<U+3E64>_<U+653C><U+3E63>‹œêµ°êµ¬ <U+653C><U+3E64>˜„<U+653C><U+3E64>™©_8. <U+653C><U+3E64>ê¸°ë¬¼ì²˜ë¦¬<U+653C><U+3E63>—… <U+653C><U+3E64>˜„<U+653C><U+3E64>™©_8ë§<U+383C><U+3E38>. ì¤‘ê°„<U+653C><U+3E63>¬<U+653C><U+3E64>™œ<U+653C><U+3E63>š©<U+653C><U+3E63>—…ì²<U+623C><U+3E34>.csv")
middle.construction <- read.csv("4) middle_final_overall/1) Middle/04_02_2015_<U+653C><U+3E63> „êµãå<U+3E64>_<U+653C><U+3E63>‹œêµ°êµ¬ <U+653C><U+3E64>˜„<U+653C><U+3E64>™©_8. <U+653C><U+3E64>ê¸°ë¬¼ì²˜ë¦¬<U+653C><U+3E63>—… <U+653C><U+3E64>˜„<U+653C><U+3E64>™©_8<U+653C><U+3E63>•„.ì¤‘ê°„ì²˜ë¦¬<U+653C><U+3E63>—…ì²<U+623C><U+3E34>(ê±´ì„¤<U+653C><U+3E64>ê¸°ë¬¼).csv")

final.disposal <- read.csv("4) middle_final_overall/2) Final/04_02_2015_<U+653C><U+3E63> „êµãå<U+3E64>_<U+653C><U+3E63>‹œêµ°êµ¬ <U+653C><U+3E64>˜„<U+653C><U+3E64>™©_8. <U+653C><U+3E64>ê¸°ë¬¼ì²˜ë¦¬<U+653C><U+3E63>—… <U+653C><U+3E64>˜„<U+653C><U+3E64>™©_8<U+653C><U+3E62>¼.ìµœì¢…ì²˜ë¶„<U+653C><U+3E63>—…ì²<U+623C><U+3E34>.csv")
final.recycle <- read.csv("4) middle_final_overall/2) Final/04_02_2015_<U+653C><U+3E63> „êµãå<U+3E64>_<U+653C><U+3E63>‹œêµ°êµ¬ <U+653C><U+3E64>˜„<U+653C><U+3E64>™©_8. <U+653C><U+3E64>ê¸°ë¬¼ì²˜ë¦¬<U+653C><U+3E63>—… <U+653C><U+3E64>˜„<U+653C><U+3E64>™©_8ë°<U+393C><U+3E34>.ìµœì¢…<U+653C><U+3E63>¬<U+653C><U+3E64>™œ<U+653C><U+3E63>š©<U+653C><U+3E63>—…ì²<U+623C><U+3E34>.csv")

overall.recycle <- read.csv("4) middle_final_overall/3) Overall/04_02_2015_<U+653C><U+3E63> „êµãå<U+3E64>_<U+653C><U+3E63>‹œêµ°êµ¬ <U+653C><U+3E64>˜„<U+653C><U+3E64>™©_8. <U+653C><U+3E64>ê¸°ë¬¼ì²˜ë¦¬<U+653C><U+3E63>—… <U+653C><U+3E64>˜„<U+653C><U+3E64>™©_8<U+653C><U+3E63>‚¬.ì¢…í•©<U+653C><U+3E63>¬<U+653C><U+3E64>™œ<U+653C><U+3E63>š©<U+653C><U+3E63>—…ì²<U+623C><U+3E34>.csv")
{% endhighlight %}



{% highlight text %}
## Error: invalid multibyte character in parser at line 3
{% endhighlight %}
#

# 2. DATA HANDLING 
## 0) Disposal
- (1) change the column names     
- (2) NA -> 0
- (3) Combine columns by disposition type.

### (1) FeatureExtract

{% highlight r %}
list.disposal.name <- c("disposal.local.houseLife",
                        "disposal.local.industrialLife",
                        "disposal.local.industrialWaste",
                        "disposal.local.constructionWaste")  

# "disposal.local.houseLife", "disposal.local.industrialLife","disposal.local.constructionWaste"
for( i in c(list.disposal.name)){
    
    if( i == "disposal.local.industrialWaste"){ # only this one has 14 columns
        ## (0) bring the data
        i %in% ls(envir = .GlobalEnv)
        data <- get(i, envir = .GlobalEnv)

        ## (1)change the column names
        names(data) <- c("sido", "sigungu","self_landfill",
                         "self_incin","self_recycle",
                         "self_sea","business_landfill",
                         "business_incin","business_recycle",
                          "business_sea","own_landfill",
                          "own_incin","own_recycle","own_sea")
        
        ## (2) NA -> 0
        data %>%
            mutate_all(funs(replace(., is.na(.), 0))) -> data
        ## (3) Combine columns by disposision type
        data %>%
            mutate(landfill = rowSums(select(., contains("landfill"))),
                   incin = rowSums(select(., contains("incin"))),
                   recycle = rowSums(select(., contains("recycle"))),
                   sea = rowSums(select(., contains("sea"))))%>%
            select(c(sido, sigungu, landfill, incin, recycle, sea)) -> data
        ## (4) make prefix to diviede each data
        colnames(data)[3:6] <- paste("industrialWaste",
                                     colnames(data)[3:6],
                                     sep = "_")
        assign(x = i, value = data)
        print(paste0(i,"_done"))
        
        } else {
            ## (0) bring the data
            i %in% ls(envir = .GlobalEnv)
    data <- get(i, envir = .GlobalEnv)
            
    ## (1) change the column names
    names(data) <- c("sido","sigungu","self_landfill","self_incin","self_recycle",
                     "business_landfill","business_incin","business_recycle",
                     "own_landfill","own_incin","own_recycle")
    names(data)
        
    ## (2) NA -> 0
    data%>%
    mutate_all(funs(replace(., is.na(.), 0))) -> data

                
    ## (3) Combine columns by disposision type
    data%>%
        mutate(landfill = rowSums(select(., contains("landfill"))),
               incin = rowSums(select(., contains("incin"))),
               recycle = rowSums(select(., contains("recycle"))))%>%
        select(c(sido, sigungu, landfill, incin, recycle)) -> data
        
    ## (4) assign the orignal name to data
    str_split(i,pattern = "\\.")[[1]][3]
    tag <- str_split(i,pattern = "\\.")[[1]][3]
    colnames(data)[3:5] <- paste(tag, colnames(data)[3:5], sep = "_")
    
    assign(x = i, value = data)
    print(paste0(i,"_done"))
    }
    
}
{% endhighlight %}



{% highlight text %}
## Error in get(i, envir = .GlobalEnv): object 'disposal.local.houseLife' not found
{% endhighlight %}

### (2) merge the data 

{% highlight r %}
# check the row number of data 
nrow(disposal.local.houseLife)
{% endhighlight %}



{% highlight text %}
## Error in nrow(disposal.local.houseLife): object 'disposal.local.houseLife' not found
{% endhighlight %}



{% highlight r %}
nrow(disposal.local.industrialLife)
{% endhighlight %}



{% highlight text %}
## Error in nrow(disposal.local.industrialLife): object 'disposal.local.industrialLife' not found
{% endhighlight %}



{% highlight r %}
nrow(disposal.local.industrialWaste)
{% endhighlight %}



{% highlight text %}
## Error in nrow(disposal.local.industrialWaste): object 'disposal.local.industrialWaste' not found
{% endhighlight %}



{% highlight r %}
nrow(disposal.local.constructionWaste)
{% endhighlight %}



{% highlight text %}
## Error in nrow(disposal.local.constructionWaste): object 'disposal.local.constructionWaste' not found
{% endhighlight %}



{% highlight r %}
# merge the data using 'Outer Join'
disposal.local <- Reduce(function(x, y) merge(x, y, all=TRUE),  # using "Reuce"!!
                         list(disposal.local.houseLife,
                              disposal.local.industrialLife,
                              disposal.local.industrialWaste, 
                              disposal.local.constructionWaste))
{% endhighlight %}



{% highlight text %}
## Error in Reduce(function(x, y) merge(x, y, all = TRUE), list(disposal.local.houseLife, : object 'disposal.local.houseLife' not found
{% endhighlight %}



{% highlight r %}
head(disposal.local)
{% endhighlight %}



{% highlight text %}
##     sido sigungu houseLife_landfill houseLife_incin houseLife_recycle
## 1 °­¿øµµ  °­¸ª½Ã               79.2            11.9             216.4
## 2 °­¿øµµ  °í¼º±º                7.0            21.5               6.7
## 3 °­¿øµµ  µ¿ÇØ½Ã               78.9             0.0              45.1
## 4 °­¿øµµ  »ïÃ´½Ã               59.3             0.0              38.4
## 5 °­¿øµµ  ¼ÓÃÊ½Ã               43.5            67.4              30.4
## 6 °­¿øµµ  ¾ç±¸±º                0.0            11.0              17.6
##   industrialLife_landfill industrialLife_incin industrialLife_recycle
## 1                    42.9                  0.0                    5.4
## 2                    11.7                 10.3                    1.0
## 3                     0.0                  0.0                    1.4
## 4                     5.4                  0.0                    5.7
## 5                     4.8                  0.6                    4.2
## 6                     0.0                  0.0                    0.0
##   industrialWaste_landfill industrialWaste_incin industrialWaste_recycle
## 1                     15.4                   0.1                   583.0
## 2                      4.3                   0.0                    15.0
## 3                     71.1                   2.1                  2235.1
## 4                      3.9                   0.1                    98.0
## 5                      0.4                   0.0                     4.0
## 6                      0.0                   4.2                     2.4
##   industrialWaste_sea constructionWaste_landfill constructionWaste_incin
## 1                   8                        0.0                     0.0
## 2                   4                        0.0                     0.0
## 3                   0                        0.8                     0.0
## 4                   0                        9.7                    10.5
## 5                   0                        0.2                     0.0
## 6                   0                        0.0                     0.0
##   constructionWaste_recycle houseLife_total industrialLife_total
## 1                    1184.2           307.5                 48.3
## 2                     286.0            35.2                 23.0
## 3                     376.2           124.0                  1.4
## 4                     603.1            97.7                 11.1
## 5                     379.9           141.3                  9.6
## 6                     232.3            28.6                  0.0
##   industrialWaste_total constructionWaste_total        region
## 1                 606.5                  1184.2 °­¿øµµ_°­¸ª½Ã
## 2                  23.3                   286.0 °­¿øµµ_°í¼º±º
## 3                2308.3                   377.0 °­¿øµµ_µ¿ÇØ½Ã
## 4                 102.0                   623.3 °­¿øµµ_»ïÃ´½Ã
## 5                   4.4                   380.1 °­¿øµµ_¼ÓÃÊ½Ã
## 6                   6.6                   232.3 °­¿øµµ_¾ç±¸±º
{% endhighlight %}

### (3) overall column

{% highlight r %}
disposal.local %>%
    mutate(houseLife_total = houseLife_landfill + 
                             houseLife_incin + 
                             houseLife_recycle,
           industrialLife_total = industrialLife_landfill + 
                                  industrialLife_incin +
                                  industrialLife_recycle, 
           industrialWaste_total = industrialWaste_landfill + industrialWaste_incin + 
                                   industrialWaste_recycle + industrialWaste_sea,
           constructionWaste_total = constructionWaste_landfill +
                                     constructionWaste_incin + 
                                     constructionWaste_recycle,
           region = paste(sido, sigungu, sep = "_")) -> disposal.local
{% endhighlight %}

### *saving disposal.local*

{% highlight r %}
#write.csv(disposal.local, "disposal.local.csv", row.names = FALSE)
{% endhighlight %}


## 1) Occurence
*overview*
 - product.local.houseLife         : 2. <ed>ê¸°ë¬¼ë°œìƒ ë°<8f> ì²˜ë¦¬<ed>˜„<ed>™©_2ê°€.ê°€<ec> •<ec>ƒ<ed>™œ<ed>ê¸°ë¬¼.csv
 - product.local.industrialLife    : 2. <ed>ê¸°ë¬¼ë°œìƒ ë°<8f> ì²˜ë¦¬<ed>˜„<ed>™©_2<eb>‚˜.<ec>‚¬<ec>—…<ec>¥<ec>ƒ<ed>™œ<ed>ê¸°ë¬¼.csv
 - product.local.industrialWaste   : 2. <ed>ê¸°ë¬¼ë°œìƒ ë°<8f> ì²˜ë¦¬<ed>˜„<ed>™©_2<eb>‹¤.<ec>—…ì¢…ë³„ <ec>‚¬<ec>—…<ec>¥ë°°ì¶œ<ec>‹œ<ec>„¤ê³„íê¸°ë¬¼.csv
 - product.local.constructionWaste : 2. <ed>ê¸°ë¬¼ë°œìƒ ë°<8f> ì²˜ë¦¬<ed>˜„<ed>™©_2<eb>¼.ê±´ì„¤<ed>ê¸°ë¬¼.csv

### (2) Data Handling
#### (a) Layout(Long -> Wide)

{% highlight r %}
library(reshape2)
occurrence.industrialWaste <- occurrence.industrialWaste[, -c(3:4, 34)] # delete unnecessary column
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'occurrence.industrialWaste' not found
{% endhighlight %}



{% highlight r %}
occurrence.industrialWaste[, 19] <- as.numeric(as.character(occurrence.industrialWaste[, 19]))
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'occurrence.industrialWaste' not found
{% endhighlight %}


{% highlight r %}
# file names
file.names <- c("occurrence.houseLife", "occurrence.industrialLife", 
                "occurrence.industrialWaste", "occurrence.constructionWaste")

# data handling
for (i in file.names) {
    # data
    tmp <- get(i)
    # rename
    names(tmp)[1:3] <- c("sido", "sigungu", "type")
  
    # NA -> 0
    for (j in 4:ncol(tmp)) {
        tmp[is.na(tmp[, j]), j] <- 0
    }
    
    # row sum
    tmp$sum <- apply(tmp[, 4:ncol(tmp)], 1, sum)

    # feature selection
    tmp <- tmp[, c(1:3, ncol(tmp))]
  
    # cast & variable names
    if (i == "occurrence.industrialWaste") {
        tmp.df <- tmp %>%
            group_by(sido, sigungu, type) %>%
            summarise(newSum = sum(sum))
        df <- dcast(tmp.df, sido + sigungu ~ type, value.var = "newSum")
        
        names(df)[3:7] <- paste(substr(i, 12, nchar(i)), 
                                c("landfill", "total", "incin", "recycle", "see"),
                                sep = ".")
        } else {
            df <- dcast(data = tmp,
                        sido + sigungu ~ type, # "sido" & "sigungu" : id_column
                                               # "type" : category column
                        value.var = "sum")     # "sum"  : value column
            
            names(df)[3:6] <- paste(substr(i, start = 12, stop = nchar(i)), 
                                    c("landfill", "total", "incin", "recycle"),
                                    sep = "_")
        }
    # join key
    df$region <- paste(df$sido, df$sigungu, sep = "_")
  
    # assign data
    assign(i, tmp)
    assign(paste0(i, ".df"), df)
}
{% endhighlight %}



{% highlight text %}
## Error in get(i): object 'occurrence.houseLife' not found
{% endhighlight %}



{% highlight r %}
head(occurrence.houseLife)
{% endhighlight %}



{% highlight text %}
## Error in head(occurrence.houseLife): object 'occurrence.houseLife' not found
{% endhighlight %}



{% highlight r %}
head(occurrence.houseLife.df)
{% endhighlight %}



{% highlight text %}
## Error in head(occurrence.houseLife.df): object 'occurrence.houseLife.df' not found
{% endhighlight %}

#### (b) Merge(Occurrence)

{% highlight r %}
occurrence.local <- Reduce(function(x, y) merge(x, y, all = TRUE), 
                          list(occurrence.houseLife.df, 
                               occurrence.industrialLife.df, 
                               occurrence.industrialWaste.df, 
                               occurrence.constructionWaste.df))
{% endhighlight %}



{% highlight text %}
## Error in Reduce(function(x, y) merge(x, y, all = TRUE), list(occurrence.houseLife.df, : object 'occurrence.houseLife.df' not found
{% endhighlight %}



{% highlight r %}
# NA -> 0 
for (i in 12:16) {
    occurrence.local[is.na(occurrence.local[, i]), i] <- 0
}
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'occurrence.local' not found
{% endhighlight %}



{% highlight r %}
head(occurrence.local)
{% endhighlight %}



{% highlight text %}
## Error in head(occurrence.local): object 'occurrence.local' not found
{% endhighlight %}

### *saving occurrence.local*

{% highlight r %}
write.csv(occurrence.local, "occurrence.local.csv", row.names = FALSE)
{% endhighlight %}



{% highlight text %}
## Error in is.data.frame(x): object 'occurrence.local' not found
{% endhighlight %}


## 2) landfill_incinerate
*overview*
 - landincin.local.land : 5. <ed>ê¸°ë¬¼ ë§¤ë¦½<ec>‹œ<ec>„¤ <ed>˜„<ed>™©_5ê°€.ì§€ë°©ìì¹˜ë‹¨ì²<b4>.csv
 - landincin.own.land   : 5. <ed>ê¸°ë¬¼ ë§¤ë¦½<ec>‹œ<ec>„¤ <ed>˜„<ed>™©_5<eb>‚˜.<ec>ê°€ì²˜ë¦¬<ec>—…ì²<b4>.csv
 - landincin.local.incin  : 6. <ed>ê¸°ë¬¼<ec>†Œê°ì‹œ<ec>„¤<ed>˜„<ed>™©_6ê°€.ì§€ë°©ìì¹˜ë‹¨ì²<b4>.csv
 - landincin.ownLife.incin  : 6. <ed>ê¸°ë¬¼<ec>†Œê°ì‹œ<ec>„¤<ed>˜„<ed>™©_6<eb>‚˜.<ec>ê°€ì²˜ë¦¬<ec>—…ì²<b4>(<ec>ƒ<ed>™œ<ed>ê¸°ë¬¼ <ec>†Œê°ì‹œ<ec>„¤).csv
 - landincin.ownBusiness.incin : 6. <ed>ê¸°ë¬¼<ec>†Œê°ì‹œ<ec>„¤<ed>˜„<ed>™©_6<eb>‹¤.<ec>ê°€ì²˜ë¦¬<ec>—…ì²<b4>(<ec>‚¬<ec>—…<ec>¥<ed>ê¸°ë¬¼ <ec>†Œê°ì‹œ<ec>„¤).csv
 - landincin.local.etc : 7. ê¸°í<83>€<ec>‹œ<ec>„¤<ed>˜„<ed>™©_7ê°€.ì§€ë°©ìì¹˜ë‹¨ì²<b4>.csv
 - landincin.own.etc : 7. ê¸°í<83>€<ec>‹œ<ec>„¤<ed>˜„<ed>™©_7<eb>‚˜.<ec>ê°€ì²˜ë¦¬<ec>—…ì²<b4>.csv

### 1) FeatureSelection

{% highlight r %}
# FeatureSelection
landincin.local.land <- landincin.local.land[c(1:6,9,16)]
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'landincin.local.land' not found
{% endhighlight %}



{% highlight r %}
landincin.own.land <- landincin.own.land[c(1:8,11,15)]
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'landincin.own.land' not found
{% endhighlight %}



{% highlight r %}
landincin.local.incin <- landincin.local.incin[c(1,2,3,4,15:19)]
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'landincin.local.incin' not found
{% endhighlight %}



{% highlight r %}
landincin.ownLife.incin <- landincin.ownLife.incin[c(1:6,10)]
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'landincin.ownLife.incin' not found
{% endhighlight %}



{% highlight r %}
landincin.ownBusiness.incin <- landincin.ownBusiness.incin[c(1,2,3,4,5,6,10)]
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'landincin.ownBusiness.incin' not found
{% endhighlight %}



{% highlight r %}
landincin.local.etc <- landincin.local.etc[c(1,2,3,4,5,8,14)]
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'landincin.local.etc' not found
{% endhighlight %}



{% highlight r %}
landincin.own.etc <- landincin.own.etc[c(1,2,3,4,5,6,7,10)]
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'landincin.own.etc' not found
{% endhighlight %}

{% highlight r %}
# change column name as ENG
colnames(landincin.local.land) <- c("sido","sigungu",
                                    "location","lf_area","lf_capacity",
                                    "lf_cumulate","lf_15amount","lf_plan")
{% endhighlight %}



{% highlight text %}
## Error in colnames(landincin.local.land) <- c("sido", "sigungu", "location", : object 'landincin.local.land' not found
{% endhighlight %}



{% highlight r %}
colnames(landincin.own.land) <- c("sido","sigungu",
                                  "company_name","company_boss",
                                  "location","lf_area","lf_capacity",
                                  "lf_cumulate","lf_15amount","lf_plan")
{% endhighlight %}



{% highlight text %}
## Error in colnames(landincin.own.land) <- c("sido", "sigungu", "company_name", : object 'landincin.own.land' not found
{% endhighlight %}



{% highlight r %}
colnames(landincin.local.incin) <- c("sido","sigungu",
                                     "location","ic_capacity",
                                     "eng_amount","eng_heatOut","eng_electricOut",
                                     "eng_heatIn","eng_electricIn")
{% endhighlight %}



{% highlight text %}
## Error in colnames(landincin.local.incin) <- c("sido", "sigungu", "location", : object 'landincin.local.incin' not found
{% endhighlight %}



{% highlight r %}
colnames(landincin.ownLife.incin) <- c("sido","sigungu",
                                       "company_name","company_boss",
                                       "location","ic_capacity","ic_15amount")
{% endhighlight %}



{% highlight text %}
## Error in colnames(landincin.ownLife.incin) <- c("sido", "sigungu", "company_name", : object 'landincin.ownLife.incin' not found
{% endhighlight %}



{% highlight r %}
colnames(landincin.ownBusiness.incin) <- c("sido","sigungu",
                                           "company_name","company_boss",
                                           "location","ic_capacity","ic_15amount")
{% endhighlight %}



{% highlight text %}
## Error in colnames(landincin.ownBusiness.incin) <- c("sido", "sigungu", : object 'landincin.ownBusiness.incin' not found
{% endhighlight %}



{% highlight r %}
colnames(landincin.local.etc) <- c("sido","sigungu","location",
                                   "etc_type","etc_capacity","etc_15amount",
                                   "gas_recycle")
{% endhighlight %}



{% highlight text %}
## Error in colnames(landincin.local.etc) <- c("sido", "sigungu", "location", : object 'landincin.local.etc' not found
{% endhighlight %}



{% highlight r %}
colnames(landincin.own.etc)  <- c("sido","sigungu",
                                  "company_name","company_boss","location",
                                  "etc_type","etc_capacity","etc_15amount")
{% endhighlight %}



{% highlight text %}
## Error in colnames(landincin.own.etc) <- c("sido", "sigungu", "company_name", : object 'landincin.own.etc' not found
{% endhighlight %}


## 3) collect
*overview*
- collect.lifeBusiness : 8. <ed>ê¸°ë¬¼ì²˜ë¦¬<ec>—… <ed>˜„<ed>™©_8ê°€.<ec>ˆ˜ì§‘Â·ìš´ë°˜ì—…ì²<b4>(<ec>ƒ<ed>™œ ë°<8f> <ec>‚¬<ec>—…<ec>¥<ed>ê¸°ë¬¼).csv
- collect.construction : 8. <ed>ê¸°ë¬¼ì²˜ë¦¬<ec>—… <ed>˜„<ed>™©_8<eb>‚˜.<ec>ˆ˜ì§‘Â·ìš´ë°˜ì—…ì²<b4>(ê±´ì„¤<ed>ê¸°ë¬¼).csv

### 1) FeatureSelection

{% highlight r %}
collect.lifeBusiness <- collect.lifeBusiness[c(1,2,4,6,7,9,10)]
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'collect.lifeBusiness' not found
{% endhighlight %}



{% highlight r %}
collect.construction <- collect.construction[c(1,2,3,4,5,8)] # adding type
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'collect.construction' not found
{% endhighlight %}


{% highlight r %}
colnames(collect.lifeBusiness) <-  c("sido","sigungu",
                                    "company_name","company_boss",
                                    "location","collet_15amount","type")
{% endhighlight %}



{% highlight text %}
## Error in colnames(collect.lifeBusiness) <- c("sido", "sigungu", "company_name", : object 'collect.lifeBusiness' not found
{% endhighlight %}



{% highlight r %}
colnames(collect.construction) <- c("sido","sigungu",
                                    "company_name","company_boss",
                                    "location","collet_15amount")
{% endhighlight %}



{% highlight text %}
## Error in colnames(collect.construction) <- c("sido", "sigungu", "company_name", : object 'collect.construction' not found
{% endhighlight %}

{% highlight r %}
# adding type column at collect.construction data 
collect.construction$type <- NULL
{% endhighlight %}



{% highlight text %}
## Error in collect.construction$type <- NULL: object 'collect.construction' not found
{% endhighlight %}



{% highlight r %}
collect.construction%>%
    mutate(type = "ê±´ì¶•") -> collect.construction
{% endhighlight %}



{% highlight text %}
## Error in eval(lhs, parent, parent): object 'collect.construction' not found
{% endhighlight %}


## 4) middle/final/overall
*overview*
- middle.disposal : 8. <ed>ê¸°ë¬¼ì²˜ë¦¬<ec>—… <ed>˜„<ed>™©_8<eb>‹¤.ì¤‘ê°„ì²˜ë¶„<ec>—…ì²<b4>.csv
- middle.recycle : 8. <ed>ê¸°ë¬¼ì²˜ë¦¬<ec>—… <ed>˜„<ed>™©_8ë§<88>. ì¤‘ê°„<ec>¬<ed>™œ<ec>š©<ec>—…ì²<b4>.csv
- middle.construction : 8. <ed>ê¸°ë¬¼ì²˜ë¦¬<ec>—… <ed>˜„<ed>™©_8<ec>•„.ì¤‘ê°„ì²˜ë¦¬<ec>—…ì²<b4>(ê±´ì„¤<ed>ê¸°ë¬¼).csv
- final.disposal : 8. <ed>ê¸°ë¬¼ì²˜ë¦¬<ec>—… <ed>˜„<ed>™©_8<eb>¼.ìµœì¢…ì²˜ë¶„<ec>—…ì²<b4>.csv
- final.recycle : 8. <ed>ê¸°ë¬¼ì²˜ë¦¬<ec>—… <ed>˜„<ed>™©_8ë°<94>.ìµœì¢…<ec>¬<ed>™œ<ec>š©<ec>—…ì²<b4>.csv
- overall.recycle : 8. <ed>ê¸°ë¬¼ì²˜ë¦¬<ec>—… <ed>˜„<ed>™©_8<ec>‚¬.ì¢…í•©<ec>¬<ed>™œ<ec>š©<ec>—…ì²<b4>.csv


### (1) FeatureSelection

{% highlight r %}
middle.disposal <- middle.disposal[c(1,2,3,4,6,7,9,10,11,12,13,14,18)] 
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'middle.disposal' not found
{% endhighlight %}



{% highlight r %}
middle.recycle <- middle.recycle[c(1,2,3,5,6,8,9,13)] 
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'middle.recycle' not found
{% endhighlight %}



{% highlight r %}
middle.construction <- middle.construction[c(1,2,3,4,5,7,14,18)] # adding type name
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'middle.construction' not found
{% endhighlight %}



{% highlight r %}
final.disposal <- final.disposal[c(1,2,3,6,7,9,10,11,12,17)]
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'final.disposal' not found
{% endhighlight %}



{% highlight r %}
final.recycle <- final.recycle[c(1,2,3,5,6,8,9,13)]
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'final.recycle' not found
{% endhighlight %}



{% highlight r %}
overall.recycle <- overall.recycle[c(1,2,3,5,6,8,9,13)]
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'overall.recycle' not found
{% endhighlight %}


{% highlight r %}
# middle
colnames(middle.disposal) <- c("sido","sigungu",
                               "category","company_name","company_boss","location",
                               "ic","md","cd","bd","etcd", # merge disposal column : done
                               "capacity","disposal_15amount")
{% endhighlight %}



{% highlight text %}
## Error in colnames(middle.disposal) <- c("sido", "sigungu", "category", : object 'middle.disposal' not found
{% endhighlight %}



{% highlight r %}
colnames(middle.recycle) <- c("sido","sigungu",
                              "company_name","company_boss","location",
                              "category","capacity","disposal_15amount")
{% endhighlight %}



{% highlight text %}
## Error in colnames(middle.recycle) <- c("sido", "sigungu", "company_name", : object 'middle.recycle' not found
{% endhighlight %}



{% highlight r %}
colnames(middle.construction) <- c("sido","sigungu",
                                   "company_name","location","company_boss",
                                   "lf_area","capacity","disposal_15amount")
{% endhighlight %}



{% highlight text %}
## Error in colnames(middle.construction) <- c("sido", "sigungu", "company_name", : object 'middle.construction' not found
{% endhighlight %}



{% highlight r %}
# final
colnames(final.disposal) <- c("sido","sigungu",
                              "company_name","company_boss","location",
                              "disposal_target",
                              "lf_area","lf_capacity","lf_cumulate",
                              "disposal_15amount") 
{% endhighlight %}



{% highlight text %}
## Error in colnames(final.disposal) <- c("sido", "sigungu", "company_name", : object 'final.disposal' not found
{% endhighlight %}



{% highlight r %}
colnames(final.recycle) <- c("sido","sigungu",
                              "company_name","company_boss","location",
                              "category","capacity","disposal_15amount") 
{% endhighlight %}



{% highlight text %}
## Error in colnames(final.recycle) <- c("sido", "sigungu", "company_name", : object 'final.recycle' not found
{% endhighlight %}



{% highlight r %}
# overall
colnames(overall.recycle) <- c("sido","sigungu",
                              "company_name","company_boss","location",
                              "category","capacity","disposal_15amount") 
{% endhighlight %}



{% highlight text %}
## Error in colnames(overall.recycle) <- c("sido", "sigungu", "company_name", : object 'overall.recycle' not found
{% endhighlight %}

### (2) Data Handling : middle.disposal

{% highlight r %}
# combine disposal columns to one 
## change column class
for( i in c("ic","md","cd","bd","etcd")) {
    middle.disposal[, i] <- as.character(middle.disposal[, i])
}
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'middle.disposal' not found
{% endhighlight %}



{% highlight r %}
## make blank to NA
for (i in names(middle.disposal)[c(7:11)]) {
    if( i == "bd"){
        next()
    } else {
        middle.disposal[middle.disposal[, i] == "", i] <- NA
    }
}
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'middle.disposal' not found
{% endhighlight %}



{% highlight r %}
## combine disposal column
middle.disposal$category <- dplyr::coalesce(middle.disposal$ic, 
                                            middle.disposal$md, 
                                            middle.disposal$cd, 
                                            middle.disposal$bd,
                                            middle.disposal$etcd)
{% endhighlight %}



{% highlight text %}
## Error in list2(...): object 'middle.disposal' not found
{% endhighlight %}



{% highlight r %}
## featureSelection
middle.disposal%>%
    select(-c(ic,md,cd,bd,etcd)) -> middle.disposal
{% endhighlight %}



{% highlight text %}
## Error in eval(lhs, parent, parent): object 'middle.disposal' not found
{% endhighlight %}



{% highlight r %}
names(middle.disposal)
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'middle.disposal' not found
{% endhighlight %}



{% highlight r %}
middle.disposal <- middle.disposal[,c(1,2,4:6,3,7,8)]
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'middle.disposal' not found
{% endhighlight %}


# *import saving file* 

{% highlight r %}
disposal.local <- read.csv("disposal.local.csv")
occurence.local <- read.csv("occurrence.local.csv")
{% endhighlight %}
#

# 3. integrate : collect.occurrance
:occurrance measured by colletion

{% highlight r %}
# make sure that the 2 data columns are equal
ncol(collect.lifeBusiness) # 13,560 row
ncol(collect.construction) # 1,497 row  

# delete duplicated row and change type vlaue 
collect.lifeBusiness <- collect.lifeBusiness[!duplicated(collect.lifeBusiness$company_name), ] 
collect.lifeBusiness$type <- as.character(collect.lifeBusiness$type)
collect.lifeBusiness[ ,"type"] <- "<U+653C><U+3E63>ƒ<U+653C><U+3E64>™œ/<U+653C><U+3E63>‚¬<U+653C><U+3E63>—…/<U+653C><U+3E63>Œ<U+653C><U+3E63>‹"
 
# rbind
collect.occurrance <- rbind(collect.lifeBusiness, collect.construction)

# Data handling
names(collect.occurrance)[6] <- "collect_15amount"
collect.occurrance%>%
    mutate(collect_15amount = as.numeric(round(collect_15amount, digits = 2)))%>%
    rowwise()%>%
    mutate(company = paste0(company_name,"_",company_boss)) %>%
    select(-c(company_name,company_boss))  %>%
    arrange(sido, sigungu,company) -> collect.occurrance

collect.occurrance <- collect.occurrance[c(1,2,6,3,5,4)]
head(collect.occurrance)
{% endhighlight %}



{% highlight text %}
## Error: invalid multibyte character in parser at line 8
{% endhighlight %}




# 4. integrate : mfo.disposal
: middle/final/overall disposal

## 1) middle

{% highlight r %}
names(middle.disposal)
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'middle.disposal' not found
{% endhighlight %}



{% highlight r %}
names(middle.recycle)
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'middle.recycle' not found
{% endhighlight %}



{% highlight r %}
names(middle.construction)
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'middle.construction' not found
{% endhighlight %}



{% highlight r %}
# data handling
for(i in c("middle.disposal","middle.recycle","middle.construction")) {
    i %in% ls(envir = .GlobalEnv)
    data <- get(i, envir = .GlobalEnv)
    if( i == "middle.construction") {
        data%>%
            rowwise()%>%
            mutate(lf_area = as.numeric(gsub(",", "", lf_area)),
                disposal_15amount = as.numeric(gsub(",", "",disposal_15amount)),
                capacity = as.numeric(str_split(capacity, pattern = " ")[[1]][1]),
                category = "ë§¤ë¦½",
                company = paste0(company_name,"_",company_boss))%>%
            select(-c(company_boss,company_name)) -> data
        
        
    } else{
        data%>%
            mutate(company = paste0(company_name,"_",company_boss),
                   disposal_15amount = as.numeric(gsub(",", "",disposal_15amount)))%>%
            select(-c(company_boss,company_name)) -> data

    }

    # list.wise deletion
    data[is.na(data$disposal_15amount) == TRUE, "disposal_15amount"] <- 0
    data <- data[data$sido != "",]
    assign(x = i, value = data)
    head(i)
}
{% endhighlight %}



{% highlight text %}
## Error in get(i, envir = .GlobalEnv): object 'middle.disposal' not found
{% endhighlight %}



{% highlight r %}
# reorder and selection the column
middle.construction <- middle.construction[c(1,2,3,7,5,6,8)]
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'middle.construction' not found
{% endhighlight %}


{% highlight r %}
# merge 3 middle data 
m.disposal <- do.call("rbind", list(middle.disposal, 
                                    middle.recycle, 
                                    middle.construction))
{% endhighlight %}



{% highlight text %}
## Error in do.call("rbind", list(middle.disposal, middle.recycle, middle.construction)): object 'middle.disposal' not found
{% endhighlight %}



{% highlight r %}
m.disposal%>%
    arrange(sido, sigungu,company) -> m.disposal 
{% endhighlight %}



{% highlight text %}
## Error in eval(lhs, parent, parent): object 'm.disposal' not found
{% endhighlight %}


## 2) final

{% highlight r %}
names(final.disposal)
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'final.disposal' not found
{% endhighlight %}



{% highlight r %}
names(final.recycle)
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'final.recycle' not found
{% endhighlight %}



{% highlight r %}
# final.disposal
final.disposal%>%
    rename(capacity = lf_capacity) %>%
    mutate(category = "ë§¤ë¦½",
           company = paste0(company_name,"_",company_boss),
           capacity = as.numeric(gsub(",", "",capacity)),
           disposal_15amount = as.numeric(gsub(",", "",disposal_15amount)))%>%
    select(-c(company_boss,company_name,
              disposal_target,lf_area,lf_cumulate)) -> final.disposal
{% endhighlight %}



{% highlight text %}
## Error in eval(lhs, parent, parent): object 'final.disposal' not found
{% endhighlight %}



{% highlight r %}
final.disposal <- final.disposal[c("sido","sigungu","location",
                                   "category","capacity",
                                   "disposal_15amount","company")]
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'final.disposal' not found
{% endhighlight %}



{% highlight r %}
# final.recycle
final.recycle%>%
    mutate(company = paste0(company_name,"_",company_boss),
           capacity = as.numeric(gsub(",", "",capacity)),
           disposal_15amount = as.numeric(gsub(",", "",disposal_15amount)))%>%
    select(-c(company_boss,company_name)) -> final.recycle
{% endhighlight %}



{% highlight text %}
## Error in eval(lhs, parent, parent): object 'final.recycle' not found
{% endhighlight %}



{% highlight r %}
final.recycle <- final.recycle[c("sido","sigungu","location",
                                 "category","capacity",
                                 "disposal_15amount","company")]
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'final.recycle' not found
{% endhighlight %}


{% highlight r %}
# merge 2 final data 
f.disposal <- do.call("rbind", list(final.disposal, # merge
                                    final.recycle))
{% endhighlight %}



{% highlight text %}
## Error in do.call("rbind", list(final.disposal, final.recycle)): object 'final.disposal' not found
{% endhighlight %}



{% highlight r %}
f.disposal <- f.disposal[f.disposal$sido != "",] # listwise deletion
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'f.disposal' not found
{% endhighlight %}



{% highlight r %}
f.disposal%>%
    arrange(sido, sigungu, company) -> f.disposal # column arrange 
{% endhighlight %}



{% highlight text %}
## Error in eval(lhs, parent, parent): object 'f.disposal' not found
{% endhighlight %}

## 3) overall

{% highlight r %}
head(overall.recycle)
{% endhighlight %}



{% highlight text %}
## Error in head(overall.recycle): object 'overall.recycle' not found
{% endhighlight %}



{% highlight r %}
overall.recycle%>%
    mutate(company = paste0(company_name,"_",company_boss),
           capacity = as.numeric(gsub(",", "",capacity)),
           disposal_15amount = as.numeric(gsub(",", "",disposal_15amount)))%>%
    select(-c(company_boss,company_name)) -> overall.recycle
{% endhighlight %}



{% highlight text %}
## Error in eval(lhs, parent, parent): object 'overall.recycle' not found
{% endhighlight %}



{% highlight r %}
overall.recycle <- overall.recycle[c("sido","sigungu","location",
                                     "category","capacity",
                                     "disposal_15amount","company")] # 
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'overall.recycle' not found
{% endhighlight %}



{% highlight r %}
o.disposal <- overall.recycle[overall.recycle$sido != "",] # listwise deletion
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'overall.recycle' not found
{% endhighlight %}

## 4) make : mfo.disposal

{% highlight r %}
mfo.disposal <- do.call("rbind", list(m.disposal, # merge
                                      f.disposal,
                                      o.disposal))
{% endhighlight %}



{% highlight text %}
## Error in do.call("rbind", list(m.disposal, f.disposal, o.disposal)): object 'm.disposal' not found
{% endhighlight %}



{% highlight r %}
mfo.disposal[is.na(mfo.disposal$disposal_15amount) == TRUE,"disposal_15amount"] <- 0
{% endhighlight %}



{% highlight text %}
## Error in mfo.disposal[is.na(mfo.disposal$disposal_15amount) == TRUE, "disposal_15amount"] <- 0: object 'mfo.disposal' not found
{% endhighlight %}

*target data* 
 - collect.occurrance
 - mfo.disposal

## 5) GeoCode column

{% highlight r %}
for ( i in c("mfo.disposal", "collect.occurrance")) {
    i %in% ls(envir = .GlobalEnv)
    data <- get(i, envir = .GlobalEnv)

    data%>%
        mutate(sido = as.character(sido),
               sigungu = as.character(sigungu),
               location = as.character(location)) %>%
        mutate(geocode = paste0(sido," ",sigungu," ",location)) -> data 
    
    assign(x = i, value = data)
    print(paste0(i,"_done"))
}
{% endhighlight %}



{% highlight text %}
## Error in get(i, envir = .GlobalEnv): object 'mfo.disposal' not found
{% endhighlight %}



{% highlight r %}
head(mfo.disposal)
{% endhighlight %}



{% highlight text %}
## Error in head(mfo.disposal): object 'mfo.disposal' not found
{% endhighlight %}



{% highlight r %}
head(collect.occurrance)        
{% endhighlight %}



{% highlight text %}
## Error in head(collect.occurrance): object 'collect.occurrance' not found
{% endhighlight %}
## *saving target data*

{% highlight r %}
write.csv(x = collect.occurrance, file = "collect.occurrance.csv", row.names = FALSE)
{% endhighlight %}



{% highlight text %}
## Error in is.data.frame(x): object 'collect.occurrance' not found
{% endhighlight %}



{% highlight r %}
write.csv(x = mfo.disposal, file = "mfo.disposal.csv", row.names = FALSE)
{% endhighlight %}



{% highlight text %}
## Error in is.data.frame(x): object 'mfo.disposal' not found
{% endhighlight %}



# 4. VIS_1 
#: Disposal & Occurrence
## 1) Spatial Data

{% highlight r %}
library(rgdal)
# data import
korea.sp <- readOGR("C:/Users/TaeHwan/Desktop/0. R/0. Kaggle/9. 2018_3rd_publicData_competition/sigungu/sigungu.shp",
                    p4s = "+proj=tmerc +lat_0=38 +lon_0=127 +k=1 +x_0=200000 
                    +y_0=500000 +ellps=bessel +units=m +no_defs",
                    encoding = "UTF8")
{% endhighlight %}



{% highlight text %}
## OGR data source with driver: ESRI Shapefile 
## Source: "C:\Users\TaeHwan\Desktop\0. R\0. Kaggle\9. 2018_3rd_publicData_competition\sigungu\sigungu.shp", layer: "sigungu"
## with 252 features
## It has 6 fields
{% endhighlight %}



{% highlight r %}
sido.code <- read.csv("C:/Users/TaeHwan/Desktop/0. R/0. Kaggle/9. 2018_3rd_publicData_competition/sigungu/sido_code.csv")

# coordinate system
wgs <- "+proj=longlat +datum=WGS84 +no_defs +ellps=WGS84 +towgs84=0,0,0"
korea.wgs <- spTransform(korea.sp, CRS(wgs))
korea.df <- data.frame(korea.wgs)

# merge
korea.re <- korea.df %>%
    mutate(sido.code = substr(SIGUNGU_CD, 1, 2))

korea.re <- merge(korea.re, sido.code, 
                  by.x = "sido.code", by.y = "sido_code",
                  all.x = TRUE)
{% endhighlight %}


## 2) Merge(Spatial Data & Occurrence / Disposal)

{% highlight r %}
# dissolve
korea.re$SIGUNGU_NM <- as.character(korea.re$SIGUNGU_NM)
dissolve.lnfo <- nchar(korea.re$SIGUNGU_NM) >= 5
korea.re[dissolve.lnfo, 5] <- substr(korea.re[dissolve.lnfo, 5], 1, 3)

# merge(occurrence)
korea.re <- korea.re %>%
  mutate(region = paste(sido_name, SIGUNGU_NM, sep = "_"))

occurrence.wgs <- merge(korea.re[, -c(6:7)], occurrence.local[, 3:20], 
                       by = "region", all.x = TRUE)
{% endhighlight %}



{% highlight text %}
## Error in merge(korea.re[, -c(6:7)], occurrence.local[, 3:20], by = "region", : object 'occurrence.local' not found
{% endhighlight %}



{% highlight r %}
disposal.wgs <- merge(korea.re[, -c(6:7)], disposal.local[, 3:20], 
                      by = "region", all.x = TRUE)
{% endhighlight %}

## 3) Arrange

{% highlight r %}
id.order1 <- order(occurrence.wgs$OBJECTID)
{% endhighlight %}



{% highlight text %}
## Error in order(occurrence.wgs$OBJECTID): object 'occurrence.wgs' not found
{% endhighlight %}



{% highlight r %}
id.order2 <- order(disposal.wgs$OBJECTID)

occurrence.wgs <- occurrence.wgs[id.order1, ]
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'occurrence.wgs' not found
{% endhighlight %}



{% highlight r %}
disposal.wgs <- disposal.wgs[id.order2, ]
{% endhighlight %}

## 4) Mapping

{% highlight r %}
library(classInt)
library(RColorBrewer)
# x, y axis
x <- bbox(korea.wgs)

# color
display.brewer.all()
{% endhighlight %}

![plot of chunk unnamed-chunk-31](/assets/article_images/study/2018-08-21-PublicData-Competition-trashAnalasys/unnamed-chunk-31-1.png)

{% highlight r %}
purples <- brewer.pal(5, "Purples")

# class
houseTotalClass <- classIntervals(occurrence.wgs$houseLife_total, n = 5,
                                  style = "jenks")
{% endhighlight %}



{% highlight text %}
## Error in is.factor(var): object 'occurrence.wgs' not found
{% endhighlight %}



{% highlight r %}
houseTotalClass <- classIntervals(occurrence.wgs$houseLife_total, n = 5,
                                  style = 'quantile')
{% endhighlight %}



{% highlight text %}
## Error in is.factor(var): object 'occurrence.wgs' not found
{% endhighlight %}



{% highlight r %}
# legend break
a <- houseTotalClass[[2]]
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'houseTotalClass' not found
{% endhighlight %}



{% highlight r %}
# plot
plot(korea.wgs, col = findColours(houseTotalClass, purples), border = FALSE)
{% endhighlight %}



{% highlight text %}
## Error in findColours(houseTotalClass, purples): object 'houseTotalClass' not found
{% endhighlight %}



{% highlight r %}
axis(1, at = seq(x[1], x[3], by = ((x[3] - x[1]) / 4)), 
     labels = parse(text = degreeLabelsEW(seq(x[1], x[3],
                                          by = ((x[3] - x[1]) / 4)))))
axis(2, at = seq(x[2], x[4], by = ((x[4] - x[2]) / 4)), 
     labels = parse(text = degreeLabelsNS(seq(x[2], x[4], 
                                          by = ((x[4] - x[2]) / 4)))))
{% endhighlight %}

![plot of chunk unnamed-chunk-31](/assets/article_images/study/2018-08-21-PublicData-Competition-trashAnalasys/unnamed-chunk-31-2.png)


# 5. VIS_2
# : collect.occurrance & mfo.disposal

{% highlight r %}
head(collect.occurrance)
{% endhighlight %}



{% highlight text %}
## Error in head(collect.occurrance): object 'collect.occurrance' not found
{% endhighlight %}



{% highlight r %}
head(mfo.disposal)
{% endhighlight %}



{% highlight text %}
## Error in head(mfo.disposal): object 'mfo.disposal' not found
{% endhighlight %}
## 1) rgdal
### (1) rgdal base map

{% highlight r %}
library(rgdal)
korea.sp <- readOGR("C:/Users/TaeHwan/Desktop/0. R/0. Kaggle/9. 2018_3rd_publicData_competition/sigungu/sigungu.shp",
                    p4s = "+proj=tmerc +lat_0=38 +lon_0=127 +k=1 +x_0=200000 
                    +y_0=500000 +ellps=bessel +units=m +no_defs",
                    encoding = "UTF8")
{% endhighlight %}



{% highlight text %}
## OGR data source with driver: ESRI Shapefile 
## Source: "C:\Users\TaeHwan\Desktop\0. R\0. Kaggle\9. 2018_3rd_publicData_competition\sigungu\sigungu.shp", layer: "sigungu"
## with 252 features
## It has 6 fields
{% endhighlight %}



{% highlight r %}
korea.df <- data.frame(korea.sp) # we can also see the shp data as 
class(korea.sp)
{% endhighlight %}



{% highlight text %}
## [1] "SpatialPolygonsDataFrame"
## attr(,"package")
## [1] "sp"
{% endhighlight %}

### (2) converse tm coordination  to x&y
: using *spTransform* function,
  change korea.sp's *tm* coordination to  *X & Y* coordination

{% highlight r %}
# Coordinate system
wgs <- CRS("+proj=longlat +datum=WGS84 +no_defs +ellps=WGS84 +towgs84=0,0,0")
korea.wgs <- spTransform(korea.sp, wgs)
korea.df <- data.frame(korea.wgs)
{% endhighlight %}


### (3) Geo_code Merge 
: *merge* function makes some na...so we using just *cbind*

{% highlight r %}
## a) collect.occurrance
collect.occurr.geo <- read.csv("geocoding_collect.csv")
collect.occurr.geo$Field_1 <- as.character(collect.occurr.geo$Field_1)

collect.occurr.wgs <- cbind(collect.occurrance,
                            collect.occurr.geo[,c("Field_1","x","y")]) 
{% endhighlight %}



{% highlight text %}
## Error in cbind(collect.occurrance, collect.occurr.geo[, c("Field_1", "x", : object 'collect.occurrance' not found
{% endhighlight %}



{% highlight r %}
collect.occurr.wgs[, "Field_1"] <- NULL
{% endhighlight %}



{% highlight text %}
## Error in collect.occurr.wgs[, "Field_1"] <- NULL: object 'collect.occurr.wgs' not found
{% endhighlight %}



{% highlight r %}
## b) mfo.disposal
mfo.disposal.geo <- read.csv("geocoding_disposal.csv")
mfo.disposal.geo$geocode <- as.character(mfo.disposal.geo$Field_1)

mfo.disposal.wgs <- cbind(mfo.disposal,
                          mfo.disposal.geo[,c("Field_1","x","y")]) 
{% endhighlight %}



{% highlight text %}
## Error in cbind(mfo.disposal, mfo.disposal.geo[, c("Field_1", "x", "y")]): object 'mfo.disposal' not found
{% endhighlight %}



{% highlight r %}
mfo.disposal.wgs[, "Field_1"] <- NULL
{% endhighlight %}



{% highlight text %}
## Error in mfo.disposal.wgs[, "Field_1"] <- NULL: object 'mfo.disposal.wgs' not found
{% endhighlight %}



{% highlight r %}
### make the same column name and order
colnames(collect.occurr.wgs)[6] <- "15amount"
{% endhighlight %}



{% highlight text %}
## Error in colnames(collect.occurr.wgs)[6] <- "15amount": object 'collect.occurr.wgs' not found
{% endhighlight %}



{% highlight r %}
colnames(mfo.disposal.wgs)[c(4, 6)] <- c("type", "15amount")
{% endhighlight %}



{% highlight text %}
## Error in colnames(mfo.disposal.wgs)[c(4, 6)] <- c("type", "15amount"): object 'mfo.disposal.wgs' not found
{% endhighlight %}



{% highlight r %}
mfo.disposal.wgs <- mfo.disposal.wgs[c("sido", "sigungu", "company", "location", "type", "15amount", "geocode", "x", "y", "capacity")]
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'mfo.disposal.wgs' not found
{% endhighlight %}


### (4) Mapping_1 : Spatial Points

{% highlight r %}
for ( i in c("collect.occurr", "mfo.disposal")) {
    assign(paste0(i,".point"),
           SpatialPoints(get(paste0(i,".wgs"))[, c("x","y")]
                         ,proj4string = wgs))
    plot(korea.wgs)                # background map 
    plot(get(paste0(i,".point")), add = TRUE) # target point data
    print(i)
    }
{% endhighlight %}



{% highlight text %}
## Error in get(paste0(i, ".wgs")): object 'collect.occurr.wgs' not found
{% endhighlight %}

### (5) Mapping_2 : Rating each point by amount

{% highlight r %}
# classfy the review count
library(classInt)
for( i in c("collect.occurr.wgs","mfo.disposal.wgs")) {
    data <- get(i)
    amountClass <- classIntervals(data[,"15amount"],
                                  n = 3,
                                  style = "quantile" ) 
    # why does"quantile" only devide the value into 4 class..?
    
    data$amountLevel <- as.numeric(cut(data[, "15amount"],
                                       breaks = amountClass$brks,
                                       labels = as.character(1:3)))
    data[is.na(data$amountLevel) == TRUE,"amountLevel"] <- 0
    assign(i,data)
}                      
{% endhighlight %}



{% highlight text %}
## Error in get(i): object 'collect.occurr.wgs' not found
{% endhighlight %}

{% highlight r %}
# plotting
library(RColorBrewer)
orrd <- brewer.pal(3, "OrRd")
orrd
{% endhighlight %}



{% highlight text %}
## [1] "#FEE8C8" "#FDBB84" "#E34A33"
{% endhighlight %}



{% highlight r %}
for ( i in c("collect.occurr", "mfo.disposal")) {
    plot(korea.wgs, border = "Grey 50")  # background map 
    plot(get(paste0(i,".point")), add = TRUE,
         pch = 19, cex = 1.2, 
         col = findColours(amountClass, orrd))
    # *amountClass* has geo and class information
    print(i)
}
{% endhighlight %}



{% highlight text %}
## Error in get(paste0(i, ".point")): object 'collect.occurr.point' not found
{% endhighlight %}

![plot of chunk unnamed-chunk-38](/assets/article_images/study/2018-08-21-PublicData-Competition-trashAnalasys/unnamed-chunk-38-1.png)

*many way of classIntervals style*
 | - "fixed"  | - "sd"      | - "equal"  |
 | - "pretty" | - "quantile"| - "kmeans" |
 | - "hclust" | - "bclust"  | - "fisher" |
 | - "jenks"  | 
 

## 2) ggmap
### (1) merge : rbind

{% highlight r %}
collect.occurr.wgs %>%
    mutate(division = "occurr") %>%
    select("geocode", "type", "division",
           "15amount", "x", "y", "amountLevel") -> collect.m
{% endhighlight %}



{% highlight text %}
## Error in eval(lhs, parent, parent): object 'collect.occurr.wgs' not found
{% endhighlight %}



{% highlight r %}
mfo.disposal.wgs %>%
    mutate(division = "disposal") %>%
    select("geocode", "type", "division",
           "15amount", "x", "y", "amountLevel") -> disposal.m
{% endhighlight %}



{% highlight text %}
## Error in eval(lhs, parent, parent): object 'mfo.disposal.wgs' not found
{% endhighlight %}



{% highlight r %}
ggmap.df <- rbind(collect.m, disposal.m)
{% endhighlight %}



{% highlight text %}
## Error in rbind(collect.m, disposal.m): object 'collect.m' not found
{% endhighlight %}

### (2) Maaping_1

{% highlight r %}
ggplot() + 
  geom_polygon(data = korea.wgs, aes(x = long, y = lat, group = group), 
               fill = 'white', color = 'Grey 50') +
  geom_point(data = disposal.m, aes(x = x, y = y, alpha = 0.1, 
                                        color = "indianred")) +
  geom_point(data = collect.m, aes(x = x, y = y, alpha = 0.1, 
                                       color = "skyblue")) +
  guides(alpha = "none")
{% endhighlight %}



{% highlight text %}
## Error in fortify(data): object 'disposal.m' not found
{% endhighlight %}

### (2) Maaping_2 
: using ggamp

{% highlight r %}
library(ggmap)
basemap <- get_map(location = "south korea", 
                   source = "google", 
                   maptype = "roadmap",
                   zoom = 7)

ggmap(basemap) +
    geom_point(data = ggmap.df,
               aes(x = x, y = y, alpha = 0.01, color = division, size = amountLevel*0.001)) +
    guides(alpha = "none")
{% endhighlight %}



{% highlight text %}
## Error in fortify(data): object 'ggmap.df' not found
{% endhighlight %}


# 6. VIS_3 : differential map 
## 1) Data handling
### (1) group sum

{% highlight r %}
# group sum by sigungu and type
for( i in c("collect.occurr", "mfo.disposal")) {
    data <- get(paste0(i,".wgs"))
    #
    data %>%
        mutate(division = str_split(i, pattern = "\\.")[[1]][2]) %>%
        group_by(sido, sigungu) %>%
        mutate(amount_sum = sum(`15amount`)) %>%
        group_by(sido, sigungu, type) %>%
        mutate(type_sum = sum(`15amount`)) %>%
        select(c(sido, sigungu, division, type, amount_sum, type_sum)) -> tmp
    
    tmp <- tmp[duplicated(tmp) == FALSE,] # delete duplicated rows
    
    assign(x = paste0(i,".sum"), value = tmp)
    print(i)
}
{% endhighlight %}



{% highlight text %}
## Error in get(paste0(i, ".wgs")): object 'collect.occurr.wgs' not found
{% endhighlight %}

### (2) change longForm to wideForm

{% highlight r %}
# rbind 
waste.sum <- rbind(collect.occurr.sum, mfo.disposal.sum)
{% endhighlight %}



{% highlight text %}
## Error in rbind(collect.occurr.sum, mfo.disposal.sum): object 'collect.occurr.sum' not found
{% endhighlight %}



{% highlight r %}
waste.sum <- waste.sum[order(waste.sum$sido,waste.sum$sigungu,waste.sum$division,waste.sum$type),] # sorting
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'waste.sum' not found
{% endhighlight %}



{% highlight r %}
head(waste.sum)
{% endhighlight %}



{% highlight text %}
## Error in head(waste.sum): object 'waste.sum' not found
{% endhighlight %}



{% highlight r %}
# divide the data into overall and type
waste.sum.type <- waste.sum[-5]
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'waste.sum' not found
{% endhighlight %}



{% highlight r %}
waste.sum <- waste.sum[,-c(4,6)]
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'waste.sum' not found
{% endhighlight %}



{% highlight r %}
waste.sum <- waste.sum[duplicated(waste.sum) == FALSE,]
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'waste.sum' not found
{% endhighlight %}



{% highlight r %}
# change longForm to wideForm
library(reshape2)
waste.sum.wide <- dcast(waste.sum,
                        sido+sigungu ~ division) # using '+', for 2 id variables
{% endhighlight %}



{% highlight text %}
## Error in "value" %in% names(df): object 'waste.sum' not found
{% endhighlight %}



{% highlight r %}
# interpolation the NA
waste.sum.wide[is.na(waste.sum.wide$disposal) == TRUE, "disposal"] <- 0
{% endhighlight %}



{% highlight text %}
## Error in waste.sum.wide[is.na(waste.sum.wide$disposal) == TRUE, "disposal"] <- 0: object 'waste.sum.wide' not found
{% endhighlight %}



{% highlight r %}
waste.sum.wide[is.na(waste.sum.wide$occurr) == TRUE, "occurr"] <- 0
{% endhighlight %}



{% highlight text %}
## Error in waste.sum.wide[is.na(waste.sum.wide$occurr) == TRUE, "occurr"] <- 0: object 'waste.sum.wide' not found
{% endhighlight %}



{% highlight r %}
# maket target column : diff
waste.sum.wide %>%
    mutate(diff = round(occurr - disposal, digits = 0),
           region = paste0(sido,"_", sigungu)) -> waste.sum.wide
{% endhighlight %}



{% highlight text %}
## Error in eval(lhs, parent, parent): object 'waste.sum.wide' not found
{% endhighlight %}



## 2) Spatial Data

{% highlight r %}
library(rgdal)
# data import
korea.sp <- readOGR("C:/Users/TaeHwan/Desktop/0. R/0. Kaggle/9. 2018_3rd_publicData_competition/sigungu/sigungu.shp",
                    p4s = "+proj=tmerc +lat_0=38 +lon_0=127 +k=1 +x_0=200000 
                    +y_0=500000 +ellps=bessel +units=m +no_defs",
                    encoding = "UTF8")
{% endhighlight %}



{% highlight text %}
## OGR data source with driver: ESRI Shapefile 
## Source: "C:\Users\TaeHwan\Desktop\0. R\0. Kaggle\9. 2018_3rd_publicData_competition\sigungu\sigungu.shp", layer: "sigungu"
## with 252 features
## It has 6 fields
{% endhighlight %}



{% highlight r %}
sido.code <- read.csv("C:/Users/TaeHwan/Desktop/0. R/0. Kaggle/9. 2018_3rd_publicData_competition/sigungu/sido_code.csv")

# coordinate system
wgs <- "+proj=longlat +datum=WGS84 +no_defs +ellps=WGS84 +towgs84=0,0,0"
korea.wgs <- spTransform(korea.sp, CRS(wgs))
korea.df <- data.frame(korea.wgs)

# merge
korea.re <- korea.df %>%
    mutate(sido.code = substr(SIGUNGU_CD, 1, 2))

korea.re <- merge(korea.re, sido.code, 
                  by.x = "sido.code", by.y = "sido_code",
                  all.x = TRUE)

# dissolve
korea.re$SIGUNGU_NM <- as.character(korea.re$SIGUNGU_NM)
dissolve.lnfo <- nchar(korea.re$SIGUNGU_NM) >= 5
korea.re[dissolve.lnfo, 5] <- substr(korea.re[dissolve.lnfo, 5], 1, 3)
{% endhighlight %}

### (2) Merge(Spatial Data & waste.sum.wide)

{% highlight r %}
# merge
korea.re <- korea.re %>%
  mutate(region = paste(sido_name, SIGUNGU_NM, sep = "_"))

waste.sum.wgs <- merge(korea.re[, -c(6:7)], waste.sum.wide[,-c(1:2)], 
                       by = "region", all.x = TRUE)
{% endhighlight %}



{% highlight text %}
## Error in merge(korea.re[, -c(6:7)], waste.sum.wide[, -c(1:2)], by = "region", : object 'waste.sum.wide' not found
{% endhighlight %}



{% highlight r %}
# Arrange
id.order <- order(waste.sum.wgs$OBJECTID)
{% endhighlight %}



{% highlight text %}
## Error in order(waste.sum.wgs$OBJECTID): object 'waste.sum.wgs' not found
{% endhighlight %}



{% highlight r %}
waste.sum.wgs <- waste.sum.wgs[id.order1, ]
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'waste.sum.wgs' not found
{% endhighlight %}

## 3) Mapping

{% highlight r %}
library(classInt)
library(RColorBrewer)
# x, y axis
x <- bbox(korea.wgs)

# color
display.brewer.all()
{% endhighlight %}

![plot of chunk unnamed-chunk-46](/assets/article_images/study/2018-08-21-PublicData-Competition-trashAnalasys/unnamed-chunk-46-1.png)

{% highlight r %}
RdYlBu <- brewer.pal(10, "RdYlBu")

# class : how do i divide the minus class and attach lagend
wasteSumClass.jenks <- classIntervals(waste.sum.wgs$diff, n = 10,
                                  style = "jenks")
{% endhighlight %}



{% highlight text %}
## Error in is.factor(var): object 'waste.sum.wgs' not found
{% endhighlight %}



{% highlight r %}
wasteSumClass.quantile <- classIntervals(waste.sum.wgs$diff, n = 10,
                                  style = 'quantile')
{% endhighlight %}



{% highlight text %}
## Error in is.factor(var): object 'waste.sum.wgs' not found
{% endhighlight %}



{% highlight r %}
# legend break
lg_jks <- wasteSumClass.jenks[[2]]
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'wasteSumClass.jenks' not found
{% endhighlight %}



{% highlight r %}
lg_qt <- wasteSumClass.quantile[[2]]
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'wasteSumClass.quantile' not found
{% endhighlight %}



{% highlight r %}
# plot_1 : jenks
plot(korea.wgs, col = findColours(wasteSumClass.jenks, RdYlBu), border = FALSE)
{% endhighlight %}



{% highlight text %}
## Error in findColours(wasteSumClass.jenks, RdYlBu): object 'wasteSumClass.jenks' not found
{% endhighlight %}



{% highlight r %}
axis(1, at = seq(x[1], x[3], by = ((x[3] - x[1]) / 4)), 
     labels = parse(text = degreeLabelsEW(seq(x[1], x[3],
                                          by = ((x[3] - x[1]) / 4)))))
axis(2, at = seq(x[2], x[4], by = ((x[4] - x[2]) / 4)), 
     labels = parse(text = degreeLabelsNS(seq(x[2], x[4], 
                                          by = ((x[4] - x[2]) / 4)))))
{% endhighlight %}

![plot of chunk unnamed-chunk-46](/assets/article_images/study/2018-08-21-PublicData-Competition-trashAnalasys/unnamed-chunk-46-2.png)

{% highlight r %}
legend(131.20, 38.61, fill = RdYlBu,
       legend = c(paste("Less than", lg_jks[2]),
                  paste(lg_jks[2], "-", lg_jks[3]),
                  paste(lg_jks[3], "-", lg_jks[4]),
                  paste(lg_jks[4], "-", lg_jks[5]),
                  paste(lg_jks[5], "-", lg_jks[6]),
                  paste(lg_jks[6], "-", lg_jks[7]),
                  paste(lg_jks[7], "-", lg_jks[8]),
                  paste(lg_jks[8], "-", lg_jks[9]),
                  paste(lg_jks[9], "-", lg_jks[10]),
                  paste("More than", lg_jks[10])),
       title = "Collect - Disposal", cex = 1, bty = "n")
{% endhighlight %}



{% highlight text %}
## Error in paste("Less than", lg_jks[2]): object 'lg_jks' not found
{% endhighlight %}



{% highlight r %}
# plot_2 : quantile
#png(filename = "quantile.png", width = 800, height = 600)
plot(korea.wgs, col = findColours(wasteSumClass.quantile, RdYlBu), border = FALSE)
{% endhighlight %}



{% highlight text %}
## Error in findColours(wasteSumClass.quantile, RdYlBu): object 'wasteSumClass.quantile' not found
{% endhighlight %}



{% highlight r %}
axis(1, at = seq(x[1], x[3], by = ((x[3] - x[1]) / 4)), 
     labels = parse(text = degreeLabelsEW(seq(x[1], x[3],
                                          by = ((x[3] - x[1]) / 4)))))
axis(2, at = seq(x[2], x[4], by = ((x[4] - x[2]) / 4)), 
     labels = parse(text = degreeLabelsNS(seq(x[2], x[4], 
                                          by = ((x[4] - x[2]) / 4)))))
{% endhighlight %}

![plot of chunk unnamed-chunk-46](/assets/article_images/study/2018-08-21-PublicData-Competition-trashAnalasys/unnamed-chunk-46-3.png)

{% highlight r %}
legend(131.20, 38.61, fill = RdYlBu,
       legend = c(paste("Less than", lg_qt[2]),
                  paste(lg_qt[2], "-", lg_qt[3]),
                  paste(lg_qt[3], "-", lg_qt[4]),
                  paste(lg_qt[4], "-", lg_qt[5]),
                  paste(lg_qt[5], "-", lg_qt[6]),
                  paste(lg_qt[6], "-", lg_qt[7]),
                  paste(lg_qt[7], "-", lg_qt[8]),
                  paste(lg_qt[8], "-", lg_qt[9]),
                  paste(lg_qt[9], "-", lg_qt[10]),
                  paste("More than", lg_qt[10])),
       title = "Disposal - Collect", cex = 1, bty = "n")
{% endhighlight %}



{% highlight text %}
## Error in paste("Less than", lg_qt[2]): object 'lg_qt' not found
{% endhighlight %}



{% highlight r %}
#dev.off()
{% endhighlight %}

# 7. VIS_4 : Type
## 1) Data handling

{% highlight r %}
waste.sum.type$type_2 <- NA
# disposal
waste.sum.type[str_detect(waste.sum.type$type,
                          pattern = "<U+653C><U+3E63>†Œê°<U+383C><U+3E31>"), "type_2"] <- "incineration"
waste.sum.type[str_detect(waste.sum.type$type,
                          pattern = "ë§¤ë¦½"), "type_2"] <- "landfill"
waste.sum.type[is.na(waste.sum.type$type_2) == TRUE &
                   waste.sum.type$division != "occurr", "type_2"] <- "recycle"

# occurr
waste.sum.type[is.na(waste.sum.type$type_2) == TRUE &
                   waste.sum.type$division == "occurr" &
                   str_detect(waste.sum.type$type, pattern = "ê±´ì¶•"), "type_2"] <- "waste_construct"
waste.sum.type[is.na(waste.sum.type$type_2) == TRUE &
                   waste.sum.type$division == "occurr" &
                   str_detect(waste.sum.type$type, pattern = "<U+653C><U+3E63>ƒ<U+653C><U+3E64>™œ/<U+653C><U+3E63>‚¬<U+653C><U+3E63>—…/<U+653C><U+3E63>Œ<U+653C><U+3E63>‹"), "type_2"] <- "waste_life"

waste.sum.type.vector <- waste.sum.type$type
waste.sum.type$type <- NULL
colnames(waste.sum.type)[5] <- "type"

# aggregate the recylce value
waste.sum.type %>%
    group_by(sido, sigungu, division, type) %>%
    mutate(type_sum = round(sum(type_sum),2)) %>%
    distinct(sido,sigungu, division, type_sum, type) -> waste.sum.type

write.csv(x = waste.sum.type, file = "waste.sum.type.csv", row.names = FALSE)
{% endhighlight %}



{% highlight text %}
## Error: invalid multibyte character in parser at line 4
{% endhighlight %}


{% highlight r %}
waste.sum.type %>%
    filter(division == "occurr") -> waste.sum.type.occurr
{% endhighlight %}



{% highlight text %}
## Error in eval(lhs, parent, parent): object 'waste.sum.type' not found
{% endhighlight %}



{% highlight r %}
waste.sum.type %>%
    filter(division == "disposal") -> waste.sum.type.disposal
{% endhighlight %}



{% highlight text %}
## Error in eval(lhs, parent, parent): object 'waste.sum.type' not found
{% endhighlight %}



{% highlight r %}
## type data ----
type_landfill <- waste.sum.type.disposal[waste.sum.type.disposal$type == "landfill","type_sum"]
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'waste.sum.type.disposal' not found
{% endhighlight %}



{% highlight r %}
type_incin <-waste.sum.type.disposal[waste.sum.type.disposal$type == "incineration","type_sum"]
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'waste.sum.type.disposal' not found
{% endhighlight %}



{% highlight r %}
type_recycle <- waste.sum.type.disposal[waste.sum.type.disposal$type == "recycle","type_sum"]
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'waste.sum.type.disposal' not found
{% endhighlight %}



{% highlight r %}
type_life <- waste.sum.type.occurr[waste.sum.type.occurr$type == "waste_life","type_sum"]
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'waste.sum.type.occurr' not found
{% endhighlight %}



{% highlight r %}
type_consturct <- waste.sum.type.occurr[waste.sum.type.occurr$type == "waste_construct","type_sum"]
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'waste.sum.type.occurr' not found
{% endhighlight %}


{% highlight r %}
#png(filename = paste0("type_sum",".png"), width = 800, height = 600)
waste.sum.type.occurr %>%
    group_by(type) %>%
    summarise(occurr_sum = sum(type_sum)) %>%
    ggplot(aes(x = type, y = occurr_sum, fill = type)) +
    geom_col() +
    geom_text(aes(label = round(occurr_sum, 0))) +
    theme(legend.position="none", 
          axis.text.x = element_text(angle = 0, face = "italic", vjust = 1 ,hjust = 1),
          plot.title = element_text(face = "bold.italic", hjust = 0.5)) 
{% endhighlight %}



{% highlight text %}
## Error in eval(lhs, parent, parent): object 'waste.sum.type.occurr' not found
{% endhighlight %}



{% highlight r %}
#dev.off()
{% endhighlight %}



## 2) Mapping
### (1) source

{% highlight r %}
type_1 <- classIntervals(type_landfill, 
                         n = 5, style = "quantile")
{% endhighlight %}



{% highlight text %}
## Error in is.factor(var): object 'type_landfill' not found
{% endhighlight %}



{% highlight r %}
type_2 <- classIntervals(type_incin,
                         n = 5, style = "quantile")
{% endhighlight %}



{% highlight text %}
## Error in is.factor(var): object 'type_incin' not found
{% endhighlight %}



{% highlight r %}
type_3 <- classIntervals(type_recycle, 
                         n = 5, style = "quantile")
{% endhighlight %}



{% highlight text %}
## Error in is.factor(var): object 'type_recycle' not found
{% endhighlight %}



{% highlight r %}
type_4 <- classIntervals(type_life,
                         n = 5, style = "quantile")
{% endhighlight %}



{% highlight text %}
## Error in is.factor(var): object 'type_life' not found
{% endhighlight %}



{% highlight r %}
type_5 <- classIntervals(type_consturct,
                         n = 5, style = "quantile")
{% endhighlight %}



{% highlight text %}
## Error in is.factor(var): object 'type_consturct' not found
{% endhighlight %}



{% highlight r %}
title <- c("disposal_landfill amount",
           "disposal_incineration amount",
           "disposal_recycle amount",
           "occurr_waste_life amount",
           "occurr_waste_construct amount")
{% endhighlight %}

### (2) mapping

{% highlight r %}
# color
blues <- brewer.pal(5, "Blues")
reds <- brewer.pal(5, "Reds")
color_tab <- c("reds", "reds", "reds", "blues", "blues")
# plot                
for( i in 1:5) {
#    png(filename = paste0(title[i],".png"), width = 800, height = 600)
    
    plot(korea.wgs, col = findColours(get(paste0("type_",i)), 
                                      get(color_tab[i])), border = FALSE, main = title[i])
    axis(1, at = seq(x[1], x[3], by = ((x[3] - x[1]) / 4)),
         labels = parse(text = degreeLabelsEW(seq(x[1], x[3],
                                                  by = ((x[3] - x[1]) / 4)))))
    axis(2, at = seq(x[2], x[4], by = ((x[4] - x[2]) / 4)), 
         labels = parse(text = degreeLabelsNS(seq(x[2], x[4],
                                                  by = ((x[4] - x[2]) / 4)))))
    legend(131.20, 38.61, fill = get(color_tab[i]),
               legend = c(paste("Less than", get(paste0("type_",i))[[2]][2]),
                          paste(get(paste0("type_",i))[[2]][2], "-", get(paste0("type_",i))[[2]][3]),
                          paste(get(paste0("type_",i))[[2]][3], "-", get(paste0("type_",i))[[2]][4]),
                          paste(get(paste0("type_",i))[[2]][4], "-", get(paste0("type_",i))[[2]][5]),
                          paste("More than", get(paste0("type_",i))[[2]][5])),
               title = title[i], cex = 1, bty = "n")

#    dev.off()
}            
{% endhighlight %}



{% highlight text %}
## Error in get(paste0("type_", i)): object 'type_1' not found
{% endhighlight %}

![plot of chunk unnamed-chunk-51](/assets/article_images/study/2018-08-21-PublicData-Competition-trashAnalasys/unnamed-chunk-51-1.png)


# 8. T-test

{% highlight r %}
waste.t.test <- t.test(waste.sum.wide$disposal, waste.sum.wide$occurr)
{% endhighlight %}



{% highlight text %}
## Error in t.test(waste.sum.wide$disposal, waste.sum.wide$occurr): object 'waste.sum.wide' not found
{% endhighlight %}



{% highlight r %}
waste.t.test$statistic
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'waste.t.test' not found
{% endhighlight %}



{% highlight r %}
waste.t.test$p.value
{% endhighlight %}



{% highlight text %}
## Error in eval(expr, envir, enclos): object 'waste.t.test' not found
{% endhighlight %}
 : p-value =  0.8672247 , which is bigger than 0.05. so we can't say that two groups are different


{% highlight r %}
waste.sum.wide %>%
    ggplot(aes(x = occurr, y = disposal, color = diff)) +
    geom_point(alpha = 0.5)    
{% endhighlight %}



{% highlight text %}
## Error in eval(lhs, parent, parent): object 'waste.sum.wide' not found
{% endhighlight %}
























