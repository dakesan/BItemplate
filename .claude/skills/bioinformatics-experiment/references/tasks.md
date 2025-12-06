# Task Sequences (Canonical)

Use these exact task IDs and names in `notebook/tasks.md`.

## Project Setup Tasks

| ID | Task | Output | Validation Criteria |
|----|------|--------|---------------------|
| P01 | Define project name | README.md | Name filled in |
| P02 | Define research question | README.md | Question stated |
| P03 | Document background & observations | README.md | Sources cited |
| P04 | List hypotheses to test | README.md | Testable hypotheses |
| P05 | Document data overview | README.md | Type, location, format |

## Experiment Tasks

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

## Task Format in tasks.md

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

## File Naming

| Type | Pattern |
|------|---------|
| Labnote | `notebook/labnote/Exp##_description.md` |
| Report | `notebook/report/Exp##_description.md` |
| Results | `results/Exp##_description/` |
