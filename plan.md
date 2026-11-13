# Web Data Management System — Delivery Plan

## Goal

Build a web-based Data Management System (DMS). A user uploads or connects a dataset, profiles it, safely changes it through a visual workspace, validates the result, visualizes it, and publishes a versioned export or database table.

The first implementation uses Python and Pandas for bounded, interactive batch work. It must not treat Pandas as a distributed-compute engine: every job has file-size, memory, run-time, and row-count limits. Large analytical workloads move to Parquet plus DuckDB or a warehouse worker later.

## Product principles

- Raw uploads are immutable. Every change produces a new dataset version.
- A transformation is a structured, replayable recipe; never only a notebook session.
- Preview before write. Validate before publish.
- Keep rejected rows, error reasons, job logs, input/output counts, and actor identity.
- Apply least privilege, tenant isolation, encryption, retention, and PII masking from the start.
- LLMs propose plans and explain data. Deterministic code validates and executes them.

## Research retained from `Data-Analysis-Projects-With-Pandas`

The research repository is a useful Pandas learning catalogue, not production application code. Reuse its capabilities, not its notebooks directly.

| Research area | Production feature |
| --- | --- |
| Dataset exploration (`info`, `describe`, distributions, missing values) | Upload profile, schema inference, null/duplicate/outlier report |
| Cleaning and messy-database projects | trim/normalize text, parse dates, replace values, rename fields, deduplicate |
| Merging and transformation | joins, unions, column mapping, flattening, pivot/unpivot, aggregation |
| SQLite/Pandas project | staging/import to approved SQL targets; query preview |
| Many-file import project | folder/archive batch ingestion and schema-compatible append |
| EDA and Seaborn projects | reusable charts, segmentation, trend and correlation views |
| Feature engineering project | governed derived columns and ML-ready exports |
| Web/API import project | allow-listed connector framework, not unrestricted scraping |
| Time-series projects | date-based grouping, rolling metrics, period comparisons |

Do not copy notebook assumptions into the product: hard-coded paths, mutable in-memory state, unchecked external data, notebook checkpoints, and finance-specific calculation logic.

## Research retained from `KeithGalli/Pandas-Data-Science-Tasks`

This repository adds one practical pattern: take monthly sales files, clean a repeated-header/blank-row issue, create derived fields, and answer reusable business questions through aggregation and charts.

| Research pattern | Production feature |
| --- | --- |
| Enumerate and concatenate monthly CSV files | Batch-folder import with file manifest, schema compatibility checks, deterministic ordering, and append result |
| Detect blank/repeated header rows | Import validation and reject/quarantine rules; never silently discard unexplained rows |
| Numeric/date conversion | Typed parsing rules with invalid-value report, locale/time-zone settings, and user confirmation |
| Derived `Sales = quantity × unit price` | Visual calculated-field builder with decimal-safe arithmetic and lineage |
| Extract date month/hour and address dimensions | Date-part operations and governed string/regex extraction templates |
| `groupby` sales by month/city/product | KPI builder: aggregate, group, filter, rank, compare period, and export table/chart |
| Hourly purchase counts | Time-series and operational peak-analysis charts |
| Products bought together | Relationship/co-occurrence analysis, restricted to authorized and appropriately de-identified data |
| Quantity versus price dual-axis chart | Multi-metric comparison charts with clear units and accessible labels |

Production corrections: parse dates before deriving date parts; use `Decimal`/database decimal types for money, not binary floats; validate source schemas before concatenation; use an explicit order/transaction key for co-occurrence analysis rather than concatenated text; protect location and purchase data as sensitive.

## Research retained from the EDA and cleaning repositories

| Source | Adoptable method | DMS product decision |
| --- | --- | --- |
| `Anas1108/Exploratory-Data-Analysis-with-Pandas` | Question-led segmented statistics: counts, proportions, group mean/std-dev, threshold analysis | Guided EDA question templates and result tables; keep questions, filters, and denominators in the saved analysis |
| `arinskyyyy/data-cleaning` | Cleaning stages: schema trim, type normalization, duplicate handling, targeted imputation, entity standardization, outlier treatment, multi-source mapping | Versioned quality rules and a cleaning recipe library; every imputation, mapping, drop, and cap is previewed, explained, and reversible through source version retention |
| `PacktPublishing/Mastering-Exploratory-Analysis-with-pandas` | Multi-format loading, filtering, selection, date handling, merge/concatenate, grouping, and chart choice/aesthetics | Reusable import adapters, visual filter builder, join diagnostics, date operations, and accessible chart templates |
| `imarranz/essential-guide-to-pandas` | Data-quality checks, reshaping, categories, advanced merges, time-series, JSON/XML, export, and efficient query patterns | Governed recipe operations. CSV/XLSX/JSON first; XML and advanced formats after core format quality is proven. Never expose arbitrary `query`/`eval` or Python expressions to users. |
| `PacktPublishing/Hands-on-Exploratory-Data-Analysis-with-Python` | EDA sequence, descriptive statistics, grouping, correlation, time-series, hypothesis tests, regression, and model evaluation | Add an analysis workspace after quality MVP: descriptive/statistical cards first; opt-in, clearly labelled advanced analysis later. Statistical outputs need assumptions, sample size, and interpretation warnings. |

