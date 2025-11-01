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

- User requests creating a new experiment
- Starting a new analysis or pipeline
- Beginning a new phase of research

### Execution Steps

1. **Find next experiment number**

   ```bash
   ls -1 notebook/labnote/Exp*.md 2>/dev/null | grep -oP 'Exp\K\d+' | sort -n | tail -1
   ```

   If no experiments exist, start with Exp01. Otherwise increment by 1 and zero-pad to 2 digits.

2. **Gather essential information**

   Ask user for:
   - Brief title/description (lowercase-with-hyphens format)
   - Objective (1-2 sentences describing what to accomplish)
   - Input data path
   - Expected output location

   Keep questioning minimal - only essentials.

3. **Load and populate template**

   - Read `assets/labnote.md`
   - Replace placeholders:
     - `[EXP_NUMBER]` → Next experiment number (01, 02, etc.)
     - `[TITLE]` → User's title
     - `[DATE]` → Current date (YYYY-MM-DD)
     - `[DESCRIPTION]` → Lowercase description for filename
     - `[OBJECTIVE]` → User's objective
     - `[INPUT_PATH]` → User's input path
     - `[OUTPUT_PATH]` → results/Exp##_description
   - Leave `[TOOL1]`, `[VERSION]` as placeholders for later

4. **Write file**

   Create: `notebook/labnote/Exp##_description.md`

5. **Report completion**

   ```
   ✓ Experiment labnote created

   File: notebook/labnote/Exp##_description.md
   Experiment: Exp##
   Title: [title]

   Next steps:
   - Run Experiment Clarification Workflow (recommended)
   - Start working on the experiment
   - Use Labnote Update Workflow to track progress
   ```

See `references/workflow-exp-plan.md` for detailed instructions.

## Experiment Clarification Workflow

### Purpose

Identify underspecified areas in experiment plans and resolve them through targeted Q&A (max 5 questions). Prevent wasted computational resources by ensuring clear input/output paths, data formats, success criteria, and resource requirements before execution.

### When to Use

- After creating experiment plan (before execution)
- When experiment plan lacks critical details
- To validate paths, formats, and expectations

### Key Priorities

Questions prioritized in this order:
1. **Path specification** (input/output) - CRITICAL
2. **Data format & scale** - prevents wrong tool choice
3. **Success criteria** - prevents uninterpretable results
4. **Tool/parameter rationale** - prevents poor analysis choices
5. **Biological context** - ensures meaningful interpretation

### Coverage Scan Categories

Assess each category as **Clear** / **Partial** / **Missing**:

- Experiment Objective & Scope
- Input Data (HIGH PRIORITY - absolute paths, format, scale)
- Output Specification (HIGH PRIORITY - paths, format, naming)
- Analysis Method (tool justification, key parameters)
- Success Criteria & Validation (quantitative metrics)
- Compute Resources (threads, memory, runtime)
- Edge Cases & Failure Handling
- Biological Context (hypothesis, interpretation)

### Execution Approach

1. Parse experiment number (Exp##)
2. Load `pyproject.toml` for compute defaults and labnote file
3. Perform coverage scan
4. Generate up to 5 prioritized questions
5. Present questions ONE at a time (multiple choice or short answer)
6. After EACH answer:
   - Validate format
   - Update labnote immediately
   - Add to `## Clarifications` section
   - Replace vague terms with specifics
7. Report coverage summary and readiness assessment

### Integration Rules

- Always prioritize path clarification first
- Replace vague statements:
  - "quality data" → "Q-score ≥20"
  - "sufficient coverage" → "≥30X mean coverage"
  - "some samples" → "12 tumor-normal pairs"
- Save file after each answer (atomic writes)
- Never exceed 5 questions
- Respect early termination signals ("done", "stop", "skip")

See `references/workflow-exp-clarify.md` for comprehensive instructions.

## Labnote Update Workflow

### Purpose

Update existing experiment labnotes with commands, results, observations, or issues during execution.

### When to Use

- After executing analysis steps
- Recording tool commands and parameters
- Documenting results and observations
- Noting issues or unexpected findings

### Execution Steps

1. **Parse experiment number** (Exp##)

2. **Find and read labnote**
   - Path: `notebook/labnote/Exp##_*.md`
   - If not found, suggest running Experiment Planning Workflow

3. **Determine update type**

   Ask user what to add:
   - New process step with command
   - Results/observations
   - Issues encountered
   - Tool versions

4. **For new process steps**

   Gather:
   - Step name/action
   - Rationale (why this step/approach)
   - Complete command with all parameters
   - Result (numbers, metrics, status)

   Append in timeline format:
   ```markdown
   ### Step N: [ACTION]

   [RATIONALE]

   ```bash
   [COMMAND]
   ```

   Result: [RESULT]
   ```

5. **For results or observations**

   Append bullet points with specific numbers and metrics

6. **Save and report**

   ```
   ✓ Labnote updated

   File: notebook/labnote/Exp##_description.md
   Added: [summary]
   ```

### Notes

- Keep additions simple and factual
- Record what was done and what happened
- Commands should be reproducible (include all parameters)
- Include specific numbers/metrics when available

See `references/workflow-exp-update-labnote.md` for details.

## Report Generation Workflow

### Purpose

Create comprehensive analysis reports from completed experiments. Reports are human-focused (40% of project content), emphasizing interpretation and biological meaning.

### When to Use

- Experiment(s) completed
- Ready to interpret and discuss findings
- Need formal documentation of results

### Execution Steps

1. **Parse experiment range**
   - Single: Exp## (e.g., Exp03)
   - Range: Exp##-Exp## (e.g., Exp01-Exp03)

2. **Read corresponding labnotes**

   Extract from `notebook/labnote/Exp##_*.md`:
   - Objectives
   - Methods used
   - Key findings
   - Tool versions and commands

3. **Ask for report details**

   Get user input:
   - Report title
   - Main findings to highlight
   - Biological interpretations (if ready)
   - Author name

4. **Load and populate template**

   - Read `assets/report.md`
   - Auto-fill from labnotes:
     - `[TITLE]`, `[EXP_RANGE]`, `[DATE]`, `[AUTHOR]`
     - `[OBJECTIVE]`, `[DATA_DESCRIPTION]`
     - `[STEP1]`, `[STEP2]` (pipeline steps)
     - `[LABNOTE_REFS]` (list of labnotes)
     - `[TOOL1]`, `[VERSION]` (software versions)
   - Leave interpretation placeholders for human input

5. **Write file**

   Create: `notebook/report/Exp##_report.md` or `Exp##-##_report.md`

6. **Report completion**

   ```
   ✓ Analysis report created

   File: notebook/report/Exp##_report.md
   Experiments covered: Exp##-Exp##

   Auto-filled sections:
   - Objective, Data, Pipeline, Software versions

   Sections to complete (HUMAN INPUT):
   - Results interpretation
   - Biological implications
   - Discussion of findings
   - Conclusions

   This is for HUMANS - write clearly with thoughtful interpretation.
   ```

### Report Philosophy

- Reports focus on "why" and biological meaning, not just "what"
- Include citations to labnotes, figures, and data files
- Interpretation and discussion are human-written
- This is the 40% human-readable content of the project

See `references/workflow-exp-report.md` for details.

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
