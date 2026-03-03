---
name: toy-store-revenue-leak-observatory
description: Multi-iteration Prophecy pipeline build for the Maven Fuzzy Factory dataset. Use when building Databricks SQL models, funnel diagnostics, landing-page experiments, refund-aware revenue analysis, or a staged observatory over Databricks source tables.
argument-hint: [iteration-number or task description]
---

# Toy Store Revenue Leak Observatory Skill

You are building a Prophecy pipeline in multiple stages over Databricks-backed source tables.

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

1. **Databricks only**
   - Use Databricks-compatible SQL patterns only.
   - Do not emit Spark, T-SQL, BigQuery, or warehouse-specific syntax that is not also valid for Databricks SQL in this project.
   - This project should target Databricks SQL models.

2. **Read Databricks support tables and local docs before reasoning from memory**
   - Read `chris_demos.demos.phase_plan`, the current stage IR table, `chris_demos.demos.source_manifest`, and the profile tables before generating code.
   - When structured resources answer the question, trust them over memory.

3. **No silent assumptions**
   - Do not invent columns, tables, time windows, joins, or business logic.
   - If an ambiguity remains after reading the supplied resources, ask an explicit question instead of guessing.

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

1. Read `chris_demos.demos.phase_plan`.
2. Read the current iteration prompt in `prompts/`.
3. Read the current stage IR table in Databricks.
4. Re-read any previous stage outputs and support tables referenced by the current prompt.
5. List the models to be created, including grain and upstream dependencies.
6. Generate the models using Databricks-safe SQL.
7. Validate against `chris_demos.demos.acceptance_tests`.
8. Report what was created, what upstream refs were used, and which quality gates were satisfied.

## Required source tables

The source tables are expected in Databricks under:

- `chris_demos.demos.website_sessions`
- `chris_demos.demos.website_pageviews`
- `chris_demos.demos.orders`
- `chris_demos.demos.order_items`
- `chris_demos.demos.order_item_refunds`
- `chris_demos.demos.products`
- `chris_demos.demos.maven_fuzzy_factory_data_dictionary`

## Read these support tables and docs as needed

- `chris_demos.demos.source_manifest`
- `chris_demos.demos.model_registry`
- `chris_demos.demos.metric_catalog`
- `chris_demos.demos.join_contracts`
- `chris_demos.demos.acceptance_tests`
- `docs/known-quirks.md`
- `docs/page-taxonomy.md`
- `docs/traffic-taxonomy.md`
- profile tables such as `chris_demos.demos.table_profiles`, `chris_demos.demos.key_integrity`, `chris_demos.demos.page_catalog`, `chris_demos.demos.traffic_catalog`, and `chris_demos.demos.chronology_summary`

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
