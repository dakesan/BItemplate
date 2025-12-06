# Jupyter Notebook Template: Exp[NN]_{name}.ipynb

[TODO: Use this as a guide to create your Jupyter notebook. Delete this file after creating the .ipynb]

## Cell 1: Header (Markdown)

```markdown
# Exp[NN]: [TODO: Title]

Date: [TODO: YYYY-MM-DD]
Objective: [TODO: Brief objective in 1-2 sentences]

- Input: [TODO: input path]
- Output: results/Exp[NN]_{name}/
```

## Cell 2: Setup (Code)

```python
import polars as pl
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
from pathlib import Path

sns.set_theme(style="whitegrid")

RESULTS_DIR = Path("results/Exp[NN]_{name}")
RESULTS_DIR.mkdir(exist_ok=True, parents=True)

# Print versions
print(f"polars: {pl.__version__}")
print(f"numpy: {np.__version__}")
```

## Cell 3+: Load Data (Code)

[TODO: Add data loading. Modify as needed]

```python
data = pl.read_csv("{path/to/data}")
print(f"Loaded {len(data)} rows")
data.head()
```

## Cell N-1: Visualization (Code)

[TODO: Add visualizations. All figures must be saved to RESULTS_DIR]

```python
fig, ax = plt.subplots(figsize=(10, 6))
sns.histplot(data=data, x="{column}", ax=ax)
ax.set_title("{title}")

# Save figure (required)
plt.savefig(RESULTS_DIR / "{figure_name}.png", dpi=300, bbox_inches="tight")
plt.show()
```

## Cell N: Summary (Markdown)

```markdown
## Results

- {finding}
- {finding}

## Next Steps

- {next_step}
```
