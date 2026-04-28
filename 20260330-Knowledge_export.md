# Knowledge export: Introduction to R for SPSS users

_Prepared for: Rendell Ernest de Kort | DCDC Network / LovelyData | April 2026_

---

## 1. Course context and logistics

| Item                 | Detail                                     |
| -------------------- | ------------------------------------------ |
| Dates                | April 22 and 24, 2026                      |
| Venue                | University of Aruba                        |
| Capacity             | 15–20 participants                         |
| Cost to participants | Free                                       |
| Organizer            | DCDC Network                               |
| Training developer   | LovelyData (quote ref: DCDC-TRAIN-2026-01) |
| Funder               | NWO via Open Science NL                    |
|                      |                                            |
|                      |                                            |

**Audience profile:** Researchers, lecturers, and data practitioners at Dutch Caribbean institutions who currently use SPSS for data analysis. They are statistically literate but not necessarily programmers. Many will have anxiety about switching tools. Expect a mix of experienced SPSS users and some who use SPSS only occasionally.

**Two-session structure:** Session 1 (Apr 22) should build confidence and orientation. Session 2 (Apr 24) should consolidate and apply. A 48-hour gap between sessions is an asset — assign light practice between sessions.

---

## 2. The core pedagogical challenge

The biggest barrier is not statistical — it is psychological. SPSS users are accustomed to a point-and-click interface that feels safe and produces immediate output. R requires them to _write_ before they _see_. Your presentation must address this head-on.

**Key reframe to communicate:** R is not harder than SPSS. It is _different_. SPSS hides its logic; R makes it visible. That visibility is initially uncomfortable but ultimately more powerful and trustworthy.

**Adult learning principles to apply:**

- Lead with the "why" before the "how"
- Anchor every new R concept to its SPSS equivalent
- Celebrate small wins early (a clean plot in 3 lines of code is magic to an SPSS user)
- Normalize errors — they are part of the workflow, not signs of failure

---

## 3. Conceptual map: SPSS vs R

### Philosophy

|Dimension|SPSS|R|
|---|---|---|
|Interface|GUI (menus) + syntax|Script-first (RStudio IDE)|
|Workflow|Click → output|Write → run → output|
|Data view|Spreadsheet always visible|Data in memory, viewed on demand|
|Reproducibility|Limited (unless syntax saved)|Full (script = full record)|
|Cost|Licensed (~€1,500+/yr)|Free and open source|
|Community|Declining|Large, active, global|
|Output|Fixed tables|Fully customizable|
|Learning curve|Low initial, low ceiling|Higher initial, very high ceiling|

### Data concepts

|Concept|SPSS term|R equivalent|
|---|---|---|
|Data file|`.sav` file / Data View|Data frame (`data.frame` or `tibble`)|
|Variable|Column in Variable View|Vector / column|
|Case|Row|Row / observation|
|Value labels|Labels in Variable View|Factor levels|
|Missing values|System missing (`.`)|`NA`|
|String variable|String|Character vector|
|Numeric variable|Numeric|Numeric vector (`dbl` or `int`)|
|Output window|Output Viewer|Console + Plots pane + R Markdown|

### Analysis concepts

|Task|SPSS|R|
|---|---|---|
|Descriptives|Analyze → Descriptive Statistics|`summary()`, `skimr::skim()`, `psych::describe()`|
|Frequencies|Analyze → Frequencies|`table()`, `janitor::tabyl()`|
|Crosstabs|Analyze → Crosstabs|`table()`, `janitor::tabyl()`|
|T-test|Analyze → Compare Means|`t.test()`|
|ANOVA|Analyze → GLM|`aov()`, `lm()`|
|Correlation|Analyze → Correlate|`cor()`, `corrplot::corrplot()`|
|Regression|Analyze → Regression|`lm()`, `summary(lm(...))`|
|Recode variable|Transform → Recode|`dplyr::mutate()` + `case_when()`|
|Compute variable|Transform → Compute|`dplyr::mutate()`|
|Select cases|Data → Select Cases|`dplyr::filter()`|
|Sort cases|Data → Sort Cases|`dplyr::arrange()`|
|Merge files|Data → Merge Files|`dplyr::left_join()` etc.|
|Split file|Data → Split File|`dplyr::group_by()`|
|Charts|Graphs → Chart Builder|`ggplot2`|

