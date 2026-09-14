# Company Pack Specification

## Purpose
A Company Pack is a concise, structured representation of one company's relatively stable, reusable business knowledge.

## Canonical structure

```text
company/packs/<company-id>/
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

The host Agent may map this structure to another root, but logical roles should remain the same.

## PACK.yaml
Recommended metadata:
- `pack_id`
- `company_name`
- `version`
- `status`
- `updated_at`
- `source_types`
- `default_language`
- `fact_scope_policy`
- `notes`

## INDEX.md
A short navigation/load guide:
- what this Pack represents;
- fact-scope warning;
- which file to load for which task;
- key source/maintenance note.

Do not duplicate all Pack content into INDEX.

## COMPANY_PROFILE.md
Include only stable/reusable items such as:
- identity;
- location;
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

Avoid exposing confidential customer identity unless explicitly authorized.

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
- source ID/name;
- source type;
- date/effective date if known;
- scope;
- what Pack sections it supports;
- status: active / superseded / partial / to-confirm;
- notes.

## products/
Create product-category files only when detail is large enough to justify selective loading.

Do not create one file per trivial SKU by default. Group by reusable category/knowledge need.

## Compression target
A good Pack should be shorter and more operational than raw source materials, while preserving all caveats that change business decisions.

## Admission rule
Admit information only when it is relatively stable, reusable, properly scoped, supported, and safe for long-term company knowledge.

## Formal update rule
Formal Company Pack changes require operator confirmation.