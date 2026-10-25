# Questionnaire Specification

## 1. Purpose and implementation rules

This is the canonical specification for the Longevity Estimator's 38 core questions. Preserve question wording exactly in the rendered UI. Internal IDs (`Q01`–`Q38`) must be stable. Medical follow-ups are conditional and do not change the count of core questions.

The questionnaire collects sensitive information. Explain purpose, make nonessential items optional, allow `Not sure` / `Unknown` and `Prefer not to answer` where applicable, and never convert missing or declined answers into `No` or a healthy default. Use accessible labels and validation messages. The questionnaire does not itself establish a person's medical prognosis.

## 2. Section A — Demographics and geographic context

### Q01
**Exact question:** What is your date of birth?

- Input: date picker.
- Validation: reject future dates; calculate age using calendar dates.
- Purpose: establishes current age at assessment.

### Q02
**Exact question:** What country do you currently live in?

- Input: searchable country selector.
- Purpose: selects a relevant national mortality baseline when supported.

### Q03
**Exact question:** What state, province, or region do you live in?

- Input: region selector or text field.
- Purpose: regional context only where appropriate data exist.

### Q04
**Exact question:** What is your approximate postal code or geographic area?

- Input: optional postal code/approximate area field.
- Purpose: potentially relevant local environmental and socioeconomic context.
- Privacy: do not require a precise address; record if the value is actually used by a model.

### Q05
**Exact question:** What sex-related category does the chosen medical model require?

- Input: only categories supported by the selected model, plus appropriate unknown/decline options.
- Purpose: use a matching baseline/model when justified.
- Rule: never silently force unsupported classification or add an arbitrary penalty.

### Q06
**Exact question:** What is your gender identity?

- Input: optional, inclusive response choices, self-description, and Prefer not to answer.
- Purpose: relevant healthcare-access or social context where justified.
- Rule: identity is not itself a diagnosis and must not receive an arbitrary mortality penalty.

### Q07
**Exact question:** How do you describe your race or ethnicity? (Optional)

- Input: optional selections, self-description, Prefer not to answer.
- Purpose: potential population-disparity analysis/model calibration.
- Rule: no automatic demographic penalty/bonus; use only with an ethically justified, validated method.

### Q08
**Exact question:** In what country and region were you born?

- Input: country and optional region.
- Purpose: early-life/geographic context if a validated feature supports it.

### Q09
**Exact question:** How long have you lived in your current region?

- Input: duration and units.
- Purpose: residence duration where supported by evidence.

### Q10
**Exact question:** Do you live in an urban, suburban, rural, or remote area?

- Input: Urban; Suburban; Rural; Remote; Not sure; Prefer not to answer.
- Purpose: environmental/healthcare-access context.

## 3. Section B — Family history

### Q11
**Exact question:** How old are your biological parents, if living?

- Input: separate records for each biological parent: living, deceased, unknown; ask current age only if living; optionally record age at death if deceased if supported by product scope.
- Purpose: available family longevity context.
- Rule: a living parent's present age is not their eventual lifespan. Do not use family age as a direct predictor without model support.

## 4. Section C — Medical history

### Q12
**Exact question:** Have you ever been diagnosed with a chronic or life-threatening medical condition?

- Input: Yes; No; Not sure; Prefer not to answer.
- When Yes: display a multi-select checklist with these exact categories and descriptions.

1. **Cardiovascular** — Heart disease, heart failure, arrhythmia, previous heart attack, vascular disease
2. **Cerebrovascular** — Previous stroke, transient ischemic attack, vascular complications
3. **Blood pressure** — Hypertension, typical readings, treatment and control
4. **Metabolic** — Type 1 or type 2 diabetes, prediabetes, blood sugar control
5. **Cancer** — Type, stage, diagnosis date, treatment, remission or recurrence
6. **Respiratory** — Asthma, COPD, emphysema, pulmonary disease, severity
7. **Kidney** — Chronic kidney disease, stage, kidney-function measurements
8. **Liver and digestive** — Chronic liver disease, cirrhosis, inflammatory bowel disease, other significant disorders
9. **Neurological** — Dementia, Parkinson's disease, seizure disorders, other neurological disease
10. **Mental health** — Depression, bipolar disorder, anxiety disorders, PTSD, psychotic disorders, other diagnoses
11. **Immune and inflammatory** — Autoimmune diseases, chronic inflammatory diseases, immune deficiencies
12. **Infectious** — Chronic infections with medically relevant long-term effects
13. **Musculoskeletal** — Osteoporosis, recurrent fractures, severe mobility-limiting disorders
14. **Sleep-related** — Diagnosed sleep apnea and other significant sleep disorders
15. **Other** — Any additional condition expected to influence long-term health or mortality

For each condition selected, display these exact conditional questions:

- **Have you been hospitalized for it?**
- **Are you currently receiving treatment?**

Answers: Yes; No; Not sure; Prefer not to answer.

Collect optional model-relevant details where applicable (for example, diagnosis date, severity, blood pressure/control, diabetes control, cancer stage/status, or kidney-function measurements). Do not require unavailable medical records. Distinguish known from unknown, diagnosis from concern, and stable disease from complications where model-supported. Do not infer prognosis from diagnosis alone or double-count correlated conditions.

## 5. Section D — Physical measurements

### Q13
**Exact question:** What is your current height?

- Input: positive numeric value; metric/imperial toggle.
- Purpose: BMI where both height and weight are available.

### Q14
**Exact question:** What is your current weight?

- Input: positive numeric value; metric/imperial toggle.
- Purpose: body-size features where supported.

### Q15
**Exact question:** Has your weight changed substantially in the last year?

