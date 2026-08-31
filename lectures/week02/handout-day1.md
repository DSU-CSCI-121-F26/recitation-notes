# CSCI-121 · Week 2, Day 1

**Name _______________________________  Section (circle):  R3 Mon  /  R4 Wed**

---

## The two rules from today

> Java widens for free. Java **never** narrows without a cast.

> `==` for primitives. `.equals()` for everything else.

---

## The eight primitives

Everything else in Java is a reference.

`byte`  `short`  `int`  `long`  `float`  `double`  `char`  `boolean`

Lowercase, always. **If the type starts with a capital letter, the variable holds an arrow.**

---

## Predict, then we run it

Write your answer *before* it goes on the screen. Being wrong here is free; being wrong
in three weeks is not.

| | Code | Your prediction |
|---|---|---|
| 1 | `System.out.println(7 / 2);` | |
| 2 | `System.out.println(7 / 2.0);` | |
| 3 | `int x = 3.9;` | |
| 4 | `int x = (int) 3.9;` | |
| 5 | `char c = 'A'; System.out.println(c + 1);` | |
| 6 | `System.out.println("" + 1 + 2);` | |
| 7 | `System.out.println(1 + 2 + "");` | |

---

## Draw the boxes

```java
int n = 5;
String s = "hi";
```

Draw what `n` holds and what `s` holds. One of them has an arrow in it.

<div class="draw"></div>

---

## The one that matters

```java
int[] x = {1, 2, 3};
int[] y = x;
y[0] = 99;
System.out.println(x[0]);
```

**Prediction:** ______________

**What actually happened, and why — one sentence:**

<div class="write"></div>

_______________________________________________________________________

<div class="write"></div>

_______________________________________________________________________

---

## `==` and `.equals()`

```java
String a = "hi";
String b = new String("hi");
String c = "hi";
```

| | Answer | Why |
|---|---|---|
| `a == b` | | |
| `a.equals(b)` | | |
| `a == c` | | |

**The last row is the dangerous one.** In one sentence, why is it dangerous to rely on?

<div class="write"></div>

_______________________________________________________________________

---

## This week

| | |
|---|---|
| **Q1 — Thursday**, 10 min, start of class, on paper, no notes | data types, operators, strings |
| **Recitation 2** — finish at home, push, open the PR | **Sun Sep 6, 11:59 PM** |
| **Drills** — Asterisks · Show me the Numbers | **Sun Sep 6, 11:59 PM** |
| **Skill Builder 1** | **Sun Sep 13, 11:59 PM** |
| Reading — Think Java **Ch 2**, **Ch 3**, **§6.10**, **§9.3** | nothing tracks it; look things up |

**Everything on Thursday's quiz is in Recitation 2.** If your tests are green, you have
studied.

---

<div class="pagebreak"></div>

## Exit ticket — tear this off and hand it in at the door

**Name _______________________________  Section (circle):  R3 Mon  /  R4 Wed**

*Keep the other pages. This one is mine.*

**1.** `int x = 7 / 2;` — what is `x`?

<div class="write"></div>

**2.** Draw the box for `int n = 5;` and the box for `String s = "hi";`

<div class="draw"></div>

**3.** Two strings print the same text. `==` says `false`. In one sentence, why?

<div class="write"></div>

_______________________________________________________________________

---

