SummaryPlots
================
11/26/2021

``` r
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.1 ──

    ## ✓ ggplot2 3.3.5     ✓ purrr   0.3.4
    ## ✓ tibble  3.1.6     ✓ dplyr   1.0.7
    ## ✓ tidyr   1.1.4     ✓ stringr 1.4.0
    ## ✓ readr   2.1.0     ✓ forcats 0.5.1

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

Here we import datasets for age, gender, race, and blood type using a
for loop, string manipulation with regular expressions, and map-reduce
approach.

``` r
phrase = "SRTR Multiorgan Transplant Data, August 2020 Release"

suffix = list("age","gender","demographics","blood_type")

for (i in suffix){
  data_path = "./data/"   # path to the data
  files = dir(data_path, 
              pattern = paste0("csrs_final_tables_2006_[A-Z][A-Z]_", i,".csv"))
  assign(paste0("df_all_", i),
         files %>%
           map(~ read_csv(file.path(data_path, .))%>%
                 mutate(org = str_replace(org, "HR", "Heart"),
                        org = str_replace(org, "HL", "Heart-Lung"),
                        org = str_replace(org, "IN", "Intestine"),
                        org = str_replace(org, "KI", "Kidney"),
                        org = str_replace(org, "KP", "Kidney-Pancreas"),
                        org = str_replace(org, "LI", "Liver"),
                        org = str_replace(org, "LU", "Lung"),
                        org = str_replace(org, "PA", "Pancreas"))) %>%
           reduce(rbind))
  }
