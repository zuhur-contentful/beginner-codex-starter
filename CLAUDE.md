# CLAUDE.md

## Session behaviour

**On every session start:** read `.codex/memory/log.md` and `.codex/assignments.md`, then run the mentor skill — greet the learner with a one-sentence recap of last session and their next task.

**On every session end:** run the memory skill — write a structured entry to `.codex/memory/log.md` covering what was built, what broke, decisions made, and next task.

---

## Project Overview

PROJECT_DESCRIPTION

**Repo:** github.com/GITHUB_ORG/PROJECT_NAME
**Deploy:** DEPLOY_URL

---

## Tech Stack

| Layer | Technology |
|---|---|
| Language | Python 3.12 |
| Web framework | Flask (simple) or FastAPI (if you want type hints) |
| Database | SQLite (local) or Supabase (free hosted PostgreSQL) |
| AI coding assistant | OpenAI Codex (via ChatGPT Plus — `codex` CLI) |
| AI in your app | OpenAI API (`openai` Python SDK) |
| Frontend | Plain HTML + CSS, or React if you want to go further |
| Hosting | Render.com free tier (backend), Vercel (frontend) |

> Beginner tip: Start with Flask + SQLite. You can always upgrade later.
> Codex tip: Run `codex` in your project folder and describe what you want to build in plain English.

---

## Key Directories

```
my-project/
  main.py          — app entry point
  routes/          — URL handlers (one file per feature)
  templates/       — HTML templates (if using Flask)
  static/          — CSS, images, JS files
  models/          — data models (database tables)
  tests/           — automated tests
  .env             — your secrets (NEVER commit this)
  .env.example     — template showing which secrets are needed
  requirements.txt — list of Python packages
```

---

## Development Commands

```bash
# First time setup — create virtual environment
python3 -m venv venv
source venv/bin/activate      # Mac/Linux
# venv\Scripts\activate       # Windows

# Install dependencies
pip install -r requirements.txt

# Run the app locally
python main.py
# → open http://localhost:5000 in your browser

# Run tests
python -m pytest tests/ -v

# Add a new package
pip install <package-name>
pip freeze > requirements.txt   # save it so others can install it too
```

---

## Secrets & Environment

Your secrets live in `.env` locally. **Never commit `.env` to GitHub.**

```bash
# Copy the template
cp .env.example .env
# Open .env and fill in your real values
```

Required env vars (see `.env.example`):
- `OPENROUTER_API_KEY` — free API key for AI calls in your app (get it from openrouter.ai — no credit card)
- `SECRET_KEY` — a random string used to secure your app (generate with: `python3 -c "import secrets; print(secrets.token_hex(32))"`)

---

## Active MCP Servers

See `.mcp.json`. Configured:
- **github** — lets Codex read your GitHub issues, PRs, and code

---

## Security Rules (beginner version)

The most important things to know:

- **Never hardcode passwords or API keys in your code.** Use `.env` files.
- **Never commit `.env` to GitHub.** It's in `.gitignore` for a reason.
- **Validate what users type in.** Never trust form input without checking it.
- **Use parameterized queries for databases.** Never build SQL with f-strings.

```python
# CORRECT — parameterized query (safe from SQL injection)
cursor.execute("SELECT * FROM users WHERE email = ?", (email,))

# NEVER — string concatenation in SQL (dangerous!)
cursor.execute(f"SELECT * FROM users WHERE email = '{email}'")
```

---

## Error Handling

```python
# CORRECT — catch specific errors with context
try:
    result = call_some_api()
except requests.Timeout:
    print("API call timed out — try again")
    return None
except Exception as err:
    print(f"Unexpected error: {err}")
    raise

# AVOID — swallowing errors silently
try:
    result = call_some_api()
except:
    pass  # never do this — you'll never know what broke
```

---

## Known Beginner Pitfalls

**Forgetting to activate your virtual environment**
```bash
# You'll see "ModuleNotFoundError" — fix it with:
source venv/bin/activate   # Mac/Linux
```

**Committing secrets to GitHub**
```bash
# Check before committing:
git diff --staged | grep -i "api_key\|password\|secret"
# If you see anything, remove it first
```

**Not saving dependencies**
```bash
# After pip install, always run:
pip freeze > requirements.txt
```

**Flask in debug mode in production**
```python
# CORRECT for local dev only
app.run(debug=True)

# NEVER in production — exposes your source code
# Use environment variables to control this:
app.run(debug=os.environ.get("FLASK_DEBUG", "false") == "true")
```
