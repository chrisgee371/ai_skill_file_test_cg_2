# Toy Store Revenue Leak Observatory

This bundle is a repo-ready, multi-iteration Prophecy skill package for building a DuckDB-backed pipeline over the supplied Maven Fuzzy Factory dataset.

## What is included

- `skills/toy-store-revenue-leak-observatory/` - the skill, prompts, IR, contracts, and supporting docs
- `datasets/maven-fuzzy-factory/raw/` - the extracted raw CSV files, included uncompressed
- `datasets/maven-fuzzy-factory/profiles/` - machine-readable source profiles and chronology metadata
- `datasets/maven-fuzzy-factory/manifests/` - dataset summary and checksums

## Installation

Transport format is a single zip archive.

Runtime expectation is **unpacked directories on disk**. Extract this archive at repo root so that these two paths exist:

- `skills/toy-store-revenue-leak-observatory/`
- `datasets/maven-fuzzy-factory/`

If your agent can unzip files itself, you may commit the archive into the repo and have the agent extract it. The skill itself is intended to run from the unpacked filesystem layout above.

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
2. `phase-plan.json`
3. `contracts/source-manifest.json`
4. `datasets/maven-fuzzy-factory/profiles/table-profiles.json`
5. the prompt and IR file for the current iteration

## Important packaging note

This bundle intentionally improves on the supplied example skill archive.

Improvements:
- repo-root extractable pathing
- no nested compression for data
- no `__MACOSX` or `.DS_Store` clutter
- machine-readable contracts and stage IR
- data-first DuckDB design instead of domain-specific dashboard prose alone
