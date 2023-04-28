#' OLS-Project-databases
#' Assign domain
#' 
#' Created on 28/04/2023 by Angelica Maineri
#' 
#' Aim: write script to automatically tag the domain (SSH, LSH, NES, Other)
#' based on keywords

## 1. Load and install packages -----
# Uncomment (= remove the #) the following lines as fit:
#install.packages("tidyverse")

library(tidyverse) # for most operations

# for wordclouds
install.packages("wordcloud")
library(wordcloud)
install.packages("RColorBrewer")
library(RColorBrewer)
install.packages("wordcloud2")
library(wordcloud2)


## 2. Load data ----
df = read_delim("Data/projects.csv")

## 3. Prepare data ----
# rename name field to title
df = df |>
  rename(title = name)
# add identifier for projects - OLS + cohort + number
df = df |>
  group_by(cohort) |>
  mutate(row = row_number()) |> 
  ungroup()

df = df |>
  mutate(id = paste("OLS", df$cohort, df$row, sep = "-")) |>
  print()
df$id

#make list of keywords, retain project ID
df2 = df |> 
  mutate(keywords = strsplit(keywords, ",[ ]")) |>
  unnest(keywords) |>
#  group_by(id) |>
#  mutate(row = row_number()) |>
 # spread(row, keywords) |>
  print()

df2 = df2 |>
  dplyr::select(c("keywords", "id")) |>
  print(n=100)

# make list of unique keywords, remove duplicates
(list = unique(df2$keywords))  

# with occurrences
df3 = df2 |>
  mutate(n=1) |>
  dplyr::select("keywords", "n") |>
  mutate(keywords = tolower(keywords)) |> # remove capitalization to avoid duplication
  group_by(keywords) |>
  count(n) |>
  ungroup() |>
  print()



## 4. Wordcloud -----
set.seed(42) # for reproducibility 
(wc1 = wordcloud(words = df3$keywords, freq = df3$nn, min.freq = 1, max.freq = 50, colors=brewer.pal(8, "Dark2")))

