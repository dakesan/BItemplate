# Exp01: RNA-seq Quality Control

**Action required**: Fill in [EXP_NUMBER] (zero-padded, e.g., 01, 02), [TITLE], and [DATE] (YYYY-MM-DD format).

Date: 2025-11-01

## Configuration

**Action required**: Fill in config file reference if applicable. Format: config/YYYYMMDD_Exp[NN]_[description].yaml

Config: config/20251101_Exp01_rnaseq-qc.yaml (optional)

## Objective

**Action required**: Briefly describe what you want to achieve and why (2-3 sentences).

Assess the quality of RNA-seq raw reads to identify potential sequencing issues and determine if samples are suitable for downstream analysis. This initial quality control step is critical for ensuring reliable results in subsequent expression quantification and differential expression analysis.

## Tools & Versions

**Action required**: List all tools with exact versions. Add or remove lines as needed.

- [TOOL1]: [VERSION]
- [TOOL2]: [VERSION]

## Data

**Action required**: Specify exact input and output paths.

- Input: data/raw/rnaseq_samples/
- Output: results/Exp01_rnaseq-qc/

---

## Trial 1 - [SUBTITLE]

**Action required**: Replace [SUBTITLE] with a brief description of this trial (e.g., "Initial parameter exploration", "SAM-based pseudo-labeling").

### Plan

**Action required**: Briefly outline approach for this trial (3-5 bullet points).

- [STEP1]
- [STEP2]
- [STEP3]

### Methods

**Action required**: Document what you actually executed. Add or remove steps as needed. Do not write a whole python code here. All codes should be written in src or script directory. What should be noteed here is the running command to invoke those codes in src or sctript.

#### Step 1: [ACTION]

**Why**: [RATIONALE - why this approach was chosen or why it differs from plan]

```bash
[ACTUAL_COMMAND]
```

**Parameters**:
- [PARAM1]: [VALUE] - [EXPLANATION]
- [PARAM2]: [VALUE] - [EXPLANATION]

#### Step 2: [ACTION]

**Why**: [RATIONALE]

```bash
[ACTUAL_COMMAND]
```

**Parameters**:
- [PARAM1]: [VALUE] - [EXPLANATION]

### Results

**Action required**: List key findings from this trial (3-5 bullet points). Focus on numbers and observations.

- [FINDING1]
- [FINDING2]
- [FINDING3]

**Key Figures**:

![Figure 1: [DESCRIPTION]](results/Exp01_rnaseq-qc/trial1_[figure1.png])

### Discussion

#### Interpretation

[How do you interpret the results? What worked? What didn't?]

#### Problems & Limitations

[What issues were encountered? What could be improved?]

#### Next Steps

- [NEXT_STEP1]
- [NEXT_STEP2]

---

## Trial 2 - [SUBTITLE]

**Action required**: Copy the Trial template above for additional trials. Each trial should have its own Plan/Methods/Results/Discussion.

### Plan

- [STEP1]
- [STEP2]

### Methods

#### Step 1: [ACTION]

**Why**: [RATIONALE]

```bash
[ACTUAL_COMMAND]
```

**Parameters**:
- [PARAM1]: [VALUE]

### Results

- [FINDING1]
- [FINDING2]

### Discussion

#### Interpretation

[INTERPRETATION]

#### Problems & Limitations

[PROBLEMS]

#### Next Steps

- [NEXT_STEP1]

---

## Overall Summary

**Action required**: Fill in after completing all trials. Summarize key learnings across trials.

### Key Findings

- [OVERALL_FINDING1]
- [OVERALL_FINDING2]

### Conclusions

[What did you learn from this experiment? What approach works best?]

### Recommended Next Experiment

[What should Exp02 focus on?]

---

## Notes

**Action required**: Add any additional observations, unexpected findings, or technical details. This section is optional.

[NOTES]
