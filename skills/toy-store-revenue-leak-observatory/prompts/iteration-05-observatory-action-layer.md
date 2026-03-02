# Iteration 05 - Observatory and action layer

## Objective

Turn the leak diagnostics into a unified decision layer that can be consumed by downstream users without reading every mart individually.

## Read these files first

- `skills/toy-store-revenue-leak-observatory/contracts/model-registry.json`
- `skills/toy-store-revenue-leak-observatory/contracts/metric-catalog.json`
- `skills/toy-store-revenue-leak-observatory/contracts/acceptance-tests.json`

## Inputs

Use stage-3 and stage-4 diagnostic models via `{{ ref('model_name') }}`.

## What to build in this iteration

- `obs__leak_registry`
- `obs__priority_actions`
- `obs__executive_scorecard`
- `obs__leak_explainers`

## Design intent

### obs__leak_registry
One row per period, entity, and leak family, with:
- severity_score
- supporting_metrics
- confidence_note
- recommended_action
- upstream_model_refs

### obs__priority_actions
Rank actions by severity and likely value recovery.

### obs__executive_scorecard
Summarize the health of the business in a compact, decision-ready form.

### obs__leak_explainers
Provide human-readable justification for each finding.

## Explicit constraints

- Do not output opaque scores without support.
- Do not leave findings unranked.
- Do not hide uncertainty; state it.
- Preserve traceability to the supporting upstream models.

## Completion standard

This iteration is complete only when a human can look at the observatory outputs and understand what is going wrong, why it matters, and what should be done first.
