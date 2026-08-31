# Recitation 01 — Setup, Git, and Your First Java Program

**Student Notes**

These notes cover everything from our first recitation, plus a few corrections and clarifications on things I explained quickly in the moment. Where a note says **Correction**, that's a spot where the version I gave in class was a useful first approximation but not precisely right — read those carefully, because you'll see these concepts again in Networking and in Operating Systems, and I don't want you carrying a wrong mental model into those courses.

---

## 1. Class Logistics

- Lecture is Tuesdays and Thursdays at 3:00 PM. The door closes at 3:05. If you're late without having communicated with me beforehand, you're marked absent.
- Recitations: plan to be on camera and to participate.
- You need a GitHub account. Any email works — it does not have to be your DSU address.
- Fill out the roster form with your GitHub username so I can match your work to you in the gradebook. If you change your username later, tell me.

---

## 2. Git: Fork, Then Clone

You can't push directly to the class repository. The workflow is **fork → clone → work → commit → push**, and later, **pull request**.

### Forking

A fork is your own copy of a repository, living under your GitHub account, that stays linked to the original ("upstream").

1. Open the class repo on GitHub.
2. Click **Fork**.
3. Leave the owner (your username) and repository name as-is.
4. Click **Create fork**.

The URL changes from `github.com/DSU-CSCI-121-F26/recitation-00` to `github.com/your-username/recitation-00`. That's how you know it worked.

**Why forking matters:** the link back to upstream is a two-way street. You can pull my bug fixes and updates down into your fork, and you can propose your changes back to me through a **pull request**. That's how open source works, and it's how most professional teams handle outside contributors. We'll cover pull requests in detail later in the semester.

### Cloning

Cloning downloads your fork onto your machine.

1. On **your** fork (not the DSU one), click the green **Code** button.
2. Make sure the **HTTPS** tab is selected and copy the URL.
3. In your terminal, `cd` into your dev folder.
4. Run:

```bash
git clone https://github.com/your-username/recitation-00.git
```

We're using HTTPS for this class. SSH is the other option and it's what most professionals eventually switch to, but it requires generating and registering a key pair, and I don't want that to be the thing that blocks you in week one.

---

## 3. Terminal Commands

Learn these. When you intern somewhere, you will be SSH'd into a remote server with no graphical file browser, and the terminal is the only interface you get.

| Command | Stands for | What it does |
|---|---|---|
| `pwd` | print working directory | Shows the directory you're currently in |
| `ls` | list | Lists the contents of the current directory |
| `cd <dir>` | change directory | Moves into a directory |
| `cd ..` | — | Moves up one level |
| `cd ~` | — | Jumps to your home directory |
| `mkdir <name>` | make directory | Creates a folder |
| `clear` | — | Clears the screen |
| `rm <file>` | remove | Deletes a file |
| `rm -rf <dir>` | remove, recursive + force | Deletes a directory and everything in it |

### A serious warning about `rm`

`rm` does **not** move things to the Trash. There is no undo. There is no recovery. `rm -rf` on the wrong path will silently destroy hours of work.

Before you ever run `rm -rf`, run `pwd` and read the output. Make it a reflex.

---

## 4. Where Your Code Lives: `~/dev`

Create a `dev` folder in your home directory and keep **all** your code in it.

```bash
cd ~
mkdir dev
cd dev
mkdir student-work
cd student-work
```

### Why this matters

Your home directory is the one place on a shared machine where your user account reliably has full read/write permissions. On a server with a dozen other users, your process is not going to have permission to write to `/`, `/usr`, or `/opt`. If you develop somewhere your machine lets you get away with, and then deploy somewhere it doesn't, you get a permissions failure in production that never appeared on your laptop.

Working out of `~/dev` from day one means your development environment already resembles the constrained environment your code will actually run in.

### Organize by year

My own habit: `~/dev/2026/`, and inside that, one folder per client, class, or personal project. At the end of the year I zip the whole thing and move it to archives. Ten seconds of discipline now saves you an afternoon of archaeology later.

---

## 5. The Twelve-Factor App

The Twelve-Factor App is a set of twelve principles for building modern, cloud-deployable software. We touched three today; we'll return to the rest as they become relevant.

**Factor I — Codebase.** One codebase tracked in version control, many deploys. By using Git, you've already satisfied this.

**Factor II — Dependencies.** Explicitly declare and isolate dependencies. Your project should never rely on a library that "just happens to be installed" on the machine. In Java we do this with a build tool (see §7) — the `pom.xml` file lists every external library your project needs, and anyone who clones your repo gets exactly the same set.

