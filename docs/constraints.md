# 工程约束

约束是必须遵守的规则，不是建议。违反约束应视为 bug 或 review blocker。

## 0. 变更纪律

- 编辑前先读 `AGENTS.md`、本文和对应 owner contract。
- 边界或命令变化时，文档必须同改动一起更新。
- Bug fix 必须添加最小长期测试。
- 从所属抽象修复问题，不围绕症状打补丁。
- 对废弃的活跃路径，优先删除或归档，不保留“也许还能用”的选项。

## 1. 代码边界

| 区域 | 路径 | 规则 |
|---|---|---|
| 入口 | `[path]` | 只做编排，不承载可复用业务逻辑。 |
| Domain/Model | `[path]` | 纯领域规则，不依赖框架或 I/O。 |
| Services | `[path]` | 应用行为，不泄漏 UI 或框架细节。 |
| Clients | `[path]` | SDK 薄封装，使用结构化异常。 |
| Infrastructure | `[path]` | 技术原语，不承载业务语义。 |
| Tests | `[path]` | 覆盖被修改行为。 |
| Scratch | `[ignored path]` | 临时脚本，不作为生产依赖。 |

## 2. 唯一真源

- `[规则/配置/model]` 是 `[领域]` 的唯一真源。
- `[生成文件/路径]` 是派生产物，必须通过 `[命令]` 生成。
- `[runtime registry/API/schema]` 负责 `[能力发现]`。
- 如果两个 active source 冲突，先修唯一真源边界。

## 3. 运行时和副作用

- import 阶段不得调用外部 API。
- import 阶段不得查询运行时元数据。
- import 阶段不得执行昂贵计算。
- 长任务必须放在明确的运行时入口。
- 跨步骤 artifact 必须使用文档化契约。

## 4. 配置和密钥

- 环境变量只能在 `[config owner path]` 读取。
- 密钥不得存入普通数据库字段，除非项目明确设计了加密 secret storage。
- Connection/authentication 配置必须和业务 resource id 分离。
- 可运行时编辑的设置必须有明确 consumer 和 reload 语义。

## 5. API 和数据契约

- 公开错误必须遵守 `[error shape]`。
- 写操作必须经过认证、鉴权、校验、事务、幂等和审计边界。
- 强关系需要显式字段、外键或专用关系表。
- 通用 JSON 或弱关系表是逃生口，不是核心可查询 schema。

## 6. UI 和自动化契约

- 有稳定语义 selector 时，测试不得依赖展示文案、DOM 顺序或坐标。
- UI selector 是契约，改动时必须检查。
- Browser automation 验证体验；业务写入仍必须经过 API 和后端保护。

## 7. Git 和 Review

- 不得回退用户的无关改动。
- 大改动拆成语义化 commit。
- history rewrite 前创建 backup 分支。
- Review 发现必须使用当前证据，不复用旧报告。
