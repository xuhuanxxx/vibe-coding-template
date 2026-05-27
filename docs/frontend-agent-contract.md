# 前端 Agent 契约

当项目有浏览器 UI 时使用本文。它定义 browser agent 和端到端测试如何在不依赖文案、坐标或 DOM 偶然结构的情况下验证真实体验。

## 1. 页面根

重要页面应暴露稳定页面标记：

```tsx
<div data-page="[page-key]">
```

资源列表页同时暴露：

```tsx
<div data-resource-list="[resource-key]">
```

## 2. 导航

一级导航：

```tsx
<a data-nav-item="[nav-key]" data-route="/[route]">
```

上下文导航：

```tsx
<button data-contextual-nav-item="[tab-key]" data-route="/[route]">
```

规则：

- Selector key 描述稳定产品语义。
- 不使用翻译文案作为测试身份。
- `data-route` 必须匹配真实路由。

## 3. 动作、字段和区域

动作：

```tsx
<button data-action="create" data-testid="[resource].create">
```

字段：

```tsx
<input data-field="[field-name]">
```

区域：

```tsx
<section data-surface="[surface-name]">
```

机器可读状态：

```tsx
<div role="status" data-app-status="loading" className="sr-only">loading</div>
```

常用状态：

- `loading`
- `saving`
- `saved`
- `validation_error`
- `server_error`

## 4. 写入边界

Browser automation 可以验证体验、导航和渲染。业务写入仍必须经过后端 API 契约、认证、鉴权、CSRF 或等价保护、事务、幂等和审计。

## 5. 验证

```bash
[frontend typecheck/lint]
[ui contract check]
[browser smoke command]
```

最低 browser smoke：

- 首页或默认路由可渲染。
- 一级导航可用。
- 至少一个只读列表或详情页可渲染。
- 一个创建/编辑流能展示校验错误。
- 关键响应式宽度无重叠。
