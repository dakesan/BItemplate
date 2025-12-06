# Validation Criteria

Quality checklists and validation rules for research documentation.

## Hypothesis Quality

- [ ] Testable (has expected outcomes for true/false)
- [ ] Based on explicit observation or prior knowledge
- [ ] Verification strategy distinguishes outcomes

## Documentation Quality

- [ ] Results contain only observations (no interpretation)
- [ ] Interpretations clearly labeled as reasoning
- [ ] Alternative explanations acknowledged
- [ ] Confidence levels explicit

## Project Integrity

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

## Report Validation Checklist

- [ ] All TODO placeholders filled
- [ ] Executive Summary is 3-5 sentences
- [ ] Results organized by finding
- [ ] What We Know contains only facts
- [ ] What We Think contains interpretations with reasoning
- [ ] Each conclusion references evidence
- [ ] Future Directions are prioritized

## Validation Failure Handling

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
