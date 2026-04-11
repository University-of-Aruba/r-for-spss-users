---
title: "Your First R Session"
teaching: 60
exercises: 30
---

:::::::::::::::::::::::::::::::::::::: questions

- How does RStudio compare to the SPSS interface?
- How do I import data, including SPSS `.sav` files?
- How do I get descriptive statistics and frequency tables in R?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Navigate the RStudio interface and identify the equivalent of SPSS panels
- Import CSV and SPSS `.sav` files into R
- Run basic descriptive statistics and frequency tables
- Inspect variables and data structure

::::::::::::::::::::::::::::::::::::::::::::::::

![The iguana is optional. The coconut water is not.](fig/scene_2.jpg){alt="Cartoon of a researcher at a Caribbean beach bar opening his laptop to the R console, with an iguana watching from the counter"}

## RStudio orientation

When you open RStudio for the first time, you see four panes. If you have used
SPSS before, each one has a rough equivalent:

| RStudio pane | Location | SPSS equivalent | What it does |
|---|---|---|---|
| **Source Editor** | Top-left | Syntax Editor | Where you write and save your code (scripts) |
| **Console** | Bottom-left | Output Viewer | Where R runs commands and prints results |
| **Environment** | Top-right | Data View header | Lists all objects (datasets, values) currently in memory |
| **Files / Plots / Help** | Bottom-right | *(no equivalent)* | File browser, plot preview, and built-in documentation |

The key difference from SPSS: in SPSS, you usually have *one* dataset open at
a time and interact through menus. In RStudio, you write instructions in the
Source Editor (top-left), send them to the Console (bottom-left), and the
results appear either in the Console or the Plots pane.

::::::::::::::::::::::::::::::::::::: callout

## The Source Editor is your new best friend

In SPSS, many users never open the Syntax Editor — they click menus instead.
In R, the Source Editor *is* how you work. Think of it as a recipe: you write
the steps once, and you (or anyone else) can re-run them at any time.

Save your scripts with the `.R` extension. You will thank yourself later.

::::::::::::::::::::::::::::::::::::::::::::::::

## Objects and assignment

In SPSS, when you compute a new variable, it appears as a column in your
dataset. In R, everything you create is stored as a named **object**.

You create objects with the **assignment operator** `<-` (a less-than sign
followed by a hyphen). Read it as "gets" or "is assigned".


``` r
# Store a number
population <- 106739

# Store text (called a "character string" in R)
island <- "Aruba"

# Store the result of a calculation
density <- population / 180  # Aruba is about 180 km²
```

To see the value of an object, type its name and run it:


``` r
population
```

``` output
[1] 106739
```

``` r
island
```

``` output
[1] "Aruba"
```

``` r
density
```

``` output
[1] 592.9944
```

::::::::::::::::::::::::::::::::::::: callout

## Why `<-` and not `=`?

You will see some people use `=` for assignment, and it works in most cases.
However, the R community convention is `<-`. It makes your code easier to read
because `=` is also used inside function arguments (as you will see shortly).

In RStudio, the keyboard shortcut **Alt + -** (Alt and the minus key) types
`<-` for you automatically.

::::::::::::::::::::::::::::::::::::::::::::::::

## Functions: R's version of menu clicks

In SPSS, you click **Analyze > Descriptive Statistics > Descriptives** and a
dialog box appears. In R, you call a **function** instead. A function has a
name, and you pass it **arguments** inside parentheses.


``` r
# round() is a function. 592.777 is the input, digits = 1 is an option.
round(592.777, digits = 1)
```

``` output
[1] 592.8
```


``` r
# sqrt() calculates a square root
sqrt(density)
```

``` output
[1] 24.35148
```

The pattern is always: `function_name(argument1, argument2, ...)`. This is
the R equivalent of filling in an SPSS dialog box — the function name is the
menu item, and the arguments are the fields you would fill in.

## Packages: extending R

R comes with many built-in functions, but its real power comes from
**packages** — add-on libraries written by other users. Think of them as SPSS
modules, except they are free.

