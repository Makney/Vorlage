# Vorlage

Meta-/Doku-Vorlage für neue Software-Projekte. Voll-kompatibel zur [TakumiDeck](https://github.com/Makney/TakumiDeck)-Workbench: die `workbench:`-YAML-Frontmatter in `CLAUDE.md` wird von der App gelesen, alle Pfade folgen der TakumiDeck-Konvention. Die Vorlage ist **stack-agnostisch** gehalten — es gibt kein Code-Gerüst, nur Agent-Kontext, Regeln und Workflow-Dokumente.

Ziel: Ein frisches Projekt soll vom ersten Commit an eine konsistente Kommunikation mit Coding-Agenten, eine saubere Entscheidungs-History und ein funktionierendes Feature-/Roadmap-Tracking haben — ohne dass man die Strukturen jedes Mal neu erfindet.

## Struktur

```
.
├── CLAUDE.md                       — Auto-geladener Agent-Kontext, YAML-Frontmatter mit workbench-Config
├── CLAUDE.local.md                 — Lokale Overrides (in abgeleiteten Projekten nicht committed)
├── README.md                       — Diese Datei
├── .claude/
│   └── rules/                      — Auto-Inject-Regeln für Claude Code
│       ├── coding-rules.md
│       └── markdown-rules.md
└── docs/
    ├── README.md                   — Doku-Index („wer liest/schreibt was wann?")
    ├── ARCHITEKTUR.md              — Modul-Aufbau, Datenflüsse (Detail-Doku)
    ├── {{PROJEKT_NAME}}_ARCHITEKTUR.md — Master-Architektur-Referenz (Skelett)
    ├── CODING_RULES.md             — Coding-Konventionen (on-demand)
    ├── MARKDOWN_RULES.md           — Markdown-Konventionen (on-demand)
    ├── FEATURES.md                 — Feature-Status-Matrix (✅/🟡/⛔)
    ├── CHANGELOG.md                — Was kann der Nutzer jetzt, was vorher nicht ging?
    ├── ENTSCHEIDUNGEN.md           — Warum-Entscheidungen (ADR-artig)
    ├── TECH_SCHULDEN.md            — Bewusste Shortcuts mit Auflösungsplan
    ├── GLOSSAR.md                  — Domain-Vokabular
    ├── DEV_SETUP.md                — Setup-Anleitung
    ├── SEASON_LOG.md               — Season-Retrospektiven
    ├── roadmap/
    │   ├── ROADMAP.md              — Phasen-Übersicht
    │   ├── PHASE1.md               — MVP
    │   ├── PHASE2.md               — Komfort/v1.0
    │   └── PHASE3.md               — Power-Features
    ├── code-review/
    │   ├── TEMPLATE.md             — Bauplan für wiederkehrende Reviews
    │   └── OFFEN_TEMPLATE.md       — Vorlage für „bewusst offen"-Listen
    ├── release/
    │   ├── VERSIONIERUNG.md        — Versionsschema + Release-Ablauf (Quelle der Wahrheit)
    │   ├── RELEASES.md             — Index aller veröffentlichten Versionen
    │   ├── REVIEW_TEMPLATE.md      — Bauplan für den Release-Code-Review
    │   └── TEMPLATE.md             — Vorlage für eine einzelne Release-Notes-Datei
    └── templates/
        ├── SEASON_PROMPT.md        — Season-Prompt-Template (TakumiDeck-App liest es)
        ├── BUG_REPORT.md           — Bug-Report-Template (TakumiDeck-App liest es)
        ├── CODE_REVIEW_START.md    — Orchestrator-Template für Code-Review-Läufe (Sub-Agents)
        └── RELEASE_START.md        — Orchestrator-Template für Release-Läufe (Sub-Agents)
```

## So nutzt du die Vorlage

1. **Repo erstellen**: Entweder „Use this template" auf GitHub oder `git clone` + `.git/`-Ordner löschen + neu initialisieren.
2. **Platzhalter ersetzen**: Die Vorlagen-Dateien enthalten Tokens der Form `{{NAME}}`. Alle mit einem globalen Suchen-und-Ersetzen auf den eigenen Projektkontext setzen. Eine Liste aller Tokens steht unten.
3. **`{{PROJEKT_NAME}}_ARCHITEKTUR.md` umbenennen**: Datei `docs/{{PROJEKT_NAME}}_ARCHITEKTUR.md` muss auch im Dateinamen ersetzt werden (z.B. `docs/MeineApp_ARCHITEKTUR.md`).
4. **Stack-spezifisches ausfüllen**: `CODING_RULES.md` Section 8 mit Stack-spezifischen Regeln ergänzen.
5. **Architektur schreiben**: `docs/{{PROJEKT_NAME}}_ARCHITEKTUR.md` mit dem ersten Entwurf befüllen, bevor Code entsteht.
6. **Phasen-Pitch**: Die drei `roadmap/PHASE*.md` sind als Gerüst angelegt — Inhalte befüllen, Phasen die nicht gebraucht werden löschen.
7. **CLAUDE.md anpassen**: YAML-Frontmatter (`workbench:`) auf das Projekt zuschneiden — besonders `default_model`, `current_phase_file` und die `trigger_phrases`.

## Platzhalter-Liste

| Token                        | Bedeutung                                                            | Beispiel                                                      |
| ---------------------------- | -------------------------------------------------------------------- | ------------------------------------------------------------- |
| `{{PROJEKT_NAME}}`           | Name des Projekts                                                    | `TakumiDeck`                                                  |
| `{{KURZBESCHREIBUNG}}`       | Ein-Satz-Beschreibung der App                                        | `Persönliches Multi-Session-Management-Tool für Claude Code`  |
| `{{STACK}}`                  | Technologie-Stack kompakt                                            | `TypeScript · Electron · React · SQLite`                      |
| `{{ZIELPLATTFORM}}`          | Zielplattform(en)                                                    | `Windows 11`                                                  |
| `{{REPO_URL}}`               | Git-Remote-URL                                                       | `https://github.com/Makney/TakumiDeck.git`                    |
| `{{AGENT_ROLLE}}`            | Wer der Agent ist (Profil, Seniorität)                               | `Senior TypeScript Developer mit Schwerpunkt Electron`        |
| `{{KOMMENTAR_SPRACHE}}`      | Sprache für Code-Kommentare und Doku                                 | `Deutsch`                                                     |
| `{{CURRENT_PHASE}}`          | Aktuell aktive Phase (Fließtext)                                     | `Phase 2 (v1.0)`                                              |
| `{{DEFAULT_MODEL}}`          | Claude-Modell-ID für Standard-Sessions                               | `claude-sonnet-4-6`                                           |
| `{{DOCS_TRIGGER}}`           | Trigger-Phrase für Doku-Updates                                      | `ist korrekt umgesetzt`                                       |
| `{{COMMIT_TRIGGER}}`         | Trigger-Phrase für Git-Commit                                        | `commit`                                                      |
| `{{RELEASE_TRIGGER}}`        | Trigger-Phrase für Release-Code-Review (Gate 1)                      | `release vorbereiten`                                         |
| `{{FIX_TRIGGER}}`            | Trigger-Phrase für Fix-Anwendung nach Review (Gate 2)                | `fix it`                                                      |
| `{{RELEASE_ARTIFACTS_TRIGGER}}` | Trigger-Phrase für Release-Notes + Indizes (Gate 3)               | `release artefakte`                                           |
| `{{TAG_PUSH_TRIGGER}}`       | Trigger-Phrase für Git-Tag + Push (Gate 4)                           | `tag und push`                                                |
| `{{CURRENT_VERSION}}`        | Aktuelle Release-Version (im Frontmatter `workbench.current_version`, wird vom Release-Flow gepflegt) | `0.1.0`                            |
| `{{DATUM}}`                  | Stand-Datum im Architektur-Skelett                                   | `2026-05-15`                                                  |

Die Liste ist bewusst kurz — alles Weitere (Modul-Namen, DB-Tabellen, Feature-Gruppen) ist pro Projekt so unterschiedlich, dass Freitext besser funktioniert als weitere Tokens.

## Kompatibilität zu TakumiDeck

Die Vorlage spiegelt 1:1 die Struktur, die [TakumiDeck](https://github.com/Makney/TakumiDeck) zum Lesen erwartet:

- `CLAUDE.md` mit YAML-Frontmatter (`workbench.project_name`, `workbench.current_phase_file`, `workbench.current_version`, `workbench.trigger_phrases`, `workbench.on_demand_files`)
- `docs/templates/*.md` als von der App gelesene Prompt-Templates (Bracketed Paste mit `{{...}}`-Befüllung):
  - `SEASON_PROMPT.md` — Start einer Feature-Season
  - `BUG_REPORT.md` — strukturierte Bug-Meldung
  - `CODE_REVIEW_START.md` — Orchestrator für Code-Review-Läufe
  - `RELEASE_START.md` — Orchestrator für Release-Läufe
- Phasen-Dateien in `docs/roadmap/PHASE<N>.md`
- Master-Architektur in `docs/{{PROJEKT_NAME}}_ARCHITEKTUR.md`

Wer die Vorlage benutzt, kann das resultierende Projekt sofort als neuen Eintrag in TakumiDeck einbinden — Status-Lesung, Phase-Erkennung und Season-Spawn funktionieren ohne weitere Anpassung.

## Quelle

Die Struktur entstand parallel zur Praxis von [TanaLib](https://github.com/Makney/TanaLib) und wurde durch [TakumiDeck](https://github.com/Makney/TakumiDeck) konsolidiert. Änderungen an der Vorlage wandern zurück in dieses Repo, damit spätere Projekte vom Lern-Nachzug profitieren.
