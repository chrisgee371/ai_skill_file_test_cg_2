---
name: toy-store-revenue-leak-observatory
description: Multi-iteration Prophecy pipeline build for the Maven Fuzzy Factory dataset. Use when building DuckDB-only SQL models, funnel diagnostics, landing-page experiments, refund-aware revenue analysis, or a staged observatory over local CSV sources.
argument-hint: [iteration-number or task description]
---

# Toy Store Revenue Leak Observatory Skill

You are building a Prophecy pipeline in multiple stages over a local DuckDB-friendly CSV dataset.

## Mission

Build an explainable **Revenue Leak Observatory** over the Maven Fuzzy Factory data. The observatory should identify where commercial value is leaking out of the system across the full path from traffic to refund.

Leak families:
- acquisition leak
- journey leak
- basket leak
- refund leak
- launch leak

The outcome should be a stable, lineage-safe pipeline, not a one-off dashboard or a giant denormalized query.

## Non-negotiable rules

1. **DuckDB only**
   - Use DuckDB-compatible SQL patterns only.
   - Do not emit Spark, Databricks, T-SQL, BigQuery, or warehouse-specific syntax unless it is also valid in DuckDB.
   - This project is not a Spark project.

2. **Read from disk before reasoning from memory**
   - Read `phase-plan.json`, the current stage IR JSON, `contracts/source-manifest.json`, and the dataset profile files before generating code.
   - When on-disk resources answer the question, trust them over memory.

3. **No silent assumptions**
   - Do not invent columns, tables, time windows, joins, or business logic.
   - If an ambiguity remains after reading the local resources, ask an explicit question instead of guessing.

4. **Stage discipline**
   - Review all previous phases before building the next phase.
   - Do not skip ahead.
   - Do not rebuild previous phases unless they are contract-breaking and must be corrected.

5. **Lineage rule for staged builds**
   - If a new phase uses any objects as inputs that are outputs of previous phases in the same pipeline, the SQL model must reference those upstream models using:
     `{{ ref('model_name') }}`
     rather than
     `{{ source() }}`
   - This rule exists to preserve dbt-style model dependencies and to prevent duplicate disconnected DAG fragments.

6. **No direct gem reuse across iterations**
   - Do not reference prior canvas gems directly when the intent is to continue the same pipeline.
   - Reference the underlying generated SQL models instead with `{{ ref('model_name') }}`.

7. **Keep the idea original**
   - Do not collapse this into a generic marketing dashboard.
   - Build the leak taxonomy, experiment-aware diagnostics, and final action layer as defined in the skill docs.

## Build algorithm

For every iteration:

1. Read `phase-plan.json`.
2. Read the current iteration prompt in `prompts/`.
3. Read the current stage IR in `ir/`.
4. Re-read any previous stage outputs and contracts referenced by the current prompt.
5. List the models to be created, including grain and upstream dependencies.
6. Generate the models using DuckDB-safe SQL.
7. Validate against `contracts/acceptance-tests.json`.
8. Report what was created, what upstream refs were used, and which quality gates were satisfied.

## Required source files

The local dataset is already included under:

- `datasets/maven-fuzzy-factory/raw/website_sessions.csv`
- `datasets/maven-fuzzy-factory/raw/website_pageviews.csv`
- `datasets/maven-fuzzy-factory/raw/orders.csv`
- `datasets/maven-fuzzy-factory/raw/order_items.csv`
- `datasets/maven-fuzzy-factory/raw/order_item_refunds.csv`
- `datasets/maven-fuzzy-factory/raw/products.csv`
- `datasets/maven-fuzzy-factory/raw/maven_fuzzy_factory_data_dictionary.csv`

## Read these support files as needed

- `contracts/source-manifest.json`
- `contracts/model-registry.json`
- `contracts/metric-catalog.json`
- `contracts/join-contracts.json`
- `contracts/acceptance-tests.json`
- `docs/known-quirks.md`
- `docs/page-taxonomy.md`
- `docs/traffic-taxonomy.md`
- dataset profile JSON files under `datasets/maven-fuzzy-factory/profiles/`

## Response style

When you generate a stage:
- state the stage objective
- list the models you are creating
- state the upstream models and refs used
- call out any constraints or chronology caveats
- confirm which acceptance tests you are satisfying

## What “good” looks like

A good build:
- is faithful to the real supplied schema
- is decomposed into safe stages
- preserves lineage with `{{ ref('model_name') }}`
- produces diagnostics that explain where value is leaking
- ends with a unified observatory and ranked action layer
