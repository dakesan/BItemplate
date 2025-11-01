---
date: 2025-11-01
tags: [labreport, bioinformatics, squidiff, diffusion-model, validation]
status: draft
author: Hiro
version: "1.0"
reviewers: []
---

# Squidiff Validation - Lab Report

**Report Date**: 2025-11-01
**Author**: Hiro
**Status**: draft
**Version**: 1.0

---

## Executive Summary

This report documents the initial validation testing of Squidiff, a diffusion model-based framework for predicting single-cell transcriptomic changes. Experiment 01 (Exp01) successfully demonstrated basic functionality with sample datasets, confirming that the framework can train models and generate high-quality single-cell profiles.

**Key Findings**:
- Squidiff training completed successfully in 45 minutes with final loss of 0.0245 (target: < 0.05)
- Generated samples showed high correlation with original data (Pearson r=0.87, target: > 0.80)
- All performance metrics met or exceeded target values (training time, memory usage, generation speed)

**Main Conclusions**:
- Squidiff is functional and ready for more extensive testing with larger datasets
- Performance is suitable for practical use in single-cell analysis workflows
- Minor optimization opportunities identified in batch size and early-epoch stability

---

## Introduction

### Background

Squidiff is a diffusion model designed to predict transcriptomic changes across diverse cell types in response to environmental changes. Key capabilities include:
- Predicting single-cell transcriptomics upon drug treatments
- Predicting cell differentiation
- Predicting gene perturbation

The framework accepts h5ad files containing single-cell count matrices and metadata, with optional drug compound information.

