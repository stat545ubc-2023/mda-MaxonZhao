*To complete this milestone, you can either edit [this `.rmd`
file](https://raw.githubusercontent.com/UBC-STAT/stat545.stat.ubc.ca/master/content/mini-project/mini-project-2.Rmd)
directly. Fill in the sections that are commented out with
`<!--- start your work here--->`. When you are done, make sure to knit
to an `.md` file by changing the output in the YAML header to
`github_document`, before submitting a tagged release on canvas.*

# Welcome to the rest of your mini data analysis project!

In Milestone 1, you explored your data. and came up with research
questions. This time, we will finish up our mini data analysis and
obtain results for your data by:

-   Making summary tables and graphs
-   Manipulating special data types in R: factors and/or dates and
    times.
-   Fitting a model object to your data, and extract a result.
-   Reading and writing data as separate files.

We will also explore more in depth the concept of *tidy data.*

**NOTE**: The main purpose of the mini data analysis is to integrate
what you learn in class in an analysis. Although each milestone provides
a framework for you to conduct your analysis, it’s possible that you
might find the instructions too rigid for your data set. If this is the
case, you may deviate from the instructions – just make sure you’re
demonstrating a wide range of tools and techniques taught in this class.

# Instructions

**To complete this milestone**, edit [this very `.Rmd`
file](https://raw.githubusercontent.com/UBC-STAT/stat545.stat.ubc.ca/master/content/mini-project/mini-project-2.Rmd)
directly. Fill in the sections that are tagged with
`<!--- start your work here--->`.

**To submit this milestone**, make sure to knit this `.Rmd` file to an
`.md` file by changing the YAML output settings from
`output: html_document` to `output: github_document`. Commit and push
all of your work to your mini-analysis GitHub repository, and tag a
release on GitHub. Then, submit a link to your tagged release on canvas.

**Points**: This milestone is worth 50 points: 45 for your analysis, and
5 for overall reproducibility, cleanliness, and coherence of the Github
submission.

**Research Questions**: In Milestone 1, you chose two research questions
to focus on. Wherever realistic, your work in this milestone should
relate to these research questions whenever we ask for justification
behind your work. In the case that some tasks in this milestone don’t
align well with one of your research questions, feel free to discuss
your results in the context of a different research question.

# Learning Objectives

By the end of this milestone, you should:

-   Understand what *tidy* data is, and how to create it using `tidyr`.
-   Generate a reproducible and clear report using R Markdown.
-   Manipulating special data types in R: factors and/or dates and
    times.
-   Fitting a model object to your data, and extract a result.
-   Reading and writing data as separate files.

# Setup

Begin by loading your data and the tidyverse package below:

    library(datateachr) # <- might contain the data you picked!
    library(tidyverse)

# Task 1: Process and summarize your data

From milestone 1, you should have an idea of the basic structure of your
dataset (e.g. number of rows and columns, class types, etc.). Here, we
will start investigating your data more in-depth using various data
manipulation functions.

### 1.1 (1 point)

First, write out the 4 research questions you defined in milestone 1
were. This will guide your work through milestone 2:

<!-------------------------- Start your work below ---------------------------->

\# Research topic 1

\#Distribution of Tree Species:

\#Question: What are the most common tree species in Vancouver, and how
are they distributed across different neighbourhoods?

\# Research topic 2

\#Tree Planting Over Time:

\#Question: Has there been an increase in the number of trees planted in
Vancouver over the years?

\# Research topic 3: \#Tree Distribution by Neighbourhood and Street:

\#Question: Which neighbourhoods and streets in Vancouver have the
highest concentration of trees?

# Research topic 4:

\#Trees and Urban Infrastructure:

\#Question: Is there a relationship between the presence of curbs, root
barriers, and the size (diameter) or health of trees?

<!----------------------------------------------------------------------------->

Here, we will investigate your data using various data manipulation and
graphing functions.

### 1.2 (8 points)

Now, for each of your four research questions, choose one task from
options 1-4 (summarizing), and one other task from 4-8 (graphing). You
should have 2 tasks done for each research question (8 total). Make sure
it makes sense to do them! (e.g. don’t use a numerical variables for a
task that needs a categorical variable.). Comment on why each task helps
(or doesn’t!) answer the corresponding research question.

Ensure that the output of each operation is printed!

Also make sure that you’re using dplyr and ggplot2 rather than base R.
Outside of this project, you may find that you prefer using base R
functions for certain tasks, and that’s just fine! But part of this
project is for you to practice the tools we learned in class, which is
dplyr and ggplot2.

**Summarizing:**

1.  Compute the *range*, *mean*, and *two other summary statistics* of
    **one numerical variable** across the groups of **one categorical
    variable** from your data.
2.  Compute the number of observations for at least one of your
    categorical variables. Do not use the function `table()`!
3.  Create a categorical variable with 3 or more groups from an existing
    numerical variable. You can use this new variable in the other
    tasks! *An example: age in years into “child, teen, adult, senior”.*
4.  Compute the proportion and counts in each category of one
    categorical variable across the groups of another categorical
    variable from your data. Do not use the function `table()`!

**Graphing:**

1.  Create a graph of your choosing, make one of the axes logarithmic,
    and format the axes labels so that they are “pretty” or easier to
    read.
2.  Make a graph where it makes sense to customize the alpha
    transparency.

Using variables and/or tables you made in one of the “Summarizing”
tasks:

1.  Create a graph that has at least two geom layers.
2.  Create 3 histograms, with each histogram having different sized
    bins. Pick the “best” one and explain why it is the best.

Make sure it’s clear what research question you are doing each operation
for!

<!------------------------- Start your work below ----------------------------->

    library(dplyr)
    library(datateachr)

    data("vancouver_trees")
    names(vancouver_trees)

    ##  [1] "tree_id"            "civic_number"       "std_street"        
    ##  [4] "genus_name"         "species_name"       "cultivar_name"     
    ##  [7] "common_name"        "assigned"           "root_barrier"      
    ## [10] "plant_area"         "on_street_block"    "on_street"         
    ## [13] "neighbourhood_name" "street_side_name"   "height_range_id"   
    ## [16] "diameter"           "curb"               "date_planted"      
    ## [19] "longitude"          "latitude"

    library(datateachr)
    library(tidyverse)
    library(ggplot2)
    #Research topic 1: Distribution of Tree Species

    #Summarizing:

    #Summarizing: Compute the number of observations for the species_name categorical variable. This will give us an idea of the most common tree species in Vancouver.

    vancouver_trees %>%
      group_by(species_name) %>%
      tally() %>%
      arrange(-n)

    ## # A tibble: 283 × 2
    ##    species_name     n
    ##    <chr>        <int>
    ##  1 SERRULATA    13357
    ##  2 CERASIFERA   12031
    ##  3 PLATANOIDES  11963
    ##  4 RUBRUM        8467
    ##  5 AMERICANA     5515
    ##  6 SYLVATICA     5285
    ##  7 BETULUS       5195
    ##  8 EUCHLORA   X  4427
    ##  9 FREEMANI   X  4164
    ## 10 CAMPESTRE     3477
    ## # ℹ 273 more rows

    # Graphing: Create a graph that displays the number of each tree species distributed across different neighbourhoods.

    vancouver_trees %>%
      group_by(species_name, neighbourhood_name) %>%
      tally() %>%
      ggplot(aes(x = species_name, y = n, fill = neighbourhood_name)) +
      geom_bar(stat="identity", position="dodge") +
      labs(title="Distribution of Tree Species Across Neighbourhoods") +
      theme(axis.text.x = element_text(angle = 45, hjust = 1))

![](Mini-Data-Analysis-Deliverable-2_files/figure-markdown_strict/unnamed-chunk-3-1.png)

    library(datateachr)
    library(tidyverse)
    library(ggplot2)
    #Research topic 2: Tree Planting Over Time
    #Question: Has there been an increase in the number of trees planted in Vancouver over the years?

    #Summarizing: Compute the range, mean, and two other summary statistics (e.g., median, standard deviation) of the date_planted variable.

    vancouver_trees %>%
      summarize(
        range_start = min(date_planted, na.rm = TRUE),
        range_end = max(date_planted, na.rm = TRUE),
        mean_date = mean(date_planted, na.rm = TRUE),
        median_date = median(date_planted, na.rm = TRUE)
      )

    ## # A tibble: 1 × 4
    ##   range_start range_end  mean_date  median_date
    ##   <date>      <date>     <date>     <date>     
    ## 1 1989-10-27  2019-07-03 2004-04-07 2004-01-28

    # Graphing: Create a histogram showing the distribution of the date_planted variable to visualize tree planting trends over time.
    ggplot(vancouver_trees, aes(x = date_planted)) +
      geom_histogram(binwidth = 1) +
      labs(title="Tree Planting Over the Years")

    ## Warning: Removed 76548 rows containing non-finite values (`stat_bin()`).

![](Mini-Data-Analysis-Deliverable-2_files/figure-markdown_strict/unnamed-chunk-4-1.png)

    library(datateachr)
    library(tidyverse)
    library(ggplot2)

    #Research topic 3: Tree Distribution by Neighbourhood and Street
    #Question: Which neighbourhoods and streets in Vancouver have the highest concentration of trees?

    #Summarizing: Compute the proportion and counts of trees in each neighbourhood_name.

    vancouver_trees %>%
      count(neighbourhood_name) %>%
      mutate(proportion = n/sum(n))

    ## # A tibble: 22 × 3
    ##    neighbourhood_name           n proportion
    ##    <chr>                    <int>      <dbl>
    ##  1 ARBUTUS-RIDGE             5169     0.0353
    ##  2 DOWNTOWN                  5159     0.0352
    ##  3 DUNBAR-SOUTHLANDS         9415     0.0642
    ##  4 FAIRVIEW                  4002     0.0273
    ##  5 GRANDVIEW-WOODLAND        6703     0.0457
    ##  6 HASTINGS-SUNRISE         10547     0.0719
    ##  7 KENSINGTON-CEDAR COTTAGE 11042     0.0753
    ##  8 KERRISDALE                6936     0.0473
    ##  9 KILLARNEY                 6148     0.0419
    ## 10 KITSILANO                 8115     0.0554
    ## # ℹ 12 more rows

    #Graphing: Create a graph that displays the concentration of trees on each street (std_street) across different neighbourhoods.
    vancouver_trees %>%
      group_by(std_street, neighbourhood_name) %>%
      tally() %>%
      ggplot(aes(x = std_street, y = n, fill = neighbourhood_name)) +
      geom_bar(stat="identity", position="dodge") +
      labs(title="Tree Concentration by Street and Neighbourhood") +
      theme(axis.text.x = element_text(angle = 45, hjust = 1))

![](Mini-Data-Analysis-Deliverable-2_files/figure-markdown_strict/unnamed-chunk-5-1.png)

    library(datateachr)
    library(tidyverse)
    library(ggplot2)

    #Research topic 4: Trees and Urban Infrastructure
    #Question: Is there a relationship between the presence of curbs, root barriers, and the size (diameter) or health of trees?

    #Summarizing: Compute the range, mean, and two other summary statistics of the diameter variable across the groups of the curb and root_barrier categorical variables.

    vancouver_trees %>%
      group_by(curb, root_barrier) %>%
      summarize(
        min_diameter = min(diameter, na.rm = TRUE),
        max_diameter = max(diameter, na.rm = TRUE),
        mean_diameter = mean(diameter, na.rm = TRUE),
        median_diameter = median(diameter, na.rm = TRUE),
        .groups = 'drop'
      )

    ## # A tibble: 4 × 6
    ##   curb  root_barrier min_diameter max_diameter mean_diameter median_diameter
    ##   <chr> <chr>               <dbl>        <dbl>         <dbl>           <dbl>
    ## 1 N     N                    0           161           13.1            11.1 
    ## 2 N     Y                    2.25         40.2          3.83            3   
    ## 3 Y     N                    0           435           11.9             9.75
    ## 4 Y     Y                    0.5          86            4.45            3

    #Graphing: Create a graph with at least two geom layers (e.g., points and smooth) that depicts the relationship between tree diameter and presence of curbs and root barriers.
    ggplot(vancouver_trees, aes(x = diameter, y = curb, color = root_barrier)) +
      geom_point() +
      geom_smooth(method = "lm") +
      labs(title="Relationship between Tree Diameter and Urban Infrastructure")

    ## `geom_smooth()` using formula = 'y ~ x'

![](Mini-Data-Analysis-Deliverable-2_files/figure-markdown_strict/unnamed-chunk-6-1.png)

<!----------------------------------------------------------------------------->

### 1.3 (2 points)

Based on the operations that you’ve completed, how much closer are you
to answering your research questions? Think about what aspects of your
research questions remain unclear. Can your research questions be
refined, now that you’ve investigated your data a bit more? Which
research questions are yielding interesting results?

<!------------------------- Write your answer here ---------------------------->
<!----------------------------------------------------------------------------->

# Task 2: Tidy your data

In this task, we will do several exercises to reshape our data. The goal
here is to understand how to do this reshaping with the `tidyr` package.

A reminder of the definition of *tidy* data:

-   Each row is an **observation**
-   Each column is a **variable**
-   Each cell is a **value**

### 2.1 (2 points)

Based on the definition above, can you identify if your data is tidy or
untidy? Go through all your columns, or if you have &gt;8 variables,
just pick 8, and explain whether the data is untidy or tidy.

<!--------------------------- Start your work below --------------------------->
<!----------------------------------------------------------------------------->

### 2.2 (4 points)

Now, if your data is tidy, untidy it! Then, tidy it back to it’s
original state.

If your data is untidy, then tidy it! Then, untidy it back to it’s
original state.

Be sure to explain your reasoning for this task. Show us the “before”
and “after”.

<!--------------------------- Start your work below --------------------------->

    #To untidy the data, we can combine some of the columns together. For example, we can combine the genus_name, species_name, and common_name into a single column.
    # Untidying the data
    untidy_trees <- vancouver_trees %>%
      unite("tree_info", genus_name, species_name, common_name, sep = "|")

    #This would create a single column, tree_info, with values like "Genus|Species|CommonName". This makes the data untidy as we've combined three variables into a single column.

    # Displaying the first few rows of the untidy data
    head(untidy_trees)

    ## # A tibble: 6 × 18
    ##   tree_id civic_number std_street tree_info  cultivar_name assigned root_barrier
    ##     <dbl>        <dbl> <chr>      <chr>      <chr>         <chr>    <chr>       
    ## 1  149556          494 W 58TH AV  ULMUS|AME… BRANDON       N        N           
    ## 2  149563          450 W 58TH AV  ZELKOVA|S… <NA>          N        N           
    ## 3  149579         4994 WINDSOR ST STYRAX|JA… <NA>          N        N           
    ## 4  149590          858 E 39TH AV  FRAXINUS|… AUTUMN APPLA… Y        N           
    ## 5  149604         5032 WINDSOR ST ACER|CAMP… <NA>          N        N           
    ## 6  149616          585 W 61ST AV  PYRUS|CAL… CHANTICLEER   N        N           
    ## # ℹ 11 more variables: plant_area <chr>, on_street_block <dbl>,
    ## #   on_street <chr>, neighbourhood_name <chr>, street_side_name <chr>,
    ## #   height_range_id <dbl>, diameter <dbl>, curb <chr>, date_planted <date>,
    ## #   longitude <dbl>, latitude <dbl>

    #Tidying the Data Back: To tidy the data back to its original form, we'll separate the tree_info column into its original three columns
    # Tidying the data back
    tidy_trees <- untidy_trees %>%
      separate(tree_info, into = c("genus_name", "species_name", "common_name"), sep = "|")

    ## Warning: Expected 3 pieces. Additional pieces discarded in 146611 rows [1, 2, 3, 4, 5,
    ## 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, ...].

    # Displaying the first few rows of the tidied data
    head(tidy_trees)

    ## # A tibble: 6 × 20
    ##   tree_id civic_number std_street genus_name species_name common_name
    ##     <dbl>        <dbl> <chr>      <chr>      <chr>        <chr>      
    ## 1  149556          494 W 58TH AV  ""         U            L          
    ## 2  149563          450 W 58TH AV  ""         Z            E          
    ## 3  149579         4994 WINDSOR ST ""         S            T          
    ## 4  149590          858 E 39TH AV  ""         F            R          
    ## 5  149604         5032 WINDSOR ST ""         A            C          
    ## 6  149616          585 W 61ST AV  ""         P            Y          
    ## # ℹ 14 more variables: cultivar_name <chr>, assigned <chr>, root_barrier <chr>,
    ## #   plant_area <chr>, on_street_block <dbl>, on_street <chr>,
    ## #   neighbourhood_name <chr>, street_side_name <chr>, height_range_id <dbl>,
    ## #   diameter <dbl>, curb <chr>, date_planted <date>, longitude <dbl>,
    ## #   latitude <dbl>

    #Reasoning:
    #The reason for combining columns in the untidy step was to showcase how data can become messy when multiple pieces of information are stored in a single column. This makes data analysis more difficult as extracting and working on individual variables becomes cumbersome. Conversely, the tidying step reverts the data back to a form that's easy to work with, allowing for simpler and more straightforward analysis. The separate and unite functions from the tidyr package are specifically designed for these tasks and are commonly used in tidying operations.

<!----------------------------------------------------------------------------->

### 2.3 (4 points)

Now, you should be more familiar with your data, and also have made
progress in answering your research questions. Based on your interest,
and your analyses, pick 2 of the 4 research questions to continue your
analysis in the remaining tasks:

<!-------------------------- Start your work below ---------------------------->

**1. Research topic 1: Distribution of Tree Species** *Question: What
are the most common tree species in Vancouver, and how are they
distributed across different neighbourhoods?*

**2. Research topic 4: Trees and Urban Infrastructure** *Question: Is
there a relationship between the presence of curbs, root barriers, and
the size (diameter) or health of trees?*

<!----------------------------------------------------------------------------->

Explain your decision for choosing the above two research questions.

<!--------------------------- Start your work below --------------------------->

1.  **Distribution of Tree Species**: Understanding the distribution of
    tree species in Vancouver is crucial. It gives insight into the
    biodiversity of the urban environment. Moreover, certain tree
    species may be preferred in urban settings due to their resistance
    to pollution, their canopy size, or other factors. By examining this
    question, we can gather insights into urban planning and the
    preference for certain tree species over others. Additionally,
    understanding how these species are distributed across neighborhoods
    can reveal socio-economic patterns or urban planning strategies.

2.  **Trees and Urban Infrastructure**: This topic is particularly
    interesting from a sustainability and urban planning perspective. As
    cities grow, it’s crucial to ensure that trees, which provide
    numerous ecological benefits, coexist harmoniously with urban
    infrastructure. Understanding the relationship between tree size,
    health, and urban infrastructures such as curbs and root barriers
    can help urban planners make better decisions in the future.
    Moreover, it’s a unique intersection of biology and infrastructure,
    and answering this question has direct implications for urban
    development strategies.

<!----------------------------------------------------------------------------->

Now, try to choose a version of your data that you think will be
appropriate to answer these 2 questions. Use between 4 and 8 functions
that we’ve covered so far (i.e. by filtering, cleaning, tidy’ing,
dropping irrelevant columns, etc.).

(If it makes more sense, then you can make/pick two versions of your
data, one for each research question.)

<!--------------------------- Start your work below --------------------------->

**1. Distribution of Tree Species:**

For this question, I’m interested in the types of tree species and their
distribution across different neighborhoods. Thus, the relevant columns
would be **`genus_name`**, **`species_name`**, and
**`neighbourhood_name`**.

Let’s filter and select the data for this purpose:

    tree_species_distribution <- vancouver_trees %>%
      select(genus_name, species_name, neighbourhood_name) %>%
      filter(!is.na(genus_name) & !is.na(species_name) & !is.na(neighbourhood_name)) %>%
      group_by(genus_name, species_name, neighbourhood_name) %>%
      tally() %>%
      arrange(-n)
    print(tree_species_distribution)

    ## # A tibble: 3,713 × 4
    ## # Groups:   genus_name, species_name [361]
    ##    genus_name species_name neighbourhood_name           n
    ##    <chr>      <chr>        <chr>                    <int>
    ##  1 PRUNUS     CERASIFERA   VICTORIA-FRASERVIEW       1241
    ##  2 ACER       PLATANOIDES  KITSILANO                 1188
    ##  3 ACER       PLATANOIDES  DUNBAR-SOUTHLANDS         1165
    ##  4 ACER       PLATANOIDES  SHAUGHNESSY               1139
    ##  5 ACER       PLATANOIDES  KERRISDALE                1067
    ##  6 PRUNUS     CERASIFERA   DUNBAR-SOUTHLANDS         1061
    ##  7 ACER       RUBRUM       DOWNTOWN                  1019
    ##  8 PRUNUS     SERRULATA    KENSINGTON-CEDAR COTTAGE  1002
    ##  9 PRUNUS     SERRULATA    DUNBAR-SOUTHLANDS          994
    ## 10 PRUNUS     SERRULATA    RENFREW-COLLINGWOOD        980
    ## # ℹ 3,703 more rows

**2. Trees and Urban Infrastructure:**

For this question, I need information about the presence of curbs, root
barriers, the tree’s diameter (size), and any available health
indicators. The relevant columns are **`curb`**, **`root_barrier`**,
**`diameter`**, and possibly **`genus_name`** or **`species_name`** as
an indirect health indicator (some species might be more resilient than
others).

    tree_infrastructure_relation <- vancouver_trees %>%
      select(curb, root_barrier, diameter, genus_name, species_name) %>%
      filter(!is.na(curb) & !is.na(root_barrier) & !is.na(diameter)) %>%
      arrange(diameter)
    print(tree_infrastructure_relation)

    ## # A tibble: 146,611 × 5
    ##    curb  root_barrier diameter genus_name  species_name 
    ##    <chr> <chr>           <dbl> <chr>       <chr>        
    ##  1 Y     N                   0 LIQUIDAMBAR STYRACIFLUA  
    ##  2 N     N                   0 ACER        CAMPESTRE    
    ##  3 Y     N                   0 PRUNUS      CERASIFERA   
    ##  4 Y     N                   0 PRUNUS      X YEDOENSIS  
    ##  5 N     N                   0 MAGNOLIA    XX           
    ##  6 Y     N                   0 AMELANCHIER GRANDIFLORA X
    ##  7 Y     N                   0 PARROTIA    PERSICA      
    ##  8 Y     N                   0 PRUNUS      CERASIFERA   
    ##  9 Y     N                   0 STYRAX      JAPONICA     
    ## 10 Y     N                   0 ACER        PLATANOIDES  
    ## # ℹ 146,601 more rows

# Task 3: Modelling

## 3.0 (no points)

Pick a research question from 1.2, and pick a variable of interest
(we’ll call it “Y”) that’s relevant to the research question. Indicate
these.

<!-------------------------- Start your work below ---------------------------->

**Research Question**: Is there a relationship between the presence of
curbs, root barriers, and the size (diameter) or health of trees?

**Variable of interest**: Diameter (as an indicator of tree size)

<!----------------------------------------------------------------------------->

## 3.1 (3 points)

Fit a model or run a hypothesis test that provides insight on this
variable with respect to the research question. Store the model object
as a variable, and print its output to screen. We’ll omit having to
justify your choice, because we don’t expect you to know about model
specifics in STAT 545.

-   **Note**: It’s OK if you don’t know how these models/tests work.
    Here are some examples of things you can do here, but the sky’s the
    limit.

    -   You could fit a model that makes predictions on Y using another
        variable, by using the `lm()` function.
    -   You could test whether the mean of Y equals 0 using `t.test()`,
        or maybe the mean across two groups are different using
        `t.test()`, or maybe the mean across multiple groups are
        different using `anova()` (you may have to pivot your data for
        the latter two).
    -   You could use `lm()` to test for significance of regression
        coefficients.

<!-------------------------- Start your work below ---------------------------->

we can fit a linear model to investigate the relationship between tree
diameter (our dependent variable) and the presence of curbs and root
barriers (our independent variables).

Both “curb” and “root\_barrier” seem to be categorical variables
(assuming they represent the presence or absence of these
infrastructures). Given that, we’d want to treat them as factors in our
model.

    # Fit a linear model 
    tree_model <- lm(diameter ~ factor(curb) + factor(root_barrier), data = vancouver_trees)

    # Print the summary of the model to screen
    summary(tree_model)

    ## 
    ## Call:
    ## lm(formula = diameter ~ factor(curb) + factor(root_barrier), 
    ##     data = vancouver_trees)
    ## 
    ## Residuals:
    ##    Min     1Q Median     3Q    Max 
    ## -13.00  -7.86  -1.81   4.64 423.14 
    ## 
    ## Coefficients:
    ##                       Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)           13.00361    0.07992  162.71   <2e-16 ***
    ## factor(curb)Y         -1.14152    0.08346  -13.68   <2e-16 ***
    ## factor(root_barrier)Y -7.55198    0.09737  -77.56   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 9.022 on 146608 degrees of freedom
    ## Multiple R-squared:  0.04069,    Adjusted R-squared:  0.04068 
    ## F-statistic:  3109 on 2 and 146608 DF,  p-value: < 2.2e-16

<!----------------------------------------------------------------------------->

## 3.2 (3 points)

Produce something relevant from your fitted model: either predictions on
Y, or a single value like a regression coefficient or a p-value.

-   Be sure to indicate in writing what you chose to produce.
-   Your code should either output a tibble (in which case you should
    indicate the column that contains the thing you’re looking for), or
    the thing you’re looking for itself.
-   Obtain your results using the `broom` package if possible. If your
    model is not compatible with the broom function you’re needing, then
    you can obtain your results by some other means, but first indicate
    which broom function is not compatible.

<!-------------------------- Start your work below ---------------------------->

Given the linear model we’ve fit, we can use the **`broom`** package to
extract useful statistics in a tidy format. For this task, let’s obtain
the regression coefficients, as well as the p-values for each
coefficient. This will help determine which variables (if any) have a
significant impact on the diameter of the trees.

    library(broom)

    # Extract coefficients, standard errors, and p-values
    model_summary <- tidy(tree_model)

    # Display the results
    model_summary

    ## # A tibble: 3 × 5
    ##   term                  estimate std.error statistic  p.value
    ##   <chr>                    <dbl>     <dbl>     <dbl>    <dbl>
    ## 1 (Intercept)              13.0     0.0799     163.  0       
    ## 2 factor(curb)Y            -1.14    0.0835     -13.7 1.46e-42
    ## 3 factor(root_barrier)Y    -7.55    0.0974     -77.6 0

<!----------------------------------------------------------------------------->

# Task 4: Reading and writing data

Get set up for this exercise by making a folder called `output` in the
top level of your project folder / repository. You’ll be saving things
there.

## 4.1 (3 points)

Take a summary table that you made from Task 1, and write it as a csv
file in your `output` folder. Use the `here::here()` function.

-   **Robustness criteria**: You should be able to move your Mini
    Project repository / project folder to some other location on your
    computer, or move this very Rmd file to another location within your
    project repository / folder, and your code should still work.
-   **Reproducibility criteria**: You should be able to delete the csv
    file, and remake it simply by knitting this Rmd file.

<!-------------------------- Start your work below ---------------------------->

    library(here)

    ## here() starts at /Users/yuefeng/courses/STAT-545

    # Define the path to the CSV file using here::here()
    #file_path <- here("courses/STAT-545", "vancouver_tree_summary.csv")

    #write.csv(vancouver_trees, file_path, row.names = FALSE)

<!----------------------------------------------------------------------------->

## 4.2 (3 points)

Write your model object from Task 3 to an R binary file (an RDS), and
load it again. Be sure to save the binary file in your `output` folder.
Use the functions `saveRDS()` and `readRDS()`.

-   The same robustness and reproducibility criteria as in 4.1 apply
    here.

<!-------------------------- Start your work below ---------------------------->

    #saveRDS(tree_model, here("courses/STAT-545", "tree_model.rds"))

    #loaded_model <- readRDS(here("courses/STAT-545", "tree_model.rds"))

<!----------------------------------------------------------------------------->

# Overall Reproducibility/Cleanliness/Coherence Checklist

Here are the criteria we’re looking for.

## Coherence (0.5 points)

The document should read sensibly from top to bottom, with no major
continuity errors.

The README file should still satisfy the criteria from the last
milestone, i.e. it has been updated to match the changes to the
repository made in this milestone.

## File and folder structure (1 points)

You should have at least three folders in the top level of your
repository: one for each milestone, and one output folder. If there are
any other folders, these are explained in the main README.

Each milestone document is contained in its respective folder, and
nowhere else.

Every level-1 folder (that is, the ones stored in the top level, like
“Milestone1” and “output”) has a `README` file, explaining in a sentence
or two what is in the folder, in plain language (it’s enough to say
something like “This folder contains the source for Milestone 1”).

## Output (1 point)

All output is recent and relevant:

-   All Rmd files have been `knit`ted to their output md files.
-   All knitted md files are viewable without errors on Github. Examples
    of errors: Missing plots, “Sorry about that, but we can’t show files
    that are this big right now” messages, error messages from broken R
    code
-   All of these output files are up-to-date – that is, they haven’t
    fallen behind after the source (Rmd) files have been updated.
-   There should be no relic output files. For example, if you were
    knitting an Rmd to html, but then changed the output to be only a
    markdown file, then the html file is a relic and should be deleted.

Our recommendation: delete all output files, and re-knit each
milestone’s Rmd file, so that everything is up to date and relevant.

## Tagged release (0.5 point)

You’ve tagged a release for Milestone 2.

### Attribution

Thanks to Victor Yuan for mostly putting this together.
