# Skillify Workflow

## Purpose

本文件定义 Skillify 中大型任务的默认执行流程。

固定模式是：

- 主代理负责编排
- 子代理负责执行
- 主代理负责集成、验证和汇报

本文件与 `AGENTS.md` 配合使用，`docs` 目录中的三份基线文档是流程的长期事实源。

## Baseline Constraints

- 只在 `Skillify-new` 中工作。
- `Skillify-old` 在晋升确认前保持不动。
- 默认遵守 `xiaodu-propmt`。
- 若信息不足，先报告缺口再实施。

## Documentation Gate

### Canonical Docs

重要基线文档如下：

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

1. 重新读取三份基线文档。
2. 在汇报中说明引用了哪些文档。
3. 明确产品、设计、技术是否存在不一致。
4. 若存在不一致，先更新文档再继续实施。

## Project Start Document Pipeline

对于新项目、新模块簇或结构性改版，主代理在进入实施前必须先走文档生成链路。

固定顺序如下：

1. 收集用户的产品需求输入
2. 产出并确认 PRD
3. 基于 PRD 产出并确认设计文档
4. 基于 PRD + 设计文档产出并确认技术文档
5. 将三份文档纳入 `docs` 基线
6. 再进入拆解、派单和实施

规则要求：

- 文档生成必须分节点与用户对齐，不能一轮倾倒全部长文档
- 关键对齐节点至少包括：
  - 产品定位与目标用户
  - 核心场景与业务闭环
  - 页面与交互方向
  - 技术边界与演进路线
- 如果关键节点尚未对齐，不得继续生成下一份文档，也不得提前实施
- 文档确认后，后续实现和验收都必须引用这三份文档

## GitHub Upload Buffer

项目根目录新增本地 GitHub 上传缓冲区：

- `D:\Skillify\github-upload`

用途：

- 集中保存项目级与全局级工作流规则快照
- 作为后续 GitHub 上传前的统一取件点

固定顺序：

1. 更新源文件
2. 同步到 `github-upload`
3. 检查差异
4. 再决定是否同步到外部 GitHub 仓库

## Fixed Delivery Pipeline

1. 验证目录对
   - 确认 `Skillify-old` 与 `Skillify-new` 都存在。
   - 确认当前目标目录是 `Skillify-new`。

2. Ground in the repo
   - 检查当前代码、文档、配置和约束。
   - 判断任务是小、中还是大。
   - 若处于重要里程碑，先执行文档回看门禁。
   - 若属于新项目或结构性新阶段，先执行项目启动文档生成链路。

3. 判断是否需要派单
   - 小任务可以由主代理直接完成。
   - 中大型任务默认先派给子代理。

4. 启动拆解
   - 先调用 `task-distributor` 做任务拆解。
   - 要求输出边界、依赖、completion condition 和并发建议。

5. 锁规格
   - `product-manager` 收口范围与验收标准。
   - `ui-designer` 收口页面层级和高风险交互。
   - `api-designer` 在前后端边界不清时先锁接口契约。
   - 若文档尚未齐全，则先补齐 PRD、设计文档和技术文档，再进入宽实施。

6. 派发执行
   - 每个工作单元只给一个 owner。
   - 优先使用专职角色，不重复派重叠职责。
   - 保持并发任务的写入范围互不冲突。

7. 集成
   - 主代理整合子代理结果。
   - 解决冲突、边界错位和集成缝隙。
   - 若关键路径只剩一个小补丁，主代理可直接补位。

8. 验证
   - 运行最小但足够证明主链路的检查。
   - 必要时用 `gstack-review`、`gstack-qa`、`gstack-browse`。

9. 汇报
   - 说明派了什么、落了什么、验证了什么、还有什么风险。

## Default Role Mapping

### Planning and framing

- `task-distributor`
  - 拆解工作、定义依赖、最大化安全并发
- `product-manager`
  - 锁范围、验收标准、now / next / later
- `business-analyst`
  - 归一输入、抽取需求基线
- `project-manager`
  - 管理节奏与依赖顺序

### Design and frontend

- `ui-designer`
  - 页面结构、视觉方向、关键交互
- `frontend-developer`
  - 路由、页面、组件、状态与交互实现
- `ui-fixer`
  - 小范围 UI bug 或视觉补丁

### Backend and integration

- `backend-developer`
  - 服务端逻辑、业务行为、接口实现
- `api-designer`
  - 接口契约、边界与兼容性
- `payment-integration`
  - 支付流程、状态机、回调、对账边界

### Research and mapping

- `search-specialist`
  - 搜索源文件和事实来源
- `code-mapper`
  - 梳理执行路径、模块归属和当前实现

## Critical Role Handling

以下角色在对应任务中视为关键角色：

- `task-distributor`
- `ui-designer`
- `frontend-developer`
- `backend-developer`
- `payment-integration`
- `api-designer`

