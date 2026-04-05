# Skillify 技术文档

## 1. 文档定位

本文档采用“双轨文档”写法：

- 第一轨是当前本地前端原型的实现基线。
- 第二轨是未来接入真实认证、支付、AI 顾问和人工服务时的演进边界。

它的作用不是重复 PRD 或 UI 文档，而是把实现结构、技术边界和替换策略写清楚。

## 2. 当前原型基线

### 2.1 技术栈

当前原型使用以下栈：

- React 19
- Vite 7
- TypeScript 5
- React Router 7
- Tailwind CSS v4
- 本地状态持久化使用 `localStorage`

对应文件：

- `package.json`
- `src/app/App.tsx`
- `src/store/app-store.tsx`

### 2.2 目录结构

- `src/app`
  - 应用壳与路由
- `src/pages`
  - 页面级组件
- `src/components`
  - 布局与通用 UI 组件
- `src/features/advisor`
  - AI 顾问交互
- `src/data`
  - mock 数据与 mock 服务
- `src/store`
  - 应用状态管理
- `src/types`
  - 领域模型定义
- `src/styles`
  - 样式基线

### 2.3 路由与访问控制

当前路由定义在 `src/app/App.tsx`：

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

访问控制通过两个包装组件实现：

- `RequireAuth`
  - 未登录用户访问业务页时，跳转到 `/auth`
- `RequireCompleteProfile`
  - 已登录但未补全另一种联系方式时，跳转到 `/complete-profile`

当前开放页：

- `/`
- `/auth`
- `/faq`

其余业务页都要求登录，且大多数要求资料补全。

### 2.4 状态架构

全局状态由 `src/store/app-store.tsx` 提供。

实现方式：

- React Context
- `useReducer`
- `localStorage` 持久化

持久化 key：

- `skillify-demo-state`

当前状态域：

- `session`
- `user`
- `packages`
- `advisorConversations`
- `customRequirements`
- `orders`
- `payments`

### 2.5 Store Action

当前 reducer 支持以下 action：

- `LOGIN`
- `COMPLETE_PROFILE`
- `UPSERT_CONVERSATION`
- `ADD_CUSTOM_REQUIREMENT`
- `ADD_ORDER`
- `UPDATE_ORDER`
- `UPSERT_PAYMENT`
- `RESET_DEMO`

补充说明：

- 登录后会自动创建默认顾问会话 `main-advisor`。
- 页面刷新后，`localStorage` 中的状态会重新 hydrate。
- `packages` 每次 hydrate 时会以 `servicePackages` 为准，避免本地篡改。

### 2.6 领域类型

领域类型定义在 `src/types/models.ts`，当前基线包含：

- `ContactChannel`
- `AdvisorRole`
- `OrderType`
- `PaymentStatus`
- `FulfillmentStatus`
- `SessionState`
- `User`
- `ServicePackage`
- `AdvisorMessage`
- `AIConversationSession`
- `CustomRequirement`
- `Order`
- `Payment`
- `HomeSection`
- `FaqItem`
- `AppState`

当前关键实体语义：

- `SessionState`
  - 登录态、当前用户、首选登录方式、资料是否补全
- `User`
  - 手机号、邮箱、验证状态、昵称、头像
- `ServicePackage`
  - 场景方案名称、适用对象、亮点、交付内容、周期、价格
- `AIConversationSession`
  - 顾问会话上下文、推荐方案、摘要、消息记录
- `CustomRequirement`
  - 自定义需求表单内容及状态
- `Order`
  - 订单类型、金额、支付状态、服务状态、创建时间
- `Payment`
  - 支付渠道、金额、状态、交易号、支付时间

说明：`FulfillmentStatus` 与部分中文文案目前存在编码问题，业务语义应以本文档与产品文档为准。

### 2.7 mockData

静态 mock 数据位于 `src/data/mockData.ts`，当前包含：

- `demoCode`
  - 演示验证码，固定为 `246810`
- `homeSections`
  - 首页分屏内容
- `servicePackages`
  - 4 类场景方案：
    - 内容创作
    - 私域运营
    - 客服响应
    - 资料整理
- `faqItems`
  - FAQ 问答内容

### 2.8 mockServices

交互逻辑与本地服务函数位于 `src/data/mockServices.ts`，当前接口包括：

- `sendPhoneCode`
- `sendEmailCode`
- `verifyPhoneLogin`
- `verifyEmailLogin`
- `completeProfile`
- `createOrder`
- `createCustomRequirement`
- `mockPayOrder`
- `buildAdvisorReply`
- `createInitialConversation`

这些函数仅在前端内部工作，不发起真实网络请求。

### 2.9 关键页面与流程映射

#### 登录与补全联系方式

对应文件：

- `src/pages/AuthPage.tsx`
- `src/pages/CompleteProfilePage.tsx`

流程：

1. 用户在 `/auth` 选择手机号或邮箱登录。
2. 点击发送验证码后进入 60 秒倒计时。
3. 验证成功后写入 `LOGIN`。
4. 若缺少另一种联系方式，则跳转 `/complete-profile`。
5. 补全成功后触发 `COMPLETE_PROFILE`，进入 `/solutions`。

#### 方案选购与 AI 顾问

对应文件：

- `src/pages/SolutionsPage.tsx`
- `src/features/advisor/AdvisorPanel.tsx`

流程：

1. 从 `packages` 中读取 4 类方案。
2. 用户切换当前关注方案。
3. 顾问根据当前方案和用户输入生成推荐回复。
4. 顾问会话通过 `UPSERT_CONVERSATION` 持久化。
5. 用户可直接购买方案，或跳转自定义方案页。

#### 自定义需求收集

