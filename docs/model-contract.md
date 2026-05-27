# 模型和资源契约

本文定义数据关系、API 字段、资源名称、路由、权限、派生产物和 UI resource type 的真源。

## 1. 关系原则

强关系必须有显式真源：

- 决定身份、归属、生命周期或状态。
- 参与权限、状态流转、筛选、排序、聚合或导出。
- 带有业务字段，例如角色、金额、生效日期、范围或独占性。
- 需要数据库约束，例如唯一性、XOR、非空或外键。

弱关系只能表达补充引用、附件、备注或低频关联。

通用 JSON 字段只用于稀疏逃生口。字段一旦参与查询、排序、权限或运营判断，就应该升格。

## 2. 唯一真源表

| 概念 | 唯一真源 | 派生输出 | 契约检查 |
|---|---|---|---|
| [concept] | `[file/table/service]` | `[generated/API/UI]` | `[command]` |
| [concept] | `[file/table/service]` | `[generated/API/UI]` | `[command]` |

## 3. 命名契约

| 层 | 名称 |
|---|---|
| 领域概念 | `[Name]` |
| 数据库表或存储 key | `[name]` |
| API route | `/api/[name]` |
| API object type | `[object_type]` |
| Permission resource | `[resource]` |
| Frontend resource type | `[ResourceType]` |
| UI route | `/[route]` |
| 派生产物 | `[path]` |

规则：

- 一个概念只保留一个活跃名称。
- 代码路径中避免历史别名。
- 展示文案可以使用业务口语，但代码契约使用 canonical name。

## 4. 派生属性

| 派生字段 | 来源 | 规则 |
|---|---|---|
| [field] | [source] | [rule] |

除非有明确性能、历史事实或审计理由，不要落库存储派生字段。若必须存储，定义刷新和对账规则。

## 5. 迁移和兼容

- Schema 变更必须有显式 migration。
- Backfill 必须可重复执行或明确一次性边界。
- Breaking contract change 必须列出受影响 consumer。
- Deprecated 字段需要移除计划或归档说明。
