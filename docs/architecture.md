# 架构

本文面向工程师、reviewer 和 AI agent，说明系统结构和稳定边界。它不需要罗列所有实现细节，但必须解释分层、依赖方向和扩展点。

## 1. 系统总览

```text
[外部用户/系统]
        |
        v
[入口层：UI/API/DAG/CLI]
        |
        v
[应用服务层]
        |
        v
[领域模型/规则层]
        |
        v
[存储/外部系统]
```

## 2. 模块布局

| 路径 | 职责 | 不应做 |
|---|---|---|
| `[path]` | [职责] | [禁止依赖或禁止行为] |
| `[path]` | [职责] | [禁止依赖或禁止行为] |
| `[path]` | [职责] | [禁止依赖或禁止行为] |

## 3. 依赖方向

允许方向：

```text
[入口/框架层] -> [services] -> [domain/models] -> [infrastructure primitives]
```

规则：

- 底层 domain/model 代码不得 import 框架运行时对象。
- 通用工具不得承载业务语义。
- 外部 client 应是薄封装，配置由所属 framework/service 层注入。
- 入口文件只做编排，不实现可复用业务逻辑。

## 4. 核心数据流

描述一次典型请求、任务、DAG run 或命令：

1. [步骤]
2. [步骤]
3. [步骤]
4. [步骤]

Artifact 和交接契约：

| 生产者 | Artifact | 消费者 | 契约 |
|---|---|---|---|
| [component] | [data/event/file] | [component] | [schema/path/key] |

## 5. 扩展点

### 新增数据源或外部系统

必改文件：

1. `[client path]`
2. `[binding/hook path]`
3. `[repository/service path]`
4. `[tests path]`
5. `[docs/config path]`

### 新增业务能力

推荐顺序：

1. 更新当前能力或 spec。
2. 添加唯一真源 config/model。
3. 添加 service 实现。
4. 添加 API/UI/job 绑定。
5. 添加验证。

## 6. 架构测试和契约检查

```bash
[检查分层或契约的命令]
```

如果项目还没有自动架构检查，当同一边界第二次被破坏时，应优先补检查脚本。
