# Singularity – Development Guide

This guide explains how we use issues, labels, branches, commits, and pull requests when working on Singularity.

The goal is to keep the workflow predictable, traceable, and easy to work with over time.

---

## Quick start

1. Open or pick an issue before you start work (except for tiny, obvious fixes).
2. Branch from `develop` using a short-lived, typed name (for example `feature/add-basic-login`).
3. Commit with structured messages that match the branch/issue type.
4. Open a PR into `develop`, link the issue, and follow the PR template.
5. Keep tests green; add or adjust them for new behavior or fixes.

The sections below contain the detailed rules and examples for each step.

---

## 1. Issues

### 1.1 When to create an issue

Create an issue for:

- New features or behavior changes.
- Bug reports.
- Refactors, build/CI changes, dependency updates.
- Documentation work.
- Project/repo/process changes (labels, CI, conventions, etc).

Avoid drive-by changes without an issue, except for truly trivial fixes (typos in comments, tiny doc wording, etc).

### 1.2 Issue titles

Keep titles:

- Short and factual.
- Focused on outcome, not implementation details.

Examples:

- `Setup Gradle project`
- `Define GitHub label scheme`
- `Fix NPE when payload is null`

Do **not** put type/area/priority prefixes in the issue title (`build:`, `meta:`, etc).  

### 1.3 Issue labels (overview)

We use GitHub labels to classify issues and project items along four axes:

- **Type** – what kind of work this is  
- **Area** – which part of the system or process it primarily affects  
- **Priority** – how urgent it is for the project  
- **Workflow** – special handling / state (question, duplicate, wontfix, etc.)

These axes are implemented as labels (for example, `feature`, `bug`,
`priority:P1`, `question`), so that the project board stays easy to filter and scan.

When you create or triage an issue:

- **Type**  
  - Apply **exactly one** type label (required), e.g. `feature`, `enhancement`, `bug`, `chore`, `documentation`, `meta`.
- **Area**  
  - Apply **one** area label (required), e.g. `domain`, `auth`, `workflow`, `build`, `infra`.  
  - If an issue truly affects multiple areas in a balanced way, you may add
    more than one area label, but this should be rare. Prefer choosing the single
    area with the most visible impact to keep filtering on the project board useful.
- **Priority**  
  - Apply **at most one** priority label (`priority:P0`..`priority:P3`).  
  - New issues may be created without a priority; maintainers set or adjust priority during triage.
- **Workflow**  
  - Add workflow labels only when needed: `question`, `help wanted`, `good first issue`, `duplicate`, `wontfix`, etc.  
  - These refine handling/state and never replace type, area, or priority.

Full definitions of each label and axis live in [Project meta](docs/project-meta.md).

### 1.4 Issue templates

When opening an issue, use the provided templates under [`.github/ISSUE_TEMPLATE`](.github/ISSUE_TEMPLATE):

  - use the **general** template for features, enhancements, chores, and meta tasks;
  - use the **bug** template for defects and regressions.

The goal is to keep issues consistent and easy to triage.

Templates are a starting point, not a straitjacket, but issues should contain at least the information these templates ask for.

---

## 2. Branches and commits

This section is a short version. Full details are in the [Git workflow](docs/git-workflow.md) document.

### 2.1 Branching model (high-level)

We use a simple `main`/`develop` model:

- `develop` is the primary **integration branch** for day-to-day work.
- `main` is reserved for **release-ready** code and is updated from `develop` when a release is cut.

### 2.2 Branch naming

We use short-lived branches created from `develop` with names in the form:

```text
<issue-type>/<short-description>
```
- `<issue-type>` is usually one of: `feature`, `bugfix`, `chore`, `docs`, `meta`;
- `<short-description>` is a short, kebab-case summary, e.g. `add-basic-login`.

We do not encode issue numbers in branch names.

