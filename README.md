Plan for Lightweight Models

A Codex skill that turns a software change request into a repository-grounded implementation plan for a lightweight AI model.

## Install

Copy `SKILL.md` to `~/.agents/skills/plan-for-lightweight-models/SKILL.md`. From the repository root on Windows, run:

```powershell
$skillDir = Join-Path $env:USERPROFILE '.agents\skills\plan-for-lightweight-models'
New-Item -ItemType Directory -Path $skillDir -Force | Out-Null
Copy-Item -LiteralPath '.\SKILL.md' -Destination $skillDir
```

## Use

Open your target project in Codex, select `plan-for-lightweight-models`, and describe the change you want to plan.

> Plan the addition of CSV export to the existing orders page. Generate `PLAN.md` and `PROGRESS.md`.

The skill analyzes the project and creates two files without editing source code:

- `PLAN.md` defines the design, ordered tasks, files to edit, acceptance criteria, and validation steps.
- `PROGRESS.md` records task status, validation results, blockers, and the next action.

For implementation, ask the executor to read both files. It works on one task at a time, continues after saving a passing result, and stops on the first failed check or blocker.
