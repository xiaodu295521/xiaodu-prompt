# 快速开始

这份文档面向第一次使用这套工作流模板的人。

## 你会做什么

你需要完成 5 件事：

1. 准备项目双目录
2. 复制项目模板
3. 复制全局模板
4. 替换占位符
5. 用文档链路启动项目

## 第 1 步：创建项目双目录

在你的工作区里创建两个目录：

- `<YOUR_PROJECT>-old`
- `<YOUR_PROJECT>-new`

用途：

- `-old` 保存每一轮开始前的完整基线
- `-new` 负责实际开发

## 第 2 步：复制项目模板

把 [templates/project](../templates/project) 里的内容复制到 `<YOUR_PROJECT>-new`。

至少复制这些文件：

- `AGENTS.example.md`
- `WORKFLOW.example.md`
- `docs/01-product-requirements.example.md`
- `docs/02-ui-design-spec.example.md`
- `docs/03-technical-architecture.example.md`

复制后，把文件名改成你项目要用的正式文件名。

## 第 3 步：复制全局模板

把 [templates/global](../templates/global) 里的内容复制到你的全局规则位置。

常见用法：

- 把全局 `AGENTS` 模板复制到你的 Codex 全局规则文件
- 把全局 `WORKFLOW` 模板复制到你自己的工作流总览文件

## 第 4 步：替换占位符

模板里会出现这些占位符：

- `<YOUR_PROJECT>`
- `<YOUR_PROJECT_NEW>`
- `<YOUR_PROJECT_OLD>`
- `<YOUR_CODEX_HOME>`
- `<YOUR_BACKUP_REPO_URL>`

你需要把它们替换成你自己的实际值。

详细规则见 [customization-guide.md](customization-guide.md)。

## 第 5 步：按文档链路启动

不要一开始就直接写代码。

标准顺序是：

1. 先和用户对齐产品需求
2. 生成 PRD
3. 基于 PRD 生成设计文档
4. 基于 PRD 和设计文档生成技术文档
5. 再进入实现

## 第一轮开发前必须做的事

在真正动手改代码前，先把 `<YOUR_PROJECT>-new` 当前的完整内容复制到 `<YOUR_PROJECT>-old`。

这一步的意义是：

- 给当前轮次留一个完整可回退版本
- 避免 `old` 变成空目录占位

## 看不懂时从哪里开始

建议顺序：

1. 先看根 [README.md](../README.md)
2. 再看 [workflow/WORKFLOW.md](../workflow/WORKFLOW.md)
3. 再看 [templates](../templates)
4. 最后看 [examples/skillify](../examples/skillify)
