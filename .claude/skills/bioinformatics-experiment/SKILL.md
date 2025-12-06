---
name: bioinformatics-experiment
description: This skill should be used when conducting bioinformatics research, planning experiments, running analyses, or managing scientific projects. Triggers include requests like "研究を始める", "実験する", "新しい実験を計画", "Start research", "Plan experiment", "Run analysis", or "What's the current research status?".
---

# Bioinformatics Research Management

Orchestrate hypothesis-driven bioinformatics research projects.

## First Action

1. Read `STEERING.md` to understand current project status and priorities
2. Read `notebook/tasks.md` for detailed experiment progress

## Role

Act as **research strategist**:
- Define project objectives and research questions
- Organize hypotheses into testable experiments
- Track progress across experiments
- Ensure scientific rigor (facts vs interpretation)

Delegate individual experiment tasks to **subagents** via Task tool.

## Document Hierarchy

| Document | Role | Update Frequency |
|----------|------|------------------|
| README.md | Project overview (static) | Rarely |
| STEERING.md | Current status, TODO, links (dynamic) | Frequently |
| knowledge/ | Reusable procedures (reference) | As needed |
| notebook/tasks.md | Experiment-level progress | Per experiment |

## Project Structure

```
├── README.md             # Project overview
├── STEERING.md           # Current status & navigation
├── knowledge/            # Reusable procedures
│   ├── workflow_*.md
│   └── protocol_*.md
├── notebook/
│   ├── tasks.md          # Experiment progress
│   ├── labnote/Exp##_*.md
│   ├── report/Exp##_*.md
│   └── analysis/Exp##_*.ipynb
├── results/Exp##_*/      # Output data (gitignored)
└── data/raw/             # Input data (gitignored)
```

## Workflow

### 1. Project Setup

To initialize a new project (when STEERING.md shows "Project Setup" phase):

Gather from user:
- Project name
- Research question
- Observations that led to this
- Hypotheses to test
- Data overview (type, location, format)

Update files:
- `README.md` - Fill in project information section
- `STEERING.md` - Update status, add initial TODOs
- `notebook/tasks.md` - Create initial task list

### 2. Experiment Planning

To plan a new experiment:
- Ensure hypothesis is testable (clear true/false outcomes)
- Define verification strategy
- Identify required data and tools

Delegate to subagent:

```
Use Task tool with prompt:
"Create experiment labnote for Exp##.
Hypothesis: [hypothesis]
Verification: [strategy]
Data: [input path]
Template: notebook/labnote/Exp00_TEMPLATE_labnote.md
Output: notebook/labnote/Exp##_description.md"
```

### 3. Experiment Execution

To record progress, delegate to subagent:

```
Use Task tool with prompt:
"Update labnote notebook/labnote/Exp##_*.md
Add: [method step / result / interpretation]
Remember: Results = facts only, Interpretation = reasoning"
```

### 4. Report Generation

To create report from completed experiment, delegate to subagent:

```
Use Task tool with prompt:
"Create report from notebook/labnote/Exp##_*.md
Template: notebook/report/Exp00_TEMPLATE_report.md
Output: notebook/report/Exp##_description.md
Focus: What We Know vs What We Think"
```

### 5. Progress Update

After each subagent task:
1. Update `notebook/tasks.md` with experiment-level progress
2. Update `STEERING.md` if project status or priorities changed

### 6. Knowledge Management

When creating reusable procedures:
1. Save to `knowledge/` with appropriate prefix (workflow_, protocol_, reference_)
2. Add link to STEERING.md Quick Links section

## Quality Checklist

Validate continuously:

### Hypothesis Quality
- [ ] Testable (has expected outcomes for true/false)
- [ ] Based on explicit observation or prior knowledge
- [ ] Verification strategy distinguishes outcomes

### Documentation Quality
- [ ] Results contain only observations (no interpretation)
- [ ] Interpretations clearly labeled as reasoning
- [ ] Alternative explanations acknowledged
- [ ] Confidence levels explicit

### Project Integrity
- [ ] Exp## numbers are sequential
- [ ] All paths are absolute
- [ ] Tool versions recorded
- [ ] tasks.md reflects current state
- [ ] STEERING.md reflects current status and priorities

## Scientific Rigor Reminders

| Section | Should Contain | Should NOT Contain |
|---------|---------------|-------------------|
| Results | Numbers, observations, outputs | "suggests", "indicates", "means" |
| Interpretation | Reasoning, explanations | Raw data, commands |
| Conclusion | Hypothesis verdict with evidence | New observations |

## File Naming

| Type | Pattern |
|------|---------|
| Labnote | `notebook/labnote/Exp##_description.md` |
| Report | `notebook/report/Exp##_description.md` |
| Results | `results/Exp##_description/` |
