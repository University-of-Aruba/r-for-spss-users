---
title: "Data Manipulation"
teaching: 60
exercises: 30
---

:::::::::::::::::::::::::::::::::::::: questions

- How do I filter, sort, and recode data in R the way I do in SPSS?
- What is the tidyverse and why does it matter?
- How do I create new variables from existing ones?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Filter rows, select columns, and sort data using dplyr
- Create new variables and recode existing ones
- Chain operations together using the pipe operator
- Recognize the SPSS menu equivalent for each operation

::::::::::::::::::::::::::::::::::::::::::::::::

![You can't cook without ingredients. You can't wrangle without verbs.](fig/scene_3.jpg){alt="Cartoon of a researcher as a Caribbean chef with jars labeled filter(), select(), and mutate(), cooking a pot of tidy data"}

## The tidyverse approach

In SPSS, you manipulate data through menus: **Data > Select Cases**, **Data >
Sort Cases**, **Transform > Compute Variable**, and so on. In R, the
`dplyr` package gives you a set of **verbs** — functions with plain-English
names that do exactly what they say.

The `dplyr` package is part of the **tidyverse**, which you already loaded in
the previous episode. If you are starting a fresh R session, load it now:


``` r
library(tidyverse)
```

``` output
── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
✔ dplyr     1.2.1     ✔ readr     2.2.0
✔ forcats   1.0.1     ✔ stringr   1.6.0
✔ ggplot2   4.0.2     ✔ tibble    3.3.1
✔ lubridate 1.9.5     ✔ tidyr     1.3.2
✔ purrr     1.2.2     
── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
✖ dplyr::filter() masks stats::filter()
✖ dplyr::lag()    masks stats::lag()
ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors
```

``` r
# Also load our dataset
visitors <- read_csv("data/aruba_visitors.csv")
```

``` output
Rows: 120 Columns: 9
── Column specification ────────────────────────────────────────────────────────
Delimiter: ","
chr (2): quarter, origin
dbl (7): year, visitors_stayover, visitors_cruise, avg_stay_nights, avg_spen...

ℹ Use `spec()` to retrieve the full column specification for this data.
ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

::::::::::::::::::::::::::::::::::::: callout

## What is a dependency?

A package in R is a bundle of code that someone else wrote so you do not have to. `tidyverse`, for example, is actually a collection of packages that work together for data manipulation and visualisation. When you use `library(tidyverse)`, R loads those packages into your session so their functions become available.

A dependency is a package that another package needs in order to work. `tidyverse` depends on `dplyr`, `ggplot2`, `readr`, and several others. When you run `install.packages("tidyverse")`, R automatically installs everything it depends on too. You do not have to manage the chain manually.

Two things this means in practice. First, the first time you install a package it can take a minute or two because R is pulling down the dependency chain. That is normal. Second, when you share your script with a colleague and they get an error like `there is no package called 'dplyr'`, the fix is almost always `install.packages("tidyverse")`, not `install.packages("dplyr")`, because the dependency lives inside the larger package.

We come back to this in Episode 6 (reproducible reporting), where recording which packages your script needs is part of making sure it still runs six months from now.

::::::::::::::::::::::::::::::::::::::::::::::::

Here is the key idea: every SPSS menu operation you use for data manipulation
has a dplyr verb equivalent.

| SPSS menu path | dplyr verb | What it does |
|---|---|---|
| Data > Select Cases | `filter()` | Keep rows that match a condition |
| *(selecting columns in Variable View)* | `select()` | Keep or drop columns |
| Transform > Compute Variable | `mutate()` | Create or modify a column |
| Transform > Recode into Different Variables | `case_when()` | Assign values based on conditions |
| Data > Sort Cases | `arrange()` | Sort rows |
| Data > Split File + Aggregate | `group_by()` + `summarise()` | Calculate summaries by group |

Let us work through each one.

## `filter()` — Select Cases

In SPSS, you would go to **Data > Select Cases**, click "If condition is
satisfied", and type a condition like `origin = "United States"`. In R:


``` r
us_visitors <- filter(visitors, origin == "United States")
us_visitors
```

``` output
# A tibble: 20 × 9
    year quarter origin        visitors_stayover visitors_cruise avg_stay_nights
   <dbl> <chr>   <chr>                     <dbl>           <dbl>           <dbl>
 1  2019 Q1      United States             72450           45200             6.8
 2  2019 Q2      United States             65200           38100             6.5
 3  2019 Q3      United States             58900           32400             6.2
 4  2019 Q4      United States             69800           42800             6.7
 5  2020 Q1      United States             68100           40200             6.6
 6  2020 Q2      United States              4200               0             5.8
 7  2020 Q3      United States             18500               0             6  
 8  2020 Q4      United States             42100            8200             6.3
 9  2021 Q1      United States             48200           12400             6.4
