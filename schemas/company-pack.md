# Company Pack Data Contract

A formal Pack should preserve:
- stable `company_id` / pack identity;
- version / update date / status;
- source references;
- active facts grouped by topic;
- actual scope of sensitive facts;
- `TO_CONFIRM` items only when intentionally retained as open knowledge gaps;
- superseded relationships where relevant;
- de-identification/shareability status appropriate to this repository.

## Canonical storage

In this standalone Skill repository, the normal formal location is:

```text
company-data/packs/<company-id>/
```

Each reusable formal Pack should also be discoverable from:

```text
company-data/REGISTRY.yaml
```

The Registry should point to the Pack; it should not duplicate the Pack's detailed facts.

## Consumer entry

Downstream Agents should open the Pack's `INDEX.md` first, then selectively load relevant files.

The Pack should not require every source sentence to be represented. It is a curated operational knowledge layer, not a raw archive.
