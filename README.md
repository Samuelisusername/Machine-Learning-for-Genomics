Built PyTorch deep generative models (scVI/scANVI) and NNLS regression pipelines to annotate $\sim$50k single-cell profiles and deconvolve bulk RNA-seq samples (RMSE: 0.077).


Developed an end-to-end Scanpy and Harmony batch-correction pipeline, optimizing graph clustering via grid search to achieve a 0.79 ARI score earning a 0.25 grade bonus for ranking in the top 10\% of the class.}



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