**Factor X — Dev/Prod Parity.** Keep development, staging, and production as similar as possible.

### The Super Bowl analogy

The Super Bowl is held in a climate-controlled dome (or a warm-weather city) rather than in whatever stadium happens to be available in February. The reason is fairness: neither team should win because they're more accustomed to snow. Both teams prepared under controlled conditions, so they compete under controlled conditions. The conditions you train in should be the conditions you perform in.

Software is the same. If you develop on macOS with Java 21 and deploy to Linux with Java 17, you will find out about the mismatch at the worst possible moment. Bugs are cheap to fix in development and expensive to fix in production, so you want your development environment to surface them first.

### Environments you'll hear about

`local` → `dev` → `QA` / `test` → `UAT` (user acceptance testing) → `staging` → `production`

Not every organization uses all of them, but the progression is always the same: each environment is a little more production-like than the one before it.

---

## 6. Protocols and How Data Moves

**Correction — this is the section I compressed the most in class, and I collapsed two layers of the network stack into one. Here's the accurate version.**

Networking is built in **layers**. Each layer solves one problem and hands off to the next. The two we care about right now:

### The transport layer: TCP and UDP

This is the layer that actually breaks your data into **packets**, routes them, and decides what happens when one goes missing.

**TCP (Transmission Control Protocol)** is the reliable one. It:
- Splits your data into numbered packets
- Sends them across the network, where they may take different routes and arrive out of order
- Reassembles them in the correct order at the destination
- Detects missing packets and requests retransmission
- Guarantees that everything arrives, and arrives in order

**UDP (User Datagram Protocol)** is the fast one. It sends packets and does not track them. If one is lost, it's lost — no retransmission, no reordering. That sounds bad until you consider a live video call: a packet from 400 milliseconds ago is *useless* even if it arrives, and stopping to re-request it would stall everything behind it. Better to drop a frame and keep moving.

> **What I said in class:** that HTTP handles packetization and guarantees delivery.
> **What's actually true:** TCP does that. HTTP sits on top of TCP and inherits the guarantee.

### The application layer: HTTP, HTTPS, SSH, FTP, SMTP

These protocols define the *format and meaning* of the messages. They don't handle packets at all — they hand their data to TCP and let it deal with transport.

| Protocol | Stands for | Purpose |
|---|---|---|
| HTTP | HyperText Transfer Protocol | Web requests and responses |
| HTTPS | HTTP Secure | HTTP wrapped in TLS encryption |
| SSH | Secure Shell | Encrypted remote terminal access |
| SFTP / FTP | (Secure) File Transfer Protocol | Moving files between machines |
| SMTP | Simple Mail Transfer Protocol | Sending email |

**HTTPS** is HTTP running inside a TLS-encrypted tunnel. Without it, everything you send — passwords, card numbers, session cookies — travels in plaintext and is readable by anything sitting between you and the server. Modern TLS uses 128-bit or 256-bit encryption. The padlock in your browser means the tunnel is up and the server presented a valid certificate.

**SSH** is Secure Shell: an encrypted connection to a terminal session on a remote machine. It's how you'll log into servers, and it's the other option Git offers for authenticating pushes.

### Correction on streaming

> **What I said in class:** streaming services use UDP, and HTTP won't display anything until the entire response has loaded.
>
> **What's actually true:** neither of those holds up.

Netflix, YouTube, Hulu, and Disney+ stream over **HTTP**, using adaptive bitrate protocols called **HLS** and **DASH**. The video is chopped into small segments (typically 2–10 seconds), each fetched as an ordinary HTTP request over TCP. Your player keeps a buffer a few segments ahead, and when your bandwidth drops it silently requests lower-quality segments for the next chunk. That's why the picture gets blurry before it stops entirely — that's adaptive bitrate doing its job.

HTTP also does *not* wait for a complete response before displaying anything. **Chunked transfer encoding** lets a server stream a response body in pieces, and browsers render progressively as content arrives. That's why you see a page's text before its images finish.

**Where UDP actually is:** Zoom, Discord voice, FaceTime, and online gaming — anything real-time and interactive, where latency hurts more than a dropped frame. Also DNS lookups, and **QUIC**, the newer protocol underneath HTTP/3, which is built on UDP but reimplements reliability itself.

The instinct I was pointing at in class was correct — *some* things trade reliability for speed. I just attached it to the wrong example.

