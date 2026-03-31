# Skill: Save Session Memory

Run this automatically at the end of every session to log what happened.

## How to trigger
Say: "save memory" or "end session" or "we're done for today" or "goodbye" or "see you later"

Also run this automatically whenever the user says goodbye or signals they are done.

## Prompting the learner to save

After every feature is completed or committed, say:
"Good work. Before you close — say 'save memory' or just 'done for today' and I'll log this session so we pick up exactly here next time."

If the learner has been working for more than 30 minutes without saving, remind them once:
"Quick reminder — say 'save memory' before you close so I remember where we got to."

## What to do

1. Read `.codex/memory/log.md` if it exists (to append, not overwrite).
2. Read `git log --oneline -10` to see what was committed this session.
3. Read `git diff HEAD~5..HEAD --stat` to see what files changed recently.
4. Write a new dated entry to `.codex/memory/log.md` in this exact format:

```
## [DATE] — Session [N]

### What we built
- [bullet: each feature or file added]

### What broke and how we fixed it
- [bullet: error message → what caused it → what fixed it]
- (write "nothing broke" if nothing broke)

### Decisions made
- [bullet: any choices about how to do something and why]
- e.g. "chose SQLite over Supabase because the app is single-user for now"

### What the learner understood
- [bullet: concepts they asked about or demonstrated understanding of]

### Current stage
- Stage [0/1/2/3/4] — [stage name]

### Next thing to do
- [one clear sentence: the next concrete task]
```

5. After writing, say: "Session saved. Next time we open this project, I'll remember everything we did. Your next task is: [next thing to do]."

## Rules
- Always append — never overwrite existing entries
- Date format: YYYY-MM-DD
- Keep each bullet to one line
- If nothing was committed, still write the entry based on what was discussed
- The "next thing to do" must be specific and actionable, not vague like "keep building"
