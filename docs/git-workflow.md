# Git Workflow

This document describes how we use branches and merges in the Singularity repository.

The goal is to keep history clean, make it easy to understand what changed and why, and avoid conflicts between parallel tasks.

The [Contributing guide](../CONTRIBUTING.md#2-branches-and-commits) explains how branches, labels, commits, and pull requests fit together in the overall workflow. This document focuses on the branching and merge strategy.

---

## 1. Branches

### 1.1 Long-lived branches

We use two primary long-lived branches:

- `main`
  - Always points to the latest **release-quality** state.
  - Protected: changes come only from merges (no direct pushes).
  - Used to tag releases.

- `develop`
  - Primary **integration branch** for active development.
  - All feature, bugfix, docs and meta work is merged into `develop` first.
  - Also protected: changes go through pull requests.

Additional long-lived branches (e.g. `release/*`, `hotfix/*`) may appear later if the project needs them. Their rules will be documented here.

### 1.2 Short-lived branches

All day-to-day work happens in short-lived branches created from `develop`:

Branches are named using the pattern:

```text
<issue-type>/<short-description>
```
Use short, kebab-case descriptions in the `<short-description>` part.

We do not encode issue numbers in branch names. The mapping between work and
issues is kept through issue/PR links (for example, `Closes #NN`) and the project board.

Prefixes correspond to issue types defined in the [Project meta - Issue Labels](project-meta.md#1-issue-labels-types)

- feature/<short-description>        – for `feature` issues
- enhancement/<short-description>    – for `enhancement` issues
- bugfix/<short-description>         – for `bug` issues
- chore/<short-description>          – for `chore` issues
- docs/<short-description>           – for `documentation` issues
- meta/<short-description>           – for `meta` issues

Examples:

- `feature/add-basic-login`
- `bugfix/fix-login-status-code`
- `chore/remove-legacy-config`
- `docs/update-readme-build-section`
- `meta/adjust-bug-template`

---

## 2. Typical workflow

Example for a feature:

1. Create or reuse an issue, e.g. `#12 Enable Spotless`.
2. Create a branch from `develop`:

```bash
git checkout develop
git pull
git checkout -b chore/spotless-setup
```

3. Commit changes using structured commit messages (see the [Commit conventions](commit-conventions.md)).
4. Push the branch and open a pull request into `develop`.
5. Follow the PR rules from [Contributing guide - Pull requests](../CONTRIBUTING.md#3-pull-requests).
6. Once the PR is approved and CI is green, merge it according to the [merge strategy](#3-merge-strategy).
7. Delete the short-lived branch once merged (both locally and remotely).

This workflow applies to all short-lived branches.

---

## 3. Merge strategy

### 3.1 Into `develop`: Squash and merge

For branches targeting develop:

- Use "**Squash and merge**":
    - The entire branch is merged as a **single commit**.
    - This keeps the develop history linear and groups changes by task/issue.

- Before merging:
    - Clean up the final commit message:
        - Subject describes what changed.
        - Body can summarize important details or reference issues.

Intermediate commits inside the branch are treated as work-in-progress and are not preserved in the main history.

### 3.2 From `develop` to `main`: Release merges

When a release or milestone is ready:
1. Make sure `develop` is in a stable state.
2. Create a pull request from `develop` into `main`.
3. Merge **without squash** (regular merge/--no-ff equivalent in the UI):
    - The merge commit into `main` represents a release event.
4. Tag the release on `main`:

```bash
git checkout main
git pull
git tag -a vX.Y.Z -m "Release vX.Y.Z"
git push origin vX.Y.Z
```

This makes it easy to:
- see which changes are included in a release;
- roll back to a previous release if needed.

### 3.3 Handling conflicts

If `develop` has moved forward and your branch is behind:
- Prefer updating the branch before merging the PR:

```bash
git checkout feature/something
git fetch origin
git merge origin/develop
# or, if you're comfortable with rebase:
# git rebase origin/develop
```
- Resolve conflicts locally, run tests, then push the updated branch.
- Avoid rebasing public branches that other people already depend on, unless everyone involved agrees.

---

## 4. Small / trivial changes

Tiny fixes (typos, very small documentation tweaks) may be committed directly to develop if:
- They clearly do not affect behavior.
- CI passes.

However, the default expectation remains: use short-lived branches and pull requests, even for small changes, to keep history and review consistent.

---
If the workflow evolves (additional long-lived branches, different strategies for hotfixes, etc.), this document and the [Contributing guide](../CONTRIBUTING.md#2-branches-and-commits) should be updated to reflect the actual process.

---