10  2021 Q2      United States             52800           18600             6.5
11  2021 Q3      United States             55400           25200             6.3
12  2021 Q4      United States             64200           38500             6.6
13  2022 Q1      United States             74800           46800             6.9
14  2022 Q2      United States             67500           39200             6.6
15  2022 Q3      United States             61200           34600             6.3
16  2022 Q4      United States             72100           44500             6.8
17  2023 Q1      United States             78200           48900             7  
18  2023 Q2      United States             70100           41200             6.7
19  2023 Q3      United States             63500           36200             6.4
20  2023 Q4      United States             75600           46100             6.9
# ℹ 3 more variables: avg_spending_usd <dbl>, hotel_occupancy_pct <dbl>,
#   satisfaction_score <dbl>
```

Notice the **double equals sign** `==`. This is how R tests equality. A single
`=` is for assigning values to function arguments (like `digits = 1`); a
double `==` asks "is this equal to?".

You can combine conditions:


``` r
# US visitors in 2023 only
us_2023 <- filter(visitors, origin == "United States", year == 2023)
us_2023
```

``` output
# A tibble: 4 × 9
   year quarter origin        visitors_stayover visitors_cruise avg_stay_nights
  <dbl> <chr>   <chr>                     <dbl>           <dbl>           <dbl>
1  2023 Q1      United States             78200           48900             7  
2  2023 Q2      United States             70100           41200             6.7
3  2023 Q3      United States             63500           36200             6.4
4  2023 Q4      United States             75600           46100             6.9
# ℹ 3 more variables: avg_spending_usd <dbl>, hotel_occupancy_pct <dbl>,
#   satisfaction_score <dbl>
```


``` r
# Rows where stayover visitors exceeded 50,000
big_quarters <- filter(visitors, visitors_stayover > 50000)
big_quarters
```

``` output
# A tibble: 16 × 9
    year quarter origin        visitors_stayover visitors_cruise avg_stay_nights
   <dbl> <chr>   <chr>                     <dbl>           <dbl>           <dbl>
 1  2019 Q1      United States             72450           45200             6.8
 2  2019 Q2      United States             65200           38100             6.5
 3  2019 Q3      United States             58900           32400             6.2
 4  2019 Q4      United States             69800           42800             6.7
 5  2020 Q1      United States             68100           40200             6.6
 6  2021 Q2      United States             52800           18600             6.5
 7  2021 Q3      United States             55400           25200             6.3
 8  2021 Q4      United States             64200           38500             6.6
 9  2022 Q1      United States             74800           46800             6.9
10  2022 Q2      United States             67500           39200             6.6
11  2022 Q3      United States             61200           34600             6.3
12  2022 Q4      United States             72100           44500             6.8
13  2023 Q1      United States             78200           48900             7  
14  2023 Q2      United States             70100           41200             6.7
15  2023 Q3      United States             63500           36200             6.4
16  2023 Q4      United States             75600           46100             6.9
# ℹ 3 more variables: avg_spending_usd <dbl>, hotel_occupancy_pct <dbl>,
#   satisfaction_score <dbl>
```

::::::::::::::::::::::::::::::::::::: callout

## Common comparison operators

| Operator | Meaning | Example |
|---|---|---|
| `==` | equal to | `origin == "Canada"` |
| `!=` | not equal to | `origin != "Other"` |
| `>` | greater than | `visitors_stayover > 10000` |
| `<` | less than | `avg_stay_nights < 5` |
| `>=` | greater than or equal to | `year >= 2021` |
| `<=` | less than or equal to | `satisfaction_score <= 7.5` |
| `%in%` | matches one of several values | `origin %in% c("United States", "Canada")` |

::::::::::::::::::::::::::::::::::::::::::::::::

## `select()` — Keep or drop columns

Sometimes your dataset has more columns than you need. In SPSS, you might
delete variables or simply ignore them. In R, `select()` lets you keep only the
columns you want:


``` r
# Keep only year, quarter, origin, and stayover visitors
slim <- select(visitors, year, quarter, origin, visitors_stayover)
head(slim)
```

``` output
# A tibble: 6 × 4
   year quarter origin        visitors_stayover
  <dbl> <chr>   <chr>                     <dbl>
