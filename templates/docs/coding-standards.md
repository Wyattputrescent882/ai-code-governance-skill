# Coding Standards

本文件定义 AI 生成代码必须遵守的编码标准。

## 命名规则

- 组件：`PascalCase`，如 `PaymentMask.vue`。
- Hooks / Composables：`useXxx`，如 `usePoints.ts`。
- Service：`xxx.service.ts`，如 `payment.service.ts`。
- Store：`xxx.store.ts`，如 `auth.store.ts`。
- Utils：按功能命名，如 `date.ts`、`validators.ts`。
- Types：按领域命名，如 `user.ts`、`chat.ts`。

## 文件长度

- 单文件超过 300 行必须考虑拆分。
- 单函数超过 60 行必须考虑拆分。
- 组件模板过长时，优先拆子组件。
- 重复逻辑出现第三次时，必须抽象。

## TypeScript 规则

- 禁止滥用 `any`。
- 优先使用显式类型。
- API 响应类型必须定义在 `src/types/`。
- 公共函数必须有清晰输入输出类型。
- 不允许复制粘贴相似 interface。

## 错误处理

- API 错误统一通过 `src/utils/error.ts` 或请求层处理。
- 不允许空 `catch`。
- 不允许吞掉错误。
- 用户可见错误文案应集中管理。

## 样式规则

- 颜色、字号、间距优先使用设计 token。
- 不允许在多个文件硬编码相同样式值。
- 业务组件不得私自定义新的视觉体系。

## 注释规则

- 只为复杂业务约束写注释。
- 不写解释显而易见代码的注释。
- TODO 必须说明原因和后续处理方式。
- 不保留“临时”“后续再改”“备用方案”注释。

## 测试规则

- 公共 utils 应优先补充单元测试。
- 复杂 hooks / services 应补充测试。
- 修复 Bug 时优先补回归测试。
- 不允许删除测试来通过检查。
