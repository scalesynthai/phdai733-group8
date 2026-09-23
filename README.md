# PhDAI 733-A02 — Group 8

Course project repository for *Python Application for Data Analytics in AI*.

**Team:** Subba Taniparti · Harini Mamidala · Christian Gaston · Naveen Vishal Bellary
**Instructor:** Dr. Karriem Perry

## Dataset

Heart Disease UCI — 303 patients, 13 predictors, binary target (presence of heart disease).

```python
URL = 'https://raw.githubusercontent.com/sharmaroshan/Heart-UCI-Dataset/master/heart.csv'
df = pd.read_csv(URL)
```

Loading by URL rather than committing the file keeps the repo clean and guarantees everyone
works from an identical copy. A local copy lives in `data/` as a fallback.

## Layout

```
part1/
  notebooks/   analysis notebooks, one per owner to avoid merge conflicts
  report/      written deliverable
  figures/     exported PNGs used in the report
part2/         (same structure, added later)
data/          dataset copy
DECISIONS.md   log of decisions and who made them
```

## Part 1 — due Sunday, September 27, 2026, 11:59 PM EDT

| Area | Rubric weight | Owner |
|---|---|---|
| Problem Definition + Real-World Application | 25% | TBD |
| Dataset Exploration + Ethics & Impact | 25% | TBD |
| Model Development + Optimization & Evaluation | 30% | TBD |
| Teamwork & Documentation + Writing & Structure | 20% | TBD |

## Working agreement

**One notebook per person** in `part1/notebooks/`, named `<name>_<area>.ipynb`. Jupyter files
store output cells and execution counts, so two people editing the same notebook produces merge
conflicts that are painful to resolve by hand. Separate notebooks, merged at the end by whoever
owns assembly, avoids this entirely.

**Clear outputs before committing** where practical (`Kernel → Restart & Clear Output`), or run
`nbstripout --install` once in the repo to do it automatically.

**Log decisions in `DECISIONS.md`** as they happen. Section 4 of the report is graded on
documenting the team process, and a dated log is far better evidence than scrolling back through
WhatsApp.
