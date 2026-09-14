# Company Knowledge Curation Skill

A standalone, model-agnostic skill for turning messy company materials into a structured, reviewable, reusable Company Pack.

这是一个独立的 **公司信息整理 / 浓缩 / 更新 Skill**。它不是普通“总结文档”工具，而是把 PDF、PPT、Word、Excel、图片、证书、产品目录、网页导出资料，以及业务对话中已确认的新公司信息，整理成可长期复用、可追溯、可维护的公司知识。

> 核心原则：**先提取事实，再判断范围，再审核；用户确认后，才进入正式公司知识。**

## 它解决什么问题？

真实公司的资料通常散落在很多地方：公司介绍、产品目录、供应商资料、证书、业务员口述、旧 PPT、Excel、项目记录……普通 AI 很容易把这些内容“总结成一篇文章”，但真正给业务 Agent 使用时会出现几个问题：

- 公司级、工厂级、产品级、项目级信息混在一起；
- 临时报价、某客户特批被误写成长期能力；
- 新旧资料冲突时不知道哪条有效；
- 认证 / 产能 / 测试能力被错误扩大范围；
- AI 推测被混进正式事实；
- 公司信息越来越长，重复越来越多，不方便 Agent 按需调用。

这个 Skill 的作用就是把“杂乱资料”变成“可运行的公司知识”。

## 最直接的使用效果

- **浓缩**：把大量资料压缩成高信号 Company Pack，而不是保留所有原文。
- **分层**：区分公司 / 工厂 / 产品 / 项目 / 客户范围。
- **去重**：同一事实只保留一个清晰版本，同时保留来源。
- **冲突检查**：新旧资料冲突时不擅自选答案，标记并要求确认。
- **防污染**：客户价格、单项目 MOQ、一次性老板特批不会进入长期公司知识。
- **可追溯**：重要事实保留来源、更新时间和 superseded 关系。
- **可维护**：支持新建、增量更新、审计、迁移和压缩已有公司知识。
- **可插拔**：可被外贸 Business AI、销售 AI、采购 AI、内部知识 Agent 等复用。

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
Formal Company Pack
```

**任何正式写入动作都应经过操作者确认。**

## 可以读什么？

只要宿主 Agent / 平台具备对应文件读取能力，本 Skill 可处理：

- PDF
- PPT / PPTX
- Word / DOCX
- Excel / XLSX
- 图片 / 扫描件
- 证书 / 审核文件
- 产品目录
- 公司介绍
- 工厂资料
- 网页导出内容
- 业务对话中已确认的长期公司信息
- 已有 Company Pack / legacy knowledge files

Skill 本身不假装拥有宿主平台没有提供的 OCR、浏览器或文件读取能力。

## 输出不是“一篇公司介绍”

标准 Company Pack 建议拆分为：

```text
company/packs/<company-id>/
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

## 独立使用，也可以接入其他 Agent

这个仓库本身不绑定任何公司，也不绑定某个 Business AI。

推荐关系：

```text
Business / Sales / Procurement Agent
            ↓ invokes
Company-Knowledge-Curation-Skill
            ↓ produces / updates
        Company Pack
```

宿主 Agent 只需要提供：

1. 原始资料或已有 Company Pack；
2. Company Pack 的目标存储位置；
3. 用户审核 / 确认入口；
4. 所需的文件读取工具。

详见 `INTEGRATION.md`。

## 主要文件

- `SKILL.md` — Skill 的正式执行协议
- `WORKFLOW.md` — BUILD / UPDATE / PATCH / AUDIT / MIGRATE 流程
- `SCOPE_RULES.md` — 公司 / 工厂 / 产品 / 项目 / 客户范围判断
- `FACT_RULES.md` — 事实状态、冲突和 supersession 规则
- `COMPANY_PACK_SPEC.md` — 标准输出格式
- `INTEGRATION.md` — 如何接到其他 Agent / Harness
- `templates/` — 空白 Company Pack 模板
- `examples/` — 抽象示例
- `evals/` — 防乱编、错分范围、错误写入的测试

## Safety / fact boundary

本 Skill 不应该：

- 把推断自动写成事实；
- 用模型常识替代公司来源；
- 把工厂能力扩大成整个公司所有项目能力；
- 把证书持有者范围扩大；
- 自动覆盖冲突事实；
- 没有用户确认就正式更新 Company Pack；
- 把客户 / 项目隐私放进长期公司知识。

## Version

Current baseline: **V1 standalone skill architecture**.

核心目标不是保证不同模型输出一模一样，而是保持同样的：事实纪律、范围判断、审核边界和 Company Pack 结构。