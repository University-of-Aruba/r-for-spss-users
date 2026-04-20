---
title: "Opening sequence: Wednesday morning"
duration: "10 to 12 minutes of story, then hands on the keyboard"
fits_within: "Episode 01 — The case for switching"
delivery: "Live and voice-driven. The Episode 1 page already shows one atmospheric scene image at the top. Beyond that, no slides. The wow demo moves to minute 45 or so, after participants have typed their first R code."
version: 3
---

# Opening sequence (v3)

The earlier versions assumed a six-cartoon slide deck. That is not how the lesson pages are built. Each of the seven episodes opens with a single atmospheric scene image at the top of its page (`episodes/fig/scene_1.jpg` through `scene_7.jpg`), and those images are decorative, not characters in a story. The opening sequence carries itself on voice, pacing, and silence. The Episode 1 page (`scene_1.jpg`, "One road costs you a license fee. The other one costs you a learning curve.") sets atmosphere; everything else lands through delivery.

Story first, a deliberate handoff into Episode 1, hands typing within fifteen minutes, and the public-repo demo lands at the end of Episode 1 as the payoff.

## Ground rules for delivery

Open the Episode 1 page in the browser before you start. The scene image is at the top; it sets atmosphere without you having to do anything. Beyond that, you are the medium: no slides, no projector switching during the opening.

Before you say your name, before you say the course title, before you say hello, you deliver the cold open. The question comes before the introduction.

Hold silences. The refinery moment works only if you do not rescue yourself. Count three seconds in your head after "I had no idea."

When you get to the thesis line, put silence on both sides of it. "A ritual cannot answer a follow-up question" is the sentence the rest of the two days descends from. Let it breathe.

Use specific time anchors. "Twelve years ago" is stronger than "some years ago" for oral storytelling. Pick a specific year and stick to it.

## The arc

Cold open. Origin. The refinery moment. The thesis. The turn. The handoff into Episode 1. The wow demo arrives at the end of Episode 1, not the start.

---

## Cold open (0:00 to 0:45)

You are at the front. The Episode 1 page is on the screen with the scene image visible. The room is not yet quiet. You wait.

First words, before you introduce yourself:

> Sixteen years ago, I presented the quarterly GDP results to the management of the central bank. And they asked me a question I could not answer.

Beat.

> The question was: what is driving the growth number this quarter. Is it the refinery coming back online. Is it tourism. Is it construction. I stood there with my printout and had no idea.

Beat.

> The model told me the answer. It did not tell me why. And that is what this course is really about.

Now you introduce yourself. Name, role, why you are here. Thirty seconds.

> My name is Rendell de Kort, i'm the DCDC Network adminsitrator and i have been analyzing data as an economist in different capacities.

## Origin (0:45 to 3:30)

> Quick rewind. I was in my twenties. I had just started at the Central Bank of Aruba as a research economist. I had Excel, SPSS, Stata and EViews on my laptop. I was convinced I was the sharpest analyst in the building.

Brief pause. Do not undercut the confidence.

> I had the software, I had the training, and I was producing output.

> Then consultants arrived from the Netherlands. They had been contracted to build us a nowcasting model. They worked on it for 2 weeks. When they left, they handed me a script and said: update the data here, run this code, this is your output. As long as you follow the steps, you will have a good working model.

> It was written in base R. At the time, R was this mysterious coding thing. I had never seen it. But I had my instructions. So every quarter, I did what they said.

## The refinery moment (3:30 to 5:00)

> For about two years, I ran their code every quarter. Update the data here, press run, send the output upstairs. Until one day I was presenting to management. And they asked me that question.

Slow down. Ask the question again, as if you are being asked it now:

> What is driving the growth number this quarter. Is it the refinery. Is it tourism. Is it construction.

Longer pause. Look at them. Do not rescue.

> I had no idea.

**Hold the silence. Three full seconds.**

## The thesis (5:00 to 5:30)

Walk forward half a step.

> What I had was not a model.

Beat.

> I had a ritual.

Beat.

> And a ritual cannot answer a follow-up question.

**Three more seconds of silence.** This is the line the whole workshop is built on. Let it land.

## The turn (5:30 to 7:00)

> So I started learning R. Slowly. Badly. It took years to get comfortable. And along the way I learned something I did not expect. The issue was never SPSS against R. The issue was between ritual and understanding. You can use any tool as a ritual. You can use any tool to understand.

> But one of these tools makes the ritual easy and understanding hard. The other makes understanding possible, at a cost. That cost is what you are paying with the next two days.

## The contract for the next two days (7:00 to 9:30)

> Two days. Nine to four-thirty, with breaks. You will leave with working code, a report you generated yourself, and a starting point for your own projects. The only thing we ask outside the room is a short survey at the end, which feeds into the network we are building across the islands.

> Three ground rules.

> One. Everyone here is a beginner in R. Including the people who are not beginners. Treat today as if you have never seen it before. You will learn more that way.

