Data Notes
================

# Question 1:

## What the data includes

-   comparison of one program to the region and to the country

## GAP IN INFO AVAILABLE:

-   does not show one program to another single program
-   does not show trends in data necessarily except in individual
    reports (PDF)

## How do centers vary by geography:

-   offer acceptance ratios
-   who gets added/death while on waitlist
-   association btwn willingness to accept high-risk pts (e.g., based on
    kidney donor risk index, donor creatinine, hep C status) and time to
    transplant?

# Question 2:

-   Have centers changed their practices over time? Use years 11/2017 -
    present

# Question 3:

-   What center-related features are associated with higher/riskier
    offer acceptance ratios?

# Potential Visualizations

## Plots

1.  characteristics of waiting list candidates at center level
2.  characteristics of transplant recipients at center level
3.  scatterplot of high-risk offer acceptance ratios (? clarify a cut
    off for high risk) and transplant volume at multi-center level
4.  Forest plots of hazard ratios?

## Interactivity:

-   add centers into graph based on geographic proximity
-   add centers into graph based on ?? academic institution?

## Selectors

-   center(s)
-   zip code radius
-   ?organ
-   ?time span (years)

## Comparisons

Show comparisons between different regions (have a slider for mile
radius perhaps based on zipcode?) - use ZipRadius package
<https://cran.r-project.org/web/packages/ZipRadius/vignettes/ZipRadius.html>

## Dashboard Layout

? Dashboard like this with multiple centers:
<https://www.srtr.org/transplant-centers/ny-presbyterian-hospitalcolumbia-univ-medical-center-nycp/?organ=kidney&recipientType=adult>

# Data inclusion

## Center Level Details

Consider including only this info for each center:

-   number of additions/period
-   Number of adults vs. peds
-   Ages %
-   Genders %
-   Race/Ethnicity %
-   Blood types %
-   Primary disease %
-   Previous transplant %
-   Average time of wait list
-   Deceased vs. living donor %
-   Number of people who die wait list %
-   Survival on wait list (Graft vs. whole human)
-   HR for 1m, 1y, 3y (compared to national)

# Potential data needed?:

-   zip code of center (Tiers sheet in each file or from Matt
    zipcodes.xlsx)
-   organ risk scores (KDRI)
-   donor risk score
-   waiting list length
-   average duration of time on wait list
-   average age of transplant recipients who died
-   average age of transplant recipients who lived
-   most common comorbidity?
-   offer acceptance ratio over time

# Explanations of data avaialable via download

Tables B\* are waiting list info Tables C\* are transplant info Table D1
is follow-up rates for living DONORS

Suffixes: - L == living - D == deceased

## Proposed levels of analysis

-   program
-   miles radius/city
-   region
-   national

## REGIONS FROM OPTN

![OPTN regions](data/regions_OPTN.png)

Region 1: Connecticut, Maine, Massachusetts, New Hampshire, Rhode
Island, Eastern Vermont

Region 2: Delaware, District of Columbia, Maryland, New Jersey,
Pennsylvania, West Virginia, Northern Virginia

Region 3: Alabama, Arkansas, Florida, Georgia, Louisiana, Mississippi,
Puerto Rico

Region 4: Oklahoma, Texas

Region 5: Arizona, California, Nevada, New Mexico, Utah

Region 6: Alaska, Hawaii, Idaho, Montana, Oregon, Washington

Region 7: Illinois, Minnesota, North Dakota, South Dakota, Wisconsin

Region 8: Colorado, Iowa, Kansas, Missouri, Nebraska, Wyoming

Region 9: New York, Western Vermont

Region 10: Indiana, Michigan, Ohio

Region 11: Kentucky, North Carolina, South Carolina, Tennessee, Virginia

## Plan to grab data

``` r
# for file in data file aka year
# read in csv spec sheets
# pull in the zip code data
# pull in the OPTN region data
# mutate and make tidy, one var per column
```

Table combining the following: - Center info - Center zip code (from
Tiers) - Center region (from OPTN data) - Center rank (from Tiers)

### Sheets to combine?

-   combine B1-B3
-   combine B4-B7
-   combine B8-B10

### Consider including some of the following:

-   Table B1: waiting list activity summary

-   Table B2: demographic characteristics (new for year and all)
    (ethnicity, age, gender)

-   Table B3: medical characteristics (new for year and all) (blood
    type, prev transplant, initical CPRA, primary disease)

-   Table B4: transplant rates: count at start of year, person years,
    removal for transplant, divided into all, adult, and peds, observed
    vs. expected

-   Table B5: pre transplant mortality rates

-   Table B6: rates of patient mortality AFTER listing (exclude B6 - SFL
    for 2021)

-   Table B7: wait list status post listing

-   Table B8: percent of candidates with decreased donor transplants,
    demographics (percent transplanted at a specific time since
    listing - 30d, 1y, 2y, 3y)

-   Table B9: medical charactersitics of above

-   Table B10: time to transplant for waiting list percentiles (months):
    5th, 10th, 25th, 50th, 75th

-   Table B11: OFFER ACCEPTANCE PRACTICES – overall (KDRI = kidney donor
    risk index) – low KDRI donors (KDRI &lt;1.05) – medium 1.05 - 1.75 –
    high &gt;1.75 – hard to place kidneys (over 100 offers)

-   Table C1: transplant recipient demographics (ethnicity, age, gender)

-   Table C2: transplant recipient medical characteristics (blood type,
    prev transplant, peak PRA/CPRA prior to transplant, BMI, primary
    disease)

-   Table C3: donor characteristics (ethnicity, age, gender, blood
    type), cause of death for deceased

-   Table C5: adult 1m GRAFT survival

-   Table C6: adult 1y GRAFT survival

-   Table C7: adult 3y GRAFT survival

-   Table C8: pediatric 1m GRAFT survival

-   Table C9: pediatric 1y GRAFT survival

-   Table C10: pediatric 3y GRAFT survival

-   Tables C11: adult 1m patient survival after FIRST transplant

-   Tables C12: adult 1y patient survival after FIRST transplant

-   Tables C13: adult 3y patient survival after FIRST transplant

-   Tables C14: pediatric 1 month patient survival after FIRST
    transplant

-   Tables C15: pediatric 1 yr patient survival after FIRST transplant

-   Tables C16: pediatric 3y patient survival after FIRST transplant (D)
    deceased donor, (L) living donor

**KDRI definition**
(<https://optn.transplant.hrsa.gov/media/1512/guide_to_calculating_interpreting_kdpi.pdf>):
The Kidney Donor Profle Index (KDPI) is a numerical measure that
combines ten donor factors, including clinical parameters and
demographics, to summarize into a single number the quality of deceased
donor kidneys relative to other recovered kidneys. The KDPI is derived
by frst calculating the Kidney Donor Risk Index (KDRI) for a deceased
donor. Kidneys from a donor with a KDPI of 90%, for example, have a KDRI
(which indicates relative risk of graft failure) greater than 90% of
recovered kidneys. The KDPI is simply a mapping of the KDRI from a
relative risk scale to a cumulative percentage scale. The reference
population used for this mapping is all deceased donors in the United
States with a kidney recovered for the purpose of transplantation in the
prior calendar year. Lower KDPI values are associated with increased
donor quality and expected longevity.

### Consider EXCLUDING:

-   Table B6 - SFL (unique to 2021 data?)
-   Table C4: transplant characteristics (ischemic time, mismatch,
    relation)
-   Tables C17-18: Multi-organ transplant graft survival / Multi-organ
    transplant patient survival
-   Table D1: Living donor summary