**Source**: bioRxiv (https://doi.org/10.1101/2024.11.16.623974)

### Objectives

Validate Squidiff's basic functionality by:
1. Confirming successful model training with sample datasets
2. Verifying sampling/generation capabilities
3. Assessing computational performance and resource requirements
4. Identifying technical issues or limitations

### Scope

This validation focused on basic functionality testing using simulated data (gene_size=100). Drug structure incorporation and larger-scale testing are deferred to future experiments.

**Source Labnote**: [[20251101_squidiff-testing]] (Exp01)

---

## Methods

### Data Sources

**Dataset**: Simulated single-cell data from Squidiff repository

| Attribute | Value |
|-----------|-------|
| Data Type | Single-cell RNA-seq (simulated) |
| Sample Size | sc_simu_test.h5ad |
| Format | h5ad (AnnData format) |
| Location | ~/Desktop/Squidiff/datasets/ |

### Analysis Pipeline

The validation consisted of three main steps:

1. **Environment Setup**: Created Python virtual environment and installed Squidiff package in editable mode
2. **Model Training**: Executed train_squidiff.py with basic parameters (gene_size=100, output_dim=100)
3. **Sampling Test**: Ran sample_squidiff.py to generate 1000 single-cell profiles and evaluate quality

Detailed methods are documented in: [[20251101_squidiff-testing]] Exp01

### Software and Tools

| Tool | Version | Purpose |
|------|---------|---------|
| Squidiff | (repo version) | Diffusion model framework |
| Python | 3.x | Runtime environment |
| PyTorch | 2.0+ | Deep learning framework |

### Compute Resources

- **Cores**: 16 CPU cores
- **GPU**: NVIDIA A100
- **Memory**: Peak 12.3GB (GPU: 8.1GB, System: 4.2GB)
- **Runtime**: 45 minutes (training)

---

## Results

### Training Performance

Model training completed successfully with the following metrics:

**Key Metrics**:
| Metric | Value | Target | Status |
|--------|-------|--------|--------|
| Final Training Loss | 0.0245 | < 0.05 | ✓ Pass |
| Training Time | 45 min | < 60 min | ✓ Pass |
| GPU Memory Usage | 8.1 GB | < 16 GB | ✓ Pass |
| Sample Generation Speed | 0.15 s/sample | < 1.0 s/sample | ✓ Pass |
| Sample Quality (Pearson r) | 0.87 | > 0.80 | ✓ Pass |

**Observations**:
- Training loss converged steadily over 100 epochs
- GPU utilization remained stable at 95-98%
- No memory leaks observed during extended execution
- Initial 10 epochs showed loss oscillation, suggesting learning rate warmup may improve stability

### Sample Generation Quality

Generated 1000 single-cell profiles with high fidelity to original data:
- **Correlation**: Pearson r = 0.87 (strong positive correlation)
- **Generation Speed**: 0.15 seconds per sample (suitable for practical use)
- **Consistency**: Generated distributions closely matched original data patterns

---

## Discussion

### Summary of Key Findings

Squidiff demonstrated robust basic functionality across all tested dimensions. The framework successfully trained a diffusion model and generated high-quality single-cell profiles within acceptable time and resource constraints. All performance metrics met or exceeded predefined targets.

### Technical Significance

**Performance Considerations**:
- Batch size optimization is critical: batch_size=32 optimal for gene_size=100; batch_size=64 causes Out of Memory errors
- Model loading overhead (30 seconds on first sampling) should be considered for production workflows; subsequent samplings benefit from caching

**Reproducibility**: All commands and parameters are fully documented in the source labnote, enabling exact replication of results.

### Limitations and Considerations

**Technical Limitations**:
- Testing limited to small-scale data (gene_size=100); performance with larger gene sets (500+) not yet validated
- Some h5ad files in datasets/ require preprocessing (missing `obs` key)
- PyTorch 2.0+ deprecation warnings present but non-blocking

**Scope Constraints**:
- Drug structure incorporation (use_drug_structure=True) not tested
- Single experiment only; statistical validation across multiple runs pending

### Unexpected Observations

- **Early Training Instability**: Loss oscillation in first 10 epochs was more pronounced than expected. Literature suggests learning rate warmup should mitigate this.
- **Batch Size Sensitivity**: Out of Memory errors at batch_size=64 were unexpected given GPU capacity; suggests potential memory optimization opportunities in the codebase.

---

## Conclusions

1. **Squidiff is functional and suitable for initial research applications**. All basic operations (training, sampling) work as documented.
2. **Performance metrics meet practical requirements** for single-cell analysis workflows, with generation speed and quality both acceptable.
3. **Minor optimizations identified** (learning rate warmup, batch size tuning) can improve stability and efficiency.

### Implications

Squidiff can proceed to next-phase testing with:
- Larger datasets (gene_size=500+)
- Drug structure incorporation
- Multi-run statistical validation

### Recommendations

1. **Implement learning rate warmup** to address early-epoch training instability
2. **Profile memory usage** to understand batch_size=64 OOM errors and potentially increase batch capacity
3. **Preprocess all datasets** in datasets/ directory to ensure consistent `obs` key presence

---

## Next Steps

- [ ] Test with larger datasets (gene_size=500, output_dim=500)
- [ ] Implement and validate drug structure incorporation (use_drug_structure=True)
- [ ] Conduct parameter optimization study (learning rate, batch size)
- [ ] Perform statistical validation across multiple training runs
- [ ] Evaluate prediction accuracy on known cell differentiation scenarios

---

## References

### Source Labnotes

- [[20251101_squidiff-testing]] - Exp01: 基本動作確認

### Protocols and Methods

- [[Squidiff Training Protocol]] (train_squidiff.py)
- [[Squidiff Sampling Protocol]] (sample_squidiff.py)

### Literature

1. Squidiff bioRxiv preprint: https://doi.org/10.1101/2024.11.16.623974

---

## Appendix

### Data Files

**Raw Data**:
- `~/Desktop/Squidiff/datasets/sc_simu_test.h5ad`

**Processed Data**:
- Model checkpoint: `test_logger/model.pt`

**Analysis Results**:
- `results/20251101_squidiff-testing/exp01/`

### Figure List

| Figure | File | Description |
|--------|------|-------------|
| Figure 1 | training_loss.png | Training loss curve over 100 epochs |
| Figure 2 | sample_quality.png | Comparison of generated vs original data distributions |

---

## Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2025-11-01 | Hiro | Initial draft from Exp01 results |

---

## Approval

**Reviewed By**: [Pending Review]
**Review Date**: [Pending]
**Status**: Draft

**Comments**: This report documents initial validation only. Further testing required before production use.
