# Bioinformatics Analysis Project

AI-First Workflow Template for Reproducible Bioinformatics Analysis

## Project Philosophy

This is an AI-assisted bioinformatics analysis template where:
- 60% of content is read/written by AI (commands, technical details, structured records)
- 40% is for humans (objectives, insights, interpretations, discussions)

### What to Write Thoroughly (Human-readable)
- Research objectives and goals
- Biological interpretations and insights
- Discussion of unexpected findings
- Next steps and hypotheses

### What to Keep Simple (AI-readable)
- Tool names and versions
- Commands executed
- Parameters used
- File paths and outputs
- Structured experimental records

## Core Principles

1. Simple, Structured Records: Record what you did, not how to do it
2. AI Context First: Optimize for AI to understand and continue work
3. Experiment-Based Organization: Everything uses Exp## numbering
4. Reproducibility by Default: Tool versions, commands, parameters always recorded

## Directory Structure

```
.
├── AGENTS.md                        # This file - AI context and project rules
├── README.md                        # Project-specific information (fill in template)
├── .docs/                           # Template usage guide (rarely modified)
├── notebook/
│   ├── labnote/                     # Experiment logs (Exp##_*.md)
│   │   └── Exp00_TEMPLATE_labnote.md
│   ├── analysis/                    # Jupyter notebooks (Exp##_*.ipynb)
│   │   └── Exp00_TEMPLATE_analysis.md
│   └── report/                      # Final reports (Exp##_*.md)
│       └── Exp00_TEMPLATE_report.md
├── scripts/                         # Wrapper scripts with hardcoded parameters
├── src/                             # Reusable code and utilities
├── config/                          # Configuration files (YAML)
├── data/
│   └── raw/                         # Immutable raw data (gitignored)
└── results/                         # All analysis outputs (gitignored)
    ├── Exp01_qc/
    ├── Exp02_alignment/
    └── Exp03_variants/
```

Note: No `tests/` directory - this is research. The process of making code work is part of the research output, documented in labnotes.

## Experiment Workflow

### 1. Plan (labnote)
Create `notebook/labnote/Exp##_description.md`:
- What you want to do (objective)
- Why you want to do it (rationale)
- What tools/versions you'll use

### 2. Execute (analysis + labnote)
- Run analysis in `notebook/analysis/Exp##_*.ipynb` or scripts
- Record commands, parameters, outputs in labnote
- Update labnote as you go (timeline format)

### 3. Report (report)
When done, create `notebook/report/Exp##_*.md`:
- Summarize findings
- Interpret results (biological meaning)
- Discuss implications

## Experiment Management with Slash Commands

Use slash commands to manage experiments:

- `/exp-plan` - Create new experiment labnote
- `/exp-update-labnote` - Update existing labnote with results
- `/exp-report` - Create analysis report from experiments

Templates are stored in `.claude/templates/`:
- `labnote.md` - Experiment log template
- `report.md` - Analysis report template
- `config.yaml` - Optional configuration file template (use if needed)

Commands automatically load templates and replace placeholders like [EXP_NUMBER], [DATE], [TITLE], etc.

## File Naming

All experiment files use Exp## prefix:
- `Exp01_quality-control.md`
- `Exp02_alignment.ipynb`
- `Exp03_variant-calling.md`
- `Exp00_TEMPLATE_*.md` (templates only)

Results directories:
- `results/Exp01_fastqc/`
- `results/Exp02_bwa-alignment/`

## Configuration Management

Optional: Use YAML files in `config/` for complex parameters.

Naming: `YYYYMMDD_Exp##_description.yaml`

Example:
```yaml
# config/20251008_Exp01_qc.yaml
experiment:
  id: "Exp01"
  date: "2025-10-08"

parameters:
  threads: 16

paths:
  input: "data/raw/sample.fastq.gz"
  output: "results/Exp01_qc"
```

Reference in labnote:
```markdown
Config: config/20251008_Exp01_qc.yaml
```

Template available at `.claude/templates/config.yaml`

## Environment Management

Use `uv` for Python package management:

```bash
# Edit pyproject.toml to add dependencies
# Then sync
uv sync

# Activate
source .venv/bin/activate
```

## Git Workflow

- Commit markdown files, notebooks, scripts, configs
- Gitignore data and results
- Stage after each substantial edit
- Only commit when user approves

## What AI Should Do

When assisting with this project:

1. Read labnotes to understand what's been done
2. Follow experiment numbering (check highest Exp## and continue)
3. Record commands and versions in labnotes
4. Keep labnotes simple - facts and commands, not prose
5. Write reports thoughtfully - interpret results, discuss implications
6. Reference templates (Exp00_TEMPLATE_*.md) for format
7. Update README.md with project progress

## What AI Should NOT Do

- Don't write verbose explanations in labnotes
- Don't skip recording tool versions
- Don't skip documenting parameters
- Don't create files without Exp## prefix (except configs/docs)
- Don't commit without user permission

## Customization

To use this template for your project:

1. Edit this file (AGENTS.md) with your:
   - Research objectives
   - Data locations
   - Platform specifics (PacBio/Illumina/ONT)

2. Fill in README.md with project details

3. Start with Exp01

## Questions?

- Template usage: See `.docs/getting-started.md`
- Directory details: See `.docs/directory-structure.md`
