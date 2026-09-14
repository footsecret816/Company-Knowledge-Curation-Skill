# Workflow

## Shared pipeline

All modes use the same evidence discipline:

`Source → Fact extraction → Scope → State → Dedup/Conflict → Review → Approval → Formalization → Registry`

The difference is what enters the pipeline and what final change is allowed.

## Canonical storage targets

For this standalone Skill, use:

```text
company-data/inbox/
company-data/pending/
company-data/packs/<company-id>/
company-data/REGISTRY.yaml
```

The Pack path is the formal company-knowledge source. The Registry is the discovery index for other Agents.

## BUILD — create a Company Pack from zero

Use when there is no usable formal Pack.

1. Inventory raw materials.
2. Identify source type, date, owner/issuer if known.
3. Establish a stable `company-id`.
4. Extract atomic facts.
5. Classify scope and evidence state.
6. Group into Pack sections.
7. Remove marketing repetition and project-only data.
8. Check whether retained information is sufficiently abstracted / de-identified for publication in this repository.
9. Identify missing but important topics as `TO_CONFIRM`; do not fabricate them.
10. Produce first Review Draft.
11. Accept operator corrections/additions.
12. After approval, generate `PACK.yaml`, core Markdown files, `SOURCES.md`, and needed `products/` files under `company-data/packs/<company-id>/`.
13. Add the Pack to `company-data/REGISTRY.yaml`.

## UPDATE — new materials vs existing Pack

Use when a Company Pack already exists.

1. Resolve the Pack through `company-data/REGISTRY.yaml` when possible.
2. Load existing Pack and source records.
3. Process only the new materials first.
4. Compare extracted facts against same-scope existing facts.
5. Classify each delta as:
   - `ADD`
   - `CHANGE`
   - `CONFIRM_EXISTING`
   - `CONFLICT`
   - `SUPERSEDE`
   - `EXCLUDE`
6. Show a compact delta review.
7. Do not rewrite unaffected Pack sections.
8. After approval, patch only affected files and update source/version metadata.
9. Update the Registry entry when version, status, display name, path, or update timestamp changes.

## PATCH — approved conversation/company delta

Use when another Agent has already surfaced a candidate and the operator approved formal review.

1. Read the candidate exactly as supplied.
2. Verify whether it has supporting source or explicit operator confirmation.
3. Determine actual scope.
4. Resolve the current Pack from the Registry.
5. Compare against current Pack.
6. If still ambiguous, keep `TO_CONFIRM` and do not write.
7. If confirmed, propose the smallest Pack patch.
8. After approval, write patch + source/supersession metadata.
9. Update Registry metadata if needed.

## AUDIT — inspect without automatic rewrite

Use when the operator wants quality control.

Check for:
- duplicated facts;
- scope inflation;
- unsupported superlatives;
- stale facts;
- conflicting facts;
- missing provenance;
- company/project memory contamination;
- insufficient de-identification for the repository's sharing model;
- broken Registry entries / missing Pack paths;
- overlong sections that can be compressed without losing decision-critical detail.

Return findings grouped by severity:
- `Critical boundary issue`
- `Needs confirmation`
- `Cleanup / compression`
- `Registry / discoverability issue`
- `No action needed`

Do not change the Pack unless the operator then asks to update it.

## MIGRATE — legacy knowledge to canonical Pack

Use for old folder structures, large single Markdown company files, prompt-embedded company info, or another Agent's company knowledge format.

1. Treat legacy files as sources, not automatically authoritative structure.
2. Preserve actual facts and provenance where available.
3. Reclassify by scope.
4. Remove platform-specific paths/instructions from Company Knowledge.
5. Move customer/project-specific content out of Company Pack proposal.
6. Apply de-identification / shareability rules.
7. Convert into canonical files under `company-data/packs/<company-id>/`.
8. Produce migration review showing anything dropped, transformed, or requiring confirmation.
9. Finalize only after approval.
10. Add/update the Registry entry.

## Read-only consumption — no curation required

Another Agent that only needs company background should not run BUILD/UPDATE automatically.

Use:

```text
company-data/REGISTRY.yaml
→ target company-id
→ pack_path/INDEX.md
→ relevant Pack files
```

This is a read operation, not a curation operation.

## Multi-round review

Company curation often requires several review rounds. Do not interpret an operator correction as an annoyance or force a one-shot finalization.

Each round should:
- preserve already confirmed unaffected items;
- change only what the operator corrected;
- show remaining `TO_CONFIRM` / conflicts;
- avoid re-expanding previously condensed sections unless needed.

## Stop conditions

Stop before formalization when:
- company identity is ambiguous;
- critical source conflict is unresolved;
- scope of a certificate/capability is unclear and materially affects claims;
- the only basis is AI inference;
- information is not sufficiently de-identified for the intended repository and no safe abstraction is possible;
- operator approval has not been provided.

A workflow is not fully complete until the approved Pack is written to its target path and, when intended for shared discovery, the Registry points to it.