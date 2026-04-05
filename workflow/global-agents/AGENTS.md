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

## xiaodu-propmt

Default workflow for all future projects:
- Use `xiaodu-propmt` as the baseline process by default.
- At project start, user manually creates `<project>-old` and `<project>-new`, and AI must detect/validate the pair before implementation.
- Implement only in `-new`; keep `-old` untouched until user confirms promotion.
- If requirements/data are insufficient, pause and confirm missing items before proceeding.
- Apply skill and sub-agent usage rules from `C:\Users\29552\.codex\skills\xiaodu-propmt\SKILL.md`.
- After any workflow-file update, sync latest workflow artifacts to `xiaodu-prompt` for cloud backup (commit first, push after user confirmation).
- At project end, run a retro and evolve workflow rules/version.

## large-project-orchestration

Default policy for medium and large projects:
- Main agent should orchestrate by default.
- Sub-agents should execute scoped work.
- Prefer custom sub-agents from `C:\Users\29552\.codex\agents`.
- Use official built-in roles only as fallback when no suitable custom role exists.

Required orchestration flow:
- Verify `<project>-old` and `<project>-new` before implementation.
- Read repo constraints and current docs first.
- Start broad work with `task-distributor`.
- Lock scope and acceptance with role-specific agents before wide implementation.
- Run parallel sub-tasks only when write scopes do not overlap.
- Default parallelism target is `4-6` sub-tasks.
- Main agent integrates, validates, and reports.

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

## large-project-orchestration

Default policy for medium and large projects:
- Main agent should orchestrate by default.
- Sub-agents should execute scoped work.
- Prefer custom sub-agents from `C:\Users\29552\.codex\agents`.
- Use official built-in roles only as fallback when no suitable custom role exists.

Required orchestration flow:
- Verify `<project>-old` and `<project>-new` before implementation.
- Read repo constraints and current docs first.
- Start broad work with `task-distributor`.
- Lock scope and acceptance with role-specific agents before wide implementation.
- Run parallel sub-tasks only when write scopes do not overlap.
- Default parallelism target is `4-6` sub-tasks.
- Main agent integrates, validates, and reports.

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

