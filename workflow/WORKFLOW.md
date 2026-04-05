# Skillify Workflow

## Purpose

This file defines the default execution workflow for medium and large tasks in Skillify.
The operating model is:

- main agent orchestrates
- sub-agents execute
- the main agent integrates and validates

This document complements `AGENTS.md`.

## Baseline Constraints

- Work only in `Skillify-new`.
- Keep `Skillify-old` untouched until the user confirms promotion.
- Use the `xiaodu-propmt` process as the default workflow baseline.
- If information is insufficient, report the gap before implementation.

## Fixed Delivery Pipeline

1. Verify directory pair
   - Confirm `Skillify-old` and `Skillify-new` both exist.
   - Confirm the current work target is `Skillify-new`.

2. Ground in the actual repo
   - Inspect current code, docs, configs, and constraints.
   - Identify whether the task is small, medium, or large.

3. Decide whether delegation is required
   - Small tasks may stay local.
   - Medium and large tasks should default to sub-agent execution.

4. Start decomposition
   - Delegate the first planning split to `task-distributor`.
   - Require clear work units, ownership boundaries, dependencies, and completion conditions.

5. Lock spec before wide implementation
   - Use `product-manager` for scope and acceptance decisions.
   - Use `ui-designer` for page hierarchy, visual system, and high-risk interaction choices.
   - Use `api-designer` when frontend/backend contracts or service boundaries need to be fixed first.

6. Dispatch scoped execution
   - Assign each work unit to one owner.
   - Prefer role-specific agents over general ones.
   - Keep concurrent tasks non-overlapping in write scope.

7. Integrate
   - The main agent reviews returned work.
   - Resolve conflicts, missing seams, and cross-task mismatches.
   - If integration itself is the smallest coherent critical-path task, the main agent may do it locally.

8. Validate
   - Run the narrowest checks that prove the changed flow works.
   - Use review and QA skills when appropriate.

9. Report
   - Summarize what was delegated, what landed, what was validated, and what remains.

## Default Role Mapping

### Planning and framing

- `task-distributor`
  - break broad work into concrete units
  - define dependencies
  - maximize safe parallelism

- `product-manager`
  - lock scope
  - define success criteria
  - separate now vs later

- `business-analyst`
  - normalize messy input
  - extract acceptance criteria and requirement baseline

- `project-manager`
  - sequence larger workstreams
  - manage dependency pressure and delivery order

### Design and frontend

- `ui-designer`
  - visual direction
  - page structure
  - interaction-level design decisions

- `frontend-developer`
  - route, component, state, and UI behavior changes

- `ui-fixer`
  - narrow UI bug or small visual polish patch

### Backend and integration

- `backend-developer`
  - service logic, API handlers, domain behavior

- `api-designer`
  - contract shape, compatibility, and boundary review

- `payment-integration`
  - checkout flow, payment status, webhook and settlement logic

### Research and mapping

- `search-specialist`
  - quick discovery of likely source-of-truth files or sources

- `code-mapper`
  - execution path and ownership mapping before implementation

## Critical Role Handling

Treat these as critical when the task obviously depends on them:

- `task-distributor` for broad parallelizable work
- `ui-designer` for major UI/interaction decisions
- `frontend-developer` for frontend-heavy execution
- `backend-developer` for backend-heavy execution
- `payment-integration` for checkout, billing, or payment state work
- `api-designer` when frontend/backend contracts are the blocking decision

If a critical role is missing:

1. Check `C:\Users\29552\.codex\agents` first.
2. Check official built-in roles second.
3. If still missing, stop and tell the user:
   - missing role name
   - why it is required
   - whether work can continue
   - fallback approach
   - delivery risk of the fallback

Do not silently downgrade.
Do not pretend a weak-fit role is good enough.

## Concurrency Rules

- Default concurrency target is `4-6` sub-tasks.
- Only parallelize tasks with disjoint write scopes.
- Do not run UI design and frontend implementation on the same component path at the same time.
- Do not run two implementers against the same module unless ownership is explicitly split.
- Use one blocking chain and several sidecar chains, not six blockers at once.

## Main Agent Override Rule

The main agent may directly implement work only when:

- the task is small and self-contained
- integration is the only missing step
- the delegated result is blocking the critical path
- conflict resolution requires one shared context

The main agent should not absorb missing-specialist work without first telling the user when the missing role is critical.

## Waiting Strategy

- Do not spam waits.
- Wait only when the next critical-path action depends on the result.
- While agents are running, do non-overlapping work such as:
  - validation prep
  - acceptance criteria refinement
  - integration planning
  - risk review

## Skill Usage Guide

Use gstack skills when they materially improve the workflow.

Recommended order by task phase:

- product exploration: `gstack-office-hours`
- ambition/scope review: `gstack-plan-ceo-review`
- engineering plan lock: `gstack-plan-eng-review`
- design plan lock: `gstack-plan-design-review`
- pre-landing review: `gstack-review`
- browser QA and verification: `gstack-qa` or `gstack-qa-only`

Use `gstack-browse` for interactive browser validation instead of ad hoc browser tooling.

## Validation Expectations

Every meaningful task closeout should include:

1. what was attempted
2. what was delegated
3. what changed
4. what was verified
5. what remains risky
6. whether the result is ready for promotion

Minimum validation should cover:

- syntax or type safety where relevant
- changed critical path
- one high-risk edge condition
- any user-visible regression risk introduced by the change

## Project-End Rules

- At project end, run a retro.
- Capture:
  - new bottlenecks
  - missing roles
  - weak prompts
  - workflow changes worth standardizing
- If workflow rules change, update this file and related workflow artifacts.

## Workflow Artifact Reminder

When workflow files are updated, follow the `xiaodu-propmt` backup rule:

- sync workflow artifacts to the backup repository
- commit before push
- push only after user confirmation
