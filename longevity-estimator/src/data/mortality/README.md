# Mortality Data Directory

This directory is reserved for approved, versioned mortality tables or reproducible import metadata. No dataset should be considered installed simply because this README exists.

## Before adding data

1. Select a source matching the intended population and calculation.
2. Verify the original publication, table type, population definition, period/cohort assumptions, age range, categories, and units.
3. Review source terms and licensing; record the outcome.
4. Preserve the original source file or a secure reference where permitted.
5. Record retrieval date, data year, source URL, transformations, and SHA-256 checksum.
6. Add integrity tests for age coverage, numeric types, probabilities, survivor counts, monotonicity, and expected values.
7. Compare parsed values against a sample of the original source.
8. Update `docs/mortality-data-sources.md` and the model/baseline metadata.

## Suggested layout

```text
src/data/mortality/
  README.md
  manifest.json          # approved source metadata, if implemented
  official/              # only if license/size/terms permit
  processed/             # reproducible normalized tables
  fixtures/              # synthetic test fixtures only; never real personal records
```

Do not commit restricted, personally identifiable, or oversized data. If a data file must be obtained during setup, document a reproducible command and verify its checksum before use. Avoid downloading changing “latest” URLs during each production prediction; pin the approved data version.

## Required metadata

At minimum: stable source ID, provider, source URL, retrieval date, publication/data year, population definition, table type, age range, strata/categories, units, license review, checksum, transformation version, and known limitations.

A baseline life table is not an individualized clinical model and does not justify invented coefficients for questionnaire answers.
