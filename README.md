# beginner-codex-starter

Starter template and step-by-step learning guide for beginners building personal projects with Python and OpenAI Codex.

## Quick Start

```bash
# Clone this repo into your projects folder
git clone https://github.com/zuhur-contentful/beginner-codex-starter ~/Codebases/my-project
cd ~/Codebases/my-project

# Copy the secrets template and fill in your values
cp .env.example .env

# Wire up the pre-commit hook (prevents accidental secret commits)
git config core.hooksPath .githooks
chmod +x .githooks/pre-commit
```

Then read the **Learning Guide** below — it walks you through everything step by step.

---

## What's in this repo

| File | What it does |
|------|-------------|
| `CLAUDE.md` | Context file — Codex reads this to understand your project. Edit it as you build. |
| `.env.example` | Template listing every secret your app needs. Copy to `.env`, never commit `.env`. |
| `.mcp.json` | Connects Codex to GitHub so it can read your issues and PRs. |
| `.githooks/pre-commit` | Runs before every commit and blocks accidentally committed secrets. |
| `.github/workflows/ci.yml` | Runs your tests automatically on every push to GitHub. |

---

# Learning Guide — Building Personal Projects with Codex

This guide is for beginners who want to build real things for themselves. No computer science degree needed. No prior experience required. Just follow it step by step.

---

## Part 1: Foundation — Before You Write Any Code

### Step 1.1 — Set Up Your Machine

**Install these tools first (one time only):**

