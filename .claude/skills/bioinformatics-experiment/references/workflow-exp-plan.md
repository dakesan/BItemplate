# Labnote Creation Workflow

## Purpose

Create a new Obsidian-compatible labnote file with proper frontmatter, callouts, and structure.

## Execution Steps

### 1. Request Essential Information from User

**IMPORTANT**: Never auto-generate dates or titles. Always ask the user.

Ask user for:
- **Date**: Experiment date in YYYYMMDD format (e.g., 20250125)
- **Title**: Brief experiment title in lowercase-with-hyphens (e.g., "rnaseq-qc")
- **Objective**: What you want to accomplish (1-2 sentences)
- **Background**: Why this is important (Optional, 1-2 sentences)
- **Purpose**: Specific experimental purpose or hypothesis
- **Author**: Researcher name
- **Tags**: Additional tags for categorization (e.g., "rnaseq", "quality-control")

### 2. Load Labnote Template

Read template from: `assets/labnote.md`

### 3. Replace Frontmatter and Initial Placeholders

Take time to carefully compose each replacement:

**Frontmatter (YAML)**:
- `[DATE_YYYY-MM-DD]` → Formatted date (e.g., 2025-01-25)
  - Used for both `cdate` and `mdate` fields
- `[TAG1]` → User's tags (e.g., "rnaseq", "quality-control")
  - Can be multiple tags: `tags: [labnote, rnaseq, qc]`
- `[AUTHOR]` → User's name (e.g., "Hiro")
- `status` → Keep as "in-progress"

**Background Section (>[!Todo] callout)**:
- `[BACKGROUND]` → User's background text
- `[TRIAL_ID]` → Trial ID if applicable (or remove line if not needed)
- `[OBJECTIVE]` → User's overall objective

**Purpose Section (>[!Works] callout)**:
- `[PURPOSE]` → User's specific purpose/hypothesis
- `[HYPOTHESIS]` → Additional hypothesis details (or placeholder)

**Results Summary Section (>[!Done] callout)**:
- Leave template placeholders for user to fill later

**Key Points Section (>[!Important] callout)**:
- Leave template placeholders for user to fill later

**Experimental Timeline Table**:
- `[DATE_YYYY-MM-DD]` → User's experiment date(s)
- `[EXP_NAME]` → Placeholder for experiment names
- Leave as placeholders for user to update as experiments progress

**Individual Experiment Sections (Exp1, Exp2, etc.)**:
- `[DATE_YYYY-MM-DD]` → User's experiment date
- `[EXP_TITLE]` → Placeholder (e.g., "実験タイトル")
- `[EXP_PURPOSE]` → Placeholder
- `[HYPOTHESIS]` → Placeholder
- All other fields in Materials, Procedure, Results, Discussion → Keep as placeholders
- User will fill these in as experiments are performed

**Bottom Sections (総合考察と結論)**:
- Leave all placeholders as-is
- User will fill these in after completing experiments

### 4. Create Labnote File

Write to: `notebook/labnote/[DATE_YYYYMMDD]_[title].md`

Example: `notebook/labnote/20250125_rnaseq-qc.md`

### 5. Report Completion to User

Provide clear feedback:

```
✓ Labnote file created

File: notebook/labnote/20250125_rnaseq-qc.md
Date: 2025-01-25
Format: Obsidian-compatible with callouts

Frontmatter configured:
- cdate/mdate: 2025-01-25
- tags: [labnote, rnaseq, qc]
- status: in-progress
- author: Hiro

Sections filled:
- Background with objective
- Purpose with hypothesis

Sections ready to fill:
- Results Summary (update as experiments complete)
- Experimental Timeline (update as you add experiments)
- Individual experiment sections (Exp1, Exp2, etc.)
- 総合考察と結論 (fill after all experiments complete)

Next steps:
- Fill in experiment sections (Exp1, Exp2, etc.) with details
- Update Experimental Timeline table as you add experiments
- Update Results Summary with key findings
- Use Labnote Update Workflow to modify sections as needed
```

## Important Notes

- **Never auto-generate dates**: Always ask the user for the date
- **Never auto-generate titles**: Always ask the user for the title
- **Preserve Obsidian syntax**: Maintain callout format `>[!Type]`
- **Keep placeholders**: Don't try to fill all placeholders - many are for user to complete later
- **YAML frontmatter**: Ensure proper YAML syntax with correct indentation
- **File naming**: Use YYYYMMDD_lowercase-with-hyphens.md format

## Template Placeholder Reference

Placeholders filled during creation:
- `[DATE_YYYY-MM-DD]` - Formatted date (2025-01-25)
- `[TAG1]` - User's tags
- `[AUTHOR]` - User's name
- `[BACKGROUND]` - User's background text
- `[OBJECTIVE]` - User's objective
- `[PURPOSE]` - User's purpose/hypothesis
- `[TRIAL_ID]` - Trial ID (optional)

Placeholders left for user to fill:
- `[EXP_TITLE]` - Experiment titles
- `[EXP_PURPOSE]` - Specific experiment purposes
- `[HYPOTHESIS]` - Detailed hypotheses
- All Materials, Procedure, Results, Discussion fields
- 総合考察 (Overall discussion) sections
- 推奨事項 (Recommendations) sections
