# Reviews

Review 文档是证据快照，不是 spec，也不是实施计划。

## 目录

| 目录 | 含义 |
|---|---|
| `current/` | 仍有未解决发现，或近期仍在 active follow-up 的 review。 |
| `archive/` | 发现已修复、被拒绝或已经过期的 review。 |

## 写作规则

- 顶部必须写清评审范围、评审基线和本轮门禁状态。
- Commit hash 必须能通过 `git cat-file -t <hash>` 验证。
- 当前结论必须基于当前仓库事实，避免只写“优秀”“良好”这类不可复核总评。
- 发现列表放在“当前问题”章节，按严重程度排序。
- 每条发现必须有可复核证据：文件行号、命令输出、日志、数据样本或截图。
- 只使用本次 review 实际运行的命令结果。
- 不写猜测式实施指令。
- 如果没发现问题，要明确说明，并列出剩余测试缺口。
- Review 只记录“当前问题”和“剩余风险”，不把未来计划当作缺陷证据。
- 建议写到 owner boundary 层级，例如 service、model contract、deployment render、UI selector contract，不写逐行 patch。
- 已修复历史问题、误报和当前仍存在的问题必须分开写。
- 建议项必须说明它解决的是当前缺陷、维护性风险，还是历史归档说明。

## 推荐结构

1. 基线和门禁。
2. 当前结论。
3. 已确认的工程基础。
4. 当前问题。
5. 已修复历史问题和误报。
6. 剩余风险和范围外。
7. 未决问题。
8. 摘要。

## Severity

| 级别 | 含义 |
|---|---|
| Blocker | 会导致发布不可用、数据破坏、安全绕过、主流程失败，必须先修。 |
| High | 明确行为回归、重要契约破坏、生产风险高。 |
| Medium | 局部功能错误、测试缺口、可维护性问题，应该修但不一定阻断发布。 |
| Low | 文档、命名、轻微一致性问题，不影响主要行为。 |

## Finding 必备字段

每条 finding 至少包含：

- 严重程度和标题。
- 状态：`open / fixed / false positive / accepted risk / needs info`。
- 类别：bug、regression、security、architecture、contract、performance、test gap、docs。
- Owner boundary。
- 问题。
- 证据。
- 影响。
- 最小修复。
- 理想修复。
- 实际处理。
- 验证要求。

## 生命周期

- 仍有未解决发现时，放在 `current/`。
- 发现全部修复、关闭或不再适用后，移到 `archive/`。
- 如果 review 结论已经被当前 owner docs 吸收，保留归档即可，不继续在 active docs 里重复维护。
