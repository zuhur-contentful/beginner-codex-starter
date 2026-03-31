# Skills Guide

This repo comes with a set of pre-built skills for the Codex App and Codex CLI. They make Codex behave like a structured mentor, not just a code generator.

Each skill is a set of instructions Codex follows when you use a specific trigger phrase. You don't need to install anything -- they're in the `.codex/skills/` folder and Codex reads them automatically.

---

## The Five Skills

### 1. Plan -- before you build anything

**Trigger:** say "plan [feature name]" or "I want to add [feature]"

**What it does:**
- Asks you clarifying questions before writing any code
- Helps you define the smallest useful version of the feature
- Saves a plan file in `.codex/plans/` so you can refer back
- Gets your confirmation before starting

**Use it:** every time you start something new. Skipping this leads to building the wrong thing and having to redo it.

---

### 2. Review -- after you write code

**Trigger:** say "review my code" or "check what I just wrote"

**What it does:**
- Reads what changed since your last commit
- Flags security issues, missing error handling, and confusing code
- Explains every issue in plain English with the fixed version shown
- Points out what you did well, not just what to fix

**Use it:** before every commit. This is how you learn to write better code over time.

---

### 3. Debug -- when something is broken

**Trigger:** say "something's broken" or paste your error message

**What it does:**
- Asks for the full error message and what you were doing
- Reads the relevant files (doesn't guess)
- Forms a hypothesis and tests one fix at a time
- Explains what caused the bug and why the fix works

**Use it:** the moment something stops working. Don't spend an hour guessing -- just say "debug this" and paste the error.

---

### 4. Commit -- when you're ready to save

**Trigger:** say "commit this" or "save my work"

**What it does:**
- Shows you exactly what files changed and what the diff looks like
- Checks for accidentally included secrets before committing
- Writes a properly formatted commit message
- Asks for your confirmation before running anything

**Use it:** every time you finish a piece of work. Small, frequent commits are better than one giant commit at the end.

---

### 5. Learn -- when you want to understand something

**Trigger:** say "explain this" or "what does this do" or "teach me what's happening here"

**What it does:**
- Explains any code in three levels: one sentence, line by line, and why it's written that way
- Uses analogies to everyday things
- Asks what's still unclear and explains it differently if needed

**Use it:** any time Codex writes something you don't fully understand. Never let code you don't understand stay in your project.

---

## Workflow: how to use skills together

Here's the workflow for adding any new feature:

```
1. PLAN   -- "plan [feature]"  -- agree on what you're building before touching code
     |
2. BUILD  -- Codex writes the code, you review and approve each change
     |
3. LEARN  -- "explain this"    -- make sure you understand what was written
     |
4. REVIEW -- "review my code"  -- check for issues before saving
     |
5. COMMIT -- "commit this"     -- save your work with a clear message
     |
6. PUSH   -- git push          -- back it up to GitHub
```

You don't have to follow this exactly. But if something goes wrong, come back to this order -- it covers the most common failure modes.

---

## How skills work technically

The skills are stored as markdown files in `.codex/skills/`. When you open this project in the Codex App, Codex can read them. When you use a trigger phrase, Codex follows the instructions in the matching skill file.

You can edit any skill file to change how Codex behaves. For example, if you want the review skill to be stricter or more lenient, open `.codex/skills/review.md` and change the rules.

You can also create your own skills. Add a new `.md` file to `.codex/skills/` with a trigger phrase and instructions, and Codex will use it.

---

### 6. Mentor — check progress and get your next assignment

**Trigger:** say "mentor" or "what should I do next" or "am I ready for the next stage"

**Also runs automatically:** at the start of every session

**What it does:**
- Reads your session memory and assignment list
- Checks your understanding of the last thing you built (asks you to explain it)
- Gives you the next concrete assignment with clear success criteria
- Won't move you forward until you can explain what you just built

**Use it:** at the start of every session, or whenever you're not sure what to do next.

---

### 7. Memory — save what happened this session

**Trigger:** say "save memory" or "end session" or "we're done for today"

**Also runs automatically:** at the end of every session

**What it does:**
- Reads your git log to see what was committed
- Writes a structured entry to `.codex/memory/log.md`: what was built, what broke, what was fixed, decisions made, next task
- Codex reads this log at the start of every future session — you never have to re-explain your project

**Use it:** you don't have to — it runs automatically. But you can trigger it manually anytime.

---

## Quick reference

| You want to... | Say... |
|---------------|--------|
| Plan a new feature | "plan [feature name]" |
| Review code you just wrote | "review my code" |
| Fix something that's broken | "debug this" + paste the error |
| Save your work | "commit this" |
| Understand code | "explain this" |
| Get your next assignment | "mentor" |
| Save session memory | "save memory" (or just say goodbye — it runs automatically) |
| Start the Codex App | Open the Codex App, select this folder |
| Start the Codex CLI | `cd [project folder] && codex` |