There are two steps:

1. **Install** the package (once per computer, like installing an app):


``` r
install.packages("tidyverse")
```

2. **Load** the package (once per session, like opening an app):


``` r
library(tidyverse)
```

``` output
── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
✔ dplyr     1.2.0     ✔ readr     2.2.0
✔ forcats   1.0.1     ✔ stringr   1.6.0
✔ ggplot2   4.0.2     ✔ tibble    3.3.1
✔ lubridate 1.9.5     ✔ tidyr     1.3.2
✔ purrr     1.2.1     
── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
✖ dplyr::filter() masks stats::filter()
✖ dplyr::lag()    masks stats::lag()
ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors
```

::::::::::::::::::::::::::::::::::::: callout

## `install.packages()` vs `library()`

A common source of confusion for beginners:

- `install.packages("tidyverse")` — downloads and installs the package. You
  only need to do this **once** (or when you want to update). Note the
  **quotation marks**.
- `library(tidyverse)` — loads a package that is already installed so you can
  use it in your current session. You do this **every time** you start R. No
  quotation marks needed (though they work too).

Analogy: `install.packages()` is buying a book and putting it on your shelf.
`library()` is taking the book off the shelf and opening it.

::::::::::::::::::::::::::::::::::::::::::::::::

## Importing data

### CSV files with `read_csv()`

The most common data format in R is CSV (comma-separated values). The
`readr` package (loaded as part of `tidyverse`) provides `read_csv()`:


``` r
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

R prints a summary of the column types it detected. This is equivalent to
opening a CSV in SPSS via **File > Open > Data** and checking the variable
types.

### SPSS `.sav` files with `haven`

If you have existing SPSS datasets, the `haven` package reads them directly —
including variable labels and value labels:


``` r
# install.packages("haven")  # run once if needed
library(haven)
spss_data <- read_sav("path/to/your/file.sav")
```

This means you do not have to convert your SPSS files to CSV first. R reads
them as-is.

## Exploring your data

Now that we have the `visitors` dataset loaded, let us explore it. Each of the
functions below is the R equivalent of something you would do in SPSS.

### `View()` — the Data View equivalent


``` r
View(visitors)
```

This opens a spreadsheet-like viewer in RStudio, just like SPSS Data View. You
can scroll, sort columns by clicking headers, and filter. (Note the capital V.)

### `head()` — see the first few rows


``` r
head(visitors)
```

``` output
# A tibble: 6 × 9
   year quarter origin        visitors_stayover visitors_cruise avg_stay_nights
  <dbl> <chr>   <chr>                     <dbl>           <dbl>           <dbl>
1  2019 Q1      United States             72450           45200             6.8
2  2019 Q1      Netherlands               18300            1200            10.2
3  2019 Q1      Venezuela                  8200             400             5.1
4  2019 Q1      Colombia                   6100             800             4.8
5  2019 Q1      Canada                     4500            3200             7.1
6  2019 Q1      Other                      9800            5600             5.5
# ℹ 3 more variables: avg_spending_usd <dbl>, hotel_occupancy_pct <dbl>,
#   satisfaction_score <dbl>
```

This is faster than `View()` when you just want a quick look. By default it
shows 6 rows. You can change that: `head(visitors, n = 10)`.

### `str()` — the Variable View equivalent

In SPSS, you would switch to **Variable View** to see variable names, types,
and labels. In R, `str()` does the same thing:


``` r
str(visitors)
```

``` output
spc_tbl_ [120 × 9] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
 $ year               : num [1:120] 2019 2019 2019 2019 2019 ...
 $ quarter            : chr [1:120] "Q1" "Q1" "Q1" "Q1" ...
 $ origin             : chr [1:120] "United States" "Netherlands" "Venezuela" "Colombia" ...
 $ visitors_stayover  : num [1:120] 72450 18300 8200 6100 4500 ...
 $ visitors_cruise    : num [1:120] 45200 1200 400 800 3200 5600 38100 900 300 700 ...
 $ avg_stay_nights    : num [1:120] 6.8 10.2 5.1 4.8 7.1 5.5 6.5 9.8 4.9 4.6 ...
 $ avg_spending_usd   : num [1:120] 1250 980 620 710 1180 890 1220 960 600 690 ...
 $ hotel_occupancy_pct: num [1:120] 82.3 82.3 82.3 82.3 82.3 82.3 78.1 78.1 78.1 78.1 ...
 $ satisfaction_score : num [1:120] 8.1 7.9 7.5 7.7 8 7.6 8 7.8 7.4 7.6 ...
 - attr(*, "spec")=
  .. cols(
  ..   year = col_double(),
  ..   quarter = col_character(),
  ..   origin = col_character(),
  ..   visitors_stayover = col_double(),
  ..   visitors_cruise = col_double(),
  ..   avg_stay_nights = col_double(),
  ..   avg_spending_usd = col_double(),
  ..   hotel_occupancy_pct = col_double(),
  ..   satisfaction_score = col_double()
  .. )
 - attr(*, "problems")=<externalptr> 
