---
description: Create a new experiment plan (labnote)
---

User input: $ARGUMENTS

Execute the experiment planning workflow:

1. Find the highest existing Exp## number:
   ```bash
   ls -1 notebook/labnote/Exp*.md 2>/dev/null | grep -oP 'Exp\K\d+' | sort -n | tail -1
   ```
   - If no experiments exist, start with Exp01
   - Otherwise increment by 1

2. Ask user for experiment details (consider $ARGUMENTS if provided):
   - Brief title/description (lowercase-with-hyphens)
   - Objective (what they want to accomplish - 1-2 sentences)
   - Input data path
   - Expected output location

3. Load template from `.claude/templates/labnote.md`

4. Replace placeholders:
   - [EXP_NUMBER] → next experiment number (zero-padded: 01, 02, etc.)
   - [TITLE] → user's title
   - [DATE] → current date (YYYY-MM-DD)
   - [DESCRIPTION] → lowercase description for file name
   - [OBJECTIVE] → user's objective
   - [INPUT_PATH] → user's input path
   - [OUTPUT_PATH] → results/Exp##_description
   - Leave [TOOL1], [VERSION], etc. as is for user to fill

5. Create file: `notebook/labnote/Exp##_description.md`

6. Report to user:
   - File created: [path]
   - Next steps:
     - Create config: `/exp-config Exp##`
     - Start working on the experiment
     - Update labnote: `/exp-update Exp##`

Keep it simple. Only ask for essential information.
