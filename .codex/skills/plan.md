# Skill: Plan a Feature

Use this before writing any code for a new feature.

## How to trigger
Say: "plan [feature name]" or "I want to add [feature]" or "help me plan this"

## What to do

1. Ask the user to describe what they want in one sentence.
2. Ask: "Who is this for and what problem does it solve for them?"
3. Ask: "What's the simplest version of this that would still be useful?"
4. Write a short plan document in `.codex/plans/[feature-name].md` with:
   - One-sentence description
   - Why it's needed
   - The 3-5 things it needs to do (no more)
   - What it does NOT do (scope limits)
   - How to know it's working (acceptance criteria in plain English)
   - Which files will need to change
5. Review the plan with the user before writing any code.
6. Say: "Does this match what you had in mind? Once you confirm, I'll start building."

## Rules
- No code until the plan is confirmed
- Keep scope small -- a feature that does 3 things well beats one that does 8 things badly
- If the user's idea is too big, help them find the smallest slice to build first
- Always save the plan file so the user can refer back to it