1  2019 Q1      United States             72450
2  2019 Q1      Netherlands               18300
3  2019 Q1      Venezuela                  8200
4  2019 Q1      Colombia                   6100
5  2019 Q1      Canada                     4500
6  2019 Q1      Other                      9800
```

You can also drop columns by putting a minus sign in front:


``` r
# Drop the satisfaction score column
no_satisfaction <- select(visitors, -satisfaction_score)
head(no_satisfaction)
```

``` output
# A tibble: 6 × 8
   year quarter origin        visitors_stayover visitors_cruise avg_stay_nights
  <dbl> <chr>   <chr>                     <dbl>           <dbl>           <dbl>
1  2019 Q1      United States             72450           45200             6.8
2  2019 Q1      Netherlands               18300            1200            10.2
3  2019 Q1      Venezuela                  8200             400             5.1
4  2019 Q1      Colombia                   6100             800             4.8
5  2019 Q1      Canada                     4500            3200             7.1
6  2019 Q1      Other                      9800            5600             5.5
# ℹ 2 more variables: avg_spending_usd <dbl>, hotel_occupancy_pct <dbl>
```

## `mutate()` — Compute Variable

In SPSS: **Transform > Compute Variable**. You would type a target variable
name, then an expression. In R, `mutate()` creates a new column (or modifies
an existing one):


``` r
visitors <- mutate(visitors,
  total_visitors = visitors_stayover + visitors_cruise
)
head(select(visitors, year, quarter, origin, visitors_stayover, visitors_cruise, total_visitors))
```

``` output
# A tibble: 6 × 6
   year quarter origin        visitors_stayover visitors_cruise total_visitors
  <dbl> <chr>   <chr>                     <dbl>           <dbl>          <dbl>
1  2019 Q1      United States             72450           45200         117650
2  2019 Q1      Netherlands               18300            1200          19500
3  2019 Q1      Venezuela                  8200             400           8600
4  2019 Q1      Colombia                   6100             800           6900
5  2019 Q1      Canada                     4500            3200           7700
6  2019 Q1      Other                      9800            5600          15400
```

You can create multiple columns at once:


``` r
visitors <- mutate(visitors,
  spending_per_night = avg_spending_usd / avg_stay_nights,
  stayover_pct = visitors_stayover / total_visitors * 100
)
```

## `case_when()` — Recode into Different Variables

In SPSS: **Transform > Recode into Different Variables**, where you map old
values to new values. In R, you use `case_when()` inside `mutate()`:


``` r
visitors <- mutate(visitors,
  region = case_when(
    origin == "United States" ~ "North America",
    origin == "Canada"        ~ "North America",
    origin == "Netherlands"   ~ "Europe",
    origin == "Venezuela"     ~ "South America",
    origin == "Colombia"      ~ "South America",
    .default                  = "Other"
  )
)

table(visitors$region)
```

``` output

       Europe North America         Other South America 
           20            40            20            40 
```

The syntax is: `condition ~ value_to_assign`. The `.default` line catches
everything that did not match a previous condition — like the "Else" box in
SPSS Recode.

## `arrange()` — Sort Cases

In SPSS: **Data > Sort Cases**. In R:


``` r
# Sort by stayover visitors, ascending (default)
arrange(visitors, visitors_stayover)
```

``` output
# A tibble: 120 × 13
    year quarter origin      visitors_stayover visitors_cruise avg_stay_nights
   <dbl> <chr>   <chr>                   <dbl>           <dbl>           <dbl>
 1  2020 Q2      Canada                    180               0             5.2
 2  2020 Q2      Venezuela                 200               0             3.5
 3  2020 Q2      Colombia                  300               0             3.8
 4  2020 Q2      Other                     400               0             4.1
 5  2020 Q3      Venezuela                 800               0             3.9
 6  2020 Q2      Netherlands              1100               0             8.5
 7  2020 Q3      Canada                   1100               0             5.8
 8  2020 Q3      Colombia                 1200               0             4  
 9  2020 Q4      Venezuela                1800               0             4.1
