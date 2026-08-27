# CSCI-121 · Week 1, Day 2

**Name _______________________________  Section (circle):  R3 Wed  /  R4 Fri**

---

## The rule

> **A class should have one reason to change.**

**The test:** say out loud everything the class does. Count how many *different* forces
would make you edit it. More than one means it should probably be more than one class.

---

## Warm-up — `FleetManager`

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

## The bike share

> Bikes live at docking stations. A student unlocks a bike with their ID, rides it, and
> returns it to any station. Bikes need maintenance after a set number of rides. Staff
> need to know which stations are empty or full.

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

**4. Draw two of them. Connect them with an arrow and label it in plain English.**

<br><br><br><br><br><br>

---

## Your first push

Three of these four boxes are **on your laptop**. Only the last one is me.

```
working directory ──add──▶ staging ──commit──▶ local repo ──push──▶ GitHub
 (you edited it)          (marked)            (on your laptop)     (I can see it)
```

```bash
git status                                    # run this constantly
git add design.md
git commit -m "Add bike share class diagram"
git push
```

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
