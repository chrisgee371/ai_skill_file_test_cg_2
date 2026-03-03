# Toy Store Revenue Leak Observatory

This bundle is a repo-ready, multi-iteration Prophecy skill package for building a Databricks-backed pipeline over the Maven Fuzzy Factory dataset.

## What is included

- `skills/toy-store-revenue-leak-observatory/` - the skill, prompts, IR, contracts, and supporting docs
- references to Databricks source and support tables under `chris_demos.demos`

## Installation

Transport format is a single zip archive.

Runtime expectation is **an unpacked skill directory on disk plus Databricks tables**. Extract this archive at repo root so that this path exists:

- `skills/toy-store-revenue-leak-observatory/`

Then make the required source and support tables available in Databricks under `chris_demos.demos`.

## Why this bundle exists

The goal is not to build a generic e-commerce dashboard. The goal is to build an explainable **Revenue Leak Observatory** that identifies where value is being lost across:

- acquisition
- session journey
- checkout
- basket structure
- refunds
- product launches

## Dataset baseline

- sessions: 472,871
- pageviews: 1,188,124
- orders: 32,313
- order items: 40,025
- refunded order items: 1,731
- products: 4
- activity window: 2012-03-19T08:04:16 to 2015-04-01T18:11:08

## Recommended read order for the agent

1. `SKILL.md`
2. `chris_demos.demos.phase_plan`
3. `chris_demos.demos.source_manifest`
4. `chris_demos.demos.table_profiles`
5. the current prompt file and current IR table

## Important packaging note

This bundle intentionally improves on the supplied example skill archive.

Improvements:
- `skills/` remains the repo-visible root for the skill files
- Databricks table references replace local dataset-path and JSON-object dependencies
- machine-readable support tables and stage IR
- data-first Databricks design instead of domain-specific dashboard prose alone