---

## 7. Java Build Tools

Java projects use a build tool to manage dependencies (Factor II), compile, run tests, and package the application.

| Tool | Config file | Where you'll see it |
|---|---|---|
| **Maven** | `pom.xml` | Enterprise and cloud Java — our tool this semester |
| **Gradle** | `build.gradle` or `build.gradle.kts` | Android, and increasingly modern Java |
| **Ant** | `build.xml` | Legacy projects; largely superseded |

You can identify any Java project's build tool in about two seconds by looking for these files in the root directory.

### Opening the project in IntelliJ

**File → Open**, navigate to the cloned folder, and select the **folder itself**. IntelliJ detects the `pom.xml` and imports the Maven project automatically. Click **Trust Project** when prompted.

If the import misbehaves — dependencies unresolved, no Maven tool window, red squiggles everywhere — close it and reopen, selecting the `pom.xml` file directly instead of the folder. That forces IntelliJ to treat it as a Maven project.

### Standard Maven layout

```
recitation-00/
├── pom.xml                    ← dependencies and build config
├── src/
│   ├── main/
│   │   ├── java/              ← your source code ("src" = source)
│   │   └── resources/         ← config files, static assets
│   └── test/
│       └── java/              ← your unit tests
└── target/                    ← compiled output (never commit this)
```

---

## 8. Java Language Fundamentals

### `class`

A class is a template. It describes what an object of that type will look like and what it can do. `Recitation00` is the name of our class. Declaring it `public` means code anywhere in the project can use that template to create objects.

By convention, one public class per file, and the filename must match the class name exactly: `Recitation00` lives in `Recitation00.java`.

### Access modifiers: `public` and `private`

**Correction — my heap drawing in class implied that access control is about objects seeing each other in memory at runtime. That's not what's happening.**

Access modifiers are enforced by the **compiler**, before your program ever runs. If you write code that violates them, you don't get a runtime error — you get a compile error, and no program at all. And the unit of access control is the **class**, not the individual object.

The correct question is never "can this object see that object?" It's **"is the code I'm writing right now located inside a class that's allowed to touch this member?"**

| Modifier | Accessible from |
|---|---|
| `public` | Anywhere |
| `protected` | Same package, plus subclasses anywhere |
| *(no modifier)* | Same package only — called "package-private" or "default" |
| `private` | Inside the same class only |

### The thing that trips people up

Two objects of the same class can access each other's private fields:

```java
public class BankAccount {
    private double balance;

    public boolean hasMoreThan(BankAccount other) {
        return this.balance > other.balance;  // legal — reading another object's private field
    }
}
```

This looks like a violation, but it isn't. `private` means "only code written inside the `BankAccount` class may touch this," and the method above *is* inside `BankAccount`. The compiler doesn't care which instance you're reading from.

This is exactly the case I described in class as "two private circles of the same type can see each other." The observation was right; the explanation was wrong. It works because of where the *code* lives, not because of what the objects can perceive.

### Why this matters — encapsulation

Making fields `private` and exposing them through public methods means you control every way your data can change:

```java
public class BankAccount {
    private double balance;              // nobody can set this directly

    public double getBalance() {
        return balance;
    }

    public void deposit(double amount) {
        if (amount <= 0) {
            throw new IllegalArgumentException("Deposit must be positive");
        }
        balance += amount;
    }
}
```

If `balance` were public, any code anywhere could set it to `-5000` and you'd have no way to catch it. Private fields plus validating methods means invalid states are impossible by construction. **Default to `private`, and open things up only when you have a reason.**

---

## 9. Stack and Heap

**Correction — I said in class that the stack "lives on the CPU." It does not.**

Both the stack and the heap are regions of **RAM**. The stack is fast for three reasons, none of which is physical location on the processor:

1. **Allocation is trivial.** Pushing a frame is incrementing a pointer. Popping is decrementing it. No searching for free space.
2. **No garbage collection.** A stack frame disappears the instant its method returns. Nothing has to track it.
3. **Excellent cache locality.** The stack is small and constantly reused, so it's almost always sitting in fast CPU cache. This is what I was groping toward with "it's on the CPU" — the *data* is frequently cached, but the memory itself is RAM.

### The actual division of labor

