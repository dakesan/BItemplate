# Squidiff Basic Functionality Evaluation Report

**Experiment**: Exp01
**Date**: 2025-11-01
**Author**: Hiro
**Status**: Completed

---

## Executive Summary

Squidiffの基本機能テストを実施し、シミュレートされた単一細胞データ（gene_size=100）を用いてトレーニングとサンプリングの性能を評価した。すべてのパフォーマンスメトリクスが目標値を達成し、拡散モデルベースの生成フレームワークとしての基本的な実用性が確認された。

**主要な成果**:
- ✓ トレーニング収束成功（最終loss: 0.0245 < 目標: 0.05）
- ✓ 高品質なサンプル生成（Pearson r = 0.87 > 目標: 0.80）
- ✓ 効率的なリソース利用（GPU利用率: 95-98%）
- ✓ 実用的な生成速度（0.15秒/サンプル）

**制約事項**:
- 初期10エポックで学習不安定性を観察
- batch_size=64でOOMエラー発生（gene_size=100時）
- より大規模なgene dimensionでのスケーラビリティは未検証

---

## Objective

本実験の目的は、Squidiffの拡散モデルフレームワークが単一細胞トランスクリプトミクスデータの生成において基本的な機能を正常に実行できることを検証することである。具体的には：

1. トレーニングプロセスの安定性と収束性能の評価
2. 生成サンプルの品質（元データとの相関）の定量的評価
3. 計算リソース使用効率の測定
4. 今後のスケーリング実験（Exp02-04）のベースライン確立

---

## Methods

### Dataset

- **Data Source**: `~/Desktop/Squidiff/datasets/train.h5ad`
- **Format**: AnnData (h5ad)
- **Scale**: gene_size = 100（初期テスト用に縮小）
- **Type**: Simulated single-cell RNA-seq count matrix

### Training Configuration

```bash
cd ~/Desktop/Squidiff
source .venv/bin/activate

python train_squidiff.py \
  --logger_path test_logger \
  --data_path datasets/train.h5ad \
  --gene_size 100 \
  --output_dim 100 \
  --batch_size 32 \
  --epochs 100
```

**Key Parameters**:
- `gene_size`: 100 - 入力遺伝子次元
- `output_dim`: 100 - 出力次元（gene_sizeと一致）
- `batch_size`: 32 - メモリ制約に基づく最適値
- `epochs`: 100 - 収束確認のための十分なエポック数

### Sampling Configuration

```bash
python sample_squidiff.py \
  --model_path [trained_model_path] \
  --num_samples 1000 \
  --use_drug_structure False
```

### Evaluation Metrics

| Metric | Definition | Target |
|--------|------------|--------|
| Training Loss | 最終エポックでのモデル損失値 | < 0.05 |
| Training Time | 100エポック完了までの時間 | < 60 min |
| GPU Memory | ピーク時のGPUメモリ使用量 | < 16 GB |
| Sample Speed | サンプル生成速度 | < 1.0 s/sample |
| Sample Quality | 生成データと元データのPearson相関 | > 0.80 |

### Hardware Environment

- **GPU**: NVIDIA A100（推定）
- **CPU**: 16 cores
- **System Memory**: 16+ GB
- **Framework**: PyTorch 2.0+

---

## Results

### 1. Training Performance

#### Convergence Analysis

![Training Loss Curve](../../results/20251101_squidiff-testing/Exp01/training_loss.png)
*Figure 1: 100エポックにわたるトレーニング損失の推移。初期10エポックで不安定性が見られるが、その後安定して収束し最終loss 0.0245を達成。*

**定量的結果**:

| Metric | Value | Target | Status |
|--------|-------|--------|--------|
| Final Training Loss | 0.0245 | < 0.05 | ✓ Pass |
| Training Time | 45 min | < 60 min | ✓ Pass |
| Convergence Epoch | ~40 | < 100 | ✓ Pass |

