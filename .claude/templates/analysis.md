# Jupyter Notebook Structure for Exp[EXP_NUMBER]_[DESCRIPTION].ipynb

## Cell 1: Title & Metadata (Markdown)

**Action required**: Fill in [EXP_NUMBER], [TITLE], [DATE], [OBJECTIVE], [INPUT_PATH], and [DESCRIPTION].

```markdown
# Exp[EXP_NUMBER]: [TITLE]

Date: [DATE]
Objective: [Describe objective od this experiment in 5-10 lines.]

Config: config/[DATE]_Exp[EXP_NUMBER]_[DESCRIPTION].yaml
Input: [INPUT_PATH]
Output: results/Exp[EXP_NUMBER]_[DESCRIPTION]/
```

## Cell 2: Setup (Code)

**Action required**: Fill in [DATE], [EXP_NUMBER], [DESCRIPTION], [INPUT_PATH], [PARAM1], [TOOL1], and [VERSION].

```python
# Imports
import polars as pl
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
from pathlib import Path
import yaml

# Seaborn settings
sns.set_theme(style="whitegrid")

# Load configuration
with open('config/[DATE]_Exp[EXP_NUMBER]_[DESCRIPTION].yaml') as f:
    config = yaml.safe_load(f)

# Paths
DATA_DIR = Path("[INPUT_PATH]")
RESULTS_DIR = Path(config['paths']['output'])
RESULTS_DIR.mkdir(exist_ok=True, parents=True)

# Parameters
THREADS = config['parameters']['threads']
[PARAM1] = config['parameters']['[PARAM1]']

# Tool versions
print(f"polars: {pl.__version__}")
print(f"numpy: {np.__version__}")
print(f"seaborn: {sns.__version__}")
print(f"[TOOL1]: [VERSION]")
```

---

**Note**: The following cells (Cell 3 and beyond) are templates that vary depending on your analysis. Adjust the number and content of cells according to your project needs.

---

## Cell 3+: Load Data (Code)

**Action required**: Replace [LOAD_COMMAND], [CHECK_METRIC], and [DISPLAY_COMMAND] with your data loading code.

```python
# Load input data
data = [LOAD_COMMAND]

# Basic check
print(f"Loaded {[CHECK_METRIC]}")
[DISPLAY_COMMAND]
```

## Cell 4+: Analysis Step (Code)

**Action required**: Replace [STEP_DESCRIPTION], [ANALYSIS_COMMAND], [METRIC], and [KEY] with your analysis code. Add or remove analysis cells as needed.

```python
# [STEP_DESCRIPTION]
result = [ANALYSIS_COMMAND]

# Display results
print(f"[METRIC]: {result['[KEY]']}")
```

## Cell N-2: Visualization (Code)

**Action required**: Replace [PLOT_TYPE], [DATA], [X_COL], [Y_COL], [X_LABEL], [Y_LABEL], [PLOT_TITLE], and [FIGURE_NAME] with your visualization code. Add multiple visualization cells as needed.

**Note**: ALL figures must be saved as PNG files to RESULTS_DIR. These PNG files will be referenced in labnotes and reports.

```python
# Create figures
fig, ax = plt.subplots(figsize=(10, 6))
sns.[PLOT_TYPE](data=[DATA], x='[X_COL]', y='[Y_COL]', ax=ax)
ax.set_xlabel('[X_LABEL]')
ax.set_ylabel('[Y_LABEL]')
ax.set_title('[PLOT_TITLE]')

# Save figure (required - use descriptive filename)
plt.savefig(RESULTS_DIR / '[FIGURE_NAME].png', dpi=300, bbox_inches='tight')
plt.show()

print(f"Figure saved: {RESULTS_DIR / '[FIGURE_NAME].png'}")
```

## Cell N-1: Save Results (Code)

**Action required**: Replace [SAVE_COMMAND1] and [SAVE_COMMAND2] with your data export commands.

```python
# Save outputs
[SAVE_COMMAND1]
[SAVE_COMMAND2]
print(f"Results saved to {RESULTS_DIR}")
```

## Cell N: Summary (Markdown)

**Action required**: Fill in your findings, metrics, notes, and next steps.

```markdown
## Results Summary

- [FINDING1]
- [FINDING2]
- [FINDING3]

## Quality Metrics

- [METRIC1]: [VALUE1]
- [METRIC2]: [VALUE2]

## Issues & Notes

[NOTES]

## Next Steps

- [NEXT_STEP1]
- [NEXT_STEP2]
```
