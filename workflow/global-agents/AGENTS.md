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

