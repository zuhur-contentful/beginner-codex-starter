# beginner-codex-starter

You want to build things. You have no idea where to start. That's exactly what this is for.

This repo gives you a working project template and a step-by-step guide to go from zero -- no coding experience, no idea what a terminal is -- to building real software for yourself, using AI to help you every step of the way.

**You do not need to know how to code to start this guide.** You can ask AI to explain everything, install everything, and write the first version of everything. Your job is to understand what it's doing and gradually take over.

---

## What's in this repo

| File | What it does |
|------|--------------|
| `README.md` | This guide -- read it top to bottom |
| `SKILLS.md` | Your skill stack -- what to say to Codex at each stage of building |
| `CLAUDE.md` | Context file Codex reads to understand your project -- edit it as you build |
| `.env.example` | Template listing every secret your app needs -- copy to `.env`, never commit `.env` |
| `requirements.txt` | Python packages your app needs -- install with `pip install -r requirements.txt` |
| `tests/` | Automated tests -- run with `python -m pytest tests/ -v` |
| `.codex/skills/` | Pre-built Codex skills: plan, review, debug, commit, learn |
| `.githooks/pre-commit` | Runs before every commit and blocks you from accidentally committing secrets |
| `.github/workflows/ci.yml` | Runs your tests automatically every time you push code to GitHub |
| `.mcp.json` | Connects Codex to your GitHub repo so it can read your issues and PRs |

---

# The Guide

## Part 0 -- Read This First

### What you're going to build

By the end of this guide you will have built a real web app -- something that runs in a browser, saves data, and uses AI. It will be something *you* want to use, not a tutorial project.

Examples of things beginners have built:
- A private journal that summarises your week using GPT
- A habit tracker that gives you an encouraging message each morning
- A reading list with AI-generated summaries of each book
- A tool that emails you a daily digest of things you care about
- A recipe organiser that suggests meals based on what's in your fridge

None of these require a computer science degree. All of them are buildable by someone who has never coded before, using the tools in this guide.

---

### How AI changes the game for beginners

Traditionally, learning to code meant months of tutorials before you could build anything real. AI changes this completely.

**You can now ask AI to:**
- Set up your entire development environment step by step (install Python, Git, VS Code -- it will walk you through it)
- Plan your whole project before you write a single line of code
- Write the first version of any feature you describe in plain English
- Explain any error message and tell you exactly how to fix it
- Explain any concept as many times as you need, in different ways, until it clicks
- Review your code and point out what could go wrong
- Write tests for your code

**What you still need to do:**
- Understand what the code does (so you can fix it when it breaks)
- Make decisions about what to build and why
- Test that things actually work
- Learn gradually -- AI is your tutor, not a replacement for understanding

**The mental model:** AI is a very fast, very patient senior developer sitting next to you. It can write code faster than you. But you're the one deciding what to build, and you need to understand the code well enough to debug it when something goes wrong.

---

### The tools you'll use

OpenAI makes several things called "Codex." They're different products and it's confusing at first. Here's a plain-English breakdown:

| Product | What it is | Good for |
|---------|-----------|----------|
| **ChatGPT desktop app** | Chat interface — lives in your dock | Brainstorming, questions, planning, learning |
| **Codex App** | GUI coding agent — reads/edits your files, runs code | Actually building things |
| **Codex CLI** | Same as the Codex App but in your terminal | Same as above, keyboard-first |
| **ChatGPT web** (`chatgpt.com`) | Chat in a browser tab | Quick questions anywhere |

You need a **ChatGPT Plus subscription ($20/month)** to use all of these.

The **ChatGPT desktop app** and **Codex App** are two different downloads. Install both.

---

## Part 1 -- Set Up Your Tools

### Step 1.1 -- Install the ChatGPT desktop app first

Download the **ChatGPT desktop app** for Mac or Windows:
`openai.com/desktop`

This is a **chat interface** -- not a coding agent. It can't edit your files. Use it for:
- Brainstorming what to build
- Asking questions while you're looking at code
- Getting unstuck when something doesn't make sense
- Walking you through installing everything else

