---
title: "The Case for Switching"
teaching: 45
exercises: 0
---

:::::::::::::::::::::::::::::::::::::: questions

- Why should I switch from SPSS to R?
- What can R do that SPSS cannot?
- How much does SPSS actually cost compared to R?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Describe the practical advantages of R over SPSS for research
- See live examples of R capabilities that go beyond SPSS
- Understand the cost and reproducibility arguments for switching

::::::::::::::::::::::::::::::::::::::::::::::::

![A researcher stands at a crossroads on a sun-drenched Caribbean road. The cracked path to SPSS fades into scrubland, while a smooth paved road to R leads toward the coast and a wind-bent divi-divi tree.](fig/scene_1.jpg){alt="Cartoon of a researcher choosing between a faded SPSS path and a vibrant R path at a Caribbean crossroads"}

## Introduction

This episode is a motivational opening. You will **not** write any code yourself
yet — sit back and watch the instructor demonstrate what R can do. By the end,
you should have a clear picture of *why* learning R is worth the investment of
your time.

### What you will see

The instructor will demonstrate four things that are impossible or impractical
in SPSS:

1. **Pulling live data from the World Bank** for Aruba, Curacao, and Sint
   Maarten — directly from R, no browser required.
2. **Creating a publication-quality chart** in under 10 lines of code.
3. **A reproducible report** that updates automatically when new data arrives.
4. **An interactive dashboard** built entirely in R.

If any of those sound appealing, you are in the right place.

## The cost argument

Let us start with the most concrete reason. SPSS is expensive — especially for
small island institutions that pay per seat.

| | **SPSS Standard** | **R + RStudio** |
|---|---|---|
| License type | Annual subscription | Free, open-source |
| Cost per user per year | USD 1,170 – 5,730 (varies by tier) | USD 0 |
| 5-year cost for 5 users | USD 29,250 – 143,250 | USD 0 |
| Runs on | Windows, Mac | Windows, Mac, Linux, cloud |
| Updates | Paid upgrades | Continuous, free |

For a university department in the Dutch Caribbean with three SPSS licenses,
that is easily AWG 10,000+ per year that could be redirected to research
funding, student assistants, or conference travel.

::::::::::::::::::::::::::::::::::::: callout

## "But my institution already pays for SPSS"

That is true today. But institutional budgets change, and when you graduate or
change jobs, your personal SPSS license disappears. R stays with you forever —
on your laptop, on a cloud server, on a Raspberry Pi if you want. Your scripts
will still run in 10 years.

::::::::::::::::::::::::::::::::::::::::::::::::

## What R gives you that SPSS does not

### Reproducibility

In SPSS, a typical workflow looks like this: open a dataset, click through
menus, copy output into Word, repeat. If your supervisor asks "can you re-run
this with the updated data?", you have to remember every click.

In R, your entire analysis lives in a script. You change one line (the file
path) and re-run. Every step is documented.

### Packages

SPSS has a fixed set of procedures. R has over 20,000 add-on packages on CRAN
alone, covering everything from Bayesian statistics to text mining to
geographic mapping. If a method exists, there is probably an R package for it.

### Automation

Need to run the same analysis on 50 files? In SPSS, that means 50 times
through the menus (or learning SPSS syntax, which few people do). In R, it is
a three-line loop.

### Communication

R Markdown and Quarto let you combine narrative text, code, and output into a
single document — a PDF, a Word file, a website, or a slideshow. This lesson
itself was built with R.

### Career value

Data science job postings almost never list SPSS. R and Python dominate. Even
within academia, journals increasingly expect reproducible code alongside
submissions.

## Live demonstration

The instructor will now run a live demonstration. Watch the screen.

::::::::::::::::::::::::::::::::::::: callout

## What is happening on screen

Do not worry about understanding the code right now. The goal is to see what is
*possible*. You will learn the building blocks starting in the next episode.

::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: instructor

## Live demo script

This is the complete script to run live. **Practice this before the workshop.**
Make sure you have the `WDI`, `ggplot2`, and `scales` packages installed.

### Step 1: Pull live World Bank data

Open a new R script in RStudio and type (or paste) the following. Run it line
by line so participants can see each step.


``` r
# Install packages if needed (do this BEFORE the workshop)
# install.packages(c("WDI", "ggplot2", "scales"))

# Load packages
library(WDI)
library(ggplot2)
library(scales)

# Pull international tourism arrivals for three Dutch Caribbean islands
tourism <- WDI(
  country   = c("AW", "CW", "SX"),
  indicator  = "ST.INT.ARVL",
  start      = 2010,
  end        = 2023
)

# Quick look at what we got
head(tourism)
```

Pause here. Point out: "We just downloaded World Bank data for three countries
in two lines of code. No browser, no manual download, no copy-paste."

### Step 2: Create a publication-quality chart


``` r
ggplot(tourism, aes(x = year, y = ST.INT.ARVL, colour = country)) +
  geom_line(linewidth = 1.2) +
  geom_point(size = 2) +
  scale_y_continuous(labels = label_comma()) +
  labs(
    title    = "International Tourism Arrivals",
    subtitle = "Aruba, Curacao, and Sint Maarten (2010-2023)",
    x        = NULL,
    y        = "Arrivals",
    colour   = "Country",
    caption  = "Source: World Bank (WDI)"
  ) +
  theme_minimal(base_size = 14)
```

Pause again. Key talking points:

- "This chart is ready for a journal or a policy report."
- "If the World Bank updates the data next month, I re-run this script and get
  an updated chart. No re-clicking through menus."
- "Every choice — colours, labels, layout — is documented in the code."

### Step 3: Show the contrast with SPSS

Ask the audience: "How would you do this in SPSS?"

Walk through the SPSS steps:

1. Open browser, navigate to World Bank data portal
2. Search for the indicator, select countries, download CSV
3. Open SPSS, File > Open > Data, navigate to the CSV
4. Graphs > Chart Builder > Line chart, drag variables
5. Double-click chart to edit titles, colours, fonts
6. Copy to clipboard, paste into Word

Then say: "That is about 15 minutes of clicking. In R it was 10 lines of code
that you can re-run in 3 seconds."

### Backup plan

If the internet is unavailable (common in workshop venues), have a saved
version of the `tourism` data frame as a CSV. Load it with:


``` r
tourism <- read.csv("backup_tourism_data.csv")
```

Then proceed with the ggplot2 code as normal.

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

## Summary

You have now seen R:

- **Pull live data** from the internet with a single function call
- **Create a publication-ready chart** in 10 lines of code
- Do both of these things in a way that is **fully reproducible**

Starting in the next episode, you will learn to do these things yourself — one
step at a time.

::::::::::::::::::::::::::::::::::::: keypoints

- R is free, open-source, and runs on any operating system
- R scripts make your analysis fully reproducible
- R can pull data from APIs, create interactive visualizations, and automate reports — things SPSS cannot do
- Switching builds on your existing statistical knowledge, not replaces it

::::::::::::::::::::::::::::::::::::::::::::::::
