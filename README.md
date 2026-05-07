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

- **UMAP** reveals clear separation of later clades (GRA/Omicron, GK, GRY/Alpha)
- **Random Forest** achieves **81% accuracy** on 50,000 genomes without any sequence alignment
- **SHAP analysis** reveals clade-specific k-mer signatures:
  - **GRA/Omicron** → dominated by AT-rich motifs (ATA, TAT, GGG)
  - **GK & GRY/Alpha** → dominated by CpG-containing motifs (CGG, CCG)
- **CpG suppression** confirmed across all clades (~60% below expected frequency)
- **Clade G** shows strongest CpG suppression (0.379) — suggesting rapid early host adaptation
- **GRA/Omicron** shows lowest GC-rich dinucleotide content — breaking the evolutionary trend

---

## 📊 Results

### 1. PCA — Dimensionality Reduction

> After outlier removal (Z-score < 3), PCA reveals the non-linear nature of genomic signatures. Only 48% of variance is captured in 2 components, confirming that k-mer space requires non-linear methods for proper visualization.

![PCA](figures/pca_clean.png)

---

### 2. UMAP — Non-linear Visualization

> UMAP clearly separates the **later clades** (GRA/Omicron, GK, GRY/Alpha) into distinct clusters, while earlier clades (G, GH, GR, GV) overlap — reflecting their evolutionary proximity.

![UMAP](figures/umap_plot.png)

---

### 3. Random Forest — Classification Performance

> Random Forest achieves **81% overall accuracy** on 50,000 genomes. Later clades (GRA, GK, GRY) show the highest F1-scores, consistent with their more divergent genomic signatures.

| Clade | F1-Score |
|-------|----------|
| GRA (Omicron) | **0.94** |
| GK | **0.89** |
| GRY (Alpha) | **0.88** |
| GV | 0.83 |
| GH | 0.72 |
| GR | 0.71 |
| G | 0.67 |

![Confusion Matrix](figures/confusion_matrix.png)

---

### 4. Feature Importance — Top k-mers

> CpG-containing trinucleotides (CGG, CCG) and G/C-rich motifs dominate the top features, confirming the biological relevance of CpG dynamics in SARS-CoV-2 evolution.

![Feature Importance](figures/feature_importance.png)

---

### 5. SHAP Analysis — Global Explainability

> SHAP values reveal that each clade contributes differently to each k-mer feature, providing a per-clade explainability layer beyond simple accuracy metrics.

![SHAP Summary](figures/shap_summary.png)

---

### 6. SHAP — Per Clade Signatures

> Clade-specific SHAP analysis reveals fundamentally different discriminative features:
> - **GRA/Omicron**: AT-rich motifs (ATA, TAT) — distinct from all other clades
> - **GK & GRY/Alpha**: CpG-containing motifs (CGG, CCG)

![SHAP per Clade](figures/shap_per_clade.png)

---

### 7. k-mer Heatmap — Mean Frequencies per Clade

> The heatmap confirms universal CpG suppression (CG column — dark blue across all clades) and reveals subtle differences in GC-rich motif composition between clades.

![Heatmap](figures/heatmap_clades.png)

---

### 8. CpG Suppression Quantification

> All clades show ~60% CpG suppression below the expected frequency (1.0), confirming strong host immune pressure. Clade G (earliest) shows the strongest suppression (0.379).

![CpG Quantification](figures/cpg_quantification.png)

---

### 9. Evolutionary Trajectory

> CpG suppression is most pronounced in Clade G (0.379) and stabilizes (~0.406) across later clades, suggesting rapid early host adaptation followed by an evolutionary plateau. GRA/Omicron breaks the GC-rich trend — a distinct evolutionary strategy.

![Evolutionary Trajectory](figures/evolutionary_trajectory.png)

---

## 📦 Results Summary

| Analysis | Key Result |
|----------|-----------|
| PCA | 48% variance in 2 PCs — non-linear structure confirmed |
| UMAP | GRA, GK, GRY clearly separated |
| Random Forest Accuracy | **81%** (50k sample, no alignment) |
| GRA F1-Score | **0.94** — highest among all clades |
| G F1-Score | 0.67 — most difficult (earliest clade) |
| CpG Suppression | ~60% below expected across all clades |
| Clade G CpG | 0.379 — strongest suppression |

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
| 01 | `EDA_and_PCA` | Exploratory data analysis, outlier removal, PCA |
| 02 | `UMAP` | Non-linear dimensionality reduction |
| 03 | `Random_Forest` | Classification, confusion matrix, F1-scores |
| 04 | `SHAP_Analysis` | Global and per-clade explainability |
| 05 | `CpG_Quantification` | CpG suppression analysis + heatmap |
| 06 | `Evolutionary_Trajectory` | Temporal trends in nucleotide composition |

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

- **Ibraheem Mustafa** — Bioinformatician & Field Application Specialist, MSc Student in Bioinformatics, University of Sadat City
- **Hagar El-Azab** — Bioinformatician, BSc Graduate in Biotechnology, Faculty of Agriculture, Cairo University

---

## 📚 Reference

Elsherbini et al. (2024). *Utilizing genomic signatures to gain insights into the dynamics of SARS-CoV-2 through Machine and Deep Learning techniques.* **BMC Bioinformatics**, 25, 131.
https://doi.org/10.1186/s12859-024-05648-2

---

## 📄 License

MIT License — see [LICENSE](LICENSE) for details.