**How to use it to set up your machine:**

Open it and say:

> "I'm a complete beginner. I want to learn to build web apps with Python. Can you walk me through installing everything I need on my Mac? I need Python 3.12, Git, VS Code, Node.js, and the GitHub CLI. Tell me one step at a time and wait for me to confirm each step before moving on."

It will walk you through every step. You don't need to follow the rest of this section manually.

**If you prefer to install manually**, here's what you need:

| Tool | What it does | Install |
|------|-------------|---------|
| Python 3.12 | The programming language | `python.org/downloads` |
| Git | Saves versions of your code | `git-scm.com` |
| VS Code | Code editor (free) | `code.visualstudio.com` |
| Node.js | Required for Codex CLI | `nodejs.org` |
| GitHub CLI (`gh`) | Manage GitHub from the terminal | `brew install gh` (Mac) or `winget install GitHub.cli` (Windows) |

**Verify everything is installed:**
```bash
python3 --version   # should say Python 3.12.x
git --version       # should say git version 2.x
node --version      # should say v20.x or higher
gh --version        # should say gh version 2.x
```

### Step 1.1b -- Install the Codex App

The **Codex App** is the actual coding agent. It can read your project files, make edits, run commands, and commit to Git -- all from a graphical window on your desktop. This is the tool that builds things.

Download it from the GitHub releases page:
`github.com/openai/codex/releases`

Download the `.dmg` (Mac) or `.exe` (Windows), install it, and sign in with your OpenAI account.

**How the Codex App works:**
1. You open a project (point it at your project folder)
2. You describe what you want in plain English in the chat panel
3. It shows you exactly what it wants to change before doing anything
4. You approve or reject each change -- nothing happens without your say-so
5. You can see diffs, commit to Git, and push to GitHub all from inside the app

Three modes (start with the default):
- **Suggest** (default) -- proposes changes, you approve each one
- **Auto Edit** -- applies file changes automatically, asks before running commands
- **Full Auto** -- does everything automatically in a sandboxed folder

> The Codex App reads your `CLAUDE.md` file automatically -- that's how it understands your project. Keep it updated as you build.

---

### Step 1.2 -- Sign in to Codex

To **use Codex** (the desktop app, web app, VS Code extension, or CLI), you just sign in with your OpenAI account. That's it. No API key needed.

```bash
# If using the Codex CLI:
codex login
# Opens a browser -- sign in with your OpenAI account
```

The desktop app and web app work the same way -- just sign in. Codex uses OAuth, the same way you sign into any app with Google.

> **API keys are a separate thing.** You only need one when you want the *app you build* to call AI programmatically -- for example, your journal app calling GPT to summarise entries. We cover that in Part 4, and we'll start with a free option.

---

### Step 1.3 -- Set up GitHub

GitHub stores your code online. It's free and every developer uses it.

1. Sign up at `github.com`
2. Then authenticate the GitHub CLI:

```bash
gh auth login
# Choose: GitHub.com -> HTTPS -> Login with browser
```

---

### Step 1.4 -- When to use each tool

You now have two things installed: the ChatGPT desktop app (chat) and the Codex App (agent). Here's when to use what.

---

#### ChatGPT desktop app -- your thinking partner

Use this whenever you're thinking, not building.

**Best for:**
- **Brainstorming**: *"I want to build a habit tracker -- what features should I start with?"*
- **Planning**: *"Here's my idea. What order should I tackle things in?"*
- **Learning**: *"Explain what a database is like I've never heard of it"*
- **Debugging help**: screenshot your error, paste it in, describe what you tried
- **Understanding code**: paste anything and ask *"explain this line by line"*

**Important -- the ChatGPT desktop app is not deterministic.** The same question can get a different answer each time. This is fine for brainstorming and learning. It's a problem if you copy code you don't understand -- you won't be able to fix it when it breaks.

**Rule: never paste code into your project without understanding what each line does.** Ask the desktop app to explain it to you first.

---

#### Codex App -- your builder

