---
name: xiaodu-propmt
description: 全项目默认流程：手动双目录、信息不足先确认、技能/子代理规则、工作流云端备份
---

# Project Workflow Standard

## 默认行为
- 后续所有新项目默认使用本流程。
- 每个项目启动时，用户手动创建 `<project>-old` 与 `<project>-new` 两个目录。
- 所有改动只在 `-new` 进行；确认前不改 `-old`。

## 目录识别规则（强制）
1. AI 开始实施前必须先识别双目录。
2. 若当前目录是 `*-new`，自动匹配同级 `*-old`。
3. 若当前目录是 `*-old`，自动匹配同级 `*-new`。
4. 若目录缺失、命名不符合规则、或匹配不唯一，必须先和用户确认后再继续。

## 强制规则
1. 阶段前信息检查：若信息不足，先输出缺失项、阻塞原因、建议默认方案，等待确认后继续。
2. 技能调用：用户点名技能或任务明显匹配技能时，必须调用并说明用途。
3. 子代理策略：
   - 小项目：默认单人，先给是否启用建议。
   - 中/大项目：默认主代理负责编排，子代理负责具体执行。
   - 中/大项目启动时，默认先调用 `task-distributor` 做任务拆解，再按边界派单。
   - 子代理优先使用 `C:\Users\29552\.codex\agents` 中的自定义角色，官方内置角色只作兜底。
   - 默认并发强度为 4-6 条，只允许非重叠写入范围并行。
   - 若缺少关键子代理角色导致项目无法按既定方式推进，必须先向用户说明缺失角色、阻塞原因、可选降级方案与风险，不能静默降级。
   - 主代理仅在关键路径被阻塞时允许亲自补位，不默认吞掉大块实现工作。
4. UI 改动：先给预览，再改代码。
5. 每轮结束：必须有验证结论（语法/核心路径/关键异常）。
6. 仅在用户确认后执行 `new -> old` 晋升。

## 工作流云端备份（强制）
当以下文件更新后，必须执行 GitHub 备份：
- `WORKFLOW.md`
- `workflow-templates/SKILL.md`
- `workflow-templates/PROMPT.txt`
- `workflow-templates/RETRO_TEMPLATE.md`
- `workflow-templates/WORKFLOW_CHANGELOG.md`
- 当前全局技能 `xiaodu-propmt/SKILL.md`

备份仓库：`git@github.com:xiaodu295521/xiaodu-prompt.git`

备份映射：
- `workflow/WORKFLOW.md`
- `workflow/templates/*`
- `workflow/global-skill/xiaodu-propmt/SKILL.md`
- `workflow/global-agents/AGENTS.md`

备份规则：
1. `pull -> sync -> diff -> commit -> (用户确认) -> push`
2. 无差异时报告“无备份更新”。
3. push 失败不影响本地流程文件，仅报告并保留本地提交。

## 可选工具
- 可使用：`C:\Users\29552\.codex\skills\xiaodu-propmt\sync_workflow_backup.ps1`
- 作用：自动执行同步与本地提交；推送阶段仍遵守“确认后 push”。

## 项目收尾（可演进）
- 项目结束必须复盘：新难点、遗漏点、规则新增/修改/删除建议。
- 按复盘更新流程版本并写入变更记录。

## 每轮固定输出
1. 本轮目标
2. 信息充足性检查
3. 技能使用情况
4. 子代理使用情况
5. 改动摘要
6. 验证结果
7. 风险与待确认项
8. 是否建议晋升（`new -> old`）

