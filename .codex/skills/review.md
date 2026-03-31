# Skill: Code Review (Beginner Mode)

Use this after writing a feature or fixing a bug. Reviews code and explains everything.

## How to trigger
Say: "review my code" or "check what I just wrote" or "is this code okay?"

## What to do

1. Read the files that were recently changed (check git diff).
2. For each issue found, explain:
   - What the problem is in plain English
   - Why it matters (what could go wrong)
   - How to fix it, with the corrected code shown
3. Also point out things that are done well -- learning what's right is as important as fixing what's wrong.
4. End with a summary: "Here's what to fix before moving on: [list]"

## What to check for (in priority order)

**Must fix:**
- Secrets or API keys hardcoded in the code (not in .env)
- SQL built with string concatenation instead of parameterized queries
- User input used directly without validation
- Unhandled exceptions that would crash the app silently

**Should fix:**
- Missing error handling around API calls
- Functions that do too many things at once
- Variable names that don't describe what they hold

**Good to know:**
- Code that works but could be simpler
- Missing tests for the happy path and the most obvious failure case

## Rules
- Explain every issue as if the reader has never seen it before
- Show the fixed version, not just "fix this"
- Don't overwhelm -- if there are more than 5 issues, focus on the must-fix ones first
- Never say "this is bad" -- say "here's a safer way to do this"