Use this when you're ready to actually write code. Open your project folder in the Codex App and describe what you want built.

**Best for:**
- Scaffolding a new feature: *"Add a search bar that filters journal entries by keyword"*
- Fixing bugs: *"The form at /submit is throwing a 500 error -- here's the traceback"*
- Running your tests and fixing failures
- Committing and pushing to GitHub

The Codex App reads your files, proposes changes, and waits for your approval. It also has Git built in -- you can review diffs, commit, and push without leaving the app.

---

#### ChatGPT web (`chatgpt.com`) -- same as the desktop app, in a browser

Good for quick questions when you're not at your desk. Same non-determinism caveat applies.

---

#### VS Code extension -- AI inside your editor

Install the **ChatGPT extension** for VS Code (made by OpenAI):
```
VS Code -> Extensions (Ctrl+Shift+X) -> search "ChatGPT" -> install the one by OpenAI
```

Gives you a chat panel that can see the file you're editing. Good for inline questions without switching windows.

> Tip: **Cursor** (`cursor.com`) is a VS Code fork with deeper AI integration -- worth switching to once you're comfortable with VS Code basics.

---

#### Codex CLI -- same as the Codex App, in your terminal

```bash
npm install -g @openai/codex
codex login
cd ~/projects/my-journal-app
codex
```

Functionally identical to the Codex App but keyboard-driven. Use this if you prefer the terminal over a GUI -- otherwise the Codex App gives you the same power with a more visual interface.

---

**When to use what:**

| Situation | Tool |
|-----------|------|
| Brainstorming, questions, planning, learning | ChatGPT desktop app or web |
| Actually building -- creating files, running code, committing | Codex App |
| Inline help while editing a file | VS Code ChatGPT extension |
| Prefer terminal over GUI | Codex CLI instead of Codex App |

---

## Part 2 -- Your First Project

### Step 2.1 -- Decide what to build

Before touching any code, spend 20 minutes with the ChatGPT desktop app.

Open it and say:
> *"I want to build a personal project to learn coding. Here are some ideas: [list your ideas]. Help me pick the simplest one to start with. I want something I'll actually use. Ask me questions to help narrow it down."*

Come out with:
1. A one-sentence description of what you're building
2. A list of 3-5 features for the first version (no more)
3. A rough idea of what the main page looks like

Write these down. You'll put them in `CLAUDE.md` next.

---

### Step 2.2 -- Set up your project

```bash
# Clone this template
git clone https://github.com/zuhur-contentful/beginner-codex-starter ~/projects/my-first-app
cd ~/projects/my-first-app

# Copy the secrets template
cp .env.example .env

# Wire up the pre-commit hook (stops you committing secrets)
git config core.hooksPath .githooks
chmod +x .githooks/pre-commit

# Create your own GitHub repo
gh repo create my-first-app --public --source=. --push
```

Open in VS Code:
```bash
code ~/projects/my-first-app
```

---

### Step 2.3 -- Fill in CLAUDE.md

Open `CLAUDE.md` and replace the placeholder text with your actual project details. Codex reads this every session -- it's how Codex knows what you're building.

You can ask the desktop app to help:
> *"Help me write a CLAUDE.md for my project. It's [description]. Main features: [list]. I'm using Python and Flask."*

---

### Step 2.4 -- Fill in your .env file

Open `.env` and add your values:

```
OPENAI_API_KEY=sk-...your key from Step 1.2...
SECRET_KEY=...generate one below...
```

Generate a SECRET_KEY:
```bash
python3 -c "import secrets; print(secrets.token_hex(32))"
```

Copy the output into `.env`. This key secures your app's sessions.

**`.env` is already in `.gitignore` -- that's what stops it going to GitHub.**

---

### Step 2.5 -- Install dependencies and run

```bash
# Create a virtual environment (keeps this project's packages isolated)
python3 -m venv venv

# Activate it
source venv/bin/activate      # Mac/Linux
# venv\Scripts\activate       # Windows

# Install packages
pip install -r requirements.txt

# Run the starter test to confirm everything works
python -m pytest tests/ -v
```

