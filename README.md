# [Your Project Name]

[Brief description of your bioinformatics analysis project]

## Project Information

- Author: [Name]
- Institution: [Institution Name]
- Start Date: [YYYY-MM-DD]
- Status: [Planning/In Progress/Completed]

## Research Objective

[Describe the main research question or goal of this project]

Example:
> This project aims to identify structural variants in cancer genomes using PacBio HiFi sequencing data to understand genomic rearrangements associated with tumorigenesis.

## Data Overview

### Samples
- Sample Type: [e.g., Tumor/Normal pairs, RNA-seq samples]
- Number of Samples: [X samples]
- Sample IDs: [List or description]

### Data Specifications
- Data Type: [e.g., Sequencing reads, Microarray, Proteomics]
- Platform/Technology: [e.g., PacBio Revio, Illumina NovaSeq, Oxford Nanopore]
- Format: [e.g., FASTQ, BAM, CSV, HDF5]
- Scale: [e.g., 60X coverage, 50K cells, 1000 samples]
- Data Location: [Path to raw data]

### Expected Output
- [Output type 1, e.g., Variant call set (VCF)]
- [Output type 2, e.g., Differential expression results]
- [Output type 3, e.g., Analysis report]

## Quick Start

### For New Users

If this is your first time with this template, please read:
- [Getting Started Guide](.docs/getting-started.md)
- [Project Setup Guide](.docs/project-setup.md)

### Setup Environment

```bash
# Navigate to project directory
cd /path/to/this/project

# Sync environment and install dependencies
uv sync

# Activate environment
source .venv/bin/activate
```

### Run Analysis

```bash
# [Add your specific commands here]
# Example:
# jupyter lab  # Start Jupyter for notebooks
# python scripts/Exp01_quality-control.py
```

## Analysis Workflow

### Current Status

- [x] Project setup
- [ ] Experiment 01: [Brief description]
- [ ] Experiment 02: [Brief description]
- [ ] Final report and publication

### Completed Experiments

| Exp # | Description | Date | Status | Results |
|-------|-------------|------|--------|---------|
| Exp01 | [Description] | [Date] | ✅ Complete | [Link to report] |
| Exp02 | [Description] | [Date] | 🔄 In Progress | - |

### Planned Experiments

1. Exp03: [Description and goals]
2. Exp04: [Description and goals]

## Key Findings

[Update this section as you complete analyses]

### Summary
[High-level summary of main findings]

### Important Results
1. [Finding 1]
2. [Finding 2]
3. [Finding 3]

For detailed results, see:
- [Analysis Reports](notebook/report/)
- [Project Documentation](docs/)

## Software and Tools

### Main Analysis Tools
| Tool | Version | Purpose |
|------|---------|---------|
| [Tool 1] | [v1.0] | [Purpose] |
| [Tool 2] | [v2.0] | [Purpose] |

### Python Packages
See [pyproject.toml](pyproject.toml) for complete list.

Key packages:
- `numpy` - Numerical computing
- `pandas` - Data manipulation
- `biopython` - Bioinformatics utilities

### Reference Data
- Genome: [e.g., GRCh38]
- Annotation: [e.g., GENCODE v42]
- Database: [e.g., dbSNP, gnomAD]
- Location: [Path to references]

## Documentation

### Template Documentation (How to use this template)
- [Getting Started](.docs/getting-started.md) - Quick start guide
- [Project Setup](.docs/project-setup.md) - Setup and customization
- [Directory Structure](.docs/directory-structure.md) - Organization guide
- [Best Practices](.docs/best-practices.md) - Reproducibility guidelines
- [Customization Guide](.docs/customization.md) - How to adapt this template

### Project Documentation (This project's specific docs)
- [Requirements](docs/requirements.md) - Project requirements and objectives
- [Methods](docs/methods.md) - Detailed analysis methods
- [Results](docs/results/) - Analysis results and findings

### Analysis Notebooks
- [Lab Notes](notebook/labnote/) - Chronological experiment logs
- [Analysis](notebook/analysis/) - Jupyter notebooks
- [Reports](notebook/report/) - Comprehensive analysis reports
- [Knowledge Base](notebook/knowledge/) - Background information

## Project Timeline

| Phase | Description | Timeline | Status |
|-------|-------------|----------|--------|
| Setup | Environment and data preparation | [Dates] | ✅ |
| Phase 1 | [Description] | [Dates] | 🔄 |
| Phase 2 | [Description] | [Dates] | ⏳ |
| Phase 3 | [Description] | [Dates] | ⏳ |

## Team and Collaborators

### Analysis Team
- [Name] - [Role]
- [Name] - [Role]

### Collaborators
- [Name] - [Institution/Role]

## Funding and Acknowledgments

[Funding source, grant numbers, acknowledgments]

## Data Availability

[Information about where data will be deposited/shared]

## Publications

### Planned Publications
- [ ] [Manuscript 1 description]
- [ ] [Manuscript 2 description]

### Related Publications
- [Citation 1]
- [Citation 2]

## Contact

For questions about this project:
- Email: [email]
- Lab Website: [URL]

---

## Notes

### Important Dates
- [Date]: [Event/Milestone]
- [Date]: [Event/Milestone]

### Known Issues
- [Issue 1 and workaround]
- [Issue 2 and status]

### TODO
- [ ] [Task 1]
- [ ] [Task 2]

---

*Last updated: [YYYY-MM-DD]*
