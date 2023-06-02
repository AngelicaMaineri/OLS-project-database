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


## Phase 3: Prepare table
Compile markdown and export html

## Phase 4: Publish
Publish github page

# How to update the table
## 
