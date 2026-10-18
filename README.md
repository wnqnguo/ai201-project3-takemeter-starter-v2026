# TakeMeter

> ### 👋 Start here
>
> **New to this repo? Read [RUNNING.md](RUNNING.md) first** — setup, the
> notebook, the baseline, and what to do when something breaks.
>
> Once `python test.py` passes:
>
> ```bash
> head -5 data/practice_labels.csv     # the shape your labels.csv needs
> ```
>
> Then open `takemeter.ipynb` **in this folder** — in VS Code, or with
> `jupyter notebook` if you prefer. Pick the kernel: the `.venv` inside this
> project. Run section 1, which reports the hardware you'll be training on.
> Everything else waits until you have data.
>
> Nothing to upload, nothing to connect, no accounts and no keys. The notebook
> runs on your machine and writes next to your code.
>
> **The rest of this file is your submission.** Fill it in as you go.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     HOW TO USE THIS FILE

     Unit 5 asks for the first five sections. Unit 6 adds the five below them.

     Everything is pasted as TEXT. No screenshots, no images.

     ⚠️ The confusion matrix especially. The notebook prints one as a markdown
     table, ready to copy. A screenshot of a matrix earns nothing. Paste the
     table.
     ───────────────────────────────────────────────────────────────────────── -->

<!-- ═══════════════════════ UNIT 5 — THE BUILD ═══════════════════════ -->

## What This Does

<!-- Your community, and what your classifier sorts posts into. Three or four
     sentences. -->

TakeMeter sorts posts from r/ExperiencedDevs, a public subreddit where working software engineers discuss careers, teams, and engineering practice. It labels each post by what kind of post it is and how well it is supported: an opinion backed by something specific, an opinion with nothing behind it, a personal share (a feeling or an experience), or a question. The goal is to tell substantial posts from noise the way a regular of the community would, using distinctions I can state in a sentence and apply the same way twice.

---

## Label Taxonomy

<!-- Each label: a one-sentence definition and two real examples from your
     reading. Then your decision rule for the hardest boundary.

     The decision rule is worth a point on its own and it's the thing most
     people leave out. Every taxonomy has a hardest boundary. Name yours. -->

<!-- DRAFT: working labels and definitions from Milestone 1. Replace the
     example placeholders with real posts from r/ExperiencedDevs, and tighten
     the definitions in Milestone 2. -->

### `argued_opinion`

**Definition:** A claim someone could argue with, backed by something specific such as a number, a real experience, or a named tool or incident.

**Example 1:**
> A post titled as a question about LLM-written documentation becoming unreadable. It argues docs have gotten worse and backs this with the writer's own experience: in the industry since 2013, hired four months ago, and now faced with giant generated CLI commands, large Terraform files, and YAML written for LLMs. It never asks readers for help; the title question is rhetorical.

**Example 2:**
> A post whose title cites a study finding about reduced brain activity among ChatGPT users. It links two news reports, quotes specific results (a 21% improvement with AI, then 15.3% worse unassisted by week four), and argues the same loss of skills is even more prevalent in software development. It does not ask readers anything.

### `unsupported_opinion`

**Definition:** A confident claim someone could argue with, with nothing specific offered to support it.

**Example 1:**
> "Datadog is objectively better than Grafana, Chronosphere" (post title). The body lists feature areas (traces, logs, dashboards, alerting) but gives no comparison, number, or example for any of them.

**Example 2:**
> A Meta post claiming the subreddit is being taken over by hobbyists and students who have never been paid as developers. It illustrates this with a generic five-step pattern of how comment chains go, but gives no number, no named thread, and no specific incident, and it offers no solution.

### `personal_share`

**Definition:** A post that mainly expresses a feeling or recounts the writer's own experience, with no ask for advice or information and no claim offered for debate.

**Example 1:**
> A writer recounts three years of heavy AI coding tool use, then stopping because of how it affected their wellbeing, and says they are sharing the story in case others relate. They explicitly make no claim about AI quality or productivity and ask readers for nothing.

