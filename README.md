# Colon Survival Modeling

Notebook-driven survival analysis on an open colon cancer cohort, comparing a Kaplan-Meier baseline with tuned survival models for time-to-event risk stratification.

## Problem
The notebook studies survival after a colon cancer diagnosis, with death as the event of interest and right censoring handled explicitly. The cohort in the notebook contains 929 patients and uses a 3,329-day study window so the analysis starts at diagnosis and follows patients through the observed period.

This is a clinical modeling exercise rather than a deployed system. The goal is to compare survival techniques, understand the strongest prognostic variables, and produce an interpretable risk ranking.

## Approach
The workflow in [`colon_cancer_survival_anaylsis.ipynb`](colon_cancer_survival_anaylsis.ipynb) is:

1. Load and inspect the colon cancer cohort.
2. Define the time-to-event setup and censoring rules.
3. Run a simple Kaplan-Meier / log-rank comparison by surgery status.
4. Train survival models with a train/test split.
5. Tune both a Linear Survival SVM and a Conditional Survival Forest with grid search.
6. Compare discrimination and calibration-style metrics, then derive risk groups from the predicted risk scores.

The notebook also surfaces feature importance from the survival forest and highlights the most informative variables for the fitted model.

## Outcome
The visible notebook results show:

- Kaplan-Meier log-rank test statistic `6.43` with `p = 0.01` for the surgery comparison.
- Best tuned Linear Survival SVM with `C-index = 0.63`.
- Best tuned Conditional Survival Forest with `C-index = 0.65`.
- Integrated Brier Score (`IBS`) of `0.23` for the survival forest, which the notebook treats as a strong result for this setup.
- Top feature importances led by `node4`, `nodesrange_8-14`, `nodesrange_4-7`, `surg`, and `extent`.

The notebook's interpretation is that the conditional survival forest is the stronger of the two tuned models, but this is still an exploratory notebook result, not a clinical validation claim.

## How To Explore
- Open [`colon_cancer_survival_anaylsis.ipynb`](colon_cancer_survival_anaylsis.ipynb) and run the cells in order.
- Review [`requirements.txt`](requirements.txt) for the historical environment. The notebook uses older packages such as `lifelines`, `pysurvival`, `scikit-learn`, `pandas`, and `torch`.
- Pay special attention to the sections labeled Kaplan-Meier analysis, grid search, metrics, and feature importance.

## Limitations
- The repository is notebook-first, so reproducibility depends on the notebook environment and package versions in `requirements.txt`.
- The underlying dataset is not packaged as a polished data pipeline in the repo, so path/data availability may need manual setup.
- The results are exploratory survival-model comparisons on one cohort, not a validated production or clinical decision-support model.
- Some notebook language is experimental and the hyperparameter search is expensive, especially for the conditional survival forest.
