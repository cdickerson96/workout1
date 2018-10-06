workout01-cory-dickerson
================

### Repo Tasks and Library Adds

``` bash
git config --global user.name "Cory Dickerson"
git config --global user.email "cdickerson@berkeley.edu"
git config --global core.editor "nano -w"
```

``` bash
cd ../../Desktop/'School Files'/'Fall 2018 Semester'/'Stat 133'/'hw-stat133'
git init
git remote add origin https://github.com/stat133-f18/hw-stat133-cdickerson96
git pull origin master
```

    ## bash: line 0: cd: ../../Desktop/School Files/Fall 2018 Semester/Stat 133/hw-stat133: No such file or directory
    ## Reinitialized existing Git repository in /Users/Cory/Desktop/School Files/Fall 2018 Semester/Stat 133/hw-stat133/workout1/report/.git/
    ## fatal: remote origin already exists.
    ## From https://github.com/stat133-f18/hw-stat133-cdickerson96
    ##  * branch            master     -> FETCH_HEAD
    ## Already up-to-date.

``` r
# adding libraries
library(dplyr)
```

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
library(ggplot2)
library(readr)
```

### File Structure

``` bash
#mkdir 'workout1'
#cd 'workout1'
#touch README.md
#mkdir 'data' 'code' 'output' 'report'
```

``` bash
#cd ../../
#git add 'workout1'/
#git commit -m "first commit"
```

### Download the Data

``` bash
cd ../data
curl -O https://raw.githubusercontent.com/ucb-stat133/stat133-fall-2018/master/data/nba2018.csv
```

    ##   % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
    ##                                  Dload  Upload   Total   Spent    Left  Speed
    ## 
      0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
    100 94937  100 94937    0     0   246k      0 --:--:-- --:--:-- --:--:--  247k

### Create and Edit a README.md File

``` bash
#cd ../
#git add README.md
#git commit -m "README.md file description"
```

### Create a Data Dictionary

``` r
setwd('../data')
file.create(file.path('../data','nba2018-dictionary.md'))
```

    ## [1] TRUE

``` r
#file.edit('nba2018-dictionary.md')
```

### Data Preparation

``` bash
#cd ../../
#git add 'workout1'/
#git commit -m " add data dictionary, summaries, and csv"
```

### Ranking Teams

``` r
library(ggplot2)
library(dplyr)
library(readr)
```

``` r
teams <- read_csv('../data/nba2018-teams.csv')
```

    ## Parsed with column specification:
    ## cols(
    ##   team = col_character(),
    ##   experience = col_integer(),
    ##   salary = col_double(),
    ##   points3 = col_integer(),
    ##   points2 = col_integer(),
    ##   points1 = col_integer(),
    ##   points = col_integer(),
    ##   off_rebounds = col_integer(),
    ##   def_rebounds = col_integer(),
    ##   assists = col_integer(),
    ##   steals = col_integer(),
    ##   blocks = col_integer(),
    ##   turnovers = col_integer(),
    ##   fouls = col_integer(),
    ##   efficiency = col_double()
    ## )

``` r
plot <- ggplot(teams, aes(x = reorder(team,salary), y = salary)) + geom_bar(stat='identity', width = 0.8, position = position_dodge(width = .9)) + coord_flip() + theme_light() +
  theme(
    axis.text.x = element_text(size = 9, color = "gray10"),
    axis.text.y = element_text(size = 9, color = "gray10")) +
  geom_hline(aes(yintercept = mean(salary)), color = "red")
plot + labs(x = "Teams", y = "Salary (in millions)", title = "NBA Teams ranked by Total Salary")
```

![](workout01-cory-dickerson_files/figure-markdown_github/barplot%201-1.png)

``` r
plot2 <- ggplot(teams, aes(x = reorder(team,points), y = points)) + geom_bar(stat='identity', width = 0.8, position = position_dodge(width = .9)) + coord_flip() + theme_light() +
  theme(
    axis.text.x = element_text(size = 9, color = "gray10"),
    axis.text.y = element_text(size = 9, color = "gray10")) +
  geom_hline(aes(yintercept = mean(points)), color = "red")
plot2 + labs(x = "Teams", y = "Points", title = "NBA Teams ranked by Total Points")
```

![](workout01-cory-dickerson_files/figure-markdown_github/barplot%202-1.png)

``` r
plot3 <- ggplot(teams, aes(x = reorder(team,efficiency), y = efficiency)) + geom_bar(stat='identity', width = 0.8, position = position_dodge(width = .9)) + coord_flip() + theme_light() +
  theme(
    axis.text.x = element_text(size = 9, color = "gray10"),
    axis.text.y = element_text(size = 9, color = "gray10")) +
  geom_hline(aes(yintercept = mean(efficiency)), color = "red")
