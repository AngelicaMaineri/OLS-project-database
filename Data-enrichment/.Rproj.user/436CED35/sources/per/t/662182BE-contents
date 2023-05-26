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

rm(list = ls())
setwd("C:/Users/angel/Documents/GitHub/OLS-project-database/Data-enrichment")

## 2. Load data ----
df = read_delim("Data/projects_domain.csv") # Load data with added domain
df_people = read_delim("C:/Users/angel/Documents/GitHub/ols-program-paper/data/people.csv") # Load updated copy from the paper repo

## 3. data prep
colnames(df_people)[1] = c("githandle") #rename firs col

## 4. Merge

#select only first and last names and github handle
#create full name (NAME) in df_people
#create full gitlINK (GITFULL) in df_people

df_people_small = df_people |>
  select(c("githandle", "first-name", "last-name")) |>
  mutate(name = paste(`first-name`, `last-name`, sep = ' ')) |>
  mutate(gitfull = paste("https://github.com/", githandle, sep = ''))  |>
  select(c("name", "gitfull"))
df_people_small

#solve duplicates!!!!!
list_names = df_people_small |>
  select(c(name)) |>
  mutate(n=1) |>
  group_by(name) |>
  count(n) |>
  filter(nn>1) |>
  print()

df_people_small$drop = 0
df_people_small$drop[df_people_small$gitfull=="https://github.com/david-selassie-opoku"] = 1
df_people_small$drop[df_people_small$gitfull=="https://github.com/gladys-jerono-rotich"] = 1
df_people_small$drop[df_people_small$gitfull=="https://github.com/hilyatuz-zahroh"] = 1
df_people_small$drop[df_people_small$gitfull=="https://github.com/iris-san-pedro"] = 1
df_people_small$drop[df_people_small$gitfull=="https://github.com/laurah-nyasita-ondari"] = 1
df_people_small$drop[df_people_small$gitfull=="https://github.com/marta-lloret-llinares"] = 1
df_people_small$drop[df_people_small$gitfull=="https://github.com/muhammetcelik"] = 1
df_people_small$drop[df_people_small$gitfull=="https://github.com/pradeep-eranti"] = 1
df_people_small$drop[df_people_small$gitfull=="https://github.com/umar-farouk-ahmad"] = 1

df_people_small = df_people_small |>
  filter(drop == 0)
colnames(df_people_small)
cols = c("name", "gitfull")
df_people_small = df_people_small[, cols] 

# split participants
df = df |>
  separate(participants, into = c("part1", "part2", "part3", "part4", "part5", "part6"), sep=",[ ]" ) |>
  print(n=100)

# long format
df_long = df |>
  gather(partnum, name, part1:part6, factor_key=TRUE)

# if df$part1-6 in df_people_small, then change string to [df_part1-6](gitfull)
df_long = left_join(df_long, df_people_small, by=c("name"))
df_long = df_long |>
  mutate(name = paste("<a href=\"", gitfull, "\">", name, "</a>", sep = "")) |> #   <a href="https://pypi.org/project/plenpy/">plenoptic</a>

  #mutate(name = paste("[", name, "](", gitfull, ")", sep = "")) |> 
  select(-c("gitfull"))
df_long

# back to wide format
df_long$id <- factor(df_long$id) 
df_wide = df_long |>
  pivot_wider(names_from = partnum, values_from = name)

df_wide = df_wide|>
  mutate(participants = case_when(
      part2=="<a href=\"NA\">NA</a>" & part3=="<a href=\"NA\">NA</a>" & part4=="<a href=\"NA\">NA</a>" & part5=="<a href=\"NA\">NA</a>" & part6=="<a href=\"NA\">NA</a>" ~ paste(part1),  
      part2!="<a href=\"NA\">NA</a>" & part3=="<a href=\"NA\">NA</a>" & part4=="<a href=\"NA\">NA</a>" & part5=="<a href=\"NA\">NA</a>" & part6=="<a href=\"NA\">NA</a>" ~ paste(part1, part2, sep=", "),
      part2!="<a href=\"NA\">NA</a>" & part3!="<a href=\"NA\">NA</a>" & part4=="<a href=\"NA\">NA</a>" & part5=="<a href=\"NA\">NA</a>" & part6=="<a href=\"NA\">NA</a>" ~ paste(part1, part2, part3, sep=", "),
      part2!="<a href=\"NA\">NA</a>" & part3!="<a href=\"NA\">NA</a>" & part4!="<a href=\"NA\">NA</a>" & part5=="<a href=\"NA\">NA</a>" & part6=="<a href=\"NA\">NA</a>" ~ paste(part1, part2, part3, part4, sep=", "),
      part2!="<a href=\"NA\">NA</a>" & part3!="<a href=\"NA\">NA</a>" & part4!="<a href=\"NA\">NA</a>" & part5!="<a href=\"NA\">NA</a>" & part6=="<a href=\"NA\">NA</a>" ~ paste(part1, part2, part3, part4, part5,  sep=", "),
      part2!="<a href=\"NA\">NA</a>" & part3!="<a href=\"NA\">NA</a>" & part4!="<a href=\"NA\">NA</a>" & part5!="<a href=\"NA\">NA</a>" & part6!="<a href=\"NA\">NA</a>" ~ paste(part1, part2, part3, part4, part5, part6, sep=", ")))
df_wide$participants

# clean
df_wide = df_wide |>
  select(-c("part1", "part2", "part3", "part4", "part5", "part6"))

col_order <- c("...1", "id", "title", "participants", "mentors","description", "cohort","keywords", "status", "domain")
df2 <- df_wide[, col_order]


# export
write.csv(df2, file="Data/projects_domain_people.csv", fileEncoding = "UTF-8")
