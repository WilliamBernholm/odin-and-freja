# Odin & Freja

Two [Claude Code](https://claude.com/claude-code) skills that turn a course's
own materials into a Socratic quiz tutor and a homework generator.

- **Freja** (student-facing) — a Socratic quiz engine. You pick a lecture, a
  textbook chapter, or a homework problem; Freja walks you through it one
  question at a time and scaffolds hints until *you* reach the answer. It
  does not hand over solutions.
- **Odin** (teacher-facing) — a homework generator. It reads your existing
  lectures, chapters, and assignments, then writes genuinely new problems —
  either mimicking the style and difficulty of an existing homework, or
  applying a course technique to a new applied scenario in a subject you
  choose.

**This repo contains no course material.** It is the two skills and nothing
else. You supply your own content.

---

## Credit — this is a rework of MiLLy

Both skills descend from **MiLLy**, the Mastery Learning Loop skill created by

> **Richard James Glassey** — KTH Royal Institute of Technology, Stockholm
> · glassey@kth.se
> Implemented at KTH as part of the **AI First Programming** initiative.

MiLLy is the original and the pedagogical core. The Mastery Learning Loop
itself — skill analysis, then **Conceptual → Procedural → Predictive →
Corrective → Transfer**, one question at a time, inspired by Bloom's mastery
learning — is his design, and Freja preserves it stage for stage.

**What was changed here is not the pedagogy.** MiLLy works against a single
task and its solution. The rework makes the same loop run against a **course
folder structure** — `Lectures/`, `Literature/`, `Homeworks/` — so a student
can point it at "lecture 6" or "HW2 problem 3" and it finds the material
itself. That is the whole idea: a layout simple enough that students can drop
in a course and start using it. Odin then extends the same core in the other
direction, generating homework rather than quizzing on it.

If you find this useful, the credit for the underlying method belongs to
Richard Glassey.

---

## Setup

**1. Install Claude Code** (needs a Claude subscription; no API key):

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

On Windows PowerShell:

```powershell
irm https://claude.ai/install.ps1 | iex
```

Reopen your terminal afterwards, run `claude`, and log in with your Claude
account.

**2. Get the skills** — either clone this repo and use it as your course
folder:

```bash
git clone https://github.com/WilliamBernholm/odin-and-freja.git
```

…or copy the `.claude/` folder into a course folder you already have.

**3. Add your course content** (see the structure below).

**4. Run `claude` from inside that folder.** This matters — Claude Code only
picks up `.claude/skills/` when started from the folder that contains it.

---

## Folder structure

Everything is discovered by folder name. Put your files in these three
folders and both skills will find them:

```
your-course/
├── .claude/
│   ├── settings.json          <- pre-approves both skills (from this repo)
│   └── skills/
│       ├── freja/SKILL.md     <- the student quiz engine
│       └── odin/SKILL.md      <- the homework generator
│
├── Lectures/                  <- your lecture notes, one markdown file per lecture
│   ├── 01_introduction.md
│   ├── 02_fourier_transforms.md
│   └── ...
│
├── Literature/                <- your textbook chapters, one markdown file per chapter
│   ├── Chapter_1_....md
│   └── ...
│
└── Homeworks/                 <- your assignments — markdown or PDF, both work
    ├── HW1/HW1.pdf                (nested layout)
    ├── HW2.pdf                    (or bare — both are handled)
    ├── data.csv                   (any starter files students need)
    └── solutions/                 (optional — official answer keys, if you have them)
```

Things worth knowing about this layout:

- **Only the folder names are a convention.** File names inside them are
  yours — both skills `glob` for whatever is actually on disk rather than
  assuming a naming pattern.
- **Nothing is mandatory.** Have only lectures? Freja quizzes on lectures.
  No answer keys? Freja quizzes anyway, checking your reasoning against the
  source material instead.
- **Markdown works best** for `Lectures/` and `Literature/`, because the
  skills read and quote your exact notation from them. PDFs are read fine in
  `Homeworks/`.
- **Odin writes into `Homeworks/`**, never over your files:
  - `Homeworks/Generated/` — mimic-mode output
  - `Homeworks/<Domain>/` — applied-mode output, named after whichever
    subject you picked (`Biomedical/`, `Aerospace/`, whatever you choose)

---

## Using Freja (students)

Just ask, in plain English:

> Quiz me on lecture 6

> Quiz me on the compressed sensing chapter

> Quiz me on HW1 problem 4

Freja resolves what you meant, reads the source material, and starts the
loop — **one question at a time**:

| Stage | What it asks |
|---|---|
| Conceptual | the WHAT — definitions, meaning, why it matters |
| Procedural | the HOW — the steps, the method |
| Predictive | tracing outcomes and consequences |
| Corrective | spotting and fixing flawed reasoning |
| Transfer | applying it to a related but new problem |

It gives feedback after each answer, escalates hints if you're stuck, and
won't produce a submittable solution for you — if you ask it to just write
the answer, it will keep scaffolding instead.

## Using Odin (teachers)

> Generate a new HW2-style problem about hierarchical clustering

> Generate a new applied problem based on lecture 5

Odin will not write anything until you've agreed on what it's writing. It
walks through:

1. **Deep research?** — it offers, up front, to ground the scenario in real
   missions/papers/data via web search.
2. **Five scenario alternatives** — in-depth and distinct, not variations of
   one idea. You pick.
3. **Which subject domain?** — never assumed. Aerospace, biomedical,
   finance, anything, or "no domain, keep it abstract."
4. **Starter code?** — whether students get a skeleton, and how sparse it
   should be.
5. **A short summary to confirm** — topic, theory tested, application.

Then it writes: the problem file, a **separate** solution file (never inline),
a LaTeX twin of each document, a difficulty rating with an ordered concept
map, a **runnable solution script it actually executes to verify**, and a
Freja-safe practice file — extra questions on the same technique in a
different scenario, so students can be quizzed without the real answer key
ever entering the tutor's context.

---

## Bring your own content

This repo ships **no** lecture notes, textbook chapters, homework problems,
or solutions — deliberately. Whatever you add is yours, and checking that
you have the right to use it (textbook chapters in particular are usually
copyrighted) is your responsibility, not this repo's.

## A note on AI use and correctness

- Both skills default to **study mode**: Socratic questioning only, never a
  final solution a student could submit as their own work. If your course's
  lecture notes state their own AI-use or academic-integrity policy, both
  skills look for it and follow that instead.
- **Odin's answer keys are LLM-authored and need a human check.** They are
  new teaching material, not verified truth. Odin runs its solution scripts
  to check they execute, but that is not the same as the mathematics being
  right. Spot-check before putting anything in front of students.

## License

MIT — see [LICENSE](LICENSE). The MIT license covers the skill files in this
repo. It does not extend to MiLLy, to any course content you add, or to
anything either skill generates from that content.
