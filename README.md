# xiaodu-prompt / Skillify Upload Workspace

本目录现在作为 Skillify 项目内的本地 git 上传仓位使用。

它承担两类同步内容：

- `workflow/`
  - 全局工作流规则快照
- `skillify/workflow/`
  - Skillify 项目级工作流规则和基线文档快照

## 使用原则

- 源文件仍然是唯一编辑入口
- 规则更新后，先更新源文件，再同步到本仓位
- 本仓位用于本地 commit、分支管理和云端 push
- 默认先推送到专用分支，再决定是否合并到远端主分支

## 当前远端

- `git@github.com:xiaodu295521/xiaodu-prompt.git`

## 当前同步结构

- `workflow/WORKFLOW.md`
- `workflow/global-agents/AGENTS.md`
- `workflow/global-skill/xiaodu-propmt/SKILL.md`
- `skillify/workflow/AGENTS.md`
- `skillify/workflow/WORKFLOW.md`
- `skillify/workflow/docs/*`

详见 `MAPPING.md`。