10  2021 Q1      Venezuela                2100              50             4  
# ℹ 110 more rows
# ℹ 7 more variables: avg_spending_usd <dbl>, hotel_occupancy_pct <dbl>,
#   satisfaction_score <dbl>, total_visitors <dbl>, spending_per_night <dbl>,
#   stayover_pct <dbl>, region <chr>
```


``` r
# Sort descending — use desc()
arrange(visitors, desc(visitors_stayover))
```

``` output
# A tibble: 120 × 13
    year quarter origin        visitors_stayover visitors_cruise avg_stay_nights
   <dbl> <chr>   <chr>                     <dbl>           <dbl>           <dbl>
 1  2023 Q1      United States             78200           48900             7  
 2  2023 Q4      United States             75600           46100             6.9
 3  2022 Q1      United States             74800           46800             6.9
 4  2019 Q1      United States             72450           45200             6.8
 5  2022 Q4      United States             72100           44500             6.8
 6  2023 Q2      United States             70100           41200             6.7
 7  2019 Q4      United States             69800           42800             6.7
 8  2020 Q1      United States             68100           40200             6.6
 9  2022 Q2      United States             67500           39200             6.6
10  2019 Q2      United States             65200           38100             6.5
# ℹ 110 more rows
# ℹ 7 more variables: avg_spending_usd <dbl>, hotel_occupancy_pct <dbl>,
#   satisfaction_score <dbl>, total_visitors <dbl>, spending_per_night <dbl>,
#   stayover_pct <dbl>, region <chr>
```


``` r
# Sort by multiple columns: year first, then by stayover visitors descending
arrange(visitors, year, desc(visitors_stayover))
```

``` output
# A tibble: 120 × 13
    year quarter origin        visitors_stayover visitors_cruise avg_stay_nights
   <dbl> <chr>   <chr>                     <dbl>           <dbl>           <dbl>
 1  2019 Q1      United States             72450           45200             6.8
 2  2019 Q4      United States             69800           42800             6.7
 3  2019 Q2      United States             65200           38100             6.5
 4  2019 Q3      United States             58900           32400             6.2
 5  2019 Q3      Netherlands               21200             800            10.5
 6  2019 Q4      Netherlands               19600            1100            10.4
 7  2019 Q1      Netherlands               18300            1200            10.2
 8  2019 Q2      Netherlands               15400             900             9.8
 9  2019 Q1      Other                      9800            5600             5.5
10  2019 Q4      Other                      8900            5100             5.4
# ℹ 110 more rows
# ℹ 7 more variables: avg_spending_usd <dbl>, hotel_occupancy_pct <dbl>,
#   satisfaction_score <dbl>, total_visitors <dbl>, spending_per_night <dbl>,
#   stayover_pct <dbl>, region <chr>
```

## `group_by()` + `summarise()` — Split File and Aggregate

This is one of the most powerful combinations in dplyr, and it replaces two
SPSS operations at once:

- **Data > Split File** (which tells SPSS to run analyses separately for each
  group)
- **Data > Aggregate** (which calculates summary statistics by group)


``` r
# Average stayover visitors per year
yearly_summary <- visitors |>
  group_by(year) |>
  summarise(
    mean_stayover = mean(visitors_stayover),
    total_stayover = sum(visitors_stayover)
  )
yearly_summary
```

``` output
# A tibble: 5 × 3
   year mean_stayover total_stayover
  <dbl>         <dbl>          <dbl>
1  2019        18360.         440650
2  2020         8687.         208480
3  2021        14883.         357200
4  2022        18488.         443700
5  2023        19321.         463700
```

Wait — what is that `|>` symbol? That is the **pipe operator**, and it
deserves its own section.

## The pipe operator `|>`

The pipe `|>` is one of the most important ideas in modern R. Read it as
**"and then"**. It takes the result of the expression on the left and passes
it as the first argument to the function on the right.

Without the pipe, you would write:


``` r
# Nested style (hard to read)
summarise(group_by(filter(visitors, origin == "United States"), year), mean_spend = mean(avg_spending_usd))
```

That is like reading a sentence from the inside out. With the pipe, the same
code becomes:


``` r
visitors |>
  filter(origin == "United States") |>
  group_by(year) |>
  summarise(mean_spend = mean(avg_spending_usd))
```

``` output
# A tibble: 5 × 2
   year mean_spend
  <dbl>      <dbl>
