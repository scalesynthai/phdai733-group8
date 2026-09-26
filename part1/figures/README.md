# Part 1 Figures & Visual Artifacts

This directory contains the publication-quality exported figures embedded as Appendix Figures A1–A3 in the final written report deliverable (`part1/report/Group8_Part1_Report_FINAL.docx`).

---

## Active Report Figures (Appendix Figures A1–A3)

### Figure A1: Exploratory Data Analysis & Physiological Distributions
**File:** [`fig1_eda.png`](fig1_eda.png)  
**Report Reference:** Appendix Figure A1 (Section 2 — Dataset Exploration & Preprocessing)  
**Description:**
- **Panel A (Class Distribution):** Visualizes disease prevalence ($45.7\%$, 138 / 302 patients), demonstrating balanced class proportions and justifying the lack of synthetic resampling.
- **Panel B (Maximum Heart Rate `thalach`):** Boxplot comparing peak exercise heart rate by outcome, showing significantly lower achieved heart rate in patients with coronary disease ($139.10$ vs $158.38$ bpm).
- **Panel C (Exercise ST Depression `oldpeak`):** Boxplot comparing exercise-induced ST segment depression, showing markedly higher depression in diseased patients ($1.59$ vs $0.59$ mm), consistent with myocardial ischemia.

---

### Figure A2: Confusion Matrices & Clinical Error Analysis
**File:** [`fig3_confusion.png`](fig3_confusion.png)  
**Report Reference:** Appendix Figure A2 (Section 3 — Model Development & Optimization, RQ2 / H2)  
**Description:**
- **Panel A (Tuned Logistic Regression):** Confusion matrix on held-out test set ($N=76$). Yields 82.9% accuracy with only 7 false negatives (missed disease cases).
- **Panel B (Tuned Random Forest):** Confusion matrix on held-out test set ($N=76$). Yields 77.6% accuracy with 10 false negatives.
- **Clinical Implication:** In clinical screening and triage, minimizing false negatives is critical to avoid untreated cardiac disease; Logistic Regression demonstrates superior sensitivity and fewer missed cases.

---

### Figure A3: Algorithmic Fairness & Subgroup Stability Audit
**File:** [`fig5_fairness.png`](fig5_fairness.png)  
**Report Reference:** Appendix Figure A3 (Section 4 — Ethics, Impact & Demographic Fairness, RQ3 / H3)  
**Description:**
- **Panel A (Recall by Subgroup & Model):** Compares sensitivity across patient biological sex (`sex = 0` female vs `sex = 1` male), illustrating the recall penalty experienced by the lower-prevalence group (`sex = 0`: 71.4% recall vs `sex = 1`: 82.1% recall).
- **Panel B (Recall Gap Distribution Across 30 Resampling Splits):** Histogram of the recall disparity ($\text{Recall}_{\text{female}} - \text{Recall}_{\text{male}}$) across 30 independent stratified train/test iterations (mean gap: $-0.090 \pm 0.184$), confirming prevalence-driven disparity while documenting small-sample variance bounds.

---

## Archived / Unused Figures
The following figures generated during exploratory analysis were pruned during page budget formatting and are archived in [`unused/`](unused/):
- `unused/fig2_corr.png` — Pairwise correlation heatmap and univariate Pearson $r$ rankings.
- `unused/fig4_roc.png` — Receiver Operating Characteristic (ROC) curve comparisons.
