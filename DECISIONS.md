# PhDAI 733-A02 — Group 8 Project
## Research Decision & Methodology Log

**Institution:** Department of Computer and Information Sciences, University of the Cumberlands  
**Course:** PhDAI 733-A02: Python Application for Data Analytics in AI  
**Instructor:** Dr. Karriem Perry  
**Team Members:** Subba Taniparti · Harini Mamidala · Christian Gaston · Naveen Vishal Bellary  

---

### Purpose & Documentation Standards
This decision log serves as the primary auditable record of the research process, technical decisions, experimental design trade-offs, and collaborative governance for Group 8. Per the course evaluation criteria (Section 4: Teamwork & Documentation), entries are maintained chronologically to reflect methodological formulation, technical departures from assignment hints, consensus mechanisms, and individual contributions.

**Log Format:** `YYYY-MM-DD — Decision & Technical Rationale — Originator / Consensus Mechanism`

---

### Chronological Decision Log

- **2026-09-22 — Team Formation & Research Kickoff:** Formed 4-member research cohort; established initial communication via Blackboard — Subba
- **2026-09-23 — Collaborative Infrastructure:** Established WhatsApp as the primary real-time communication channel and synchronized scheduling for sprint check-ins — Subba
- **2026-09-23 — Cohort Finalization:** Onboarded Naveen Vishal Bellary and Christian Gaston; finalized 4-member research team — Team consensus
- **2026-09-23 — Dataset Benchmarking & Multi-Criteria Evaluation:** Evaluated five candidate datasets (Heart Disease UCI, Credit Card Default, Diabetes 130-Hospitals, Online Retail, NYC Taxi) against rubric criteria (feasibility, clinical/business relevance, demographic variables for ethics audit) — Naveen Vishal & Subba
- **2026-09-23 — Dataset Selection (Heart Disease UCI):** Selected Heart Disease UCI (Cleveland subset, $N=303$) for clinical clarity, complete feature sets, and demographic attributes permitting empirical fairness audits — Proposed by Naveen Vishal; unanimously approved by Harini, Christian, and Subba
- **2026-09-23 — Reproducibility Standard (Remote URL Ingestion):** Mandated remote GitHub URL data loading with local fallback (`data/heart.csv`) to ensure byte-level environment parity across Google Colab and local Python environments — Harini & Subba
- **2026-09-23 — Version Control & Branch Hygiene:** Established repository structure with isolated per-member notebooks (`<name>_<area>.ipynb`) and automated `nbstripout` execution to eliminate Jupyter JSON merge conflicts — Christian; adopted by team
- **2026-09-23 — Research Role & Section Allocation:** Distributed responsibilities across rubric sections aligned with team strengths:
  - **Harini Mamidala:** Problem Framing, Clinical Translation, Triage Asymmetry Analysis (Section 1)
  - **Naveen Vishal Bellary:** Dataset Exploration, Preprocessing Architecture & EDA Visualizations (Section 2)
  - **Subba Taniparti:** Leakage-Free Model Pipeline, Hyperparameter Tuning & Cross-Validation Architecture (Section 3)
  - **Christian Gaston:** Candidate Dataset Analysis, Feature Engineering & Empirical Ethics/Fairness Audit (Section 4) & Report Synthesis (Lead)
  — Agreed collaboratively
