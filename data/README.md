# PhDAI 733-A02 — Group 8 Project
## Dataset Documentation & Clinical Data Dictionary: Heart Disease UCI (Cleveland)

**Institution:** Department of Computer and Information Sciences, University of the Cumberlands  
**Course:** PhDAI 733-A02: Python Application for Data Analytics in AI  
**Team:** Subba Taniparti · Harini Mamidala · Christian Gaston · Naveen Vishal Bellary  
**Instructor:** Dr. Karriem Perry  

---

## 1. Overview & Provenance

- **Dataset:** Heart Disease Dataset (Cleveland Clinic Foundation subset)
- **Original Citation:** Janosi, A., Steinbrunn, W., Pfisterer, M., & Detrano, R. (1989). *Heart Disease* [Data set]. UCI Machine Learning Repository. [https://doi.org/10.24432/C52P4X](https://doi.org/10.24432/C52P4X)
- **GitHub Mirror (Primary Ingestion Source):** [https://raw.githubusercontent.com/sharmaroshan/Heart-UCI-Dataset/master/heart.csv](https://raw.githubusercontent.com/sharmaroshan/Heart-UCI-Dataset/master/heart.csv)
- **Local Fallback:** `data/heart.csv`
- **Instance Count:** 303 raw patient records (302 after deduplication)
- **Feature Count:** 13 clinical & demographic predictors + 1 binary target

---

## 2. Target Variable & Critical Label Validation

> [!IMPORTANT]
> **Label Polarity Verification:**  
> In this repository's mirrored source, exploratory clinical validation against physiological markers (fluoroscopy vessel count `ca`, ST depression `oldpeak`, and exercise-induced angina `exang`) confirmed that:
> - `target = 0` $\rightarrow$ **Disease Present** (elevated fluoroscopy vessels, higher ST depression, higher angina prevalence)
> - `target = 1` $\rightarrow$ **Disease Absent / Healthy**
> 
> To adhere to standard machine learning convention ($1 = \text{positive case / disease}$, $0 = \text{negative / healthy}$) and prevent inverted clinical metrics, our analysis defines:
> ```python
> df['disease'] = 1 - df['target']
> ```
> **Overall Disease Prevalence:** $45.7\%$ (138 out of 302 patients).

---

## 3. Data Dictionary

The 13 predictors consist of continuous physiological measurements, binary indicators, and multi-category clinical integer codes.

| Variable | Type | Category | Description | Value Range / Units | Clinical Notes |
|---|---|---|---|---|---|
| `age` | Continuous | Demographic | Patient age | 29 – 77 years | Primary cardiovascular risk factor |
| `sex` | Binary | Demographic | Patient biological sex | `0` = Female, `1` = Male | Used for demographic fairness audit |
| `cp` | Categorical | Symptoms | Chest pain presentation type | `0`: Typical angina<br>`1`: Atypical angina<br>`2`: Non-anginal pain<br>`3`: Asymptomatic | Nominal integer code (requires one-hot encoding) |
| `trestbps` | Continuous | Baseline Vitals | Resting blood pressure | 94 – 200 mm Hg (on admission) | Hypertension indicator ($>130$ mm Hg elevated) |
| `chol` | Continuous | Laboratory | Serum cholesterol | 126 – 564 mg/dL | Serum lipid concentration |
| `fbs` | Binary | Laboratory | Fasting blood sugar | `1`: $>120$ mg/dL (true)<br>`0`: $\le 120$ mg/dL (false) | Potential diabetes indicator |
| `restecg` | Categorical | Diagnostic | Resting electrocardiographic results | `0`: Normal<br>`1`: ST-T wave abnormality<br>`2`: Left ventricular hypertrophy | Nominal diagnostic classification |
| `thalach` | Continuous | Stress Test | Maximum heart rate achieved | 71 – 202 bpm | Inversely correlated with disease severity |
| `exang` | Binary | Stress Test | Exercise-induced angina | `1` = Yes, `0` = No | Angina provoked during physical exertion |
| `oldpeak` | Continuous | Stress Test | ST depression induced by exercise relative to rest | 0.0 – 6.2 mm | Key electrocardiographic ischemia indicator |
| `slope` | Categorical | Stress Test | Slope of peak exercise ST segment | `0`: Upsloping<br>`1`: Flat<br>`2`: Downsloping | Downsloping / flat slopes correlate with ischemia |
| `ca` | Categorical | Diagnostic | Major vessels colored by fluoroscopy | 0 – 3 vessels (codes `0`, `1`, `2`, `3`, plus rare `4`) | Number of visible coronary vessels ($>0$ indicates blockage) |
| `thal` | Categorical | Diagnostic | Thallium scintigraphy stress test | `1`: Normal<br>`2`: Fixed defect<br>`3`: Reversible defect (also codes `0`) | Nuclear cardiology perfusion imaging |
| `target` | Binary | Outcome | Raw dataset diagnostic target | `0` = Disease present, `1` = Healthy | Corrected to `disease = 1 - target` in analysis |

---

## 4. Preprocessing & Data Hygiene Protocol

1. **Deduplication:** 1 exact duplicate record identified and dropped ($303 \to 302$ patients) to eliminate cross-split patient leakage.
2. **Missing Value Audit:** All 302 patient records are complete ($0$ missing values). Forward-fill imputation proposed in assignment hints was intentionally rejected because clinical records lack temporal sequence.
3. **Categorical Encoding:** Nominal integer codes (`cp`, `restecg`, `slope`, `ca`, `thal`) are converted to one-hot dummy variables (`pd.get_dummies(..., drop_first=True)` / `OneHotEncoder`) to prevent models from assuming false ordinal magnitude.
4. **Data Leakage Prevention (Pipeline Scaling):** Continuous features (`age`, `trestbps`, `chol`, `thalach`, `oldpeak`) are scaled using `StandardScaler` strictly encapsulated inside a `Pipeline` / `ColumnTransformer` fitted only on training folds.

---

## 5. Demographic & Subgroup Characteristics

- **Sex Breakdown:** 96 female (`sex = 0`, 31.8%) vs. 206 male (`sex = 1`, 68.2%)
- **Subgroup Prevalence Gap:**
  - `sex = 0` (Female): $25.0\%$ disease prevalence (24 / 96 patients)
  - `sex = 1` (Male): $55.3\%$ disease prevalence (114 / 206 patients)
- **Fairness Implications:** The lower baseline prevalence in the `sex = 0` group suppresses subgroup recall at default decision thresholds (0.50), motivating threshold calibration in clinical triage applications.
