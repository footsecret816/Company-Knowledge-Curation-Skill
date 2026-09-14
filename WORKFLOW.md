# Workflow

## Shared pipeline

All modes use the same evidence discipline:

`Source → Fact extraction → Scope → State → Dedup/Conflict → Review → Approval → Formalization`

The difference is what enters the pipeline and what final change is allowed.

## BUILD — create a Company Pack from zero

Use when there is no usable formal Pack.

1. Inventory raw materials.
2. Identify source type, date, owner/issuer if known.
3. Extract atomic facts.
4. Classify scope and evidence state.
5. Group into Pack sections.
6. Remove marketing repetition and project-only data.
7. Identify missing but important topics as `TO_CONFIRM`; do not fabricate them.
8. Produce first Review Draft.
9. Accept operator corrections/additions.
10. After approval, generate `PACK.yaml`, core Markdown files, `SOURCES.md`, and needed `products/` files.

## UPDATE — new materials vs existing Pack

Use when a Company Pack already exists.

1. Load existing Pack and source records.
2. Process only the new materials first.
3. Compare extracted facts against same-scope existing facts.
4. Classify each delta as:
   - `ADD`
   - `CHANGE`
   - `CONFIRM_EXISTING`
   - `CONFLICT`
   - `SUPERSEDE`
   - `EXCLUDE`
5. Show a compact delta review.
6. Do not rewrite unaffected Pack sections.
7. After approval, patch only affected files and update source/version metadata.

## PATCH — approved conversation/company delta

Use when another Agent has already surfaced a candidate and the operator approved formal review.

1. Read the candidate exactly as supplied.
2. Verify whether it has supporting source or explicit operator confirmation.
3. Determine actual scope.
4. Compare against current Pack.
5. If still ambiguous, keep `TO_CONFIRM` and do not write.
6. If confirmed, propose the smallest Pack patch.
7. After approval, write patch + source/supersession metadata.

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
- overlong sections that can be compressed without losing decision-critical detail.

Return findings grouped by severity:
- `Critical boundary issue`
- `Needs confirmation`
- `Cleanup / compression`
- `No action needed`

Do not change the Pack unless the operator then asks to update it.

## MIGRATE — legacy knowledge to canonical Pack

Use for old folder structures, large single Markdown company files, prompt-embedded company info, or another Agent's company knowledge format.

1. Treat legacy files as sources, not automatically authoritative structure.
2. Preserve actual facts and provenance where available.
3. Reclassify by scope.
4. Remove platform-specific paths/instructions from Company Knowledge.
5. Move customer/project-specific content out of Company Pack proposal.
6. Convert into canonical files.
7. Produce migration review showing anything dropped, transformed, or requiring confirmation.
8. Finalize only after approval.

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
- operator approval has not been provided.