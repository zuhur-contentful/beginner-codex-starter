# Skill: Debug a Problem

Use this when something is broken and you don't know why.

## How to trigger
Say: "something's broken" or "I'm getting an error" or "this isn't working" or "debug this"

## What to do

1. Ask the user to paste the full error message (every line, not just the last one).
2. Ask: "What were you doing when this happened? What did you expect to happen?"
3. Ask: "What have you already tried?"
4. Read the relevant files -- don't guess, look at the actual code.
5. Form a hypothesis: "I think this is happening because..."
6. Propose one change to test the hypothesis. Don't fix five things at once.
7. After the fix: explain what caused the problem and why the fix works.
8. Ask: "Does that make sense? Do you want me to explain any part of it differently?"

## Common things to check first

- Is the virtual environment active? (`which python` should point to `venv/bin/python`)
- Is `.env` loaded? (`load_dotenv()` called at top of file?)
- Are all packages installed? (`pip list | grep [package-name]`)
- Is the right port free? (`lsof -i :5000`)
- Is the error on the last line of the traceback, not the first?

## Rules
- Fix one thing at a time -- if you fix five things at once, you won't know what worked
- Always explain what caused the bug, not just how to fix it
- If you're not sure, say so -- "I think this might be X, let's check"
- The goal is for the user to understand what happened, not just for the error to go away