| | **Stack** | **Heap** |
|---|---|---|
| Holds | Local variables, method parameters, object *references* | The objects themselves |
| Size | Small, fixed (often ~512KB–1MB per thread) | Large, grows on demand |
| Lifetime | Frame destroyed when the method returns | Until no references remain, then garbage collected |
| Sharing | One stack per thread — private to it | One heap shared by all threads |
| Failure mode | `StackOverflowError` (usually runaway recursion) | `OutOfMemoryError` |

### What this looks like in practice

```java
public void example() {
    int count = 5;                          // the value 5 lives on the stack
    String name = "Tariq";                  // reference on stack, String object on heap
    BankAccount acct = new BankAccount();   // reference on stack, object on heap
}
```

When `example()` returns, its stack frame is destroyed — `count`, `name`, and `acct` all vanish. The `BankAccount` object on the heap is now unreachable, and the garbage collector will reclaim it eventually.

Java has other memory areas too (the metaspace, the program counter, native method stacks), but stack and heap are the two that will affect how you write code this semester.

---

## 10. `public static void main(String[] args)`

Every Java program starts here. This exact signature — commonly abbreviated **PSVM** — is what the JVM looks for when it launches your program.

```java
public static void main(String[] args) {
    System.out.println("Hello World!");
}
```

Breaking it down word by word:

- **`public`** — the JVM must be able to call it from outside your class
- **`static`** — it belongs to the class, not to any instance. This is essential: at launch there are no objects yet, so there's nothing to call an instance method *on*. `static` is what makes the method callable without first constructing something.
- **`void`** — returns nothing. Your exit code goes to the OS through the JVM, not through a return value.
- **`main`** — the name the JVM searches for. Not `Main`, not `start`, not `run`.
- **`String[] args`** — command-line arguments, passed in as an array of strings

Get any of it wrong and the JVM won't find an entry point. You'll get:

```
Error: Main method not found in class Recitation00
```

`public` and `static` may appear in either order (`static public void main` compiles fine), but everything else is fixed. Convention is `public static void`.

**IntelliJ shortcut:** type `psvm` and press Tab. The whole signature expands. Also try `sout` + Tab for `System.out.println()`.

---

## 11. Assignment 00

**Required:**

1. Create your `~/dev` folder if you haven't
2. Fork the `recitation-00` repository
3. Clone your fork into `~/dev`
4. Open it in IntelliJ
5. Modify `main` to print `Hello World!` — **exactly that**, capital W, no comma, with the
   exclamation mark. The test compares against that string character for character
6. Run it and confirm the output
7. **Push it.** See below — this is the step that makes it count

**Optional / extra credit:** fork the [Robocode Arena repo](https://github.com/DSU-CSCI-121-F26/robocode-arena). No hardware needed, it runs all semester, and there is a tournament on the last day of class.

### Handing it in

We covered this in lecture on **Thursday Aug 27**. Committing saves your work on your laptop; only pushing makes it exist for me.

```bash
git status                        # run this constantly
git add .
git commit -m "Print Hello World"
git push
```

Then **reload your repository page on GitHub and look at it.** The work is not done until you have seen it on the server.

> **`push` will ask for a password, and your GitHub password will not work.** It has not worked since 2021. What it wants is a **Personal Access Token**:
>
> GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic) → Generate new token → check `repo` → Generate.
>
> **Copy it immediately — it is shown once and never again.** Paste it where Git asks for your password.
>
> If you get `Authentication failed`, that is what it is. Not your fork, not your clone. The token.

Stuck on any of it? Bring it to section — it costs you nothing to arrive with a problem rather than a blank screen, and we will fix it together.

---

## Quick Reference

**Git**
```bash
git clone <url>          # download a repository
git status               # what's changed
git add <file>           # stage a change
git commit -m "message"  # save staged changes locally
git push                 # upload commits to GitHub
```

**Terminal**
```bash
pwd                      # where am I
ls                       # what's here
ls -la                   # including hidden files, with detail
cd <dir>                 # go into a directory
cd ..                    # go up one
cd ~                     # go home
mkdir <name>             # make a directory
rm -rf <dir>             # delete a directory — NO UNDO
```

**Glossary**

- **Fork** — your own copy of someone else's repo on GitHub, linked to the original
- **Clone** — a local copy of a repo on your machine
- **Pull request** — a formal proposal to merge your changes into the original repo
- **Upstream** — the original repository your fork came from
- **Dependency** — an external library your project needs to compile or run
- **POM** — Project Object Model; Maven's `pom.xml` configuration file
- **JVM** — Java Virtual Machine; runs your compiled bytecode
- **Encapsulation** — hiding internal state behind a controlled public interface
