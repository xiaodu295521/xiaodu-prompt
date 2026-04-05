---
name: project-workflow-standard
description: 手动双目录安全机制 + 信息不足先确认 + 技能/子代理规则 + 工作流云端备份
---

# Project Workflow Standard

## 必须遵守
1. 每个项目先手动建立 `<project>-old` 与 `<project>-new`。
2. 所有改动只能在 `-new` 执行，`-old` 在确认前不得修改。
3. AI 在项目开始时必须识别双目录：
   - 当前目录为 `*-new` 时，自动匹配同级 `*-old`。
   - 当前目录为 `*-old` 时，自动匹配同级 `*-new`。
   - 若目录缺失或存在多个候选，先确认，禁止继续实施。
4. 每阶段前先检查信息是否充足；不足时先确认再继续。
5. 用户点名技能或任务匹配技能时必须调用技能。
6. 小项目先给是否启用子代理建议；中/大项目默认建议启用并最小分工。
7. UI 先预览再改代码。
8. 验证通过且用户确认后，才允许 `new -> old` 晋升。

## 工作流云端备份（强制）
当以下文件更新后，必须执行 GitHub 备份：
- `WORKFLOW.md`
- `workflow-templates/SKILL.md`
- `workflow-templates/PROMPT.txt`
- `workflow-templates/RETRO_TEMPLATE.md`
- `workflow-templates/WORKFLOW_CHANGELOG.md`
- 全局 `project-workflow-standard/SKILL.md`

备份仓库：`git@github.com:xiaodu295521/xiaodu-prompt.git`

备份映射：
- `workflow/WORKFLOW.md`
- `workflow/templates/*`
- `workflow/global-skill/project-workflow-standard/SKILL.md`
- `workflow/global-agents/AGENTS.md`

备份规则：
1. 先 pull 最新 `main`。
2. 同步文件后检查差异。
3. 无差异则结束并报告“无备份更新”。
4. 有差异先本地提交，再等待用户确认后 push。
5. push 失败不回滚本地流程文件，仅报告冲突/错误详情。

## 信息不足输出格式
- 缺失项：
- 阻塞原因：
- 建议默认方案：

## 每轮输出格式
1. 本轮目标
2. 信息充足性检查
3. 技能使用情况
4. 子代理使用情况
5. 改动摘要
6. 验证结果
7. 风险与待确认项
8. 是否建议晋升（`new -> old`）

## 项目收尾
必须做复盘，输出：
1. 新难点
2. 流程遗漏
3. 建议新增/修改/删除规则
4. 版本更新建议（`vX.Y -> vX.Y+1`）

