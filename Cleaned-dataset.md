Creating Cleaned WEO Data Set
================

# Introduction

Okay! Lets Get Going. I am using the World MacroEconomic Outlook data
published by IMF twice a year. For the purpose of this presentation, I
am usig the lastest dataset available in the series i.e. October 2023.

## Data Summary

Lets look at how the data look like!! We can see that it is very messy
and disorganized. It is Raw. It is in complex and unstructured format.
Without proper organization, labeling, and formatting, raw data can be
overwhelming and difficult to interpret. Additionally, it contains
missing or erroneous information. Instead of variable names we have
years in the columns and all the economic determinants are under WEO
subject code and discription columns. Lets Clean it, step by step.

``` r
summary(weo)
```

    ##  WEO Country Code       ISO            WEO Subject Code     Country         
    ##  Length:8626        Length:8626        Length:8626        Length:8626       
    ##  Class :character   Class :character   Class :character   Class :character  
    ##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##  Subject Descriptor Subject Notes         Units              Scale          
    ##  Length:8626        Length:8626        Length:8626        Length:8626       
    ##  Class :character   Class :character   Class :character   Class :character  
    ##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##  Country/Series-specific Notes     1980               1981          
    ##  Length:8626                   Length:8626        Length:8626       
    ##  Class :character              Class :character   Class :character  
    ##  Mode  :character              Mode  :character   Mode  :character  
    ##                                                                     
    ##                                                                     
    ##                                                                     
    ##                                                                     
    ##      1982               1983               1984               1985          
    ##  Length:8626        Length:8626        Length:8626        Length:8626       
    ##  Class :character   Class :character   Class :character   Class :character  
    ##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##      1986               1987               1988               1989          
    ##  Length:8626        Length:8626        Length:8626        Length:8626       
    ##  Class :character   Class :character   Class :character   Class :character  
    ##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##      1990               1991               1992               1993          
    ##  Length:8626        Length:8626        Length:8626        Length:8626       
    ##  Class :character   Class :character   Class :character   Class :character  
    ##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##      1994               1995               1996               1997          
    ##  Length:8626        Length:8626        Length:8626        Length:8626       
    ##  Class :character   Class :character   Class :character   Class :character  
    ##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##      1998               1999               2000               2001          
    ##  Length:8626        Length:8626        Length:8626        Length:8626       
    ##  Class :character   Class :character   Class :character   Class :character  
    ##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##      2002               2003               2004               2005          
    ##  Length:8626        Length:8626        Length:8626        Length:8626       
    ##  Class :character   Class :character   Class :character   Class :character  
    ##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##      2006               2007               2008               2009          
    ##  Length:8626        Length:8626        Length:8626        Length:8626       
    ##  Class :character   Class :character   Class :character   Class :character  
    ##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##      2010               2011               2012               2013          
    ##  Length:8626        Length:8626        Length:8626        Length:8626       
    ##  Class :character   Class :character   Class :character   Class :character  
    ##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##      2014               2015               2016               2017          
    ##  Length:8626        Length:8626        Length:8626        Length:8626       
    ##  Class :character   Class :character   Class :character   Class :character  
    ##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##      2018               2019               2020               2021          
    ##  Length:8626        Length:8626        Length:8626        Length:8626       
    ##  Class :character   Class :character   Class :character   Class :character  
    ##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##      2022               2023               2024               2025          
    ##  Length:8626        Length:8626        Length:8626        Length:8626       
    ##  Class :character   Class :character   Class :character   Class :character  
    ##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##      2026               2027           Estimates Start After
    ##  Length:8626        Length:8626        Min.   :2003         
    ##  Class :character   Class :character   1st Qu.:2020         
    ##  Mode  :character   Mode  :character   Median :2021         
    ##                                        Mean   :2020         
    ##                                        3rd Qu.:2021         
    ##                                        Max.   :2022         
    ##                                        NA's   :985

## Filtering Out

I am going to use selected 10 economic indicators out of many under the
WEO Subject Code column. Lets Rename the column names and filter out a
shorter dataset with the indicators we are interested in…

``` r
weo  %<>% 
  rename("Subject_Code" = "WEO Subject Code")
weo  %<>% 
  rename("Country_Code" = "WEO Country Code")

weo1 = weo %>% 
  filter(Subject_Code == 'NGDP_RPCH' | Subject_Code == 'PPPSH'|
         Subject_Code == 'PCPIPCH' | Subject_Code == 'LUR' |
           Subject_Code == 'LE' |  Subject_Code == 'LP'| 
           Subject_Code == 'GGR_NGDP' | Subject_Code == 'GGX_NGDP' |
           Subject_Code == 'GGXWDN_NGDP' | Subject_Code ==  'BCA_NGDPD')
```

## Pivoting Longer

