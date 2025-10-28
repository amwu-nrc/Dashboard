```{r, setup, echo = FALSE}
library(reportabs)
library(tidyverse)
library(directlabels)
library(readabs)
library(gghighlight)
library(strayr)
library(gt)
library(scales)

national_accounts <- read_abs_local(cat_no = "5206.0", path = "data")

productivity_decouple <- read_absdata("productivity", export_dir = "data") |> 
  pivot_longer(cols = c(gdp_per_hour_index, real_compensation_per_hour_index)) |> 
  mutate(name = case_when(
    name == "gdp_per_hour_index" ~ "Productivity (GDP per Hour Worked)",
    name == "real_compensation_per_hour_index" ~ "Real Compensation per Hour Worked"
  )) 

productivity_sector <- read_abs_local("5204.0", 
                                path = "data") |> 
  filter(table_no == "5204015_Labour_Productivity_Input",
         str_detect(series, "GVA"),
         !is.na(value)) |>
  mutate(industry = str_extract(series, "^(.*?);"),
         industry = trimws(str_remove_all(industry, ";"))) |>
  group_by(industry) |> 
  mutate(index = 100*value/value[date == "1998-06-01"]) |> 
  ungroup() 

```
