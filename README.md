# xiaodu-prompt

一个面向 Codex / AI 编码协作场景的公共工作流模板仓库。

这个仓库的目标很直接：

- 帮你快速搭建一套可复制的项目规则流
- 让新项目从需求、设计、技术文档开始，而不是直接开写
- 给你一套可扩展的“主代理编排、子代理执行”协作方式
- 提供一个真实示例，方便你理解模板怎么落到项目里

## 适合谁

- 想给 Codex 配一套稳定工作流的人
- 希望项目从 PRD、设计文档、技术文档开始的人
- 想把“旧版本留档、在新目录开发”这套机制固定下来的人
- 想让 AI 输出更像团队研发流程，而不是零散对话的人

## 你能得到什么

- 一套全局规则入口
- 一套项目级模板文件
- 一套文档模板
- 一套工作流资产模板
- 一个真实案例：Skillify

## 3 步快速开始

1. 先看 [docs/getting-started.md](docs/getting-started.md)，了解最小上手流程。
2. 从 [templates](templates) 复制全局模板和项目模板到你的环境。
3. 再去看 [workflow](workflow) 里的全局规则，按你的项目需要做替换。

## 仓库结构

- [workflow](workflow)
  - 全局规则、全局技能和通用工作流资产
- [templates](templates)
  - 可以直接复制的模板文件
- [docs](docs)
  - 公开说明文档
- [examples/skillify](examples/skillify)
  - 真实案例，用来展示模板如何落地

更详细的目录解释见 [docs/repo-structure.md](docs/repo-structure.md)。

## 公开入口

- 全局规则入口：[workflow/global-agents/AGENTS.md](workflow/global-agents/AGENTS.md)
- 全局技能入口：[workflow/global-skill/xiaodu-propmt/SKILL.md](workflow/global-skill/xiaodu-propmt/SKILL.md)
- 通用工作流总览：[workflow/WORKFLOW.md](workflow/WORKFLOW.md)
- 模板入口：[templates](templates)
- 示例入口：[examples/skillify](examples/skillify)

## 如何复制到你自己的项目

建议按这个顺序做：

1. 在你的工作区创建 `<YOUR_PROJECT>-old` 和 `<YOUR_PROJECT>-new`
2. 把项目模板复制到 `-new`
3. 把全局模板复制到你的 Codex 全局规则位置
4. 按占位符替换项目名、路径、仓库地址和角色说明
5. 用 PRD、设计文档、技术文档启动第一轮开发

详细替换说明见 [docs/customization-guide.md](docs/customization-guide.md)。

## 示例项目

Skillify 被保留为一个真实示例，但它不是主模板。

你应该先用模板起项目，再看示例理解“模板在真实项目中会长成什么样”。示例入口见 [examples/skillify/README.md](examples/skillify/README.md)。

## 常见问题

### 这个仓库是不是你个人本地同步仓库？

不是。这个公开仓库现在按公共模板库整理，不包含你必须照搬的个人本地路径和私有同步习惯。

### 我需要完全照抄 Skillify 吗？

不需要。Skillify 是案例，不是模板本体。

### 我能只用其中一部分吗？

可以。你可以只用全局规则，也可以只用项目模板，或者两者一起用。

### 后续规则升级怎么办？

看 [docs/upgrade-guide.md](docs/upgrade-guide.md)。
