# Agent 入口矩阵

编辑前先看本矩阵。

| 请求类型 | 先读 | 常用命令 |
|---|---|---|
| 理解/解释代码 | `AGENTS.md`、`docs/README.md`、`docs/architecture.md` | `rg`、`find`、定向读文件 |
| 新增功能 | `docs/current-capabilities.md`、owner contract | `[tests]`、`[contract checks]` |
| 修 Bug | failing test/log、`docs/error-handling.md`、owner contract | 复现、窄测试、相关全量门禁 |
| UI 改动 | `docs/frontend-agent-contract.md` | `[frontend checks]`、browser smoke |
| 数据/model 改动 | `docs/model-contract.md` | `[migration check]`、`[model tests]` |
| 部署改动 | `docs/deployment.md` | `[render check]`、`[smoke]` |
| 规则/config 改动 | 唯一真源文档 | `[generate]`、`[parity tests]` |
| Review | `.vibe/review-checklist.md` | 只使用当前门禁结果 |

## 默认调查顺序

1. 读 `AGENTS.md`。
2. 读被修改表面的 owner doc。
3. 用 `rg` 查现有模式。
4. 找到唯一真源。
5. 在所属边界做最小改动。
6. 跑 targeted verification。
7. 报告修改文件和实际运行门禁。

## 停下来问用户的条件

只有以下情况才停下来问：

- 多种产品行为都合理，且无法从文档推断。
- 破坏性操作会删除用户数据或重写历史。
- 缺少必要凭据或外部系统，且没有本地替代验证。
