# SPSS Assignment 1 — Grading Review

**Student:** Jason O'Brien
**Course:** CI 7303 — Psychometric Methods
**Assignment:** SPSS Assignment 1: Data Quality and Reliability Analysis
**Date Reviewed:** 2026-03-23
**Tool Used:** Python (in place of SPSS), with AI assistance (disclosed)

---

## Overall Grade Estimate: A

This submission meets or exceeds every requirement in the lab handout, demonstrates genuine conceptual understanding beyond surface-level reporting, and presents the work in a format that would export cleanly as a PDF. The decision to use Python instead of SPSS is defensible given the equivalence of procedures and the transparent disclosure.

---

## Section-by-Section Assessment

### 1. Data Import and Overview — Full Credit

The notebook loads the `.sav` file using `pyreadstat`, confirms 384 observations and 19 variables, and displays the first rows. A clear variable-group table identifies SECT items, SFT items, pre-computed scales, and outcome variables. This exceeds the handout requirement to "confirm variable names, value labels, and measurement levels" — the student organized them into a meaningful taxonomy.

### 2. Descriptive Statistics (Means, SDs, Frequencies) — Full Credit

- Full descriptive table with count, mean, SD, min, quartiles, max for all 19 variables.
- Frequency distributions printed for all 13 scale items.
- Interpretation correctly notes that means fall in the expected 3.0–4.0 range for 5-point Likert items.
- The student immediately flags the two non-plausible values (sect18_2 max = 9, sft71_2 min = 0) from the descriptive output, which shows they actually read the table rather than just generating it.

### 3. Missing Data Analysis — Full Credit (Exceeds Expectations)

- Missing data table correctly identifies the four variables with missingness: sect21_2 (1.8%), sft74_2 (3.4%), Exam_Score (7.8%), Homework_Score (1.3%).
- The interpretation goes well beyond the handout requirement. The handout asks: "Is missing data minimal and randomly distributed across items?" The student answers this directly, then provides a substantive explanation of MCAR, MAR, and MNAR mechanisms with concrete examples. This demonstrates understanding of the concepts, not just ability to report numbers.
- The conclusion that the pattern is consistent with MCAR/MAR is reasonable and correctly justified.

### 4. Non-Plausible Values and Outliers — Full Credit

- Both non-plausible values correctly identified by case ID (3102, 3334) and value.
- Boxplots generated for both item sets and outcome variables, matching the handout's Explore procedure.
- The distinction between non-plausible values and outliers is explicitly stated and correct: "These are not outliers (extreme but possible values); they are impossible values on the measurement scale."
- The rationale for recoding to NaN rather than imputing is sound: "Imputation assumes a true score exists to be estimated — for an impossible value, there is no underlying true score to recover."
- Outcome variable outliers (Homework_Score near 150, Exam_Score above 100) are flagged but retained with appropriate justification. This shows judgment rather than mechanical application of rules.
- Cleaning is performed transparently with before/after verification.

### 5. Reliability Analysis (Cronbach's Alpha) — Full Credit

**Statistical accuracy check:**

- SECT alpha = .8564 (8 items). This is plausible and consistent with the reported item-total correlations. The custom function uses the correct formula: (k/(k-1)) * (1 - sum(item variances)/total variance), with ddof=1 for sample variance.
- SFT alpha = .6626 (5 items). Also plausible given the item count and correlation magnitudes.
- Alpha-if-deleted values all fall below their respective overall alphas for both scales — correctly computed and correctly interpreted.
- Corrected item-total correlations use the standard approach (correlate item with sum of remaining items). Values are in the expected range.

**No computational errors detected.** The custom functions replicate the standard SPSS Reliability procedure correctly.

### 6. Alpha-if-Item-Deleted Interpretation — Full Credit (Exceeds Expectations)

This is the strongest section of the submission. Key observations:

