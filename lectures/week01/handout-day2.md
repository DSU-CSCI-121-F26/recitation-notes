# CSCI-121 · Week 1, Day 2

**Name _______________________________  Section (circle):  R3 Mon  /  R4 Wed**

---

## The rule

> **A class should have one reason to change.**

**The test:** say out loud everything the class does. Count how many *different* forces
would make you edit it. More than one means it should probably be more than one class.

---

## Warm-up — `TicketOffice`

List what it does:

| # | It... | Reason you would edit it |
|---|---|---|
| 1 | | |
| 2 | | |
| 3 | | |
| 4 | | |

**How many reasons to change? _______**

**How would you split it?**

<br><br>

---

## Reading a diagram

| Shape | Means |
|---|---|
| Box, three compartments | a class — name, state, behavior |
| Solid arrow, hollow head | "is a" — points at the **parent** |
| Dotted arrow, hollow head | "fulfils a contract" |
| Filled diamond | "owns" — destroy the owner, this dies too |
| Hollow diamond | "has" — this outlives the owner |

From the BRACE diagram on screen, write these as plain-English sentences:

`RobotController <|-- MazeRobot` → ____________________________________________

`RobotController *-- SensorCache` → ___________________________________________

---

## Drawing it — draw.io

**[app.diagrams.net](https://app.diagrams.net)** — nothing to install, no account needed.

1. Left panel → **Shape Search** → type `class` → drag the three-compartment UML class shape
   onto the canvas
2. Double-click each compartment to fill it in

```
┌──────────────────────┐
│       Ticket         │   ← name
├──────────────────────┤
│ - seat: String       │   ← state    ( - private,  + public )
│ - scanned: boolean   │
├──────────────────────┤
│ + scan(): void       │   ← behavior
└──────────────────────┘
```

**Saving it into your repo — the one step people get wrong:**

> **File → Export as → PNG**, tick ☑ **"Include a copy of my diagram"**, save it next to
> `design.md` as `diagram.drawio.png`

That checkbox is what lets you re-open the PNG in draw.io later and keep editing. Without it
you have a flat picture and no way back.

Then add this one line to `design.md`:

```markdown
![Class diagram](diagram.drawio.png)
```

---

## Selling tickets at a home game

> Fans buy tickets for a game. Every ticket is for one specific seat in one section, and it
> gets scanned once at a gate on the way in. Students pay less if they show a student ID.
> Staff need to know how many seats are still unsold in each section, and how many people
> are actually inside.

**1. The objects.**

<br><br><br>

**2. Fill in your best three.**

| | Object 1 | Object 2 | Object 3 |
|---|---|---|---|
| Name | | | |
| Identity | | | |
| State | | | |
| Behavior | | | |

**3. Apply the test.** Is any one of them doing more than one job?

Which one: ______________________  Split it into: ______________________________

**4. Now open draw.io.** Draw your best two, connect them with an arrow, and label the arrow
in plain English.

> **Decide here, draw there.** Steps 1–3 stay on this page. Open the tool only when you know
> what your objects are — otherwise you will spend the time moving boxes around instead of
> thinking.

---

## Your first push

Three of these four boxes are **on your laptop**. Only the last one is me.

```
working directory ──add──▶ staging ──commit──▶ local repo ──push──▶ GitHub
 (you edited it)          (marked)            (on your laptop)     (I can see it)
```

```bash
git status                                    # run this constantly
git add .                                     # BOTH files — the .md and the .png
git commit -m "Add ticket sales class diagram"
git push
```

**`git add .`, not `git add design.md`.** You are committing two files now. Stage only the
Markdown and your diagram will show up on GitHub as a broken image.

**Drew it on your partner's laptop?** You each hand in your own repo, so you each need the
PNG in your own. Send it to yourself — AirDrop, email, a shared drive — or export it a second
time from their screen straight into your folder. Do this **now**, in class, not tonight when
you no longer have their laptop.

**When `push` asks for a password, your GitHub password will not work.** It wants a
**Personal Access Token**:

> GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)
> → Generate new token → check `repo` → **copy it now, it is shown once**

Paste the token where it asks for a password.

`Authentication failed` tonight = the token. Nothing else is broken.

**Committed is not submitted.** If you did not push, the gradebook sees nothing.

---

## Exit ticket — hand in on your way out

Find a class in the BRACE diagram with **one** clear responsibility.

Class: ______________________

Its one responsibility, in a sentence:

<br><br>

---

**Section this week:** Recitation 0. **Laptop + GitHub username required.**

**Tonight:** Assignment 00 pushed, if it is not already. Read the Recitation 00 notes —
the three sections marked **Correction** especially.
