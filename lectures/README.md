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

> **This week is live-coded.** Java typed and run in front of you, which is the one thing a
> slide cannot do and the thing you actually need coming from Python. There are slides for
> both days, but they are a scaffold — **the code repo and the terminal are the real record
> of the lecture.** Print the handout and bring it.

| Day | Deck | Handout | Covered |
|---|---|---|---|
| **Tue Sep 1** | [Day 1 — What a Variable Actually Holds](week02/CSCI-121-Week2-Day1.pdf) | [handout](week02/handout-day1.md) · [print version](week02/handout-day1.pdf) | Static types · primitives vs references · the box-and-arrow model · **`==` vs `.equals()`** |
| **Thu Sep 3** | [Day 2 — What “Compiled” Actually Means](week02/CSCI-121-Week2-Day2.pdf) | [handout](week02/handout-day2.md) · [print version](week02/handout-day2.pdf) | Strings are immutable · casting chops but formatting rounds · `javac` → `.class` → JVM · **no quiz — Q1 is Tue Sep 8** |

> ### 📘 Day 1 — the code and the study guide
>
> Everything typed in Tuesday's lecture is in
> **[DSU-CSCI-121-F26/lecture-week02-day1](https://github.com/DSU-CSCI-121-F26/lecture-week02-day1)**.
> Fork it, run it, break it.
>
> **Start with the [Study Guide](https://github.com/DSU-CSCI-121-F26/lecture-week02-day1/blob/main/STUDY-GUIDE.md)**
> — the lecture written up in the order we did it, **the six traps where the obvious answer
> is the wrong one**, and the list of terms to study for Q1.

> ### 💻 Day 2 — the deck is a transcript, not a replacement
>
> Thursday happened **in a terminal**. The dark panels in the Day 2 deck are exactly what
> those commands printed on the projector — `javac`, `xxd`, `javap -c`, `java Hello`, and
> the `int x = "hi";` that fails to compile and therefore produces **no `.class` file at
> all**. They are there so you can replay the sequence at home.
>
> **Replay it.** Type the four lines of `Hello.java` into an empty folder and run the
> commands in order. Reading the slide takes thirty seconds and teaches you nothing; doing
> it takes four minutes and you will never again wonder what the green triangle in IntelliJ
> is actually doing.

**Both handouts have a predict-then-run table.** Fill it in *before* the answer goes on the
screen — being wrong on paper is free, and being wrong on Q1 is not.

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
