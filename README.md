# Vorlage

Meta-/Doku-Vorlage für neue Software-Projekte. Basiert auf der bewährten Struktur aus [TanaLib](https://github.com/Makney/TanaLib) und ist **stack-agnostisch** gehalten — es gibt kein Code-Gerüst, nur Agent-Kontext, Regeln und Workflow-Dokumente.

Ziel: Ein frisches Projekt soll vom ersten Commit an eine konsistente Kommunikation mit Coding-Agenten, eine saubere Entscheidungs-History und ein funktionierendes Feature-/Roadmap-Tracking haben — ohne dass man die Strukturen jedes Mal neu erfindet.

## Enthaltene Dateien

| Datei                                                              | Rolle                                                                              |
| ------------------------------------------------------------------ | ---------------------------------------------------------------------------------- |
| [CLAUDE.md](./CLAUDE.md)                                           | Auto-geladener Agent-Kontext (Projekt-Steckbrief, Arbeitsregeln, Coding-Verhalten) |
| [docs/README.md](./docs/README.md)                                 | Doku-Index (welche Datei wann lesen / schreiben)                                   |
| [docs/CODING_RULES.md](./docs/CODING_RULES.md)                     | Projektspezifische Coding-Konventionen (bei Code-Arbeit laden)                     |
| [docs/MARKDOWN_RULES.md](./docs/MARKDOWN_RULES.md)                 | Markdown-Konventionen (bei `.md`-Arbeit laden)                                     |
| [docs/ARCHITEKTUR.md](./docs/ARCHITEKTUR.md)                       | Modul-Aufbau, Datenflüsse, Persistenz                                              |
| [docs/ENTSCHEIDUNGEN.md](./docs/ENTSCHEIDUNGEN.md)                 | *Warum*-Entscheidungen (ADR-artig, mit Varianten-Pitch)                            |
| [docs/FEATURES.md](./docs/FEATURES.md)                             | Feature-Status-Matrix pro Bereich (✅ / 🟡 / ⛔)                                      |
| [docs/ROADMAP.md](./docs/ROADMAP.md)                               | Phasen-Übersicht                                                                   |
| [docs/ROADMAP_PHASE1.md](./docs/ROADMAP_PHASE1.md)                 | Phase 1 — minimal lauffähige Version                                               |
| [docs/ROADMAP_PHASE2.md](./docs/ROADMAP_PHASE2.md)                 | Phase 2 — intelligente Erweiterungen                                               |
| [docs/ROADMAP_PHASE3.md](./docs/ROADMAP_PHASE3.md)                 | Phase 3 — langfristige Features                                                    |
| [docs/CHANGELOG.md](./docs/CHANGELOG.md)                           | „Was kann der Nutzer jetzt, was vorher nicht ging?"                                |
| [docs/SEASON_PROMPT_TEMPLATE.md](./docs/SEASON_PROMPT_TEMPLATE.md) | Vorlage für Agent-Prompts pro Feature-Season                                       |
| [docs/CODE_REVIEW_TEMPLATE.md](./docs/CODE_REVIEW_TEMPLATE.md)     | Bauplan für wiederkehrende Code-Reviews                                            |
| [docs/CODE_REVIEW_OFFEN_TEMPLATE.md](./docs/CODE_REVIEW_OFFEN_TEMPLATE.md) | Leere Vorlage für bekannte, bewusst offen gelassene Befunde pro Bereich     |

## So nutzt du die Vorlage

1. **Repo erstellen**: Entweder „Use this template" auf GitHub oder `git clone` + `.git/`-Ordner löschen + neu initialisieren.
2. **Platzhalter ersetzen**: Die Vorlagen-Dateien enthalten Tokens der Form `{{NAME}}`. Alle mit einem globalen Suchen-und-Ersetzen auf den eigenen Projektkontext setzen. Eine Liste aller Tokens steht unten.
3. **Stack-spezifisches ausfüllen**: `CODING_RULES.md` hat ein ausgefülltes Python-Beispiel-Set als Abschnitt — durch das eigene Stack-Set ersetzen oder ergänzen.
4. **Architektur schreiben**: `docs/ARCHITEKTUR.md` mit dem ersten Entwurf der Modul-Struktur füllen, bevor Code entsteht.
5. **Phasen-Pitch**: Die drei `ROADMAP_PHASE*.md` sind als Gerüst angelegt — Inhalte befüllen, Phasen die nicht gebraucht werden löschen.
6. **CLAUDE.md anpassen**: Agent-Rolle, Projekt-Steckbrief und (wenn vorhanden) projektspezifische Regeln eintragen.

## Platzhalter-Liste

| Token                        | Bedeutung                                                            | Beispiel (TanaLib)                                            |
| ---------------------------- | -------------------------------------------------------------------- | ------------------------------------------------------------- |
| `{{PROJEKT_NAME}}`           | Name des Projekts                                                    | `TanaLib`                                                     |
| `{{KURZBESCHREIBUNG}}`       | Ein-Satz-Beschreibung der App                                        | `Desktop-App zur Verwaltung einer persönlichen E-Book-Sammlung` |
| `{{STACK}}`                  | Technologie-Stack kompakt                                            | `Python 3 · PySide6 · SQLite`                                 |
| `{{ZIELPLATTFORM}}`          | Zielplattform(en)                                                    | `Windows 11`                                                  |
| `{{REPO_URL}}`               | Git-Remote-URL                                                       | `https://github.com/Makney/TanaLib.git`                       |
| `{{AGENT_ROLLE}}`            | Wer der Agent ist (Profil, Seniorität)                               | `Senior-Python-Entwickler`                                    |
| `{{KOMMENTAR_SPRACHE}}`      | Sprache für Code-Kommentare und Doku                                 | `Deutsch`                                                     |
| `{{CURRENT_PHASE}}`          | Aktuell aktive Phase                                                 | `Phase 2 (v1.0)`                                              |
| `{{AKTUELLE_PHASE_DATEI}}`   | Dateiname der aktuellen Phasen-Roadmap                               | `docs/ROADMAP_PHASE2.md`                                      |

Die Liste ist bewusst kurz — alles Weitere (Modul-Namen, DB-Tabellen, Feature-Gruppen) ist pro Projekt so unterschiedlich, dass Freitext besser funktioniert als weitere Tokens.

## Quelle

Die Struktur ist destilliert aus der Praxis von [TanaLib](https://github.com/Makney/TanaLib) (Phase 1 → Phase 2). Änderungen an der Vorlage wandern zurück in dieses Repo, damit spätere Projekte vom Lern-Nachzug profitieren.
