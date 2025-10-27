---
name: bioinformatics-experiment
description: Manage bioinformatics experiment workflows - planning, clarification, execution tracking, and reporting
version: 1.0.0
author:
  name: BItemplate
  email: your-email@example.com
license: MIT
keywords:
  - bioinformatics
  - experiment
  - workflow
  - research
  - labnote
  - reproducibility
---

# Bioinformatics Experiment Plugin

This plugin provides comprehensive workflow management for bioinformatics experiments in an AI-first research environment.

## Features

- **Experiment Planning**: Create structured experiment labnotes with proper numbering
- **Interactive Clarification**: Resolve ambiguities through targeted Q&A (max 5 questions)
- **Progress Tracking**: Update labnotes with commands, results, and observations
- **Report Generation**: Create analysis reports from completed experiments

## Installation

Install this plugin from the marketplace:

```
/plugin install bioinformatics-experiment
```

Or add the marketplace first:

```
/plugin marketplace add owner/BItemplate
/plugin install bioinformatics-experiment
```

## Usage

Once installed, the skill will automatically activate when you:

- Create new experiment plans
- Clarify experiment details
- Update experiment progress
- Generate analysis reports

## Included Skills

- `bioinformatics-experiment`: Main workflow management skill with 4 sub-workflows

## Project Structure

This plugin assumes your project follows the bioinformatics template structure:

```
notebook/
├── labnote/          # Experiment logs (Exp##_*.md)
├── analysis/         # Jupyter notebooks
├── report/           # Final reports
└── knowledge/        # Background documentation

results/              # Analysis outputs (gitignored)
config/               # YAML configuration files
pyproject.toml        # Project settings
```

## Documentation

For detailed workflow instructions, see the skill's bundled references:

- Experiment Planning Workflow
- Experiment Clarification Workflow
- Labnote Update Workflow
- Report Generation Workflow

## License

MIT