- **2026-09-24 — Dataset Selection & Recommendation Notebook Contribution (PR #1):** Naveen Vishal completed candidate dataset benchmarking and rubric scoring analysis in `part1/notebooks/Gropup_Project_1.ipynb`, submitting Pull Request #1 (`feature/dataset-selection-analysis`) which was reviewed and merged into `main` — Naveen Vishal & Subba
- **2026-09-24 — Data Hygiene & Exact Duplicate Removal:** Identified 1 exact duplicate patient row during initial profiling and removed it ($303 \to 302$ patients) to eliminate cross-split data leakage — Harini & Naveen Vishal; verified by team
- **2026-09-24 — Target Label Audit & Polarity Correction:** Discovered dataset mirror used an inverted label convention (`target=0` denoting heart disease presence, `target=1` denoting absence) by cross-referencing clinical markers (fluoroscopy vessel count `ca`, ST depression `oldpeak`, exercise angina `exang`); corrected to `disease = 1 - target` to ensure clinical metric integrity — Christian & Subba; confirmed by team
- **2026-09-24 — Imputation Strategy Formulation:** Formally audited missingness (0 missing values across all 302 patients); explicitly rejected forward-fill imputation suggested in assignment hints as theoretically unsound for unordered clinical records — Harini, Naveen Vishal & Subba
- **2026-09-24 — Categorical Encoding Architecture:** Replaced nominal integer representations (`cp`, `restecg`, `slope`, `ca`, `thal`) with one-hot dummy variables (`drop_first=True`) rather than treating them as continuous ordinal integers — Harini & Naveen Vishal; implemented into preprocessing
- **2026-09-24 — Data Leakage Prevention (Pipeline Scaling):** Encapsulated continuous feature standardization (`StandardScaler`) within a scikit-learn `Pipeline`/`ColumnTransformer` fitted strictly on training folds post-split, departing from the assignment hint of pre-split scaling to avoid data leakage — Subba; adopted by team
- **2026-09-24 — Validation Rigor for Small Samples (RQ2/H2):** Supplemented 5-fold Stratified K-Fold CV with a 30-iteration Monte Carlo CV simulation ($75/25$ split) to quantify metric variance and ensure model ranking stability on $N=302$ — Naveen Vishal & Subba
- **2026-09-24 — Clinical Metric Prioritization (Triage Asymmetry):** Formulated model evaluation around ROC-AUC and Recall (Sensitivity) rather than raw Accuracy to penalize false negatives (missed cardiac cases) in a clinical triage setting — Christian & Subba; approved by team
- **2026-09-24 — Algorithmic Fairness & Subgroup Prevalence Audit (RQ3/H3):** Disaggregated model performance across patient `sex`; discovered that despite higher accuracy in `sex=0` (0.917 vs 0.788), recall was substantially lower (0.714 vs 0.821), empirically attributing this disparity to baseline prevalence imbalance (25.0% vs 55.3%) rather than direct feature bias — Naveen Vishal & Christian; documented for Section 4
- **2026-09-24 — Dataset Exploration Notebook Contribution (PR #2):** Naveen Vishal completed exploratory data profiling and feature distribution analysis in `part1/notebooks/Bellary_Naveen_Vishal_Data_Exploration.ipynb`, submitting Pull Request #2 (`feature/DataExploration`) which was reviewed and merged into `main` — Naveen Vishal & Subba
- **2026-09-24 — Written Report Deliverable Iteration (Draft v2):** Christian consolidated initial section submissions, synthesized clinical and ethics narratives into Report Draft v2, and shared with the team for collaborative review — Christian
- **2026-09-24 — Written Report Deliverable Refinement (Draft v3):** Subba modified Draft v2, integrated final model evaluation figures, updated methodology descriptions to Draft v3, and transmitted to Christian for editorial review and input — Subba & Christian
- **2026-09-25 — Ethics & Teamwork Collaboration Documentation Delivery:** Christian authored and delivered the finalized written sections for Ethics & Impact (demographic fairness audit, subgroup recall disparity analysis) and Teamwork Collaboration Process for integration into the report deliverable — Christian; shared with team
- **2026-09-25 — Final Report & Codebase Consolidation:** Finalized submission artifacts; audited and corrected label polarity in exploratory notebooks, standardized master analysis notebook (`Group8_Part1_Analysis.ipynb`), archived superseded report drafts, and designated `Group8_Part1_Report_FINAL.docx` as the authoritative report deliverable — Team consensus
- **2026-09-25 — Version Control Attribution Note:** The team drafted collaboratively in a shared Google Colab notebook rather than committing individually. Subba Taniparti synchronised that work to GitHub, so the commit history attributes to a single account and does not reflect individual contribution. The role assignments recorded above and Section 4 of the report are the authoritative record of who did what; the commit log reflects the synchronisation mechanism only — Team consensus



