# 文档索引

用本页判断一个事实应该归哪个文档维护。这里是索引，不承载具体规则。

| 文档 | 负责回答的问题 |
|---|---|
| `architecture.md` | 系统如何分层？依赖方向是什么？ |
| `constraints.md` | 改代码时哪些必须做、哪些禁止做？ |
| `current-capabilities.md` | 项目现在具备什么能力？明确不具备什么？ |
| `documentation-governance.md` | 文档体系如何分工？current/archive 如何区分？ |
| `model-contract.md` | 数据关系、API、资源、命名从哪里来？ |
| `frontend-agent-contract.md` | Browser agent 如何安全、稳定地验收 UI？ |
| `deployment.md` | 哪些本地和生产路径是可执行真源？ |
| `error-handling.md` | 哪一层负责 catch、raise、retry、log、degrade？ |
| `pitfalls.md` | 哪些运行时陷阱无法靠类型检查发现？ |

## 分工原则

- 本页只做索引，不维护详细规则。
- 具体契约以对应 owner 文档为准。
- 目录级生命周期由对应目录的 `README.md` 负责。
