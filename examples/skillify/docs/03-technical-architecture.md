# Skillify 示例技术文档

## 1. 技术定位

这个案例采用“双轨文档”方式：

- 当前轨：本地可演示前端原型
- 未来轨：后续接入真实认证、支付、AI 顾问和人工服务

## 2. 当前原型基线

### 技术栈

- React
- Vite
- TypeScript
- React Router
- Tailwind CSS

### 路由集合

- `/`
- `/auth`
- `/complete-profile`
- `/solutions`
- `/custom-plan`
- `/checkout/:orderId`
- `/payment-result/:orderId`
- `/orders`
- `/orders/:orderId`
- `/profile`
- `/faq`

### 状态模型

- `session`
- `user`
- `packages`
- `advisorConversations`
- `customRequirements`
- `orders`
- `payments`

### mock 服务

- `sendPhoneCode`
- `sendEmailCode`
- `verifyPhoneLogin`
- `verifyEmailLogin`
- `completeProfile`
- `createOrder`
- `createCustomRequirement`
- `mockPayOrder`

## 3. 当前边界

- 无真实后端
- 无真实短信或邮件服务
- 无真实支付
- AI 顾问是脚本式推荐，不是真实模型服务

## 4. 未来演进方向

- 接入真实认证服务
- 接入微信支付与支付宝
- 把 mock service 替换为真实 API
- 把脚本式顾问升级为真实模型服务
- 接入 CRM 和人工跟进链路

## 5. 这个示例想表达的通用思路

- 页面路由和业务主链路最好先固定
- 当前实现和未来演进要分开写清楚
- mock 数据结构最好先稳定，这样以后更容易接真实服务
