# DMS Enterprise Plan — Business Organizations

## Executive summary

Sell a governed data preparation and analysis platform to organizations. Enterprise users bring files or approved data connections into controlled workspaces, collaboratively define repeatable transformations and quality rules, review changes, and publish approved outputs with lineage, audit, identity, and operational controls.

The product builds on the free user workflow, adding organization governance, integration, scale, security, service commitments, and managed operations.

## Target customers and buyers

- Mid-market and enterprise teams with recurring spreadsheet/file pipelines and inconsistent data quality.
- Analytics, operations, finance, marketing, research, and data-stewardship teams.
- Buyers: Head of Data/Analytics, IT/security, business operations, and transformation leaders.
- Users: analysts, data stewards, administrators, reviewers, and read-only stakeholders.

## Customer problems

- Manual spreadsheet cleanup is slow and difficult to reproduce.
- Teams lack clear ownership, provenance, and quality checks for datasets.
- Business users need self-service preparation while IT must constrain access and production writes.
- Existing notebooks/scripts can be hard to govern, share, and hand over.

## Product promise

“Turn recurring data preparation into governed, reviewable, repeatable workflows.”

## Enterprise capabilities

### Governed workspace

- Organization and project workspaces; roles and granular permissions.
- SSO/SAML or OIDC; SCIM provisioning in a higher enterprise tier; audit logs.
- Dataset catalog with owners, descriptions, tags, classifications, data dictionary, lineage, versions, and retention policies.
- Row/column restrictions and sensitive-field masking where required.

### Ingestion and integration

- Upload CSV/Excel/JSON/Parquet; batch folders and schema-compatible appends.
- Approved PostgreSQL/MySQL/SQL Server connections; start read-only.
- Later allow-listed REST, SFTP, and object-storage connectors with secret vaulting, rate limits, retries, and provenance.
- Customer-selected cloud/region and optional private networking or customer-managed keys, subject to architecture and customer demand.

### Transformation and quality

- Versioned, deterministic recipes with preview, approval, replay, and rollback to prior dataset versions.
- Schema harmonization, field-level null policies, data type/date/currency handling, deduplication, joins, entity mappings, derived fields, and aggregation.
- Quality tests for completeness, uniqueness, validity, freshness, schema drift, and referential integrity.
- Rejected/quarantined rows with reasons; controlled publish gates.
- Scheduled runs, run history, alerts, notifications, and failure recovery.

### Analysis and delivery

- Shared KPI/EDA views, charts, guided questions, reusable reports, and exports.
- Stage-table publish and controlled promotion to approved SQL destinations.
- Optional AI suggestions in policy-bound workflows; redact or minimize sensitive values, require typed allow-listed plans, preview, and user approval.
- Advanced statistics remain explicitly exploratory and show sample size, method, assumptions, and limitations.

## Deployment and service options

Offer a staged commercial model, validating demand before supporting every variant:

1. **Hosted multi-tenant:** default, with strong tenant isolation and selectable region if commercially justified.
2. **Hosted dedicated environment:** for customers needing dedicated compute/storage boundaries.
3. **Private cloud or customer-managed deployment:** only for validated requirements; adds deployment, upgrade, support, and security costs.

Define availability, support response, backup/restore, incident communication, and data deletion commitments before selling production use. Avoid promises beyond measured operational capability.

## Commercial model

Use subscription plus transparent usage dimensions. Test pricing rather than inventing unsupported prices now.

- Base organization subscription: workspaces, governance, catalog, audit, and standard support.
- Seat or active-user component, if customer interviews confirm value alignment.
- Metered compute/storage/connector volume for variable costs, with quotas and alerts.
- Higher tiers for SSO/SCIM, advanced retention, dedicated environment, private networking, customer-managed keys, premium support, and deployment options.
- Paid onboarding/migration services only where they accelerate adoption and can be delivered repeatably.

## Go-to-market

- Start with a narrow ideal customer profile: teams with recurring CSV/Excel-to-database or reporting workflows.
- Sell a paid pilot with one workflow, one source, one approved output, measurable baseline, and defined security review.
- Demonstrate time saved, reduced error/rework, improved freshness, and reproducible audit evidence.
- Convert pilots into annual subscriptions after production use and support boundaries are proven.
- Channels: direct design partners first; later data consultancies, cloud marketplaces, and technology partners.

