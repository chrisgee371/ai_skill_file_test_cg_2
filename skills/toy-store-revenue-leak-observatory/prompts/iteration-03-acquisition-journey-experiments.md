# Iteration 03 - Acquisition, journey, and experiment diagnostics

## Objective

Diagnose where top-of-funnel and checkout performance is leaking value, while respecting chronology and valid comparison windows.

## Read these files first

- `datasets/maven-fuzzy-factory/profiles/page-catalog.json`
- `datasets/maven-fuzzy-factory/profiles/traffic-catalog.json`
- `datasets/maven-fuzzy-factory/profiles/chronology-summary.json`
- `skills/toy-store-revenue-leak-observatory/docs/known-quirks.md`
- `skills/toy-store-revenue-leak-observatory/contracts/metric-catalog.json`

## Inputs

Use stage-2 internal models via `{{ ref('model_name') }}`.

## What to build in this iteration

- `mart__traffic_source_day`
- `mart__landing_page_day`
- `mart__funnel_step_day`
- `mart__campaign_variant_day`
- `mart__checkout_variant_day`
- `diag__acquisition_leak`
- `diag__journey_leak`
- `diag__experiment_findings`

## Diagnostic intent

### Acquisition leak
Find channels, campaigns, or entry pages that drive sessions but underperform on:
- conversion
- bounce rate
- revenue per session
- net revenue per session

### Journey leak
Find page-path or funnel stages where the business is losing too many users before order completion.

### Experiment findings
Compare landing-page, ad-content, and billing-page variants only inside valid overlap windows.

## Explicit constraints

- Do not compare variants across the full history if the variants did not coexist.
- Treat `/billing` and `/billing-2` as a checkout variant family.
- Preserve `NULL` UTM traffic as a legitimate class.
- Make severity scores bounded and explainable.

## Completion standard

This iteration is complete only when the diagnostic layer can point to concrete top-of-funnel and journey leaks without breaking chronology.
