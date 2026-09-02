# Recitation 02 — Java for Python Programmers

**Student Notes**

> **Recitation 2 starts in section and you finish it at home**, so these notes cover the
> whole lab — including the exercises we did not reach together. **R3 met Monday Aug 31**
> and the recording is below. **R4:** your section is Wednesday Sep 2, and nothing here is
> spoiled by reading it first.

> ### 📹 The recording — R3, Monday Aug 31
>
> **Webex:** CSCI-121 Symposium-20260831 1852-1
> <https://desu.webex.com/desu/ldr.php?RCID=610578d95d471003064a1fee9f218dc6>
>
> **The password is posted in Canvas**, with this link, in the Recitation 2 announcement.
>
> Worth rewatching if you missed it, if your screen share failed, or if you want the
> `nextLetter` cast walked through again.

As always, where a note says **Correction**, the version I gave in class was a useful
first approximation but not precisely right — read those carefully.

This session has one job: **get Java out of your fingers and onto the screen.** You
already know how to solve every problem in it. You have solved all of them in Python. The
only new thing is saying it in Java, and the five or six places where Java's answer is
*different from Python's answer*.

Repo: <https://github.com/DSU-CSCI-121-F26/recitation2>

---

## What we did together on Monday

We got through **two of the eight exercises** in the room, on purpose — slowly, with
someone driving on a shared screen. **The other six are yours to finish by Sunday.**
Everything you need for them is in the sections below.

### Setup, and why the `dev` folder

```bash
cd ~/dev/student-work
git clone https://github.com/<your-username>/recitation2.git
```

**Fork first, then clone your fork.** Cloning this repo directly gives you something you
cannot push to.

We work inside a `dev` folder for a real reason, and it is an interview answer: **dev/prod
parity.** You want the place you write code to look as much as possible like the place it
eventually runs. That is one of the twelve factors, and "why is your project laid out this
way" is a question you will be asked.

### Unit tests, and why `src/main` and `src/test` mirror each other

A **unit** is one action of work — one method. A **unit test** tests exactly one of them,
not the whole class.

```
src/main/java/recitation/CharArithmetic.java      ← the code you write
src/test/java/recitation/CharArithmeticTest.java  ← the test that checks it
```

They are separated because tests are only needed *before* you ship. They add weight to the
program, so they do not get deployed with it.

> **READMEs and comments go stale. Tests do not.** Code that arrives with no tests is code
> nobody has checked. Treat it accordingly.

**How this is graded:** a script runs the unit tests. You get the percentage that pass. No
interpretation, no partial credit for intent — which also means **you can see your score
before I do.** Run `./mvnw test` and you already know.

### Exercise 3 — `CharArithmetic`

**A `char` is a number.** Every character has a numeric code — `'A'` is **65**, `'a'` is
**97**. That is also why sorting works: `'A'` sorts before `'a'` because 65 is less than 97.

**`letterCode(char c)`** — return an `int` for the character coming in:

```java
public int letterCode(char c) {
    return c;              // char widens to int automatically
}
```

Someone suggested `return 65;` first, and it is worth saying why that was a good move:
**it passed the first test and failed the second.** The test asking about `'a'` caught it
immediately. Hard-coding a value that satisfies one case is exactly what the second test
exists to find.

**`nextLetter(char c)`** — return the *next* letter, so `'A'` comes back as `'B'`:

```java
public char nextLetter(char c) {
    return (char) (c + 1);
}
```

Two things happen on that line and both matter:

1. `c + 1` is an **`int`**, because `char + int` widens. The method promises a `char`, so
   Java stops you — that is the compiler catching a real mismatch, not being difficult.
2. `(char)` is a **cast**: you telling the compiler how to treat the value. It is not a
   calculation.

**The parentheses are PEMDAS.** `(char) (c + 1)` means *do the addition first, then cast
the result*. Writing `(char) c + 1` casts `c` and then adds — different thing.

> **On looking things up:** googling *"java convert int to char"* and reading the answer is
> exactly right, and the AI summary at the top of the results is fine. That is not what
> Tier 0 is about. **Tier 0 means you type the code.** Reading how a language feature works
> is research; having something write the method for you is the part that costs you later,
> when you are asked to explain it.

### Exercise 2 — `Concatenation`

**`joinDigits(int a, int b)`** — two `int`s in, the digits joined as a `String` out. So
`1` and `2` give `"12"`, not `3`.

`a + b` will not do it. Two `int`s with `+` between them is arithmetic, every time. You
have to make them text *before* you join them:

```java
String num1 = String.valueOf(a);
String num2 = String.valueOf(b);
return num1 + num2;
```

You could write it as a one-liner — `return String.valueOf(a) + String.valueOf(b);` — and
that is fine. **The three-line version is easier to read six weeks from now, and readable
wins.** You are not being scored on line count.

### Where that leaves you

| | |
|---|---|
| Done together | **Exercise 3** `CharArithmetic` · **Exercise 2** `Concatenation` |
| Yours by Sunday | The other six — 1, 4, 5, 6, 7, 8 |

**Exercise 4 is `==` versus `.equals()`**, and it is the one that matters most. It is
section 5 below. Do not skim it.

