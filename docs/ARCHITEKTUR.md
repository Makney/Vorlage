# Architecture

This file describes the **static structure** of the project: which modules exist, how they relate, and where data lives. Distinction from other docs:

- **CLAUDE.md** → Project overview (1 paragraph), reference points here
- **ENTSCHEIDUNGEN.md** → *why* the structure is the way it is (not here)
- **FEATURES.md / roadmap/ROADMAP.md** → what exists / will be built (not here)

## Folder Structure

```
{{PROJEKT_NAME}}/
├── <entry point>               # e.g. main.py / index.ts / cmd/<name>/main.go
├── <dependency manifest>       # requirements.txt / package.json / Cargo.toml …
├── <runtime artifacts>         # DB file, caches — excluded via .gitignore
├── .gitignore
│
├── <layer-1>/                  # e.g. database · core · backend
│   ├── <module>.ext
│   └── …
│
├── <layer-2>/                  # e.g. core · domain · service
│   └── …
│
├── <layer-3>/                  # e.g. ui · frontend · api
│   └── …
│
└── docs/                       # You are here
```

Layers are intentionally separated: *upper* imports from *lower*, never the reverse. This keeps business logic free from UI/framework dependencies and makes future swaps (different UI stack, different server) manageable.

## Startup Data Flow

```
<Entry point>
  ├─ <step 1 — e.g. DB init>
  ├─ <step 2 — e.g. load config>
  └─ <step 3 — e.g. launch main window / server>
       └─ <what happens at level 3>
```

## Data Flow for <Main Use Case>

Example placeholder — document a separate sequence for each important flow (import / request / render cycle …):

```
<Trigger>
  → <Action in layer 1>
  → <Action in layer 2>
  → <Result returned to layer 3>
```

## Data Model

If the project has a persistence layer: document tables / collections / schemas and their relationships briefly here.

### Table / Collection `<name>`

| Field | Type | Meaning |
| ----- | ---- | ------- |
| id    |      |         |
| …     |      |         |

Relationships: `<table_a> (1) ─── (n) <table_b>`.

Mark clearly what is **cached** (computed from source data) vs. **primary** (must be maintained) — otherwise the first "field set manually, not propagated" bug will be painful.

## Key Constructs / Patterns

Document project-specific patterns that appear repeatedly and would otherwise cause confusion when reading across the codebase. Typical examples:

- **Signal/event direction** — how do components communicate outward?
- **Thread/async model** — who may touch the UI, who may not?
- **Styling/theming strategy** — central file or component-local?
- **Configuration lookup** — where do values come from (ENV, settings store, config file)?

## Configuration / Persistence

| What             | Where                                                  |
| ---------------- | ------------------------------------------------------ |
| User settings    | `<Store>` — e.g. QSettings, OS Keychain, config.toml  |
| Project data     | `<File/DB>` — e.g. `{{PROJEKT_NAME}}.db`              |
| Generated assets | `<Folder>` — e.g. `assets/covers/`                    |
| Secrets          | **never in repo** — e.g. `.env` (ignored)             |

## Versioning

- Git remote: {{REPO_URL}}
- `.gitignore` excludes runtime artifacts (see file).
