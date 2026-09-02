# CSCI-121 · Week 2, Day 2

**Name _______________________________  Section (circle):  R3 Mon  /  R4 Wed**

---

## The rule from today

> **Casting truncates. Formatting rounds. Choose on purpose.**

```java
double v = 3.999;

(int) v                      // 3
String.format("%.0f", v)     // "4"
```

---

## Strings — the set worth memorising

| Java | Python |
|---|---|
| `s.length()` | `len(s)` |
| `s.charAt(i)` | `s[i]` |
| `s.substring(a, b)` | `s[a:b]` — stops **before** `b` |
| `s.equals(t)` | `s == t` |
| `s.toUpperCase()` | `s.upper()` |
| `s.trim()` | `s.strip()` |
| `s.contains(t)` | `t in s` |

**No negative indexing.** The last character is `s.charAt(s.length() - 1)`.

**Every one of these returns a new String.** None of them change the one you had.

---

## Predict, then we run it

| | Code | Your prediction |
|---|---|---|
| 1 | `String s = "hi"; s.toUpperCase(); print(s);` | |
| 2 | `print("hello".substring(0, 3));` | |
| 3 | `print("hello".charAt(4));` | |
| 4 | `print((int) 2.99);` | |
| 5 | `print(String.format("%.0f", 2.99));` | |
| 6 | `print(((int)(1.4815 * 100)) / 100.0);` | |
| 7 | `print(((int)(1.4815 * 100)) / 100);` | |

**6 and 7 differ by one character.** Say why:

<br>

_______________________________________________________________________

---

## The two-decimal trick — SB1 needs this

```java
double v = 1.4815297665908702;
double t = ((int)(v * 100)) / 100.0;
```

Fill in each step:

| Step | Expression | Value |
|---|---|---|
| 1 | `v * 100` | |
| 2 | `(int)(v * 100)` | |
| 3 | `... / 100.0` | |

---

## `printf` vs `String.format`

```java
System.out.printf("%.2f%n", v);          // ______________________________
String out = String.format("%.2f", v);   // ______________________________
```

Which one would you use inside a method that has to **return** the text?

<br>

_______________________________________________________________________

---

## Compiling — what the terminal showed us

```bash
javac Hello.java
```

**What new file appeared?** ______________________

**Is it for you to read?** ______________________

**The first four bytes of every Java class file ever compiled:** ______________________

```bash
java Hello
```

**Why is there no `.java` or `.class` on that command?**

<br>

_______________________________________________________________________

### Compile time vs run time

| | When it happens | Example |
|---|---|---|
| **Compile time** | | |
| **Run time** | | |

---

## `TimeUtils` — with your neighbour

3725 seconds. Fill in the blanks so this returns `01:02:05`.

```java
public static String formatTime(int totalSeconds) {

    int hours   = totalSeconds ______ 3600;

    int rem     = totalSeconds ______ 3600;

    int minutes = rem ______ 60;

    int seconds = rem ______ 60;

    return String.format("%02d:%02d:%02d", hours, minutes, seconds);
}
```

**`3725 / 3600` is `1`, not `1.03`.** Here integer division is not something you are
working around — it is the tool. Why?

<br>

_______________________________________________________________________

---

## Exit ticket — hand this in at the door

**1.** `(int) 2.99` and `String.format("%.0f", 2.99)` — give both answers.

<br>

**2.** You run `javac` and get an error. How many `.class` files were produced?

<br>

**3.** One thing from Tuesday that makes more sense now than it did on Tuesday.

<br>

_______________________________________________________________________

---

## This week and next

| | |
|---|---|
| **Skill Builder 1** | **Sun Sep 13, 11:59 PM** — today was its content |
| **Drills** — Asterisks · Show me the Numbers | **Sun Sep 6, 11:59 PM** |
| **Recitation 2** — finish at home, push, open the PR | **Sun Sep 6, 11:59 PM** |
| Reading — Think Java **Ch 2**, **Ch 3** | |
| **§6.10** *String Comparison* · **§9.3** *Strings Are Immutable* | the two sections that cover today and Tuesday |

> **R3 — no section on Mon Sep 7. Labor Day.** Your next section is **Sep 14**, and SB1 is
> due Sep 13. Use office hours and tutoring, and re-read **Recitation 2 exercises 6, 7 and
> 8** — they are SB1's spine.
