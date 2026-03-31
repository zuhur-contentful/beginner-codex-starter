# Skill: Commit Your Work

Use this when you're ready to save your progress to Git.

## How to trigger
Say: "commit this" or "save my work" or "commit what I just did"

## What to do

1. Run `git status` and show the user what files changed.
2. Run `git diff --staged` (or `git diff` if nothing staged yet) -- check for any secrets.
3. If any API keys, passwords, or secrets are visible in the diff, STOP and tell the user:
   "This diff contains what looks like a secret on line X. Move it to .env before committing."
4. Write a commit message in this format:
   ```
   type: short description of what changed

   Optional longer explanation if needed.
   ```
   Types: `feat` (new feature), `fix` (bug fix), `docs` (docs only), `chore` (maintenance)
5. Show the message to the user and ask: "Does this accurately describe what you did?"
6. After confirmation, run:
   ```bash
   git add [specific files]
   git commit -m "[message]"
   ```
7. Ask: "Do you want to push this to GitHub now? (`git push`)"

## Rules
- Never use `git add .` or `git add -A` -- always add specific files
- Always show the diff before committing so the user sees what they're saving
- If `.env` appears in `git status`, stop and explain why it must not be committed
- Keep commit messages short (under 72 characters for the first line)
- One logical change per commit -- don't bundle unrelated things together
