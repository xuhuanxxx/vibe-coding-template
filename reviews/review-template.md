# Review：[主题]

日期：[YYYY-MM-DD]
Reviewer：[姓名/工具]
对象：[分支 / PR / commit / 文件范围 / 部署路径]
Review 类型：[代码 / 架构 / UI / 数据 / 部署 / 安全 / 文档]
基线：[base branch / commit / 环境 / 数据分区，如适用]

## 结论

[一句话结论：发现 N 个 blocker / high / medium / low；或“未发现阻断问题，剩余风险是 …”。]

## Findings

> Findings 必须放在前面，按严重程度排序。每条 finding 都必须能被当前仓库或当前命令输出复核。

### F-001 [Severity] [标题]

状态：[open / fixed / won't fix / needs info]
类别：[bug / regression / security / architecture / contract / performance / test gap / docs]
Owner boundary：[应负责修复的模块、层或契约，不写具体 patch]

证据：

- 文件/行号：`[path:line]`
- 命令输出：`[command] -> [关键输出]`
- 数据样本：`[table/partition/row/sample id]`
- 截图/页面：`[path or URL]`

复现方式：

```bash
[最小复现命令，或写“静态证据即可复核”]
```

影响：

[说明会导致什么实际问题：用户可见回归、数据错误、权限绕过、部署失败、契约漂移、测试盲区等。]

为什么这是当前问题：

[说明它违反了哪个当前契约、当前代码路径或当前运行时事实。避免使用旧报告或未来计划作为证据。]

建议修复边界：

[指出应在哪个 owner boundary 修复，例如 service、model contract、deployment render、UI selector contract。不要写逐行 patch 指令。]

验证要求：

- [修复后必须通过的测试、contract check、smoke 或数据校验。]

## 无问题区域

如果某些范围已检查且未发现问题，记录在这里：

| 范围 | 检查方式 | 结论 |
|---|---|---|
| [path/surface] | [manual/code/test] | [未发现问题 / 风险较低] |

## 验证记录

只记录本次 review 实际运行的命令，不复用旧结果。

| 命令 | 结果 | 备注 |
|---|---|---|
| `[command]` | pass/fail/not run | [关键输出或阻塞原因] |

未运行但相关的门禁：

| 命令 | 未运行原因 | 剩余风险 |
|---|---|---|
| `[command]` | [原因] | [风险] |

## 未决问题

- [需要产品、架构、数据 owner 或运维确认的问题；没有则写“无”。]

## 范围外

- [本次 review 明确没有覆盖的范围。]

## 摘要

[简短背景和 review 范围补充。不要在这里隐藏 finding；finding 必须在前面。]