```

    ## New names:
    ## * `` -> ...1

    ## Rows: 56 Columns: 8

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (5): entire_name, ctr_cd, ctr_ty, org, age_category
    ## dbl (3): ...1, zipcode, age_category_percent

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## New names:
    ## * `` -> ...1

    ## Rows: 1000 Columns: 8

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (5): entire_name, ctr_cd, ctr_ty, org, age_category
    ## dbl (3): ...1, zipcode, age_category_percent

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## New names:
    ## * `` -> ...1

    ## Rows: 136 Columns: 8

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (5): entire_name, ctr_cd, ctr_ty, org, age_category
    ## dbl (3): ...1, zipcode, age_category_percent

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## New names:
    ## * `` -> ...1

    ## Rows: 1888 Columns: 8

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (5): entire_name, ctr_cd, ctr_ty, org, age_category
    ## dbl (3): ...1, zipcode, age_category_percent

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## New names:
    ## * `` -> ...1

    ## Rows: 952 Columns: 8

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (5): entire_name, ctr_cd, ctr_ty, org, age_category
    ## dbl (3): ...1, zipcode, age_category_percent

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## New names:
    ## * `` -> ...1

    ## Rows: 1104 Columns: 8

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (5): entire_name, ctr_cd, ctr_ty, org, age_category
    ## dbl (3): ...1, zipcode, age_category_percent

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## New names:
    ## * `` -> ...1

    ## Rows: 560 Columns: 8

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (5): entire_name, ctr_cd, ctr_ty, org, age_category
    ## dbl (3): ...1, zipcode, age_category_percent

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## New names:
    ## * `` -> ...1

    ## Rows: 560 Columns: 8

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (5): entire_name, ctr_cd, ctr_ty, org, age_category
    ## dbl (3): ...1, zipcode, age_category_percent

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## New names:
    ## * `` -> ...1

    ## Rows: 20 Columns: 8

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (5): entire_name, ctr_cd, ctr_ty, org, gender_category
    ## dbl (3): ...1, zipcode, gender_category_percent

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## New names:
    ## * `` -> ...1

    ## Rows: 274 Columns: 8

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (5): entire_name, ctr_cd, ctr_ty, org, gender_category
    ## dbl (3): ...1, zipcode, gender_category_percent

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## New names:
    ## * `` -> ...1

    ## Rows: 34 Columns: 8

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (5): entire_name, ctr_cd, ctr_ty, org, gender_category
    ## dbl (3): ...1, zipcode, gender_category_percent

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## New names:
    ## * `` -> ...1

    ## Rows: 472 Columns: 8

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (5): entire_name, ctr_cd, ctr_ty, org, gender_category
    ## dbl (3): ...1, zipcode, gender_category_percent

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## New names:
    ## * `` -> ...1

    ## Rows: 242 Columns: 8

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (5): entire_name, ctr_cd, ctr_ty, org, gender_category
    ## dbl (3): ...1, zipcode, gender_category_percent

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## New names:
    ## * `` -> ...1

    ## Rows: 280 Columns: 8

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (5): entire_name, ctr_cd, ctr_ty, org, gender_category
    ## dbl (3): ...1, zipcode, gender_category_percent

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## New names:
    ## * `` -> ...1

    ## Rows: 142 Columns: 8

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (5): entire_name, ctr_cd, ctr_ty, org, gender_category
    ## dbl (3): ...1, zipcode, gender_category_percent

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## New names:
    ## * `` -> ...1

    ## Rows: 142 Columns: 8

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (5): entire_name, ctr_cd, ctr_ty, org, gender_category
    ## dbl (3): ...1, zipcode, gender_category_percent

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## New names:
    ## * `` -> ...1

    ## Rows: 60 Columns: 8

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (5): entire_name, ctr_cd, ctr_ty, org, race_category
    ## dbl (3): ...1, zipcode, race_category_percent

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## New names:
    ## * `` -> ...1

    ## Rows: 822 Columns: 8

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (5): entire_name, ctr_cd, ctr_ty, org, race_category
    ## dbl (3): ...1, zipcode, race_category_percent

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## New names:
    ## * `` -> ...1

    ## Rows: 102 Columns: 8

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (5): entire_name, ctr_cd, ctr_ty, org, race_category
    ## dbl (3): ...1, zipcode, race_category_percent

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## New names:
    ## * `` -> ...1

    ## Rows: 1416 Columns: 8

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (5): entire_name, ctr_cd, ctr_ty, org, race_category
    ## dbl (3): ...1, zipcode, race_category_percent

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## New names:
    ## * `` -> ...1

    ## Rows: 726 Columns: 8

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (5): entire_name, ctr_cd, ctr_ty, org, race_category
    ## dbl (3): ...1, zipcode, race_category_percent

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## New names:
    ## * `` -> ...1

    ## Rows: 840 Columns: 8

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (5): entire_name, ctr_cd, ctr_ty, org, race_category
    ## dbl (3): ...1, zipcode, race_category_percent

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## New names:
    ## * `` -> ...1

    ## Rows: 426 Columns: 8

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (5): entire_name, ctr_cd, ctr_ty, org, race_category
    ## dbl (3): ...1, zipcode, race_category_percent

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## New names:
    ## * `` -> ...1

    ## Rows: 426 Columns: 8

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (5): entire_name, ctr_cd, ctr_ty, org, race_category
    ## dbl (3): ...1, zipcode, race_category_percent

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## New names:
    ## * `` -> ...1

    ## Rows: 50 Columns: 8

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (5): entire_name, ctr_cd, ctr_ty, org, blood_type_category
    ## dbl (3): ...1, zipcode, blood_type_category_percent

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## New names:
    ## * `` -> ...1

    ## Rows: 685 Columns: 8

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (5): entire_name, ctr_cd, ctr_ty, org, blood_type_category
    ## dbl (3): ...1, zipcode, blood_type_category_percent

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## New names:
    ## * `` -> ...1

    ## Rows: 85 Columns: 8

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (5): entire_name, ctr_cd, ctr_ty, org, blood_type_category
    ## dbl (3): ...1, zipcode, blood_type_category_percent

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## New names:
    ## * `` -> ...1

    ## Rows: 1180 Columns: 8

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (5): entire_name, ctr_cd, ctr_ty, org, blood_type_category
    ## dbl (3): ...1, zipcode, blood_type_category_percent

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## New names:
    ## * `` -> ...1

    ## Rows: 605 Columns: 8

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (5): entire_name, ctr_cd, ctr_ty, org, blood_type_category
    ## dbl (3): ...1, zipcode, blood_type_category_percent

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## New names:
    ## * `` -> ...1

    ## Rows: 700 Columns: 8

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (5): entire_name, ctr_cd, ctr_ty, org, blood_type_category
    ## dbl (3): ...1, zipcode, blood_type_category_percent

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## New names:
    ## * `` -> ...1

    ## Rows: 355 Columns: 8

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (5): entire_name, ctr_cd, ctr_ty, org, blood_type_category
    ## dbl (3): ...1, zipcode, blood_type_category_percent

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## New names:
    ## * `` -> ...1

    ## Rows: 355 Columns: 8

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (5): entire_name, ctr_cd, ctr_ty, org, blood_type_category
    ## dbl (3): ...1, zipcode, blood_type_category_percent

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

Here we plot the age dataframes.

``` r
plot = 
  df_all_age %>% 
  ggplot(aes(x = zipcode, y = age_category_percent, color = age_category)) + 
  geom_point() + 
  labs(
    title = "Patient Age Groups by Zipcode", 
    subtitle = phrase,
    x = "Zipcode",
    y = "Age Group (Percent)",
    color = "Age Group"
    ) + 
  theme_minimal() + 
  theme(axis.text.x=element_text(angle=90,hjust=1)) + 
  scale_color_hue(labels = c("Less Than 2 Years", "2 to 11 Years", 
                             "12 to 17 Years", "18 to 34 Years", 
                             "35 to 49 Years", "50 to 64 Years", 
                             "65 to 69 Years", "More Than 70 Years")) + 
  facet_wrap(~org)

