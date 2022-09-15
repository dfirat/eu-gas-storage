EU Gas Storage
================
Deniz Firat

## PREPARE

### Load needed packages

``` r
library("tidyverse")
library("janitor")
library("lubridate")
library("hms")
library("jsonlite")
```

### Import data sets [(Source)](https://agsi.gie.eu/)

``` r
eu <- fromJSON("StorageData_GIE_2012-09-12_2022-09-12.json", flatten = TRUE)
```

### Add new year and month column

``` r
eu$year <- format(as.Date(eu$gasDayStart), "%Y")
eu$month <- format(as.Date(eu$gasDayStart), "%m-%d")
```

### Exclude 2022 for calculations

``` r
eu_edit <- eu[eu$year != 2022, ]
```

### Calcuate daily average

``` r
eu_average <- eu_edit %>% 
    group_by(month) %>% 
    summarise(Mean = mean(full))
```

### Calcuate daily maximum

``` r
eu_max <- eu_edit %>% 
    group_by(month) %>% 
    summarise(Max = max(full))
```

### Calcuate daily minimum

``` r
eu_min <- eu_edit %>% 
    group_by(month) %>% 
    summarise(Min = min(full))
```

### Split data set into each year

``` r
eu2022 <- eu[eu$year == 2022, ]
eu2021 <- eu[eu$year == 2021, ]
eu2020 <- eu[eu$year == 2020, ]
eu2019 <- eu[eu$year == 2019, ]
eu2018 <- eu[eu$year == 2018, ]
eu2017 <- eu[eu$year == 2017, ]
eu2016 <- eu[eu$year == 2016, ]
eu2015 <- eu[eu$year == 2015, ]
eu2014 <- eu[eu$year == 2014, ]
eu2013 <- eu[eu$year == 2013, ]
```

### Save new data set

``` r
write.csv(eu, "eu-gas-storage.csv")
write.csv(eu_average, "eu-gas-storage-average.csv")
write.csv(eu_max, "eu-gas-storage-max.csv")
write.csv(eu_min, "eu-gas-storage-min.csv")
write.csv(eu2022, "eu-gas-storage2022.csv")
write.csv(eu2021, "eu-gas-storage2021.csv")
write.csv(eu2020, "eu-gas-storage2020.csv")
write.csv(eu2019, "eu-gas-storage2019.csv")
write.csv(eu2018, "eu-gas-storage2018.csv")
write.csv(eu2017, "eu-gas-storage2017.csv")
write.csv(eu2016, "eu-gas-storage2016.csv")
write.csv(eu2015, "eu-gas-storage2015.csv")
write.csv(eu2014, "eu-gas-storage2014.csv")
write.csv(eu2013, "eu-gas-storage2013.csv")
```
