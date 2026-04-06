# Skillify Workflow

## Purpose

这份文件定义 Skillify 的默认研发流程。核心原则很简单：

- 先留好可回退版本，再开始改
- 先把需求讲清楚，再进入实现
- 主代理负责拆解、协调、集成和汇报
- 子代理负责边界清晰的具体执行

## Baseline Constraints

- 只在 `Skillify-new` 中开发。
- `Skillify-old` 保存“本轮开始前”的完整基线快照。
- 每次新的开发轮次开始前，必须先把 `Skillify-new` 完整同步到 `Skillify-old`。
- 如果还没完成这一步，不应继续修改 `Skillify-new`。
- 默认遵守 `xiaodu-propmt`。

## Step 0：先做 `new -> old` 基线同步

每次开始以下工作前，都先执行这一步：

- 新功能开发
- 较大的修复
- 规则更新
- 架构调整
- 发布前收口

同步原则：

- 覆盖源码、文档、配置、静态资源
- 不必复制 `node_modules`、构建产物、缓存目录
- 目标是让 `Skillify-old` 成为“本轮开工前的完整版本”

## Documentation Gate

### Canonical Docs

项目正式基线文档：

- `docs/01-product-requirements.md`
- `docs/02-ui-design-spec.md`
- `docs/03-technical-architecture.md`

### Milestone Re-read Rule

以下节点视为重要里程碑：

- 新的大功能或新页面簇启动前
- 涉及架构边界变化的实现前
- 接入真实外部服务前
- QA、验收、准备发布前

到达这些节点时，主代理必须：

1. 重新读取三份基线文档
2. 在汇报中说明引用了哪些文档
3. 说明产品、设计、技术是否一致
4. 若不一致，先更新文档再继续

## Project Start Document Pipeline

新项目、新模块或大阶段启动前，先走文档链路：

1. 收集用户的产品需求
2. 产出并对齐 PRD
3. 基于 PRD 产出并对齐设计文档
4. 基于 PRD 和设计文档产出并对齐技术文档
5. 将三份文档纳入 `docs` 基线
6. 再进入拆解、派单和实现

执行要求：

- 不能一次性把整套长文全部甩给用户
- 必须分节点对齐
- 如果某个关键节点没对齐，不进入下一份文档，也不直接开做

## User-Facing Communication Rule

面向用户发送以下内容时，默认用通俗中文：

- 实施计划
- 方案说明
- 阶段汇报
- 风险说明
- 验证结果

表达要求：

- 先讲“这件事会带来什么结果”
- 再讲“为什么要这样做”
- 最后再讲“技术上怎么做”
- 能不用术语就不用术语
- 必须用术语时，补一句白话解释

## Fixed Delivery Pipeline

1. 验证目录
- 确认 `Skillify-old` 和 `Skillify-new` 都存在
- 确认本轮先完成了 `new -> old` 基线同步
- 确认真正实施目录是 `Skillify-new`

2. 在仓库里做 grounding
- 检查当前代码、文档、配置和约束
- 判断任务是小、中还是大
- 若处于里程碑，先回看基线文档

3. 判断是否需要先走文档
- 如果是新模块、新页面簇或结构性阶段，先走 PRD -> 设计 -> 技术文档
- 如果只是小修或已有基线内的实现，直接进入拆解与实施

4. 启动拆解
- 先调用 `task-distributor`
- 要求输出边界、依赖、完成条件和并发建议

5. 锁规格
- `product-manager` 收口范围和验收标准
- `ui-designer` 收口页面结构和关键交互
- `api-designer` 在接口边界不清时先锁契约

6. 派发执行
- 每个子任务只有一个 owner
- 默认并发 `2`
- 写入范围不重叠才允许并行

7. 主代理集成
- 整合子代理结果
- 解决冲突
- 补必要的小缺口

8. 验证
- 至少跑与本轮相关的最小主链路验证
- 需要时使用 `gstack-review`、`gstack-qa`、`gstack-browse`

9. 汇报
- 用用户能看懂的话说明：
  - 本轮做了什么
  - 为什么这样做
  - 验证结果如何
  - 还剩什么风险

## Default Role Mapping

### Planning

- `task-distributor`：拆工作、定边界、排依赖
- `product-manager`：收口范围和验收标准
- `business-analyst`：归一输入、提炼需求
- `project-manager`：协调节奏和依赖顺序

### Design and Frontend

- `ui-designer`：页面层级、视觉方向、关键交互
- `frontend-developer`：页面、组件、状态、交互实现
- `ui-fixer`：小范围 UI 补丁

### Backend and Integration

- `backend-developer`：服务端逻辑和接口实现
- `api-designer`：接口契约和演进边界
- `payment-integration`：支付流程、回调、状态机

### Research and Mapping

- `search-specialist`：快速搜源文件和事实位置
- `code-mapper`：梳理代码路径和模块归属

## Critical Role Handling

如果关键角色缺失或不可用，且已经影响推进，必须先告诉用户：

- 缺了哪个角色
- 为什么它对当前任务关键
- 当前还能不能继续
- 可选降级方案是什么
- 风险是什么

不允许静默降级。

## Concurrency Rules

- 默认并发 `2`
- 不再默认一次放出 `4-6` 个代理
- 只有在以下条件都满足时才允许短时提升到 `3`
  - 最近没有 `429`
  - 第 3 个代理是只读轻量分析
  - 第 3 个代理不阻塞主线

## Phase-Based Dispatch

### Phase A：拆解阶段

- 只启 `task-distributor`

### Phase B：规格锁定阶段

- 同时最多 `2` 个代理
- 常见组合：
  - `product-manager` + `ui-designer`
  - `product-manager` + `api-designer`
  - `business-analyst` + `code-mapper`

### Phase C：实现阶段

- 同时最多 `2` 个写入型代理
- 同一路径、同一模块、同一页面簇禁止并发写入

### Phase D：集成阶段

- 默认本地集成
- 只有发现明确缺口时，再派 `1` 个补丁代理

## Rate Limit Handling

### 第一次 `429`

- 停止继续 spawn
- 等待 `60-90` 秒
- 只重试一次
- 缩小 prompt 上下文

### 第二次 `429`

- 并发降到 `1`
- 剩余任务改为串行
- 汇报里明确说明限流影响

## Prompt and Thread Hygiene

- `fork_context: true` 不默认开启
- 优先传文件路径、事实摘要、明确输出物
- 已有代理优先复用
- 完成或空闲的代理及时关闭

## GitHub Upload Buffer

- `D:\Skillify\github-upload` 是规则快照缓冲区
- 工作流文件更新顺序固定为：
  1. 更新源文件
  2. 同步到 `github-upload`
  3. 检查差异
  4. 再决定是否同步到云端仓库

## Validation Expectations

每轮较大任务收尾时，至少说明：

1. 本轮做了什么
2. 本轮开始前是否完成了 `new -> old` 快照
3. 哪些工作由子代理完成
4. 改了哪些关键文件
5. 验证结果如何
6. 还剩哪些风险

## Project-End Rules

- 项目结束时要做复盘
- 复盘要记录：
  - 新瓶颈
  - 缺失角色
  - 弱提示词
  - 值得固化的流程变化

## Workflow Artifact Reminder

工作流文件更新后：

- 先同步到 `D:\Skillify\github-upload`
- 再按既有规则决定是否同步到云端仓库
- 本地可先 commit
- push 仍等待用户确认
