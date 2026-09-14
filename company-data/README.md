# Company Data Hub

This directory is the canonical company-knowledge data area for this standalone Skill.

这里存放的是经过清洗、结构化、审核，并适合跨 Agent 复用的**抽象化 / 脱敏公司知识**。

## Fixed contract

```text
company-data/
├── REGISTRY.yaml
├── inbox/
├── pending/
└── packs/
    └── <company-id>/
```

## Meaning

- `REGISTRY.yaml` — company discovery index. Other Agents should read this first.
- `inbox/` — de-identified raw/intermediate company materials waiting for curation.
- `pending/` — update candidates waiting for formal review/approval.
- `packs/` — formal reviewed Company Packs ready for downstream Agent use.

## Consumer rule

A downstream Agent that only needs company background should use:

```text
REGISTRY.yaml
→ target company-id
→ pack_path/INDEX.md
→ selectively load relevant Pack files
```

It does not need to invoke the curation workflow just to read existing Company Knowledge.

## Publication rule

Only operator-approved, sufficiently de-identified, reusable company knowledge should be published under `packs/`.

Do not place raw customer/project privacy, credentials, sensitive contacts, private pricing history, or other non-shareable information here.
