# Subagent Prompts

Detailed prompts for delegating tasks to subagents via Task tool.

## E01: Create Labnote

```
Delegate to subagent:
"Create experiment labnote for Exp##: [description].
Template: notebook/labnote/Exp00_TEMPLATE_labnote.md
Output: notebook/labnote/Exp##_[description].md
Only create the file from template. Do not fill in content yet."
```

## E02-E04: Fill Background Sections

Use information gathered in Add New Experiment:

| Task | Input Source | Target Section |
|------|--------------|----------------|
| E02 | observation | Background > Observation |
| E03 | hypothesis | Background > Hypothesis |
| E04 | verification | Background > Verification |

```
Delegate to subagent:
"Update labnote notebook/labnote/Exp##_[description].md
Task: [task name]
Section: [target section]
Content: [extracted info]
Validation: [criteria from task table]"
```

## E05: Document Tools & Data

Ask user first:
```
使用するツールとデータについて教えてください。
- ツール名とバージョン
- 入力データのパス
```

Then delegate with user input.

## E06: Document Methods

Ask user first:
```
実験手順を教えてください。
各ステップで何をするか、なぜそうするかを含めてください。
```

Then delegate with user input.

## E07: Execute Experiment

```
Delegate to subagent:
"Execute experiment Exp##.
Labnote: notebook/labnote/Exp##_[description].md
Follow Methods section exactly. Record all commands and outputs.
Save results to: results/Exp##_[description]/"
```

## E08: Record Results

```
Delegate to subagent:
"Update Results section in notebook/labnote/Exp##_[description].md
Based on outputs in results/Exp##_[description]/
Record facts only: numbers, observations, figure paths
Do NOT include interpretation"
```

## E09: Write Interpretation

```
Delegate to subagent:
"Update Interpretation section in notebook/labnote/Exp##_[description].md
Based on Results section, write:
- What the results suggest
- Supporting evidence
- Alternative explanations
- Limitations"
```

## E10: Write Conclusion

```
Delegate to subagent:
"Update Conclusion section in notebook/labnote/Exp##_[description].md
Determine hypothesis status: Supported / Refuted / Inconclusive
Summarize: What we now know, what remains unknown, next steps"
```

## E11: Create Report

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