- Input: Yes; No; Not sure; Prefer not to answer.
- Conditional optional details: direction, approximate magnitude, intentional/unintentional.

## 6. Section E — Education, work, and housing

### Q16
**Exact question:** What is your highest completed level of education?

- Input: configurable education-level selector.
- Purpose: contextual data only when supported by an ethically justified model.

### Q17
**Exact question:** What is your current occupation or principal source of work?

- Input: text or structured occupation/work status.
- Purpose: relevant occupational/socioeconomic context.

### Q18
**Exact question:** How long have you worked in that occupation?

- Input: duration and units.
- Purpose: occupational exposure context if supported.

### Q19
**Exact question:** Do you have stable housing?

- Input: Yes; No; Sometimes or uncertain; Prefer not to answer.
- Purpose: housing stability as relevant social context.

## 7. Section F — Transportation and safety

### Q20
**Exact question:** How frequently do you drive, ride a motorcycle, cycle, or use other forms of transportation?

- Input: applicable transport modes and frequency.
- Purpose: describes transport exposure.

### Q21
**Exact question:** Do you routinely use seat belts, helmets, and other appropriate protective equipment?

- Input: Always; Usually; Sometimes; Never; Not applicable; Prefer not to answer.
- Purpose: protective behavior relevant to applicable activities.

### Q22
**Exact question:** Do you drive when sleepy or under the influence of alcohol or other substances?

- Input: Never; Rarely; Sometimes; Frequently; Not applicable; Prefer not to answer.
- Purpose: relevant safety exposure.

## 8. Section G — Function, sleep, and activity

### Q23
**Exact question:** Can you independently bathe, dress, eat, and use the bathroom?

- Input: Yes, independently; I need help with some activities; I need help with most or all activities; Not sure; Prefer not to answer.
- Purpose: functional independence.

### Q24
**Exact question:** How many hours do you sleep on an average night?

- Input: numeric hours and unknown option.
- Purpose: habitual sleep duration.

### Q25
**Exact question:** How many hours per day do you spend sitting or being otherwise sedentary?

- Input: numeric value from 0 to 24, plus unknown.
- Purpose: reported sedentary time.

### Q26
**Exact question:** How many days per week do you exercise?

- Input: integer from 0 to 7, plus unknown.
- Purpose: exercise frequency; does not measure duration or intensity.

## 9. Section H — Hydration and meals

### Q27
**Exact question:** Approximately how much water and other nonalcoholic fluid do you consume daily?

- Input: amount/unit, plus unknown.
- Purpose: reported fluid intake; do not assume one universal target or direct lifespan effect.

### Q28
**Exact question:** How many meals do you typically eat per day?

- Input: numeric value and unknown option.
- Purpose: eating-frequency context; do not assume meal count directly determines lifespan.

## 10. Section I — Drugs and substance exposure

### Q29
**Exact question:** Do use drugs?

- Preserve the exact wording, including its grammar.
- Input choices: Currently; In the past, but not currently; Never; Not sure; Prefer not to answer.

### Q30
**Exact question:** Which substances have you used, and how frequently?

- Input: conditional multi-select substance list, with frequency and optional duration where known.
- Purpose: distinguish substances and exposure patterns.

### Q31
**Exact question:** Have you used prescription medication other than directed?

- Input: Yes; No; Not sure; Prefer not to answer.

### Q32
**Exact question:** Have you ever injected drugs, or had another substance-related exposure that created an infectious or other medical risk?

- Input: Yes; No; Not sure; Prefer not to answer.

Do not collapse all substances into one generic risk score or assume exposure means a disease is present.

## 11. Section J — Alcohol

### Q33
**Exact question:** Do you currently consume alcohol?

- Input: Yes; No; Prefer not to answer.
- Purpose: current status; do not infer quantity or frequency.

## 12. Section K — Tobacco

### Q34
**Exact question:** Have you ever smoked cigarettes?

- Input: Yes; No; Not sure; Prefer not to answer.

### Q35
**Exact question:** Do you currently smoke cigarettes?

- Input: Yes; No; Prefer not to answer.
- Display relevant follow-ups when applicable.

### Q36
**Exact question:** At what age did you start smoking?

- Input: numeric age; display when smoking history is reported.
- Validation: must not be greater than current age; allow unknown.

### Q37
**Exact question:** Approximately how many cigarettes do you smoke per day?

- Input: numeric cigarettes/day; distinguish current non-smoking from unknown exposure.

Pack-years may be calculated as `(cigarettes per day / 20) × years smoked` only when duration is known. Do not invent cessation dates or smoking duration for former smokers.

## 13. Section L — Prescription medications

### Q38
**Exact question:** What prescription medications are you currently taking?

- Input: optional repeatable list of medication name and dosage/frequency if known.
- Purpose: treatment context only as supported by a validated model.
- Rule: do not assign a generic mortality penalty based on medication count.

## 14. Workflow requirements

- Multi-step responsive form with progress indicator, Back/Continue, review, submit, and reset.
- Preserve answers when navigating backward.
- Show condition-specific follow-ups only for selected conditions.
- Show drug details and smoking follow-ups only when relevant.
- Keep all nonessential fields optional.
- Validate on client and trusted calculation boundary.
- Do not store answers by default.
- Ensure all 38 core questions are present exactly once in the registry and review screen.

## 15. Explicit non-goals

The questionnaire alone does not supply validated coefficients. Do not compute an arbitrary point score, claim that every answer adjusts mortality, predict an exact death date, or imply that demographic identity causes an individual outcome. Model-specific input mappings belong in versioned model metadata.
