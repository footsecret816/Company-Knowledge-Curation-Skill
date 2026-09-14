# Company Pack Specification

## Purpose
A Company Pack is a concise, structured representation of one company's relatively stable, reusable, de-identified business knowledge.

In this standalone Skill repository, approved Packs are not only outputs of the curation workflow; they are also the canonical company-background data source that other Agents can discover and consume.

## Canonical storage root

The default formal storage location is:

```text
<SKILL_ROOT>/company-data/packs/<company-id>/
```

The discovery registry is:

```text
<SKILL_ROOT>/company-data/REGISTRY.yaml
```

A Pack intended for cross-Agent use should be both:
1. present under `company-data/packs/<company-id>/`; and
2. registered in `company-data/REGISTRY.yaml`.

## Canonical structure

```text
company-data/packs/<company-id>/
├── PACK.yaml
├── INDEX.md
├── COMPANY_PROFILE.md
├── PRODUCT_CAPABILITIES.md
├── SUPPLY_CHAIN_MODEL.md
├── COMPLIANCE_BOUNDARIES.md
├── MARKETS_AND_CUSTOMERS.md
├── BUSINESS_SOP.md
├── SOURCES.md
└── products/
```

An operator may explicitly request another compatible output root, but the standalone repository's normal default is `company-data/packs/`.

## PACK.yaml
Recommended metadata:
- `pack_id`
- `company_id`
- `company_name` or de-identified display name
- `version`
- `status`
- `updated_at`
- `source_types`
- `default_language`
- `fact_scope_policy`
- `deidentification_status`
- `notes`

`company_id` should remain stable across updates so downstream Agents can keep resolving the same Pack.

## INDEX.md
A short navigation/load guide:
- what this Pack represents;
- fact-scope warning;
- which file to load for which task;
- key source/maintenance note;
- important limitations / boundaries.

Do not duplicate all Pack content into INDEX.

Downstream Agents should normally open `INDEX.md` before loading the rest of the Pack.

## COMPANY_PROFILE.md
Include only stable/reusable items such as:
- identity or safe de-identified identity;
- location / region when appropriate to retain;
- business model;
- positioning;
- core strengths supported by sources;
- customer/channel orientation;
- external-communication boundaries.

## PRODUCT_CAPABILITIES.md
Include:
- core product families;
- extended/project-sourced categories separately;
- stable customization scope;
- material/structure capability at appropriate scope;
- boundary that exact price/MOQ/test/lead time require project confirmation.

## SUPPLY_CHAIN_MODEL.md
Include:
- owned vs partner-factory model;
- sourcing/production coordination model;
- reusable supplier-selection logic;
- QC/logistics coordination capability when supported;
- important ownership/capability wording boundaries.

## COMPLIANCE_BOUNDARIES.md
Include:
- known certifications/audits with actual holder/scope;
- test/compliance support model;
- claim restrictions;
- IP/confidentiality boundaries;
- explicit `TO_CONFIRM` areas where needed.

This file is a boundary file, not a place to make broad regulatory guarantees.

## MARKETS_AND_CUSTOMERS.md
Include:
- target customer types;
- target channels;
- major markets/regions when supported;
- customer-acquisition channels;
- relevant positioning notes.

Avoid exposing confidential customer identity unless explicitly authorized and compatible with the repository's de-identification policy.

## BUSINESS_SOP.md
Include reusable workflow only:
- inquiry / qualification;
- product selection / development;
- quotation / sampling;
- order confirmation;
- production/QC;
- shipment/documents;
- after-sales / review.

Do not store one customer's historical timeline as SOP.

## SOURCES.md
Track source provenance. Suggested fields:
- source ID/name or safe de-identified reference;
- source type;
- date/effective date if known;
- scope;
- what Pack sections it supports;
- status: active / superseded / partial / to-confirm;
- notes.

When raw source names themselves are sensitive, use stable abstract source IDs rather than leaking the original filename or party name.

## products/
Create product-category files only when detail is large enough to justify selective loading.

Do not create one file per trivial SKU by default. Group by reusable category/knowledge need.

## Registry entry
After a Pack is formally approved, add or update an entry in `company-data/REGISTRY.yaml`.

Minimum fields:
- `company_id`
- `display_name`
- `pack_path`
- `status`
- `version`
- `updated_at`

Recommended `pack_path` format:

```text
company-data/packs/<company-id>
```

See `schemas/company-registry.md`.

## Compression target
A good Pack should be shorter and more operational than raw source materials, while preserving all caveats that change business decisions.

The goal is not to reproduce source documents. The Pack should help another Agent answer: **Who is this company, what can it reliably do, what are its important boundaries, and which file should I load for this task?**

## De-identification / shareability rule
Because the standalone repository may serve as a reusable Company Knowledge source, content written to `company-data/packs/` should be appropriate for that sharing model.

Do not place raw credentials, personal contacts, confidential customer/project data, private pricing history, or other non-shareable information in a formal Pack.

If useful company knowledge cannot be safely published in de-identified form, exclude it from this repository or route it to a private host-specific data layer.

## Admission rule
Admit information only when it is relatively stable, reusable, properly scoped, supported, safe, and sufficiently de-identified for the intended repository use.

## Formal update rule
Formal Company Pack changes require operator confirmation. A complete formal update normally includes:
1. the Pack file changes; and
2. any required `REGISTRY.yaml` version/status/path update.