---
title: "Pre-course checklist"
course_dates: "Wed Apr 22 and Fri Apr 24, 2026"
---

# Pre-course checklist

Things only you can do. Work down the list; tick as you go.

## Content verification (tonight or Tuesday morning)

- [ ] **Knit Episode 6 end-to-end.** Open `episodes/06-reproducible-reporting.Rmd` in RStudio, click Knit, watch where it errors. The hidden data-load chunk I added fixes the missing-object class of error. If other errors remain (chunk-header display issues, inline-R rendering), fix them one at a time using "Run Current Chunk" to isolate. Do not push to GitHub until the episode knits cleanly end-to-end.
- [ ] **Verify both surveys** in an incognito browser window so your Google login does not mask a broken link:
  - Course evaluation: `https://docs.google.com/forms/d/e/1FAIpQLSeq_hRNTbsBXCrvHRUYky8h4aHDAIzrjRjHEhGxdkzuTAwTyQ/viewform`
  - DCDC Network onboarding: `https://docs.google.com/forms/d/e/1FAIpQLScMSYe1trO9g_ajjftEMLk0k1I8fXDUBiyOyydGTCh7xX7Dcw/viewform`
  - Confirm each form loads and accepts a test response. If broken or renamed, repeat the Forms → Send → link icon copy and replace in both `episodes/07-next-steps.Rmd` and this checklist.
- [ ] **Tone check Episode 2 .R-extension callout.** Silent-read the page. If the expanded three-reasons version feels heavy inside a callout block, split it: keep the short "you will thank yourself later" line as the callout, move the three reasons into a paragraph of body text after.
- [ ] **Pin the year in the cold open.** The opening script currently says "Twelve years ago." If a specific year is sharper for you ("In 2013"), swap it. Stick to whatever you choose.

## Delivery dry-run (Tuesday evening)

- [ ] **Three-line demo on the course Wi-Fi.** Walk into the room, run the `library(tidyverse)` + `read_csv` from GitHub + `ggplot` block from the opening-script. If it fails, switch to the local-file fallback.
- [ ] **Local fallback CSV on desktop.** Download `countries_reference_xlsform.csv` to the desktop. Write an alternate version of the three lines pointing at the local file. Have it ready to paste.
- [ ] **Read the opening script aloud, once.** Time the silences. Three seconds after "I had no idea" feels longer than you expect.

## Physical prep (Tuesday night, pack the bag)

- [ ] Print `instructors/faq-card.html` (A5, one card per page, keep face-down next to laptop)
- [ ] Six cartoons in order on the slide deck
- [ ] Power strip (Esther's outlet shortage) plus two USB-C and two USB-A loaners
- [ ] Green and red sticky notes for every seat
- [ ] Printed attendance list

## Professional visibility (Tuesday evening, after knit passes)

- [ ] Push the fixed episodes to GitHub
- [ ] Short WhatsApp to Esther: "Fixed the callouts and the broken chunks in 6, added the graph gallery link, surveys tested. Ready for Wednesday." She flagged the issues; she should know you acted on them.

## During the course

- [ ] Opening: announce the outlet location ("outlets on the left wall; top up during breaks, not during live coding")
- [ ] Day 1 close: Cartoon 4 returns. Ask the room the refinery question.
- [ ] Day 2 close: Cartoon 6 as the final slide. Callback closes the loop.