**Example 2:**
> A manager posts an update to an earlier thread: their team improved, was then laid off, and a new disengaged team now reports to them. It describes events and ends on stress and uncertainty ("unsure where to go from here") without asking for advice or making a claim to debate.

### `question`

**Definition:** A post that mainly asks for help, advice, or information rather than making a point.

**Example 1:**
> "How do you explain a race condition to a non-technical person?" (post title). The writer describes two analogies that did not work and closes by asking whether they are missing a principle for communicating technical problems.

**Example 2:**
> A teacher of first-year IT students asks which key skills and topics to cover for requirements gathering and project management, and asks for resource recommendations. They list their current topic ideas as background, but the post exists to ask for recommendations.

### The hardest boundary

**Which two labels:** `personal_share` vs. the opinion labels (many personal posts carry a claim, and many opinions are written with strong feeling). Second candidates: `question` vs. the opinion labels, and `argued_opinion` vs. `unsupported_opinion`.

**The decision rule I used every time:**
<!-- e.g. "If the post names a specific checkable fact, it's `analysis`, even
     if the tone is heated." -->
Apply in this order:
1. If the post makes a real request, it is a `question`. A request is real only if answering it would give the writer something to act on, such as a decision, a how-to, or a recommendation (including a writer who states a preference but still needs to decide). These are not requests: rhetorical questions, "anyone else...?" or "does it always feel like this?" (invitations to relate), and challenges to a claim the writer already made ("has anyone actually seen X work?").
2. Otherwise, if the post makes a claim someone could argue with, it is an opinion even when the tone is angry. It is `argued_opinion` only if the support is checkable: a number, a specific situation described in concrete detail, a named tool or incident, or a linked source. A general impression ("nobody I know does it") is not enough, so the post is `unsupported_opinion`.
3. Otherwise, if it mainly expresses a feeling or recounts the writer's own experience, it is `personal_share`.

**The borderline post:** A post whose title says AI has made the 80/20 rule worse and is killing the writer's passion for creative projects. It argues that AI gives the first 80% for free but makes the last 20% harder to justify, and supports that with a story about a vibecoded game. It then ends by describing frustration and loss of direction, with no question or ask. It could be `argued_opinion` (it has a thesis and an example) or `personal_share` (the title and closing are about feeling). Under my rule I label it `argued_opinion`: it states a thesis someone could argue with and supports it with a specific example, so step 2 applies before step 3, even though the tone is emotional.

---

## The Dataset

<!-- Where you collected from, how you labelled, your counts, and three hard
     cases. -->

**Where the posts came from:** Public posts from r/ExperiencedDevs, sampled across New, Hot, and Top so weak posts are included.

**How I labelled them:** <!-- Cold first? Pre-labelled with AI and corrected?
Say so plainly — the disclosure is required, not penalised. -->

**Counts per label:**

| Label | Count | Share |
|---|---|---|
|  |  |  |
|  |  |  |
|  |  |  |
| **Total** |  | 100% |

**Three hard cases**

<!-- Any post that made you pause: what it was, which two labels it could have
     been, and what you chose. These are worth more than the easy 190. -->

**1.**
> *The post:* A manager asks how to handle developers' unrequested AI-built side projects and dashboards, which cause duplicated work and leave the team unsure what is going on. It describes specific incidents and claims AI makes people talk less, then closes by asking for practical suggestions.
>
> *Could have been:* `question` or `argued_opinion`
>
> *I chose `question`, because:* the post ends by asking for advice and its claims serve as context for that ask. The one claim about AI reducing conversation rests only on "I've noticed," so it is not strongly argued either.

**2.**
> *The post:* A senior engineer with about 12 years of experience describes being passed over for promotion while less experienced colleagues advance, and asks what to do. It has concrete specifics (years without promotion, five managers in two years) and a frustrated tone.
>
> *Could have been:* `question` or `personal_share`
>
> *I chose `question`, because:* it opens with a request for advice and closes with "what do I do here?", so the ask decides the label even though the tone is frustrated.