plot3 + labs(x = "Teams", y = "Total Efficiency", title = "NBA Teams ranked by Total Efficiency")
```

![](workout01-cory-dickerson_files/figure-markdown_github/barplot%203-1.png)

``` r
getwd()
```

    ## [1] "/Users/Cory/Desktop/School Files/Fall 2018 Semester/Stat 133/hw-stat133/workout1/report"

``` r
# getting all variables
nba2018 <- read_csv(
  '../data/nba2018.csv',
  col_types = cols(
    player = col_character(),
    number = col_character(),
    team = col_character(),
    position = col_factor(c("C","PF","PG","SF","SG")),
    height = col_character(),
    weight = col_integer(),
    birth_date = col_character(),
    country = col_character(),
    experience = col_character(),
    college = col_character(),
    salary = col_double(),
    rank = col_integer(),
    age = col_integer(),
    games = col_integer(),
    games_started = col_integer(),
    minutes = col_integer(),
    field_goals = col_integer(),
    field_goals_atts = col_integer(),
    field_goals_perc = col_double(),
    points3 = col_integer(),
    points3_atts = col_integer(),
    points3_perc = col_double(),
    points2 = col_integer(),
    points2_atts = col_integer(),
    points2_perc = col_double(),
    effective_field_goal_perc = col_double(),
    points1 = col_integer(),
    points1_atts = col_integer(),
    points1_perc = col_double(),
    off_rebounds = col_integer(),
    def_rebounds = col_integer(),
    total_rebounds = col_integer(),
    assists = col_integer(),
    steals = col_integer(),
    blocks = col_integer(),
    turnovers = col_integer(),
    fouls = col_integer(),
    points = col_integer()
  )
)
```

``` r
# adding new index by calculating it
nba2018_w_accuracy_index <- mutate(nba2018, accuracy = (field_goals_perc + points3_perc + points2_perc + points1_perc)/games)
```

``` r
# getting columns needed for plot 
plotdata <- select(nba2018_w_accuracy_index,team, accuracy)
plotdata <- (na.exclude(plotdata))
```

``` r
# manipulating data to get accuracy for each team
dat <- summarize(group_by(plotdata, team),
          accuracy = sum(accuracy))
dat
```

    ## # A tibble: 30 x 2
    ##    team  accuracy
    ##    <chr>    <dbl>
    ##  1 ATL      1.46 
    ##  2 BOS      1.07 
    ##  3 BRK      1.73 
    ##  4 CHI      0.821
    ##  5 CHO      1.26 
    ##  6 CLE      2.26 
    ##  7 DAL      2.96 
    ##  8 DEN      0.720
    ##  9 DET      0.608
    ## 10 GSW      0.500
    ## # ... with 20 more rows

``` r
# plotting index of accuracy
plot4 <- ggplot(dat, aes(x = reorder(team,accuracy), y = accuracy)) + geom_bar(stat='identity', width = 0.8, position = position_dodge(width = .9)) + coord_flip() + theme_light() +
  theme(
    axis.text.x = element_text(size = 9, color = "gray10"),
    axis.text.y = element_text(size = 9, color = "gray10")) +
  geom_hline(aes(yintercept = mean(accuracy)), color = "red")
plot3 + labs(x = "Teams", y = "Accuracy", title = "NBA Teams ranked by Accuracy")
```

![](workout01-cory-dickerson_files/figure-markdown_github/barplot%204-1.png)

My new index `accuracy` is calculated by adding up the percentages in all point values, which include points, free throws, and field goals. I then divided it by the games played. My rationale is that the teams that make a higher proportion of their shots (i.e. more acurate) are more likely to be the top teams.

### Comments and Reflections

Overall, I felt that this project was challenging. While it wasn't the first time I have worked with GitHub or having a file structure in this format, having all of these elements together in the project made it tedius. This was not the first time using relative paths, but the importance of the are that they allow for different individuals to look at the data and reports while having a different file structure of their own. This was my first time using an R script file, and writing code on there was awkward at first, but it does feel easier than an rmd file once I got used to it. The plots were very difficult for me even though I saw them in class. It was because there were options of the ggplots that we did go over, but I have not extensively practiced yet. Writing tables to csv was very easy even though we have not done this before in lab. It is simply a reverse of the read option so it was intuitive. It took me about 7 to 8 hours to complete this assignment, and the most consuming portion was the plots. I found the capabiities that I have with data to be interesting after this project. I am thinking of many ways that I can use this information to work with data on my own.

``` bash
#cd ../../
#git add 'workout1'/
#git commit -m " add plots and comments"
```
