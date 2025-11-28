# Commit Conventions

We use a lightweight convention for commit messages to keep history readable and to make it easier to understand what changed.

The goal is structure and clarity, not ceremony for its own sake.

For how commit messages fit into the overall workflow (issues, branches, PRs),
see the [Contributing guide – Commit messages](../CONTRIBUTING.md#23-commit-messages).

---

## 1. Basic format

The basic format is:

```text
<type>: <short summary>
```

Optionally, you can add a scope:
```text
<type>(scope): <short summary>
```

- **Commit type** – *what actually changed in this diff?*  

Keep the summary:
- in present tense where it makes sense ("add", "fix", "update"), or
- as a concise description of what changed.

---

## 2. Allowed types

| Type   | Mainly used for                                  |
|--------|--------------------------------------------------|
| feat   | New behavior / capability                        |
| fix    | Bug fixes                                        |
| docs   | Documentation-only changes                       |
| chore  | Refactors, deps, internal cleanups               |
| build  | Build & CI/CD configuration                      |
| meta   | Repo/process metadata (templates, CODEOWNERS, …) |

Examples:
- `feat: add basic file upload endpoint`
- `fix: handle null payload in task update`
- `chore: update Gradle wrapper`
- `docs: document issue workflow`
- `build: configure base CI pipeline`
- `meta(workflow): introduce develop integration branch`

Other types may appear if the project later needs them, but this set should cover most cases.

---

## 3. Scopes (optional)

Scopes are an optional hint about the area the commit touches.
For now, the scopes should use the same area labels that are defined in the [Project meta](docs/project-meta.md#4-areas).

Examples:
- `feat(domain): add domain model for file metadata`
- `fix(domain): handle invalid status transition`
- `docs(workflow): describe squash merge into develop`
- `meta(workflow): introduce issue templates config`

Avoid meaningless scopes like:
- `build(build): enable tests in CI pipeline`

Use scopes when they genuinely help; don't invent them just to fill the space.

---

## 4. Commit size and structure

- Prefer small, coherent commits over huge "misc" commits.
- Each commit should represent a logically consistent change:
  - one bug fix,
  - one refactor,
  - one new piece of behavior.
- Avoid mixing large refactors with behavioral changes:
  - If you must, split into:
    - `chore: refactor X`
    - `feat: change behavior Y`

Before opening a PR, it is okay to:
- squash noisy WIP commits for clear history or reviewers,
- reorder commits for clarity (if history is not yet shared),
- clean up messages so they reflect what the commit actually does.

---

## 5. Relationship to PR titles

- Commits describe individual steps; 
- PR titles describe the overall outcome.

- Commit messages use `<type>: <summary>`.
- Pull requests use `<area>: <short outcome>`.

---

If these conventions ever become a burden instead of a help, we will adjust them. The point is clarity, not ritual.

---
