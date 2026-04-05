# Workflow Changelog

## v1.2 - 2026-04-05
- 新增“工作流文件更新后必须进行 GitHub 云端备份”规则。
- 固定备份仓库为 `xiaodu-prompt`，并约束目录映射：
  - `workflow/`
  - `workflow/templates/`
  - `workflow/global-skill/`
  - `workflow/global-agents/`
- 新增备份执行顺序：`pull -> sync -> diff -> commit -> (用户确认) -> push`。
- 新增失败策略：push 失败不影响本地流程文件，保留本地提交并报告。

## v1.1 - 2026-04-05
- 取消初始化脚本作为默认入口，改为手动建立双目录。
- 增加“AI 自动识别 `<project>-old / <project>-new>`”规则。
- 目录缺失或匹配不唯一时，强制先与用户确认。

## v1.0 - 2026-04-05
- 建立双目录安全机制（`<project>-old` / `<project>-new`）。
- 增加“信息不足先确认”强制流程。
- 明确技能调用规则与子代理使用规则。
- 增加 UI 先预览后改动规则。
- 增加打包与清理规范（支持“仅保留安装包”）。
- 增加项目收尾复盘与流程版本迭代机制。

