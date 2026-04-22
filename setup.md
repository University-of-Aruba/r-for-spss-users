---
title: Setup
---

You need to install R and RStudio **before the first session on April 22**.
Both are free. Follow the instructions below for your operating system.

::::::::::::::::::::::::::::::::::::::: callout

### Using a work-issued laptop? Check with IT first

Many universities and employers lock their laptops so that users cannot install
software themselves. If your laptop was issued by an institution, check with
your IT department before following the steps below, otherwise the installer
will simply fail.

**University of Aruba laptops** require a ticket through TopDesk. When you
submit the ticket, explicitly ask IT to install **both R and RStudio**. Asking
for only one of them is a common cause of a half-working setup that wastes
course time.

Give IT at least a week to process the request so your laptop is ready before
the first session.

:::::::::::::::::::::::::::::::::::::::::::::::::::

## Pre-workshop installation clinic

We will not spend course time on installation troubleshooting. To make sure
everyone starts ready to go, there is an optional drop-in session before the
course:

**When:** Thursday, April 16, 2026, 9:00 -- 12:00
**Where:** University of Aruba Research Center
**What:** Bring your laptop. We help you install R and RStudio, verify
everything works, and install the required packages. Walk in, walk out.

If you cannot attend the clinic, follow the instructions below and test your
setup by opening RStudio and typing `1 + 1` in the console. If it returns `2`,
you are ready.

## Software Setup

::::::::::::::::::::::::::::::::::::::: discussion

### Install R and RStudio

You need both R (the language) and RStudio (the interface). Think of R as the
engine and RStudio as the dashboard — you will work in RStudio, but it needs R
installed to run.

:::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::: spoiler

### Windows

1. Download R from [CRAN](https://cran.r-project.org/bin/windows/base/) — click
   "Download R for Windows", then "base", then the download link.
2. Run the installer with default settings.
3. Download RStudio from
   [Posit](https://posit.co/download/rstudio-desktop/) — click "Download
   RStudio Desktop".
4. Run the RStudio installer with default settings.
5. Open RStudio — if you see a console panel with the R version number, you are
   ready.

::::::::::::::::::::::::

:::::::::::::::: spoiler

### macOS

1. Download R from [CRAN](https://cran.r-project.org/bin/macosx/) — choose the
   `.pkg` file that matches your Mac (Apple Silicon or Intel).
2. Open the `.pkg` file and follow the installer.
3. Download RStudio from
   [Posit](https://posit.co/download/rstudio-desktop/).
4. Drag RStudio to your Applications folder.
5. Open RStudio — if you see a console panel with the R version number, you are
   ready.

::::::::::::::::::::::::

:::::::::::::::: spoiler

### Linux

1. Follow the instructions for your distribution at
   [CRAN](https://cran.r-project.org/bin/linux/).
2. Download RStudio from
   [Posit](https://posit.co/download/rstudio-desktop/) — choose the `.deb` or
   `.rpm` file for your distribution.
3. Install and open RStudio.

::::::::::::::::::::::::

## R Packages

During the course, we will install packages together. If you want to get ahead,
open RStudio and run this command in the console:

```r
install.packages(c("tidyverse", "haven", "rmarkdown"))
```

- **tidyverse** includes dplyr (data manipulation), ggplot2 (visualization),
  readr (reading data), and more
- **haven** reads SPSS `.sav` files directly into R
- **rmarkdown** creates reproducible reports

## Verify your setup

Open RStudio and paste this into the console:

```r
install.packages(c("tidyverse", "haven", "rmarkdown"))
library(tidyverse)
ggplot(mpg, aes(x = displ, y = hwy)) + geom_point()
```

If a scatter plot appears in the Plots pane, everything is working. Bring any
errors you see to the installation clinic or email the instructor.

## Download the workshop data

From Episode 2 onwards you will load the same small dataset in two different
formats — first as a CSV file, then as an Excel workbook with multiple sheets.
Download **both** files now and keep them together.

- [aruba_visitors.csv](https://github.com/University-of-Aruba/r-for-spss-users/blob/main/episodes/data/aruba_visitors.csv) — plain-text version (one flat table of 120 rows)
- [aruba_visitors.xlsx](https://github.com/University-of-Aruba/r-for-spss-users/raw/main/episodes/data/aruba_visitors.xlsx) — Excel version, two sheets: `stayover` and `cruise`

Open each link in your browser, then click the **Download raw file** button
near the top right of the preview and save the file. Do not open the CSV in
Excel and re-save — that can silently change the encoding.

### Where to put the files

Create a folder for the workshop, for example `Documents/r-workshop/`, and
inside it create a subfolder called `data`. Drop both files into `data`.
Your structure should look like this:

```
r-workshop/
└── data/
    ├── aruba_visitors.csv
    └── aruba_visitors.xlsx
```

When you open RStudio during the course, use **File → Open Project** to open
`r-workshop` (or set your working directory to the folder). The code in the
lessons assumes this layout, so `read_csv("data/aruba_visitors.csv")` and
`read_excel("data/aruba_visitors.xlsx")` both find their files without any
extra path work.

If you cannot download the files in advance, we will walk through this step
together at the start of Episode 2. Bring the two links.
