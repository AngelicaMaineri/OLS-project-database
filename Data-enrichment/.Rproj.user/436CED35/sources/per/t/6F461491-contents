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
#install.packages("wordcloud")
library(wordcloud)
#install.packages("RColorBrewer")
library(RColorBrewer)
#install.packages("wordcloud2")
library(wordcloud2)

# for embeddings
#install.packages("word2vec")
library(word2vec)

## 2. Load data ----
df = read_delim("Data/projects.csv")
domains = read_delim("Data/domains.csv")

# Create list domain
# Science = Astronomy, Chemistry, Computer Science, Earth Sciences, Life Sciences, Mathematics and Physics.
# SSH = 

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
  mutate(keywords = tolower(keywords)) |> # remove capitalization to avoid duplication
  mutate(keywords = str_trim(keywords, "right")) |>  #remove all trailing whitespace
  mutate(keywords = str_trim(keywords, "left")) |> #remove all leading whitespace
  print(n=100)

  
# make list of unique keywords, remove duplicates
(list = unique(df2$keywords))  

# with occurrences
df3 = df2 |>
  mutate(n=1) |>
  dplyr::select("keywords", "n") |>
  group_by(keywords) |>
  count(n) |>
  ungroup() |>
  print()

# remove capitalisation
domains = domains |>
  mutate(discipline=tolower(discipline))

(listdf3 = unique(df3$keywords))  

## 4. Wordcloud -----
set.seed(42) # for reproducibility 
#(wc1 = wordcloud(words = df3$keywords, freq = df3$nn, min.freq = 1, max.freq = 50, colors=brewer.pal(8, "Dark2")))

## 5. String match
(unique(df2$keywords)%in%unique(domains$discipline))

#write.csv(df2, file = "data/keywords.csv")

df_enriched = left_join(df2, domains, by=c("keywords" = "discipline"))

count(df_enriched, domain)

df_dom = left_join(df, df_enriched, by="id", multiple = "any") |>
  dplyr::select(!keywords.y, !row) |>
  rename(keywords = keywords.x) |>
  print(n=100) 
  
col_order <- c("id", "title","participants","mentors","description","cohort", "keywords", "status", "domain")
df_dom = df_dom[, col_order]
df_dom

# export
write.csv(df_dom, file="Data/projects_domain.csv", fileEncoding = "UTF-8")


## Next steps
#' Improve domains classification
#' Add "open science" or similar; add 'community building"
