# xiaodu-prompt / Skillify Upload Workspace

这个目录是 Skillify 项目在本地的 GitHub 上传缓冲仓库。

它承担两类同步内容：

- `workflow/`
  - 全局工作流规则快照
- `skillify/workflow/`
  - Skillify 项目级工作流规则和基线文档快照

## 使用原则

- 源文件仍然是唯一编辑入口
- 规则更新后，先更新源文件，再同步到本仓库
- 本仓库用于本地 commit、分支管理和后续云端 push
- 默认先推到专用分支，再决定是否合并到远端主分支

## 与 Skillify 双目录规则的关系

从现在开始，Skillify 项目进入新一轮开发前，先执行：

1. 将 `Skillify-new` 的完整项目基线同步到 `Skillify-old`
2. 再修改 `Skillify-new`
3. 若本轮涉及工作流规则更新，再同步相关规则文件到本仓库

也就是说，`old` 保存的是“开工前的完整版本”，不是空目录占位。

## 用户沟通规则

上传到这里的工作流规则，默认要求主代理在给用户发送实施计划、阶段汇报和风险说明时使用通俗中文。

## 当前远端

- `git@github.com:xiaodu295521/xiaodu-prompt.git`

## 当前同步结构

- `workflow/WORKFLOW.md`
- `workflow/global-agents/AGENTS.md`
- `workflow/global-skill/xiaodu-propmt/SKILL.md`
- `skillify/workflow/AGENTS.md`
- `skillify/workflow/WORKFLOW.md`
- `skillify/workflow/docs/*`

具体路径映射见 `MAPPING.md`。
