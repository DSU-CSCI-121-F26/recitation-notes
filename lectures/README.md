# Lecture Slides

Slides from every lecture, by week. **CSCI-121 · Fall 2026**

Decks are posted as PDFs so they open in the browser — click any file below and GitHub
renders it, no download needed. **Some weeks have no deck at all** — the syntax weeks are
live-coded on purpose. Those weeks post the handout instead, and the handout is the
scaffold.

> These are the slides, not a transcript. They are a scaffold for what was said in the room,
> and they are **not a substitute for being there**. What is on them is the skeleton; the
> examples worked on the board are not.

---

## Week 1 · Aug 24–28 — What an object is

*No Java syntax this week — that is deliberate. What is new coming from Python is not `for`
loops, it is deciding what should be an object at all.*

| Day | Deck | Handout | Covered |
|---|---|---|---|
| **Tue Aug 25** | [Day 1 — What an Object Is](week01/CSCI-121-Week1-Day1.pdf) | [handout](week01/handout-day1.md) | Identity, state, behavior · decomposing a problem into objects · your first class diagram |
| **Thu Aug 27** | [Day 2 — One Reason to Change](week01/CSCI-121-Week1-Day2.pdf) | [handout](week01/handout-day2.md) | Single Responsibility · reading a real class diagram (BRACE) · `git add` / `commit` / `push` |

---

## Week 2 · Aug 31–Sep 4 — Java for Python programmers

> **There is no deck this week, and that is on purpose.** Both days are live-coded — Java
> typed and run in front of you, which is the one thing a slide cannot do and the thing you
> actually need coming from Python. The handouts below are what the lecture is built
> around, so they carry more than usual. **Print one and bring it.**

| Day | Deck | Handout | Covered |
|---|---|---|---|
| **Tue Sep 1** | *live-coded* | [handout](week02/handout-day1.md) · [print version](week02/handout-day1.pdf) | Static types · primitives vs references · the box-and-arrow model · **`==` vs `.equals()`** |
| **Thu Sep 3** | *live-coded* | [handout](week02/handout-day2.md) · [print version](week02/handout-day2.pdf) | Strings · casting chops but formatting rounds · `javac` → `.class` → JVM · **Q1 in the first ten minutes** |

**Both handouts have a predict-then-run table.** Fill it in *before* the answer goes on the
screen — being wrong on paper is free, and being wrong on Thursday's quiz is not.

Day 1's last page is an **exit ticket you tear off and hand in**. Keep the rest.

---

## Coming weeks

Material goes up here as each week arrives — a deck when there is one, the handout always.
See **[SCHEDULE.md](../SCHEDULE.md)** for what is coming, what to read, and when things are
due.

---

## The through-line

Everything in this course runs on one pipeline. You will see it in every week's slides:

> **The diagram specifies structure → the test specifies behavior → the code satisfies both.**

A model can write the code. It cannot write your spec, and it cannot verify itself.