> Two. We use sticky notes. Green on your laptop means I am following. Red means I am stuck. No raised hands. The notes tell me who needs what without anyone having to speak.

> Three. We type code together. I type it on the screen, you type it on your laptop. Not copy-paste. You will not remember anything you copy-paste. You will remember what your fingers did.

## Handoff into Episode 1 (9:30 to 10:00)

> Let's open RStudio.

Switch to the live RStudio window. Walk them through the four panes. Begin Episode 1 proper.

From here, you are in Carpentries live-coding mode. Types, they type, sticky notes guide the pace.

---

## The wow demo moves here: end of Episode 1 (roughly minute 45)

After participants have typed their first assignments, run their first `mean()`, maybe drawn their first quick plot against the aruba_visitors dataset, you take three minutes to show them where this is going.

Switch to a blank script.

> Before we break, let me show you where this road leads. I am going to write three lines of code. These three lines will go to a public repository at the University of Aruba, download a dataset I maintain on small island developing states, and draw a chart.

Type the lines in front of them. Slowly. Narrate each line as you type.

```r
library(tidyverse)

countries <- read_csv(
  "https://raw.githubusercontent.com/University-of-Aruba/island-research-reference-data/main/countries/countries_reference_xlsform.csv"
)

countries |>
  filter(is_sids == 1) |>
  count(wb_region) |>
  ggplot(aes(x = reorder(wb_region, n), y = n)) +
  geom_col(fill = "#44759e") +
  coord_flip() +
  labs(title = "Small island developing states by World Bank region",
       x = NULL, y = "Number of SIDS")
```

Run it. Let the chart appear.

> Notice what just happened. I did not download a file. I did not store a copy. The data lives in one place, a public repository, maintained, versioned, auditable. Anyone in this room, anyone in the world, can run those three lines and get the same chart I just got. That is what reproducibility looks like, and you just saw enough R in the last forty-five minutes to start reading what I typed.

> The repository is real. It is part of the DCDC Network infrastructure we are building at the University of Aruba. After Friday, you can pull from it, contribute to it, use it in your own work.

> By Friday afternoon you will be writing those three lines yourselves. And the hundred lines that come after. Let's take fifteen.

Break.

---

## Why the demo moved

Version one had the demo in the opening. Reasons to move it:

The opening three lines of R that a learner sees should be lines they are about to type themselves. A remote data pull into a `coord_flip` is interesting to watch but it is not the shape of what they will do in the next five minutes. It creates distance, not proximity.

Carpentries pedagogy treats the first live-coding block as the first real beat of the workshop. Loading up the room with a showcase before they have typed anything pushes the live-coding block into the shadow of the demo. Better to let them own their first `c(1, 2, 3)` uninterrupted.

The wow of a public repo pull is bigger at minute forty-five than at minute eight, because by minute forty-five they can read it. They can see `library()`, `read_csv()`, the pipe, `ggplot()`. At minute eight those are all noise. At minute forty-five they are vocabulary. The demo also earns its place as a preview of Episode 6, reproducible reporting, which closes the arc.

---

## On the scene images

Each episode's lesson page already opens with one atmospheric scene image (`fig/scene_1.jpg` through `scene_7.jpg`) and a short quip caption. They are decoration that sets tone for the page. They are not characters or a recurring narrative across the workshop. Do not point at them, do not flip back to them, do not use them as story beats. They do their work passively.

Day 1 close: re-ask the refinery question to the room, not to yourself. "What is driving the growth number this quarter? Refinery, tourism, construction?" Different weight after a day of code. A few people will say "the refinery." A few will say "it depends." Both answers are wins. No visual aid needed; the question lands harder unaccompanied.

Day 2 close: return to "a ritual cannot answer a follow-up question." Pose it back to them as something they can now answer with their own scripts. Close on the silence.

---

## What to have ready before you walk in

RStudio already open with tidyverse loaded, a blank script visible. Browser tab with the Island Research Reference Data README already loaded on a second monitor in case anyone asks where the data lives. A local fallback CSV on the desktop with an alternate version of the three demo lines pointing at the local file, in case the Wi-Fi is unreliable.

The FAQ card printed and placed next to your laptop, face down. You will use it at least twice.

Green and red sticky notes at every seat. A printed attendance list. Chargers and extension cords, since Esther flagged outlet shortage. A spare one if you have it.

Baseline survey link verified and tested. DCDC onboarding survey link verified and tested. Feedback survey link verified and tested.

## What not to do

Do not open with a joke. Self-deprecation belongs inside the story, not on top of it.

Do not name the consultants' institution. "Consultants from the Netherlands" is enough. Specificity there turns a personal arc into a grievance.

Do not name the refinery company or the management member who asked the question. The sector and the role carry the weight.

Do not skip the silence after "I had no idea," and do not skip the silence on either side of "A ritual cannot answer a follow-up question." The silences are not dead air. They are the work.

Do not flip between slides during the opening. The Episode 1 page sets the visual frame. Beyond that, you are the medium.

Do not put the GitHub pull demo before they have typed their own first line of R.
