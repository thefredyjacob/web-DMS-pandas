# DMS Free Plan — Online Users

## Executive summary

Offer a self-service, web-based data workspace for individuals who need to inspect, clean, transform, analyze, visualize, and export small datasets. The free plan helps users solve a complete first task in the browser, then provides a clear path to paid capacity or team governance when their needs grow.

## Target users and need

- Students, independent analysts, researchers, small business owners, and occasional data users.
- Users working with CSV, Excel, or JSON who need practical work without writing Pandas code.
- Core need: quickly understand a file, fix common issues, make a repeatable transformation, and download a useful result.

## Product promise

“Understand and prepare a dataset in minutes, in a visual workspace.”

## Free product scope

- Browser-based account and personal workspace.
- Upload CSV/TSV, Excel, and JSON; preview sheets and basic schema.
- Basic data profile: row/column counts, types, missing values, duplicates, distributions, and sample rows.
- Visual transforms: select, rename, reorder, cast, filter, sort, trim/normalize text, parse dates, fill or retain nulls, deduplicate, calculate basic fields, group/aggregate, and join small compatible files.
- Preview changes before execution; keep source file and transformation history for a bounded period.
- Basic charts and guided analysis questions: distributions, category counts, grouped metrics, trends, top-N.
- Download CSV and Excel results. Parquet may be a later free feature if storage/compute economics support it.
- Optional AI assistance with plain-language transform suggestions, using masked samples and user confirmation.

## Free limits and upgrade boundary

Set exact limits after cost modeling and beta measurement. Start with explicit caps for file size, rows/columns, job runtime, concurrent jobs, storage, history retention, and AI requests. Show limits before upload and offer a clear upgrade path when a job exceeds them. Do not accept an upload that cannot be processed within the product’s safe resource limits.

Free should exclude enterprise controls such as organization administration, SSO, private networking, custom retention, regulated deployment, shared governance, and production database publishing.

## User journey

1. Sign up and upload a supported file.
2. Review the profile and warnings.
3. Add a transform visually or request an AI suggestion.
4. Preview changed rows, rejected rows, and schema effects.
5. Run, inspect chart/table output, then download.
6. Save a reusable recipe within plan limits or upgrade for longer retention and collaboration.

## Revenue and growth model

- Free self-serve tier builds adoption and product awareness.
- Conversion to paid individual/pro tier can be tested later for higher limits, longer history, scheduled refresh, and more AI assistance.
- Enterprise is the primary paid offering in the current two-plan strategy; avoid prematurely building a full paid-individual tier.
- Acquisition: useful free workflow, educational examples, shareable exports/reports, referrals, and search-friendly documentation.

## Cost and sustainability controls

- Meter storage, worker CPU/memory/time, egress, and model use per account.
- Queue and throttle large jobs; run isolated workers with hard quotas.
- Use Pandas only for bounded jobs. Route larger analytics to a measured Parquet/DuckDB path only when economics justify it.
- Make AI opt-in, quota-bound, and transparent. Offer non-AI workflows with equivalent core capabilities.
- Define automatic deletion and user export before retention expiry.

## Success metrics

- Signup-to-first-successful-profile conversion.
- Upload-to-first-export activation and time to first useful result.
- Weekly returning users and completed datasets per active user.
- Transform preview-to-run and run-to-export conversion.
- Free-to-enterprise lead conversion, where the user belongs to a business.
- Cost per active user and per successful job; abuse/failure rate; support burden.

## Delivery phases

### Free Phase 1 — Useful first result

Build signup, bounded upload, CSV/XLSX/JSON profile, data preview, basic transforms, job feedback, CSV/XLSX download, and basic charts. Include quotas, deletion, and clear privacy/retention information.

**Exit:** a new user can complete upload → profile → transform → export without assistance; resource use stays within tested caps.

### Free Phase 2 — Repeat use

Add saved recipes, richer joins/grouping, validation warnings, reusable chart views, guided EDA, and optional limited AI assistance. Measure retention, common workflows, and cost before widening limits.

**Exit:** repeat users can reproduce a result and understand every changed/rejected row.

### Free Phase 3 — Growth funnel

Add public tutorials/sample datasets, shareable non-sensitive reports, account usage page, business-interest capture, and upgrade prompts tied to actual limits. Keep user files private by default.

**Exit:** acquisition, activation, retention, and unit-cost metrics support sustainable free access.

## Risks and responses

- **Compute/storage cost growth:** caps, lifecycle deletion, quotas, and usage monitoring.
- **Sensitive uploads:** private-by-default storage, encryption, access controls, minimal AI exposure, and documented deletion.
- **Confusing limits:** show file/job limits before work starts and explain failures clearly.
- **Free product too broad:** prioritize the upload-to-clean-to-export loop; defer advanced statistics and connectors.

## Decisions still needed

- Exact file/row/job/storage limits and retention period.
- Hosting region, privacy terms, and supported jurisdictions.
- Whether account creation is required before upload.
- Whether free AI is enabled at launch and which model/data policy applies.
- Whether later individual paid plans are desirable.

## Research provenance

Patterns are catalogued in [research-references.md](research-references.md). Particularly relevant: Pandas profiling and cleanup, multi-file ingestion, guided EDA, visualizations, reusable filters, grouping, and safe cleaning previews. Research repositories are learning examples; product behavior must be independently implemented and validated.
