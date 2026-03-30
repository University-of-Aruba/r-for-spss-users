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
| 05 - Statistical Analysis | 120 min | This is the core for survey researchers. Take your time. |
| Break | 15 min | |
| 06 - Reproducible Reporting | 60 min | R Markdown is often the biggest "wow" for SPSS users |
| Break | 15 min | |
| 07 - Where to Go from Here | 45 min | End with practical next steps and community resources |

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

Prepare cleaned versions of these datasets in the `episodes/data/` folder before
the course. Test all data downloads — URLs and APIs can change.

## Train-the-Trainer

This course is designed for replication. If you are adapting it for another
island or institution:
1. Replace datasets with locally relevant equivalents
2. Adjust the SPSS operations covered based on your pre-course survey results
3. Keep the "wow first, skills second" structure
4. All materials are CC-BY 4.0 — please attribute the DCDC Network