plot
```

![](SummaryPlots_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

Here we plot the gender dataframes.

``` r
plot = 
  df_all_gender %>% 
  ggplot(aes(x=zipcode, y =gender_category_percent, color = gender_category)) + 
  geom_point()+ 
  labs(title = "Patient Gender by Zipcode", 
       subtitle = phrase,
       x = "Zipcode",
       y = "Gender (Percent)", color = "Gender"
  ) + 
  theme_minimal() + 
  theme(axis.text.x=element_text(angle=90,hjust=1)) + 
  scale_color_hue(labels = c("Female", "Male")) + 
  facet_wrap(~org)

plot
```

    ## Warning: Removed 42 rows containing missing values (geom_point).

![](SummaryPlots_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

Here we plot the race dataframes.

``` r
plot = 
  df_all_demographics %>% 
  ggplot(aes(x=zipcode, y =race_category_percent, color = race_category)) + 
  geom_point() + 
  theme_minimal() + 
  labs(
    title = "Patient Demographics by Zipcode", subtitle = phrase,
    x = "Zipcode",
    y = "Race (Percent)", 
    color = "Race") + 
  scale_color_hue(labels = c("African American", "Asian", "Hispanic or Latino", 
                             "Other", "Unknown", "White")) + 
  theme(axis.text.x=element_text(angle=90,hjust=1)) + 
  facet_wrap(~org)

plot
```

    ## Warning: Removed 126 rows containing missing values (geom_point).

![](SummaryPlots_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

Here we plot the blood type dataframes.

``` r
plot = 
  df_all_blood_type %>%
  ggplot(aes(x = zipcode, y = blood_type_category_percent, color = blood_type_category)) + 
  geom_point() + 
  labs(
    title = "Patient Blood Types by Zipcode", subtitle = "SRTR Kidney Transplant Data, August 2020 Release",
    x = "Zipcode",
    y = "Blood Type (Percent)", color = "Blood Type"
  ) + 
  theme_minimal() + 
  scale_color_hue(labels = c("A", "AB", "B", "O", "Unknown")) + 
  theme(axis.text.x=element_text(angle=90,hjust=1)) + 
  facet_wrap(~org)

plot
```

    ## Warning: Removed 105 rows containing missing values (geom_point).

![](SummaryPlots_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

``` r
# png('blood_type_summary.png')
```
