# Iteration 01 - Source intake and profiling

## Objective

Create the source-entry layer for the supplied local CSV files and verify that the real schema matches the provided manifests.

## Read these files first

- `datasets/maven-fuzzy-factory/profiles/table-profiles.json`
- `datasets/maven-fuzzy-factory/profiles/key-integrity.json`
- `skills/toy-store-revenue-leak-observatory/contracts/source-manifest.json`
- `skills/toy-store-revenue-leak-observatory/contracts/acceptance-tests.json`

## What to build in this iteration

Create exactly these source models:

- `src__website_sessions`
- `src__website_pageviews`
- `src__orders`
- `src__order_items`
- `src__order_item_refunds`
- `src__products`

Do not create staging, marts, or diagnostic layers yet.

## Required behavior

- Map each raw file cleanly into a source model.
- Preserve all source columns unless there is a documented reason to drop or rename something.
- Use safe typing for timestamps, numeric values, and identifiers.
- Confirm row counts and primary keys.
- Document any mismatch between the manifest and the discovered file structure.

## Explicit constraints

- Do not guess columns.
- Do not infer new business fields yet.
- Do not create a data mart.
- Do not skip quality checks because the source files “look clean”.

## Completion standard

This iteration is complete only when the source layer matches the supplied files exactly and the source-level acceptance tests can be satisfied.