## Pilot design

- 4–8 week pilot assumption; confirm with customer procurement and workflow complexity.
- One team, one or two data sources, one governed recipe, one destination.
- Baseline manual time, failure/rework rate, publish latency, and quality exceptions.
- Exit criteria: successful replay, customer-approved quality checks, permissions/audit validated, and quantified operational benefit.

## Delivery phases

### Enterprise Phase 1 — Team governance foundation

Implement tenant/workspace isolation, roles, audit, immutable versions, catalog basics, admin controls, and security documentation. Build on the reliable free ingestion and transform workflow.

**Exit:** organization administrators can grant/revoke access and review who accessed or changed a dataset.

### Enterprise Phase 2 — Repeatable controlled workflows

Add shared versioned recipes, quality rules, approvals, quarantine, scheduled jobs, notifications, lineage, and supportable run recovery.

**Exit:** a recurring workflow can run and be reviewed end-to-end without a person manually editing source files.

### Enterprise Phase 3 — Approved database exchange

Add secrets management, allow-listed read-only source connections, stage-table publishing, validation, approval, and rollback. Add SSO and stronger identity integrations according to design-partner demand.

**Exit:** a customer can import, transform, validate, approve, and publish through an auditable path.

### Enterprise Phase 4 — Scale, compliance, and deployment options

Add usage metering, quotas, autoscaling, recovery objectives, security testing, formal operational controls, dedicated/private deployments, and advanced identity/encryption options as justified.

**Exit:** service levels and recovery have been demonstrated under target customer load; security review evidence is available.

### Enterprise Phase 5 — Governed AI and broader connectors

Roll out typed-plan AI, semantic mapping, data dictionaries, and more connectors behind customer policy controls. Track acceptance, correction, latency, cost, and sensitive-data exposure.

**Exit:** AI and connectors pass customer security review and cannot exceed configured permissions or operations.

## Success measures

- Pilot-to-paid conversion and time to production.
- Annual recurring revenue, gross margin, renewal, and expansion.
- Manual hours saved and workflow error/rework reduction.
- Successful scheduled-run rate, freshness, mean recovery time, and quality-rule resolution time.
- Seat/workspace adoption and number of governed workflows.
- Support cost, compute/storage cost per tenant, and security incidents.

## Security and trust requirements

- Tenant isolation verified; least privilege; encryption in transit and at rest; secrets manager.
- Data classification, retention/deletion, backup/restore, audit, incident response, vulnerability management.
- No arbitrary user Python/shell execution or unrestricted SQL access in the application.
- No automatic production write without an approved destination, staged validation, and explicit policy.
- AI receives only necessary masked or approved data; prompts/results handled under documented retention and provider terms.
- Obtain legal/security review for applicable contracts, privacy commitments, and compliance claims before making them.

## Risks and responses

- **Long security/procurement cycles:** sell narrow paid pilots and prepare accurate security evidence early.
- **Custom-work trap:** keep connectors and workflow operations standardized; price genuinely customer-specific work separately.
- **Pandas capacity mismatch:** cap jobs and route larger workloads through Parquet/DuckDB or a warehouse execution path based on measured workload.
- **High support burden:** define supported deployment matrix, SLOs, upgrade policy, and paid service boundaries.
- **AI trust concerns:** make AI optional, auditable, policy-limited, and reviewable.

## Decisions still needed

- Initial vertical and ideal customer profile.
- Hosted cloud/region and tenant model.
- Identity provider and first SQL connector.
- Seat-based versus usage-based pricing emphasis.
- Support hours, service levels, recovery objectives, and deployment options.
- Required security/compliance roadmap based on target buyers.

## Research provenance

Detailed source and revision record: [research-references.md](research-references.md). Adoptable patterns include schema normalization, batch ingestion, cleaning/quality recipes, reproducible transformations, grouped KPIs, joins, lineage-worthy workflows, time-series analysis, and validated exports. Repositories supply research examples, not production guarantees or an enterprise control framework.