You should see the placeholder test pass. You're ready to build.

---

### Step 2.6 -- Start building with the Codex App

Open the Codex App, click "Open Project", and select your `~/projects/my-first-app` folder.

Then describe what you want:

> *"I want to build a simple Flask web app. It should have one page where I can write a journal entry and save it to a SQLite database. Walk me through setting it up step by step, and explain each piece as you go."*

The Codex App will propose files to create, show you the code before writing it, and ask for your approval at each step. Review each change -- don't just approve everything blindly. Reading what it's doing is how you learn.

If you prefer the terminal, the Codex CLI does the same thing:
```bash
cd ~/projects/my-first-app
source venv/bin/activate
codex
```

---

## Part 3 -- Things You Need to Understand

Don't skip this section. These concepts come up in every project.

---

### Virtual environments -- why packages break

A virtual environment is an isolated Python installation for your project. Without it, packages from different projects conflict.

```bash
# Create once per project
python3 -m venv venv

# Activate every time you open a new terminal
source venv/bin/activate    # Mac/Linux
venv\Scripts\activate       # Windows

# You'll see (venv) in your prompt when it's active
(venv) $
```

**Common symptom:** `ModuleNotFoundError: No module named 'flask'`
**Fix:** `source venv/bin/activate`

---

### The .env pattern -- keeping secrets safe

Once your app starts making AI calls, it needs an API key. That key must never go into your code or onto GitHub.

```
.env.example   <- committed to GitHub (shows what's needed, no real values)
.env           <- NOT committed (has your real values)
```

In your code:
```python
from dotenv import load_dotenv
import os

load_dotenv()  # reads .env into environment variables

api_key = os.environ.get("OPENROUTER_API_KEY")
```

**Common symptom:** `KeyError: 'OPENROUTER_API_KEY'` or 401 errors
**Fix:** check `.env` exists, has the right key, and `load_dotenv()` is at the top of your file

---

### Git -- saving your work

Git is version control. Save points for your code. If you break something, you can go back.

```bash
# See what changed
git status

# Preview what you're about to save (do this before every commit)
git diff --staged

# Stage specific files -- never use "git add ." (can accidentally include .env)
git add main.py routes/journal.py

# Save with a message
git commit -m "feat: add journal entry form"

# Push to GitHub
git push
```

**Commit message format:**
```
feat: add new feature
fix: fix a bug
docs: update README
chore: update dependencies
```

---

### How to prompt Codex well

**Bad:**
> "fix my code"

**Good:**
> "My Flask route at `/submit` returns a 500 error when I submit the form. Here's the full error: [paste]. Here's the route code: [paste]. What's wrong?"

**Best -- give full context:**
> "I'm building a journal app. Here's my CLAUDE.md: [paste]. I'm working on search. When I search for 'monday' it only finds exact matches. Here's the search code: [paste]. How do I fix it?"

**Useful prompts:**
- "Explain this code to me line by line"
- "What could go wrong with this approach?"
- "What's the simplest way to add X?"
- "How would a more experienced developer do this differently?"
- "Write a test for this function"
- "I got this error -- what does it mean and how do I fix it?"

---

### Testing -- knowing when you break something

Tests are small pieces of code that verify your code works. Run them before every commit.

```python
# tests/test_journal.py
def test_entry_saves():
    from app import create_app
    app = create_app(testing=True)
    with app.test_client() as client:
        response = client.post("/submit", data={"entry": "Today was good"})
        assert response.status_code == 200

def test_empty_entry_rejected():
    from app import create_app
    app = create_app(testing=True)
    with app.test_client() as client:
        response = client.post("/submit", data={"entry": ""})
        assert response.status_code == 400
```

```bash
python -m pytest tests/ -v
```

Ask Codex: *"Write pytest tests for this function: [paste function]"*

---

## Part 4 -- Building AI Features

### Step 4.0 -- Get a free API key with OpenRouter

When you use Codex to *build* your app, you sign in with OAuth -- no key needed.