For full details and examples, see the [Git workflow](docs/git-workflow.md#12-short-lived-branches).

### 2.3 Commit messages

At a glance, they usually look like:

```text
<type>: <short summary>
```

Examples:

- `feat: add refresh token support`
- `fix: handle null payload in request`
- `build: configure Gradle wrapper`

Keep commit scope focused and avoid huge “misc” blobs. 

The detailed rules (allowed types, scopes, structure) are in the [Commit conventions](docs/commit-conventions.md) document.

---

### 2.4 Naming consistency (issue → branch → commit)

As a rule of thumb, the “kind of work” stays the same across issues,
branches, and commits, even if the wording changes:

| Issue type      | Typical branch prefix      | Typical commit type(s) |
|-----------------|----------------------------|------------------------|
| `bug`           | `bugfix/...`               | `fix: ...`             |
| `feature`       | `feature/...`              | `feat: ...`            |
| `documentation` | `docs/...`                 | `docs: ...`            |
| `meta`          | `meta/...`                 | `meta: ...`            |
| `chore`         | `chore/...`                | `chore: ...`or`build: ...` |

Other types follow the same idea: the issue type determines the branch
prefix and normally maps to the corresponding commit `type`.

This naming is not enforced by tools, but it is the **expected default**.
Stick to it unless you have a clear reason not to; it keeps issues, branches,
and history easy to follow.

---

## 3. Pull Requests

This section is the main reference for how we use pull requests. The [Git workflow](docs/git-workflow.md) shows where PRs fit into the branch and release process.

### 3.1 General rules

- All non-trivial work goes through a pull request.
- By default, the PR is directed to the integration branch `develop`. We use the `main` branch only for release merges.
- Link the PR to the relevant issue:
  - `Closes #NN` for issues that are fully resolved,
  - `Related to #NN` for partial or exploratory work.
- Keep PRs focused on a single logical change set (or a tight group of related ones).

### 3.2 PR title and description

**PR title** should summarize the outcome and indicate the area.

**Format:**

```text
<area>: <short outcome (imperative or past tense, sentence case)>
```
where:
- `<area>` should be one of the defined project areas (lowercase).
- `<short outcome>` starts with a capital letter and is written in sentence case.

Examples:
- workflow: Add GitHub issue and PR templates
- build: Setup base Gradle build

> Note: PR titles are not conventional commits.
> Commits may use `chore:`, `feat:`, `fix:`, etc., while PR titles use `<area>`.

The **PR description** should follow [`pull_request_template.md`](.github/pull_request_template.md).

### 3.3 Reviews and merging
- At least one other team member reviews non-trivial changes.
- Author is responsible for:
    - Making sure the build passes.
    - Ensuring tests are green or explicitly calling out what’s missing.
- Reviewer focuses on:
    - Correctness and impact.
    - Clarity of code and tests.
    - Consistency with existing patterns in the codebase.

By default, we use **Squash and merge** into `develop`.
See [Git workflow](docs/git-workflow.md) for details.

---

## 4. Testing and code style

### 4.1 Tests

Baseline expectations:
- **Bug fixes**: add or adjust tests that demonstrate the bug and the fix.
- **New features**: add tests for core behavior.
- **Refactors**: keep coverage at least equivalent, avoid silently dropping tests.

By default:
- locally, run at least `./gradlew test` before opening a PR;
- CI will normally run `./gradlew check`, which may include additional verification steps (style checks, static analysis, etc.).

### 4.2 Style and structure

- Follow the style of the file you are editing.
- Prefer clear, readable code over clever shortcuts.
- Avoid mixing large refactors with behavioral changes in the same PR; split into separate PRs when possible.

---

## 5. Changing project rules

Some work doesn’t change product behavior at all. Instead, it changes **how the project itself is run**: labels, branching strategy, CI rules, templates, required checks, etc.

Treat this work explicitly, as first-class, instead of sneaking it into random feature branches.

When you change project rules:

1. Create an issue labeled `meta`.
2. Make the change via a pull request.
3. Update this guide and/or nearby docs so the new process is documented.
4. Call out the change in the PR description so it’s easy to discover later.

This file is the entry point for “how we work”. If reality and this guide
ever diverge, either update the guide or revert the process change.

---

## 6. Further reading

For detailed conventions, see:

- [`docs/git-workflow.md`](docs/git-workflow.md) – branching model and merge strategy.
- [`docs/project-meta.md`](docs/project-meta.md) – label scheme, priorities, and project meta.
- [`docs/commit-conventions.md`](docs/commit-conventions.md) – commit message format and examples.

---