```

This tells you: how many observations (rows), how many variables (columns),
and the type of each variable (`num` for numbers, `chr` for text).

### `glimpse()` — a tidyverse alternative to `str()`

The `glimpse()` function from `dplyr` gives similar information in a tidier
format:


``` r
glimpse(visitors)
```

``` output
Rows: 120
Columns: 9
$ year                <dbl> 2019, 2019, 2019, 2019, 2019, 2019, 2019, 2019, 20…
$ quarter             <chr> "Q1", "Q1", "Q1", "Q1", "Q1", "Q1", "Q2", "Q2", "Q…
$ origin              <chr> "United States", "Netherlands", "Venezuela", "Colo…
$ visitors_stayover   <dbl> 72450, 18300, 8200, 6100, 4500, 9800, 65200, 15400…
$ visitors_cruise     <dbl> 45200, 1200, 400, 800, 3200, 5600, 38100, 900, 300…
$ avg_stay_nights     <dbl> 6.8, 10.2, 5.1, 4.8, 7.1, 5.5, 6.5, 9.8, 4.9, 4.6,…
$ avg_spending_usd    <dbl> 1250, 980, 620, 710, 1180, 890, 1220, 960, 600, 69…
$ hotel_occupancy_pct <dbl> 82.3, 82.3, 82.3, 82.3, 82.3, 82.3, 78.1, 78.1, 78…
$ satisfaction_score  <dbl> 8.1, 7.9, 7.5, 7.7, 8.0, 7.6, 8.0, 7.8, 7.4, 7.6, …
```

### `summary()` — Descriptives in one command

In SPSS: **Analyze > Descriptive Statistics > Descriptives**. In R:


``` r
summary(visitors)
```

``` output
      year        quarter             origin          visitors_stayover
 Min.   :2019   Length:120         Length:120         Min.   :  180    
 1st Qu.:2020   Class :character   Class :character   1st Qu.: 4050    
 Median :2021   Mode  :character   Mode  :character   Median : 5900    
 Mean   :2021                                         Mean   :15948    
 3rd Qu.:2022                                         3rd Qu.:17875    
 Max.   :2023                                         Max.   :78200    
 visitors_cruise   avg_stay_nights  avg_spending_usd hotel_occupancy_pct
 Min.   :    0.0   Min.   : 3.500   Min.   : 400.0   Min.   :12.10      
 1st Qu.:  242.5   1st Qu.: 4.575   1st Qu.: 677.5   1st Qu.:70.72      
 Median : 1100.0   Median : 5.650   Median : 900.0   Median :77.95      
 Mean   : 6624.8   Mean   : 6.220   Mean   : 898.2   Mean   :71.61      
 3rd Qu.: 4425.0   3rd Qu.: 6.900   3rd Qu.:1142.5   3rd Qu.:81.47      
 Max.   :48900.0   Max.   :10.700   Max.   :1310.0   Max.   :86.40      
 satisfaction_score
 Min.   :6.50      
 1st Qu.:7.30      
 Median :7.65      
 Mean   :7.63      
 3rd Qu.:8.00      
 Max.   :8.40      
