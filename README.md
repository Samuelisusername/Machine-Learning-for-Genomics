# Deep Generative Modeling for Single-Cell Annotation & Bulk Deconvolution

A PyTorch pipeline leveraging deep generative models (scVI/scANVI VAEs), unsupervised domain adaptation, and NNLS regression to learn compact latent representations from ~50k high-dimensional single-cell profiles for cell-type classification and bulk RNA-seq deconvolution.

---

## Architecture & Methodology

1. **Latent Representation Learning (VAEs)**
   * Trained deep generative models (scVI) to map high-dimensional, noisy single-cell count data into low-dimensional latent embeddings.
   * Leveraged semi-supervised Variational Autoencoders (scANVI) for cell-type annotation across unlabeled profiles.

2. **Domain Adaptation & Graph Clustering**
   * Aligned shifted data distributions across batches using Harmony domain adaptation.
   * Optimized KNN graph-clustering topology via grid search to enforce neighborhood structure in the latent space.

3. **Constrained Regression Deconvolution**
   * Constructed a Non-Negative Least Squares (NNLS) regression pipeline operating on signature matrices derived from latent embeddings to predict cell-type proportions in bulk RNA-seq samples.

---

## Results

| Task | Metric | Score |
| :--- | :--- | :--- |
| **Domain Alignment & Clustering** | Adjusted Rand Index (ARI) | **0.79** |
| **Bulk Sample Deconvolution** | Root Mean Square Error (RMSE) | **0.077** |
| **Class Benchmark** | Performance Ranking | **Top 10%** (+0.25 Grade Bonus) |

---

## Dependencies

```bash
pip install torch scanpy scvi-tools harmony-pytorch numpy pandas scikit-learn scipy



Epigenomic Gene Expression: Engineered TSS-centered 2kb genomic features across 7 histone and chromatin accessibility markers 

# Project 1
The project predicts gene expression levels (gex) across cell lines based on epigenomic histone modifications and chromatin accessibility around Transcription Start Sites (TSS).
## Project Overview
Gene regulation is heavily influenced by local chromatin state. This project extracts continuous and discrete genomic signals around TSS regions ($\pm 2000\text{ bp}$) to train regression models that rank and predict quantitative gene expression.Epigenomic Marks & Features: H3K27me3, H3K4me1, H3K4me3, H3K27ac, H3K36me3, H3K9me3, and DNase.Primary Metric: Spearman’s rank correlation ($\rho$).
## Pipeline Architecture
Feature Extraction (pyBigWig & pandas)BigWig Signal: Calculates mean signal intensity within a $\pm 2000\text{ bp}$ window around each gene's TSS.BED Peak Data: Extracts peak counts, maximum peak scores, cumulative peak lengths, and distance to the nearest peak.Data Preprocessing & TransformationApplies target log-transformation ($\log(1 + y)$) to handle skewed expression distributions.Handles missing genomic tracks using dynamic fallback values and imputation.
## Model Selection & Hyperparameter Tuning
XGBoost Regressor: Optimized via 5-Fold GridSearchCV using a custom Spearman correlation scorer (greater_is_better=True).Gaussian Process Regressor (GPR): Evaluated with RBF and White noise kernels for uncertainty analysis.Inference & SubmissionReverts log predictions via $\exp(x) - 1$.Generates formatted submission files for test cell lines ($X3$).
## Results

| Model | Target Metric | Validation Score (Spearman's $\rho$) |
| :--- | :--- | :--- |
| **XGBoost Regressor** (Tuned) | Spearman's rank correlation | **0.7625** |
| **Gaussian Process Regressor** | Spearman's rank correlation | 0.6025 |

---

## Dependencies

### Prerequisites
* Python >= 3.9

### Required Packages
* `numpy`
* `pandas`
* `scipy`
* `scikit-learn`
* `xgboost`
* `pyBigWig`

### Installation

```bash
pip install numpy pandas scipy scikit-learn xgboost pyBigWig