**3.**
> *The post:* An engineer at a large tech company notes that monthly AI spend splits into a low-three-figure group and a low-four-figure group, and says the heavy spenders do not look more productive. They then ask the heavy spenders about their workflow and ask managers how they view both groups.
>
> *Could have been:* `question` or `argued_opinion`
>
> *I chose `question`, because:* the post ends with several direct questions to readers. Its main claim (higher spend does not mean higher productivity) is only anecdotal and is offered as the reason for asking.

---

## The Training Run

<!-- Your starting model, your settings, and anything you changed and why. -->

**Base model:**

**Settings:** <!-- epochs, learning rate, batch size, seed -->

**Anything I changed from the defaults, and why:**

**Split sizes:** <!-- train / val / test, and per-label counts in the test
split. If a label had fewer than about 8 in test, say so — it explains a lot
of next unit's variance. -->



---

## How I Used AI

<!-- Two specific moments — what you asked, what came back, what you changed.

     ⚠️ Plus disclosure of any pre-labelling. If you had a model pre-label a
     batch and then read and corrected every one, say that. It's an allowed
     workflow and disclosing it costs you nothing. Not disclosing it is the
     problem. -->

**Moment 1**

- *What I asked for:*
- *What came back:*
- *What I changed:*

**Moment 2**

- *What I asked for:*
- *What came back:*
- *What I changed:*

**Pre-labelling disclosure:**

<!-- ═══════════════════════ UNIT 6 — THE TEST ═══════════════════════

     Don't fill these in during unit 5.
     ═══════════════════════════════════════════════════════════════════ -->

---

## Baseline vs. Trained

<!-- Both models on the same posts. `python baseline.py --trained results.json`
     prints this table for you. -->

| Measure | Baseline | Trained | Difference |
|---|---|---|---|
| Overall accuracy |  |  |  |
| Macro F1 |  |  |  |
| F1 — `label_one` |  |  |  |
| F1 — `label_two` |  |  |  |

**What I predicted before I looked:**
<!-- Milestone 1 asks you to write this BEFORE seeing the trained numbers. A
     prediction made afterwards isn't one. -->

**What the gap actually means:**
<!-- If the baseline matched your trained model, your fine-tuning added
     nothing — and that is a real finding, not a failure. Say it plainly. -->



---

## Run Log — Before

<!-- Five criteria across three seeds. The notebook's section 6 prints the
     spread table; the Target and Verdict columns are yours. -->

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1.  |  |  |  |  |  |
| 2.  |  |  |  |  |  |
| 3.  |  |  |  |  |  |
| 4.  |  |  |  |  |  |
| 5.  |  |  |  |  |  |

### Confusion matrix

<!-- ⚠️ TYPED AS A MARKDOWN TABLE. The notebook prints one ready to paste.
     An image of a matrix earns nothing. -->

| true \ predicted |  |  |  |
|---|---|---|---|
| **** |  |  |  |
| **** |  |  |  |
| **** |  |  |  |

**My biggest off-diagonal number, and what it means:**
<!-- Not "the model made mistakes" — WHICH boundary it didn't learn, and which
     direction. "7 real analysis posts were called hot_take and only 3 went the
     other way" is a direction, not just an error rate. -->



---

## Verdicts and Diagnoses

<!-- MET or MISSED against LAST UNIT's target. The target has to hold across
     all three seeds, not turn up sometimes. -->

| # | Criterion | Target | Verdict | How I decided |
|---|---|---|---|---|
| 1 |  |  |  |  |
| 2 |  |  |  |  |
| 3 |  |  |  |  |
| 4 |  |  |  |  |
| 5 |  |  |  |  |

**Diagnoses**

