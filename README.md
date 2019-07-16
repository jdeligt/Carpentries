# Carpentries
Snippets relating the carpentries curriculum

-----
# Data Carpentry for Ecologists - Day2 prep
library(tidyverse)

# Load 'dirty' data
surveys <- read_csv("data/portal_data_joined.csv")

# ----------------- Cleaning of data ----------------- 
## Remove missing data
surveys_complete <- surveys %>%
  filter(!is.na(weight),           # remove missing weight
         !is.na(hindfoot_length),  # remove missing hindfoot_length
         !is.na(sex))              # remove missing sex

## Extract the most common species_id
species_counts <- surveys_complete %>%
  count(species_id) %>% 
  filter(n >= 50)

## Only keep the most common species
surveys_complete <- surveys_complete %>%
  filter(species_id %in% species_counts$species_id)

## Export cleaned data
dir.create("data_output")
write_csv(surveys_complete, path = "data_output/surveys_complete.csv")

# --------------- Start of day 2 ---------------  

# Load cleaned data
surveys_complete <- read_csv("data_output/surveys_complete.csv")
