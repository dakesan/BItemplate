---
date: 2025-11-01
tags: [labnote, bioinformatics, squidiff, diffusion-model, single-cell]
status: in-progress
author: Hiro
---

# 20251101_squidiff-testing

>[!Todo] Background
>
>## 実験目的
>
>Squidiffの拡散モデルベースの生成フレームワークをテストし、薬物処置、細胞分化、遺伝子摂動に対する単一細胞トランスクリプトミクス変化の予測性能を検証する。具体的には、モデルのトレーニング、サンプリング、予測精度の評価を通じて、実用性とパフォーマンスを確認する。
>
>## 実験の背景
>
>Squidiffは、多様な細胞タイプにおける環境変化に対する転写的変化を予測するために設計された拡散モデルである。主な機能として、薬物構造の組み込み（use_drug_structure）、細胞分化の予測、遺伝子摂動の予測を持つ。bioRxiv論文（https://doi.org/10.1101/2024.11.16.623974）で発表されており、単一細胞カウントマトリクスとメタデータを入力として受け取り、h5ad形式で処理する。
>
>## 参考文献・関連実験
>
>- bioRxiv: https://doi.org/10.1101/2024.11.16.623974
>- GitHub Repository: ~/Desktop/Squidiff
>- [[Diffusion Models for Single-Cell Analysis]]

---

## 実験1: Exp01 ([PURPOSE])

>[!Works] [EXPERIMENT_TYPE]
>
>### 実験情報
>- **試験番号**: Exp01
>- **実施日**: [EXPERIMENT_DATE]
>- **作業者**: Hiro
>- **目的**: [SPECIFIC_OBJECTIVE]
>
>### 実験設計
>- [DESIGN_DETAIL_1]
>- [DESIGN_DETAIL_2]
>- [DESIGN_DETAIL_3]
>
>### 使用サンプル
>
>| Sample ID | サンプル種類 | 条件 | 本数 | 備考 |
>|-----------|------------|------|------|------|
>| [SAMPLE_ID] | [SAMPLE_TYPE] | [CONDITION] | [COUNT] | [NOTES] |
>
>### Methods
>
>#### [Step Title]
>
>**Why**: [Rationale for this approach]
>
>```bash
>[COMMAND]
>```
>
>**Parameters**:
>- [PARAM1]: [VALUE] - [EXPLANATION]
>- [PARAM2]: [VALUE] - [EXPLANATION]

>[!Done] Results
>
>### Key Findings
>
>- [FINDING_1]
>- [FINDING_2]
>- [FINDING_3]
>
>**Key Figures**:
>
>![Figure 1: [DESCRIPTION]](results/20251101_squidiff-testing/exp01/[figure_name].png)

>[!Important]
>
>### Observations
>
>- [OBSERVATION_OR_ISSUE_1]
>- [OBSERVATION_OR_ISSUE_2]
>
>### Next Steps
>
>- [ ] [NEXT_STEP_1]
>- [ ] [NEXT_STEP_2]

---

## 実験2: Exp02 ([PURPOSE])

>[!Works] [EXPERIMENT_TYPE]
>
>### 実験情報
>- **試験番号**: Exp02
>- **実施日**: [EXPERIMENT_DATE]
>- **作業者**: Hiro
>- **目的**: [SPECIFIC_OBJECTIVE]
>
>### 実験設計
>- [DESIGN_DETAIL_1]
>- [DESIGN_DETAIL_2]

>[!Done] Results
>
>### Key Findings
>
>- [FINDING_1]
>- [FINDING_2]

---

## 総合結果サマリー (Overall Summary)

>[!Done] Integrated Results
>
>### [Analysis Section 1]
>
>- [INTEGRATED_FINDING_1]
>- [INTEGRATED_FINDING_2]
>
>### [Analysis Section 2]
>
>- [COMPARISON_OR_TREND]
>- [QUANTITATIVE_SUMMARY]

## 総合的考察 (Discussion)

### [Key Finding or Theme]

[Interpretation of results across all experiments. What worked? What didn't? Why?]

### 技術的課題と制約

[Technical limitations, unexpected issues, areas for improvement]

### 生物学的意義

[Biological interpretation and implications of findings]

## Conclusions

1. [MAIN_CONCLUSION_1]
2. [MAIN_CONCLUSION_2]
3. [MAIN_CONCLUSION_3]

## Recommended Next Experiment

[What should the next experiment focus on? What questions remain?]

---

## References

### 元データファイル

- `~/Desktop/Squidiff/datasets/`
- `[PATH_TO_RAW_DATA_2]`

### プロトコル・試薬情報

- [[Squidiff Training Protocol]]
- [[Squidiff Sampling Protocol]]

### ソフトウェア・ツール

| Tool | Version | Purpose |
|------|---------|---------|
| Squidiff | [VERSION] | Diffusion model for single-cell prediction |
| Python | [VERSION] | Runtime environment |
| PyTorch | [VERSION] | Deep learning framework |

---

## Notes

[Any additional observations, unexpected findings, or technical details]
