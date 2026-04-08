# xiaodu-prompt

这是一个给 Codex / AI 编码协作场景使用的公共工作流模板仓库。

它的目标不是展示某一个项目怎么开发，而是给你一套可以直接照着配置的稳定方法：

- 新项目先从需求、设计、技术文档开始
- 实施前先保留一个可回退版本
- 主代理负责拆解、协调、验收
- 子代理负责边界清晰的具体执行
- Web 项目默认带上最小 CI 和预览环境

## 适合谁

- 想给 Codex 配一套稳定工作流的人
- 不想每开一个项目都从零想目录和规则的人
- 希望 AI 输出更接近真实研发流程的人
- 想保留一个可直接参考的示例项目的人

## 你能得到什么

- 一套全局规则入口
- 一套项目级模板文件
- 一套文档模板
- 一套工作流总览
- 一个真实示例：Skillify

## 3 步快速开始

1. 先看 [docs/getting-started.md](docs/getting-started.md)
2. 再从 [templates](templates) 复制模板到你的环境
3. 最后按 [workflow](workflow) 里的规则启动第一轮项目

## 仓库结构

- [workflow](workflow)
  - 放全局规则、全局技能和通用工作流说明
- [templates](templates)
  - 放可直接复制的全局模板、项目模板和文档模板
- [docs](docs)
  - 放上手说明、结构说明、自定义指南和升级指南
- [examples/skillify](examples/skillify)
  - 放 Skillify 这个真实案例，帮助你理解模板如何落地

更详细的目录解释见 [docs/repo-structure.md](docs/repo-structure.md)。

## 推荐阅读顺序

1. [README.md](README.md)
2. [docs/getting-started.md](docs/getting-started.md)
3. [templates](templates)
4. [workflow/WORKFLOW.md](workflow/WORKFLOW.md)
5. [examples/skillify/README.md](examples/skillify/README.md)

## 公开入口

- 全局规则入口：[workflow/global-agents/AGENTS.md](workflow/global-agents/AGENTS.md)
- 全局技能入口：[workflow/global-skill/xiaodu-propmt/SKILL.md](workflow/global-skill/xiaodu-propmt/SKILL.md)
- 通用工作流总览：[workflow/WORKFLOW.md](workflow/WORKFLOW.md)
- 模板入口：[templates](templates)
- 示例入口：[examples/skillify](examples/skillify)
- 更新说明：[CHANGELOG.md](CHANGELOG.md)

## 如何复制到你自己的项目

建议按这个顺序做：

1. 创建 `<YOUR_PROJECT>-old` 和 `<YOUR_PROJECT>-new`
2. 把项目模板复制到 `-new`
3. 把全局模板复制到你的 Codex 全局规则位置
4. 替换模板里的占位符、项目名、路径和仓库地址
5. 先写 PRD，再写设计文档，再写技术文档，然后再进入开发

详细替换说明见 [docs/customization-guide.md](docs/customization-guide.md)。

## 关于 Skillify 示例

Skillify 是一个真实案例，但它不是主模板。

更准确的用法是：

- 先用模板启动你自己的项目
- 再看 Skillify，理解模板在真实项目里会长成什么样

示例入口见 [examples/skillify/README.md](examples/skillify/README.md)。

## 常见问题

### 这是个人同步仓库吗

不是。这个仓库按公共模板库整理，不应该依赖某台电脑的绝对路径和私有同步习惯。

### 我需要完全照抄 Skillify 吗

不需要。Skillify 更适合参考结构和方法，不适合整段原文照抄。

### 我能只用其中一部分吗

可以。你可以只用全局规则，也可以只用项目模板，或者两者一起用。

### 后续规则升级怎么办

看 [docs/upgrade-guide.md](docs/upgrade-guide.md)。
