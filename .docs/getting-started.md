# Getting Started

Minimal guide to start using this bioinformatics analysis template.

## Quick Setup

### 1. Install uv

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
source ~/.bashrc  # or ~/.zshrc
```

### 2. Clone Template

```bash
git clone <template-url> my-analysis-project
cd my-analysis-project
```

### 3. Setup Environment

```bash
# Edit pyproject.toml to add your dependencies
# Then sync
uv sync

# Activate
source .venv/bin/activate
```

### 4. Customize Project

Edit these files with your project details:

1. [AGENTS.md](../AGENTS.md) - Add data paths, research objectives
2. [README.md](../README.md) - Fill in project information template
3. `config/` - Add your configuration files

### 5. Start First Experiment

```bash
# Create your first labnote
cp notebook/labnote/Exp00_TEMPLATE_labnote.md notebook/labnote/Exp01_my-first-analysis.md

# Edit it with your experiment details
# Then start working!
```

## File Structure Quick Reference

```
├── AGENTS.md                    # Project charter - read this first
├── README.md                    # Project info (fill template)
├── notebook/
│   ├── labnote/                 # Experiment logs (Exp##_*.md)
│   ├── analysis/                # Jupyter notebooks (Exp##_*.ipynb)
│   └── report/                  # Final reports (Exp##_*.md)
├── scripts/                     # Wrapper scripts
├── config/                      # Configuration files
├── data/
│   └── raw/                     # Immutable raw data (gitignored)

└── results/                     # All analysis outputs (gitignored)
    ├── Exp01_qc/
    ├── Exp02_alignment/
    └── Exp03_variants/
```

## Workflow

1. Plan: Create labnote with objective and approach
2. Execute: Run analysis, record commands and results
3. Report: Summarize findings when done

See templates in `notebook/*/Exp00_TEMPLATE_*.md`

## Key Principles

- Use Exp## numbering for all experiments
- Record tool versions and commands
- Keep labnotes simple (facts, not prose)
- Write reports thoroughly (interpretation, discussion)
- Update README.md as project progresses

## Common Commands

```bash
# Add new dependency
# Edit pyproject.toml, then:
uv sync

# Start Jupyter
jupyter lab

# Check experiment history
ls -lt notebook/labnote/
```

## Need More Details?

- Project rules: [AGENTS.md](../AGENTS.md)
- Directory details: [directory-structure.md](directory-structure.md)
- Template structure: [TEMPLATE.md](TEMPLATE.md)
