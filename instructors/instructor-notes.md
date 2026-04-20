---
title: 'Instructor Notes'
---

## General Teaching Approach

This course follows the Carpentries live-coding pedagogy: the instructor types
code live while participants follow along. Avoid slides for code — always
demonstrate in RStudio.

Key principles:
- **Start from what they know**: Every R operation is introduced alongside its
  SPSS equivalent. Use SPSS terminology first, then introduce the R term.
- **Wow first, skills second**: Episode 1 is pure motivation. Show impressive
  things before asking anyone to type.
- **Sticky notes**: Use colored sticky notes (or digital equivalents) for
  real-time feedback. Green = I'm following. Red = I need help.
- **Helpers**: Aim for 1 helper per 5-8 participants to assist with individual
  issues without stopping the class.

## Session Structure

### Session 1 (5-6 hours with breaks)

| Episode | Time | Notes |
|---|---|---|
| 01 - The Case for Switching | 45 min | Instructor demo only, no participant coding |
| Break | 15 min | |
| 02 - Your First R Session | 90 min | First hands-on. Go slow. Many will struggle with typos. |
| Break | 15 min | |
| 03 - Data Manipulation | 90 min | The pipe operator is the key "aha" moment |
| Break | 15 min | |
| 04 - Visualization | 60 min | End on a high — everyone leaves with a beautiful chart |

### Session 2 (5-6 hours with breaks)

| Episode | Time | Notes |
|---|---|---|
| Review and troubleshooting | 30 min | Address questions from between-session practice |
| 05 - Statistical Analysis | 120 min | Core for survey researchers. The normality-testing section (histogram, Q-Q plot, Shapiro-Wilk, robustness note) maps directly onto the SPSS Explore output most participants will recognise. Take your time. |
| Break | 15 min | |
| 06 - Reproducible Reporting | 60 min | R Markdown is often the biggest "wow" for SPSS users |
| Break | 15 min | |
| 07 - Where to Go from Here | 55 min | End with practical next steps. The new UA datasets subsection (CAS_election_data and island-research-reference-data) is a chance to live-demo `read.csv()` straight from a raw GitHub URL — most SPSS users have never seen data load over HTTPS without a manual download. |

## Common Issues

- **Installation problems**: The pre-course installation clinic should catch
  most of these. Have a USB drive with R and RStudio installers as backup.
- **Typos**: SPSS users are not used to typing commands. Expect many syntax
  errors. Normalize this — "error messages are how R talks to you."
- **Parentheses and quotes**: The most common beginner errors. Show how RStudio
  auto-completes these.
- **Loading packages**: Participants will forget `library()`. Remind them at
  the start of each episode.

## Local Data Notes

The course uses Dutch Caribbean datasets to keep examples relevant:
- CBS Aruba tourism and CPI data (Excel downloads from cbs.aw)
- World Bank indicators via the `WDI` package
- CBS Netherlands BES island data via `cbsodataR`
- **CAS_election_data** — Aruba, Curacao, Sint Maarten election results 1985-2025 (tidy CSV at github.com/University-of-Aruba/CAS_election_data). Used in Episode 7.
- **island-research-reference-data** — country reference list with SIDS, SNIJ, and World Bank classifications (CSV at github.com/University-of-Aruba/island-research-reference-data). Used in Episode 7.

Prepare cleaned versions of these datasets in the `episodes/data/` folder before
the course. Test all data downloads — URLs and APIs can change.

### Note on the elections example

The Episode 7 election-data example deliberately groups MEP and AVP together
versus all other parties, rather than singling out one party. Aruba's two-party
dynamic means filtering on `party == "MEP"` (or `"AVP"`) on its own can read
as partisan bias in a publicly distributed course. If extending the example
live, default to the same grouped framing or to all-parties views (e.g. all
parties for the most recent election, or vote share over time). If a
participant asks why we don't filter to one party, this is the reason worth
naming briefly: it is a small editorial choice that protects the course and
the network's neutrality.

## Train-the-Trainer

This course is designed for replication. If you are adapting it for another
island or institution:
1. Replace datasets with locally relevant equivalents
2. Adjust the SPSS operations covered based on your pre-course survey results
3. Keep the "wow first, skills second" structure
4. All materials are CC-BY 4.0 — please attribute the DCDC Network
