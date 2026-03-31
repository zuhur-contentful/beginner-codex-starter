# Assignments

This file tracks your progress through the 5 stages. The mentor skill reads it to know where you are and what comes next.

**How to update your stage:** tell Codex "I finished task [N]" or "mark task [N] done" and it will update this file.

---

## Current stage: 0
## Current task: 0.1

---

## Stage 0 — Understand Codex and get set up
*Goal: have the tools installed and run your first AI-assisted script*

- [ ] **0.1** Watch the Replit Vibe Coding course (30 min) — learn.replit.com
- [ ] **0.2** Install Python 3.12, Git, VS Code, and the Codex App — ask ChatGPT desktop to guide you through it step by step
- [ ] **0.3** Sign in to the Codex App with your ChatGPT Plus account
- [ ] **0.4** Watch CS50P Week 0 (2 hrs) — cs50.harvard.edu/python/2022/weeks/0/
- [ ] **0.5** Open this project in the Codex App and run your first session: ask Codex to create a Python script that asks your name and prints a greeting
- [ ] **0.6** Open the file Codex created and explain every line back to Codex — say "explain this line by line" for anything unclear

**You are ready for Stage 1 when:** you can open a Python file and explain what each line does in plain English.

---

## Stage 1 — Build your first real app
*Goal: a working web app with a database — input, save, display. No AI calls yet.*

- [ ] **1.1** Read Python.org Tutorial chapters 1–3 (1 hr) — docs.python.org/3/tutorial/
- [ ] **1.2** Watch Git in 100 Seconds — youtube.com/watch?v=hwP7WQkmECE
- [ ] **1.3** Read Flask Quickstart (30 min) — flask.palletsprojects.com/en/stable/quickstart/
- [ ] **1.4** Say "plan to-do list app" — agree on the scope with Codex before writing any code
- [ ] **1.5** Build the to-do app: add items, mark done, delete — runs at localhost:5000
- [ ] **1.6** Add SQLite: items persist when you restart the app
- [ ] **1.7** Say "review my code" — understand every issue Codex flags before moving on
- [ ] **1.8** Say "commit this" — make your first clean commit
- [ ] **1.9** Read CS50P Weeks 1–3 alongside building (6 hrs) — cs50.harvard.edu/python/2022/
- [ ] **1.10** Do the Codex for Builders course on OpenAI Academy — academy.openai.com/public/resources/codex-for-builders

**You are ready for Stage 2 when:** your to-do app runs at localhost:5000, saves to SQLite, and you can explain what a route, a template, and a database query each do.

---

## Stage 2 — Add AI to your app
*Goal: your app makes a real AI call and shows the result to the user*

- [ ] **2.1** Sign up for OpenRouter (free, no credit card) — openrouter.ai
- [ ] **2.2** Copy your `OPENROUTER_API_KEY` into `.env`
- [ ] **2.3** Read the OpenAI Platform Quickstart (20 min) — platform.openai.com/docs/quickstart
- [ ] **2.4** Say "plan AI summary feature" — plan how the AI call will fit into your app
- [ ] **2.5** Build it: add a button that sends your to-do list to an AI model and displays a plain-English summary
- [ ] **2.6** Say "explain this" on the API call function — make sure you understand what `messages`, `role`, and `content` mean
- [ ] **2.7** Read the OpenAI Prompt Engineering Guide — platform.openai.com/docs/guides/prompt-engineering
- [ ] **2.8** Improve your prompt so the summary is consistently useful
- [ ] **2.9** Say "review my code" — check for any API key leaks or missing error handling
- [ ] **2.10** Say "commit this" — clean commit before moving on

**You are ready for Stage 3 when:** clicking a button in your app sends a real API call and displays the result, and your API key is in `.env` not in your code.

---

## Stage 3 — Ship a real product
*Goal: something live on the internet with a real URL that you actually use*

- [ ] **3.1** Read Pytest Getting Started (30 min) — docs.pytest.org/en/stable/getting-started.html
- [ ] **3.2** Say "plan tests for my app" — write tests for your main features before deploying
- [ ] **3.3** Push to GitHub and confirm CI passes (green checkmark on your repo)
- [ ] **3.4** Sign up for Render.com with your GitHub account
- [ ] **3.5** Deploy your app to Render — follow render.com/docs/deploy-flask
- [ ] **3.6** Add your environment variables to Render's dashboard (never hardcode them)
- [ ] **3.7** Share the URL with one person and watch them use it
- [ ] **3.8** Fix the first thing that confuses them

**You are ready for Stage 4 when:** your app is live at a public URL, CI runs on every push, and at least one other person has used it.

---

## Stage 4 — Go deeper
*Goal: build more ambitious things on a solid foundation*

- [ ] **4.1** Add user login — Supabase Auth (supabase.com/docs/guides/auth)
- [ ] **4.2** Upgrade to Supabase PostgreSQL when SQLite stops being enough
- [ ] **4.3** Try the Codex 102 Workshop — github.com/openai/codex-102
- [ ] **4.4** Build your next idea from scratch using the full plan → build → review → commit loop

**There is no "done" here.** Keep building things you actually want to use.

---

## How the mentor reads this file

The mentor skill checks `## Current task:` to find where you are. After you complete a task, it updates the checkbox and the current task number. Your full history is in `.codex/memory/log.md`.
