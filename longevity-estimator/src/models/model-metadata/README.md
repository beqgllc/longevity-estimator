# Model Metadata Registry

This directory documents versioned survival-model metadata. It must not be treated as evidence that a validated model has already been installed.

## One metadata record per model version

Create a separate JSON/YAML metadata record for each immutable model version. Keep the model card and evaluation report linked by stable IDs and versions. Do not overwrite a version after its outputs have been used; publish a new version and retain the audit trail where lawful.

Recommended fields:

- `id`: stable model identifier.
- `name`, `version`, `maintainer`.
- `sourceCitation`, `implementation`, `artifactChecksum`.
- `trainingPopulation`, `validatedPopulation`, `geographicScope`.
- `supportedAgeRange`, `supportedHorizonsYears`, `outcomeDefinition`.
- `requiredFeatures`, `optionalFeatures`, `featureDefinitionsVersion`.
- `baselineCompatibility` and `baselineSource`.
- `missingDataStrategy`.
- `validationReport`, `modelCard`, `approvalStatus`, `approvalDate`.
- `limitations`, `knownUnsupportedPopulations`, `revalidationDueDate`.

See [`docs/model-card-template.md`](../../../docs/model-card-template.md) and [`docs/model-validation.md`](../../../docs/model-validation.md).

## Activation rule

A model must remain disabled for individualized estimation unless a reviewer has confirmed its intended use, input mapping, baseline compatibility, supported population/horizon, calibration, discrimination, uncertainty handling, and external validation evidence. Metadata must describe actual evidence, not future plans.

Do not place personal data, restricted training datasets, API credentials, or private clinical records in this directory. Model coefficient/artifact files may be included only when terms permit and they can be versioned safely. Store checksums and secure artifact references when they cannot be committed.
