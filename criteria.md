# Acceptance criteria — TakeMeter

Five criteria that say what "working" means for this classifier, written in
unit 5 **before** anything was trained.

**All five are yours this time.** None are given. You've had two projects of
practice.

An acceptance criterion names a number. *"The model is accurate"* is an
opinion. *"Every label has an F1 of at least 0.60 on the held-out set"* is a
criterion.

Under each, write a sentence or two on **why that number**. A reason that says
something about your data or your taxonomy earns credit — *"I picked 0.60 F1
for `reaction` because it's my smallest label and I only have about 50
examples of it"*. A reason that could be attached to any project does not.

> Missing your own targets next unit costs you nothing. Setting a target so
> easy you can't miss it does.

---

## Pick numbers you can defend

Not numbers that sound impressive. Three labels means a coin-flip guesser gets
about 33%, so a target of 0.40 is barely a target. Your number should sit
somewhere you'd honestly call useful.

**Cover at least three of these five areas.** They're here as prompts, not as a
form to fill in — a criterion that fits none of them is fine if it names a
number.

| Area | A question it could answer |
|---|---|
| Overall accuracy | How often does it need to be right to be worth using? |
| Per-label performance | Is one label allowed to be much worse than the others? |
| Balance | How lopsided can your label counts get before it's a problem? |
| Consistency | If someone else labelled the same posts, how often should you agree? |
| Confidence | Should a confident prediction be right more often than an unsure one? |

Two things worth knowing before you pick numbers, because both will affect
whether you hit them:

- **Your smallest label will have the jumpiest score.** If a label has 50
  examples, about 8 land in the test split. An F1 computed on 8 examples moves
  a lot between seeds. A target for that label should be looser than one for
  your biggest label, and saying so is a good reason.
- **Unit 6 tests across three seeds, and the target has to hold across all
  three.** A target of 0.65 against results of 0.71, 0.62, 0.68 is a **miss**.
  Pick with that in mind — it is stricter than it first sounds.

---

## 1.

Every label has an F1 of at least 0.55 on the held-out test split.

**Why this target:** With four labels, random guessing scores about 0.25 per label, so 0.55 is clearly better than chance. I am aiming for about 150 labeled posts, so the test split will be about 22 posts and my thinnest label (`argued_opinion`, 16 examples) will have only about 2 or 3 of them, so one post moves its recall by 33 to 50 points and its score will swing between seeds, which is why I'm not setting the bar higher and why I expect this target may miss.

---

## 2.

Overall accuracy on the held-out test split is at least 75%.

**Why this target:** Random guessing gets about 25%, but always guessing my biggest label, `question`, would get about 65%, so a score only slightly above that would not show the model learned anything. 75% is 10 points above that baseline. It is deliberately ambitious: `personal_share` vs. the opinion labels and `question` vs. the opinion labels are fuzzy boundaries, and I expect to miss it if my labels are noisy. With about 22 test posts, one post is about 4.5 points, so I know the score will move between seeds.

---

## 3.

The smallest label has at least 15 examples in `labels.csv`.

**Why this target:** After collecting 150 posts, my thinnest label, `argued_opinion`, has 16 examples, and I could not add more without removing the `question` posts that make up most of what r/ExperiencedDevs actually posts. 15 is the lowest I would accept: with 15% of the data in the test split, that is only about 2 or 3 test posts, so I know that label's score will be noisy. I first wanted 40, but 4 labels x 40 would need 160 posts with none above 70%, which my community does not have. I am setting the floor at what my data supports, and saying so now, before training.

---

## 4.

When I label the staff's 30-post set, I agree with the staff label on at least 20 of 30.

**Why this target:** 20 of 30 is about 67%. My decision rule is new, and the staff set includes deliberately ambiguous posts, so I am not aiming for near-perfect agreement. I want to find out where my rule is loose.

---

## 5.

On the test split, the half of predictions with the highest confidence is more accurate than the lowest-confidence half by at least 10 points.

**Why this target:** A confident prediction should be right more often than an unsure one. The test split is about 22 posts (15% of about 150), so each half is about 11 and one post moves accuracy by about 9 points. A gap under about 10 points is within one post and could be luck.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     UNIT 6 — read this before you change anything above.

     If a criterion turns out to be BROKEN rather than merely unmet, you can
     revise it, and that earns credit. But never delete or edit the original
     line. Add the revision underneath, like this:

         ## 2. Every label performs acceptably

         The model performs well on all labels.

         **Why this target:** ...

         > **Revised in unit 6:** Every label has an F1 of at least 0.60 on
         > the held-out set.
         >
         > **Why revised:** "performs well" gave me nothing to check. I
         > couldn't produce a verdict from it at all.

     That's a revision because the criterion couldn't be MEASURED.

     Lowering a target because you missed it is not a revision, and it costs
     you the point:

         ✗ "Overall accuracy of at least 0.65" → "at least 0.55", because
            0.65 turned out to be optimistic for 200 examples.

     A number you missed stays where it is, gets diagnosed, and gets a fix
     attempted. That's where the points are.
     ───────────────────────────────────────────────────────────────────────── -->