But when your *app itself* needs to call AI (for example, your journal app summarising your entries), it needs an API key. **Start with OpenRouter -- it's free.**

**OpenRouter** is a service that gives you access to many AI models through one API key. The free tier includes several capable models with no credit card required.

**Get your free OpenRouter key:**
1. Go to `openrouter.ai`
2. Sign up -- it's free, no credit card
3. Go to Keys -> Create Key
4. Copy it and put it in your `.env` file as `OPENROUTER_API_KEY`

**When to upgrade to a paid key:**
Once you've built something real and you're hitting the free tier limits, or you want access to the latest GPT-4o or Claude models, you can:
- Add OpenAI credits at `platform.openai.com` (pay as you go, a few dollars gets you a long way)
- Or keep using OpenRouter and add credits there (same models, one place)

Don't pay for anything until you've actually built something and know you need it.

---

### Calling AI from your app (using OpenRouter)

OpenRouter uses the same interface as the OpenAI SDK -- so the code looks identical, you just point it at a different URL.

```bash
pip install openai python-dotenv
pip freeze > requirements.txt
```

```python
from openai import OpenAI
from dotenv import load_dotenv
import os

load_dotenv()

# OpenRouter -- free tier, works with the openai SDK
client = OpenAI(
    api_key=os.environ.get("OPENROUTER_API_KEY"),
    base_url="https://openrouter.ai/api/v1",
)

def ask_ai(question: str, context: str = "") -> str:
    prompt = question
    if context:
        prompt = f"Context:\n{context}\n\nQuestion: {question}"

    response = client.chat.completions.create(
        model="mistralai/mistral-7b-instruct:free",  # free model on OpenRouter
        messages=[{"role": "user", "content": prompt}],
        max_tokens=1024,
    )
    return response.choices[0].message.content
```

> **When you're ready to upgrade:** change `base_url` to `https://api.openai.com/v1`, swap in your `OPENAI_API_KEY`, and use `model="gpt-4o-mini"`. The rest of the code stays identical.

---

### Three patterns you'll use constantly

**Summarise content:**
```python
def summarise_entries(entries: list[str]) -> str:
    combined = "\n---\n".join(entries)
    return ask_ai(
        "Summarise these journal entries in 3 bullet points. Focus on recurring themes.",
        context=combined
    )
```

**Answer questions about your data:**
```python
def answer_question(question: str, entries: list[str]) -> str:
    context = "\n---\n".join(entries[-20:])  # last 20 entries only
    return ask_ai(question, context=context)
```

**Extract structured data:**
```python
import json

def extract_mood(entry: str) -> dict:
    response = ask_ai(
        """Analyse this journal entry. Return a JSON object with:
        - mood: one of positive / negative / neutral / mixed
        - energy: number from 1 to 10
        - keywords: list of up to 5 keywords
        Return ONLY the JSON. No other text.""",
        context=entry
    )
    return json.loads(response)
```

---

## Part 5 -- Deploying Your App

### Free hosting options

| Service | Best for | Free tier |
|---------|----------|-----------|
| Render.com | Python/Flask backends | 750 hrs/month (sleeps when idle) |
| Vercel | Frontend (HTML/CSS/React) | Unlimited personal projects |
| Railway.app | Full apps with databases | $5/month free credit |
| Supabase | PostgreSQL database | 500MB free forever |

### Deploy to Render

1. Go to `render.com` -- sign up with GitHub
2. "New Web Service" -- select your GitHub repo
3. Build command: `pip install -r requirements.txt`
4. Start command: `python main.py`
5. Add your environment variables (copy from `.env`)
6. Click Deploy

### Before you deploy -- checklist

```bash
# Tests pass
python -m pytest tests/ -v

# requirements.txt is current
pip freeze > requirements.txt

# No secrets in code
git diff HEAD | grep -iE "api_key|password|secret"

# Push latest
git push
```

---

## Part 6 -- Training Resources

Do these in order. Each stage maps to where you are in the guide.

---

### Before anything else -- start here if you know nothing