---

## 1. The one sentence to take away

> **Syntax you get wrong is cheap. Semantics you get wrong is expensive.**

If you misspell `System.out.println`, the compiler stops you before the program ever
runs. That mistake costs you fifteen seconds.

If you write `5 / 2` expecting `2.5`, everything compiles, nothing throws, no red
squiggle appears, and your program quietly computes the wrong number forever. That
mistake costs you a grade, or in a job, a customer.

Every one of the eight exercises today was a place where **your Python instinct produces
working Java that gives the wrong answer.** That is why we did them at the keyboard
instead of on a slide.

---

## 2. Integer division

```java
System.out.println(5 / 2);      // 2      -- not 2.5
System.out.println(5 / 2.0);    // 2.5
System.out.println(-7 / 2);     // -3     -- not -4
```

**The rule:** if *both* sides of `/` are `int`, Java does integer division and throws the
fraction away. If *either* side is a `double`, you get a `double`.

The `-7 / 2` case is worth a second look, because Java and Python disagree in a way that
is easy to miss:

| | `-7 / 2` |
|---|---|
| Python (`//`) | `-4` — rounds **down**, toward negative infinity |
| Java | `-3` — truncates **toward zero** |

For positive numbers the two agree, which is exactly why this bites you: it works on
every example you test until it doesn't.

> **Say it precisely.** It is tempting to describe this as "Java rounds down." That is
> wrong, and the `-7` case is why. Java **truncates toward zero** — it deletes everything
> after the decimal point. For positive numbers the two descriptions give the same
> answer, so the shortcut is harmless right up until you hand it a negative number.

### The trap in the fix

```java
double bad  = 5 / 2;      // 2.0  -- divided FIRST, widened after. Too late.
double good = 5 / 2.0;    // 2.5  -- one side is a double before the divide happens
```

Declaring the variable `double` does not help. The division already happened.

---

## 3. `+` is two different operators

```java
"" + 1 + 2      // "12"   -- joins
1 + 2 + ""      // "3"    -- adds, then joins
```

Same numbers, same operators, different answer. Java reads `+` **left to right**, and
the moment one side is a `String`, every `+` after it joins text instead of adding
numbers.

Read the expression out loud from the left and say what each `+` is doing. That is the
whole technique.

---

## 4. A `char` is a number

Python has no `char` type — a single character is just a one-letter string. Java has one,
and it holds **a number**:

```java
char c = 'A';
System.out.println(c + 1);          // 66     -- 'A' is 65
System.out.println((char)(c + 1));  // B
```

`c + 1` produces an `int`. Java widens `char` to `int` on its own, but it will **never**
narrow back for you. Getting a `char` out requires saying `(char)` and taking
responsibility for it.

This came back in the last exercise, where `initials("Jean", "Claude")` returned a
number instead of `"JC"` — because `'J' + 'C'` is arithmetic, not joining. Starting with
`""` fixes it, which is section 3 again.

---

## 5. `==` versus `.equals()` — the big one

**This is the most important thing in these notes.**

```java
String a = "hi";
String b = new String("hi");

a == b          // false
a.equals(b)     // true
```

In Python, `==` compares the text. In Java, `==` on two objects asks **"are these the
same object in memory?"** Two separate objects holding identical text are not `==`.

- **`==`** — same object?
- **`.equals()`** — same contents?

For text, you almost always want `.equals()`.

### Why "almost always" and not "always"

```java
String a = "hi";
String b = "hi";
System.out.println(a == b);   // true
```

Both are *literals*, and Java stores identical literals once and points both names at
that one object. So `==` gives `true` here — and this is the cruel part, because it means
**`==` appears to work** for as long as you only test it with literals. The first time a
string arrives from a `Scanner`, a file, or the network, it is a different object and
your comparison silently starts returning `false`.

**Use `.equals()`. Every time. Do not rely on the literal case.**

---

## 6. Strings never change

```java
String s = "hello";
s.toUpperCase();
System.out.println(s);      // hello  -- unchanged
```

A Java `String` cannot be modified. Every method that looks like it edits the string
actually builds a **new** string and hands it back. Discard the return value and nothing
happens.

```java
String s = "hello";
s = s.toUpperCase();        // keep the answer
System.out.println(s);      // HELLO
```

The fix is always the same: **use what the method returns.**

---

## 7. Casting chops. Formatting rounds.

These two look similar and do different things. Keeping them straight is most of Skill
Builder 1.

```java
int x = 3.9;                        // does not compile
int y = (int) 3.9;                  // 3     -- chopped
int z = (int) Math.round(3.9);      // 4     -- rounded
String s = String.format("%.2f", 3.999);   // "4.00" -- rounded
```

Java will widen a small type into a bigger one on its own. It will **never** narrow one
for you — `int x = 3.5;` is a compile error, not a silent truncation. You have to write
`(int)` and accept what gets lost.

And what gets lost is everything after the decimal point. `(int) 3.9` is `3`.

### The two-decimal-places trick

To cut a number off at two places *without* rounding:

```java
double v = 1.4815297665908702;
double t = ((int)(v * 100)) / 100.0;      // 1.48
```