| Tool | What it does | How to install |
|------|-------------|----------------|
| Python 3.12 | The programming language you'll use | [python.org/downloads](https://python.org/downloads) |
| Git | Saves versions of your code | [git-scm.com](https://git-scm.com) |
| GitHub account | Stores your code online | [github.com](https://github.com) |
| VS Code | Code editor (free) | [code.visualstudio.com](https://code.visualstudio.com) |
| Codex CLI | AI coding agent in your terminal (free with ChatGPT Plus) | `npm install -g @openai/codex` |

**Verify everything installed:**
```bash
python3 --version    # should say Python 3.12.x
git --version        # should say git version 2.x
gh --version         # GitHub CLI: brew install gh
```

**Authenticate with GitHub:**
```bash
gh auth login
# Follow the prompts — choose GitHub.com → HTTPS → Login with browser
```

---

### Step 1.2 — Understand the Mental Model

Before writing code, understand how the pieces fit together:

```
Your idea
    ↓
You write code (Python)
    ↓
Code runs on your computer (or a server)
    ↓
Users interact via a web browser
    ↓
Data gets saved in a database
    ↓
AI (GPT via OpenAI API) can read/write/reason over all of it
```

**The three things every app does:**
1. **Input** — user types something, clicks a button, uploads a file
2. **Process** — your code does something with it (calls an API, saves to DB, runs AI)
3. **Output** — user sees a result

Every feature you ever build is just a variation of these three steps.

---

### Step 1.3 — Get Your API Keys & Set Up Codex

**OpenAI API Key (for GPT in your app):**
1. Go to `platform.openai.com/api-keys`
2. Sign up — ChatGPT Plus subscription or pay-as-you-go API credits both work
3. Click "Create new secret key" → copy it somewhere safe
4. Never share it. Never put it in your code. Put it in `.env`.

**GitHub Personal Access Token:**
1. Go to `github.com/settings/tokens`
2. Click "Generate new token (classic)"
3. Select scopes: `repo`, `read:user`
4. Copy the token — you'll only see it once

---

### Step 1.4 — Pick How You Use Codex

Codex is your AI coding assistant. You can use it in several ways — pick whichever feels most comfortable. You can use all of them; they all share the same OpenAI account.

#### Option A — ChatGPT web app (easiest to start)
Just go to `chatgpt.com` and start a conversation. Paste your code, describe your error, ask questions. No install needed.

**Best for:** asking "why does this code do X", explaining errors, brainstorming approaches.

**Limitation:** it can't directly read or edit files on your computer.

---

#### Option B — VS Code extension (recommended for most beginners)
Install the **GitHub Copilot** extension in VS Code. Sign in with your GitHub account (free trial available).

```
VS Code → Extensions (Ctrl+Shift+X) → search "GitHub Copilot" → Install
```

Then open VS Code's Copilot Chat panel (`Ctrl+Shift+I` / `Cmd+Shift+I`) and ask questions about your open files.

**Best for:** getting suggestions as you type, asking questions about the file you're looking at, explaining code inline.

**Tip:** You can also use the **Cursor** editor (a VS Code fork with deeper AI integration) — `cursor.com`.

---

#### Option C — Codex desktop app
OpenAI's desktop app for Mac/Windows. Download from `openai.com/desktop`.

Works like the web app but lives on your desktop with better keyboard shortcuts and file attachment support.

**Best for:** longer coding sessions, attaching files and screenshots to your conversation.

---

#### Option D — Codex CLI in the terminal (most powerful)
Runs directly in your project folder. Can read your files, make edits, and run commands — all with your approval.

```bash
# Install (requires Node.js)
npm install -g @openai/codex

# Authenticate
codex login

# Use it (run from your project folder)
cd ~/Codebases/my-journal-app
codex
```

**Best for:** letting Codex make changes across multiple files, running tests, scaffolding features end-to-end.

**How it works:**
- You describe what you want in plain English
- Codex proposes changes or commands
- You approve or reject each one before it runs
- It reads your `CLAUDE.md` for project context automatically

---

**Which to start with?**

| You want to... | Use |
|---|---|
| Ask questions, learn concepts | ChatGPT web (Option A) |
| Get help while typing code | VS Code Copilot (Option B) |
| Chat with files attached | Desktop app (Option C) |
| Let AI make edits for you | Codex CLI (Option D) |

Most beginners start with **A or B**, then graduate to **D** once they're comfortable reading code.

---

## Part 2: Your First Project

### Step 2.1 — Set Up Your First Project

```bash
# Clone this template into your projects folder
git clone https://github.com/zuhur-contentful/beginner-codex-starter ~/Codebases/my-journal-app
cd ~/Codebases/my-journal-app

# Copy secrets template
cp .env.example .env

# Wire up the pre-commit hook
git config core.hooksPath .githooks
chmod +x .githooks/pre-commit

# Create your own GitHub repo for this project
gh repo create my-journal-app --public --source=. --push
```

Done. You now have a project folder with all the starter files and your own GitHub repo.

---

### Step 2.2 — Understand What Was Created

Open the project in VS Code:
```bash
code ~/Codebases/my-journal-app
```

Key files to understand:

**`CLAUDE.md`** — Codex reads this every time you start a session. It tells Codex what your project is, what stack you're using, and what the rules are. Edit it as your project grows.

**`.env.example`** — Lists every secret your app needs. Copy it to `.env` and fill in your real values:
```bash
cp .env.example .env
# Open .env and fill in your OPENAI_API_KEY etc.
```

**`.gitignore`** — Tells Git to ignore certain files. Your `.env` file is listed here — that's intentional. Your secrets never go to GitHub.

**`.githooks/pre-commit`** — Runs automatically before every `git commit`. It checks for accidental secrets in your code.

**`.github/workflows/ci.yml`** — Runs your tests automatically on every push to GitHub.

---

### Step 2.3 — Write Your First Feature

Open a terminal in your project folder and start Codex:
```bash
cd ~/Codebases/my-journal-app
codex
```

Tell Codex what you want to build. Be specific:

> "I want to build a simple Flask web app. It should have one page where I can write a journal entry and save it to a SQLite database. Show me how to set this up step by step."

Codex will write the code with you. Your job is to understand each piece before moving on.

---

## Part 3: Core Concepts (Read These)

### Concept 1 — Virtual Environments

Every Python project should have its own virtual environment. This keeps your dependencies isolated.

```bash
# Create a virtual environment (run once per project)
python3 -m venv venv

# Activate it (run every time you open a terminal)
source venv/bin/activate    # Mac/Linux
venv\Scripts\activate       # Windows

# You'll see (venv) in your prompt — that means it's active
(venv) $ python main.py
```

**Why this matters:** Without a virtual environment, all your Python packages get mixed together across projects. This causes weird version conflicts. Always use venvs.

---

### Concept 2 — The `.env` File Pattern

Your app needs secrets (API keys, database passwords) to run. Never put them directly in code.

**The pattern:**
```
.env.example   ← committed to GitHub (shows what's needed, no real values)
.env           ← NOT committed (has your real values, listed in .gitignore)
```

**In your Python code:**
```python
from dotenv import load_dotenv
import os

load_dotenv()  # reads .env file

api_key = os.environ.get("OPENAI_API_KEY")
# Now api_key has the value from your .env file
```

**Install dotenv:**
```bash
pip install python-dotenv
pip freeze > requirements.txt
```

---

### Concept 3 — Git: Save Your Work Properly

Git is version control. Think of it as "save points" for your code.

**The daily workflow:**
```bash
# See what changed
git status

# Stage the files you want to save
git add main.py routes/journal.py

# Save with a message describing what you did
git commit -m "feat: add journal entry form"

# Push to GitHub
git push
```

**Commit message format** (use this pattern):
```
feat: add journal entry form        ← new feature
fix: correct date formatting bug    ← bug fix
docs: update README                 ← documentation
chore: update dependencies          ← maintenance
```

**Never do:**
```bash
git add .    # adds everything including .env if you forgot .gitignore
git add -A   # same problem
```

**Check before committing:**
```bash
git diff --staged   # see exactly what you're about to commit
```

---

### Concept 4 — How to Use Codex Effectively

Codex is your AI coding agent. The better you explain what you want, the better the result.

**Bad prompt:**
> "fix my code"

**Good prompt:**
> "My Flask route at `/submit` is returning a 500 error when I submit the form. Here's the error: `[paste error]`. Here's the route code: `[paste code]`. What's wrong?"

**Even better — give Codex context:**
> "I'm building a journal app using Flask and SQLite. The `CLAUDE.md` file has the full context. Right now I'm working on the feature to search past entries by keyword. The search works for exact matches but not partial matches. Here's the current code: `[paste]`"

**How Codex works differently from a chatbot:**
- Codex runs in your terminal, reads your actual files, and can edit them directly
- It can run commands (`pip install`, `python -m pytest`) on your behalf
- Always review what it's about to do before approving — Codex will ask

**Useful things to ask Codex:**
- "Explain this code to me line by line"
- "What could go wrong with this approach?"
- "Write a test for this function"
- "How would a more experienced developer do this?"
- "What's the simplest way to add X feature?"

---

### Concept 5 — Testing: Make Sure Your Code Works

Write tests so you know when you break something.

**A simple test file (`tests/test_journal.py`):**
```python
def test_journal_entry_saves():
    """Test that a journal entry is saved to the database"""
    from app import create_app
    app = create_app(testing=True)

    with app.test_client() as client:
        response = client.post("/submit", data={"entry": "Today was good"})
        assert response.status_code == 200

def test_empty_entry_rejected():
    """Test that empty entries are rejected"""
    from app import create_app
    app = create_app(testing=True)

    with app.test_client() as client:
        response = client.post("/submit", data={"entry": ""})
        assert response.status_code == 400
```

**Run tests:**
```bash
python -m pytest tests/ -v
```

**The mindset:** Write a test for every feature. When you come back to this project in 3 months, you'll know immediately if you broke something.

---

## Part 4: Building AI-Powered Features

### Step 4.1 — Calling the OpenAI API

```python
from openai import OpenAI
import os
from dotenv import load_dotenv

load_dotenv()

client = OpenAI(api_key=os.environ.get("OPENAI_API_KEY"))

def ask_gpt(question: str, context: str = "") -> str:
    """Ask GPT a question, optionally with context"""
    prompt = question
    if context:
        prompt = f"Context:\n{context}\n\nQuestion: {question}"

    response = client.chat.completions.create(
        model="gpt-4o-mini",   # cheap and fast — good for personal projects
        messages=[{"role": "user", "content": prompt}],
        max_tokens=1024,
    )
    return response.choices[0].message.content
```

**Install the SDK:**
```bash
pip install openai
pip freeze > requirements.txt
```

> Model tip: Use `gpt-4o-mini` to keep costs low while learning. Switch to `gpt-4o` when you need better quality.

---

### Step 4.2 — Practical AI Patterns

**Pattern 1: Summarize user content**
```python
def summarize_journal_entries(entries: list[str]) -> str:
    combined = "\n---\n".join(entries)
    return ask_gpt(
        "Summarize these journal entries in 3 bullet points. Focus on recurring themes.",
        context=combined
    )
```

**Pattern 2: Answer questions about stored data**
```python
def answer_question_about_journal(question: str, entries: list[str]) -> str:
    context = "\n---\n".join(entries[-20:])  # last 20 entries
    return ask_gpt(question, context=context)
```

**Pattern 3: Generate structured output**
```python
def extract_mood(entry: str) -> dict:
    response = ask_gpt(
        """Analyze this journal entry and return a JSON object with:
        - "mood": one of ["positive", "negative", "neutral", "mixed"]
        - "energy": a number from 1-10
        - "keywords": list of up to 5 keywords

        Return ONLY the JSON, no other text.""",
        context=entry
    )
    import json
    return json.loads(response)
```

**Always wrap API calls:**
```python
from openai import RateLimitError, APIConnectionError

def safe_ask_gpt(question: str, context: str = "", fallback: str = "") -> str:
    try:
        return ask_gpt(question, context)
    except RateLimitError:
        print("Rate limited — wait a moment and try again")
        return fallback
    except APIConnectionError:
        print("Network error — check your internet connection")
        return fallback
    except Exception as err:
        print(f"Unexpected OpenAI error: {err}")
        return fallback
```

---

## Part 5: Deploying Your App

### Step 5.1 — Free Hosting Options

| Service | Best for | Free tier |
|---------|---------|-----------|
| Render.com | Python/Flask backends | 750 hrs/month (sleeps after inactivity) |
| Vercel | Frontend (HTML/React) | Unlimited for personal projects |
| Railway.app | Full apps with databases | $5/month free credit |
| Supabase | PostgreSQL database | 500MB free forever |

**Deploy to Render (simplest for Flask):**
1. Go to `render.com` → sign up with GitHub
2. "New Web Service" → connect your GitHub repo
3. Set build command: `pip install -r requirements.txt`
4. Set start command: `python main.py`
5. Add your environment variables (copy from `.env`)
6. Click Deploy

---

### Step 5.2 — Before You Deploy Checklist

```bash
# 1. All tests pass
python -m pytest tests/ -v

# 2. No secrets in your code
git diff HEAD | grep -iE "api_key|password|secret" | grep -v ".env"

# 3. requirements.txt is up to date
pip freeze > requirements.txt
git add requirements.txt && git commit -m "chore: update requirements"

# 4. Debug mode is OFF for production
# In your app, check that debug=True is controlled by an env var

# 5. Push latest code
git push
```

---

## Part 6: Learning Roadmap

### Level 0 — Complete Beginner (Week 1-2)

**Goal:** Understand the basics, build something tiny.

Resources (do these in order):
- [Python.org Official Tutorial](https://docs.python.org/3/tutorial/) — Chapters 1-5 only
- [CS50P (Harvard, free)](https://cs50.harvard.edu/python/) — Week 0-3
- [Flask Quickstart](https://flask.palletsprojects.com/quickstart/) — official docs, 15 min read
- [Git in 100 Seconds (YouTube)](https://www.youtube.com/watch?v=hwP7WQkmECE) — 2 min video

**Mini project:** A webpage that displays "Hello, [your name]!" at `localhost:5000`.

---

### Level 1 — Basic App Builder (Week 3-6)

**Goal:** Build a real CRUD app (Create, Read, Update, Delete).

Resources:
- [Flask Tutorial — The Flask Mega-Tutorial](https://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world) — Chapters 1-7
- [SQLite Tutorial](https://www.sqlitetutorial.net/) — "SQLite Python" section
- [HTTP Crash Course](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview) — MDN docs
- [HTML & CSS Basics](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web) — MDN "Getting started with the Web"

**Mini project:** A personal to-do list app. Items saved to SQLite. You can add, check off, and delete items.

---

### Level 2 — AI Integration (Week 7-10)

**Goal:** Add GPT to an app you already built.

Resources:
- [OpenAI API Docs — Quickstart](https://platform.openai.com/docs/quickstart) — official getting started guide
- [OpenAI Cookbook (GitHub)](https://github.com/openai/openai-cookbook) — real code examples for common use cases
- [Prompt Engineering Guide (OpenAI)](https://platform.openai.com/docs/guides/prompt-engineering) — how to write good prompts
- [Python `dotenv` docs](https://pypi.org/project/python-dotenv/) — managing secrets safely
- [OpenAI Python SDK on PyPI](https://pypi.org/project/openai/) — install docs and changelog

**Mini project:** Add a "summarize my week" button to your to-do list app. Sends your completed tasks to GPT and displays a plain-English summary.

---

### Level 3 — Real Product (Week 11-16)

**Goal:** Build something you'd actually use every day.

Resources:
- [FastAPI Tutorial](https://fastapi.tiangolo.com/tutorial/) — official tutorial, full read
- [Supabase Quickstart — Python](https://supabase.com/docs/guides/getting-started/quickstarts/python) — hosted database
- [Pytest Docs — Getting Started](https://docs.pytest.org/en/stable/getting-started.html)
- [Render Deployment Docs](https://render.com/docs/deploy-flask)
- [GitHub Actions Tutorial](https://docs.github.com/en/actions/writing-workflows/quickstart)

**Project:** Pick something you actually need. A habit tracker. A reading list. A private blog. A tool that automates something annoying in your life. Build it fully — with tests, deployed, accessible from your phone.

---

### Level 4 — Advanced (After Week 16)

Once you're comfortable with the above, explore:

- **Authentication:** [Supabase Auth Docs](https://supabase.com/docs/guides/auth) — let users sign up/log in
- **Vector search (RAG):** [Supabase pgvector guide](https://supabase.com/docs/guides/ai/vector-columns) — search by meaning, not just keywords
- **Async Python:** [FastAPI async guide](https://fastapi.tiangolo.com/async/) — handle more users at once
- **React frontend:** [React official tutorial](https://react.dev/learn) — build proper UIs
- **Deployments with Docker:** [Docker Getting Started](https://docs.docker.com/get-started/) — package your app

---

## Part 7: When You Get Stuck

### Debugging Checklist

Before asking for help, try these in order:

```bash
# 1. Read the full error message — the last line is usually the actual problem
python main.py 2>&1 | tail -20

# 2. Check your virtual environment is active
which python   # should point to venv/bin/python, not /usr/bin/python

# 3. Check your .env is loaded
python3 -c "from dotenv import load_dotenv; import os; load_dotenv(); print(os.environ.get('OPENAI_API_KEY', 'NOT SET'))"

# 4. Check your dependencies are installed
pip list | grep flask     # or whatever package is failing

# 5. Run just the failing part in isolation
python3 -c "from your_module import failing_function; print(failing_function('test'))"
```

### How to Ask for Help

When asking Codex/ChatGPT or posting on Stack Overflow:

1. **What you expected to happen**
2. **What actually happened** (copy the full error message)
3. **What you've already tried**
4. **The relevant code** (just the part that's broken, not the whole app)

---

## Common Errors and Fixes

| Error | Likely cause | Fix |
|-------|-------------|-----|
| `ModuleNotFoundError: No module named 'flask'` | Virtual env not active, or pip install not run | `source venv/bin/activate && pip install flask` |
| `KeyError: 'OPENAI_API_KEY'` | `.env` file missing or `load_dotenv()` not called | `cp .env.example .env` then fill in values, call `load_dotenv()` at top of file |
| `Address already in use` | Another app is using port 5000 | `lsof -i :5000` then `kill <PID>`, or use a different port |
| `Permission denied` when running script | File isn't executable | `chmod +x your_script.sh` |
| `git: command not found` | Git not installed | Install from git-scm.com |
| `401 Unauthorized` from OpenAI | API key is wrong or expired | Check `platform.openai.com/api-keys`, regenerate key |
| 429 Too Many Requests | Hit API rate limit | Wait and retry; add `time.sleep(1)` between calls |
| Flask 500 error with no message | Exception being swallowed | Set `debug=True` temporarily to see the full traceback |
