# BItemplate

Bioinformatics research template with AI-first hypothesis-driven workflow.

## How to Use This Template

### 1. Setup

```bash
# Clone or fork this repository
git clone https://github.com/dakesan/BItemplate.git your-project-name
cd your-project-name

# Install dependencies
uv sync
```

### 2. Start Research

Tell the AI:
- 「研究を始める」
- 「新しい実験を計画」
- "Start research"
- "Plan experiment"

The skill will:
1. Read `notebook/tasks.md` to understand current state
2. Guide hypothesis-driven experiment planning
3. Ensure scientific rigor (facts vs interpretation)

### 3. Workflow

```
Define research question
    ↓
Form testable hypothesis
    ↓
Plan & execute experiment (Exp##)
    ↓
Record results (facts only)
    ↓
Interpret (your reasoning)
    ↓
Conclude (hypothesis supported/refuted)
    ↓
Next experiment or report
```

### Key Files

| File | Purpose |
|------|---------|
| `notebook/tasks.md` | Research progress tracking |
| `notebook/labnote/Exp##_*.md` | Experiment logs |
| `notebook/report/Exp##_*.md` | Analysis reports |

### Scientific Rigor

The template enforces separation of:
- **Results**: Facts only (numbers, observations)
- **Interpretation**: Your reasoning (what it means)
- **Conclusion**: Hypothesis verdict with evidence

---

# [Your Project Name]

[Brief description of your bioinformatics analysis project]

## Project Information

- Author: [Name]
- Institution: [Institution Name]
- Start Date: [YYYY-MM-DD]
- Status: [Planning/In Progress/Completed]

## Research Objective

[Describe the main research question or goal of this project]

### Background & Observations

[What observations or prior knowledge led to this research?]

- Source: [paper/data/previous experiment]
- Key observation: [what you noticed that motivated this project]

### Hypotheses to Test

- [ ] H1: [hypothesis]
- [ ] H2: [hypothesis]

## Data Overview

### Samples
- Sample Type: [e.g., Tumor/Normal pairs, RNA-seq samples]
- Number of Samples: [X samples]

### Data Specifications
- Platform/Technology: [e.g., PacBio Revio, Illumina NovaSeq]
- Format: [e.g., FASTQ, BAM, CSV]
- Data Location: [Path to raw data]

## Quick Start

```bash
# Navigate to project directory
cd /path/to/this/project

# Sync environment
uv sync

# Start working with AI
# Say: "研究を始める" or "Start research"
```

## Analysis Progress

See `notebook/tasks.md` for current status.

### Completed Experiments

| Exp # | Description | Hypothesis | Outcome |
|-------|-------------|------------|---------|
| Exp01 | [Description] | [Hypothesis] | [Supported/Refuted] |

## Key Findings

### What We Know (Established Facts)
- [Finding with high confidence]

### What We Think (Interpretations)
- [Interpretation with reasoning]

## Software and Tools

| Tool | Version | Purpose |
|------|---------|---------|
| uv | latest | Package management |
| Python | 3.10+ | Analysis |

See `pyproject.toml` for complete dependencies.

## Documentation

- `notebook/labnote/` - Experiment logs
- `notebook/report/` - Analysis reports
- `notebook/analysis/` - Jupyter notebooks

## Contact

- Author: [Name]
- Email: [email]

---

*Last updated: [YYYY-MM-DD]*