1  2019      1225 
2  2020      1170 
3  2021      1215 
4  2022      1252.
5  2023      1275 
```

Read this as: "Take `visitors`, **and then** filter to US rows, **and then**
group by year, **and then** summarise mean spending."

The pipe makes your code read from top to bottom, like a recipe. Each line is
one step.

::::::::::::::::::::::::::::::::::::: callout

## `|>` vs `%>%`

You may see `%>%` in older R code and tutorials. This is the original pipe
operator from the `magrittr` package. The native pipe `|>` was added to base R
in version 4.1 (2021) and works without loading any packages. They behave
almost identically. We use `|>` in this course because it requires no extra
dependencies.

::::::::::::::::::::::::::::::::::::::::::::::::

### Building up a pipeline step by step

A good workflow is to build your pipeline one step at a time, checking the
result after each line. Let us work through an example:


``` r
# Step 1: Start with the data
visitors |>
  filter(year >= 2022)
```

``` output
# A tibble: 48 × 13
    year quarter origin        visitors_stayover visitors_cruise avg_stay_nights
   <dbl> <chr>   <chr>                     <dbl>           <dbl>           <dbl>
 1  2022 Q1      United States             74800           46800             6.9
 2  2022 Q1      Netherlands               19100            1300            10.3
 3  2022 Q1      Venezuela                  4800             200             4.4
 4  2022 Q1      Colombia                   5900             750             4.7
 5  2022 Q1      Canada                     4600            3300             7.2
 6  2022 Q1      Other                     10200            5800             5.6
 7  2022 Q2      United States             67500           39200             6.6
 8  2022 Q2      Netherlands               16200            1000            10  
 9  2022 Q2      Venezuela                  4200             150             4.3
10  2022 Q2      Colombia                   5600             650             4.6
# ℹ 38 more rows
# ℹ 7 more variables: avg_spending_usd <dbl>, hotel_occupancy_pct <dbl>,
#   satisfaction_score <dbl>, total_visitors <dbl>, spending_per_night <dbl>,
#   stayover_pct <dbl>, region <chr>
```


``` r
# Step 2: Add a column selection
visitors |>
  filter(year >= 2022) |>
  select(year, quarter, origin, visitors_stayover, avg_spending_usd)
```

``` output
# A tibble: 48 × 5
    year quarter origin        visitors_stayover avg_spending_usd
   <dbl> <chr>   <chr>                     <dbl>            <dbl>
 1  2022 Q1      United States             74800             1280
 2  2022 Q1      Netherlands               19100             1000
 3  2022 Q1      Venezuela                  4800              570
 4  2022 Q1      Colombia                   5900              700
 5  2022 Q1      Canada                     4600             1200
 6  2022 Q1      Other                     10200              900
 7  2022 Q2      United States             67500             1250
 8  2022 Q2      Netherlands               16200              980
 9  2022 Q2      Venezuela                  4200              550
10  2022 Q2      Colombia                   5600              690
# ℹ 38 more rows
```


``` r
# Step 3: Group and summarise
visitors |>
  filter(year >= 2022) |>
  group_by(origin) |>
  summarise(
    mean_stayover = mean(visitors_stayover),
    mean_spending = mean(avg_spending_usd)
  ) |>
  arrange(desc(mean_stayover))
```

``` output
# A tibble: 6 × 3
  origin        mean_stayover mean_spending
  <chr>                 <dbl>         <dbl>
1 United States        70375          1264.
2 Netherlands          20038.         1011.
3 Other                 9275           888.
4 Colombia              5600           696.
5 Venezuela             4250           552.
6 Canada                3888.         1176.
```

This final pipeline reads: "Take visitors, keep only 2022 and later, group by
origin, calculate mean stayover visitors and mean spending, then sort by mean
stayover visitors in descending order."

:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: instructor

## Teaching tips

- Write the pipe `|>` on the whiteboard and say "and then" out loud every time
  you use it. This mental model sticks.
- Build pipelines live, one step at a time. Run after each added line so
  participants can see how the output changes.
- The most common beginner mistake is putting `|>` at the start of a line
  instead of at the end of the previous line. Emphasize: the pipe goes at the
  **end** of the line, so R knows the expression continues.
- Compare nested function calls to piped code side by side. The readability
  advantage sells itself.

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: challenge

## Challenge 1: US visitors analysis

Using the `visitors` dataset and the pipe operator, write a pipeline that:

1. Filters to only United States visitors
2. Creates a new column called `total_visitors` that adds `visitors_stayover`
   and `visitors_cruise`
3. Groups by `year`
4. Calculates the total (sum) of `total_visitors` for each year

Save the result to an object called `us_yearly` and print it. Which year had
the fewest total US visitors? Why might that be?

:::::::::::::::::::::::: solution

## Solution


``` r
us_yearly <- visitors |>
  filter(origin == "United States") |>
  mutate(total_visitors = visitors_stayover + visitors_cruise) |>
  group_by(year) |>
  summarise(total = sum(total_visitors))

