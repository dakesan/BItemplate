---
description: Create analysis report from experiments
---

User input: $ARGUMENTS

Execute the report creation workflow:

1. Parse experiment range from $ARGUMENTS or ask user:
   - Single: Exp## (e.g., Exp03)
   - Range: Exp##-Exp## (e.g., Exp01-Exp03)

2. Read corresponding labnotes to gather context:
   - Files: `notebook/labnote/Exp##_*.md`
   - Extract objectives, methods, key findings
   - Note tool versions and commands

3. Ask user for report details:
   - Report title
   - Main findings to highlight
   - Biological interpretations (if ready)
   - Author name

4. Load template from `.claude/templates/report.md`

5. Replace placeholders:
   - [TITLE] → user's report title
   - [EXP_RANGE] → Exp## or Exp##-Exp##
   - [DATE] → current date (YYYY-MM-DD)
   - [AUTHOR] → user's name
   - [OBJECTIVE] → extracted from labnotes
   - [DATA_DESCRIPTION] → summarize from labnotes
   - [STEP1], [STEP2] → major pipeline steps from labnotes
   - [LABNOTE_REFS] → list of labnote files
   - [TOOL1], [VERSION] → extract from labnotes
   - Leave interpretation placeholders for user to fill

6. Create file: `notebook/report/Exp##_report.md` or `Exp##-##_report.md`

7. Report to user:
   - Report created: [path]
   - Sections to complete:
     - Fill in interpretations
     - Add biological implications
     - Discuss findings thoroughly
   - This is for HUMANS - write clearly and completely

Auto-fill factual information from labnotes. Leave interpretation sections for user input.
