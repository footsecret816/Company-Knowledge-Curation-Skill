# Formal Company Packs

This directory is the canonical storage area for **approved, structured, de-identified Company Knowledge** that other Agents may consume.

Each company uses a stable directory:

```text
company-data/packs/<company-id>/
```

A formal Pack should follow `COMPANY_PACK_SPEC.md` and normally contain:

```text
PACK.yaml
INDEX.md
COMPANY_PROFILE.md
PRODUCT_CAPABILITIES.md
SUPPLY_CHAIN_MODEL.md
COMPLIANCE_BOUNDARIES.md
MARKETS_AND_CUSTOMERS.md
BUSINESS_SOP.md
SOURCES.md
products/
```

## Discovery

Do not make downstream Agents scan this directory blindly. Every formal Pack intended for reuse should also be listed in:

```text
company-data/REGISTRY.yaml
```

Downstream Agents should resolve the Pack through the Registry, open `INDEX.md`, then load only the files required by the task.

## Important boundary

Files here are formal reusable Company Knowledge. Drafts, unresolved conflicts, raw customer/project details, or unapproved company information belong outside this directory.
