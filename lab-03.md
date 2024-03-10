Lab 03 - Nobel laureates
================
Yang
2024.03.10

### Load packages and data

``` r
library(tidyverse) 
```

    ## Warning: package 'tidyverse' was built under R version 4.3.3

    ## Warning: package 'readr' was built under R version 4.3.3

    ## Warning: package 'forcats' was built under R version 4.3.3

    ## Warning: package 'lubridate' was built under R version 4.3.3

``` r
nobel <- read_csv("data/nobel.csv")
```

## Exercises

### Exercise 1

``` r
nrow(nobel)
```

    ## [1] 935

``` r
ncol(nobel)
```

    ## [1] 26

### Exercise 2

``` r
library(tidyverse)
nobel_living <- nobel %>% 
  filter(is.na(died_date),
         !is.na(country),
         gender !="org")

#write.csv(nobel_living, "nobel_living2.csv", row.names = FALSE) 
```

you are left with a data frame with 228 observations.

``` r
library(dplyr)
library(tidyverse)
nobel_living<-nobel_living %>% 
  mutate(country_us = if_else(country == "USA","USA","other"))
nobel_living_science<-nobel_living %>% 
  filter(category %in% c("Physics", "Medicine", "Chemistry", "Economics"))
```

### Exercise 3

``` r
# 创建分面柱状图
# 使用ggplot2创建可视化
ggplot(nobel_living_science, aes(x = category, fill = country_us)) +
  geom_bar(position = "dodge") + # 使用"dodge"位置调整来并排显示条形
  facet_wrap(~ category) + # 按类别分面
  coord_flip() + # 翻转坐标，使条形呈水平方向
  labs(title = "Nobel Prize Laureates by Category and Country",
       x = "Category",
       y = "Count",
       fill = "Laureate Location") +
  theme_minimal()
```

![](lab-03_files/figure-gfm/exercise-3-1.png)<!-- --> \### Exercise 4

``` r
library(dplyr)
library(ggplot2)
nobel_living_science<- nobel_living_science %>% 
  mutate(born_country_us=if_else(born_country == "USA", "USA","Other")) 

# 创建图形
ggplot(nobel_living_science, aes(x = country_us, fill = born_country_us)) +
  geom_bar(position = "stack") + # 使用堆叠条形图来表示不同的出生国家
  facet_wrap(~ category) + # 为每个类别创建分面
  labs(title = "Nobel Prize Laureates by Category, Country, and Birthplace",
       x = "Country of Prize Reception",
       y = "Count of Laureates",
       fill = "Birth Country") +
  theme_minimal() +
  scale_fill_manual(values = c("USA" = "blue", "Other" = "red")) # 自定义填充颜色
```

![](lab-03_files/figure-gfm/exercise-4-1.png)<!-- -->

``` r
# 注意：根据实际的数据结构和需求，可能需要调整代码。

  # ggplot(nobel_born, aes(x = category, fill = born_country_us)) +
  # geom_bar(position = "dodge") + # 使用"dodge"位置调整来并排显示条形
  # facet_wrap(~ category) + # 按类别分面
  # coord_flip() + # 翻转坐标，使条形呈水平方向
  # labs(title = "Nobel Prize Laureates by Category and Born Country",
  #      x = "Category",
  #      y = "Count",
  #      fill = "Laureate Location") +
  # theme_minimal()
```

…

### Exercise 5

The plots in the Buzzfeed article are called waffle plots. You can find
the code used for making these plots in Buzzfeed’s GitHub repo (yes,
they have one!) here. You’re not expected to recreate them as part of
your assignment, but you’re welcomed to do so for fun!
link:<https://buzzfeednews.github.io/2017-01-immigration-and-science/>

### Exercise 6

…