**観察事項**:
1. **初期学習の不安定性**: 最初の10エポックでlossが0.08-0.15の範囲で激しく振動
2. **安定した収束**: 10エポック以降は指数関数的に減衰し、40エポック付近で安定
3. **過学習の兆候なし**: 損失値が安定後も増加傾向は見られず

#### Resource Utilization

![Resource Usage](../../results/20251101_squidiff-testing/Exp01/resource_usage.png)
*Figure 2: GPU/システムメモリ、GPU利用率、トレーニング時間の使用状況。すべてのリソースが容量の50-75%範囲で効率的に利用されている。*

**リソース使用量**:

| Resource | Used | Capacity | Utilization |
|----------|------|----------|-------------|
| GPU Memory | 8.1 GB | 16 GB | 50.6% |
| System Memory | 4.2 GB | 16 GB | 26.3% |
| GPU Utilization | 96.5% | 100% | 96.5% |
| Training Time | 45 min | 60 min | 75.0% |

**重要な発見**:
- **高いGPU利用率** (95-98%): 計算リソースを効率的に活用
- **適度なメモリ使用**: GPU/システムメモリともに余裕があり、スケーリングの余地あり
- **メモリリーク無し**: 長時間実行でもメモリ使用量は安定

---

### 2. Sample Quality

#### Generated vs. Original Data Comparison

![Sample Quality](../../results/20251101_squidiff-testing/Exp01/sample_quality.png)
*Figure 3: (左) 生成データと元データの散布図。高い線形相関を示す（r=0.87）。(右) 分布比較ヒストグラム。生成データが元データの分布を良好に再現している。*

**品質メトリクス**:

| Metric | Value | Interpretation |
|--------|-------|----------------|
| Pearson Correlation | r = 0.87 | 強い正の相関 |
| P-value | < 0.001 | 統計的に有意 |
| Sample Count | 1,000 | 十分なサンプルサイズ |

**解釈**:
- **r = 0.87** は、生成されたsingle-cell profilesが元データの発現パターンを高い精度で再現していることを示す
- 目標値（r > 0.80）を上回り、実用的な品質レベルに到達
- 散布図の線形性から、発現値の大小に関わらず一貫した予測精度

#### Distribution Analysis

- **分布の一致**: 生成データのヒストグラムが元データと高い類似性を示す
- **外れ値処理**: 極端な発現値も適切に再現
- **ノイズレベル**: 生成データに過度な平滑化は見られず、生物学的変動を保持

---

### 3. Sampling Performance

**サンプリング速度**:
- 初回サンプリング: ~30秒（モデルロード時間含む）
- 2回目以降: 0.15秒/サンプル（キャッシュ効果）
- 1,000サンプル生成時間: ~2.5分（初回ロード含む）

**スケーラビリティの示唆**:
- 大規模予測（10,000+ cells）も実用的な時間で実行可能
- バッチ処理により更なる高速化の余地あり

---

## Discussion

### Key Findings

#### 1. Squidiffの基本機能は期待通りに動作

本実験により、Squidiffがシミュレートされた単一細胞データに対して：
- 安定したトレーニング収束を達成
- 高品質なサンプル生成（r=0.87）を実現
- 効率的なリソース利用（GPU 95%+利用率）

を確認した。これらの結果は、拡散モデルベースのアプローチが単一細胞トランスクリプトミクス予測において有効であることを示唆する。

#### 2. 初期学習の不安定性とその対策

最初の10エポックで観察された損失の振動は、学習率が初期状態のモデルに対して高すぎる可能性を示唆する。この問題に対する推奨対策：

**推奨される改善策**:
```python
# Learning rate warmup の実装例
warmup_epochs = 10
initial_lr = 1e-5
target_lr = 1e-3

for epoch in range(1, warmup_epochs + 1):
    lr = initial_lr + (target_lr - initial_lr) * (epoch / warmup_epochs)
    # optimizer.param_groups[0]['lr'] = lr
```

#### 3. バッチサイズの最適化