---

## 4. Core R concepts to introduce

### 4.1 The RStudio environment

Participants need a mental map before touching code. Walk through the four panes:

- **Source** (top left): where you write scripts
- **Console** (bottom left): where code runs
- **Environment/History** (top right): what's loaded in memory
- **Files/Plots/Packages/Help** (bottom right): everything else

Key message: _Save your script, not just your output. The script is the work._

### 4.2 Objects and assignment

```r
x <- 5           # assign value 5 to object x
name <- "Aruba"  # assign character string
```

SPSS analogy: there is no direct equivalent — this is a new concept, but frame it as "naming things so you can reuse them."

### 4.3 Functions

```r
mean(x)          # function(argument)
round(3.14159, 2)  # function(argument1, argument2)
```

SPSS analogy: menu options are like functions. `mean(scores)` = Analyze → Descriptive Statistics → Descriptives → Mean.

### 4.4 Packages

```r
install.packages("tidyverse")  # once
library(tidyverse)              # every session
```

SPSS analogy: like add-on modules (Custom Tables, Advanced Statistics), but free.

**Essential packages for this audience:**

- `tidyverse` (data wrangling + ggplot2)
- `haven` (import SPSS .sav files — critical transition package)
- `janitor` (clean names, frequency tables)
- `skimr` (descriptive statistics)
- `gtsummary` (publication-ready tables)
- `rstatix` (pipe-friendly stats tests)

### 4.5 Reading data

```r
library(haven)
data <- read_sav("myfile.sav")   # read directly from SPSS format
```

This is your bridge moment. Tell them: _You don't have to abandon your existing data. R reads SPSS files natively._

Also cover CSV as the preferred open format:

```r
data <- read_csv("myfile.csv")
```

### 4.6 The pipe operator

```r
data |> filter(age > 30) |> summarise(mean_score = mean(score))
```

SPSS analogy: chaining menu steps, but written out and reproducible. Explain the `|>` as "and then."

### 4.7 Tidy data principles

Before diving into dplyr, explain tidy data:

- Each variable = one column
- Each observation = one row
- Each value = one cell

Most SPSS users already work with tidy data without knowing the name. Naming the principle empowers them.

### 4.8 Core dplyr verbs (the SPSS workflow in R)

|Verb|What it does|SPSS equivalent|
|---|---|---|
|`filter()`|Keep rows matching condition|Select Cases|
|`select()`|Keep specific columns|Keep variables in output|
|`mutate()`|Create or modify columns|Compute / Recode|
|`summarise()`|Collapse to summary stats|Descriptives / Frequencies|
|`group_by()`|Group for grouped operations|Split File|
|`arrange()`|Sort rows|Sort Cases|
|`rename()`|Rename columns|Rename variables|

### 4.9 Basic visualization with ggplot2

```r
ggplot(data, aes(x = age, y = score)) +
  geom_point() +
  theme_minimal()
```

The grammar of graphics concept: every plot is built from layers. This is different from SPSS Chart Builder but more flexible.

Showcase the contrast: a publication-ready SPSS chart vs. an equivalent ggplot2 chart. Let the visual quality speak.

---

## 5. Suggested two-session structure

### Session 1 (April 22) — Orientation and foundations (~3 hours)

|Segment|Duration|Content|
|---|---|---|
|Welcome and framing|20 min|Why R? Why now? FAIR data and reproducibility|
|The SPSS–R bridge|20 min|Conceptual mapping, addressing anxieties|
|RStudio tour|15 min|Live demo of environment|
|R basics hands-on|45 min|Objects, functions, packages|
|Reading data|30 min|`haven::read_sav()`, `read_csv()`|
|Break|15 min||
|Data exploration|40 min|`glimpse()`, `summary()`, `skimr::skim()`|
|Wrap-up and between-session task|15 min|Practice instructions|