Multiply by 100, cast to `int` so the rest is chopped, divide by `100.0`.

**Watch that last divide.** Writing `/ 100` instead of `/ 100.0` puts you straight back
into section 2 — both sides are `int`, the fraction disappears, and you get a whole
number. **Skill Builder 1 asks for exactly this trick**, and this is where people lose
points on it.

---

## 8. Reaching into a String

Everything here you already do in Python. The names changed and the brackets are gone.

| Python | Java |
|---|---|
| `len(s)` | `s.length()` |
| `s[0]` | `s.charAt(0)` |
| `s[0:3]` | `s.substring(0, 3)` |
| `s[-1]` | `s.charAt(s.length() - 1)` |

**Java has no negative indexing.** The last character is always `length() - 1`. You will
write that expression for the rest of the semester, so get comfortable with it now.

`substring(0, 3)` stops **before** index 3 — the same half-open range as a Python slice,
so that intuition carries over unchanged.

---

## 9. Quick Reference — Python to Java

The table from the board. This is the whole session on one page.

| Python | Java | Why |
|---|---|---|
| `5 / 2` → `2.5` | `5 / 2` → `2` | both `int` ⇒ integer division |
| `-7 // 2` → `-4` | `-7 / 2` → `-3` | Python floors, Java truncates toward zero |
| `str(1) + str(2)` | `"" + 1 + 2` | `+` joins once one side is a `String` |
| `'A' + 1` → error | `'A' + 1` → `66` | a `char` is a number |
| `chr(ord('A') + 1)` | `(char)('A' + 1)` | narrowing needs an explicit cast |
| `a == b` → same text | `a == b` → same object | use `.equals()` for text |
| `s.upper()` | `s.toUpperCase()` **and keep it** | Strings are immutable |
| `int(3.9)` → `3` | `(int) 3.9` → `3` | casting chops |
| `round(3.9)` → `4` | `(int) Math.round(3.9)` → `4` | rounding is a method call |
| `f"{x:.2f}"` | `String.format("%.2f", x)` | formatting rounds |
| `len(s)` | `s.length()` | it is a method, with parentheses |
| `s[-1]` | `s.charAt(s.length() - 1)` | no negative indexing |

---

## Housekeeping from Monday

**The quiz moved.** In the room on Monday I said Q1 would be at the start of the next
recitation. **It is not — Q1 is Tuesday Sep 8, in lecture, in the first ten minutes.** If
you wrote down "Monday, 20 minutes," cross it out. Two reasons it moved: **Monday Sep 7 is
Labor Day** so R3 does not meet at all that week, and Sep 8 puts the quiz two days after
this repo is due, so the lab it is drawn from is finished before you sit it.

**R3 — your next section is Sep 14.** There is no section on Sep 7. That is a two-week gap
with **SB1 due Sep 13**, right at the end of it. Do not save SB1 for that weekend; office
hours and tutoring exist, and exercises 6, 7 and 8 in this repo are its spine.

**Roll is being taken from Tuesday Sep 1 onward.** Nobody was penalised for Thursday or for
Monday — there was real confusion about where recitation was meeting, and that is on the
schedule, not on you. From Tuesday it counts.

**Repo links go in Canvas before class.** If you join late or lose the chat, the link for
whatever we are working on is already posted there.

**Volunteering to share your screen earns bonus points.** They apply to the recitation
grade and they help on a week you miss or score low. Driving in front of everyone is the
fastest way to find out what you actually understand, which is the real reason to do it.

**Opening the pull request** gets demonstrated in Wednesday's session so it is on the
recording for everyone. The written steps are already in the repo README under *Turning it
in* — you do not have to wait for the demo to submit.

---

## 10. Assignments

| | Due |
|---|---|
| **Recitation 2** — finish the exercises, push, open the PR | **Sun Sep 6, 11:59 PM** |
| **Drills** — Asterisks · Show me the Numbers | **Sun Sep 6, 11:59 PM** |
| **Skill Builder 1** — input, output, variables, casting | **Sun Sep 13, 11:59 PM** |
| **Q1** — data types, operators, strings | in class, **Tuesday Sep 8** |

**Q1 is Tuesday Sep 8 — on paper, closed book, no AI, ten minutes at the start of class.**
It sits two days after this repo is due, so the lab it is drawn from will be finished and
submitted before you sit it.
Every item on it is one of the eight ideas above. If you finished today with 42 green tests, you have
already studied for it — read this page once more and you are done.

Exercises 6, 7 and 8 are the ones **Skill Builder 1** needs. `toHundredths` is the
multiply-cast-divide trick SB1 asks for by name, and `spiceReport` builds SB1's output
sentence exactly. When you get stuck on SB1 next week, come back to this repo first.

---

## The one thing that costs people points

Unchanged from last time, and it will be unchanged in December:

```bash
git status                      # run this constantly
git add <file>
git commit -m "what changed"
git push                        # <- the one people forget
```

Committing saves your work **on your laptop**. Only `git push` makes it exist for me.
Then refresh the page on GitHub and *look at it*. The work is not done until you have
seen it on the server.
