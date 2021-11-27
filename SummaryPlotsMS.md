SummaryPlotsMS
================
Matthew Spotnitz
11/26/2021

``` r
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.1 ──

    ## ✓ ggplot2 3.3.5     ✓ purrr   0.3.4
    ## ✓ tibble  3.1.5     ✓ dplyr   1.0.7
    ## ✓ tidyr   1.1.3     ✓ stringr 1.4.0
    ## ✓ readr   2.0.1     ✓ forcats 0.5.1

    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(readxl)
library(haven)
library(ggplot2)
library(zipcodeR)
library(ggmap)
```

    ## Google's Terms of Service: https://cloud.google.com/maps-platform/terms/.

    ## Please cite ggmap if you use it! See citation("ggmap") for details.

``` r
library(leaflet)
library(kableExtra)
```

    ## 
    ## Attaching package: 'kableExtra'

    ## The following object is masked from 'package:dplyr':
    ## 
    ##     group_rows

I will define the age dataframes

``` r
phrase = "SRTR Multiorgan Transplant Data, August 2020 Release"

df_one_age = read.csv("./data/csrs_final_tables_2006_HL_age.csv") 
df_two_age = read.csv("./data/csrs_final_tables_2006_HR_age.csv") 
df_three_age = read.csv("./data/csrs_final_tables_2006_IN_age.csv")
df_four_age = read.csv("./data/csrs_final_tables_2006_KI_age.csv")
df_five_age = read.csv("./data/csrs_final_tables_2006_KP_age.csv")
df_six_age = read.csv("./data/csrs_final_tables_2006_LI_age.csv")
df_seven_age = read.csv("./data/csrs_final_tables_2006_LU_age.csv")
df_eight_age = read.csv("./data/csrs_final_tables_2006_PA_age.csv")
df_all_age = rbind(df_one_age, df_two_age, df_three_age, df_four_age, df_five_age, df_six_age, df_seven_age, df_eight_age)
view(df_all_age)
```

I will plot the age dataframes

``` r
plot = df_all_age %>% ggplot(aes(x=zipcode, y =age_category_percent, color = age_category)) + geom_point() + 
  labs(
    title = "Patient Age Groups by Zipcode", subtitle = ,
    x = "Zipcode",
    y = "Age Group (Percent)",color = "Age Group"
  ) + theme_minimal()  + scale_color_hue(labels = c("Less Than 2 Years", "2 to 11 Years", "12 to 17 Years", "18 to 34 Years", "35 to 49 Years", "50 to 64 Years", "64 to 69 Years", "More Than 70 Years")) + facet_wrap(~df_all_age[, c(5)])
print(plot)
```

![](SummaryPlotsMS_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->
