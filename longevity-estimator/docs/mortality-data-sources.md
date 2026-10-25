# Mortality Data Sources and Provenance

## 1. Purpose

This document describes candidate public sources for baseline mortality information. It does not certify that a source, particular table, or reference year is suitable for every user or for an individualized model.

A data provider must record the exact file/table, source URL, retrieval date, data year, population definition, age coverage, variable definitions, terms/license, transformations, and checksum where possible.

## 2. Candidate official sources

### U.S. Social Security Administration (SSA)

- Actuarial Life Table: https://www.ssa.gov/oact/STATS/table4c6.html
- Downloadable actuarial data and related tables: https://www.ssa.gov/OACT/Downloadables/CY/index.html

Use only after documenting the relevant table year, population definition, column meanings, and whether it is a period or cohort/projection table. The SSA's Social Security area population definition is not identical to every possible U.S. resident population. Do not claim a table is a personal medical prognosis.

### U.S. Centers for Disease Control and Prevention / National Center for Health Statistics

- Life tables and related NCHS publications: https://www.cdc.gov/nchs/products/life_tables.htm
- NCHS data and publications: https://www.cdc.gov/nchs/

Confirm the current publication, population coverage, data years, and methodological notes before importing a table.

### World Health Organization (WHO)

- Global Health Estimates: https://www.who.int/data/global-health-estimates
- WHO data portal: https://www.who.int/data

WHO resources can support international comparison and national estimates. Confirm whether a particular table is a direct observation, adjusted estimate, modeled estimate, or projection, and record the relevant methodology.

### Other sources

Additional national statistical agencies or reputable demographic research repositories may be used when appropriate. Before use, review provenance, update cadence, population definitions, licensing, methodological transparency, and suitability for the intended prediction horizon. Do not combine tables from different populations or methodologies without justification.

## 3. Selection rules

1. Prefer a source matching the target population and geography.
2. Distinguish period life expectancy from cohort life expectancy.
3. Do not assume a local postal-code value represents a validated mortality rate.
4. Do not infer local risk from generic geographic data without evidence and validation.
5. Do not use race, ethnicity, gender identity, or other demographic answers as automatic risk penalties.
6. If regional data are unavailable, use an appropriate national table when available and disclose the limitation.
7. Do not extrapolate beyond supported age range without an explicit validated method.
8. Do not silently fill missing ages or strata with values from a different population.

## 4. Import and integrity process

For each source update:

1. Download only from a verified official source or approved archive.
2. Save the original file in an approved data store; do not overwrite without retaining version history.
3. Record retrieval date, publication/data year, URL, license/terms review, file format, schema, and checksum.
4. Parse into a documented canonical representation without changing source meaning.
5. Validate required columns, units, age ordering, probabilities, survivor counts, and expected monotonicity.
6. Compare a representative sample against the source publication.
7. Run automated validation tests and record the result.
8. Update the source manifest and relevant documentation.
9. Review whether model performance or assumptions require revalidation.

## 5. Recommended metadata schema

```yaml
id: [stable-source-id]
name: [published table name]
provider: [organization]
source_url: [official URL]
retrieved_at: [YYYY-MM-DD]
data_year: [year]
publication_date: [YYYY-MM-DD or unknown]
population: [official population definition]
geography: [country/region]
table_type: [period|cohort|projection|other]
measure_definitions: [description of qx, lx, ex, etc.]
age_range: [minimum, maximum]
stratification: [documented categories]
license_review: [approved|restricted|pending plus notes]
checksum_sha256: [hash]
transformations: [versioned processing steps]
limitations: [known limitations]
```

This is an illustrative metadata format; adapt it to the actual provider implementation. Do not invent unknown fields.

## 6. Data storage

Do not commit large, restricted, personal, or license-incompatible data files. Use `src/data/mortality/README.md` to explain where approved files are stored, how they are obtained, and how to validate them. If source data live outside Git, document a reproducible import command and the exact expected checksums/versions.

## 7. Baseline versus individualized adjustment

A life table provides population mortality information. It does not supply coefficients for every questionnaire answer. An individualized model must have its own validated training/validation evidence and demonstrate compatibility with the selected baseline. Do not use the existence of an official life table as justification for inventing risk weights.
