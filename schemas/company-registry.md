# Company Registry Schema

`company-data/REGISTRY.yaml` is the discovery index for formal Company Packs stored in this Skill repository.

## Purpose

Allow any downstream Agent to answer:
- which company Packs are available;
- which `company-id` to use;
- where the Pack is stored;
- whether the Pack is active;
- which version/date is current.

## Minimum structure

```yaml
schema_version: 1.0
purpose: >
  Discovery index for formal, reviewed, de-identified Company Packs.
companies:
  - company_id: acme
    display_name: ACME Example Company
    pack_path: company-data/packs/acme
    status: active
    version: 1.0.0
    updated_at: 2026-01-01
```

## Required company fields

- `company_id` — stable machine-friendly identifier;
- `display_name` — human-readable safe/de-identified name;
- `pack_path` — repository-relative path to the formal Pack;
- `status` — normally `active`, `inactive`, `archived`, or `draft`;
- `version` — current Pack version;
- `updated_at` — latest formal update date when known.

## Optional fields

- `aliases`
- `default_language`
- `tags`
- `markets`
- `product_families`
- `notes`
- `compatibility`

Optional fields are for discovery only. Do not duplicate the entire Company Pack into the Registry.

## Consumer rule

Downstream Agents should:
1. read the Registry;
2. identify the target `company_id`;
3. resolve `pack_path`;
4. open `<pack_path>/INDEX.md`;
5. load only relevant Pack files.

## Maintenance rule

Formal BUILD / UPDATE / MIGRATE operations should add or update the Registry entry after operator approval.

Do not register a Pack as `active` when its company identity is unresolved or the Pack is still only a Review Draft.