The need to pivot longer arises when data is stored in a format that
makes it difficult to analyze, we can see that we have year numbers as
columns so by bringing all year columns under one column called “year”,
we can create a more organized and structured dataset that is easier to
work with. We put all the values under different years in a new coulumn
called “Values”. Doing both of these things allows us to conduct trend
analysis, perform calculations, and draw insights across multiple years
without having to refer to each individual column separately. Then, I am
selecting the specific columns from the dataset to carry out further
cleaning.

``` r
weo2 =
  weo1 %>%
  pivot_longer(
    cols = c(31:50),
    names_to = 'year',
    names_transform = list(year = as.integer),
    values_to = 'Values'
  )

weo3 =
  weo2 %>% 
  select(Country, ISO, Country_Code, Subject_Code, year, Values)
```

## Pivoting Wider

With following codes, I am widening the dataset and creating a new ID
Variable. I am converting chosen indicators under Subject Code column
into seperate variables and assigning them values from the “Values”
variable.

``` r
weo4 =
  weo3 %>%
  pivot_wider(
    names_from = Subject_Code ,
    values_from = Values
  )  

weo4 %<>%  #creating a ID variable
  mutate(
    RID = row_number(), .before = 1
  )
```

## Final touch

With this code chunk, I am further cleaning the dataset. Renaming the
variables, making implicit NAs explicit and converting the character
variables (those are supposed to be numeric) into numeric. I am also
creating an ordered factor variable with a cool function. Until this
step, we were working on a matrix which will also be converted into a
proper dataset and select the columns which we are interested in having
in our dataset:

``` r
weo4  %<>% 
  rename("YEAR" = "year")
weo4  %<>% 
  rename("COUNTRY" = "Country")       

val_repl <- c('n/a') #replacing the implit n/a into explicit NA
weo5 = sapply(weo4,                           
                    function(x) replace(x, x %in% val_repl, NA))
weo5 = as.data.frame(weo5)



vec = c(6:15) #converting certain charater varibles into numeric 
weo5[ , vec] = apply(weo5[ , vec,drop=F], 2,          
                            function(x) as.numeric(as.character(x)))
```

    ## Warning in FUN(newX[, i], ...): NAs introduced by coercion

    ## Warning in FUN(newX[, i], ...): NAs introduced by coercion

    ## Warning in FUN(newX[, i], ...): NAs introduced by coercion

    ## Warning in FUN(newX[, i], ...): NAs introduced by coercion

    ## Warning in FUN(newX[, i], ...): NAs introduced by coercion

``` r
FctWhen = function(...) {
  args = rlang::list2(...)
  rhs = map(args, rlang::f_rhs)
  cases = case_when( !!!args )
  exec(fct_relevel, cases, !!!rhs)
}  

weo5%<>% ##creating a factor variable for unemployment rate
  mutate(
    UR = FctWhen(
      LUR < 5 ~ 'Low',
      LUR %in% 5:9 ~ 'Moderate',
      LUR  > 9 ~ 'High',
      TRUE ~ '99'
    )
  )

weo5%<>% #creating a factor variable for debt sustainability
  mutate(
    SUS = FctWhen(
      GGXWDN_NGDP < 77 ~ 'Sustainable',
      GGXWDN_NGDP  > 77 ~ 'Unsustainable',
      TRUE ~ '99'
    )
  )

weo6 = weo5 %>% #selecting variables in desired order
  select(RID, COUNTRY, ISO, Country_Code, YEAR, NGDP_RPCH,PPPSH,PCPIPCH, LUR, UR, LP, GGR_NGDP, GGX_NGDP, GGXWDN_NGDP, SUS, BCA_NGDPD)
```

## Lets see how our dataset looks!!

