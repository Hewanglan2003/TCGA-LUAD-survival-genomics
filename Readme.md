# TCGA-LUAD Survival Analysis with Elastic Net Cox Model

## Overview
This project investigates the association between gene expression profiles and overall survival (OS) in TCGA lung adenocarcinoma (LUAD) patients.  
We applied univariate Cox regression to screen survival-related genes and constructed a multigene prognostic risk score using an elastic net–penalized Cox model. The prognostic value of the derived risk score was evaluated using Kaplan–Meier survival analysis and multivariable Cox regression adjusting for clinical covariates.

---

## Data Source
- Gene expression and clinical data were obtained from **TCGA-LUAD** via the GDC Data Portal.
- Raw expression counts were filtered, variance-stabilized, and aligned with clinical metadata.
- Large raw data files are not tracked in this repository.

---

## Methods
1. **Preprocessing**
   - Low-expression genes were filtered.
   - Variance-stabilizing transformation (VST) was applied.
   - Genes with low variance were removed.

2. **Univariate Cox Regression**
   - Each gene was tested for association with OS.
   - False discovery rate (FDR) was controlled using the Benjamini–Hochberg method.

3. **Elastic Net Cox Model**
   - An elastic net–penalized Cox model (α = 0.5) was fitted using cross-validation.
   - A 47-gene signature was selected at λ_min.

4. **Risk Score Construction**
   - A continuous risk score was computed for each patient.
   - Patients were stratified into high- and low-risk groups using the median risk score.

5. **Survival Analysis**
   - Kaplan–Meier survival curves were generated.
   - Univariate and multivariable Cox models were fitted, adjusting for age, gender, and AJCC pathologic stage.

---

## Results Summary
- A 47-gene prognostic signature was identified using elastic net Cox regression.
- The derived risk score showed a strong association with overall survival.
- In multivariable Cox analysis, the risk score remained an independent predictor of OS after adjusting for clinical covariates.
- Kaplan–Meier analysis demonstrated significantly worse survival in the high-risk group.

---

## Repository Structure
```text
├── Cox regression for OS.Rmd        # Univariate and multivariable Cox analyses
├── TCGA-LUAD-download.Rmd           # Data download and preprocessing
├── Genetics Analysis.Rmd            # Gene-level analyses and elastic net modeling
├── Results.md                       # Detailed results and figures
├── README.md                        # Project overview (this file)
├── R data/                          # Intermediate data 
├── R results/                       # Model outputs and figures 
└── .gitignore
