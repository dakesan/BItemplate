# Squidiff Evaluation Project - AI Agent Guidelines

AI-First Workflow for Evaluating Diffusion Models in Single-Cell Analysis

## Project Philosophy

This is an AI-assisted method evaluation project where:
- 60% of content is technical records (commands, parameters, metrics) - AI-optimized
- 40% is human interpretation (evaluation insights, biological implications, next steps)

### What to Write Thoroughly (Human-readable)
- Evaluation objectives and hypotheses
- Method comparisons and insights
- Interpretation of performance metrics
- Unexpected findings and their implications
- Next testing priorities

### What to Keep Simple (AI-readable)
- Tool versions and command-line parameters
- Training configurations and hyperparameters
- Performance metrics (loss, time, memory)
- File paths and dataset locations
- Structured experiment records

## Core Principles

1. **Method Evaluation Focus**: This is not biological discovery - focus on technical performance
2. **Reproducibility**: Record exact commands, parameters, random seeds
3. **Quantitative Assessment**: Always include metrics and targets
4. **Experiment Numbering**: All tests use Exp## prefix
5. **Incremental Testing**: Start simple (Exp01), then scale complexity

## Project Context

### Research Question
Can Squidiff's diffusion model framework accurately predict single-cell transcriptomic changes across different perturbation types (drug treatment, cell differentiation, gene perturbation)?

### Evaluation Criteria
1. **Training Performance**
   - Convergence speed (epochs to target loss)
   - Training time vs. dataset size
   - GPU/memory efficiency

2. **Prediction Accuracy**
   - Sample quality metrics (Pearson correlation, MSE)
   - Comparison with ground truth distributions
   - Generalization to held-out conditions

3. **Scalability**
   - Performance with varying gene dimensions (100 → 500 → 2000)
   - Batch size optimization
   - Multi-GPU capability

4. **Feature-Specific Tests**
   - Drug structure incorporation (use_drug_structure=True)
   - Cell type conditioning
   - Gene perturbation prediction

## Directory Structure

```
BItemplate/                          # This project (documentation)
├── README_squidiff.md              # Project overview
├── AGENTS_squidiff.md              # This file - AI guidelines
├── docs/
│   ├── notebook/                   # Jupyter notebooks for analysis
│   │   └── Exp01_squidiff-basic-test.ipynb
│   └── markdown/                   # Labnotes and reports
│       ├── 20251101_squidiff-testing.md
│       └── Exp01_squidiff-evaluation-report.md
├── data/
│   └── raw/                        # Raw data (gitignored)
└── results/                        # Analysis outputs (gitignored)
    └── 20251101_squidiff-testing/
        ├── Exp01/
        │   ├── training_loss.png
        │   ├── sample_quality.png
        │   └── resource_usage.png
        └── Exp02/

~/Desktop/Squidiff/                 # Squidiff source code
├── train_squidiff.py              # Training script
├── sample_squidiff.py             # Sampling script
├── datasets/                      # Test datasets
│   └── train.h5ad
├── scripts/                       # Utility scripts
└── Squidiff/                      # Source code
```

## Experiment Workflow

### 1. Plan (labnote)
Document in `docs/markdown/20251101_squidiff-testing.md`:

```markdown
## 実験X: ExpXX (PURPOSE)

>[!Works] EXPERIMENT_TYPE

>### 実験情報
>- **試験番号**: ExpXX
>- **実施日**: YYYY-MM-DD
>- **作業者**: Hiro
>- **目的**: Specific technical objective

>### 実験設計
>- Dataset: [path and description]
>- Parameters: [key settings]
>- Expected outcome: [hypothesis]
```

### 2. Execute and Record
Update labnote in real-time:

```markdown
>### Methods

>#### Step 1: [Action]
>**Why**: [Rationale]
>```bash
>[exact command]
>```
>**Parameters**:
>- param1: value - explanation
>- param2: value - explanation
```

### 3. Report Results
Add quantitative results:

```markdown
>[!Done] Results

>### Key Findings
>**定量的メトリクス**:
>| Metric | Value | Target | Status |
>|--------|-------|--------|--------|
>| Training Loss | X.XX | < Y.YY | ✓/✗ |
>| Training Time | XX min | < YY min | ✓/✗ |

>**Key Figures**:
>![Figure: Description](results/path/to/figure.png)
>*Caption with interpretation*
```

### 4. Document Next Steps

```markdown
>### Next Steps
>- [x] Completed task
>- [ ] Next priority
>- [ ] Future consideration
```

## Experiment Numbering

Current experiment series in `docs/markdown/20251101_squidiff-testing.md`:

- **Exp01**: Basic functionality test ✅
  - Training with gene_size=100
  - Sampling and quality assessment

- **Exp02**: Scaling test (planned)
  - gene_size=500
  - Memory and time benchmarking

- **Exp03**: Drug structure test (planned)
  - use_drug_structure=True
  - Requires drug metadata

- **Exp04**: Parameter optimization (planned)
  - Learning rate tuning
  - Batch size optimization

## Key Commands Reference

### Training
```bash
cd ~/Desktop/Squidiff
source .venv/bin/activate

python train_squidiff.py \
  --logger_path [log_dir] \
  --data_path datasets/[file].h5ad \
  --gene_size [dimension] \
  --output_dim [dimension] \
  --batch_size [size] \
  --learning_rate [rate] \
  --epochs [num]
```

### Sampling
```bash
python sample_squidiff.py \
  --model_path [trained_model] \
  --num_samples [count] \
  --use_drug_structure [True/False]
```

### Environment Management
```bash
# Activate environment
source ~/Desktop/Squidiff/.venv/bin/activate

# Check installed packages
pip list | grep -i "torch\|anndata\|scanpy"

# Install additional dependencies
pip install [package]
```

