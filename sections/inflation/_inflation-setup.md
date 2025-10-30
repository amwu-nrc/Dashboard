```{r}
#| label: setup-inflation
library(reportabs)
library(tidyverse)
library(directlabels)
library(geomtextpath)
library(readabs)
library(gghighlight)
library(strayr)
library(gt)
cpi <- read_abs_local("6484.0", path = "data") |> 
  separate_series(column_names = c("data_type", "cpi_category", "capital_city"))

cpi_quarterly <- read_absdata("cpi_quarterly", export_dir = "data")
wpi_quarterly <- read_absdata("wpi_quarterly", export_dir = "data")
national_accounts <- read_abs_local(cat_no = "5206.0", path = "data")
lci <- read_abs_local("6467.0",  path = "data") |> 
  separate_series(c("data_type", "household_type", "cpi_category"))


```