These two courses are specifically designed for people with zero coding experience who want to build with AI. Do at least one before moving to Stage 0.

| Course | What it covers | Time | Cost |
|--------|---------------|------|------|
| [Replit -- AI Foundations: Master AI & Vibe Coding](https://learn.replit.com/) | Vibe coding, building apps without traditional programming, LLM basics -- runs inside Replit's browser IDE so nothing to install | ~30 min | Free |
| [DeepLearning.AI -- AI Python for Beginners](https://www.deeplearning.ai/short-courses/ai-python-for-beginners/) | Python fundamentals with AI assistance, writing/testing/debugging code, building real AI applications -- taught by Andrew Ng, 35 video lessons | ~10 hrs | Free |

**Replit first** if you want something quick and hands-on (30 min, runs in browser, no setup).
**DeepLearning.AI** if you want a proper structured foundation before touching this repo (10 hrs, the best beginner AI Python course available).

---

### Stage 0 -- Set up your tools and have your first Codex session

Goal: tools installed, Codex App running, first conversation done.

| Resource | What it covers | Time |
|----------|---------------|------|
| [ChatGPT desktop app](https://openai.com/desktop) | Download -- your chat/brainstorming tool | 10 min |
| [Codex App -- GitHub releases](https://github.com/openai/codex/releases) | Download -- the actual coding agent | 10 min |
| [OpenAI Help Centre -- Getting Started](https://help.openai.com/en/collections/3742473-chatgpt) | What ChatGPT and Codex can and can't do | 20 min |
| [CS50P -- Week 0 (Harvard, free)](https://cs50.harvard.edu/python/2022/weeks/0/) | First Python program, zero experience needed | 2 hrs |
| [Python.org Tutorial -- Chapters 1-3](https://docs.python.org/3/tutorial/) | Variables, strings, numbers, functions | 1 hr |

**Mini project:** Open the Codex App, point it at an empty folder, and say: "Create a Python script that asks for my name and prints Hello, [name]!" Approve the change, run it, see it work.

---

### Stage 1 -- First real app (weeks 2-4)

Goal: build something that runs in a browser and saves data.

| Resource | What it covers | Time |
|----------|---------------|------|
| [CS50P -- Weeks 1-3](https://cs50.harvard.edu/python/2022/) | Functions, conditionals, loops, exceptions | 6 hrs |
| [Flask Official Quickstart](https://flask.palletsprojects.com/en/stable/quickstart/) | Build a web app in 30 lines | 30 min |
| [Flask Mega-Tutorial -- Parts 1-4](https://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world) | Forms, databases, templates | 4 hrs |
| [SQLite Tutorial -- Python section](https://www.sqlitetutorial.net/sqlite-python/) | Save and retrieve data | 1 hr |
| [Git in 100 Seconds (YouTube)](https://www.youtube.com/watch?v=hwP7WQkmECE) | How version control works | 2 min |

**Mini project:** A to-do list app. Add items, check them off, delete them. Data saved to SQLite. Runs at `localhost:5000`.

---

### Stage 2 -- Add AI to your app (weeks 5-8)

Goal: make GPT do something useful inside an app you already built.

| Resource | What it covers | Time |
|----------|---------------|------|
| [DeepLearning.AI -- Jupyter AI: AI Coding in Notebooks](https://www.deeplearning.ai/short-courses/jupyter-ai-coding-in-notebooks/) | AI-assisted coding, generating and explaining code, analysing data -- beginner level, free | ~2 hrs |
| [OpenAI Platform Quickstart](https://platform.openai.com/docs/quickstart) | Your first API call | 20 min |
| [OpenAI Prompt Engineering Guide](https://platform.openai.com/docs/guides/prompt-engineering) | How to write prompts that work reliably | 30 min |
| [OpenAI Cookbook (GitHub)](https://github.com/openai/openai-cookbook) | Real code examples for common use cases | Reference |
| [OpenAI Python SDK (PyPI)](https://pypi.org/project/openai/) | Install docs and changelog | Reference |
| [Codex App + CLI README (GitHub)](https://github.com/openai/codex) | How the Codex agent works | 15 min |

**Mini project:** Add a "summarise my week" button to your to-do app. It sends your completed tasks to GPT and shows a plain-English summary.

---

### Stage 3 -- Real product (weeks 9-16)

Goal: build something you use every day. Deploy it. Write tests. Ship it.

| Resource | What it covers | Time |
|----------|---------------|------|
| [FastAPI Official Tutorial](https://fastapi.tiangolo.com/tutorial/) | Better alternative to Flask for APIs | 3 hrs |
| [Supabase Python Quickstart](https://supabase.com/docs/guides/getting-started/quickstarts/python) | Hosted PostgreSQL -- free tier | 30 min |
| [Pytest -- Getting Started](https://docs.pytest.org/en/stable/getting-started.html) | Write tests properly | 30 min |
| [Render Deployment -- Flask](https://render.com/docs/deploy-flask) | Put your app on the internet | 30 min |
| [GitHub Actions Quickstart](https://docs.github.com/en/actions/writing-workflows/quickstart) | Run tests automatically on every push | 20 min |

**Project:** Build something you actually need. Not a tutorial project. Something real. Deploy it. Tell someone about it.

---

### Stage 4 -- Going deeper (after week 16)

| Topic | Resource |
|-------|----------|
| User login / signup | [Supabase Auth Docs](https://supabase.com/docs/guides/auth) |
| Search by meaning, not keywords | [Supabase pgvector guide](https://supabase.com/docs/guides/ai/vector-columns) |
| Handle more users at once | [FastAPI async guide](https://fastapi.tiangolo.com/async/) |
| Build a proper frontend | [React official tutorial](https://react.dev/learn) |
| Package your app for deployment | [Docker Getting Started](https://docs.docker.com/get-started/) |
| Build your own AI agents | [OpenAI Agents SDK](https://openai.github.io/openai-agents-python/) |

---

## Part 7 -- When Things Break

### The debugging loop

```
1. Read the full error message (the last line is usually the actual problem)
2. Google the exact error message in quotes
3. Ask Codex/ChatGPT: paste the error + the relevant code + what you were trying to do
4. Make one change at a time
5. Run again
6. Repeat
```

### Common errors and fixes

| Error | Cause | Fix |
|-------|-------|-----|
| `ModuleNotFoundError: No module named 'flask'` | Virtual env not active | `source venv/bin/activate` then `pip install flask` |
| `KeyError: 'OPENROUTER_API_KEY'` | `.env` missing or `load_dotenv()` not called | `cp .env.example .env`, fill in values, add `load_dotenv()` at top of file |
| `Address already in use` | Port 5000 occupied | `lsof -i :5000` then `kill <PID>` |
| `401 Unauthorized` from OpenAI | Wrong or expired API key | Regenerate at `platform.openai.com/api-keys` |
| `429 Too Many Requests` | Hit rate limit | Wait; add `time.sleep(1)` between calls in loops |
| Flask shows blank 500 error | Exception hidden | Temporarily set `debug=True` to see the full traceback |
| `git: command not found` | Git not installed | Install from `git-scm.com` |

### Debugging checklist

```bash
# Is your virtual environment active?
which python   # should point to venv/bin/python

# Are your env vars loaded?
python3 -c "from dotenv import load_dotenv; import os; load_dotenv(); print(os.environ.get('OPENROUTER_API_KEY', 'NOT SET'))"

# Are packages installed?
pip list | grep flask

# What does the full error say?
python main.py 2>&1
```

### How to ask for help

1. What you expected to happen
2. What actually happened (paste the full error)
3. What you've already tried
4. The relevant code (just the broken bit)

---

## Quick reference

```bash
# Activate virtual environment
source venv/bin/activate

# Install packages
pip install <package-name>
pip freeze > requirements.txt   # save so others can install too

# Run your app
python main.py

# Run tests
python -m pytest tests/ -v

# Save your work
git add <files>
git commit -m "feat: describe what you did"
git push

# Start Codex CLI
codex
```
