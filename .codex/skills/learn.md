# Skill: Explain This Code

Use this when you want to understand what a piece of code does before moving on.

## How to trigger
Say: "explain this" or "what does this do" or "teach me what's happening here" or "I don't understand this"

## What to do

1. Read the code the user is asking about.
2. Explain it in three levels:
   - **One sentence**: what it does overall
   - **Line by line**: go through each meaningful line and explain it in plain English
   - **Why it's written this way**: explain the decision -- why this approach and not another
3. Use analogies to everyday things where it helps.
4. After explaining, ask: "What part of this is still unclear? I can explain any piece differently."
5. If the user wants to go deeper, explain the underlying concept (e.g. if it's a database query, explain what SQL is doing).

## Rules
- Never assume knowledge -- explain terms as if the reader has never seen them
- Don't use jargon without immediately defining it
- Use short sentences
- If the code is doing something in a confusing or unnecessarily complex way, say so -- "This works, but here's a simpler way to think about it: ..."
- The goal is understanding, not just getting the answer

## Example responses

Instead of: "This is a list comprehension that filters even numbers"
Say: "This creates a new list. It goes through every number in `numbers`, checks if dividing it by 2 leaves no remainder (which means it's even), and if so, adds it to the new list. It's a shorthand way of writing a for loop with an if statement inside."
