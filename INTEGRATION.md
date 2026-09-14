# Integration Guide

This Skill is designed to be installed or referenced by another Agent/Harness without importing that Agent's business logic into this repository.

## Conceptual contract

```text
Host Agent
  ├── provides source files / existing Company Pack
  ├── provides file-reading tools
  ├── provides operator review/approval
  └── defines target Company Workspace
          ↓
Company Knowledge Curation Skill
          ↓
Review Draft / Pack update
```

## Host responsibilities
The host Agent should provide, when available:
- `COMPANY_ROOT` or equivalent logical company workspace;
- active company identity/company-id;
- raw source locations;
- existing Company Pack location for UPDATE/AUDIT;
- file parsing capabilities;
- write permission only when formal update is approved.

## Skill responsibilities
This Skill owns:
- extraction discipline;
- scope classification;
- fact states;
- deduplication;
- conflict/supersession handling;
- Company Knowledge admission/exclusion decisions;
- Pack normalization;
- review-before-write boundary.

It does not own:
- business negotiation logic;
- customer memory;
- project memory;
- outbound email style;
- platform-specific tool implementation.

## Path portability
Do not hard-code machine-specific paths.

Use logical roots supplied by the host, for example:
- `<AGENT_ROOT>/company/`
- `<WORKSPACE_ROOT>/company/`
- plugin-managed data directory
- remote repository logical path

The Skill repository itself may be installed anywhere. Local install paths are runtime state, not Company Knowledge.

## Recommended invocation pattern

### Build
> Use Company Knowledge Curation in BUILD mode on these company materials. Produce a review draft first. Do not write formal Company Pack files until I approve.

### Update
> Use UPDATE mode. Compare these new company materials against the current Company Pack and show only the proposed delta, conflicts and TO_CONFIRM items.

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

This prevents heavy curation logic from bloating ordinary business work.

## Fully compatible existing Pack
If a Company Pack already follows the required contract, the host Agent does not need to invoke this Skill just to load/use the Pack. Invoke only for build/update/audit/migration work.

## Platform packaging
Platforms may package this repository differently (native skill folder, plugin, git submodule, imported project, managed connector, etc.). Packaging may differ; the rules in `SKILL.md` remain canonical.