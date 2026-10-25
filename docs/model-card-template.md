# Model Card: [Model Name]

> Copy this file for each model version. Replace every bracketed placeholder. Do not enable a model for production until required sections are completed and reviewed.

## 1. Model details

- **Model name:** [Name]
- **Model ID:** [Stable identifier]
- **Version:** [Semantic or immutable version]
- **Owner/maintainer:** [Team or responsible organization]
- **Date created:** [YYYY-MM-DD]
- **Last reviewed:** [YYYY-MM-DD]
- **Model type:** [e.g., Cox proportional hazards, parametric survival model, competing-risk model]
- **Source/references:** [Peer-reviewed publication, technical report, repository, DOI/URL]
- **License/usage restrictions:** [Terms and review status]
- **Implementation checksum or artifact version:** [Value]

## 2. Intended use

- **Primary intended use:** [Describe supported output and user context]
- **Target population:** [Population definition]
- **Supported age range:** [Minimum–maximum]
- **Geographic scope:** [Countries/regions]
- **Outcome:** [All-cause mortality, cause-specific mortality, or other precise endpoint]
- **Prediction origin:** [Time point from which follow-up starts]
- **Supported prediction horizons:** [Years/time points]
- **Permitted uses:** [List]
- **Uses explicitly not supported:** [List]

## 3. Model inputs

| Feature | Definition and units | Source question(s) or dataset | Required? | Missing-data strategy | Transformation/version |
|---|---|---|---|---|---|
| [Feature] | [Definition] | [Source] | [Yes/No] | [Method] | [Method] |

List all model inputs, including baseline variables, derived features, interactions, time-dependent features, and any external data. Explain how questionnaire answers map to the original fitted variables.

## 4. Training data

- **Dataset name/source:** [Name and citation]
- **Data collection period:** [Dates]
- **Population and recruitment:** [Description]
- **Sample size:** [N]
- **Outcome events:** [N and definition]
- **Follow-up duration:** [Summary]
- **Censoring and competing events:** [Treatment]
- **Inclusion/exclusion criteria:** [Criteria]
- **Missingness:** [Extent and handling]
- **Known representativeness limitations:** [Details]
- **Data access/license approval:** [Details]

Do not publish private or restricted training data in the repository.

## 5. Methodology

- **Model equation or method:** [Exact formulation]
- **Baseline hazard/table:** [Source and compatibility]
- **Feature selection:** [Method]
- **Fitting procedure:** [Method and software version]
- **Regularization/hyperparameters:** [Values/method]
- **Calibration procedure:** [Method]
- **Survival-function generation:** [Method]
- **Extrapolation:** [None or fully specified justified method]
- **Uncertainty method:** [Method or unavailable]
- **Reproducibility details:** [Seed, environment, package versions]

## 6. Validation and performance

- **Internal validation:** [Design]
- **External validation:** [Dataset/population and date]
- **Temporal validation:** [Method]
- **Discrimination:** [Metric, horizon, estimate, confidence interval]
- **Calibration:** [Metric, horizon, plots/tables]
- **Overall prediction error:** [Brier or other appropriate score]
- **Subgroup evaluation:** [Groups, sample/event counts, findings]
- **Missing-data robustness:** [Findings]
- **Prospective evaluation:** [If applicable]
- **Acceptance decision and approver:** [Record]

Report uncertainty and event counts. Do not report a metric without defining its population, outcome, and time horizon.

## 7. Applicability and known limitations

- **Known unsupported populations:** [List]
- **Input conditions that prevent prediction:** [List]
- **Known calibration drift risks:** [List]
- **Potential measurement error:** [List]
- **Causal limitations:** Predictions do not establish causation or guaranteed benefit from changing a feature.
- **Other limitations:** [List]

## 8. Fairness and subgroup analysis

Document the rationale for demographic features, subgroup calibration and discrimination, sample sizes, identified disparities, mitigation, and residual risks. Do not interpret race, ethnicity, gender identity, education, or geography as biological or causal explanations without specific evidence. Explain whether any group-specific models or thresholds are used and why.

## 9. Ethical and privacy considerations

- Data sensitivity and access controls: [Description]
- Privacy review: [Date/reviewer]
- Potential user harms: [Description]
- User-facing caveats: [Copy]
- Human review/escalation: [Where needed]
- Monitoring and incident plan: [Details]

## 10. Monitoring and change control

- Recalibration/revalidation schedule: [Schedule]
- Drift indicators: [Metrics]
- Trigger for suspension: [Criteria]
- Model-update approval: [Role/process]
- Rollback procedure: [Procedure]

## 11. Approval record

| Reviewer | Area | Decision | Date | Evidence/reference |
|---|---|---|---|---|
| [Name/role] | [Scientific/privacy/security] | [Approve/Reject/Conditions] | [Date] | [Link] |

## 12. User-facing summary

[Write a plain-language explanation of what the model estimates, for whom it has been validated, what it cannot predict, and what data and horizon it uses.]
