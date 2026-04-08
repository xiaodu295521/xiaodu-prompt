# Skillify 示例

Skillify 是这个公共模板仓库里的真实案例。

它的作用不是让你原样照抄，而是让你看清楚三件事：

- 模板在真实项目里会怎么落地
- 项目级规则如何继承全局规则
- 文档基线、交接文档和工作流规则如何一起使用

## 这个示例展示了什么

- 双目录机制怎么执行
- 项目级 `AGENTS` 和 `WORKFLOW` 怎么写
- PRD、UI、技术文档如何成为后续开发基线
- 交接文档和历史存档如何配合
- Web 项目的最小 CI/CD 规则如何接入项目说明

## 适合怎么用

推荐用法：

1. 先用模板起你自己的项目
2. 再回来看 Skillify 的规则和文档结构
3. 对照理解“模板在真实项目里长什么样”

不推荐用法：

- 直接把 Skillify 的产品描述照搬到你的项目
- 把 Skillify 的页面定义原封不动复制过去
- 不做替换就把示例文件当正式项目文件

## 示例入口

- 项目规则：[AGENTS.md](AGENTS.md)
- 项目流程：[WORKFLOW.md](WORKFLOW.md)
- 文档说明：[docs/README.md](docs/README.md)

## 读取顺序

建议顺序：

1. 先看根仓库 [README.md](../../README.md)
2. 再看本文件
3. 再看 `AGENTS.md`
4. 再看 `WORKFLOW.md`
5. 最后看 `docs/*`

## 注意

Skillify 是案例，不是模板本体。

真正要复制到你项目里的，优先还是：

- `templates/global/*`
- `templates/project/*`
- `workflow/*`
