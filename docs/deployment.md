# 部署

本文定义可执行的本地和生产路径。删除已经不支持的 active path，不要把它们作为“备选方案”继续写在当前文档里。

## 1. 选择入口

| 目标 | 入口 |
|---|---|
| 本地开发 | `[command]` |
| 本地全栈预览 | `[command]` |
| 多实例或拓扑预览 | `[command]` |
| 生产发布 | `[command/platform]` |
| 回滚 | `[command/platform]` |

## 2. 本地预览

```bash
[start command]
[health command]
[readiness command]
```

本地预览语义：

- [Migration 行为。]
- [Seed/reference data 行为。]
- [本地账号。]
- [端口和 URL。]

## 3. 生产路径

生产真源：

- Manifest/config 位于 `[path]`。
- Render/apply 命令是 `[command]`。
- Migration 或一次性 Job 先于应用 rollout 运行。
- App 容器启动时不执行副作用，除非明确设计如此。

生产必需设置：

- [数据库/缓存/队列/对象存储设置。]
- [认证/安全设置。]
- [日志/可观测性设置。]
- [Secret 来源。]

## 4. 验证

```bash
[render/check command]
[smoke command]
[logs command]
```

依赖、schema 或运行时契约未就绪时，readiness 必须提前失败。不要把 readiness 问题拖到用户页面才暴露。

## 5. 回滚

回滚步骤：

1. [步骤]
2. [步骤]
3. [步骤]

注意：应用回滚不自动回滚数据迁移。Migration 应尽量向后兼容。
