# Architecture Contract

本文件定义项目架构白名单。AI 只能在此架构内完成需求，不得自由引入第二套方案。

如果本文件是在项目中途新增的，先根据真实项目结构填写。下方内容是模板示例，不代表当前项目事实。

## 技术栈

按项目实际情况填写。未知项标记为 `TBD` 或 `needs confirmation`，不要猜测：

```text
框架：uni-app / Vue 3 / React / Next.js / Taro / 其他
语言：TypeScript
状态管理：Pinia / Zustand / Redux / 其他
请求层：src/services/request.ts
日期处理：dayjs
表单校验：src/utils/validators.ts / zod / yup / 其他
样式系统：src/styles/tokens.scss / Tailwind / CSS Modules / 其他
测试：Vitest / Jest / Playwright / 其他
```

## 推荐目录结构

```text
src/
  pages/
  components/
    base/
    business/
  hooks/
  services/
  stores/
  utils/
  types/
  styles/
```

## 分层规则

### pages

页面层只负责：

- 页面布局。
- 用户交互。
- 调用 hooks / stores。
- 绑定展示数据。

页面层禁止：

- 直接调用 API。
- 直接写复杂业务规则。
- 直接操作复杂 storage。
- 写大量表单校验逻辑。

### components

组件层只负责：

- UI 展示。
- 输入输出。
- 局部交互。

组件层禁止：

- 直接调用 API。
- 直接修改全局业务状态。
- 内嵌复杂业务流程。

### hooks

Hooks / Composables 负责：

- 页面组合逻辑。
- 复用交互流程。
- 调用 services / stores / utils。

### services

Services 负责：

- API 请求。
- 请求参数适配。
- 响应数据适配。
- 错误归一化。

Services 禁止：

- 依赖 UI 组件。
- 直接操作页面状态。

### stores

Stores 负责：

- 全局状态。
- 用户信息。
- 会话状态。
- 权限状态。
- 积分、订单、支付等跨页面状态。

Stores 禁止：

- 写 UI 细节。
- 直接拼复杂页面文案。

### utils

Utils 负责纯函数：

- 日期格式化。
- 字符串处理。
- 数字处理。
- 校验规则。
- URL 解析。

Utils 禁止：

- 依赖 store。
- 依赖 UI。
- 包含副作用。

## 硬性限制

- 不允许新建第二套请求封装。
- 不允许新建第二套日期处理。
- 不允许新建第二套表单校验。
- 不允许新建重复 UI 基础组件。
- 不允许绕过设计系统硬编码样式。
- 不允许把业务逻辑堆进页面。
