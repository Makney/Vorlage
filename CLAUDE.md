---
workbench:
  project_name: {{PROJEKT_NAME}}
  default_model: {{DEFAULT_MODEL}}
  current_phase_file: docs/roadmap/PHASE1.md
  current_version: "0.0.0-dev"
  trigger_phrases:
    docs_update: "{{DOCS_TRIGGER}}"
    commit: "{{COMMIT_TRIGGER}}"
    release: "{{RELEASE_TRIGGER}}"
    fix: "{{FIX_TRIGGER}}"
    release_artifacts: "{{RELEASE_ARTIFACTS_TRIGGER}}"
    tag_push: "{{TAG_PUSH_TRIGGER}}"
  on_demand_files:
    - path: docs/release/VERSIONIERUNG.md
      trigger: "Read before any release-related work (versioning, release-review, tagging)"
      auto_inject: false
    - path: docs/release/RELEASES.md
      trigger: "Read when the user asks about released versions or release history"
      auto_inject: false
    - path: docs/release/REVIEW_TEMPLATE.md
      trigger: "Read when preparing a release code-review across all files changed since the last version"
      auto_inject: false
    - path: docs/COMMANDS.md
      trigger: "Read before running any shell command — verified syntax + project-specific commands"
      auto_inject: true
    - path: docs/CODING_RULES.md
      trigger: "Read for every implementation or refactoring task"
      auto_inject: false
    - path: docs/MARKDOWN_RULES.md
      trigger: "Read whenever creating or editing any .md file"
      auto_inject: false
    - path: docs/ARCHITEKTUR.md
      trigger: "Read for module-/data-flow questions or when extending a module"
      auto_inject: false
    - path: docs/FEATURES.md
      trigger: "Read to check feature status before planning or after completing a feature"
      auto_inject: false
    - path: docs/CHANGELOG.md
      trigger: "Read to recall what was recently built"
      auto_inject: false
    - path: docs/ENTSCHEIDUNGEN.md
      trigger: "Read before making or revisiting an architecture/scope decision"
      auto_inject: false
    - path: docs/roadmap/PHASE1.md
      trigger: "Read for Phase 1 features only"
      auto_inject: false
    - path: docs/roadmap/PHASE2.md
      trigger: "Read for Phase 2 features only"
      auto_inject: false
    - path: docs/roadmap/PHASE3.md
      trigger: "Read for Phase 3 features only"
      auto_inject: false
    - path: docs/GLOSSAR.md
      trigger: "Read when a domain term is unclear"
      auto_inject: false
    - path: docs/TECH_SCHULDEN.md
      trigger: "Read when refactoring or touching known-debt areas"
      auto_inject: false
    - path: docs/DEV_SETUP.md
      trigger: "Read when setting up the environment or debugging installation issues"
      auto_inject: false
    - path: docs/SEASON_LOG.md
      trigger: "Read at the start of a new season"
      auto_inject: false
    - path: docs/{{PROJEKT_NAME}}_ARCHITEKTUR.md
      trigger: "Read when designing or implementing core architecture features"
      auto_inject: false
---

# {{PROJEKT_NAME}} – Agent Context

You are a {{AGENT_ROLLE}}.

{{KURZBESCHREIBUNG}}.
Stack: {{STACK}}. Target platform: {{ZIELPLATTFORM}}.
Git repo: {{REPO_URL}}

## Working Rules (mandatory)

1. **Comment language: {{KOMMENTAR_SPRACHE}}** – Applies to code comments, docstrings, and commit messages.
2. **Variants before architecture decisions** – For non-trivial scope, first present variants A/B/C with effort table + clear recommendation. User decides.
   - Describe variants in **plain language** — no variable names, function signatures, or code snippets in the proposal.
   - Explain *what* each approach does differently and what the tradeoff is.
   - Code details only after the user picks a variant.