- SECT interpretation correctly notes all alpha-if-deleted values fall below .856, meaning no item weakens the scale. The corrected item-total correlation range (.58–.65) is correctly characterized as moderate-to-strong.
- SFT interpretation correctly identifies that the low alpha is not attributable to any single bad item — all alpha-if-deleted values are below .663.
- The explanation of why a 5-item scale produces lower alpha than an 8-item scale with similar inter-item correlations is accurate and demonstrates understanding of the Spearman-Brown relationship. This is a conceptual point many students miss entirely.
- The student raises the alternative explanation (multidimensionality) and correctly notes that factor analysis would be needed to distinguish it from the item-count explanation. This shows the student is thinking about what the statistic does and does not tell you.

### 7. Scale Score Creation — Full Credit

- Mean scores computed using `df[items].mean(axis=1)`, which is the pandas equivalent of SPSS `MEAN()`.
- Descriptives reported for both scales.
- The choice of mean over sum scoring is consistent with the handout's recommendation.

**One technical note:** The `mean(axis=1)` call in pandas uses available-case analysis by default (i.e., if a respondent is missing one item, the mean is computed from the remaining items). This matches SPSS `MEAN()` behavior. The student does not explicitly discuss this choice, but the behavior is correct.

### 8. Final Verification — Full Credit

- Missing data checked on new scale scores (both show 0 missing, which is correct given pandas' default behavior with `mean()`).
- Boxplots generated for both scale scores.
- Summary table maps each deliverable to its location in the notebook.

### AI Use Disclosure — Adequate and Honest

The disclosure is detailed, specific, and structured around the what-I-did vs. what-Claude-did distinction. It describes the process (Socratic dialogue, concept reinforcement before drafting) rather than just listing tools. The reference to a version-controlled experiment log adds accountability. This is a model disclosure — it does not minimize AI involvement, and it makes clear the student directed the analysis rather than passively accepting output.

---

## Errors or Concerns

**No statistical errors found.** The calculations are correct, the interpretations are accurate, and the data handling decisions are defensible.

**Minor observations (not grade-affecting):**

1. The scale score computation uses available-case mean, meaning a respondent missing 1 of 8 SECT items gets a mean from 7 items rather than being dropped. This is standard and appropriate, but a brief note acknowledging this behavior would strengthen the methods discussion.

2. The notebook does not explicitly verify that reverse-coded items (`_r` suffix) were pre-coded in the dataset. The descriptive statistics are consistent with correct reverse coding (means for `_r` items are in the same direction as non-`_r` items), but a sentence confirming this check was performed would be useful.

3. The outcome variable outliers (Exam_Score = 115, Homework_Score = 150) could warrant slightly more discussion. The student flags them appropriately but does not investigate further. In a real analysis, checking whether these cases also show unusual patterns on scale items would be prudent.

---

## What Would Strengthen It

- Add a brief correlation matrix between scale items to complement the reliability analysis and connect to the multidimensionality discussion raised in the SFT interpretation.
- Explicitly confirm reverse coding was pre-applied in the data file.
- Note the available-case vs. listwise distinction in scale score computation.
- For the SFT scale, compute the average inter-item correlation to make the item-count argument more concrete (showing that inter-item r is comparable across the two scales).

These are enhancements, not deficiencies. The submission as written fully satisfies the assignment requirements.

---

## PDF Submission Readiness

**Ready for export.** The notebook has:

- Clear section headers following the handout's 8-step structure
- Readable tables (pandas DataFrames render cleanly in PDF export)
- Four sets of boxplots (SECT items, SFT items, outcomes, final scale scores)
- Professional formatting with no code-only cells lacking explanation
- Markdown interpretation cells after every analysis step
- A summary section that ties everything together

The only consideration is that `nbconvert` to PDF requires LaTeX or can be done via HTML intermediate. Either route should produce a clean document from this notebook.

---

## Summary

This is a strong submission. It covers every required step, the statistics are correct, the interpretations demonstrate genuine understanding (particularly around alpha's dependence on item count and the distinction between non-plausible values and outliers), and the AI disclosure is transparent and detailed. The use of Python instead of SPSS is a non-issue — the procedures are equivalent, and the student shows command of the underlying concepts rather than dependence on menu-driven software.

**Grade: A**
