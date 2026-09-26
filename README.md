# PhDAI 733-A02: Python Application for Data Analytics in AI
## Group 8 — Project Part 1: Clinical Decision-Support Prototype for Heart Disease Risk

**Institution:** Department of Computer and Information Sciences, University of the Cumberlands  
**Course:** PhDAI 733-A02: Python Application for Data Analytics in AI  
**Instructor:** Dr. Karriem Perry  
**Term:** Fall 2026  
**GitHub Repository:** [https://github.com/scalesynthai/phdai733-group8](https://github.com/scalesynthai/phdai733-group8)  

**Research Cohort (Group 8):**
- **Subba Taniparti**
- **Harini Mamidala**
- **Christian Gaston**
- **Naveen Vishal Bellary**

---

## Interactive Notebooks & Research Artifacts

| Research Artifact | Scope & Methodological Focus | Direct Access |
|---|---|---|
| **Master Analysis & Modeling Pipeline** | End-to-end clinical pipeline: label validation, leakage-free modeling, 30-split stability, & fairness audit | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/scalesynthai/phdai733-group8/blob/main/part1/notebooks/Group8_Part1_Analysis.ipynb) |
| **Exploratory Data Analysis (PR #2)** | In-depth EDA, univariate/bivariate profiling, and clinical distributions (Naveen Vishal) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/scalesynthai/phdai733-group8/blob/main/part1/notebooks/Bellary_Naveen_Vishal_Data_Exploration.ipynb) |
| **Model Development & CV Tuning** | Pipeline architecture, GridSearchCV tuning, and 30-iteration Monte Carlo CV (Subba) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/scalesynthai/phdai733-group8/blob/main/part1/notebooks/Subba_Taniparti_Model_Development.ipynb) |
| **Dataset Selection & Evaluation (PR #1)** | Rubric scoring and multi-dataset comparison analysis (Naveen Vishal & Subba) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/scalesynthai/phdai733-group8/blob/main/part1/notebooks/Group8_Project_1_Data_loading.ipynb) |

---

## 1. Research Overview & Problem Formulation

Cardiovascular disease remains the leading cause of global mortality. While downstream interventional cardiology treatments are well established, clinical triage presents a critical optimization challenge: specialist referrals and coronary angiograms are invasive and resource-intensive, whereas delayed or missed diagnoses carry catastrophic clinical consequences.

This study develops and audits a machine learning prototype for **clinical triage decision-support** (stratifying patients for further cardiac investigation) rather than automated definitive diagnosis, utilizing 13 non-invasive clinical and demographic predictors from the Heart Disease UCI dataset.

### Research Questions & Hypotheses

- **Research Question 1 (RQ1):** Can non-invasive, routinely collected clinical measurements predict presence of heart disease significantly above a naive majority-class baseline?
  - **Hypothesis 1 (H1):** Both linear and ensemble models will substantially outperform baseline classifiers due to the strong physiological signal in exercise hemodynamics and fluoroscopy markers.
- **Research Question 2 (RQ2):** Does a non-linear ensemble (Random Forest) outperform a regularized linear model (Logistic Regression) in a small-sample clinical regime ($N=302$), and is the performance ranking stable across resampling?
  - **Hypothesis 2 (H2):** Regularized Logistic Regression will achieve equal or superior performance with lower variance, as small sample sizes limit the non-linear partition benefits of tree ensembles.
- **Research Question 3 (RQ3):** Does diagnostic performance exhibit systematic disparities across demographic subgroups (`sex`), and what underlying mechanism drives any observed gap?
  - **Hypothesis 3 (H3):** Subgroup performance disparities will manifest primarily through differential disease prevalence (base rate disparity: 25.0% in females vs 55.3% in males) suppressing recall at default decision thresholds, rather than explicit reliance on demographic features.

---

## 2. Dataset & Reproducibility Protocol

- **Cohort:** Heart Disease Dataset (Cleveland Clinic Foundation subset; Janosi et al., 1989)
- **Sample Dimensions:** 303 raw patient records $\to$ 302 patients after exact duplicate elimination
- **Predictor Space:** 13 clinical variables (5 continuous, 3 binary, 5 nominal categorical codes)
- **Target Variable:** Binary presence of coronary artery disease ($\ge 50\%$ diameter narrowing)

### Ingestion Standard
To ensure exact byte-level parity across heterogeneous compute environments (Google Colab and local environments), data is loaded directly from a version-controlled source URL, with local caching in `data/heart.csv`:

```python
import pandas as pd

DATA_URL = 'https://raw.githubusercontent.com/sharmaroshan/Heart-UCI-Dataset/master/heart.csv'
df_raw = pd.read_csv(DATA_URL)
```

For complete feature dictionaries, units, reference ranges, and clinical notes, refer to the [Dataset Documentation](data/README.md).

---

## 3. Repository Architecture

```
phdai733-group8/
├── DECISIONS.md        # Comprehensive, dated decision log for Section 4 teamwork audit
├── README.md           # Master research documentation and navigation guide
├── data/
│   ├── README.md       # Comprehensive clinical data dictionary and metadata
│   └── heart.csv       # Local fallback dataset copy
├── part1/
│   ├── figures/        # High-resolution exported figures (Appendix Figs A1–A3)
│   │   └── unused/     # Pruned exploratory figures (Figs 2 & 4)
│   ├── notebooks/      # Modular research and individual contribution notebooks
│   │   ├── Group8_Part1_Analysis.ipynb                # Master clinical modeling & fairness pipeline
│   │   ├── Bellary_Naveen_Vishal_Data_Exploration.ipynb  # EDA & distribution analysis (PR #2)
│   │   ├── Subba_Taniparti_Model_Development.ipynb     # Model pipeline & CV experiments
│   │   ├── Group8_Project_1_Data_loading.ipynb        # Candidate dataset evaluation (PR #1)
│   │   └── archive/                                   # Archived duplicate/intermediate notebooks
│   └── report/
│       ├── Group8_Part1_Report_FINAL.docx             # Final consolidated submission deliverable
│       └── drafts/                                    # Archived report iterations (Drafts 1–3)
└── part2/              # Reserved for Part 2 deliverables
```

---

## 4. Part 1 Deliverables & Rubric Ownership

**Submission Deadline:** Sunday, September 27, 2026, 11:59 PM EDT

| Rubric Area | Weight | Primary Owner(s) | Focus & Key Contributions |
|---|---|---|---|
| **1. Problem Definition + Real-World Application** | 25% | Christian Gaston & Naveen Vishal Bellary | Clinical decision-support framing, triage cost-asymmetry formulation, literature grounding |
| **2. Dataset Exploration + Ethics & Impact** | 25% | Harini Mamidala & Naveen Vishal Bellary | Exploratory data analysis, deduplication, nominal encoding, empirical demographic fairness audit |
| **3. Model Development + Optimization & Evaluation** | 30% | Subba Taniparti | Leakage-free `Pipeline` architecture, Stratified 5-Fold & 30-split Monte Carlo CV, ROC-AUC/Recall tuning |
| **4. Teamwork & Documentation + Writing & Structure** | 20% | Collaborative (Lead: Christian Gaston) | Multi-notebook synthesis, auditable decision logging ([DECISIONS.md](DECISIONS.md)), report composition |

---

## 5. Methodological & Technical Rigor

1. **Target Polarity Validation:** Cross-referenced raw target codes against established clinical indicators (fluoroscopy vessels `ca`, exercise ST depression `oldpeak`, exercise angina `exang`) to correct an inverted mirror label convention (`disease = 1 - target`).
2. **Leakage-Free Preprocessing:** Encapsulated continuous feature normalization (`StandardScaler`) and nominal dummy encoding (`OneHotEncoder`) inside a scikit-learn `Pipeline`/`ColumnTransformer` fitted strictly on training folds post-split.
3. **Small-Sample Stability Assessment:** Evaluated models using both 5-fold Stratified Cross-Validation and 30-iteration Monte Carlo CV simulations ($75/25$ stratified splits) to quantify empirical confidence intervals and avoid single-split variance artifacts.
4. **Clinical Objective Function:** Tuned hyperparameters and decision thresholds for ROC-AUC and Recall (Sensitivity), reflecting the asymmetrical clinical penalty of false negatives in medical screening.
5. **Empirical Subgroup Fairness Audit:** Disaggregated performance across patient `sex` to detect sensitivity trade-offs and evaluate base-rate disparity effects.

---

## 6. Collaboration Standards & Governance

- **Shared Drafting Workflow:** The team drafted collaboratively in a shared Google Colab notebook, which was then synchronised to this repository by one member. This avoided the merge conflicts that concurrent Jupyter edits produce, at the cost of a commit history that records the synchronisation rather than individual authorship. See the attribution note in [DECISIONS.md](DECISIONS.md).
- **Output Retention:** Notebook outputs are retained in committed files so that reported results are verifiable directly from the repository. Output stripping was disabled for this reason.
- **Traceable Decision Logging:** All experimental design pivots, baseline departures, and technical trade-offs are logged chronologically in [DECISIONS.md](DECISIONS.md) to provide verifiable evidence of collaborative research governance.

---

## References

1. Janosi, A., Steinbrunn, W., Pfisterer, M., & Detrano, R. (1989). *Heart Disease* [Data set]. UCI Machine Learning Repository. [https://doi.org/10.24432/C52P4X](https://doi.org/10.24432/C52P4X)
2. Pedregosa, F., Varoquaux, G., Gramfort, A., Michel, V., Thirion, B., Grisel, O., ... & Duchesnay, E. (2011). Scikit-learn: Machine learning in Python. *Journal of Machine Learning Research, 12*, 2825–2830.
