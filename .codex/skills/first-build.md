# Skill: First Build — Guided To-Do App

Walk the learner through building their first real app from scratch, step by step.
This teaches the coding agent workflow at the same time as it builds something real.

## How to trigger
This runs automatically on the first session if assignment 0.6 is complete and 1.4 is not.
Or say: "let's build the to-do app" or "start the first build" or "I'm ready to build"

---

## The approach

Every step follows the same pattern:
1. Explain what we're about to do and why — before writing any code
2. Use the relevant skill (plan, build, learn, review, commit)
3. Check understanding before moving to the next step
4. Celebrate what was just built

The learner should finish this feeling like they know how to have a conversation with a coding agent — not just that they have a to-do app.

---

## Step 1 — Orient

Say this before anything else:

"We're going to build a real to-do app together. It'll run in your browser, save your tasks, and work even after you restart it.

More importantly — we're going to do it the way professional developers work with coding agents. You'll see how to plan before coding, how to review what gets written, and how to save your work properly.

By the end you'll have a working app AND you'll know how to use me effectively. Let's go.

First question before we write a single line: what do you want this app to do? Just describe it like you'd describe it to a friend."

Wait for their answer. Reflect it back: "So you want [their description]. Let me make sure I understand — [restate it simply]. Is that right?"

---

## Step 2 — Plan (using the plan skill)

Say: "Now let's plan this properly before touching any code. I'm going to ask you some questions — this is exactly what you should do at the start of every feature."

Run the plan skill. Ask:
- "What's the simplest version of this that would be useful to you?"
- "What does a task need? Just a name, or other details too?"
- "Should tasks disappear when you mark them done, or stay visible?"
- "Do you need to log in, or is this just for you?"

After they answer, write a short plan to `.codex/plans/todo-app.md`:
```
# Plan: To-Do App

## What it does
- [their description]

## Features in this version
- [bullet each agreed feature]

## Not in this version
- User login (future)
- [anything they mentioned but agreed to skip]

## Stack
- Python + Flask (web framework)
- SQLite (database — saves tasks between restarts)
- Plain HTML (no JavaScript framework needed yet)
```

Show them the plan. Say: "This is saved in `.codex/plans/todo-app.md`. Before I write a single line of code — do you agree with this plan? Change anything now, because it's much easier than changing it after."

Wait for confirmation.

---

## Step 3 — Explain the stack (using the learn skill)

Before building, explain what they're about to see:

"Before I write any code, let me explain the three tools we're using — because you're going to see them in every line:

**Flask** is like a receptionist for your app. When your browser asks for a page, Flask decides what to show. When you submit a form, Flask decides what to do with it.

**SQLite** is a database — a file on your computer that remembers things. When you add a task, it goes into SQLite. When you close and reopen the app, the tasks are still there because they're saved in that file.

**HTML templates** are the actual pages your browser displays. Flask fills them in with data from SQLite and sends them to your browser.

Does that make sense? Any of those worth explaining differently before we start?"

---

## Step 4 — Build Part 1: Flask hello world

Say: "Let's build this in pieces, not all at once. First piece: get Flask running and showing a page. Nothing else yet."

Create `main.py`:
```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def index():
    return 'Flask is working.'

if __name__ == '__main__':
    app.run(debug=True)
```

Then say: "Before we run it — what do you think `@app.route('/')` does? Take a guess."

Wait for answer. Explain:
"Exactly [or: close —] it means: when someone visits the homepage (`/`), run the `index` function. The `/` is the address. Think of it like a street address for a page in your app."

Tell them to run it:
```
source venv/bin/activate
python main.py
```
Then open `http://localhost:5000`.

Say: "You have a running web server. That's real. Most people never get this far. What do you see in the browser?"

---

## Step 5 — Build Part 2: add a template

Say: "Right now Flask just sends plain text. Let's make it send a real HTML page."

Create `templates/index.html`:
```html
<!DOCTYPE html>
<html>
<head><title>My To-Do App</title></head>
<body>
  <h1>My Tasks</h1>
  <p>No tasks yet.</p>
</body>
</html>
```

Update `main.py` to render it:
```python
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def index():
    return render_template('index.html')

if __name__ == '__main__':
    app.run(debug=True)
```

Ask: "Why do you think we need a `templates/` folder — why not just put the HTML file anywhere?"

Explain: "Flask looks for HTML files specifically in a folder called `templates/`. It's a convention — a rule that Flask uses so it knows where to find them. Conventions like this are everywhere in programming. Once you know them, they feel obvious."

---

## Step 6 — Build Part 3: add the database

Say: "Now the interesting part — making it remember things."

Create `database.py`:
```python
import sqlite3

def get_db():
    conn = sqlite3.connect('tasks.db')
    conn.row_factory = sqlite3.Row
    return conn

def init_db():
    db = get_db()
    db.execute('''
        CREATE TABLE IF NOT EXISTS tasks (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            title TEXT NOT NULL,
            done INTEGER DEFAULT 0
        )
    ''')
    db.commit()
    db.close()
```

Ask: "What do you think `CREATE TABLE IF NOT EXISTS` means?"

Explain: "It means: create this table, but only if it doesn't already exist. Without the `IF NOT EXISTS` part, running the app twice would crash because it would try to create the same table twice. Small detail — important habit."

Update `main.py` to initialise the database on startup and load tasks.

---

## Step 7 — Build Part 4: add, complete, delete

Add the three form actions one at a time. After each one:
- Show the learner what changed
- Ask them to use it in the browser
- Ask one question about how it works

After all three work, say: "You now have a complete CRUD app. CRUD stands for Create, Read, Update, Delete — the four operations every database app does. Everything you'll ever build does some version of this."

---

## Step 8 — Review (using the review skill)

Say: "Before we save this, let's do a code review — this is what professionals do before every commit. I'm going to read through everything we wrote and flag anything worth improving."

Run the review skill. Walk through every issue in plain English. For each one:
- Explain what the issue is
- Explain why it matters
- Show the fixed version
- Ask: "Does the fix make sense?"

---

## Step 9 — Commit (using the commit skill)

Say: "Now we save it. Watch how we do this — you'll do it the same way every time."

Run the commit skill. Narrate each step:
- "First I check what files changed — so we know exactly what we're saving"
- "Then I scan for any secrets — API keys, passwords — that shouldn't be committed"
- "Then I write a commit message that describes what changed and why"
- "Then I ask you to confirm before running anything"

After the commit: "That's your first real commit. This is saved in Git history forever. If you ever break something, you can come back to this exact point."

---

## Step 10 — Reflect

Say: "You just built a real app. Let's recap what you learned — not about the app, but about how to work with a coding agent:

1. **Plan first** — we agreed on what to build before writing anything. This stops you building the wrong thing.
2. **Build in pieces** — small steps you can test, not one big thing that might not work
3. **Understand as you go** — I asked you to explain things back to me. That's how you actually learn, not just watch.
4. **Review before saving** — you caught issues before they became bugs
5. **Commit often** — small saves you can roll back to

This is the loop. Every feature you build from here uses this exact loop. The only thing that changes is what you're building."

Ask: "What was the most confusing part? Let's make sure that's clear before you build the next thing."

---

## After this skill completes

Mark assignments 1.4 through 1.8 complete in `.codex/assignments.md`.
Run the memory skill to log the session.
Tell the learner: "Your next assignment is 1.9 — CS50P Weeks 1–3. Do it alongside your next feature. Say 'mentor' when you're ready to keep going."
