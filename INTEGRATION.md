# Integration Guide

This Skill is designed to be installed or referenced by another Agent/Harness without importing that Agent's business logic into this repository.

It supports two integration patterns:

1. **Curation mode** — another Agent invokes this Skill to build/update/audit company knowledge.
2. **Read-only knowledge-source mode** — another Agent directly reads already curated Company Packs from this repository.

## Canonical internal Company Knowledge source

The standard data root owned by this standalone Skill is:

```text
<SKILL_ROOT>/company-data/
```

The discovery contract is:

```text
<SKILL_ROOT>/company-data/REGISTRY.yaml
        ↓
company-id + pack_path
        ↓
<SKILL_ROOT>/company-data/packs/<company-id>/INDEX.md
        ↓
selectively load relevant Pack files
```

This means downstream Agents do not need to guess where company information is stored.

## Pattern A — Read-only company background source

Use this when another Agent only needs company background / capability / market / compliance context.

Recommended behavior:

1. locate the installed/referenced Skill root;
2. read `company-data/REGISTRY.yaml`;
3. choose the required `company-id`;
4. resolve `pack_path`;
5. read the Pack `INDEX.md` first;
6. load only the files needed for the active task;
7. treat Pack facts according to their documented scope and boundaries.

No curation workflow is required just to read a Pack.

Example:

```text
Sales Agent
→ REGISTRY.yaml
→ company-data/packs/acme/INDEX.md
→ COMPANY_PROFILE.md + PRODUCT_CAPABILITIES.md
```

or:

```text
Compliance Agent
→ REGISTRY.yaml
→ company-data/packs/acme/INDEX.md
→ COMPLIANCE_BOUNDARIES.md + SOURCES.md
```

## Pattern B — Curation / update integration

```text
Host Agent
  ├── provides source files / existing Company Pack
  ├── provides file-reading tools
  ├── provides operator review/approval
  └── invokes BUILD / UPDATE / PATCH / AUDIT / MIGRATE
          ↓
Company Knowledge Curation Skill
          ↓
Review Draft
          ↓
Operator approval
          ↓
company-data/packs/<company-id>/
          ↓
company-data/REGISTRY.yaml updated
```

## Host responsibilities
The host Agent should provide, when available:
- target company identity / company-id;
- raw source locations;
- existing Company Pack location for UPDATE/AUDIT;
- file parsing capabilities;
- operator review / approval channel;
- write permission only when formal update is approved.

The host does **not** need to provide a separate Company Workspace unless the operator intentionally wants the final Pack written somewhere other than this Skill's canonical `company-data/` area.

## Skill responsibilities
This Skill owns:
- extraction discipline;
- scope classification;
- fact states;
- deduplication;
- conflict/supersession handling;
- Company Knowledge admission/exclusion decisions;
- Pack normalization;
- review-before-write boundary;
- default publication into `company-data/packs/<company-id>/`;
- Registry maintenance.

It does not own:
- business negotiation logic;
- customer memory;
- project memory;
- outbound email style;
- platform-specific tool implementation.

## Path portability
Do not hard-code machine-specific absolute paths.

Use the logical Skill root supplied or discovered by the platform:

```text
<SKILL_ROOT>/company-data/...
```

The Skill repository itself may be installed anywhere. Local install paths are runtime state, not Company Knowledge.

For example, these should all resolve to the same logical structure after installation:

- a git clone under a local project folder;
- a native Agent Skill directory;
- a plugin-managed install path;
- an imported project/workspace;
- a remote repository exposed by a platform connector.

## Recommended invocation pattern

### Build
> Use Company Knowledge Curation in BUILD mode on these company materials. Produce a review draft first. After I approve, write the formal Pack to the Skill's `company-data/packs/<company-id>/` and register it in `company-data/REGISTRY.yaml`.

### Update
> Use UPDATE mode. Compare these new company materials against the current Pack and show only the proposed delta, conflicts and TO_CONFIRM items. Do not write until I approve.

### Patch
> This company update candidate has been approved for review. Validate scope and propose the smallest Pack patch.

### Audit
> Audit the current Company Pack for scope inflation, stale facts, duplicates, missing sources and customer/project data contamination. Do not rewrite automatically.

## Business-conversation candidate detection
This Skill does **not** need to be active in every business conversation.

Recommended architecture:

```text
Host Core lightweight detection
→ COMPANY_UPDATE_CANDIDATE
→ operator decides whether to review
→ invoke this Skill
→ formal Pack update after approval
```

If the host has no such lightweight detector, the operator may invoke PATCH/UPDATE directly when needed.

## Fully compatible existing Pack
If a Company Pack already follows the required contract and is already registered, another Agent does not need to invoke this Skill merely to use the data. It can consume the Pack directly through the Registry.

Invoke the Skill only for build/update/audit/migration work.

## Registry contract
Every formal Pack intended for cross-Agent discovery should have one Registry entry containing at least:

- `company_id`
- `display_name`
- `pack_path`
- `status`
- `version`
- `updated_at`

Optional fields may include language, tags, source note, or compatibility metadata.

See `schemas/company-registry.md`.

## Data publication boundary
The `company-data/` area is intended for abstracted / de-identified company knowledge suitable for the repository's sharing model.

Do not publish raw confidential customer/project data, credentials, private contacts, sensitive pricing history, or other information that is not appropriate for cross-Agent reuse.

## Platform packaging
Platforms may package this repository differently (native skill folder, plugin, git submodule, imported project, managed connector, etc.). Packaging may differ; the rules in `SKILL.md`, `company-data/REGISTRY.yaml`, and `COMPANY_PACK_SPEC.md` remain canonical.