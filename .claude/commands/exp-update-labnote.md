---
description: Update experiment labnote with command results
---

User input: $ARGUMENTS

Execute the labnote update workflow:

1. Parse experiment number from $ARGUMENTS or ask user:
   - Format: Exp## (e.g., Exp01, Exp02)

2. Find and read labnote file:
   - Path: `notebook/labnote/Exp##_*.md`
   - If not found, suggest `/exp-plan` first

3. Ask user what to add:
   - New process step with command
   - Results/observations
   - Issues encountered
   - Tool versions (if new tool used)

4. For new process step, get:
   - Step name/action
   - Brief thought or reason (why this step)
   - Command with all parameters
   - Result (what happened - numbers, metrics, status)

5. Append to Process section in timeline format:
   ```markdown
   ### Step N: [ACTION]

   [THOUGHT]

   \`\`\`bash
   [COMMAND]
   \`\`\`

   Result: [RESULT]
   ```

6. If adding to Results Summary or Next Steps:
   - Append bullet points with findings/metrics
   - Include specific numbers and observations

7. Save updated file

8. Report to user:
   - Updated: [file path]
   - What was added

Keep additions simple and factual. Record what was done and what happened.