## Performance Targets (from Exp01)

Based on initial testing with gene_size=100:

| Metric | Target | Rationale |
|--------|--------|-----------|
| Final Training Loss | < 0.05 | Convergence indicator |
| Training Time | < 60 min | Practical training speed |
| GPU Memory Usage | < 16 GB | A100 GPU capacity |
| Sample Generation Speed | < 1.0 s/sample | Scalability for large predictions |
| Sample Quality (Pearson r) | > 0.80 | High correlation with ground truth |

**Hardware Baseline**:
- GPU: NVIDIA A100 (or equivalent)
- CPU: 16 cores
- System Memory: 16+ GB

## Git Workflow

- **Commit**: Labnotes, reports, configuration files
- **Gitignore**: Datasets (`~/Desktop/Squidiff/datasets/`), model weights, results
- **Branch**: Use feature branches for major experiments
- **Commit message**: Include Exp## number (e.g., "Exp02: Complete scaling test with gene_size=500")

## What AI Should Do

When assisting with this project:

1. **Read labnote first**: Understand experiment history
2. **Follow Exp## numbering**: Check highest completed Exp and continue sequence
3. **Record metrics**: Always include quantitative performance data
4. **Document parameters**: Record all command-line arguments and configurations
5. **Update README**: Keep project status current
6. **Compare with baselines**: Reference Exp01 performance targets
7. **Suggest next experiments**: Based on results and gaps

## What AI Should NOT Do

- Don't skip parameter documentation
- Don't run experiments without recording commands
- Don't interpret results without quantitative evidence
- Don't create new experiment files without Exp## prefix
- Don't commit large datasets or model weights
- Don't modify Squidiff source code without explicit request

## Specific Guidelines for Squidiff Testing

### Data Handling
- **Location**: All datasets in `~/Desktop/Squidiff/datasets/`
- **Format**: h5ad (AnnData) with required keys: `obs`, `var`, `X`
- **Preprocessing**: Check for missing keys before training
- **Validation**: Always split into train/test for evaluation

### Training Configuration
- **Start simple**: gene_size=100 for initial tests
- **Batch size**: Start with 32 (64+ may cause OOM)
- **Learning rate**: Monitor for instability in first 10 epochs
- **Checkpoints**: Save model weights at regular intervals
- **Logging**: Use `--logger_path` for TensorBoard-compatible logs

### Performance Monitoring
```bash
# Monitor GPU usage during training
watch -n 1 nvidia-smi

# Monitor memory and CPU
htop
```

### Result Validation
After each experiment:
1. Check training loss convergence
2. Generate sample predictions
3. Compare sample quality with ground truth
4. Document any technical issues

## Experiment Design Patterns

### Pattern 1: Scaling Test
```markdown
**Objective**: Test performance with gene_size=[NEW_SIZE]
**Hypothesis**: Linear scaling in time/memory
**Method**: Same config as Exp01, increase gene_size
**Success Criteria**:
- Training completes without OOM
- Time < [prediction] min
- Quality metrics maintained
```

### Pattern 2: Feature Test
```markdown
**Objective**: Evaluate [FEATURE] functionality
**Hypothesis**: [Expected improvement/capability]
**Method**: Enable feature flag, compare with baseline
**Success Criteria**:
- Feature works without errors
- Performance delta documented
```

### Pattern 3: Optimization Test
```markdown
**Objective**: Find optimal [PARAMETER]
**Hypothesis**: [Parameter] affects [metric]
**Method**: Grid/random search over range
**Success Criteria**:
- Optimal value identified
- Trade-offs documented
```

## Questions to Ask

Before starting new experiments, consider:

1. **Is this experiment necessary?**
   - Does it test a specific hypothesis?
   - Does it fill a gap in current evaluation?

2. **Are prerequisites met?**
   - Previous experiments completed?
   - Required data prepared?
   - Environment configured?

3. **Are success criteria defined?**
   - Quantitative targets set?
   - Comparison baseline identified?

4. **Is it reproducible?**
   - Random seeds set?
   - All parameters documented?
   - Commands recorded?

## Troubleshooting Common Issues

### Issue: OOM Error
- **Cause**: Batch size too large or gene_size too high
- **Solution**: Reduce batch_size (try 16 or 8), or reduce gene_size
- **Document**: Record OOM threshold in labnote

### Issue: Training Instability
- **Cause**: Learning rate too high
- **Solution**: Reduce learning rate by 10x, add warmup
- **Document**: Plot loss curve, identify instability range

### Issue: Missing h5ad Keys
- **Cause**: Incomplete preprocessing
- **Solution**: Check required keys with `anndata.read_h5ad()`, preprocess if needed
- **Document**: List preprocessing steps in Methods

### Issue: Slow Sampling
- **Cause**: Model not cached, inefficient implementation
- **Solution**: Warm-up with dummy samples, check model loading time
- **Document**: Separate model loading time from generation time

## Customization for Your Workflow

To adapt this for your Squidiff evaluation:

1. **Update experiment goals** in README_squidiff.md
2. **Add your hypotheses** to experiment plans
3. **Define your metrics** based on research question
4. **Customize performance targets** for your hardware

## References

- Squidiff bioRxiv: https://doi.org/10.1101/2024.11.16.623974
- Squidiff repository: `~/Desktop/Squidiff`
- Main labnote: `docs/markdown/20251101_squidiff-testing.md`
- Main report: `docs/markdown/Exp01_squidiff-evaluation-report.md`
- Analysis notebook: `docs/notebook/Exp01_squidiff-basic-test.ipynb`

---

*Last updated: 2025-11-01*