``` r
summary(weo6)
```

    ##      RID              COUNTRY              ISO            Country_Code      
    ##  Length:3920        Length:3920        Length:3920        Length:3920       
    ##  Class :character   Class :character   Class :character   Class :character  
    ##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##      YEAR             NGDP_RPCH           PPPSH            PCPIPCH       
    ##  Length:3920        Min.   :-54.011   Min.   : 0.0010   Min.   :-72.729  
    ##  Class :character   1st Qu.:  1.223   1st Qu.: 0.0190   1st Qu.:  1.462  
    ##  Mode  :character   Median :  3.490   Median : 0.0650   Median :  3.369  
    ##                     Mean   :  3.301   Mean   : 0.5323   Mean   :  5.999  
    ##                     3rd Qu.:  5.816   3rd Qu.: 0.3450   3rd Qu.:  6.800  
    ##                     Max.   : 86.827   Max.   :20.0120   Max.   :557.210  
    ##                     NA's   :40        NA's   :163       NA's   :56       
    ##       LUR                UR             LP             GGR_NGDP      
    ##  Min.   : 0.655   Low     : 537   Min.   :  0.009   Min.   :  1.983  
    ##  1st Qu.: 5.077   Moderate:  22   1st Qu.:  1.708   1st Qu.: 18.747  
    ##  Median : 7.400   High    : 792   Median :  6.973   Median : 26.220  
    ##  Mean   : 9.007   99      :2569   Mean   : 22.443   Mean   : 29.220  
    ##  3rd Qu.:11.000                   3rd Qu.: 22.890   3rd Qu.: 37.134  
    ##  Max.   :38.400                   Max.   :331.234   Max.   :170.218  
    ##  NA's   :1701                     NA's   :90        NA's   :77       
    ##     GGX_NGDP        GGXWDN_NGDP                 SUS         BCA_NGDPD      
    ##  Min.   :  2.337   Min.   :-131.83   Sustainable  :1515   Min.   :-84.779  
    ##  1st Qu.: 20.619   1st Qu.:  15.82   Unsustainable: 229   1st Qu.: -7.277  
    ##  Median : 28.950   Median :  34.78   99           :2176   Median : -2.663  
    ##  Mean   : 31.166   Mean   :  39.59                        Mean   : -1.717  
    ##  3rd Qu.: 38.664   3rd Qu.:  56.37                        3rd Qu.:  2.408  
    ##  Max.   :137.359   Max.   : 550.97                        Max.   :314.906  
    ##  NA's   :85        NA's   :2176                           NA's   :172

## Codebook

Now the coolest thing ever! We can create a codebook with all the
essential information about variables using just one code command. But
you need to make sure that you have described each variable. Here I am
adding source and description to all the variables followed by the code
to print the code book as a word file. Remember, you must edit the
codebook to remove undesired content and add important stuff. You can
compare the output of this codes with the code book I have uploaded in
this repository.

``` r
weo7 = weo6 %>%
  cb_add_col_attributes(
    RID,
    description = "Serial Number",
    source = "Created by R code"
  ) %>%
  
  cb_add_col_attributes(
    COUNTRY,
    description = "IMF Member Country",
    source = "World Economic Outlook Database 2022"
  ) %>%
  
  cb_add_col_attributes(
    ISO,
    description = "Country Code for IMF Member Country",
    source = "World Economic Outlook Database 2022"
  ) %>%
  
  cb_add_col_attributes(
    YEAR,
    description = "Year",
    source = "World Economic Outlook Database 2022"
  ) %>%
  
  cb_add_col_attributes(
    NGDP_RPCH,
    description = "% in Gross domestic product, constant prices",
    source = "World Economic Outlook Database 2022"
   
  ) %>% 
  
  cb_add_col_attributes(
    PPPSH,
    description = "Gross domestic product based on purchasing-power-parity share of world total",
    source = "World Economic Outlook Database 2022"
  ) %>% 
  
  cb_add_col_attributes(
    PCPIPCH,
    description = "% in Inflation, average consumer prices",
    source = "World Economic Outlook Database 2022"
  ) %>% 
  
  cb_add_col_attributes(
    LUR,
    description = "% of population Unemployed",
    source = "World Economic Outlook Database 2022"
  ) %>% 
  
  cb_add_col_attributes(
    UR,
    description = "Nature of Unemployment",
    source = "created from LUR variable"
  ) %>%
  cb_add_col_attributes(
    LP,
    description = "Population in Millions",
    source = "World Economic Outlook Database 2022"
  ) %>% 
  cb_add_col_attributes(
    GGR_NGDP,
    description = "General government revenue as % of GDP",
    source = "World Economic Outlook Database 2022"
  ) %>%
  cb_add_col_attributes(
    GGX_NGDP,
    description = "General government Expenditure as % of GDP",
    source = "World Economic Outlook Database 2022"
  ) %>%
  cb_add_col_attributes(
    GGXWDN_NGDP,
    description = "General government net debt as % of GDP",
    source = "World Economic Outlook Database 2022"
  ) %>% 
  cb_add_col_attributes(
    SUS,
    description = "Nature of Debt",
    source = "World Economic Outlook Database 2022"
  ) %>%
  cb_add_col_attributes(
    BCA_NGDPD,
    description = "Current Account Balance as % of GDP",
    source = "World Economic Outlook Database 2022"
  )
```

    ## The following attribute(s) are being added to a variable in the data frame for the first time: description, source. If you believe this/these attribute(s) were previously added, then check for a typo in the attribute name. If you are adding this/these attribute(s) for the first time, you can probably safely ignore this message.

``` r
codebook = codebook(weo7)  
print(codebook, target = "codebook_1.docx")  
 

library("writexl") 
write.csv(weo7, "C:/Users/bharg/OneDrive/Desktop/SIS/Data Analysis/awd/World Macroeconomic Outlook.csv", row.names=FALSE)
save(weo7, file = "World macroeconomic Outlook.RData")
```

## CONCLUSION

With this code chunk, I cleaned a very disorderly available World
Macro-Economic Outlook data set and gave a step by step overview of
codes used and reason there off.
