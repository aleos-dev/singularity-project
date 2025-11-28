# Project Meta: Labels, Areas, Priorities

This document defines the label set and the meaning of each value.
The goal is to have a consistent way to filter, triage, and reason about the backlog.

The [Contributing guide](../CONTRIBUTING.md#13-issue-labels-overview) explains when and how labels
are applied in day-to-day work; here we focus on the classification
scheme itself (types, workflow labels, priorities, areas).

---

## 0. Axes of classification

Labels help classify work along four axes:

- **Issue type** – *why are we doing this / what kind of work is this?*  
- **Area** – *which part of the system or process does this primarily relate to?*  
- **Priority** – *how urgent is this for the project?*  
- **Workflow** – *how should this issue be handled?* (question, help wanted, duplicate, wontfix, etc.)

---

## 1. Issue labels (types)

These labels describe what kind of work an issue represents:

- `feature` – new feature or user-visible behavior change.
- `enhancement` – improvement or extension to existing functionality.
- `bug` – unexpected problem or incorrect behavior.
- `chore` – maintenance work without direct user-facing changes
  (refactors, dependency updates, build/CI tweaks, technical cleanups).
- `documentation` – work whose primary goal is to improve documentation
  about the system (domains, features, APIs, architecture, usage, etc.).
- `meta` – work whose primary goal is to change how the project and workflow
  behave (label scheme, branch protection rules, CI/CD structure,
  issue/PR templates, branching strategy, etc.).

Classification is based on **impact**, not on which files are touched.

---

## 2. Workflow labels

These labels describe the **state or special handling** of an issue.

- `question` – issue needs clarification or more information.  
- `help wanted` – maintainer is asking for help; open invitation to contributors.  
- `good first issue` – small, well-scoped issue suitable for newcomers.  
- `duplicate` – this issue is already covered by another one; link the canonical issue.  
- `wontfix` – decided not to work on this issue (out of scope, wrong trade-offs, obsolete).

Workflow labels refine how an issue should be handled.
They do not replace type, area, or priority labels.

---

## 3. Priority labels

Priority labels express how urgent an issue is for the project:

- `priority:P0` – **Critical**: must be addressed as soon as possible
  (broken build on `main`/`develop`, critical blocking bugs, milestone blockers).
- `priority:P1` – **High**: important for the current or next milestone.
- `priority:P2` – **Normal**: useful work scheduled after P0/P1 items.
- `priority:P3` – **Low / Backlog**: “someday, if it still matters” items.

---

## 4. Areas
In addition to labels, the project uses **areas** to describe the main
context of the work.

An area answers the question: *"Which part of the system or process does
this primarily relate to?"*

Typical areas:
- `domain` – domain-level functionality.
- `auth` – authentication and authorization.
- `workflow` – process and workflow rules for working with the repo
  (issues, labels, branches, PR conventions, etc.).
- `build` – build system, CI/CD pipelines, automation, Gradle configuration.
- `infra` – cross-cutting infrastructure: docker-compose, shared environments,
  reverse proxy, deployment-related setup.

The list of areas may evolve over time. When new areas are introduced, update the project board, [Contributing guide](../CONTRIBUTING.md#13-issue-labels-overview), and this document to keep them in sync.

---

## 5. Templates

- Issue templates live under `.github/ISSUE_TEMPLATE/`:
  - **general** – features, enhancements, chores, meta tasks.
  - **bug** – defects and regressions.
- The pull request template lives at [`pull_request_template.md`](../.github/pull_request_template.md) and enforces:
  - Summary
  - Details
  - Testing

The [Contributing guide](../CONTRIBUTING.md#14-issue-templates) describes how to use these templates in practice.

---