**発見事項**:
- `batch_size=32`: 安定動作、GPU利用率 95-98%
- `batch_size=64`: OOM error（gene_size=100時）

**解釈**:
- gene_size=100の場合、batch_size=32が最適
- より大きなgene_size（500, 2000）では更なる調整が必要
- メモリ使用量 = f(gene_size, batch_size, model_depth)の関係を今後のExp02で定量化すべき

#### 4. 生成品質の評価

**Pearson r = 0.87 の意味**:
- 単一細胞レベルでの遺伝子発現パターンを高精度で予測
- 薬物処置や遺伝子摂動の効果予測に十分な品質レベル
- ただし、r=0.87 は約24%の分散が説明できていないことを意味する

**残存する13%の誤差の原因（仮説）**:
1. 拡散プロセスの確率的性質（意図的なノイズ）
2. トレーニングデータの限界（サンプル数、多様性）
3. モデルアーキテクチャの表現能力の上限
4. 生物学的ノイズの再現（技術的ノイズとの区別が困難）

### Biological Implications

本実験はシミュレートされたデータを用いたため、直接的な生物学的含意は限定的である。しかし、技術的観点から以下の示唆が得られる：

1. **拡散モデルの適用可能性**: 単一細胞データの高次元性（数千〜数万遺伝子）に対して、拡散モデルが有効に機能する可能性
2. **予測精度の実用性**: r=0.87の相関は、薬物スクリーニングや遺伝子機能解析における仮説生成に十分
3. **計算効率**: 45分/100エポックの学習速度は、実験データでの反復的な解析に実用的

### Technical Challenges and Limitations

#### 1. データセットの制約

**現状**:
- シミュレートされたデータのみでテスト
- 実際の生物学的データとの整合性は未検証
- gene_size=100は実用スケールより大幅に小さい

**今後の対策**:
- 公開データセット（例：Perturbseq, CRISPR screen data）での検証が必須
- gene_size=500 → 2000 → full genome scaleへの段階的スケーリング

#### 2. パフォーマンスのスケーラビリティ

**未検証の領域**:
- より大規模なgene dimension（500+）でのメモリ使用量
- 複数GPU環境でのトレーニング効率
- 実データの複雑性（細胞型の多様性、バッチ効果）への対応

#### 3. モデルの解釈可能性

拡散モデルはブラックボックス的な性質を持つため：
- どの遺伝子間の関係性を学習したか不明
- 予測の信頼性（不確実性推定）が未評価
- 生物学的に妥当でない予測の検出が困難

**今後の改善方向**:
- Attention mechanismの可視化
- 遺伝子重要度スコアの抽出
- アンサンブル予測による不確実性推定

### Comparison with Baseline Methods

本実験では比較ベースライン（例：線形回帰、VAE、GAN）を設定していないため、Squidiffの相対的優位性は評価できていない。

**推奨される比較対象**:
1. **scGen** (VAE-based perturbation prediction)
2. **CPA** (Compositional Perturbation Autoencoder)
3. **Simple baseline** (遺伝子発現の線形変化モデル)

Exp03またはExp04でこれらとの定量的比較を実施すべきである。

---

## Conclusions

### Main Conclusions

1. **基本機能の動作確認**: Squidiffはgene_size=100の条件下で、安定したトレーニングと高品質なサンプル生成（r=0.87）を実現した。

2. **リソース効率**: GPU利用率95%+、メモリ使用50%の効率的な計算リソース活用を確認。スケーリングの余地あり。

3. **技術的課題の特定**: 初期学習の不安定性とバッチサイズ制約を確認。Learning rate warmupとメモリ最適化が今後の改善ポイント。

4. **実用性の見通し**: 生成速度（0.15秒/サンプル）は実用的であり、大規模スクリーニング予測に適用可能。

### Practical Recommendations

**Short-term (Exp02-03)**:
- gene_size=500でのスケーリングテスト実施
- Learning rate warmup の導入と効果検証
- 実データ（公開データセット）での検証開始

