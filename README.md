# myrepotest1
## testing my setup
This is a line I wrote in **RStudio**.

Git will be where I *experiment* for the next few days.

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE, warning = FALSE, message = FALSE)
library(dplyr)
library(ggplot2)
library(knitr)
library(readr)
library(tidyverse)
library(ggmap)
library(maps)
library(stringr)
library(tmap)
library(sf)
```

# Introduction

The 1920s were a decade characterized by prosperity - earning the moniker "The Roaring Twenties" -, increasing income inequality, and Republican dominance of 
American politics. Today, we will look at the 1924 and 1928 Presidential elections in Ohio.

## First Step: Downloading and Processing the Data

Data for this time period can be hard to find, so I have attached the county-level election data to my repository. It originally came from [ICPSR](https://www.icpsr.umich.edu/web/pages/),
and I have done some preliminary processing to make the next steps easier. You can download my pre-processed data [here](https://raw.githubusercontent.com/shanedigiovanna/myrepotest1/main/Ohio%20Coolidge%20Hoover%20elections.csv).
The county shapefile can be downloaded from [here](https://community.esri.com/t5/arcgis-enterprise-portal/where-can-i-find-a-shapefile-with-all-us-counties-and-fips-code/td-p/307592).

We will read in the data:

```{r data}
twenties_data <- read_csv("~/Desktop/R Stuff/Ohio Coolidge Hoover elections.csv")

county_shp <- st_read("/Users/shanedigiovanna/Downloads/UScounties/UScounties.shp")
```

We need to filter `county_shp` to include only Ohio counties, and adjust the case of the county names in `twenties_data` to match those in `oh_county_shp`:

```{r}
oh_county_shp <- county_shp %>%
	filter(STATE_NAME == "Ohio")

twenties_data$COUNTY_NAME <- tolower(twenties_data$COUNTY_NAME)

twenties_data$COUNTY_NAME <- str_to_title(twenties_data$COUNTY_NAME)
```


