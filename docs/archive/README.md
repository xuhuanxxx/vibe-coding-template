# 文档归档

本目录存放历史文档。除非 active doc 明确引用，否则这里的内容不应指导当前实现。

## 什么时候归档

满足任一条件就应该归档：

- 功能、部署路径或 API 已退休。
- Proposal 被拒绝或被新方案替代。
- 文档是事故、调研、一次性分析快照，不是持续系统行为。
- 文档会误导 agent 复活过期路径。

不要归档：

- 当前行为的 owner contract。
- 临时关闭但仍计划恢复的活跃路径。
- 仍在被当前实现直接消费的文档。

归档文档时，建议在文档顶部加短说明：

```text
归档日期：YYYY-MM-DD
原因：[completed/rejected/superseded/retired]
当前 owner doc：[path]
```
