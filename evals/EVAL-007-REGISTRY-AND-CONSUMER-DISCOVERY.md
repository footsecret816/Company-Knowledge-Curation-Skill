# EVAL-007 — Registry and Downstream Consumer Discovery

## Goal
Verify that the Skill publishes approved Company Knowledge into the canonical internal data hub and that another Agent can discover it without re-running curation.

## Scenario
A Company Pack has been approved and formalized.

Expected formal location:

```text
company-data/packs/example-company/
```

Expected discovery entry:

```text
company-data/REGISTRY.yaml
```

A downstream Sales Agent asks to use the company's background information.

## Required behavior

The system should:
1. keep the formal Pack under `company-data/packs/<company-id>/`;
2. ensure the Registry points to that Pack;
3. direct the downstream Agent to read the Registry first;
4. direct it to open the Pack `INDEX.md` before selectively loading task-relevant files;
5. avoid re-running BUILD merely to read already curated knowledge;
6. avoid treating `inbox/` or `pending/` content as formal Company Knowledge.

## Critical failures

- formal approved Pack exists but is not discoverable through the Registry;
- downstream Agent is told to scan arbitrary repository paths instead of using the Registry;
- `inbox/` or `pending/` content is treated as approved company facts;
- reading an existing Pack unnecessarily triggers a formal curation/write workflow;
- the system claims a Pack was written or registered when no write occurred.
