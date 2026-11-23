---
name: plan-for-lightweight-models
description: Analyze a software project and prepare a technical implementation plan for handoff to a lightweight AI model. Use when the user wants repository-grounded tasks and durable execution progress for a later implementation session.
---

# Plan projects for lightweight models

Act as a software architect and technical lead. Produce `PLAN.md` and `PROGRESS.md` in English using the templates below. Put both in the project root unless the user specifies another directory. Inspect any existing planning files before writing. If either belongs to a different initiative, ask for another destination before replacing anything. When revising the same plan, update the revision in both files and preserve completed task IDs, results, and approved decisions. Give follow-up work a new ID when it changes a completed task's acceptance criteria.

Limit planning writes to those two documents. Use read-only investigation of the project and respect its instructions and the current tool permissions.

## Plan the work

1. Establish the requested outcome, observable success criteria, scope, and constraints. Read the applicable project instructions. Trace the affected behavior through actual entry points, callers, dependencies, configuration, and tests. Record the relevant existing paths, symbols, conventions, and validation commands with their working directories. Identify new paths or symbols as proposed.
2. Clarify decisions with the user before finalizing the plan.
   - Inspect the project first. Use repository evidence to resolve questions
     about existing behavior, files, symbols, and conventions.
   - Ask about unresolved choices that materially affect scope, acceptance
     criteria, architecture, interfaces, data, or compatibility.
   - Ask the highest-impact question first. When there are concrete options,
     explain the trade-offs and recommend one. Use the structured question
     tool when available, or ask directly in the chat.
   - Wait for the answer before finalizing affected tasks. Ask a follow-up
     if the answer reveals another material choice.
   - Record the agreed decisions in `PLAN.md`. If required input or approval
     is still missing, mark the affected tasks as blocked and state what
     would unblock them. If the evidence resolves every material choice,
     proceed without a clarification round.
3. Break the work into small, ordered tasks with stable IDs such as `T01`. Give each task one verifiable outcome and list the exact project-relative paths it may create or edit, including test files when needed. Name affected classes, interfaces, methods, or other relevant symbols. Specify behavior concretely enough to implement without redoing the design, including applicable inputs, outputs, order of operations, and failure behavior. List prerequisite task IDs explicitly.
4. Separate acceptance criteria from the procedure used to verify them. Give each check a working directory, an exact command or reproducible manual steps, and the expected result. Include relevant regressions and failure cases. Preserve a known baseline failure as evidence and record the affected validation as blocked if it cannot establish acceptance.
5. Before handing off, check that each requirement maps to a task, every prerequisite comes earlier in the plan, and each task can be checked on its own once its prerequisites pass. Remove unrelated changes. Record material risks, rollout or migration steps where needed, and the conditions that require replanning.

Fill in the templates with project-specific evidence. Use `None` or `Not applicable` where accurate. Identify unknowns explicitly and remove instructional placeholders from the generated files.

## `PLAN.md` template

```markdown
# [Initiative] implementation plan

- Revision — [1 for a new plan]
- Readiness — [ready or blocked]

## Outcome and scope

- Required behavior and success criteria — [observable outcomes, mapped to task IDs]
- In scope — [requested changes]
- Out of scope — [relevant boundaries]
- Constraints — [project instructions, user constraints, required compatibility]

## Current behavior

[Relevant execution path and existing contracts. Cite verified project-relative paths and symbols. Include relevant tests, dependencies, configuration, and baseline findings.]

## Agreed design

[Target behavior, implementation decisions, affected contracts, and compatibility requirements. Describe data or control flow where it determines the implementation.]

## Ordered tasks

### T01 — [Single verifiable outcome]

- Objective — [precise result]
- Files — [exact project-relative paths, each marked create or modify]
- Symbols — [existing or proposed classes, interfaces, methods, or other relevant symbols]
- Expected behavior — [implementation instructions and observable behavior]
- Prerequisites — [earlier task IDs and any required setup or approvals]
- Constraints — [scope and invariants specific to this task]
- Acceptance criteria — [observable conditions that must pass]
- Validation — [working directory, exact command or manual steps, expected result for each check]

[Repeat the task section in execution order.]

## Risks and replanning

- Risks and compatibility — [failure modes, impact, and agreed mitigation]
- Migration and rollout — [order, verification, and recovery steps if applicable]
- Open items — [affected task IDs, missing decision or evidence, and condition for unblocking]
- Replan when — [material changes to contracts, assumptions, or scope]
```

## `PROGRESS.md` template

Initialize each task as `pending` or `blocked` based on the plan. Record the first task to address and its next action. Use `Not available` for missing version-control metadata. Keep the execution instructions in the generated file so the executor can use it in a fresh session.

```markdown
# [Initiative] execution progress

- Plan revision — [matching PLAN.md revision]
- Starting branch and commit — [branch and commit, when available]
- Starting local changes relevant to the plan — [affected paths and known changes]
- Active or next task — [task ID or None]
- Next action — [concrete step or condition for resuming]

## Task status

| Task | Status | Validation or blocker |
| --- | --- | --- |
| T01 | [pending or blocked] | [Not run, or blocker and resolution condition] |

## Execution records

[For each attempt, record the task ID, relevant changes already applied, validation command or manual check, actual result, and any error or blocker. Record the next action after an interruption. Preserve completed task records.]

## Approved decisions

[Record decisions needed across sessions, their approval source, affected tasks, and relevant plan revision.]

## Execution instructions

1. Before starting or resuming authorized work, read `PLAN.md` and `PROGRESS.md`. Check that their revisions match. Recheck the active or next task's prerequisites and compare the relevant project state with the plan and recorded progress. On resumption, inspect any partial work before changing it.
2. Follow the plan order and work on one task at a time. Mark the task `in progress` before editing. Limit edits to the listed files and constraints. Stop and obtain approval before changing the architecture or expanding scope.
3. Run the specified validation, check all acceptance criteria, and save the actual results here. Mark the task `completed` only when all criteria pass. Save the next task and next action before starting it. Then automatically continue to the next task in plan order with satisfied prerequisites. When all tasks are complete, set both fields to `None`.
4. Stop the sequence at the first failed or unavailable check, unmet prerequisite, or material difference from the plan. Mark the affected task `blocked` and record the evidence, partial work, and the condition for resuming. Leave later pending tasks untouched. Resume the same task once the blocker is resolved and work is authorized. Revalidate before marking it complete.
```
