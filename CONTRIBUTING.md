# Singularity – Development Guide

It defines how we use issues, labels, branches, and pull requests when working on the project.

The goal is to keep the workflow predictable and avoid chaos.

---

## 1. Issues

### 1.1 When to create an issue

Create an issue for:

- New features or behavior changes.
- Bug reports.
- Refactors, build/CI changes, dependency updates.
- Documentation work.
- Project / repo / process changes (labels, CI, conventions, etc).

Avoid drive-by changes without an issue, except for truly trivial fixes (typos in comments, tiny doc wording, etc).

### 1.2 Issue titles

Keep titles:

- Short and factual.
- Focused on outcome, not implementation details.

Examples:

- `Setup Gradle project`
- `Define GitHub label scheme`
- `Document label scheme in CONTRIBUTING`
- `Fix NPE when payload is null`

Do **not** put type/area prefixes in the title (`build:`, `meta:`, etc).  
Type and area are represented by labels.

### 1.3 Labels

We use a small label set to keep the tracker readable.  
These are **team conventions**; anyone on the project is expected to follow them.

#### Type labels (one per issue)

Exactly one of these should usually be applied:

- `feature` – New feature or request.
- `enhancement` – Small improvements or extensions to existing functionality; no brand-new features.
- `bug` – Unexpected problem or incorrect behavior.
- `chore` – Maintenance work: refactors, dependency bumps, build/CI tweaks without user-facing changes.
- `documentation` – Improvements or additions to documentation.
- `meta` – Project / repo / GitHub configuration and process tasks.

#### Workflow labels (optional)

Use these to describe state or purpose:

- `question` – Issue needs clarification or more information.
- `help wanted` – Another team member is invited to pick this up.
- `duplicate` – This issue is already covered by another one.
- `wontfix` – We decided not to work on this.

#### 1.4 When to reuse vs create new issues

- If an existing issue already describes the same problem/feature, **reuse it** and add a comment.
- If the behavior, area, or impact is clearly different, **open a new issue** and link related ones with references (`See #nn`).

---

## 2. Branches and commits

### 2.1 Branch naming

Use short, descriptive names. Suggested patterns:

- `feature/<short-description>`
- `bugfix/<short-description>`
- `chore/<short-description>`
- `docs/<short-description>`
- `meta/<short-description>`

Examples:

- `feature/authentication-flow`
- `chore/gradle-setup`
- `meta/label-scheme`

These are conventions to keep history readable; they are not enforced by tools.

### 2.2 Commit messages

Use something close to Conventional Commits:

- `feat: add login endpoint`
- `fix: handle null payload in request`
- `chore: update dependencies`
- `docs: document label scheme`
- `build: configure Gradle wrapper`

Keep commit scope focused. Prefer several small commits over one giant “misc changes” blob.

---

## 3. Pull Requests

### 3.1 General rules

- All non-trivial work goes through a pull request.
- Link the PR to the relevant issue: `Closes #NN` or `Related to #NN`.
- Keep PRs focused on a single logical change set (or a tight group of related ones).

### 3.2 PR title and description

**PR title** should summarize the outcome and indicate the area.
**Format:**

```text
<area>: <short outcome in imperative or past-tense>
```
Examples:
  • meta: Add GitHub issue and PR templates
  • build: Setup base Gradle build
  • labels: Implement label scheme and update existing issues
  • docs: Document issue workflow in CONTRIBUTING

Note: PR titles are not conventional commits.
Commits may use chore:, feat:, fix: etc, while PR titles use <area>:.

**Description** should cover:

```markdown
## Summary

What this PR does in 1–3 sentences.

## Details

- Key change 1
- Key change 2
- Any breaking or notable behavioral change

## Testing

- How this was tested (commands, scenarios).
- Mention if some parts are intentionally untested (and why).
```

### 3.3 Reviews and merging
  • At least one other team member reviews non-trivial changes.
	• Author is responsible for:
	  •	Making sure the build passes.
	  •	Ensuring tests are green or explicitly calling out what’s missing.
	• Reviewer focuses on:
	  •	Correctness and impact.
	  •	Clarity of code and tests.
	  •	Consistency with existing patterns in the codebase.

### 3.4 Merge strategy

We use **Squash and merge** for all pull requests.

- Every PR is merged as a **single commit** into the main branch.
- The final commit message should be cleaned up before merging:
  - Subject describes what changed.
  - Body, if needed, can summarize important details or reference issues.
- Intermediate commits inside the PR are treated as work in progress and are not preserved in the main history.

If we ever introduce long-lived release or integration branches, exceptions can be documented here, but the default is:  
**all normal PRs are merged with squash.**

⸻

4. Testing and code style

4.1 Tests

Baseline expectations:
	•	Bug fixes: add or adjust tests that demonstrate the bug and the fix.
	•	New features: add tests for core behavior.
	•	Refactors: keep coverage at least equivalent, avoid silently dropping tests.

Use the project’s standard commands, for example:

```bash
./gradlew test
./gradlew check
```
(Adjust if the actual commands will changed.)

4.2 Style and structure
	•	Follow the style of the file you are editing.
	•	Prefer clear, readable code over clever shortcuts.
	•	Avoid mixing large refactors with behavioral changes in the same PR; split into separate PRs when possible.

⸻

5. Project configuration & process

Changes to project-wide behavior (CI, build, label scheme, branching strategy, etc.) should:
	1.	Have an issue (usually labeled meta and/or chore).
	2.	Be documented briefly in this file or in a nearby doc once stable.
	3.	Be communicated in PR description so the rest of the team is aware.

This file is the place where we collect these decisions. If the process changes, update CONTRIBUTING.md instead of letting reality and docs drift apart.

## Issue labels

We use a small, consistent label set to keep the issue tracker readable.

**Type labels**

- `feature` – New feature or request.
- `enhancement` – Small improvements or extensions to existing functionality; no brand-new features.
- `bug` – Unexpected problem or incorrect behavior.
- `chore` – Maintenance work: refactors, dependency bumps, build/CI tweaks without user-facing changes.
- `documentation` – Improvements or additions to documentation.
- `meta` – Project / repo / GitHub configuration and process tasks.

**Workflow labels**

- `question` – Issue needs clarification or more information.
- `help wanted` – Maintainer would like help on this.
- `good first issue` – Small, well-scoped issue suitable for newcomers.
- `duplicate` – This issue is already covered by another one.
- `wontfix` – Decided not to work on this issue.

### Priority labels

We use priority labels to express how urgent an issue is from the project perspective.

These are set during triage by maintainers. Contributors don’t have to guess the right priority.

- `priority:P0` – Critical. Must be addressed as soon as possible. 
  - Examples: production-blocking bugs, broken main branch, issues that block a milestone.

- `priority:P1` – Important. Should be done for the current or next planned milestone.
  - Examples: key features, significant improvements, non-blocking but high-impact bugs.

- `priority:P2` – Normal. Useful work that can be scheduled after P0/P1 items.
  - Examples: nice-to-have enhancements, cleanups, non-urgent refactors, minor UX / DX polish.

 - `priority:P3` – Low. Backlog / “someday, if it still matters”.
