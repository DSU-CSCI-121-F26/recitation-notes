# CSCI-121 — Recitation Notes (Fall 2026)

Student-facing notes from each recitation for **CSCI-121**, Delaware State University.

Each file is a self-contained write-up of what we covered in that session, plus corrections and
clarifications on anything I explained quickly in the moment. Where a note is marked
**Correction**, the in-class version was a useful first approximation but not precisely right —
read those carefully.

**Some notes go up before the session rather than after.** Recitations are assignments that
*start* in class and are *finished at home*, so the notes for those are published early — you
need them for the half you do on your own. They are updated with corrections once both
sections have met.

---

## Start here

| | |
|---|---|
| 📅 **[Schedule, Readings & Due Dates](SCHEDULE.md)** | Every reading, lab, drill, quiz, and deadline for the whole semester, on one page. **Bookmark this.** |
| 🎞️ **[Lecture Slides](lectures/)** | Every deck, by week, as PDFs that open right in the browser. |

---

## Recitation notes

| # | Recitation | Topics |
|---|---|---|
| 01 | [Setup, Git, and Your First Java Program](recitation-01-setup-git-first-java-program.md) | Class logistics, fork & clone, terminal commands, `~/dev` layout, twelve-factor app, TCP/UDP and application protocols, Maven & IntelliJ, classes and access modifiers, stack vs. heap, `public static void main`, Assignment 00 |
| 02 | [Java for Python Programmers](recitation-02-java-for-python-programmers.md) | Integer division and truncation toward zero · `+` as join vs. add · `char` arithmetic and casting · **`==` vs. `.equals()`** · Strings are immutable · casting chops but formatting rounds · `length`/`charAt`/`substring` · the full Python-to-Java table |

---

## Repositories you will need

Every one of these is public. **Fork, then clone** — the workflow is in
[Recitation 01](recitation-01-setup-git-first-java-program.md).

| Repo | What it is | Due |
|---|---|---|
| [**Drills — Week 2**](https://github.com/DSU-CSCI-121-F26/Drills-Week02) | Asterisks · Show me the Numbers | **Sun Sep 6** |
| [**Recitation 2**](https://github.com/DSU-CSCI-121-F26/recitation2) | Java for Python programmers — 8 exercises, 42 tests | **Sun Sep 6** |
| [**Skill Builder 1**](https://github.com/DSU-CSCI-121-F26/SkillBuilder1) | Input, output, variables, casting | **Sun Sep 13** |
| [Recitation 0](https://github.com/DSU-CSCI-121-F26/recitation0) | Git, IntelliJ, Maven, your first Java program | *done — Sun Aug 30* |
| [Robocode Arena](https://github.com/DSU-CSCI-121-F26/robocode-arena) | Optional, runs all semester. Never graded | — |

> **Every deadline is Sunday 11:59 PM.** The full list, including the two exceptions, is in
> **[SCHEDULE.md](SCHEDULE.md)**.

---

## How to use these notes

- Read the notes for a session **before** the next class — assignments are listed at the end of each file.
- Every note ends with a **Quick Reference** section (git commands, terminal commands, glossary).
- Deadlines live in **[SCHEDULE.md](SCHEDULE.md)**, not in the individual notes. If the two ever
  disagree, the schedule is right.
- Found a mistake or something unclear? Open an issue or a pull request on this repo.

## The one thing that costs people points

Committing saves your work **on your laptop**. Only `git push` makes it exist for me.

```bash
git status                      # run this constantly
git add <file>
git commit -m "what changed"
git push                        # <- the one people forget
```

Then refresh the page on GitHub and *look at it*. The work is not done until you have seen it
on the server.

## Repository

<https://github.com/DSU-CSCI-121-F26/recitation-notes>
