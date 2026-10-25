# Model Validation Plan

## 1. Purpose

This plan defines the evidence required before a survival model may produce an individualized estimate in Longevity Estimator. A model's availability, paper publication, high discrimination, or plausible output does not alone establish suitability for this application.

Validation must evaluate the exact implementation, feature transformations, data pipeline, baseline compatibility, population, endpoint, and prediction horizon used in production.

## 2. Required pre-validation specification

Before evaluation, freeze and document:

- Intended use and user population.
- Outcome definition (for example, all-cause mortality) and prediction origin.
- Prediction horizons.
- Inclusion and exclusion criteria.
- Required and optional predictors.
- Measurement definitions and units.
- Missing-data handling.
- Model formula, coefficients, transformations, baseline hazard, and software version.
- Primary/secondary metrics and acceptance criteria.
- Subgroups and fairness analyses.
- Dataset splits and all planned comparisons.

Do not select an acceptance threshold after inspecting the final test results without documenting the change and conducting an appropriate new evaluation.

## 3. Data requirements

The validation dataset should represent the target population and contain a suitable outcome, follow-up time, censoring indicators, predictors collected in a way that matches intended use, and enough events for stable evaluation. Record data provenance, time period, inclusion/exclusion criteria, missingness, follow-up distribution, event counts, and selection limitations.

Separate model development and validation data at the individual level. When repeated records or family/group structures exist, prevent leakage across partitions. Do not use features recorded after the prediction origin. For temporal validation, use later observations to evaluate transportability over time. For external validation, use a distinct institution, region, dataset, or population as appropriate.

## 4. Validation layers

### 4.1 Code and integration validation

- Verify parsing and feature transformations against test fixtures.
- Reproduce model outputs from a reference implementation, where available.
- Confirm units, age calculations, category mapping, and missing-data behavior.
- Ensure coefficients and preprocessing versions match the model card.
- Reject unsupported populations and horizons.
- Check probability bounds and monotonic survival curves.
- Test baseline compatibility mathematically and empirically.

### 4.2 Internal validation

Use an appropriate method such as bootstrap validation or cross-validation without leakage. Report optimism correction where relevant. Avoid relying on a single random split when event counts are limited.

### 4.3 External and temporal validation

Evaluate on a dataset not used to fit or select the model. Where the application will be used across countries or regions, show evidence for each intended scope; otherwise narrow the supported population. Examine changes in mortality patterns, treatment availability, measurement, and predictor prevalence over time.

### 4.4 Calibration

Evaluate whether predicted survival probabilities correspond to observed outcomes at each supported horizon. Use calibration plots and suitable numerical summaries, such as calibration-in-the-large and calibration slope where applicable. Explain how censoring is handled. Recalibration must be treated as a model change, versioned, and revalidated.

### 4.5 Discrimination

Use survival-appropriate metrics where applicable, such as a concordance index or time-dependent AUC. State the metric definition, censoring method, horizon, sample size, event count, and uncertainty interval. Discrimination does not establish calibration.

### 4.6 Overall prediction error

Use a suitable metric, such as a time-dependent Brier score with a documented censoring adjustment, when applicable. Compare against a meaningful baseline model rather than interpreting a score in isolation.

### 4.7 Subgroup and fairness evaluation

Where sample size supports it, evaluate calibration, discrimination, error, missingness, and applicability across relevant age, sex-related, geographic, racial/ethnic, and other subgroups. Report group sample sizes and event counts. Do not make confident claims about very small groups. Investigate disparities and define mitigation or scope restrictions. Demographic attributes must not be used as arbitrary penalties or rewards.

### 4.8 Robustness and missingness

Evaluate sensitivity to realistic missing answers, measurement error, outliers, changes in questionnaire interpretation, and data provider differences. Verify that declining optional demographic data does not cause the app to silently impute a low-risk value. Compare users with complete and incomplete inputs where appropriate.

## 5. Metrics and reporting

For each supported horizon, report:

- Number of people and number of outcome events.
- Follow-up duration and censoring summary.
- Calibration plot and suitable numerical calibration metrics.
- Discrimination metric with uncertainty interval.
- Prediction error metric where appropriate.
- Subgroup performance and sample sizes.
- Comparison against baseline and existing models where meaningful.
- Missingness and robustness results.
- Known failure modes and supported population after validation.

A model card must link to the versioned evaluation report. Metrics must not be presented without their outcome and horizon.

## 6. Acceptance gate

A designated scientific reviewer must approve intended use, model applicability, calibration, discrimination, uncertainty reporting, subgroup analysis, and limitations before the model is enabled for individualized results. Acceptance criteria should be defined before final evaluation and justified by intended use and the consequences of error; do not copy arbitrary universal thresholds.

The model must remain disabled for any population/horizon with insufficient evidence. If an individualized model fails validation, baseline-only mode can remain available if its life table is appropriate.

## 7. Post-deployment monitoring

If deployed, monitor aggregate performance only where outcomes can be obtained lawfully and reliably. Watch for calibration drift, changes in demographics or treatments, input distribution drift, missingness, software changes, and data-source updates. Do not retain identifiable questionnaire responses solely for monitoring by default. Define an incident, suspension, rollback, and revalidation procedure before activation.

## 8. Change control

Revalidation is required after changes to model coefficients, baseline data, feature definitions, missing-data strategy, outcome/horizon, source population, time integration, or material dependencies. Patch changes that affect numerical results must be assessed and documented. Keep older model versions and reports reproducible where lawful and feasible.

## 9. Validation report template

- Model ID/version:
- Validation date and reviewers:
- Intended population and horizon:
- Dataset source and period:
- Sample size/events:
- Data leakage checks:
- Calibration results:
- Discrimination results:
- Prediction error:
- Subgroup results:
- Missingness/robustness:
- Baseline comparison:
- Known limitations:
- Acceptance criteria and results:
- Decision: approved / restricted / rejected:
- Restrictions and follow-up actions:
