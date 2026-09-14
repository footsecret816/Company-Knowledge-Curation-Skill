# Company Knowledge Curation Skill

A standalone, model-agnostic Skill for turning messy company materials into a structured, reviewable, reusable Company Pack — and keeping the cleaned, de-identified Company Knowledge inside this repository as a standard data source for other Agents.

这是一个独立的 **公司信息整理 / 浓缩 / 更新 / 供给 Skill**。它不仅负责把 PDF、PPT、Word、Excel、图片、证书、产品目录、网页导出资料和已确认的公司信息清洗成高信号 Company Pack，也为其他 Agent 提供一个固定、可发现的公司背景知识路径。

> 核心原则：**先提取事实，再判断范围，再审核；用户确认后，才进入正式公司知识。正式脱敏后的公司知识统一落在 `company-data/packs/<company-id>/`。**

## 这个 Skill 现在承担两类价值

### 1. Company Knowledge Curation｜公司知识清洗

把杂乱、重复、不同来源的公司资料整理成：

- 有事实边界的公司介绍；
- 产品与能力结构；
- 供应链模式；
- 合规 / 认证边界；
- 市场与客户定位；
- 可复用业务 SOP；
- 产品分类知识；
- 来源与 supersession 记录。

它不是普通“总结文档”。它会判断什么应该进入长期公司知识、什么只属于某个工厂 / 产品 / 项目 / 客户、什么需要确认、什么必须排除。

### 2. Company Knowledge Source｜公司背景信息源

清洗完成并经确认的脱敏公司知识，默认存放在本 Skill 自己的：

```text
<SKILL_ROOT>/company-data/packs/<company-id>/
```

其他 Agent 如果只想读取公司背景，不需要重新执行清洗流程。标准读取入口是：

```text
<SKILL_ROOT>/company-data/REGISTRY.yaml
        ↓
找到 company-id 与 pack_path
        ↓
<SKILL_ROOT>/company-data/packs/<company-id>/INDEX.md
        ↓
按任务选择性加载 Pack 文件
```

因此这个仓库既可以被当作一个 Skill 使用，也可以被当作一个**脱敏后的标准公司知识源**使用。

## 为什么要这样设计？

真实公司的资料通常散落在很多地方：公司介绍、产品目录、供应商资料、证书、业务员口述、旧 PPT、Excel、项目记录……普通 AI 很容易把这些内容“总结成一篇文章”，但真正给业务 Agent 使用时会出现几个问题：

- 公司级、工厂级、产品级、项目级信息混在一起；
- 临时报价、某客户特批被误写成长期能力；
- 新旧资料冲突时不知道哪条有效；
- 认证 / 产能 / 测试能力被错误扩大范围；
- AI 推测被混进正式事实；
- 公司信息越来越长，重复越来越多；
- 不同 Agent 各自保存一份公司背景，后续容易版本不一致；
- 下游 Agent 不知道去哪里读取“已经清洗过的正式公司信息”。

这个 Skill 的目标是同时解决“怎么清洗”和“清洗后放哪里、其他 Agent 怎么找到”。

## 最直接的使用效果

- **浓缩**：把大量资料压缩成高信号 Company Pack，而不是保留所有原文。
- **分层**：区分公司 / 工厂 / 产品 / 市场 / 证书持有人 / 项目 / 客户范围。
- **去重**：同一事实只保留一个清晰版本，同时保留来源。
- **冲突检查**：新旧资料冲突时不擅自选答案，标记并要求确认。
- **防污染**：客户价格、单项目 MOQ、一次性老板特批不会进入长期公司知识。
- **可追溯**：重要事实保留来源、更新时间和 superseded 关系。
- **可维护**：支持新建、增量更新、审计、迁移和压缩已有公司知识。
- **统一存储**：正式脱敏 Pack 放在固定 `company-data/packs/` 路径。
- **可发现**：其他 Agent 先读 `company-data/REGISTRY.yaml` 就能知道有哪些公司、对应 Pack 在哪里。
- **可直接消费**：读取正式 Pack 不需要重新运行 Curation Skill。
- **可插拔**：可被外贸 Business AI、销售 AI、采购 AI、内部知识 Agent 等复用。

## Repository data contract｜本仓库的数据约定

```text
Company-Knowledge-Curation-Skill/
├── SKILL.md
├── COMPANY_PACK_SPEC.md
├── ...
└── company-data/
    ├── README.md
    ├── REGISTRY.yaml
    ├── inbox/
    │   └── README.md
    ├── pending/
    │   └── README.md
    └── packs/
        ├── README.md
        └── <company-id>/
            ├── PACK.yaml
            ├── INDEX.md
            ├── COMPANY_PROFILE.md
            ├── PRODUCT_CAPABILITIES.md
            ├── SUPPLY_CHAIN_MODEL.md
            ├── COMPLIANCE_BOUNDARIES.md
            ├── MARKETS_AND_CUSTOMERS.md
            ├── BUSINESS_SOP.md
            ├── SOURCES.md
            └── products/
```

路径含义：

- `company-data/inbox/` — 待清洗的脱敏原始 / 中间资料入口；
- `company-data/pending/` — 已发现但尚未正式写入 Pack 的更新候选；
- `company-data/packs/` — **正式、已清洗、已审核、可供其他 Agent 读取的公司知识**；
- `company-data/REGISTRY.yaml` — 所有可用 Company Pack 的总索引。

本仓库约定只存放适合共享的**抽象化 / 脱敏公司知识**。真实客户隐私、真实敏感商业数据、账号信息等不应进入这里。

## 支持的 5 种工作模式

| Mode | 用途 |
|---|---|
| `BUILD` | 从 0 把原始公司资料整理成 Company Pack |
| `UPDATE` | 用新资料更新已有 Company Pack |
| `PATCH` | 把已批准的公司信息候选转成正式更新 |
| `AUDIT` | 检查已有公司知识的重复、冲突、范围错误、过期风险 |
| `MIGRATE` | 把旧格式 / 其他 Agent 的公司资料迁移到标准 Pack |

## 标准流程

```text
RAW SOURCES / APPROVED UPDATE
        ↓
Extract facts
        ↓
Scope classification
        ↓
Deduplicate + conflict check
        ↓
CONFIRMED / TO_CONFIRM / EXCLUDED
        ↓
Review Draft
        ↓
Operator correction / approval
        ↓
company-data/packs/<company-id>/
        ↓
Update company-data/REGISTRY.yaml
```

**任何正式写入动作都应经过操作者确认。**

## 其他 Agent 怎么用？

有两种方式。

### A. 只读取公司背景

不需要运行本 Skill，只需要：

```text
读取 company-data/REGISTRY.yaml
→ 找目标 company-id
→ 打开对应 pack_path/INDEX.md
→ 按任务加载需要的文件
```

例如客户开发 Agent 可能加载 `COMPANY_PROFILE.md + MARKETS_AND_CUSTOMERS.md + PRODUCT_CAPABILITIES.md`；合规 Agent 可能只加载 `COMPLIANCE_BOUNDARIES.md + SOURCES.md`。

### B. 需要新建 / 更新公司信息

宿主 Agent 调用本 Skill 的 BUILD / UPDATE / PATCH / AUDIT / MIGRATE 模式，先产生 Review Draft，用户确认后再写入 `company-data/packs/<company-id>/` 并更新 Registry。

详见 `INTEGRATION.md`。

## 输出不是“一篇公司介绍”

一个正式 Company Pack 默认拆分为：

```text
company-data/packs/<company-id>/
├── PACK.yaml
├── INDEX.md
├── COMPANY_PROFILE.md
├── PRODUCT_CAPABILITIES.md
├── SUPPLY_CHAIN_MODEL.md
├── COMPLIANCE_BOUNDARIES.md
├── MARKETS_AND_CUSTOMERS.md
├── BUSINESS_SOP.md
├── SOURCES.md
└── products/
```

这样下游 Agent 可以按任务选择性加载，而不是每次把整份公司资料塞进上下文。

## 什么会被拒绝进入长期 Company Knowledge？

默认不进入：

- 某客户专属价格；
- 某订单 / 某项目 MOQ；
- 一次性老板特批；
- 临时供应商报价；
- 单次加急交期；
- 单项目付款条件；
- 单项目测试结论；
- 客户 PO、条码、包装版本；
- AI 自己的推测；
- 没有证据支持的“公司能力”。

这些通常属于 Customer / Project Memory，而不是 Company Pack。

## 主要文件

- `SKILL.md` — Skill 的正式执行协议
- `WORKFLOW.md` — BUILD / UPDATE / PATCH / AUDIT / MIGRATE 流程
- `SCOPE_RULES.md` — 公司 / 工厂 / 产品 / 项目 / 客户范围判断
- `FACT_RULES.md` — 事实状态、冲突和 supersession 规则
- `COMPANY_PACK_SPEC.md` — 标准输出格式与固定数据路径
- `INTEGRATION.md` — 如何接到其他 Agent / Harness，以及只读消费方式
- `company-data/` — 本 Skill 的正式公司知识数据区
- `templates/` — 空白 Company Pack 模板
- `examples/` — 抽象示例
- `schemas/` — Pack / Registry / Update Candidate 数据约定
- `evals/` — 防乱编、错分范围、错误写入的测试

## Safety / fact boundary

本 Skill 不应该：

- 把推断自动写成事实；
- 用模型常识替代公司来源；
- 把工厂能力扩大成整个公司所有项目能力；
- 把证书持有者范围扩大；
- 自动覆盖冲突事实；
- 没有用户确认就正式更新 Company Pack；
- 把客户 / 项目隐私放进长期公司知识；
- 把未脱敏敏感数据当成可共享 Company Pack 发布。

## Version

Current baseline: **V1.1 standalone skill + company knowledge hub**.

核心目标不是保证不同模型输出一模一样，而是保持同样的：事实纪律、范围判断、审核边界、Company Pack 结构，以及统一可发现的数据入口。