# CSCI-121 — Recitation Notes (Fall 2026)

Student-facing notes from each recitation for **CSCI-121**, Dakota State University.

Each file is a self-contained write-up of what we covered in that session, plus corrections and
clarifications on anything I explained quickly in the moment. Where a note is marked
**Correction**, the in-class version was a useful first approximation but not precisely right —
read those carefully.

---

## Start here

| | |
|---|---|
| 📅 **[Schedule, Readings & Due Dates](SCHEDULE.md)** | Every reading, lab, drill, quiz, and deadline for the whole semester, on one page. **Bookmark this.** |

---

## Recitation notes

| # | Recitation | Topics |
|---|---|---|
| 00 | [Setup, Git, and Your First Java Program](recitation-00-setup-git-first-java-program.md) | Class logistics, fork & clone, terminal commands, `~/dev` layout, twelve-factor app, TCP/UDP and application protocols, Maven & IntelliJ, classes and access modifiers, stack vs. heap, `public static void main`, Assignment 00 |

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
