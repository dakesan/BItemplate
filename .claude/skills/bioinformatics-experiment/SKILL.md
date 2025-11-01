---
name: bioinformatics-experiment
description: Manage bioinformatics experiment workflows - planning, clarification, execution tracking, and reporting. Use when creating experiment plans (labnotes), resolving ambiguities through Q&A, updating experiment progress, or generating analysis reports from completed experiments.
---

# Bioinformatics Experiment Management

## Overview

Provide structured workflows for managing bioinformatics experiments in an AI-first research environment. Enable systematic experiment planning, interactive clarification, progress tracking, and report generation with templates optimized for 60% AI-readable (structured) and 40% human-readable (interpretive) content.

## Core Philosophy: Deliberate and Thoughtful Writing

**CRITICAL**: All workflows must emphasize careful, step-by-step text composition. Each section should be:
- Written slowly and deliberately, one paragraph at a time
- Carefully proofread before moving to the next section
- Thoughtfully composed with attention to clarity and precision
- Never rushed - quality over speed

This is research documentation that will be read and built upon for months. Take the time to write it well.

## Core Capabilities

This skill provides four main workflows for managing bioinformatics experiments:

1. **Labnote Creation** - Create new labnote file (YYYYMMDD_title.md) for an experiment theme
2. **Experiment Addition** - Add new Exp## section to existing labnote
3. **Experiment Update** - Update Methods/Results within specific Exp## section
4. **Report Generation** - Generate formal lab report from labnote(s)

### Key Concepts

- **Labnote file**: One file per experiment theme (e.g., `20250125_squidiff-testing.md`)
- **Experiment sections**: Multiple `## 実験N: ExpNN (Purpose)` sections within one labnote
- **Careful composition**: Each section written deliberately, proofread before proceeding
- **Obsidian compatibility**: Uses callouts ([!Todo], [!Works], [!Done], [!Important]) and wikilinks

## Workflow Decision Tree

Determine which workflow to use based on user intent:

```
User request → Which workflow?

"Create new labnote" / "Start experiment series" / "New labnote file"
  → Labnote Creation Workflow (creates YYYYMMDD_title.md)

"Add Exp##" / "Add new experiment" / "Add experiment to labnote"
  → Experiment Addition Workflow (adds ## 実験N: ExpNN section)

"Update Exp##" / "Record results" / "Add methods to Exp##"
  → Experiment Update Workflow (updates specific Exp## section)

"Generate report" / "Create lab report" / "Formal report from labnote"
  → Report Generation Workflow (creates YYYYMMDD_project-lab-report.md)
```

## Workflow 1: Labnote Creation

### Purpose