### Standard DMS methodology

1. State the business question, intended decision, dataset owner, and allowed audience.
2. Profile the raw version: schema, completeness, uniqueness, validity, distributions, anomalies, and sensitivity.
3. Define explicit quality rules and proposed cleaning operations. A global “zero nulls” target is invalid: each field needs its own null policy.
4. Preview transformations on a sample. Show changed, rejected, imputed, mapped, and outlier-flagged row counts.
5. Execute and validate the immutable output version. Retain raw data, recipe, rule results, lineage, and audit trail.
6. Explore with saved filters, dimensions, metrics, charts, and a documented denominator.
7. Publish only an approved version; schedule monitoring for schema drift, freshness, volume, and quality drift.

### Quality and analysis rules added to the product

- **Imputation:** field-specific options only: keep null, explicit `Unknown`, constant, forward/back fill, median/mode, interpolation, or reject. Record method and affected rows. Never silently fill values merely to reach zero nulls.
- **Outliers:** visualize and flag by default. Capping/winsorization needs a chosen rule, scope (global or group), owner approval, and original-value retention.
- **Schema harmonization:** map each source column to a canonical field; capture absent fields, incompatible types, and unmapped values in a reconciliation report.
- **Entity normalization:** use approved mapping tables first. Fuzzy matching is suggestion-only; require a review queue and confidence threshold.
- **Joins:** require selected keys and join type; preview unmatched/duplicated keys and cardinality before execution.
- **Derived fields:** provide typed, allow-listed formulas and date/text operations; prohibit arbitrary Python, SQL, `eval`, or raw Pandas expressions.
- **Statistical analysis:** correlations, distributions, tests, and regressions are exploratory outputs, not causal claims. Display method, sample size, missing-value treatment, confidence/significance values where applicable, and assumptions.
- **Visualizations:** include title, measure, aggregation, filters, time zone, units, and accessible labels. Never select a chart type automatically without user preview.

## Scope

### Initial supported inputs

| Format/source | Phase |
| --- | --- |
| CSV/TSV, including zipped archives | 1 |
| XLSX/XLS | 1 |
| JSON and newline-delimited JSON | 1 |
| Parquet | 2 |
| Approved PostgreSQL/MySQL/SQL Server connections | 3 |
| REST APIs, SFTP, object storage, web tables | 4, allow-listed |
| XML, fixed-width text, PDF/OCR | Study after core adoption; PDF/OCR is extraction, not normal tabular import |

### Initial transformations

- Select, rename, reorder, cast, add, remove, filter, sort, sample columns/rows.
- Parse/format dates; normalize text, booleans, currencies, units, and categories.
- Fill/drop nulls; deduplicate; replace/map values; split/combine fields.
- Join, union/append, aggregate, pivot/unpivot, calculate fields.
- Validate schema, ranges, patterns, uniqueness, required fields, allowed values, and referential keys.
- Build reusable KPI analyses: group/rank, time bucket, period comparison, top-N, co-occurrence, and multi-metric chart.
- Export CSV, XLSX, JSON, Parquet; publish to an approved SQL destination.

## Reference architecture

```text
Browser UI
  └─ API service: auth, metadata, previews, recipes, policy
       ├─ PostgreSQL: tenants, datasets, versions, recipes, audit, jobs
       ├─ Object storage: raw files, staged files, outputs, quarantines
       └─ Job queue → isolated Python workers
                         ├─ Pandas: bounded transforms/profiles
                         ├─ DuckDB/Parquet: larger local analytics
                         └─ Connector workers: SQL/API/SFTP
```

- Front end: React/TypeScript data-grid and chart UI.
- API: FastAPI/Python. JSON API; signed uploads; no file bytes through the API process.
- Workers: queue-backed, isolated containers. Per-job resource limits, cancellation, retry policy, structured logs.
- Storage: S3-compatible object storage; PostgreSQL metadata; Parquet as the analytical interchange format.
- Deployment: containers, managed database/object storage/queue, secrets manager, observability platform.

## LLM boundary

LLM use is optional assistance, never authority.

1. Give the model only approved sample rows, column metadata, data dictionary, and user instruction. Mask sensitive values first.
2. Require a typed transformation plan from a small allow-list: operation, target columns, parameters, expected effect.
3. Validate plan against schema, policy, permissions, and cost limits.
4. Run against a sample; show preview, changed-row count, and warnings.
5. User confirms. Worker executes the same validated recipe and records it.

LLM features: plain-language transform builder, data-quality explanations, chart suggestions, formula drafting, documentation, and semantic column mapping. Do not give it shell access, arbitrary Python execution, database credentials, or unfiltered customer data.

## Phased delivery

### Phase 0 — Product and platform decisions

**Outcome:** a buildable, secure baseline.