对应文件：

- `src/pages/CustomPlanPage.tsx`

流程：

1. 用户填写场景、目标、预算、工具、周期、备注。
2. 系统生成 `CustomRequirement`。
3. 同时生成 `Order`，订单类型为 `custom`。
4. 跳转支付确认页。

#### mock 支付与订单回写

对应文件：

- `src/pages/CheckoutPage.tsx`
- `src/pages/PaymentResultPage.tsx`
- `src/pages/OrdersPage.tsx`
- `src/pages/OrderDetailPage.tsx`

流程：

1. 支付确认页允许选择微信支付或支付宝。
2. 用户可模拟成功、失败、取消三种结果。
3. 系统通过 `UPDATE_ORDER` 与 `UPSERT_PAYMENT` 回写状态。
4. 支付结果页、订单列表、订单详情页读取本地状态展示结果。

### 2.10 当前实现限制

- 无真实后端。
- 无真实短信服务。
- 无真实邮件服务。
- 无真实支付能力。
- AI 顾问是脚本式推荐，不是真实模型服务。
- 订单与支付状态机较轻，仅服务于原型演示。
- 移动端 AI 顾问抽屉目前还是设计目标，不是完整实现。
- 源码存在中文乱码，当前文档是语义基线。

## 3. 当前实现与设计边界

以下能力属于已实现：

- 路由守卫与访问控制
- 本地会话管理
- 本地订单创建
- 本地支付状态切换
- 本地顾问会话持久化

以下能力属于设计目标或未来能力，不应视为已实现：

- 移动端底部顾问抽屉
- 真实验证码网关
- 真实微信支付与支付宝回调
- 真实 AI 模型推理服务
- CRM 与人工服务后台

## 4. 未来生产演进

### 4.1 服务边界建议

正式版本建议按以下边界拆分：

- 前端站点层
  - 页面渲染、交互状态、结果展示
- 认证层
  - 手机验证码、邮箱验证码、登录注册、会话管理
- 订单层
  - 套餐信息、订单创建、订单状态、订单查询
- 支付层
  - 微信支付、支付宝、支付回调、对账
- AI 顾问层
  - 会话上下文、推荐逻辑、模型调用、风控控制
- CRM / 人工跟进层
  - 线索跟进、服务分配、交付记录、人工接管

### 4.2 mockService 到真实 API 的替换策略

替换原则：

- 页面路由和核心业务流尽量保持不变。
- 页面层不直接耦合真实接口细节。
- `mockServices` 的调用位点可以保留，逐步替换为 API service。
- 若后端字段最终调整，优先通过适配层处理，避免页面直接感知。

推荐分层：

- `page` 层处理交互和导航
- `service` 层处理请求与响应映射
- `store` 层只保存前端需要的稳定结构

### 4.3 认证演进

正式认证需要覆盖：

- 手机验证码发送与频率控制
- 邮箱验证码发送与频率控制
- 登录注册统一入口
- token 或 cookie 会话管理
- 联系方式补全校验
- 手机号与邮箱绑定到同一用户主体

关键边界：

- “补全另一种联系方式”必须是服务端可审计状态，不能只靠前端布尔值。
- 账号合并、重复绑定、重新验证要有明确定义。

### 4.4 支付演进

正式支付需要覆盖：

- 微信支付下单
- 支付宝下单
- 前端拉起支付
- 异步回调验签
- 订单状态机
- 支付结果对账
- 退款与异常处理

建议拆分状态：

- 支付状态：
  - `pending`
  - `processing`
  - `success`
  - `failed`
  - `cancelled`
  - `refunded`
- 服务状态：
  - 待支付
  - 已支付
  - 待沟通
  - 需求确认中
  - 交付中
  - 已交付
  - 已完成
  - 已退款

### 4.5 AI 顾问演进

从脚本式顾问升级到真实模型服务时，需要明确：

- 会话上下文保存策略
- 方案推荐是规则优先还是模型优先
- 预算、场景、周期等结构化字段的抽取方式
- 哪些问题必须升级人工
- 如何避免模型承诺超出实际服务范围

建议边界：

- AI 顾问负责售前推荐和需求摘要。
- 人工顾问负责复杂需求判断、报价确认、交付承接。
- 高风险承诺、价格确认、交付范围确认必须可人工兜底。

### 4.6 CRM 与人工跟进演进

正式版本建议增加：

- 线索池
- 人工顾问接管记录
- 联系方式与触达记录
- 订单交付进度
- 需求确认纪要

这样可以把“网站前台成交”和“人工服务承接”真正连接起来。

### 4.7 工程与运维要求

接真实服务后应补齐：

- 环境变量分层管理
- 前端埋点
- 后端业务日志
- 错误追踪
- 关键链路监控
- 支付与认证操作审计
- 接口速率限制与风控
- 移动端性能和弱网可用性保障

## 5. 阶段演进路线

### 阶段一：本地原型

- 目标：完整演示商业闭环。
- 特征：前端 mock，无真实外部服务。

### 阶段二：可接真实服务

- 目标：在不大改前端体验的前提下接入真实认证和支付。
- 特征：`mockServices` 被 API service 替换，订单与支付开始进入真实状态管理。

### 阶段三：正式商用

- 目标：形成稳定的售前咨询、支付成交、人工交付闭环。
- 特征：接入真实 AI 顾问、CRM、监控、安全与运营工具。

## 6. 与其他基线文档的关系

- 产品文档定义业务目标、功能边界和页面验收。
- UI 文档定义页面结构、视觉风格和关键交互。
- 本文档定义实现结构、当前技术边界和未来替换路径。

若三者发生冲突，先更新产品和 UI，再修正技术文档。
