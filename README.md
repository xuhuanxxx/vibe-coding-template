# Vibe Coding 项目模板

这套模板用于把一个仓库整理成适合 AI coding agent、人工 reviewer 和长期维护者协作的工程工作区。

它不绑定具体技术栈。复制到新项目或已有项目后，把占位内容替换成项目真实契约即可。

## 目标

- Agent 能从仓库事实恢复上下文，而不是依赖聊天记录。
- 架构边界以可执行契约存在，而不是口头约定。
- 当前能力、历史方案、遗留路径清晰分离。
- 验证命令按变更类型映射。
- UI、API、数据、部署契约足够稳定，可被自动化检查。

## 建议接入步骤

1. 把本目录内容复制到目标仓库根目录。
2. 先填写 `AGENTS.md`，保持短、准、可执行。
3. 填写 `docs/current-capabilities.md`，只写当前事实。
4. 在大改前补齐 `docs/architecture.md` 和 `docs/constraints.md`。
5. 把真实检查命令写进 `scripts/check-contracts` 和 `scripts/verify-local`。
6. 把过期计划、旧报告、废弃路径移入 archive。

## 文件地图

| 路径 | 用途 |
|---|---|
| `AGENTS.md` | AI agent 和 reviewer 的日常操作手册。 |
| `docs/README.md` | 按读者问题组织的文档索引。 |
| `docs/architecture.md` | 系统分层、依赖方向、扩展点。 |
| `docs/constraints.md` | 必须遵守的工程规则和禁止事项。 |
| `docs/current-capabilities.md` | 当前能力地图和明确的非能力。 |
| `docs/documentation-governance.md` | 文档目录、spec、ADR、review、归档规则。 |
| `docs/model-contract.md` | 数据、API、资源、命名、真源契约。 |
| `docs/frontend-agent-contract.md` | UI 稳定 selector 和 browser agent 验收规则。 |
| `docs/deployment.md` | 本地预览、生产路径、发布、回滚、smoke。 |
| `docs/error-handling.md` | 异常、重试、日志、降级边界。 |
| `docs/pitfalls.md` | 静态检查无法覆盖的运行时坑。 |
| `specs/spec-template.md` | 需求/方案 spec 模板。 |
| `docs/adr/0000-template.md` | ADR 模板。 |
| `reviews/review-template.md` | Review 文档模板。 |
| `.vibe/project-map.md` | 给人和 agent 的高信号项目地图。 |
| `.vibe/agent-entrypoints.md` | 任务类型到入口文档/命令的映射。 |
| `.vibe/review-checklist.md` | Review 和完成前检查清单。 |

## 原则

Vibe coding 不是让 AI 更自由地乱写，而是让仓库更容易被正确理解、局部修改、确定性验证、语义化 review 和安全回滚。