<!-- For each miss: the cause, and how you know. The four common causes are:
     too few examples for a label, a boundary you applied inconsistently, a
     genuinely hard label pair, and a task the model can't reach from this
     much data.

     ⚠️ Use your agreement report as evidence. It is the only instrument you
     have that can tell a LABELLING problem from a MODEL problem, and this
     section is graded on whether you used it that way. -->



---

## Agreement Report

<!-- Your rate against the staff set, and every disagreement adjudicated.

     Remember you labelled these 30 under the STAFF taxonomy in
     data/staff_taxonomy.md, not your own — so every argument below is made
     from those definitions and those decision rules. -->

**Agreement rate:** ___ / 30 = ___%

<!-- Nobody grades this number. A 60% who argues every disagreement from the
     stated rules beats a 95% who wrote "staff was right" nine times. Several
     of the 30 were chosen because they're genuinely ambiguous — you should be
     winning some of these. -->

**Disagreements**

<!-- Three lines each: the post, both labels, and who you think is right and
     why — grounded in the staff definitions you were both applying.

     Then sort each into one of three piles:
       (a) the rule covered it and I applied it loosely → a consistency problem
       (b) the rule genuinely doesn't say               → a gap in the definitions
       (c) the rule is ambiguous here and my reading is defensible → argue it.
           This is a legitimate win.

     Pile (a) is the one that matters most for your diagnosis: if you applied a
     written rule two different ways on 30 posts, that is direct evidence about
     what you did across your own 200. -->

**1.**
> *The post:*
>
> *Staff said / I said:*
>
> *My call, and why:*
>
> *Which pile:*

**2.**
> *The post:*
>
> *Staff said / I said:*
>
> *My call, and why:*
>
> *Which pile:*

**What the pattern in my disagreements tells me:**



---

## The Improvement

**What I changed:**

**Which diagnosis pointed at it:**

### Run Log — After

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1.  |  |  |  |  |  |
| 2.  |  |  |  |  |  |
| 3.  |  |  |  |  |  |
| 4.  |  |  |  |  |  |
| 5.  |  |  |  |  |  |

**Did it help, and how do I know:**

<!-- If it didn't, say so. Relabelling that didn't help is a genuinely
     interesting result and earns full credit. -->



---

## What's Still Broken

<!-- For each criterion still missed: what you'd do, and why you stopped. -->



**The gap between what I meant my labels to capture and what the model
learned:**
<!-- Two sentences. Your confusion matrix is the evidence. -->



<!-- ═════════════════════════════════════════════════════════════════════

     SUBMISSION CHECKLIST — unit 5

       [ ] criteria.md has five numbered criteria, each naming a NUMBER
       [ ] Each has a reason underneath tied to your data or taxonomy
       [ ] labels.csv: at least 150 rows, text/label/note, ONE file not split
       [ ] No label above 70%
       [ ] All five unit 5 sections have real content
       [ ] Label Taxonomy includes the decision rule for your hardest boundary
       [ ] The Dataset includes three hard cases
       [ ] results.json and test_split.csv committed (the notebook does this)
       [ ] At least four new commits
       [ ] Repository URL submitted — WRITE IT DOWN

     SUBMISSION CHECKLIST — unit 6

       [ ] Baseline vs. Trained table, with your prediction written beforehand
       [ ] Run Log — Before, five criteria across three seeds
       [ ] Confusion matrix TYPED AS A MARKDOWN TABLE
       [ ] A verdict on every criterion
       [ ] A diagnosis for every miss, using the agreement report as evidence
       [ ] Agreement Report with every disagreement adjudicated
       [ ] One improvement, with Run Log — After
       [ ] What's Still Broken
       [ ] results_three_seeds_before.json, results_three_seeds_after.json,
           baseline_results.json and
           agreement_results.json committed
       [ ] At least four new commits
       [ ] The SAME repository URL as last unit

     Do not delete and recreate this repository.
     ═════════════════════════════════════════════════════════════════════ -->

---

📖 **How to run this project: [RUNNING.md](RUNNING.md)**
