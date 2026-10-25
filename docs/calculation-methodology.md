# Calculation Methodology

## 1. Purpose and boundary

This document specifies the intended calculation pathway. It does not claim that any particular individualized model is already installed or validated. A working implementation must identify the actual mortality table and model used, with versions and provenance.

The output is a statistical estimate of survival in a population or a model-defined group. It is not an exact death prediction, diagnosis, or guarantee.

## 2. Definitions

- **Current age**: calendar age at the assessment date.
- **Baseline death probability** `q0(k)`: probability of death during interval `k`, conditional on being alive at its start, under the selected baseline table.
- **Hazard** `h(t)`: instantaneous event rate at time `t`, conditional on survival until that time.
- **Survival function** `S(t)`: probability of surviving beyond `t` years from assessment.
- **Expected remaining lifespan**: area under the survival curve, if the curve is valid over a suitable lifetime horizon.
- **Median remaining survival**: time at which survival probability reaches 0.5, if it does within the supported horizon.
- **Restricted mean survival time (RMST)**: area under the survival curve up to a stated finite horizon. RMST must not be described as unrestricted life expectancy.
- **Period life table**: applies mortality rates observed or specified for a period across future ages; it does not necessarily represent future cohort improvements.
- **Cohort/projected life table**: uses assumed/projected mortality rates relevant to a cohort as it ages.

## 3. Age calculation

Let `B` be date of birth and `D` be the assessment date/time. Calculate age using actual calendar dates. Do not calculate age solely as `assessment year - birth year`. For any decimal-age representation, document the year-length convention and timezone/date-only interpretation. The result must be deterministic for a fixed input and assessment timestamp.

## 4. Baseline table selection

Choose a source based on the model's supported population and the person's country/region and demographic fields. Record the selected table's source, version, reference year, population definition, age coverage, stratification, and period-versus-cohort status.

A table must not be assumed suitable for every country. If regional data do not exist or are not reliable, use a justified national baseline when available and state that regional answers were not used to adjust mortality. If no appropriate baseline exists, return an unavailable state rather than borrowing an unvalidated table without disclosure.

For discrete annual intervals, a life table may provide `q_x`, the probability of death between ages `x` and `x+1`, conditional on reaching age `x`. For a person already aged `a`, follow future attained ages and avoid restarting the calculation at birth. If the supplied table contains survivor counts `l_x` and an appropriate radix, survival from current age can be derived as `l_(a+t) / l_a` only when the table's definitions and ages support that operation.

## 5. Feature engineering

Only derive features required or supported by the selected model. Keep each feature's source question IDs, transformation, unit, and missing-data behavior documented.

### BMI

`BMI = weight_kg / (height_m * height_m)`

Convert imperial values to metric units before calculating. Do not calculate if either input is absent/invalid. BMI is not a direct measure of body composition and must be interpreted only as the model intends.

### Smoking pack-years

`pack_years = (average_cigarettes_per_day / 20) * years_smoked`

Use this only when average daily amount and smoking duration are known. The questionnaire as specified does not always capture the quit date/duration for former smokers; do not invent it. A model that uses current/former/never smoking status may use those categories without requiring pack-years if that is its validated design.

### Other variables

Medical conditions, severity, hospitalization, functional status, substance exposures, treatment context, sleep, activity, and other variables must follow the selected model's definitions. Never transform the whole questionnaire into an arbitrary additive score. Avoid double counting correlated features, such as a disease and a complication, unless the validated model explicitly includes both.

## 6. Individualized model: proportional hazards example

The following equations are examples for a compatible proportional-hazards model, not a universal method for every model.

Risk index:

`eta_i(t) = sum_j beta_j * x_ij(t)`

where coefficients `beta_j`, feature transformations, time handling, and baseline hazard must come from the documented fitted model.

If `q0,k` is a valid baseline probability for interval `k`, and a constant baseline hazard within that interval is an appropriate assumption:

`h0,k = -ln(1 - q0,k)`

For hazard ratio `exp(eta_i,k)`:

`q_i,k = 1 - exp(-h0,k * exp(eta_i,k))`

This conversion is valid only if the model and baseline assumptions are compatible. Do not combine coefficients with an unrelated life table simply because both are available. Some models directly provide calibrated survival probabilities and should be used through their native prediction function instead.

Coefficients must never be invented by a developer or manually assigned to create an attractive personalized number. They must be trained/estimated from suitable outcome data and validated for the intended population and horizon.

## 7. Survival curve

For a discrete annual model:

`S(0) = 1`

`S(k+1) = S(k) * (1 - q_i,k)`

The model must satisfy:

- `0 <= q_i,k <= 1`;
- `0 <= S(k) <= 1`;
- `S(k+1) <= S(k)`;
- outputs are finite numbers;
- missing required inputs do not silently become normal/low-risk values.

If the model returns a survival curve directly, validate and use the model-native curve.

## 8. Expected remaining lifespan

Where a valid survival curve extends over an adequate lifetime horizon:

`R = integral from 0 to infinity of S(t) dt`

`R` is expected remaining lifetime in years. Numerically integrate over the available time grid, using an appropriate documented method (for example, trapezoidal integration).

For a finite horizon `tau`:

`RMST(tau) = integral from 0 to tau of S(t) dt`

Report this as restricted mean survival time through `tau`. Do not extend a model beyond its supported horizon without a defensible and validated extrapolation method. A five- or ten-year model does not automatically establish full remaining life expectancy.

For an annual grid with one-year intervals, a trapezoidal approximation is:

`R_approx = sum_k ((S(k) + S(k+1)) / 2) * (t_(k+1) - t_k)`

Ensure time units are correctly represented and final intervals are handled according to the data.

## 9. Median survival and milestone probabilities

Median remaining survival is the earliest `t` for which `S(t) <= 0.5`, estimated using interpolation only if justified by the grid and model. If the curve does not cross 0.5 during the supported horizon, return “not estimable within this horizon.”

Report survival probabilities at 1, 5, 10, or 20 years only when the selected model and horizon support them. Clearly label each time point and the population/model to which the estimate applies.

## 10. Uncertainty

Display intervals only when a defensible method is available. The method could use model-provided uncertainty, validated bootstrap procedures, or another appropriate statistical approach. State whether an interval represents uncertainty in population/model parameters, prediction uncertainty, or an uncertainty range for estimated survival. Do not invent a range or call a simple scenario spread a confidence interval.

Prediction uncertainty does not mean an individual will live inside a guaranteed range. A confidence interval for a model parameter is not the same as an interval for an individual's actual lifespan.

## 11. Time-unit conversions

For expected remaining years `R`, mathematical equivalents are:

- Months: `R * 12`
- Days: `R * 365.2425`
- Hours: `R * 365.2425 * 24`
- Minutes: `R * 365.2425 * 24 * 60`
- Seconds: `R * 365.2425 * 24 * 60 * 60`

These are conversions of a statistical expected value using an average calendar year. They do not make the prediction accurate to a day or second. Do not display an exact death date or countdown.

## 12. Required result metadata

Each result should include the calculation timestamp, result type, table source/version, model version if any, population applicability, supported horizon, features actually used, important omitted features, missing-data notes, and a statement of limitations. Do not include raw personal answers in result logs.