**Between-session task:** Load a dataset of their choice (or provided dataset), run `skim()`, and write 3 observations about the data in plain language.

### Session 2 (April 24) — Wrangling and visualization (~3 hours)

|Segment|Duration|Content|
|---|---|---|
|Recap and Q&A on task|20 min|Review what participants tried|
|dplyr core verbs|60 min|filter, mutate, group_by, summarise|
|Break|15 min||
|ggplot2 introduction|50 min|Scatter, bar, histogram|
|Reproducibility and next steps|25 min|Scripts, R Markdown intro, resources|
|Closing|10 min|DCDC network, community, follow-up|

---

## 6. Dataset recommendation

Use a Caribbean-relevant or locally familiar dataset. Options:

- **Election data** (synergy with FAIR Elections concept note): party results by island/municipality
- **Tourism/economic data**: visitor arrivals, GDP components from CBA Aruba or CBS
- **Health/education data**: publicly available from CBS Caribbean

A locally meaningful dataset transforms a technical exercise into a conversation about real issues. It also reinforces the DCDC network's message about Caribbean data.

If no suitable local dataset is available, a clean international dataset works fine (e.g., `gapminder` from the `gapminder` package — intuitive, diverse, no privacy concerns).

---

## 7. Key messages to thread throughout

1. **Reproducibility:** In SPSS, if you lose your output file, it's gone. In R, your script _is_ your analysis. Run it again and get exactly the same result.
2. **FAIR data alignment:** R workflows naturally produce FAIR-er outputs — scripts are documented, data stays in open formats, analyses are reusable.
3. **Career and institutional value:** R literacy is increasingly expected in grant applications, publications, and collaboration with European research partners.
4. **Community:** R has one of the largest, most welcoming communities in data science. You are not learning alone.
5. **R is not replacing SPSS overnight:** Frame this as expanding the toolkit, not burning the old one.

---

## 8. Common SPSS-to-R stumbling blocks (anticipate and address)

|Stumbling block|What SPSS users expect|How to address|
|---|---|---|
|Error messages|Alarming red text|"Errors are your friends. They tell you exactly what went wrong. SPSS just silently gave you wrong output."|
|No visible data table|Data always visible in SPSS|Teach `View(data)` and `glimpse()` early|
|Case sensitivity|SPSS is not case-sensitive|Emphasize: `Age` ≠ `age` in R|
|Quotation marks|Not needed in SPSS menus|Characters always need quotes; object names never do|
|Factor vs numeric|Value labels automatic in SPSS|Explain factors explicitly with a relatable example|
|`NA` vs blank cells|Blanks handled automatically|Introduce `is.na()` and `na.rm = TRUE` early|
|Package not found|SPSS modules pre-installed|Always `library()` at top of script|

---

## 9. Resources to share with participants

|Resource|Description|URL|
|---|---|---|
|R for Data Science (2e)|Core textbook, free online|r4ds.hadley.nz|
|Posit Cloud|RStudio in the browser, no install needed|posit.cloud|
|The Carpentries|Free R training workshops (aligns with DCDC model)|carpentries.org|
|Tidyverse documentation|Official package docs|tidyverse.org|
|R Graph Gallery|ggplot2 examples with code|r-graph-gallery.com|
|SPSS to R cheat sheet|Quick reference|Various; worth preparing a custom one|

---

## 10. Open science and FAIR alignment talking points

This course sits within the DCDC network's broader mission. Weave in at natural moments:

- R produces fully reproducible analyses when scripts are saved and shared — directly supporting FAIR's **Reusable** principle
- Open-format data (CSV) supports **Interoperability** and **Accessibility**
- Sharing scripts via GitHub or Zenodo supports **Findability** and community knowledge
- The DCDC network's training program is itself an example of open, modular, reusable capacity building

_This is not just a software course. It is an entry point into a different way of doing research._

---

_Document version: 1.0 | Prepared with Claude | For internal use — DCDC Network / LovelyData_