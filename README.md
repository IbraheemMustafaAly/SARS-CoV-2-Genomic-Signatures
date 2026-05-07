# 🧬 SARS-CoV-2 Genomic Signatures — Explainable Analysis
 
[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://python.org)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Status](https://img.shields.io/badge/Status-In%20Progress-yellow.svg)]()
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org)
 
## Overview
 
This project extends the work of **Elsherbini et al. (BMC Bioinformatics, 2024)** by applying **explainable machine learning** to alignment-free genomic signature analysis of SARS-CoV-2 clades.
 
Instead of focusing solely on classification accuracy, this work investigates **why** certain k-mer features distinguish viral clades — providing biological interpretability through **SHAP analysis**, **CpG suppression quantification**, and **evolutionary trajectory modeling**.
 
> 📌 Dataset provided as part of the **SOLE Competition (Feb 2025)** — Dr. Mohamed Mysara, Nile University, Egypt.
 
---
 
## 🔬 Key Findings
 
- **UMAP** reveals clear separation of later clades (GRA/Omicron, GK, GRY/Alpha) — while earlier clades (G, GH, GR, GV) overlap, reflecting evolutionary proximity
- **Random Forest** achieves **81% accuracy** on 50,000 genomes without any sequence alignment
- **SHAP analysis** reveals clade-specific k-mer signatures:
  - **GRA/Omicron** → dominated by AT-rich motifs (ATA, TAT, GGG) — distinct from all other clades
  - **GK & GRY/Alpha** → dominated by CpG-containing motifs (CGG, CCG)
- **CpG suppression** confirmed across all clades (~60% below expected frequency)
- **Clade G** shows strongest CpG suppression (0.379) — suggesting rapid early host adaptation
- **GRA/Omicron** shows lowest GC-rich dinucleotide content — breaking the evolutionary trend
---
 
## 📊 Results Summary
 
| Analysis | Key Result |
|----------|-----------|
| PCA | 48% variance in 2 PCs — confirms non-linear structure |
| UMAP | GRA, GK, GRY clearly separated from earlier clades |
| Random Forest Accuracy | 81% (50k sample) |
| GRA (Omicron) F1-Score | **0.94** — highest among all clades |
| G (earliest) F1-Score | 0.67 — most difficult to classify |
| CpG Suppression | ~60% below expected across all clades |
| Clade G CpG | 0.379 — strongest suppression |
| Clade GR CpG | 0.408 — weakest suppression |
 
---
 
## 🗂️ Repository Structure
 
```
SARS-CoV-2-Genomic-Signatures/
│
├── README.md
│
├── notebooks/
│   ├── 01_EDA_and_PCA.ipynb
│   ├── 02_UMAP.ipynb
│   ├── 03_Random_Forest.ipynb
│   ├── 04_SHAP_Analysis.ipynb
│   ├── 05_CpG_Quantification.ipynb
│   └── 06_Evolutionary_Trajectory.ipynb
│
├── figures/
│   ├── pca_clean.png
│   ├── umap_plot.png
│   ├── confusion_matrix.png
│   ├── feature_importance.png
│   ├── shap_summary.png
│   ├── shap_per_clade.png
│   ├── heatmap_clades.png
│   ├── cpg_quantification.png
│   └── evolutionary_trajectory.png
│
├── requirements.txt
└── LICENSE
```
 
---
 
## 🔄 Analysis Pipeline
 
```
Raw k-mer frequencies (GenoSig — 560k genomes)
              ↓
     Outlier Removal (Z-score < 3)
              ↓
     PCA Visualization (2 components)
              ↓
     UMAP Visualization (non-linear)
              ↓
     Random Forest Classification
     (50k sample, 80/20 split, stratified)
              ↓
     Feature Importance Analysis
              ↓
     SHAP Explainability per Clade
              ↓
     CpG Suppression Quantification
              ↓
     Evolutionary Trajectory Analysis
```
 
---
 
## 📓 Notebooks
 
| # | Notebook | Description |
|---|----------|-------------|
| 01 | `EDA_and_PCA` | Exploratory data analysis, outlier removal, PCA visualization |
| 02 | `UMAP` | Non-linear dimensionality reduction and cluster visualization |
| 03 | `Random_Forest` | Classification, accuracy, confusion matrix, F1-scores |
| 04 | `SHAP_Analysis` | Global and per-clade explainability using SHAP values |
| 05 | `CpG_Quantification` | Biological CpG suppression analysis across clades |
| 06 | `Evolutionary_Trajectory` | Temporal trends in nucleotide composition across evolution |
 
---
 
## 📦 Requirements
 
```bash
pip install -r requirements.txt
```
 
**Main libraries:**
- `pandas`, `numpy`
- `scikit-learn`
- `matplotlib`, `seaborn`
- `umap-learn`
- `shap`
---
 
## 🧬 Dataset
 
- **560,000 SARS-CoV-2 whole genomes** from GISAID
- **80 features**: 16 Di-nucleotide + 64 Tri-nucleotide frequencies (normalized)
- **7 clades**: G, GH, GK, GR, GRA, GRY, GV
- Balanced dataset (~78k–84k genomes per clade)
- Generated using [GenoSig](https://github.com/AhmedElsherbini/Code_for_Elsherbini_et_al_2023)
> ⚠️ The raw dataset is not included in this repository. Please contact the dataset owner for access.
 
---
 
## 👥 Authors
 
- **Ibrahim Mustafa (Bembo)** — Bioinformatician & Field Application Specialist, MSc Student in Bioinformatics, University of Sadat City
- **[Co-author name]** — [Affiliation]
---
 
## 📚 Reference
 
Elsherbini et al. (2024). *Utilizing genomic signatures to gain insights into the dynamics of SARS-CoV-2 through Machine and Deep Learning techniques.* **BMC Bioinformatics**, 25, 131.
https://doi.org/10.1186/s12859-024-05648-2
 
---
 
## 📄 License
 
This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.
