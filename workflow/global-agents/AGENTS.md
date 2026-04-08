## gstack

gstack is installed globally for Codex at `C:\Users\29552\.codex\skills\gstack`, with the source repo at `C:\Users\29552\gstack`.

For browser automation, site QA, deployment verification, screenshots, and reproducing live UI issues, prefer gstack skills over ad hoc browser tooling. In particular, use `gstack-browse` for interactive website work and do not use `mcp__claude-in-chrome__*` tools. If higher-priority system or developer instructions require built-in web browsing for research, verification, or citations, follow those instructions first.

Available gstack skills for this Codex install:
- `gstack`
- `gstack-autoplan`
- `gstack-benchmark`
- `gstack-browse`
- `gstack-canary`
- `gstack-careful`
- `gstack-connect-chrome`
- `gstack-cso`
- `gstack-design-consultation`
- `gstack-design-review`
- `gstack-document-release`
- `gstack-freeze`
- `gstack-guard`
- `gstack-investigate`
- `gstack-land-and-deploy`
- `gstack-office-hours`
- `gstack-plan-ceo-review`
- `gstack-plan-design-review`
- `gstack-plan-eng-review`
- `gstack-qa`
- `gstack-qa-only`
- `gstack-retro`
- `gstack-review`
- `gstack-setup-browser-cookies`
- `gstack-setup-deploy`
- `gstack-ship`
- `gstack-unfreeze`
- `gstack-upgrade`

Recommended usage:
- Start new product or feature exploration with `gstack-office-hours`
- Stress-test scope and product direction with `gstack-plan-ceo-review`
- Lock architecture and test strategy with `gstack-plan-eng-review`
- Review design quality with `gstack-plan-design-review` or `gstack-design-review`
- Use `gstack-review` before landing meaningful code changes
- Use `gstack-qa` or `gstack-qa-only` for live app testing
- Use `gstack-ship` for release prep and `gstack-land-and-deploy` after approval
- Use `gstack-careful`, `gstack-freeze`, `gstack-guard`, and `gstack-unfreeze` for safety boundaries

If gstack skills stop working or look stale, refresh them from `C:\Users\29552\gstack` with `bash ./setup --host codex` from Git Bash.

## context7

Context7 is installed globally for Codex as an MCP server through `C:\Users\29552\.codex\config.toml`.

For up-to-date library documentation, SDK usage, installation/configuration steps, framework API differences, and third-party integration guidance, prefer Context7 first.

Use Context7 especially when:
- the user asks for the latest package or framework usage
- the task depends on exact library APIs or version-specific behavior
- installation or configuration details may have changed recently

Do not force Context7 for:
- casual conversation
- stable general knowledge
- tasks that do not depend on current external documentation
- situations where local repository inspection is the primary source of truth

## xiaodu-propmt

Default workflow for all future projects:
- Use `xiaodu-propmt` as the baseline process by default.
- At project start, user manually creates `<project>-old` and `<project>-new`, and AI must detect and validate the pair before implementation.
- All implementation happens in `-new`.
- `-old` is not an empty placeholder. Before every new development round, larger fix, rule update, or major implementation phase, first copy the complete current project baseline from `-new` into `-old`, then continue editing `-new`.
- The goal of `-old` is to preserve the full “before this round started” version for fallback and comparison.

Project-type routing is now mandatory:
- If the project clearly belongs to website, web app, admin panel, SaaS, landing page, dashboard, or Web full-stack, explicitly remind the user that the default startup choice is `方案 B：稳定内核 + 可换技术栈`.
- Explain `方案 B` in plain Chinese: directory structure, module boundaries, contracts, test gates, and review rules stay fixed; the concrete stack may vary by project.
- If the project is not Web, first classify it into one of these stable lanes:
  - mobile app
  - desktop tool
  - automation / bot / bridge service
- For non-Web projects, propose the matching stable architecture instead of forcing the Web lane.
- If the project spans multiple types, choose the lane by the primary deliverable and treat the rest as submodules.

Web projects default to `方案 B`:
- Keep the repo root restrained. Do not flatten business code, docs, config, scripts, and assets all into one root.
- Prefer these top-level folders when a new Web project is initialized:
  - `apps/`
  - `packages/`
  - `docs/`
  - `scripts/`
  - `infra/` or `config/`
- Frontend internals should prefer:
  - `app`
  - `pages` or `routes`
  - `features`
  - `entities`
  - `shared`
- Backend internals should prefer:
  - `modules`
  - `adapters`
  - `contracts`
  - `infrastructure`
- Do not scatter external SDK calls, repeated state literals, or duplicate error mappings across the codebase.

Web CI/CD defaults are now part of startup:
- For solo-builder or “one person + AI” Web projects, enable CI by default instead of waiting until the project gets large.
- The default CI gate should stay small but firm:
  - dependency install must pass
  - lint must pass
  - typecheck must pass
  - build must pass
  - if key tests already exist, run the critical test subset
- The default delivery shape for Web projects is:
  - CI enabled
  - preview deployment enabled
  - production deployment kept manual
- Preview environments should be used for branch or PR verification so the user can inspect the real page before merge or release.
- Production should not auto-deploy by default for solo + AI projects unless the user explicitly asks for full automation.
- Before release-related work, the main agent should clearly report:
  - whether CI is already in place
  - whether preview deployment is already in place
  - whether production release is manual or automatic
  - what is still missing