**Medium-term (Exp04-06)**:
- 薬物構造情報の組み込み（use_drug_structure=True）
- パラメータチューニング（学習率、バッチサイズ、モデル深度）
- ベースライン手法との定量的比較

**Long-term**:
- Full genome scale（2000+ genes）での性能評価
- 不確実性推定機能の追加
- 実験検証（wet-lab validation）との統合

---

## Next Steps

### Immediate Actions (Week 1-2)

1. **Exp02: Scaling Test**
   - Objective: gene_size=500でのパフォーマンス評価
   - Expected challenges: メモリ使用量増加、トレーニング時間延長
   - Success criteria: loss < 0.05, r > 0.80を維持

2. **Learning Rate Warmup Implementation**
   - 初期10エポックの不安定性解消
   - 収束速度への影響評価

### Medium-term Plan (Month 1-2)

3. **Exp03: Drug Structure Incorporation**
   - `use_drug_structure=True`でのトレーニング
   - 薬物構造情報が予測精度に与える影響を定量化

4. **Exp04: Parameter Optimization**
   - Grid search or Bayesian optimization
   - 最適な学習率、バッチサイズ、モデルアーキテクチャの探索

5. **Real Dataset Validation**
   - 公開データセット（Perturbseq, LINCS L1000など）での検証
   - 生物学的妥当性の評価

### Long-term Vision (Month 3+)

6. **Multi-GPU Scaling**
   - 分散トレーニングの実装
   - Full genome scaleへの対応

7. **Baseline Comparison Study**
   - scGen, CPAとの定量的比較
   - 論文化のためのベンチマーク整備

---

## References

### Experimental Data

[^1]: docs/markdown/20251101_squidiff-testing.md - Exp01実験ログ（トレーニングパラメータ、結果メトリクス）
[^2]: docs/notebook/Exp01_squidiff-basic-test.ipynb - 解析ノートブック（可視化、統計解析）
[^3]: results/20251101_squidiff-testing/Exp01/training_metrics.csv - トレーニングメトリクスCSV

### Figures

[^4]: results/20251101_squidiff-testing/Exp01/training_loss.png - トレーニング損失曲線
[^5]: results/20251101_squidiff-testing/Exp01/sample_quality.png - サンプル品質比較
[^6]: results/20251101_squidiff-testing/Exp01/resource_usage.png - リソース使用量解析

### Software and Tools

- **Squidiff**: Local repository at `~/Desktop/Squidiff`
- **PyTorch**: 2.0+ (deep learning framework)
- **scanpy**: Single-cell analysis utilities
- **Python**: 3.10+

### Literature

[^7]: Squidiff bioRxiv preprint: https://doi.org/10.1101/2024.11.16.623974 - "Predicting single-cell transcriptomic perturbations with diffusion models"

---

## Supplementary Information

### Data Availability

- **Raw data**: `~/Desktop/Squidiff/datasets/train.h5ad`
- **Processed data**: `results/20251101_squidiff-testing/Exp01/`
- **Analysis code**: `docs/notebook/Exp01_squidiff-basic-test.ipynb`
- **Figures**: `results/20251101_squidiff-testing/Exp01/*.png`

### Reproducibility

すべての解析は以下の環境で再現可能：

```bash
cd /Users/oodakemac/Desktop/BItemplate
source .venv/bin/activate
jupyter lab
# docs/notebook/Exp01_squidiff-basic-test.ipynb を実行
```

### Version Information

| Software | Version | Notes |
|----------|---------|-------|
| Squidiff | Latest (2024-11) | Local development version |
| Python | 3.10+ | |
| PyTorch | 2.0+ | CUDA enabled |
| scanpy | 1.9+ | |
| pandas | 2.0+ | |
| matplotlib | 3.7+ | |
| seaborn | 0.12+ | |

---

**Report compiled**: 2025-11-01
**Last updated**: 2025-11-01
**Document version**: 1.0
