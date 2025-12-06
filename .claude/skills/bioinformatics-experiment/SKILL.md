---
name: bioinformatics-experiment
description: This skill should be used when conducting bioinformatics research, planning experiments, running analyses, or managing scientific projects. Triggers include requests like "研究を始める", "実験する", "新しい実験を計画", "Start research", "Plan experiment", "Run analysis", or "What's the current research status?".
---

# Bioinformatics Research Management

Orchestrate hypothesis-driven bioinformatics research projects.

## First Action

1. Read `STEERING.md` to get current Phase
2. Read `notebook/tasks.md` for detailed task progress
3. Determine next action based on Phase (see Phase Judgment below)

## Phase Judgment

Check `**Phase**` in STEERING.md and determine next action:

| Phase | Condition | Next Action |
|-------|-----------|-------------|
| Project Setup | P01-P05 incomplete | Continue Project Setup flow |
| Experiment Planning | No active experiment | Add new experiment |
| Experiment Execution | E01-E06 complete, E07 pending | Execute experiment |
| Analysis | E07 complete, E08-E10 pending | Record results & interpret |
| Reporting | E10 complete, E11 pending | Create report |
| Completed | All tasks done | Ask user for next direction |

When Phase does not match actual task status, update STEERING.md Phase first.

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

## Task Sequences (Canonical)

Use these exact task IDs and names in `notebook/tasks.md`.

### Project Setup Tasks

| ID | Task | Output | Validation Criteria |
|----|------|--------|---------------------|
| P01 | Define project name | README.md | Name filled in |
| P02 | Define research question | README.md | Question stated |
| P03 | Document background & observations | README.md | Sources cited |
| P04 | List hypotheses to test | README.md | Testable hypotheses |
| P05 | Document data overview | README.md | Type, location, format |

### Experiment Tasks

Each experiment follows this exact task sequence.

| ID | Task | Labnote Section | Validation Criteria |
|----|------|-----------------|---------------------|
| E01 | Create labnote | - | File created from template |
| E02 | Define observation | Background > Observation | Source cited, facts only |
| E03 | Define hypothesis | Background > Hypothesis | Testable, rationale stated |
| E04 | Define verification strategy | Background > Verification | True/False outcomes defined |
| E05 | Document tools & data | Tools, Data | Versions, absolute paths |
| E06 | Document methods | Methods | Each step has rationale |
| E07 | Execute experiment | - | Commands run, outputs exist |
| E08 | Record results | Results | Facts only, no interpretation |
| E09 | Write interpretation | Interpretation | Alternatives & limitations included |
| E10 | Write conclusion | Conclusion | Status: Supported/Refuted/Inconclusive |
| E11 | Create report | - | Report file created |

### Task Format in tasks.md

```markdown
## Project Setup

- [ ] P01: Define project name → README.md
- [ ] P02: Define research question → README.md
- [ ] P03: Document background & observations → README.md
- [ ] P04: List hypotheses to test → README.md
- [ ] P05: Document data overview → README.md

## Exp##: [description]

- [ ] E01: Create labnote
- [ ] E02: Define observation
- [ ] E03: Define hypothesis
- [ ] E04: Define verification strategy
- [ ] E05: Document tools & data
- [ ] E06: Document methods
- [ ] E07: Execute experiment
- [ ] E08: Record results
- [ ] E09: Write interpretation
- [ ] E10: Write conclusion
- [ ] E11: Create report
```

## Workflow

### 1. Project Setup

When STEERING.md shows "Project Setup" phase:

**Step 1: Request free input**

Ask user:
```
研究について教えてください。
どのようなデータがあり、何を明らかにしたいですか？
```

**Step 2: Extract information**

From user's response, extract:

| Task | Required Information | Extraction Target |
|------|---------------------|-------------------|
| P01 | Project name | Explicit name or derive from topic |
| P02 | Research question | Main question or goal |
| P03 | Background & observations | What led to this research, sources |
| P04 | Hypotheses | Testable predictions |
| P05 | Data overview | Type, location, format |

**Step 3: Fill gaps**

If any information is missing or unclear, ask follow-up questions:
- P01 missing: "プロジェクト名は何にしますか？"
- P02 unclear: "具体的に何を明らかにしたいですか？"
- P03 missing: "この研究に至った背景・観察は何ですか？"
- P04 missing: "検証したい仮説はありますか？"
- P05 missing: "データの種類、場所、フォーマットを教えてください"

**Step 4: Update files**

Once all P01-P05 information gathered:
- `README.md` - Fill in project information section
- `STEERING.md` - Update Phase to "Experiment Planning", add TODOs
- `notebook/tasks.md` - Mark P01-P05 as complete

### 2. Add New Experiment

When adding a new experiment:

1. Add task block to `notebook/tasks.md` using canonical format above
2. Add experiment entry to `STEERING.md` Experiments table
3. Delegate E01 to subagent

### 3. Execute Task

For each task E01-E11:

1. Mark task as in-progress in `notebook/tasks.md`
2. Delegate to subagent using prompts below
3. Validate output against criteria in task table
4. Mark task as complete
5. Update `STEERING.md` if status changed

### Subagent Prompts

E01 (Create labnote):
```
Use Task tool with prompt:
"Create experiment labnote for Exp##: [description].
Template: notebook/labnote/Exp00_TEMPLATE_labnote.md
Output: notebook/labnote/Exp##_[description].md
Only create the file from template. Do not fill in content yet."
```

E02-E06 (Define sections):
```
Use Task tool with prompt:
"Update labnote notebook/labnote/Exp##_*.md
Task: [E0X task name]
Section: [target section from task table]
Validation: [criteria from task table]
Input from user: [relevant information]"
```

E07 (Execute experiment):
```
Use Task tool with prompt:
"Execute experiment Exp##.
Labnote: notebook/labnote/Exp##_*.md
Follow Methods section. Record commands and outputs.
Save results to: results/Exp##_[description]/"
```

E08-E10 (Record & conclude):
```
Use Task tool with prompt:
"Update labnote notebook/labnote/Exp##_*.md
Task: [E0X task name]
Section: [target section]
Validation: [criteria]
Remember: Results = facts only, Interpretation = reasoning with alternatives"
```

E11 (Create report):
```
Use Task tool with prompt:
"Create report from notebook/labnote/Exp##_*.md
Template: notebook/report/Exp00_TEMPLATE_report.md
Output: notebook/report/Exp##_[description].md
Focus: What We Know vs What We Think"
```

### 4. Knowledge Management

When creating reusable procedures:
1. Save to `knowledge/` with prefix (workflow_, protocol_, reference_)
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