- Define users: analyst, data steward, administrator, viewer.
- Confirm tenant model, data classification, residency, retention, deletion, export approval, and audit requirements.
- Set hard limits for MVP: upload size, rows, columns, execution time, concurrency, retention.
- Write canonical metadata schema: dataset, source, version, schema, profile, recipe, validation run, job, export, lineage event.
- Choose cloud/on-prem target and identity provider.
- Create threat model for uploads, connectors, cross-tenant access, and prompt/data leakage.

**Exit gate:** approved requirements, limits, architecture decision record, and test data with no production PII.

### Phase 1 — Secure ingestion and exploration MVP

**Outcome:** user uploads CSV/XLSX/JSON and receives a safe, useful profile.

- Authentication, tenant/workspace roles, audit events.
- Direct-to-object-store resumable upload; file signature/type checks; archive-bomb and malware scanning.
- Encoding/delimiter/sheet selection; chunked inspection; schema inference with user overrides.
- Profile: dimensions, types, nulls, distinct counts, duplicates, min/max, samples, distributions, PII detection candidates.
- Dataset version screen, data-grid preview, download original, delete/retention workflow.
- Job states: queued, running, succeeded, failed, cancelled; logs and clear errors.

**Exit gate:** a user can upload an allowed file, inspect it, and safely retrieve the exact raw version. Unit, integration, access-control, and malicious-file tests pass.

### Phase 2 — Visual transformation and quality MVP

**Outcome:** user creates a reproducible cleaned dataset without code.

- Implement the initial transformation allow-list above as recipe operations.
- Each operation runs on a preview sample first; show before/after schema, changed rows, warnings, and estimated job cost.
- Save drafts; replay recipe against raw/source version; create immutable output version.
- Quality rules and quarantine output. Block publish when required rules fail.
- Export CSV/XLSX/JSON/Parquet with column-level permission checks.
- Visualizations: missingness, distribution, top categories, trend, scatter, bar, line, histogram.

**Exit gate:** replaying a recipe yields the same output for the same input and environment. Quality failures are explainable and recoverable.

### Phase 3 — Database and operational workflow

**Outcome:** governed data exchange with company systems.

- Read-only database discovery and import via secrets-managed, allow-listed connections.
- SQL write/publish flow: staging table, validation, approval, atomic promotion/rollback plan.
- Dataset catalog, search, tags, owner, descriptions, data dictionary, lineage graph.
- Scheduled source refreshes, notifications, approvals, run history, retention enforcement.
- Bulk multi-file ingestion with schema compatibility checks and reject report.

**Exit gate:** scheduled import, quality validation, approval, and publish are auditable end-to-end.

### Phase 4 — Assisted analysis and approved connectors

**Outcome:** faster analyst work with controlled intelligence.

- Add LLM typed-plan workflow and semantic mapping, with redaction and approval controls.
- Add REST/SFTP/object-storage connectors; each connector gets credential vaulting, rate limits, allow-list, retries, and provenance.
- Add saved dashboards, chart export, report delivery, and alerts for freshness/quality drift.
- Measure model suggestion acceptance, failed validations, data exposure events, and transformation latency.

**Exit gate:** model cannot execute an operation outside the allow-list or see data outside approved policy.

### Phase 5 — Scale and enterprise hardening

**Outcome:** predictable operation beyond Pandas limits.

- Partitioned Parquet storage, DuckDB execution, caching, incremental processing, and dataset-size routing.
- Route big/distributed work to warehouse/Spark/Dask only when evidence requires it.
- Autoscaling workers, quotas, backpressure, cost attribution, disaster recovery, restore exercises.
- SSO/SCIM, advanced RBAC/ABAC, customer-managed keys if required, formal compliance controls.
- Load, chaos, penetration, backup/restore, and tenant-isolation tests.

**Exit gate:** published SLOs met under target load; recovery and security controls verified.

## Build order inside each phase

1. Define user story, acceptance criteria, data policy, and failure behavior.
2. Add API contract and metadata migration.
3. Build worker operation plus deterministic tests.
4. Build UI and preview flow.
5. Add observability, authorization, audit event, and documentation.
6. Test normal, malformed, oversized, unauthorized, cancelled, and retry cases.

## Success measures

- Upload-to-profile success rate and median duration.
- Transform preview and full-run duration; failure/cancellation rate.
- Reproducibility: recipe replay hash/count agreement.
- Quality-rule failure rate and time to resolve.
- Active users, datasets published, and LLM-suggestion acceptance rate.
- Cross-tenant authorization failures: zero tolerated.

## Explicit non-goals for the MVP

- Arbitrary user Python, SQL, shell, or notebook execution.
- Live collaborative spreadsheet editing.
- Unlimited file sizes or distributed compute.
- PDF/OCR extraction, unrestricted web scraping, and automatic production writes.
- Autonomous LLM changes or irreversible transformations.

## First implementation backlog

1. Repository skeleton, CI, environment configuration, auth, PostgreSQL metadata schema.
2. Object-store upload and secure file-inspection worker.
3. CSV/XLSX/JSON parser and profile endpoint/UI.
4. Dataset version/data-grid UI.
5. Recipe model and five operations: rename, cast, filter, fill nulls, deduplicate.
6. Preview/run job engine, audit events, CSV/Parquet export.
7. Quality rules, charts, remaining Phase 2 operations.

