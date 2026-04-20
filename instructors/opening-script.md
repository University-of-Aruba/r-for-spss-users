---
title: "Opening sequence: Wednesday morning"
duration: "7 to 8 minutes of story, then into the page"
fits_within: "Episode 01 — The case for switching"
delivery: "Live and voice-driven. The Episode 1 page already shows one atmospheric scene image at the top and contains the live WDI demo as an embedded instructor block. The opening script is a wrapper around that page, not a parallel performance."
version: 4
---

# Opening sequence (v4)

This script is a wrapper around the existing Episode 1 page. Earlier versions invented a parallel six-cartoon slide deck and a separate GitHub-pull "wow demo" that competed with the WDI demo already scripted on the page. v4 strips both. The personal narrative still opens the workshop. The page then carries the cost argument, the R-vs-SPSS section, and the live WDI demo on its own terms.

Each of the seven episodes opens with one atmospheric scene image at the top (`episodes/fig/scene_1.jpg` through `scene_7.jpg`). Those are decorative, not characters in a story. The opening sequence carries itself on voice, pacing, and silence.

## Ground rules for delivery

Open the Episode 1 page in the browser before you start. The scene image is at the top; it sets atmosphere without you having to do anything. Beyond that, you are the medium: no slides, no projector switching during the opening.

Before you say your name, before you say the course title, before you say hello, you deliver the cold open. The question comes before the introduction.

Hold silences. The refinery moment works only if you do not rescue yourself. Count three seconds in your head after "I had no idea."

When you get to the thesis line, put silence on both sides of it. "A ritual cannot answer a follow-up question" is the sentence the rest of the two days descends from. Let it breathe.

Use specific time anchors. "Twelve years ago" is stronger than "some years ago" for oral storytelling. Pick a specific year and stick to it.

## The arc

Cold open. Origin. The refinery moment. The thesis. The turn. Three ground rules. Then hand into the Episode 1 page and let the page lead the rest of the hour.

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

## Handoff into the Episode 1 page (7:00 to 7:30)

You have given them the personal arc and the three ground rules. Stop scripting. Hand into the page.

> Let's get started. Episode 1 is on the screen. The big questions for the next forty-five minutes are right there at the top: why switch, what does R give you that SPSS does not, and what does the cost actually look like. We will work through those together.

Scroll to the cost-argument table. Walk them through it briefly. Then through "What R gives you that SPSS does not." Brief is fine. Their eyes are on the page; you are providing colour, not narration.

When you reach the **Live demonstration** heading, switch to RStudio and follow the embedded instructor block on the page (`:::: instructor` ... `::::`). It contains the full script: WDI tourism arrivals for AW, CW, SX, the ggplot2 chart, the SPSS contrast walkthrough. Do not improvise a different demo here. The page is the script.

After the demo, deliver the page's summary in your own words and break for fifteen.

From here, you are in Carpentries live-coding mode for the rest of the day. They type, you type, sticky notes guide the pace.

---

## Why this script does not contain a separate wow demo

Earlier versions scripted a second demo at minute forty-five (a `read_csv` from a UA GitHub repo). That demo competed with the WDI tourism demo already on the page. Two demos for one moment splits attention and makes one of them feel redundant. The page already has the wow built in: a live API pull, a publication-quality chart in ten lines, and a side-by-side with the SPSS clicking workflow. Lean on that.

The UA GitHub datasets (election data, island reference data) are introduced in Episode 7, not Episode 1. Resist the urge to preview them here.

---

## On the scene images

Each episode's lesson page already opens with one atmospheric scene image (`fig/scene_1.jpg` through `scene_7.jpg`) and a short quip caption. They are decoration that sets tone for the page. They are not characters or a recurring narrative across the workshop. Do not point at them, do not flip back to them, do not use them as story beats. They do their work passively.

Day 1 close: re-ask the refinery question to the room, not to yourself. "What is driving the growth number this quarter? Refinery, tourism, construction?" Different weight after a day of code. A few people will say "the refinery." A few will say "it depends." Both answers are wins. No visual aid needed; the question lands harder unaccompanied.

Day 2 close: return to "a ritual cannot answer a follow-up question." Pose it back to them as something they can now answer with their own scripts. Close on the silence.

---

## What to have ready before you walk in

The Episode 1 page open in the browser, scrolled to the top.

RStudio already open with `WDI`, `ggplot2`, and `scales` installed and loaded, a blank script visible. The packages list is in the page's instructor block; install before the workshop, do not improvise on the day.

A backup `tourism` CSV on the desktop with the WDI data pre-pulled, in case the Wi-Fi is unreliable. The page's instructor block tells you what to load it as.

The FAQ card printed and placed next to your laptop, face down. You will use it at least twice.

Green and red sticky notes at every seat. A printed attendance list. Chargers and extension cords, since Esther flagged outlet shortage. A spare one if you have it.

Baseline survey link verified and tested. DCDC onboarding survey link verified and tested. Feedback survey link verified and tested.

## What not to do

Do not open with a joke. Self-deprecation belongs inside the story, not on top of it.

Do not name the consultants' institution. "Consultants from the Netherlands" is enough. Specificity there turns a personal arc into a grievance.

Do not name the refinery company or the management member who asked the question. The sector and the role carry the weight.

Do not skip the silence after "I had no idea," and do not skip the silence on either side of "A ritual cannot answer a follow-up question." The silences are not dead air. They are the work.

Do not flip between slides during the opening. The Episode 1 page sets the visual frame. Beyond that, you are the medium.

Do not improvise a second demo on top of the page's WDI demo. One wow per moment. The page's demo is the wow.
