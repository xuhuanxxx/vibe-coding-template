# 异常处理

本文定义每一层负责 raise、catch、retry、log 或 degrade 什么错误。目标是失败发生时，能快速定位责任层。

## 1. 分层职责

| 层 | 抛出 | 捕获 | 日志 |
|---|---|---|---|
| Domain/model | 校验错误或业务规则错误 | 不捕获 | 不打日志 |
| Client | 结构化 client 异常 | 只捕获可重试 transport 错误 | retry 时 warning |
| Repository | 透传 client/storage 错误 | 不捕获 | 不打日志 |
| Service | 业务语义错误 | 捕获已知低层错误并翻译 | 决策点 info/warn/error |
| Entry/framework | 框架 terminal/skip 错误 | 转换为框架语义 | 使用框架 logger |

## 2. 结构化异常

Client 和集成异常应暴露字段，不只拼字符串：

```python
class ExternalAPIError(Exception):
    def __init__(self, *, operation: str, status: int, code: str, message: str):
        self.operation = operation
        self.status = status
        self.code = code
        self.message = message
        super().__init__(f"{operation} failed: status={status} code={code} message={message}")
```

测试应断言 `exc.code` 等字段，而不是断言字符串片段。

## 3. 重试和降级

| 错误类型 | 示例 | 处理方式 |
|---|---|---|
| 校验/配置错误 | 缺少必填字段 | Fail fast |
| 认证/权限错误 | Forbidden 或无效凭据 | Fail fast，除非支持 refresh |
| Transport 错误 | Timeout、429、5xx | Client retry，再交给 task/request retry |
| 业务 API 错误 | Range 越界、名称重复 | 翻译成领域错误 |
| 通知/报告失败 | 次要通道不可用 | 若业务结果已记录，可软降级 |

## 4. 日志规则

- 应用日志不使用 `print()`。
- 不记录 secret、token、password、webhook URL 或原始凭据。
- 不静默吞错。
- re-raise 的路径上不要重复打印同一堆栈。
- 有 request id、job id、run id 或类似 correlation id 时必须带上。

## 5. 公开错误形状

如果项目暴露 API，使用统一公开错误形状：

```json
{
  "error": {
    "code": "string",
    "message": "string",
    "request_id": "string",
    "details": {}
  }
}
```
