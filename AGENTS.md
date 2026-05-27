# AGENTS.md

本文是给 AI coding agent 的日常操作手册，不是完整 README，也不是完整架构文档。这里只保留高频入口、硬约束、验证命令和常见任务路径。

当启动方式、目录边界、契约、配置、验证流程或本文引用文档变化时，必须同步更新本文。

## 1. 项目定位

一句话：

> [描述项目做什么、服务谁、运行在哪里。]

非目标：

- [本项目明确不提供的能力。]
- [不应复活的历史路径或诱人但错误的抽象。]

主要技术栈：

- Runtime：[语言 / 框架 / 版本]
- Storage：[数据库 / 对象存储 / 缓存 / 队列]
- Frontend：[如适用]
- Deployment：[本地预览路径和生产发布路径]

必读入口：

- 文档索引：`docs/README.md`
- 架构：`docs/architecture.md`
- 工程约束：`docs/constraints.md`
- 当前能力：`docs/current-capabilities.md`
- 文档治理：`docs/documentation-governance.md`
- 模型/API/资源契约：`docs/model-contract.md`
- 部署：`docs/deployment.md`
- 异常处理：`docs/error-handling.md`
- 运行时陷阱：`docs/pitfalls.md`

## 2. 快速启动

本地预览：

```bash
[本地预览启动命令]
```

健康检查：

```bash
[health check 命令]
[readiness check 命令]
```

开发循环：

```bash
[安装依赖命令]
[dev server 或 watcher 命令]
```

本地账号，如有：

```text
[仅本地使用的账号，或写 none]
```

## 3. 硬约束

### 3.1 唯一真源

- `[配置/规则/schema/文件]` 是 `[领域]` 的唯一真源。
- 派生产物必须通过 `[生成命令]` 生成。
- 除非正在修改生成器，否则不得手改生成文件。

### 3.2 代码边界

- 可复用领域逻辑放在 `[path]`，不要放在 `[entrypoint path]`。
- 框架绑定放在 `[path]`。
- 外部 SDK 封装放在 `[path]`。
- 一次性探索脚本放在 `[gitignored scratch path]`。
- 同一能力不得保留两条活跃实现路径。

### 3.3 API、数据和安全

- [认证/鉴权边界。]
- [事务/幂等/审计边界。]
- [错误响应或异常契约。]
- 密钥只能来自环境变量、Secret Manager 或平台 Connection。
- 日志不得输出 token、password、private key、webhook URL 或原始凭据。

### 3.4 文档纪律

- 当前事实进入 active docs。
- 历史方案进入 archive。
- Review 文档只记录发现和证据，不写猜测式 patch 计划。

### 3.5 Worktree 和 Git 纪律

- 默认使用当前 checkout，除非明确需要隔离。
- history rewrite 或 squash 前先创建 backup 分支。
- 大型跨模块改动应拆成语义化 commit。
- 不得回退用户的无关改动。

## 4. 验证

完成前默认门禁：

```bash
[主验证命令]
```

常用 targeted gates：

```bash
[lint 命令]
[typecheck 命令]
[unit test 命令]
[contract check 命令]
[build 命令]
```

变更类型矩阵：

| 如果修改 | 必跑 |
|---|---|
| 数据模型 / schema | `[migration check]` + `[model tests]` |
| API 契约 | `[api tests]` + `[client generation/check]` |
| UI / frontend | `[frontend check]` + browser smoke |
| 部署 | `[deployment render/check]` + smoke |
| 规则 / 派生产物 | `[generate]` + `[parity/contract tests]` |
| 热路径 / 容量敏感逻辑 | `[benchmark/load check]` |

未在本轮实际运行的门禁，不能报告为通过。无法运行时，说明具体阻塞和剩余风险。

## 5. 常见任务

### 5.1 新增资源或实体

1. 先看 `docs/model-contract.md`。
2. 在所属层添加 model/schema/config。
3. 按需添加 migration 或更新派生产物。
4. 添加 permission、route、registry 或 metadata。
5. 添加聚焦测试。
6. 运行 targeted verification gate。

### 5.2 新增外部集成

1. 添加 client wrapper，并使用结构化异常。
2. 只在 integration/framework 层添加 hook/binding。
3. service 层承载业务逻辑，不泄漏框架对象。
4. 补 connection/resource 文档。
5. 添加 mock 测试；有真实凭证时跑一次真实 smoke。

### 5.3 修 Bug

1. 复现问题或定位失效契约。
2. 添加或更新最小长期测试。
3. 在所属边界修复，不只修表层症状。
4. 先跑窄测试，再跑相关项目门禁。

## 6. Review 摘要

- 文件路径和行号，或命令输出。
- 本轮实际门禁结果。
- 如果验证不完整，说明准确的剩余风险。

优先关注架构、唯一真源、契约、行为回归和缺失测试。
