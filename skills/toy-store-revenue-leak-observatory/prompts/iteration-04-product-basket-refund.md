# Iteration 04 - Product, basket, refund, and launch diagnostics

## Objective

Diagnose how value leaks after the shopper gets close to or completes purchase.

## Read these files first

- `datasets/maven-fuzzy-factory/profiles/chronology-summary.json`
- `skills/toy-store-revenue-leak-observatory/contracts/metric-catalog.json`
- `skills/toy-store-revenue-leak-observatory/docs/known-quirks.md`

## Inputs

Use stage-2 and stage-3 internal models via `{{ ref('model_name') }}`.

## What to build in this iteration

- `mart__product_day`
- `mart__primary_product_cohort`
- `mart__bundle_attachment`
- `mart__refund_rate_day`
- `diag__basket_leak`
- `diag__refund_leak`
- `diag__launch_leak`

## Diagnostic intent

### Basket leak
Find products or periods where:
- average order value underperforms
- items per order are weak
- bundle attachment is poor

### Refund leak
Find products or cohorts where refunds erase too much apparent growth.

### Launch leak
Identify launch windows where a new product creates demand but damages net-value quality.

## Explicit constraints

- Keep product logic appropriate for a four-product catalog.
- Use refund-aware net value, not gross revenue alone.
- Do not create launch windows that begin before product launch timestamps.

## Completion standard

This iteration is complete only when the post-purchase diagnostics can explain how gross success and net success diverge.
