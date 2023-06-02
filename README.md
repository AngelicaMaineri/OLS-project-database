# Building a project database of OLS projects
Hello! Thank you for your interest in my project. 

In this repository, I want to build a searchable database of OLS projects to make it easier to navigate them for past, current, and future OLS participants. [Open Life Science - OLS](https://openlifesci.org) is a mentorship programme to learn more about Open Science and Open Leadership, and mentees carry out individual or group projects. With over [200 projects](https://openlifesci.org/about#projects), the list is now very rich yet also difficult to navigate. The aim of my project is to build a searchable database of OLS projects, for future, current and past OLS participants.

Thanks to my database, it will be possible to browse all projects from one page, filter them based on keywords and/or project members, and track the projects progress and outputs. 

Contribution guidelines will follow soon. In the meantime, if you have ideas or comments, please open an issue or reach out to [Angelica Maineri](mailto:angelica@odissei-data.nl)

The prototype of the database can be seen at [https://angelicamaineri.github.io/OLS-project-database/](https://angelicamaineri.github.io/OLS-project-database/)

_This project is carried out in the framework of [OLS-7](https://openlifesci.org/ols-7)_

# Process description
In this section, I describe the steps undertaken to get from the input data to the prototype. 

## Phase 0: Design
Prepare you project, formulate your vision, write down or draw what you want to achieve. 

In my case, I had developed a [data model](https://docs.google.com/presentation/d/1N15TP1flXXeWl8OThZXr4URXzkGkxkoYJO-VhMN0EM0/edit#slide=id.p) which however was never fully implemented, but it helped me to expand my thoughts. I also drew a fictional example of how I would like the database (or even better, the catalogue) to look like at the end (see [here](https://docs.google.com/presentation/d/1IQwulPPnaIjKQucp-0K9TO0txcmdoIS9DlHMwXw_JIA/edit)). Hopefully this can be of inspiration for somebody else to pick up and continue this work!

## Phase 1: Get data 
The first step is to create (or get) the input spreadsheet in any format that can be imported into R (e.g. csv, xls, .dta, etc).

In my case, I wanted a list of the OLS projects that are already [listed on the OLS website (by cohort)](https://openlifesci.org/about#projects). After talking with an expert (thanks Berenice!) I found out that such a spreadsheet already existed in the [OLS paper repository](https://github.com/open-life-science/ols-program-paper) in the form of a [project spreadsheet](https://github.com/open-life-science/ols-program-paper/blob/main/data/projects.csv), together with an [overview of the people and their github handles](https://github.com/open-life-science/ols-program-paper/blob/main/data/people.csv). Hence I forked the repository and then loaded the data into R via the scripts from Phase 2.

## Phase 2: Data preparation and enrichment. 
This step is not mandatory, but often needed. From the initial spreadsheet, you might need to clean your data, rearrange columns, add information, you name it. I prefer to do this as much as possible via scripts to keep track of the changes. 

In my case, I wanted to enrich the initial dataset in several ways:
- Add the domain; in this case I decided to use some very coarse categories based on the way the Dutch research council classifies domains: LSH = life sciences and health; NES = Natural and Engineering Sciences; SSH = Social Sciences and Humanities. I didn't want to tag each project manually, so I tried to map keywords to domains (the mapping is in [./Data-enrichment/Data/domains.csv](./Data-enrichment/Data/domains.csv)) to then tag the projects automatically based on the keywords. The script can be found in [./Data-enrichment/Scripts/1_tag_domain.R](./Data-enrichment/Scripts/1_tag_domain.R). Unfortunately, not many projects have a matching domain based on the keywords. See the section "Next steps" to read some ideas on how to improve this. 
- I wanted to add the links to the github profiles of all the people mentioned (participants and mentors). The steps to do it in practice are included in [./Data-enrichment/Scripts/2_tag_people.R](./Data-enrichment/Scripts/2_tag_people.R)
At the end of this phase, I exported a [processed and enriched .csv file](./Data-enrichment/Data/projects_domain_people.csv).

As a side output, since I was working with the keywords, I also made a wordcloud of keywords! See [./Data-enrichment/wordcloud_1.pdf]{./Data-enrichment/wordcloud_1.pdf).


## Phase 3: Prepare table
At this point, you should have a spreadsheet (I had a .csv) which is actually the table you want to display. In this phase, you create a Rmarkdown file, which will become eventually the webpage you display via GitHub pages. That means you can write text and explanations as you see fit, using Markdown language. 

In my [RMarkdown](./project-database.Rmd), I first load two packages (tidyverse and DT), I then load the .csv file and display it using the datatable function, and finally 'knit' all this into an html file named [index.html](./docs/index.html), which I save in a new folder [docs](./docs). You can check the datatable documentation to change the display and functionalities of the table (e.g. including search bars for each column, deciding how many rows to be displayed by default, exclude some columns, etc.).

## Phase 4: Publish
At this point, you can just go to the settings of your (public) GitHub repository, go to Pages, and deploy from main/docs. On the top of the page, the URL to your Page will be available. Congrats!

# How to update the page
## Step 1
## Step 2
## Step 3
## Step 4

# Next steps