```

For numeric columns, you get the minimum, maximum, mean, median, and
quartiles. For character columns, you get the length and type.

### `table()` — Frequency tables

In SPSS: **Analyze > Descriptive Statistics > Frequencies**. In R:


``` r
table(visitors$origin)
```

``` output

       Canada      Colombia   Netherlands         Other United States 
           20            20            20            20            20 
    Venezuela 
           20 
```

The `$` operator extracts a single column from a data frame. So
`visitors$origin` means "the origin column from the visitors dataset" — like
clicking on a single variable in SPSS.

You can also make two-way frequency tables:


``` r
table(visitors$year, visitors$origin)
```

``` output
      
       Canada Colombia Netherlands Other United States Venezuela
  2019      4        4           4     4             4         4
  2020      4        4           4     4             4         4
  2021      4        4           4     4             4         4
  2022      4        4           4     4             4         4
  2023      4        4           4     4             4         4
```

:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: instructor

## Pacing notes

- Spend time on the RStudio pane orientation. Have participants identify each
  pane on their own screen before moving on.
- The `<-` assignment operator trips people up. Give them a few minutes to
  practice creating objects with different names and values.
- When loading tidyverse, the startup messages can be alarming to beginners.
  Reassure them that the "Attaching packages" and "Conflicts" messages are
  normal and expected.
- For `read_csv()`, make sure everyone has the data file in the right place.
  This is the most common point of failure. Walk around and check.

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: challenge

## Challenge 1: Explore the Aruba visitors dataset

Import the Aruba visitors dataset and answer the following questions using R
functions. Write your code in the Source Editor and run each line.

1. How many rows and how many columns does the dataset have?
2. What data type is the `origin` column? What data type is `visitors_stayover`?
3. What is the mean `avg_spending_usd` across all rows?
4. How many rows are there for each origin country?

:::::::::::::::::::::::: solution

## Solution


``` r
# Load the data (if not already loaded)
library(tidyverse)
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

**Question 1:** How many rows and columns?


``` r
# Either of these works:
dim(visitors)
```

``` output
[1] 120   9
```

``` r
glimpse(visitors)
```

``` output
Rows: 120
Columns: 9
$ year                <dbl> 2019, 2019, 2019, 2019, 2019, 2019, 2019, 2019, 20…
$ quarter             <chr> "Q1", "Q1", "Q1", "Q1", "Q1", "Q1", "Q2", "Q2", "Q…
$ origin              <chr> "United States", "Netherlands", "Venezuela", "Colo…
$ visitors_stayover   <dbl> 72450, 18300, 8200, 6100, 4500, 9800, 65200, 15400…
$ visitors_cruise     <dbl> 45200, 1200, 400, 800, 3200, 5600, 38100, 900, 300…
$ avg_stay_nights     <dbl> 6.8, 10.2, 5.1, 4.8, 7.1, 5.5, 6.5, 9.8, 4.9, 4.6,…
$ avg_spending_usd    <dbl> 1250, 980, 620, 710, 1180, 890, 1220, 960, 600, 69…
$ hotel_occupancy_pct <dbl> 82.3, 82.3, 82.3, 82.3, 82.3, 82.3, 78.1, 78.1, 78…
$ satisfaction_score  <dbl> 8.1, 7.9, 7.5, 7.7, 8.0, 7.6, 8.0, 7.8, 7.4, 7.6, …
```

The dataset has 120 rows and 9 columns (5 years x 4 quarters x 6 origin
countries = 120 rows).

**Question 2:** Data types?


``` r
str(visitors)
```

