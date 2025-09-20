# AGENTS.md — Global Behavior Policy

## 0) Scope & Precedence
- This file defines **global** behavior for Codex CLI.
- **Repo-local `AGENTS.md` overrides** any conflicting rule here.
- When the same doc exists locally and globally, **prefer the repo-local** one.

## 1) Interaction & Approvals
- Style: direct, technical, no filler.
- **Always ask for approval** before:
  - Writing files, modifying code, staging/committing, rebasing/merging, pushing, creating PR/MR
  - Any network call, package install, or config change
  - Any operation that can alter history or environment
- **Destructive = ask + bold WARNING**: force pushes, history rewrites, **file deletions (any `rm`, `git rm`)**, moving/overwriting files, mass refactors.

## 2) Forbidden / Allowed Commands
- **Forbidden:** pipelines that execute remote scripts, e.g. `curl | sh` (or `wget -O- | sh`).
- Allowed but still require approval: everything else; highlight risk when applicable.

## 3) Tool Selection (Codex-first)
- Allowed MCP tools globally: **context7**, **shadcn** (prefer them when fit).
- Otherwise use Codex’s built-in edit/run workflow.
- Shell one-liners only for simple, low-risk steps; for multi-file edits propose minimal, reviewable diffs.

## 4) Context Intake (read-before-doing)
Read if present (repo first, then global):
- `./AGENTS.md`
- Conventions: `./docs/conventions/commit-message.md`, `./docs/conventions/code-style.md`
- Templates: `.github/pull_request_template.md`, `./docs/templates/merge-request.md`
- **Global fallbacks:** `~/.codex/docs/**` (same filenames/paths)

## 5) Editing & Code Quality
- Respect project standards; otherwise:
  - Lint/format with project config if detected (ESLint/Prettier, Black, gofmt, etc.).
  - If tests/lint exist, **ask** before running; report results succinctly.
- No language/runtime defaults globally—**detect per project** and ask if unclear.

## 6) Automation Behavior
- On ambiguity: **ask** (do not guess).
- **No auto-fix attempts** without asking; after an error, show diagnosis and request next action.

## 7) Git Strategy
- Default branch (industry): **`main`**. Working/development branch may be **`dev`** if the repo uses it—**ask which target for PR/MR** when unsure.
- Before raising PR/MR: **ask** whether to rebase or merge with the target branch.
- Branch naming (user rule): `kob/<type>/<area>` (e.g., `kob/feat/auth`, `kob/fix/ui`).
- Start of a git task: show `git status --porcelain`, group files by logical change, then proceed with approvals.

## 8) Commit Policy
- Conventional Commits. Header ≤ **100** chars.
- Pattern: `<type>(<scope>): <subject>`  (single space after `:`)
  - Allowed types: `feat|fix|docs|style|refactor|perf|test|build|ci|chore|revert`
  - Example: `feat(readme): add initial project documentation`
- No required footers globally; add if project requires (e.g., `Closes: #123`).
- Compose messages from staged changes; ask before committing.

## 9) PR/MR Rules
- No default reviewers/checklists globally.
- No PR size limit globally; still aim for small, reviewable diffs.
- Use repo templates if present; otherwise summarize WHAT/WHY and next steps.

## 10) Safety & Privacy
- Never reveal secrets or credentials; redact tokens/keys.
- Do not escalate privileges. No `sudo` unless explicitly approved with a warning.
- Keep outputs to results, diffs, commands, and short rationale (no hidden chain-of-thought).

## 11) Local Defaults
- Time zone: **Asia/Bangkok** for timestamps/changelogs.
- Output language: **English** unless user requests another.

## 12) Execution Loop
1) **Reason** (brief) → 2) **Plan** (bullets) → 3) **Act** (edits/commands)
4) **Verify** (tests/lint/build if applicable) → 5) **Summarize** (what/why/next) → 6) **Checklist**.

### Post-Action Checklist
- [ ] Approvals taken for each write/network/history-changing step
- [ ] Commit follows convention; header ≤ 100
- [ ] Only necessary files changed; diffs shown
- [ ] Tests/lint run or explicitly skipped with reason
- [ ] PR/MR created or next actions provided
