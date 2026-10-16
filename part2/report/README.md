# Part 2 Report

Due: Friday 16 October 2026

## Section owners

| Section | Owner |
| --- | --- |
| Recap: problem, stakeholders, dataset | Christian Gaston |
| 1. Hyperparameter Tuning | Subba Taniparti |
| 2. Final Model Evaluation | Subba Taniparti (metrics), Harini Mamidala (figures) |
| 3. Ethical Considerations | Bellary Naveen Vishal |
| 4. Real-World Application | Christian Gaston |
| 5. Final Thoughts and Conclusion | Harini Mamidala |
| 6. Teamwork and Documentation | Bellary Naveen Vishal |

## Figures

Exported from the analysis notebook to `part2/figures/`. Each needs an APA caption with an
interpretive note stating what the reader should conclude, not a restatement of the title.

These are the final committed figures:

| File | Appears as | Supports |
| --- | --- | --- |
| `p2_fig1_calibration.png` | Figure A1 | Final Model Evaluation, whether predicted probabilities are trustworthy |
| `p2_fig3_confusion.png` | Figure A2 | Final Model Evaluation, the threshold trade in patient counts |
| `fig2_threshold_stability.png` | Figure A3 | Ethical Considerations, the group-specific threshold is unstable |

## References to carry forward from Part 1

Part 1 cited 21 sources. The following were carried forward from `part1/report/Group8_Part1_Report.docx` to the final 8-entry reference list:

- Janosi et al. (1989) — dataset provenance
- Pedregosa et al. (2011) — scikit-learn
- Rajkomar et al. (2018) — why protected attributes are retained for evaluation
- Chen et al. (2019) — deployment oversight

Considered and not used:
- Obermeyer et al. (2019) — algorithms inheriting historical patterns (considered and not used)
- Mosca et al. (2011) — sex differences in cardiovascular care (considered and not used)

## Before submission

- [x] Every number in the report matches the notebook
- [x] All in-text citations appear in the reference list and vice versa
- [x] Zero em-dashes (search for the character)
- [x] Bounded statistics have no leading zero; values that can exceed 1 keep theirs
- [x] Figures have interpretive captions
- [x] Notebook committed with outputs intact