``` output
spc_tbl_ [120 × 9] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
 $ year               : num [1:120] 2019 2019 2019 2019 2019 ...
 $ quarter            : chr [1:120] "Q1" "Q1" "Q1" "Q1" ...
 $ origin             : chr [1:120] "United States" "Netherlands" "Venezuela" "Colombia" ...
 $ visitors_stayover  : num [1:120] 72450 18300 8200 6100 4500 ...
 $ visitors_cruise    : num [1:120] 45200 1200 400 800 3200 5600 38100 900 300 700 ...
 $ avg_stay_nights    : num [1:120] 6.8 10.2 5.1 4.8 7.1 5.5 6.5 9.8 4.9 4.6 ...
 $ avg_spending_usd   : num [1:120] 1250 980 620 710 1180 890 1220 960 600 690 ...
 $ hotel_occupancy_pct: num [1:120] 82.3 82.3 82.3 82.3 82.3 82.3 78.1 78.1 78.1 78.1 ...
 $ satisfaction_score : num [1:120] 8.1 7.9 7.5 7.7 8 7.6 8 7.8 7.4 7.6 ...
 - attr(*, "spec")=
  .. cols(
  ..   year = col_double(),
  ..   quarter = col_character(),
  ..   origin = col_character(),
  ..   visitors_stayover = col_double(),
  ..   visitors_cruise = col_double(),
  ..   avg_stay_nights = col_double(),
  ..   avg_spending_usd = col_double(),
  ..   hotel_occupancy_pct = col_double(),
  ..   satisfaction_score = col_double()
  .. )
 - attr(*, "problems")=<externalptr> 
```

`origin` is character (`chr`), `visitors_stayover` is numeric (`num`).

**Question 3:** Mean average spending?


``` r
summary(visitors$avg_spending_usd)
```

``` output
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
  400.0   677.5   900.0   898.2  1142.5  1310.0 
```

The mean `avg_spending_usd` is shown in the summary output. You can also get
just the mean with:


``` r
mean(visitors$avg_spending_usd)
```

``` output
[1] 898.1667
```

**Question 4:** Rows per origin country?


``` r
table(visitors$origin)
```

``` output

       Canada      Colombia   Netherlands         Other United States 
           20            20            20            20            20 
    Venezuela 
           20 
```

Each origin country has 20 rows (4 quarters x 5 years).

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: challenge

## Challenge 2: Practice with objects and functions

1. Create an object called `my_island` that stores the text `"Aruba"`.
2. Create an object called `area_km2` that stores the value `180`.
3. Use the `nchar()` function to count the number of characters in `my_island`.
4. Use `round()` to round the mean of `avg_spending_usd` to the nearest whole
   number. (Hint: you can put one function inside another.)

:::::::::::::::::::::::: solution

## Solution


``` r
# 1 and 2: Create objects
my_island <- "Aruba"
area_km2 <- 180

# 3: Count characters
nchar(my_island)
```

``` output
[1] 5
```

``` r
# 4: Round the mean spending
round(mean(visitors$avg_spending_usd), digits = 0)
```

``` output
[1] 898
```

Nesting functions (putting one inside another) is common in R. R evaluates
from the inside out: first it calculates `mean(visitors$avg_spending_usd)`,
then it passes that result to `round()`.

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

## Summary

You have now completed your first hands-on R session. You can:

- Find your way around RStudio
- Create objects and use functions
- Install and load packages
- Import a CSV file
- Inspect your data with `View()`, `head()`, `str()`, `glimpse()`, `summary()`,
  and `table()`

In SPSS terms, you have learned the equivalent of opening a dataset, switching
between Data View and Variable View, and running Descriptives and Frequencies.
The difference is that everything you did is saved in a script that you can
re-run at any time.

::::::::::::::::::::::::::::::::::::: keypoints

- RStudio is your workspace — it combines a script editor, console, and data viewer
- `haven::read_sav()` imports SPSS files directly, preserving labels
- `summary()`, `table()`, and `str()` replace the Descriptives and Frequencies menus in SPSS

::::::::::::::::::::::::::::::::::::::::::::::::
