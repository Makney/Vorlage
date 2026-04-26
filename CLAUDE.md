# {{PROJEKT_NAME}} – Agent Context

You are a {{AGENT_ROLLE}}.

{{KURZBESCHREIBUNG}}.
Stack: {{STACK}}. Target platform: {{ZIELPLATTFORM}}.
Git repo: {{REPO_URL}}

## Working Rules (mandatory)

1. **Comment language: {{KOMMENTAR_SPRACHE}}** – Applies to code comments, docstrings, and commit messages.
2. **Variants before architecture decisions** – For non-trivial scope, first present variants A/B/C with effort table + clear recommendation. User decides.
3. **Doc updates only on explicit signal** – Only when the user says **"war korrekt umgesetzt"**, then immediately and without prompting:
   - `docs/CHANGELOG.md` – New section at the top (date · title · what works now). No "changed files" lists – git history provides that.
   - `docs/FEATURES.md` – ⛔/🟡 → ✅
   - `docs/ROADMAP_PHASE<N>.md` – Mark completed feature as ✅
   - `docs/ENTSCHEIDUNGEN.md` – For architecture decisions, add the *why*
   - `docs/TECH_SCHULDEN.md` – If a conscious shortcut was taken: add entry with risk + resolution.
   - `docs/SEASON_LOG.md` – Only at **end of season**: add retrospective entry (goal · result · what went well · blockers · hints for next season).
4. **GitHub commit on explicit signal** – Only when the user says **"commit"**, then immediately and without prompting:
   1. Stage only changed project files — never `.env`, secrets, or unrelated files.
   2. Commit with message format: `{{PROJEKT_NAME}}: <short description in {{KOMMENTAR_SPRACHE}}>`.
   3. `git push`.

## Current Status

{{CURRENT_PHASE}} actively in development.

→ [docs/FEATURES.md](./docs/FEATURES.md)        — Feature status matrix (✅/🟡/⛔)
→ [docs/ROADMAP.md](./docs/ROADMAP.md)          — Phase overview
→ [{{AKTUELLE_PHASE_DATEI}}](./{{AKTUELLE_PHASE_DATEI}}) — Open features of the current phase
→ [docs/CHANGELOG.md](./docs/CHANGELOG.md)      — Recently built features
→ [docs/ARCHITEKTUR.md](./docs/ARCHITEKTUR.md)  — Module/data flow description
→ [docs/ENTSCHEIDUNGEN.md](./docs/ENTSCHEIDUNGEN.md) — *Why* decisions

## On-Demand Files (load only when needed)

These files are **not** loaded by default — read them only when the specific task type arises (keep context small):

- [docs/ROADMAP_PHASE1.md](./docs/ROADMAP_PHASE1.md) — **Read for Phase 1 features only.** Load only when implementing or planning a Phase 1 feature.
- [docs/ROADMAP_PHASE2.md](./docs/ROADMAP_PHASE2.md) — **Read for Phase 2 features only.** Load only when implementing or planning a Phase 2 feature.
- [docs/ROADMAP_PHASE3.md](./docs/ROADMAP_PHASE3.md) — **Read for Phase 3 features only.** Load only when implementing or planning a Phase 3 feature.
- [docs/GLOSSAR.md](./docs/GLOSSAR.md) — **Read when a domain term is unclear.** Project-specific vocabulary and abbreviations.
- [docs/TECH_SCHULDEN.md](./docs/TECH_SCHULDEN.md) — **Read when refactoring or touching known-debt areas.** Intentional shortcuts and their risk/resolution plan.
- [docs/DEV_SETUP.md](./docs/DEV_SETUP.md) — **Read when setting up the environment or debugging installation issues.** Dependencies, env vars, start commands.
- [docs/SEASON_LOG.md](./docs/SEASON_LOG.md) — **Read at the start of a new season.** Process retrospectives from past seasons.
