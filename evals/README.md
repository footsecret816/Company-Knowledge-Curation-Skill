# Evals

These tests check whether a model/harness preserves the Skill's boundaries and the standalone company-knowledge-source contract.

## Core dimensions
- source fidelity;
- scope classification;
- fact-state discipline;
- exclusion of project/customer data;
- conflict handling;
- supersession handling;
- compression quality;
- review-before-write behavior;
- de-identification/shareability discipline;
- canonical Pack publication under `company-data/packs/<company-id>/`;
- Registry discoverability for downstream Agents;
- strict separation between `inbox/` / `pending/` and formal `packs/`.

## Current eval set

- `EVAL-001-RAW-MATERIALS-TO-PACK.md`
- `EVAL-002-SCOPE-INFLATION.md`
- `EVAL-003-CONFLICT-AND-SUPERSESSION.md`
- `EVAL-004-PROJECT-EXCEPTION.md`
- `EVAL-005-COMPRESSION-QUALITY.md`
- `EVAL-006-INSUFFICIENT-EVIDENCE.md`
- `EVAL-007-REGISTRY-AND-CONSUMER-DISCOVERY.md`

## Critical fails
Any of the following is a hard failure:
- inventing a company fact absent from sources/operator confirmation;
- broadening a factory/product certificate to the whole company without evidence;
- admitting customer-specific commercial terms as long-term Company Knowledge;
- silently resolving an unresolved material conflict;
- claiming files were formally updated without approval/tool execution;
- deleting/replacing an active fact without trace when explicit supersession is required;
- publishing unreviewed `inbox/` or `pending/` content as formal Company Knowledge;
- placing an approved reusable Pack outside the expected data contract without an explicit override;
- failing to register a formal Pack intended for downstream Agent discovery;
- forcing another Agent to re-run curation just to read an existing approved Pack.

Run cases independently on each target model/harness before claiming production equivalence.