若关键角色缺失或不可用到影响推进：

1. 先检查 `C:\Users\29552\.codex\agents`。
2. 再检查官方内置角色。
3. 若仍无合适角色，必须先告诉用户：
   - 缺失角色
   - 缺失原因
   - 是否还能继续
   - 降级方案
   - 风险

不允许静默降级。

## Concurrency Rules

- 默认并发 `2` 条子任务。
- 不再默认放出 `4-6` 条并发任务。
- 只有满足以下条件时才允许短时升到 `3`：
  - 最近没有出现 `429 Too Many Requests`
  - 第 3 个代理是轻量只读分析型
  - 第 3 个代理不阻塞主线
- 只并行写入范围不重叠的任务。
- 不要同时让 UI 设计和前端实现写同一路径。
- 不要让两个实现者同时写同一模块。
- 使用“一条主链 + 若干侧链”，不要把所有链路同时压满。

## Phase-Based Dispatch

### Phase A：拆解阶段

- 只启动 `task-distributor`
- 不与其他规划代理并发

### Phase B：规格锁定阶段

- 同时最多 `2` 个子代理
- 推荐组合：
  - `product-manager` + `ui-designer`
  - `product-manager` + `api-designer`
  - `business-analyst` + `code-mapper`

### Phase C：实现阶段

- 同时最多 `2` 个写入型子代理
- 推荐组合：
  - 一个前端实现者
  - 一个后端或支付实现者
- 第 3 个代理只有在满足“无近期 429 + 只读分析 + 不阻塞主线”时才允许

### Phase D：集成阶段

- 默认停止继续并发派单
- 主代理负责集成、对齐、验证
- 只在发现明确缺口时，再派 `1` 个补丁型代理

## Rate Limit Handling

### 首次 `429 Too Many Requests`

- 立即停止继续 spawn 新代理
- 等待 `60-90` 秒
- 只重试 `1` 次
- 重试时必须缩小 prompt 上下文，不再大段 `fork_context`

### 第二次 `429 Too Many Requests`

- 活跃并发立即降到 `1`
- 余下任务改为顺序执行
- 主代理汇报必须说明：
  - 哪个角色限流
  - 已采取的降级措施
  - 哪些任务改为串行
  - 对时效的影响

### 不允许的做法

- 遇到 `429` 后继续批量 spawn
- 不说明就静默删除子任务
- 让主代理无边界接管全部大任务实现

## Main Agent Override Rule

主代理可以直接下场实现，但只限这些情况：

- 任务很小且边界清晰
- 集成是唯一缺口
- 派单结果卡住主线
- 冲突解决必须在同一个上下文完成

如果补位原因是关键角色缺失，必须先向用户说明。

## Waiting Strategy

- 不频繁 wait。
- 只有主线依赖结果时才等待。
- 子代理执行期间，主代理优先做：
  - 验收脚本准备
  - 风险检查
  - 集成方案准备
  - 文档与实现的对齐
- 若刚发生 `429`，优先停止继续派单并收缩上下文，而不是继续堆并发。

## Prompt and Thread Hygiene

- `fork_context: true` 只在明确需要完整线程上下文时使用。
- 默认优先传递：
  - 文件路径
  - 已确认事实摘要
  - 明确输出物
- 对已存在的子代理，优先复用而不是重复 spawn。
- 每个子代理只承接一个边界清晰的任务。
- 已完成或空闲的代理应及时关闭。

## Skill Usage Guide

按任务阶段推荐：

- 产品探索：`gstack-office-hours`
- 范围压力测试：`gstack-plan-ceo-review`
- 工程方案锁定：`gstack-plan-eng-review`
- 设计方案锁定：`gstack-plan-design-review`
- 预合并检查：`gstack-review`
- 浏览器验证与 QA：`gstack-browse`、`gstack-qa`、`gstack-qa-only`

## Validation Expectations

每次较大任务收尾至少要说明：

1. 本轮做了什么
2. 哪些工作由子代理完成
3. 变更了什么
4. 验证了什么
5. 还存在哪些风险
6. 是否建议晋升

最小验证应覆盖：

- 变更相关的语法或类型安全
- 主链路是否可走通
- 一个高风险边界条件
- 一个可能的用户可见回归点

## Project-End Rules

- 项目结束时必须做复盘。
- 复盘要记录：
  - 新瓶颈
  - 缺失角色
  - 弱提示词
  - 值得固化的流程变化
- 若流程变化落地，需同步更新本文件、`AGENTS.md` 和必要的基线文档。

## Workflow Artifact Reminder

工作流文件更新后，仍按 `xiaodu-propmt` 规则处理备份：

- 先同步到 `D:\Skillify\github-upload` 中的对应快照
- 同步到 `xiaodu-prompt` 备份仓库
- 先 commit
- push 需等待用户确认
