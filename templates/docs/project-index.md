# Project Index

本文件是项目索引。AI 新增代码前必须先检查这里，确认是否已有可复用实现。

如果本文件是在项目中途新增的，必须先盘点真实项目再填写。下方条目是示例，不代表当前项目事实；复制模板后应删除不存在的路径，未知项标记为 `TBD` 或 `needs confirmation`。

## 通用组件

| 文件 | 职责 | 使用说明 |
|---|---|---|
| `src/components/base/AppButton.vue` | 统一按钮组件 | 禁止重复创建 Button |
| `src/components/base/AppModal.vue` | 统一弹窗组件 | 禁止重复创建 Modal |
| `src/components/base/AppInput.vue` | 统一输入框组件 | 禁止重复创建 Input |
| `src/components/base/LoadingState.vue` | 加载状态 | 禁止页面内重复写 loading UI |
| `src/components/base/EmptyState.vue` | 空状态 | 禁止页面内重复写 empty UI |

## 业务组件

| 文件 | 职责 | 使用说明 |
|---|---|---|
| `src/components/business/PointsPanel.vue` | 积分展示 | 积分相关页面优先复用 |
| `src/components/business/PaymentMask.vue` | 支付遮罩 | 付费解锁优先复用 |
| `src/components/business/ChatBox.vue` | 聊天输入框 | 聊天页面优先复用 |

## Hooks / Composables

| 文件 | 职责 | 使用说明 |
|---|---|---|
| `src/hooks/useAuth.ts` | 登录状态、token、用户信息 | 禁止重复管理用户状态 |
| `src/hooks/useChat.ts` | 聊天状态和发送流程 | 禁止页面直接写聊天流程 |
| `src/hooks/usePoints.ts` | 积分余额、任务、扣除 | 积分逻辑统一入口 |
| `src/hooks/usePayment.ts` | 支付、订单状态 | 支付逻辑统一入口 |

## Services

| 文件 | 职责 | 使用说明 |
|---|---|---|
| `src/services/request.ts` | 统一请求封装 | 禁止新建第二套 request |
| `src/services/user.service.ts` | 用户接口 | 用户 API 统一入口 |
| `src/services/chat.service.ts` | 聊天接口 | 聊天 API 统一入口 |
| `src/services/points.service.ts` | 积分接口 | 积分 API 统一入口 |
| `src/services/payment.service.ts` | 支付接口 | 支付 API 统一入口 |

## Stores

| 文件 | 职责 | 使用说明 |
|---|---|---|
| `src/stores/auth.store.ts` | 登录和用户信息 | 禁止新建并行用户状态 |
| `src/stores/chat.store.ts` | 会话状态 | 禁止页面维护跨页会话 |
| `src/stores/points.store.ts` | 积分状态 | 积分统一状态源 |

## Utils

| 文件 | 职责 | 使用说明 |
|---|---|---|
| `src/utils/date.ts` | 日期格式化 | 统一使用 dayjs |
| `src/utils/storage.ts` | 本地缓存封装 | 禁止直接散落 storage 调用 |
| `src/utils/validators.ts` | 表单校验 | 禁止页面重复写校验 |
| `src/utils/error.ts` | 错误处理 | 错误提示统一入口 |
| `src/utils/url.ts` | URL 参数处理 | 禁止重复解析 URL |

## Types

| 文件 | 职责 | 使用说明 |
|---|---|---|
| `src/types/user.ts` | 用户类型 | 禁止重复定义 User |
| `src/types/chat.ts` | 聊天类型 | 禁止重复定义 Message / Session |
| `src/types/points.ts` | 积分类型 | 禁止重复定义 PointsTask |
| `src/types/payment.ts` | 支付类型 | 禁止重复定义 Order / Payment |

## 维护规则

- 新增公共组件、Hook、Service、Store、Utils、Type 后，必须更新本文件。
- 删除或重命名公共模块后，必须更新本文件。
- AI 修改代码前，必须先查本文件。