us_yearly
```

``` output
# A tibble: 5 × 2
   year  total
  <dbl>  <dbl>
1  2019 424850
2  2020 181300
3  2021 315300
4  2022 440700
5  2023 459800
```

2020 had by far the fewest US visitors, due to the COVID-19 pandemic and
associated travel restrictions. You can see the recovery in subsequent years.

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: challenge

## Challenge 2: Top spending origins

Write a pipeline that finds the average `avg_spending_usd` for each origin
country across the entire dataset, then sorts the result from highest to
lowest. Which origin country has the highest average spending?

:::::::::::::::::::::::: solution

## Solution


``` r
visitors |>
  group_by(origin) |>
  summarise(mean_spending = mean(avg_spending_usd)) |>
  arrange(desc(mean_spending))
```

``` output
# A tibble: 6 × 2
  origin        mean_spending
  <chr>                 <dbl>
1 United States         1228.
2 Canada                1139 
3 Netherlands            978.
4 Other                  850 
5 Colombia               654 
6 Venezuela              540 
```

The United States has the highest average spending per visitor, followed by
Canada. This makes sense given the typical length of stay and the types of
tourism activities associated with visitors from these markets.

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: challenge

## Challenge 3: Regional summary

Using the `region` column we created earlier with `case_when()`, write a
pipeline that calculates the total `visitors_stayover` and mean
`satisfaction_score` for each region and each year. Sort by year and then by
total stayover visitors descending.

Hint: you will need to `group_by()` two columns.

:::::::::::::::::::::::: solution

## Solution


``` r
visitors |>
  group_by(region, year) |>
  summarise(
    total_stayover = sum(visitors_stayover),
    mean_satisfaction = mean(satisfaction_score),
    .groups = "drop"
  ) |>
  arrange(year, desc(total_stayover))
```

``` output
# A tibble: 20 × 4
   region         year total_stayover mean_satisfaction
   <chr>         <dbl>          <dbl>             <dbl>
 1 North America  2019         280950              8   
 2 Europe         2019          74500              7.92
 3 South America  2019          50500              7.45
 4 Other          2019          34700              7.5 
 5 North America  2020         141180              7.56
 6 Europe         2020          35500              7.48
 7 Other          2020          16600              7.2 
 8 South America  2020          15200              6.98
 9 North America  2021         233500              7.88
10 Europe         2021          65600              7.82
11 South America  2021          29800              7.15
12 Other          2021          28300              7.4 
13 North America  2022         290800              8.1 
14 Europe         2022          78100              8.02
15 South America  2022          38500              7.34
16 Other          2022          36300              7.6 
17 North America  2023         303300              8.19
18 Europe         2023          82200              8.12
19 South America  2023          40300              7.44
20 Other          2023          37900              7.68
```

The `.groups = "drop"` argument tells `summarise()` to remove the grouping
after calculation. Without it, the result would still be grouped by `region`,
which can cause unexpected behaviour in later steps.

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

## Summary

You now know the six core dplyr verbs and can map each one to its SPSS
equivalent:

| You used to... | Now you write... |
|---|---|
| Data > Select Cases | `filter()` |
| Select columns in Variable View | `select()` |
| Transform > Compute Variable | `mutate()` |
| Transform > Recode | `mutate()` + `case_when()` |
| Data > Sort Cases | `arrange()` |
| Data > Split File + Aggregate | `group_by()` + `summarise()` |

And you connect them all with `|>` — "and then" — to build readable,
reproducible data pipelines.

::::::::::::::::::::::::::::::::::::: keypoints

- dplyr verbs (`filter`, `select`, `mutate`, `arrange`, `summarise`) replace SPSS menu operations
- The pipe operator `|>` chains operations together, making code readable
- `group_by()` combined with `summarise()` replaces SPSS Split File + Aggregate

::::::::::::::::::::::::::::::::::::::::::::::::
