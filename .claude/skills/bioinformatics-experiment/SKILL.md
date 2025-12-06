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
| Experiment Planning | No active experiment | Add New Experiment flow |
| Experiment Execution | E01-E06 pending | Execute E01-E06 with subagents |
| Experiment Execution | E07 pending | Execute E07 (run experiment) |
| Analysis | E08-E10 pending | Execute E08-E10 with subagents |
| Reporting | E11 pending | Execute E11 (create report) |
| Completed | All tasks done | Ask user for next direction |

### Phase Transitions

| From | To | Trigger |
|------|----|---------|
| Project Setup | Experiment Planning | P01-P05 all complete |
| Experiment Planning | Experiment Execution | Experiment added, E01 started |
| Experiment Execution | Analysis | E07 complete |
| Analysis | Reporting | E10 complete |
| Reporting | Experiment Planning | E11 complete (ready for next experiment) |
| Reporting | Completed | User declares project complete |

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

When STEERING.md shows "Experiment Planning" phase (or user requests new experiment):

**Step 1: Request experiment idea**

Ask user:
```
次の実験について教えてください。
何を検証したいですか？どのような仮説がありますか？
```

**Step 2: Extract information**

From user's response, extract:

| Target | Required Information |
|--------|---------------------|
| Exp title | Short description for Exp## naming |
| Observation | What led to this experiment |
| Hypothesis | Testable prediction |
| Verification | How to distinguish true/false |

**Step 3: Fill gaps**

If any information is missing or unclear, ask follow-up questions:
- Title unclear: "この実験を一言で表すと？"
- Observation missing: "この仮説に至った観察・データは何ですか？"
- Hypothesis untestable: "この仮説が正しい/間違いの場合、それぞれどうなりますか？"
- Verification unclear: "どのような結果が出れば仮説を支持/棄却できますか？"

**Step 4: Create experiment**

Once information gathered:
1. Determine next Exp## number
2. Add task block to `notebook/tasks.md`
3. Add experiment entry to `STEERING.md` Experiments table (Status: Planning)
4. Update STEERING.md Phase to "Experiment Execution"
5. Delegate E01 to subagent, then continue E02-E06 with extracted information

### 3. Execute E01-E06 (Experiment Setup)

After Add New Experiment flow, execute E01-E06 sequentially:

**E01: Create labnote**
```
Delegate to subagent:
"Create experiment labnote for Exp##: [description].
Template: notebook/labnote/Exp00_TEMPLATE_labnote.md
Output: notebook/labnote/Exp##_[description].md
Only create the file from template. Do not fill in content yet."
```
→ Validate: File exists
→ Mark E01 complete

**E02-E04: Fill from extracted info**

Use information gathered in Add New Experiment Step 2:

| Task | Input Source | Subagent Prompt |
|------|--------------|-----------------|
| E02 | observation | "Update Background > Observation section with: [observation]" |
| E03 | hypothesis | "Update Background > Hypothesis section with: [hypothesis]" |
| E04 | verification | "Update Background > Verification section with: [verification]" |

For each E02-E04:
```
Delegate to subagent:
"Update labnote notebook/labnote/Exp##_[description].md
Task: [task name]
Section: [target section]
Content: [extracted info]
Validation: [criteria from task table]"
```
→ Validate against criteria
→ If validation fails: show issue to user, ask for correction, re-delegate
→ Mark complete

**E05: Document tools & data**

Ask user:
```
使用するツールとデータについて教えてください。
- ツール名とバージョン
- 入力データのパス
```

Delegate to subagent with user input
→ Validate: Versions and absolute paths present
→ Mark E05 complete

**E06: Document methods**

Ask user:
```
実験手順を教えてください。
各ステップで何をするか、なぜそうするかを含めてください。
```

Delegate to subagent with user input
→ Validate: Each step has rationale
→ Mark E06 complete

**After E06 complete**: Ready for E07. Confirm with user before execution.

### 4. Execute E07 (Run Experiment)

When E01-E06 complete and user confirms:

```
Delegate to subagent:
"Execute experiment Exp##.
Labnote: notebook/labnote/Exp##_[description].md
Follow Methods section exactly. Record all commands and outputs.
Save results to: results/Exp##_[description]/"
```
→ Validate: Commands run, output files exist
→ Mark E07 complete
→ Update Phase to "Analysis"

### 5. Execute E08-E10 (Analysis)

After E07 complete:

**E08: Record results**
```
Delegate to subagent:
"Update Results section in notebook/labnote/Exp##_[description].md
Based on outputs in results/Exp##_[description]/
Record facts only: numbers, observations, figure paths
Do NOT include interpretation"
```
→ Validate: Facts only, no interpretation words
→ Mark E08 complete

**E09: Write interpretation**

Ask user for their interpretation, or let subagent draft:
```
Delegate to subagent:
"Update Interpretation section in notebook/labnote/Exp##_[description].md
Based on Results section, write:
- What the results suggest
- Supporting evidence
- Alternative explanations
- Limitations"
```
→ Validate: Alternatives and limitations included
→ Show to user for review
→ Mark E09 complete

**E10: Write conclusion**
```
Delegate to subagent:
"Update Conclusion section in notebook/labnote/Exp##_[description].md
Determine hypothesis status: Supported / Refuted / Inconclusive
Summarize: What we now know, what remains unknown, next steps"
```
→ Validate: Status determined with evidence
→ Mark E10 complete
→ Update Phase to "Reporting"

### 6. Execute E11 (Create Report)

After E10 complete:

**Section mapping from labnote to report:**

| Report Section | Labnote Source | Validation Criteria |
|----------------|----------------|---------------------|
| Executive Summary | Conclusion | 3-5 sentences: question, finding, meaning |
| Background | Observation, Hypothesis | Research question & hypotheses listed |
| Methods Summary | Tools, Data, Methods | Pipeline overview with tool versions |
| Results | Results | Organized by finding, not by experiment |
| Synthesis | Interpretation, Conclusion | What We Know vs What We Think separated |
| Limitations | Interpretation > Limitations | Technical & interpretive limitations |
| Conclusions | Conclusion | Each conclusion references evidence |
| Future Directions | Conclusion > Next steps | Prioritized with rationale |

```
Delegate to subagent:
"Create report from notebook/labnote/Exp##_[description].md
Template: notebook/report/Exp00_TEMPLATE_report.md
Output: notebook/report/Exp##_[description].md

Requirements:
1. Fill all TODO placeholders from labnote content
2. Organize Results by finding (not experiment order)
3. Separate facts (What We Know) from interpretation (What We Think)
4. Include confidence levels for each interpretation
5. Reference specific evidence for each conclusion"
```

**Validation checklist:**
- [ ] All TODO placeholders filled
- [ ] Executive Summary is 3-5 sentences
- [ ] Results organized by finding
- [ ] What We Know contains only facts
- [ ] What We Think contains interpretations with reasoning
- [ ] Each conclusion references evidence
- [ ] Future Directions are prioritized

→ If validation fails: identify missing sections, re-delegate with specific instructions
→ Mark E11 complete
→ Update STEERING.md Experiments table (Status: Complete)
→ Update Phase to "Experiment Planning" (ready for next experiment)

### 7. Validation Failure Handling

When subagent output fails validation:

1. Identify specific validation criteria that failed
2. Show user the issue:
   ```
   E0X の検証に失敗しました。
   問題: [specific issue]
   修正が必要な内容: [what needs to change]
   ```
3. Ask user for correction or additional input
4. Re-delegate to subagent with corrected input
5. Re-validate

### 8. Knowledge Management

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
