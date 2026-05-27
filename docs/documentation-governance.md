# 文档治理

本文定义项目文档如何分工。每类文档的具体写法由对应目录或模板自己负责，避免读者在多个文档之间来回跳转。

## 1. 文档类型

| 类型 | 作用 | 推荐路径 | 时间语义 |
|---|---|---|---|
| 当前事实 | 系统现在做什么 | `docs/`、`specs/current/` | 现在时 |
| 契约 | 实现必须遵守的规则 | `docs/*-contract.md`、`docs/constraints.md` | 现在时 |
| Spec | 计划中或已接受的变更 | `specs/proposed/`、`specs/current/` | 实现前偏未来时 |
| ADR | 持久决策及其理由 | `docs/adr/` | 过去做出的决策，当前仍有约束力 |
| Review | 一次 review 的证据快照 | `reviews/current/` | review 当时的快照 |
| Runbook | 如何操作活跃路径 | `docs/deployment.md`、`docs/runbooks/` | 现在时 |
| 归档 | 历史、退休、废弃、已完成材料 | `docs/archive/`、`specs/archive/`、`reviews/archive/` | 历史事实 |

## 2. 文档 Owner 分工

| 主题 | Owner 文档 | 不放在这里的内容 |
|---|---|---|
| 项目日常操作入口 | `AGENTS.md` | 完整架构说明、详细文档治理规则 |
| 文档目录和分工 | `docs/documentation-governance.md` | 具体 spec/review/ADR 模板正文 |
| 当前产品和运行时能力 | `docs/current-capabilities.md` | 未来计划、历史调研 |
| 架构分层和依赖方向 | `docs/architecture.md` | 临时实施步骤 |
| 必须遵守的工程规则 | `docs/constraints.md` | 背景解释、历史方案 |
| 数据/API/资源命名 | `docs/model-contract.md` | 页面视觉规范、部署细节 |
| UI 自动化语义 | `docs/frontend-agent-contract.md` | 后端业务写入实现 |
| 部署和回滚 | `docs/deployment.md` | 本地业务开发指南 |
| 异常、重试、降级 | `docs/error-handling.md` | 具体事故复盘 |
| 隐式运行时陷阱 | `docs/pitfalls.md` | 已进入硬约束的规则全文 |
| Spec 生命周期和写法 | `specs/README.md`、`specs/spec-template.md` | 当前行为 owner 文档 |
| Review 生命周期和写法 | `reviews/README.md`、`reviews/review-template.md` | 实施计划 |
| ADR 生命周期和写法 | `docs/adr/README.md`、`docs/adr/0000-template.md` | 任务计划、临时 TODO |

## 3. 推荐目录结构

```text
docs/
  README.md
  architecture.md
  constraints.md
  current-capabilities.md
  documentation-governance.md
  deployment.md
  error-handling.md
  pitfalls.md
  model-contract.md
  frontend-agent-contract.md
  adr/
    README.md
    0001-short-title.md
  runbooks/
    production-incident.md
  archive/
    README.md

specs/
  README.md
  current/
    accepted-or-in-progress-spec.md
  proposed/
    draft-spec.md
  archive/
    completed-or-rejected-spec.md

reviews/
  README.md
  current/
    2026-01-01-topic-review.md
  archive/
    2026-01-01-topic-review.md
```

规则：

- Active docs 只描述当前事实或正在推进的 active work。
- 历史计划完成或废弃后，不继续留在 active docs。
- 生命周期不直观的目录应放 `README.md`。
- 小改动优先更新 owner doc，不要为每个小变化新建文档。

## 4. 是否需要区分当前和历史

需要。只要这个区分会影响实现、review、部署或 agent 行为，就必须区分 current 和 legacy。

放在 current 的内容：

- 生产能力。
- 已接受且正在实现的 spec。
- 仍有未解决发现的 review。
- 活跃路径的 runbook。
- 当前代码必须遵守的契约。

放在 legacy 或 archive 的内容：

- 退休功能。
- 被取代的计划。
- 已完成的实施计划。
- 问题已修复或关闭的旧 review。
- 不应默认指导新实现的历史研究。

标准目录名优先使用 `archive`。只有项目已有强约定，或内容仍被 legacy runtime path 消费时，才使用 `legacy`。

## 5. 归档分工

归档规则由各目录 README 负责：

- `docs/archive/README.md` 负责普通文档归档。
- `specs/README.md` 和 `specs/archive/README.md` 负责 spec 生命周期。
- `reviews/README.md` 负责 review 生命周期。

通用原则：

- 当前行为的 owner doc 不归档。
- 归档材料不应默认指导新实现。
- 归档前先把仍然有效的事实迁移到 owner doc。

## 6. 实施完成后的文档更新顺序

Spec 落地后：

1. 把持久行为写入 owner docs。
2. 更新 `docs/current-capabilities.md`。
3. 如果命令或 agent 行为变化，更新 `AGENTS.md`。
4. 按项目约定把 spec 移到 `specs/archive/` 或标记 complete。
5. 如果 ADR 决策仍约束当前行为，ADR 保持 active。