3. **Doc updates only on explicit signal** – Only when the user says the configured trigger phrase (see `workbench.trigger_phrases.docs_update` in frontmatter), then immediately and without prompting:
   - `docs/CHANGELOG.md` – New section at the top (date · title · what works now). No "changed files" lists – git history provides that.
   - `docs/FEATURES.md` – ⛔/🟡 → ✅
   - `docs/roadmap/PHASE<N>.md` – Mark the completed feature as ✅ only; do not restructure or rewrite other entries in this PHASE<N>.md file. The phase-level overview in `docs/roadmap/ROADMAP.md` is updated only when an entire phase closes.
   - `docs/ENTSCHEIDUNGEN.md` – For architecture decisions, add the *why*
   - `docs/TECH_SCHULDEN.md` – If a conscious shortcut was taken: add entry with risk + resolution.
   - `docs/SEASON_LOG.md` – Only at **end of season**: add retrospective entry (goal · result · what went well · blockers · hints for next season).
4. **Test scope per season** – Tests cover only the **newly added or changed feature**. No full-application regression runs unless explicitly requested.
   - Write targeted tests that verify the specific behavior introduced in this season.
   - If an existing test breaks due to the change, fix it — but don't expand coverage to unrelated areas.
5. **GitHub commit on explicit signal** – Only when the user says the configured trigger phrase (see `workbench.trigger_phrases.commit` in frontmatter), then immediately and without prompting:
   1. Stage only changed project files — never `.env`, secrets, or unrelated files.
   2. Commit with message format: `{{PROJEKT_NAME}}: <short description in {{KOMMENTAR_SPRACHE}}>`.
   3. `git push`.
6. **Pre-commit hook must be green** – Before committing, ensure linting and tests pass locally. If any check fails: fix the problem first, then commit.
7. **Release flow with four gates** – The release runs in four gates. Each gate fires only on its own configured trigger phrase from `workbench.trigger_phrases`. Never auto-advance to the next gate. Full procedure → [docs/release/VERSIONIERUNG.md](./docs/release/VERSIONIERUNG.md), orchestrator-Variante mit Sub-Agents → [docs/templates/RELEASE_START.md](./docs/templates/RELEASE_START.md).
   1. **`release` trigger** – Determine the next version per the schema in [docs/release/VERSIONIERUNG.md](./docs/release/VERSIONIERUNG.md) (MAJOR / MINOR / PATCH rules, plus the pre-1.0 breaking-change rule). Run `git diff --name-only v<prev>..HEAD`, group the changed files by area, and run the release-wide review per [docs/release/REVIEW_TEMPLATE.md](./docs/release/REVIEW_TEMPLATE.md). For multi-area diffs: start one read-only sub-agent per area in parallel. Present a consolidated findings report and wait.
   2. **`fix` trigger** – Apply only the findings I tagged for fixing. Move the rest into the matching `docs/code-review/OFFEN_<BEREICH>.md` (or into the next-phase roadmap). No code changes without this signal.
   3. **`release_artifacts` trigger** – Create release notes at `docs/release/v<MAJOR>.<MINOR>.<PATCH>.md` from [docs/release/TEMPLATE.md](./docs/release/TEMPLATE.md). Update [docs/release/RELEASES.md](./docs/release/RELEASES.md) (new row on top) AND the `workbench.current_version` field in this file's frontmatter — they must stay in sync. Prepend the version tag to the matching `docs/CHANGELOG.md` heading (`## YYYY-MM-DD — v<MAJOR>.<MINOR>.<PATCH> — <Titel>`). Show me the diff and wait.
   4. **`tag_push` trigger** – Only after linting and targeted tests are green (Rule 6): `git tag -a v<MAJOR>.<MINOR>.<PATCH> -m "{{PROJEKT_NAME}} v<MAJOR>.<MINOR>.<PATCH>"` then `git push origin v<MAJOR>.<MINOR>.<PATCH>`.

## Current Status

{{CURRENT_PHASE}} actively in development.

```text
→ [docs/roadmap/PHASE1.md](./docs/roadmap/PHASE1.md) — Open features of the current phase
→ [docs/FEATURES.md](./docs/FEATURES.md)             — Feature status matrix (✅/🟡/⛔)
→ [docs/CHANGELOG.md](./docs/CHANGELOG.md)           — Recently built features
→ [docs/{{PROJEKT_NAME}}_ARCHITEKTUR.md](./docs/{{PROJEKT_NAME}}_ARCHITEKTUR.md) — Master architecture reference
```