Create a new labnote file for an experiment theme. This file will contain multiple experiment sections (Exp##) as the research progresses.

### When to Use

- Starting a new experiment theme (e.g., "squidiff-testing", "rnaseq-qc-validation")
- Beginning a series of related experiments
- Creating formal documentation for a research project

### Execution Steps

**IMPORTANT**: Work carefully and deliberately. Each piece of information should be thoughtfully composed.

1. **Request essential information from user**

   Ask user for:
   - **Date**: Experiment start date (YYYYMMDD format, e.g., 20250125)
   - **Title**: Brief experiment theme title (lowercase-with-hyphens, e.g., "squidiff-testing")
   - **Overall objective**: What is this experiment series trying to accomplish? (2-3 sentences)
   - **Background context**: Why is this important? Related research? (Optional, 1-2 sentences)

   **Never auto-generate dates or titles**. Always request from user.

2. **Load labnote template**

   Read template from: `assets/labnote.md`

3. **Replace placeholders thoughtfully**

   Take time to compose each replacement:
   - `[DATE_YYYYMMDD]` → User's date (e.g., 20250125)
   - `[DATE_YYYY-MM-DD]` → Formatted date (e.g., 2025-01-25)
   - `[TITLE]` → User's title
   - `[EXPERIMENT_THEME]` → Title with spaces (e.g., "Squidiff Testing")
   - `[OBJECTIVE]` → User's objective (carefully written)
   - `[BACKGROUND]` → User's background (if provided)
   - `[AUTHOR]` → From pyproject.toml or ask user

4. **Create labnote file**

   Write to: `notebook/labnote/[DATE_YYYYMMDD]_[title].md`

   Example: `notebook/labnote/20250125_squidiff-testing.md`

5. **Report completion to user**

   ```
   ✓ Labnote file created

   File: notebook/labnote/20250125_squidiff-testing.md
   Date: 2025-01-25
   Theme: Squidiff Testing

   This labnote is ready to receive experiment sections (Exp01, Exp02, etc.)

   Next steps:
   - Use Experiment Addition Workflow to add your first experiment (Exp01)
   - Fill in Background section with detailed context
   - Begin executing experiments and documenting results
   ```

See `references/workflow-exp-plan.md` for detailed instructions.

## Workflow 2: Experiment Addition

### Purpose

Add a new experiment section (## 実験N: ExpNN) to an existing labnote file. Each experiment represents a distinct trial, condition test, or analysis phase within the overall experiment theme.

### When to Use

- Adding the first experiment (Exp01) to a newly created labnote
- Adding follow-up experiments (Exp02, Exp03, etc.) to an ongoing research theme
- Documenting a new experimental condition or parameter variation

### Execution Steps

**IMPORTANT**: Write each section carefully. This is permanent research documentation.

1. **Identify target labnote and experiment number**

   Ask user for:
   - **Labnote file**: Which labnote file? (e.g., "20250125_squidiff-testing.md")
   - **Experiment ID**: Which experiment number? (e.g., "Exp01", "Exp02")
   - **Experiment purpose**: Brief description of this specific experiment (e.g., "Initial parameter exploration", "Validation with real data")

   **User must provide experiment number**. Never auto-increment.

2. **Find and read existing labnote**

   - Locate file in `notebook/labnote/YYYYMMDD_title.md`
   - If file doesn't exist, suggest using Labnote Creation Workflow first
   - Read entire file to understand context

3. **Gather experiment details**

   Ask user thoughtfully:
   - **Date performed**: When was/will this experiment be conducted? (YYYY-MM-DD)
   - **Experiment objective**: What specifically does this experiment aim to test? (1-2 sentences)
   - **Sample information**: What samples/data are being used? (Optional)
   - **Planned approach**: What methods will be used? (Brief outline, 2-3 bullets)

4. **Compose new experiment section**

   Carefully write the new section:

   ```markdown
   ## 実験N: ExpNN (Purpose/Phase)

   >[!Works] [Experiment Type/Description]
   >
   >### 実験情報
   >- **試験番号**: ExpNN
   >- **実施日**: YYYY-MM-DD
   >- **作業者**: [Author]
   >- **目的**: [Specific objective]
   >
   >### 実験設計
   >- [Design details]
   >- [Sample information]
   >- [Controls and variables]
   ```

5. **Insert section into labnote**

   - Insert before the final Results/Discussion sections
   - Maintain proper Obsidian callout syntax
   - Preserve existing formatting

6. **Report completion to user**

   ```
   ✓ Experiment section added

   File: notebook/labnote/20250125_squidiff-testing.md
   Section: ## 実験1: Exp01 (Initial parameter exploration)

   Next steps:
   - Execute the experiment
   - Use Experiment Update Workflow to add Methods and Results
   - Document observations as they occur
   ```

See `references/workflow-exp-add.md` for detailed instructions.

## Workflow 3: Experiment Update

### Purpose

Update a specific experiment section (Exp##) within a labnote file with Methods, Results, or additional observations. This is used during and after experiment execution to document what was actually done and what was observed.

### When to Use

- Recording experimental procedures (Methods)
- Documenting results and observations (Results)
- Adding notes about issues, unexpected findings, or deviations from plan
- Updating any part of an existing Exp## section

### Execution Steps

**IMPORTANT**: Document thoroughly. Future you (6 months from now) needs to understand exactly what happened.

1. **Identify target experiment section**

   Ask user for:
   - **Labnote file**: Which labnote? (e.g., "20250125_squidiff-testing.md")
   - **Experiment ID**: Which experiment section? (e.g., "Exp01")
   - **Update type**: What are you updating? (Methods / Results / Observations / Other)

2. **Read existing labnote and locate section**

   - Find file: `notebook/labnote/YYYYMMDD_title.md`
   - Locate the `## 実験N: ExpNN` section
   - Read existing content to understand context

3. **Gather update content based on type**

   **For Methods updates**:
   - Ask: What step/procedure was performed?
   - Ask: Why this approach? (Rationale)
   - Ask: Command executed? (Full command with all parameters)
   - Ask: Any important parameters to highlight?

   Compose in this format:
   ```markdown
   >### [Step Title]
   >
   >**Why**: [Rationale for this approach]
   >
   >```bash
   >[COMPLETE_COMMAND]
   >```
   >
   >**Parameters**:
   >- [PARAM1]: [VALUE] - [EXPLANATION]
   >- [PARAM2]: [VALUE] - [EXPLANATION]
   ```

   **For Results updates**:
   - Ask: What were the key findings?
   - Ask: Any quantitative metrics? (Numbers, percentages, counts)
   - Ask: Any figures or tables to reference?

   Compose carefully with specific numbers and observations.

4. **Insert or append to appropriate subsection**

   Within the `## 実験N: ExpNN` section:
   - **Methods** go under `>[!Works]` callout
   - **Results** go under `>[!Done]` callout (create if doesn't exist)
   - **Issues/Notes** go under `>[!Important]` callout

   Preserve existing Obsidian callout syntax.

5. **Report completion to user**

   ```
   ✓ Experiment section updated

   File: notebook/labnote/20250125_squidiff-testing.md
   Section: ## 実験1: Exp01
   Updated: Methods (added FastQC execution)

   The update has been integrated into the appropriate callout section.
   ```

### Documentation Quality Guidelines

- **Be specific**: "Q-score ≥30" not "good quality"
- **Include units**: "16 threads" not "many threads"
- **Record failures**: Document what didn't work and why
- **Commands must be reproducible**: Include full paths, all parameters
- **Future-proof**: Write for someone reading this 6 months later

See `references/workflow-exp-update.md` for detailed instructions.

## Workflow 4: Report Generation

### Purpose

Generate a formal lab report from one or more labnote files. Reports are polished, formal documents suitable for sharing with collaborators, publication supplementary materials, or institutional records.

### When to Use

- Completing a research project or milestone
- Preparing results for presentation or publication
- Creating formal documentation for institutional requirements
- Summarizing a series of experiments for decision-making

### Execution Steps

**IMPORTANT**: Reports are formal documents. Write with extra care and attention to clarity.

1. **Identify source labnotes**

   Ask user for:
   - **Source labnote(s)**: Which labnote file(s)? (e.g., "20250125_squidiff-testing.md")
   - **Date for report**: Report creation date (YYYYMMDD)
   - **Report title**: Formal title for this report (e.g., "squidiff-validation-results")
   - **Author**: Who is authoring this report?

2. **Read and analyze source labnotes**

   For each labnote:
   - Read entire file
   - Extract Background/Objective
   - Collect all Exp## sections
   - Gather Methods from `>[!Works]` callouts
   - Gather Results from `>[!Done]` callouts
   - Note any `>[!Important]` issues or observations

3. **Ask for report specifics**

   Get user input:
   - **Executive summary**: 1-2 paragraph summary of key findings
   - **Main conclusions**: What are the takeaway messages? (2-3 bullets)
   - **Recommendations**: What should happen next?
   - **Status**: draft / review / final

4. **Load and populate lab report template**

   Read template from: `assets/lab-report.md`

   Auto-fill from labnotes:
   - `[DATE_YYYYMMDD]` → Report date
   - `[DATE_YYYY-MM-DD]` → Formatted date
   - `[PROJECT_NAME]` → Title
   - `[AUTHOR]` → Author name
   - `[STATUS]` → Report status
   - `[EXECUTIVE_SUMMARY]` → User's summary
   - `[BACKGROUND]` → From labnote Background
   - `[METHODS]` → Aggregated from all Exp## Methods
   - `[RESULTS]` → Aggregated from all Exp## Results
   - `[CONCLUSIONS]` → User's conclusions
   - `[LABNOTE_REFS]` → List of source labnotes

5. **Create report file**

   Write to: `notebook/report/[DATE_YYYYMMDD]_[project-name]-lab-report.md`

   Example: `notebook/report/20250201_squidiff-validation-lab-report.md`

6. **Report completion to user**

   ```
   ✓ Lab report generated

   File: notebook/report/20250201_squidiff-validation-lab-report.md
   Source: notebook/labnote/20250125_squidiff-testing.md
   Status: draft

   Auto-filled sections:
   - Executive Summary, Background, Methods, Results, Conclusions

   Sections requiring human review:
   - Discussion (interpretation and implications)
   - Recommendations (next steps)
   - Review and polish all auto-filled content

   This is a FORMAL document. Please review carefully before sharing.
   ```

### Report Quality Guidelines

- **Formal tone**: Professional language suitable for external sharing
- **Complete context**: Readers should not need to reference labnotes
- **Clear figures**: All figures referenced with captions
- **Reproducible**: Sufficient detail for others to replicate
- **Decision-ready**: Conclusions and recommendations clearly stated

See `references/workflow-report-gen.md` for detailed instructions.

## Project Context

### Directory Structure

Assume project follows this structure:
```
notebook/
├── labnote/          # Experiment logs (Exp##_*.md)
├── analysis/         # Jupyter notebooks
├── report/           # Final reports (Exp##_*.md)
└── knowledge/        # Background documentation

results/              # Analysis outputs (gitignored)
└── Exp##_*/

config/               # YAML configuration files
└── YYYYMMDD_Exp##_*.yaml

pyproject.toml        # Project settings (compute resources)
```

### Compute Resources

Default resources from `pyproject.toml`:
```toml
[tool.bioinfo-experiment.compute]
total_cores = 128
total_memory_gb = 512
default_cores = 90        # 70% of total
default_memory_gb = 358   # 70% of total
```

Use these defaults unless experiment requires different allocation.

### File Naming Conventions

- Labnotes: `Exp##_description.md`
- Reports: `Exp##_report.md` or `Exp##-##_report.md`
- Configs: `YYYYMMDD_Exp##_description.yaml`
- Results: `results/Exp##_description/`

All experiment numbers zero-padded to 2 digits (01, 02, ..., 10, 11, ...).

## Templates

This skill includes three templates in `assets/`:

1. **labnote.md** - Experiment log template with Trial-based structure
2. **report.md** - Analysis report template with citation system
3. **config.yaml** - Optional configuration file template

Templates use placeholder syntax: `[PLACEHOLDER_NAME]`

## Workflow References

Detailed procedural instructions available in `references/`:

- `workflow-exp-plan.md` - Experiment Planning Workflow
- `workflow-exp-clarify.md` - Experiment Clarification Workflow
- `workflow-exp-update-labnote.md` - Labnote Update Workflow
- `workflow-exp-report.md` - Report Generation Workflow

Load relevant reference files as needed for comprehensive instructions.

## Usage Examples

**Creating new experiment:**
```
User: "Create a new experiment for RNA-seq quality control"
→ Use Experiment Planning Workflow
→ Assign Exp##, create labnote from template
→ Recommend running Clarification Workflow
```

**Clarifying experiment plan:**
```
User: "Clarify Exp03 - I need to define the inputs"
→ Use Experiment Clarification Workflow
→ Prioritize input/output path questions
→ Update labnote with absolute paths and formats
```

**Recording execution:**
```
User: "I ran FastQC on the samples, update Exp03"
→ Use Labnote Update Workflow
→ Add command, parameters, and results to labnote
```

**Generating report:**
```
User: "Create a report for Exp01-03"
→ Use Report Generation Workflow
→ Extract data from labnotes
→ Create report with auto-filled facts, leave interpretations for user
```

## Best Practices

1. **Keep labnotes simple** - Record facts, commands, and observations
2. **Prioritize path clarity** - Always use absolute paths in clarifications
3. **Update incrementally** - Update labnotes during execution, not after
4. **Report thoughtfully** - Reports need human interpretation and insight
5. **Follow numbering** - Always check highest Exp## and increment
6. **Use templates** - Leverage provided templates for consistency
7. **Validate paths** - Ensure input/output paths exist and are correct
8. **Document rationale** - Record "why" decisions were made
9. **Include metrics** - Always provide specific numbers and measurements
10. **Cite sources** - In reports, cite labnotes, figures, and data files
