# Geographic Context Data

This directory is reserved for approved, coarse geographic context datasets. Geographic answers should not be used to produce a local mortality penalty unless a validated source and method support that specific use.

## Privacy-first rules

- Prefer country or broad region when adequate; do not request precise GPS or a street address by default.
- Avoid storing a postal code after the model has converted it to a necessary coarse region, unless retention is justified and disclosed.
- Do not combine location with sensitive answers in logs or analytics.
- Do not infer a person's race, income, health status, or other sensitive attribute from geography.
- Do not describe ecological/local associations as an individual's causal risk.
- If the required regional dataset is unavailable, disclose that the geographic answer was not used for adjustment.

## Dataset acceptance criteria

For each candidate file, document the provider, URL, data year, geographic granularity, coverage, variable definitions, license/terms, update schedule, known gaps, transformations, checksum, and reason it is relevant to the intended model. Review sample sizes, stability, and whether the data can legally and responsibly be used for this purpose.

## Suggested layout

```text
src/data/geographic/
  README.md
  manifest.json       # only if the application implements a source manifest
  processed/          # approved normalized aggregate data
  fixtures/           # synthetic test data only
```

Do not place exact user addresses, individual location histories, private geolocation exports, or other personal data in this repository. Geographic context is optional and should be skipped if it does not materially improve a validated calculation.
