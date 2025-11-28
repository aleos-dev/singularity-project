# Singularity – Contributing Guide

This is the entry point for how we work on Singularity. It shows where to start and points to the detailed rules that keep the workflow predictable and easy to follow over time.

Use this guide to orient yourself, then dive into the linked documents when you need specifics.

---

## Quick start

1. Find or file an issue for your work.
2. Create a short-lived branch from `develop`.
3. Commit with structured messages.
4. Open a pull request into `develop` and link the issue.
5. Keep tests green and follow review feedback.

The sections below summarize the expectations for each step and link to the detailed rules.

---

## Issues

- Create an issue for anything non-trivial: new features, bug fixes, refactors, CI/build changes, documentation, or project meta work.
- Keep titles short, factual, and outcome-focused; avoid prefixes like `build:` or `meta:`.
- Apply labels for **type**, **area**, **priority**, and **workflow** so the project board stays filterable.
- Use the templates under [`.github/ISSUE_TEMPLATE`](.github/ISSUE_TEMPLATE) to keep reports consistent.

> Full label definitions and examples live in [Project meta](docs/project-meta.md).

---

## Branches and commits

- We use a simple `develop` → `main` model; everyday work branches from `develop`.
- Name branches as `<issue-type>/<short-description>`, e.g. `feature/add-basic-login` or `meta/update-labels`.
- Keep the “kind of work” consistent across the issue, branch prefix, and commit type (`bug` → `bugfix/...` → `fix: ...`).
- Commit messages follow `<type>: <short summary>` and stay focused; avoid giant catch-all commits.

> Detailed branching rules and commit examples are in [Git workflow](docs/git-workflow.md) and [Commit conventions](docs/commit-conventions.md).

---

## Pull requests

- Route PRs to `develop` by default; `main` is used only for release merges.
- Link PRs to issues (`Closes #NN` for completed work, `Related to #NN` for partial/exploratory changes).
- Keep PRs scoped to a single logical change set.
- Format titles as `<area>: <short outcome>` in sentence case, and follow the [`pull_request_template.md`](.github/pull_request_template.md) for the description.
- Expect at least one review for non-trivial work; default merge strategy is **Squash and merge** into `develop`.

> See [Git workflow](docs/git-workflow.md#3-merge-strategy) for merge details.

---

## Testing and quality

- Bug fixes and features should ship with tests that cover the behavior.
- Run `./gradlew test` locally before opening a PR; CI will typically run `./gradlew check`.
- Match the style of surrounding code and avoid mixing large refactors with behavioral changes.

---

## Changing project rules

Changes to how the project is run—labels, templates, required checks, conventions—should be explicit:

1. Create an issue labeled `meta`.
2. Make the change via a PR.
3. Update this guide and related docs so the new rule is documented.
4. Call out the process change in the PR description for easy discovery later.

If reality and these docs diverge, update the docs or roll back the process change.

---

## Further reading

- [`docs/git-workflow.md`](docs/git-workflow.md) – branching model and merge strategy.
- [`docs/project-meta.md`](docs/project-meta.md) – label scheme, priorities, and project meta.
- [`docs/commit-conventions.md`](docs/commit-conventions.md) – commit message format and examples.