Non-Web stable lanes default to:
- mobile app: `app / features / shared / services / docs`
- desktop tool: `shell / core / adapters / docs`
- automation / bot / bridge service: `workflow / adapters / integrations / runtime / docs`

Document-first flow is still mandatory:
- Before implementation on a new project or major new phase, require product requirements input first.
- Generate documents in this order:
  - PRD first
  - design doc second
  - technical doc third
- Do not dump the full document stack in one shot.
- Align with the user at key checkpoints before continuing:
  - product positioning and target user
  - scenarios and core business flow
  - page direction and interaction direction
  - technical boundaries and evolution path

Future-expansion alignment is now mandatory during PRD and technical docs:
- Do not only align the current version.
- Also align these high-probability future items with the user:
  - what must ship now
  - what is most likely in the next phase
  - what will not be implemented now but should be reserved
  - which external services may be integrated later
  - which modules are likely to split later
- PRD should include a fixed section similar to:
  - `当前范围 / 下一阶段范围 / 暂不实现但要预留的能力`
- Technical docs should include fixed sections similar to:
  - `未来模块演进图`
  - `目录预留方案`
  - `CI/CD 策略`
- If future needs remain unclear, lock at least one “most likely next phase” before finalizing the startup spec.

Directory reservation is now part of startup:
- Directory reservation is not optional.
- The reservation moment is:
  1. initial user intent becomes clear
  2. PRD and technical direction finish one alignment round
  3. technical doc confirms the likely next-phase modules
  4. only then create the project skeleton and reserved folders
- Use `中等预留` by default:
  - reserve only high-probability modules
  - do not pre-create purely speculative modules
  - every reserved folder must have a clear purpose
  - reserve enough to keep structure clean, but do not create dozens of empty folders

Communication requirements remain:
- User-facing plans, implementation explanations, progress reports, and risk summaries should default to plain, easy-to-understand Chinese.
- Avoid dense technical jargon; if jargon is necessary, explain it immediately in simple terms.
- Prefer this order:
  - result
  - reason
  - implementation detail

Apply skill and sub-agent usage rules from `C:\Users\29552\.codex\skills\xiaodu-propmt\SKILL.md`.
- After any workflow-file update, sync latest workflow artifacts to the local GitHub upload buffer first when available.
- Workflow rule updates should default to local repository preservation only.
- Do not push workflow changes to any cloud repository unless the user explicitly confirms that this round is ready to upload.
- At project end, run a retro and evolve workflow rules and version.

## large-project-orchestration

Default policy for medium and large projects:
- Main agent should orchestrate by default.
- Sub-agents should execute scoped work.
- Prefer custom sub-agents from `C:\Users\29552\.codex\agents`.
- Use official built-in roles only as fallback when no suitable custom role exists.

Required orchestration flow:
- Verify `<project>-old` and `<project>-new` before implementation.
- Verify that the current round's `new -> old` baseline snapshot has been completed before deeper implementation starts.
- Read repo constraints and current docs first.
- Start broad work with `task-distributor`.
- Lock scope and acceptance with role-specific agents before wide implementation.
- Run parallel sub-tasks only when write scopes do not overlap.
- Default parallelism target is `2` sub-tasks.
- Allow temporary promotion to `3` only when:
  - there has been no recent `429 Too Many Requests`
  - the third agent is lightweight and read-only
  - the third agent does not block the critical path
- Main agent integrates, validates, and reports.

Phase-based dispatch default:
- Phase A: only `task-distributor`
- Phase B: at most `2` spec-locking agents
- Phase C: at most `2` writing agents
- Phase D: integration stays local unless one small patch agent is clearly needed

Rate-limit handling:
- On first `429 Too Many Requests`:
  - stop spawning new agents
  - wait `60-90` seconds
  - retry only once
  - shrink prompt context before retrying
- On second `429 Too Many Requests`:
  - reduce active concurrency to `1`
  - switch remaining work to sequential execution
  - explicitly report role, mitigation, serial fallback, and delivery impact
- Never respond to `429` by silently dropping tasks or continuing batch spawn.

Prompt and thread hygiene:
- Do not default to `fork_context: true`.
- Prefer passing file paths, fact summaries, and explicit deliverables over full thread history.
- Reuse existing agents with `send_input` when possible instead of repeatedly spawning new ones.
- Close completed or idle agents promptly.

Local GitHub upload buffer rule:
- If a project provides a local GitHub upload buffer such as `<project-root>\\github-upload`, sync workflow snapshots there first before any external GitHub backup or push flow.
- After syncing to the local buffer, local commit is allowed by default, but cloud push still requires explicit user confirmation.

Critical missing-role rule:
- If a required sub-agent role is missing and that gap materially blocks the task, report it to the user before continuing.
- Do not silently downgrade.
- Do not pretend a weak-fit role is sufficient.
- The report must include:
  - missing role
  - why it is required
  - whether work can continue
  - fallback option
  - fallback risk

Main-agent override rule:
- The main agent may patch blocking critical-path work when delegation would slow delivery more than help it.
- The main agent should not absorb large specialist work by default.

Preferred gstack sequence for larger projects:
- `gstack-office-hours`
- `gstack-plan-ceo-review`
- `gstack-plan-eng-review`
- `gstack-plan-design-review`
- `gstack-review`
- `gstack-qa` or `gstack-qa-only`
