# Research References and Adoption Register

## Purpose

This is the permanent research-to-product record for the DMS. It records what was inspected, what may be adopted, where it belongs in the plan, and limits on adoption. Update this file whenever a repository informs a product decision.

**Rule:** adopt ideas, patterns, and independently implemented behavior. Do not copy datasets, notebook outputs, credentials, or code without confirming its licence and preserving required notices.

## Source register

| Repository | Local clone | Revision inspected | Licence observed | Adopted into plan |
| --- | --- | --- | --- | --- |
| [mohammadreza-mohammadi94/Data-Analysis-Projects-With-Pandas](https://github.com/mohammadreza-mohammadi94/Data-Analysis-Projects-With-Pandas) | `research/Data-Analysis-Projects-With-Pandas` | `987ee4b0cbee89ff96076f21bacd5830749fcc87` | Verify before code reuse | Profile, cleaning, merging, SQL staging, multi-file import, EDA, feature engineering, web/API import, time series, visualization |
| [KeithGalli/Pandas-Data-Science-Tasks](https://github.com/KeithGalli/Pandas-Data-Science-Tasks) | `Pandas-Data-Science-Tasks` | `8b511cdf8aeea304bb64710784db29548414b736` | Verify before code reuse | Batch ingestion, typed cleaning, derived sales fields, KPI/time/co-occurrence analyses |
| [Anas1108/Exploratory-Data-Analysis-with-Pandas](https://github.com/Anas1108/Exploratory-Data-Analysis-with-Pandas) | `Exploratory-Data-Analysis-with-Pandas` | `ce6c675953d8f6551135d70e64c94eea21af6252` | Verify before code reuse | Question-led segmented EDA templates |
| [arinskyyyy/data-cleaning](https://github.com/arinskyyyy/data-cleaning) | `data-cleaning` | `d1ac613b61e077959d51e63940d0128f840b4e8b` | Verify before code reuse | Cleaning recipe categories, field-level null policy, schema mapping, temporal normalization, quality reports |
| [PacktPublishing/Mastering-Exploratory-Analysis-with-pandas](https://github.com/PacktPublishing/Mastering-Exploratory-Analysis-with-pandas) | `Mastering-Exploratory-Analysis-with-pandas` | `abc55445c0b6a4791c3cf4d80d6eaa2d0d23ebff` | MIT, copyright Packt (2018) | Import/filter/select/date/merge/group/chart operation catalogue |
| [imarranz/essential-guide-to-pandas](https://github.com/imarranz/essential-guide-to-pandas) | `essential-guide-to-pandas` | `f0b7cf8c86f3bd2b541f70bb55516a9de3ceabc9` | MIT, copyright imarranz (2024) | Quality checks, reshaping, categories, time-series, JSON/XML roadmap, export and merge catalogue |
| [PacktPublishing/Hands-on-Exploratory-Data-Analysis-with-Python](https://github.com/PacktPublishing/Hands-on-Exploratory-Data-Analysis-with-Python) | `Hands-on-Exploratory-Data-Analysis-with-Python` | `1ecc3cc761f83e5ad3debe544a870d5f9f80e471` | MIT, copyright Packt (2019) | EDA methodology, descriptive statistics, group/correlation/time-series, advanced analysis roadmap |

## Detailed adoption notes

### `Data-Analysis-Projects-With-Pandas`

**Adopt:** profile report; cleaning and deduplication; joins/unions/reshape; database import/export; multi-file ingestion; charts; time-series windows; external-source adapters.

**Do not adopt directly:** mutable notebook workflow, hard-coded files, checkpoint notebooks, finance-specific strategy logic, unrestricted scraping.

### `Pandas-Data-Science-Tasks`

**Adopt:** manifest-driven monthly/batch file ingestion; blank/repeated-header detection; typed conversion; calculated measures; grouped KPIs; time buckets; product relationship analysis.

**Required changes:** decimal arithmetic for money; explicit source-schema contract before append; robust date parsing; transaction-key-based co-occurrence; PII controls for purchase and location data.

### `Exploratory-Data-Analysis-with-Pandas`

**Adopt:** question-first EDA. Record population, segment, denominator, aggregation, and threshold with every result.

**Required changes:** expose results as saved, reproducible analysis cards, rather than one-off notebook answers.

### `data-cleaning`

**Adopt:** targeted null handling, duplicate removal, type normalization, source merge, category normalization, derived features, schema unification, timezone normalization, test-record exclusion, outlier review/capping.

**Required changes:** no universal zero-null objective; no irreversible drop/cap without preview and policy; medical, finance, location, and social data need classification/access controls. Fuzzy entity cleanup needs a human-review workflow.

### `Mastering-Exploratory-Analysis-with-pandas`

**Adopt:** adapter catalogue for CSV, Excel, JSON, HTML table, SQL, and delimited files; selection/filter/sort; dates; joins; grouping; chart configuration.

**Required changes:** supported formats/connector allow-list; parameterized database access; safe visual filter schema; no free-form code execution.

### `essential-guide-to-pandas`

**Adopt:** full recipe taxonomy: load, inspect, clean, transform, reshape, deduplicate, merge, aggregate, text, category, datetime/time-series, JSON/XML, export, data-quality checks.

**Required changes:** stage advanced formats after CSV/XLSX/JSON; compile typed recipe operations server-side. Never make Pandas `eval`, `query`, or `apply` user-code execution features.

### `Hands-on-Exploratory-Data-Analysis-with-Python`

**Adopt:** EDA lifecycle: investigate, summarize, visualize, validate assumptions, then model/evaluate if justified. Include descriptive, grouping, correlation, time-series, testing, and regression as increasingly advanced workspaces.

**Required changes:** advanced statistics remain optional and clearly labelled exploratory. Show sample size, assumptions, missing-data handling, methodology, and limitations; do not turn them into automatic business conclusions.

## Traceability rules

- Add this reference file link to every architecture decision, feature epic, and pull request that uses research-derived behavior.
- Record exact repository revision, licence, file/notebook, idea adopted, implementation location, and any modification made for production.
- Re-check licence before copying a material code fragment. Preserve notices and attribution where required.
- Keep original research clones outside deployable application images and never ship included sample data as production data.
