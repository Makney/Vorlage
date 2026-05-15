# Doku-Index

Diese Datei beantwortet eine einzige Frage: **„Welche Doku-Datei lese / schreibe ich wann?"**

Sie wird nicht automatisch vom Agenten geladen — sie ist für Menschen gedacht, die sich neu ins Projekt einfinden, und für Agenten als gezieltes Nachschlagewerk.

## Orientierungs-Reihenfolge für Neueinsteiger

1. [CLAUDE.md](../CLAUDE.md) — was für ein Projekt ist das, welche Regeln gelten.
2. [{{PROJEKT_NAME}}_ARCHITEKTUR.md](./{{PROJEKT_NAME}}_ARCHITEKTUR.md) — Master-Architektur-Referenz.
3. [ARCHITEKTUR.md](./ARCHITEKTUR.md) — Modul-Aufbau, Datenflüsse (Detail-Doku).
4. [FEATURES.md](./FEATURES.md) — was ist fertig, was nicht.
5. [CHANGELOG.md](./CHANGELOG.md) — was zuletzt gebaut wurde.

## Wer liest was, wann?

| Situation                                     | Datei                                                                            |
| --------------------------------------------- | -------------------------------------------------------------------------------- |
| Neue Session / Agent startet                  | `CLAUDE.md` (auto-geladen) + aktueller Season-Prompt                             |
| Aufgabe: Code schreiben / refactorn           | + `CODING_RULES.md`                                                              |
| Aufgabe: Markdown schreiben / bearbeiten      | + `MARKDOWN_RULES.md`                                                            |
| Überblick: was ist überhaupt drin?            | `FEATURES.md`                                                                    |
| Überblick: was kommt als nächstes?            | `roadmap/ROADMAP.md` + aktuelle `roadmap/PHASE<N>.md`                            |
| Frage „warum haben wir das damals so gebaut?" | `ENTSCHEIDUNGEN.md`                                                              |
| Frage „was hat sich diese Woche getan?"       | `CHANGELOG.md` (oberer Eintrag)                                                  |
| Neue Season vorbereiten                       | `templates/SEASON_PROMPT.md`                                                     |
| Season abgeschlossen — Rückblick schreiben    | `SEASON_LOG.md`                                                                  |
| Begriff oder Abkürzung unklar                 | `GLOSSAR.md`                                                                     |
| Umgebung einrichten / Installationsproblem    | `DEV_SETUP.md`                                                                   |
| Bug an den Agenten melden                     | `templates/BUG_REPORT.md`                                                        |
| Code-Review starten (Session-Prompt)          | `templates/CODE_REVIEW_START.md` (Orchestrator) + `code-review/TEMPLATE.md` (Bauplan) + passende `code-review/OFFEN_<BEREICH>.md` |
| Release vorbereiten / Versionsschema klären   | `release/VERSIONIERUNG.md` + `release/RELEASES.md`                               |
| Release-Lauf starten (Session-Prompt)         | `templates/RELEASE_START.md` (Orchestrator) + `release/REVIEW_TEMPLATE.md` (Bauplan) + `release/TEMPLATE.md` (Notes-Vorlage) |

## Wer schreibt was, wann?

| Auslöser                                          | Ziel-Datei(en)                                                                                       |
| ------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| Feature wurde implementiert (Nutzer-Signal)       | `CHANGELOG.md` (neuer Abschnitt oben) + `FEATURES.md` (Status) + `roadmap/PHASE<N>.md` (Status)      |
| Architektur-/Scope-Entscheidung getroffen         | `ENTSCHEIDUNGEN.md` (neuer *Warum*-Eintrag)                                                          |
| Neues Modul / neuer Datenflusses dazugekommen     | `ARCHITEKTUR.md` (Detail) und/oder `{{PROJEKT_NAME}}_ARCHITEKTUR.md` (Master, bei größeren Änderungen) |
| Neues Feature eingeplant                          | passende `roadmap/PHASE<N>.md`                                                                       |
| Neue Phase eröffnet                               | `roadmap/ROADMAP.md` (Tabelle) + neue `roadmap/PHASE<N>.md` anlegen                                  |
| Code-Review fand bewusst offen gelassene Befunde  | `code-review/OFFEN_<BEREICH>.md` anlegen / erweitern                                                 |
| Neue projektspezifische Coding-Konvention         | `CODING_RULES.md`                                                                                    |
| Bewusster Hack / temporäre Vereinfachung          | `TECH_SCHULDEN.md` (neuer Eintrag mit Risiko + Auflösungsplan)                                       |
| Season abgeschlossen                              | `SEASON_LOG.md` (Retrospektiv-Eintrag oben anfügen)                                                  |
| Neuer Domain-Begriff / Abkürzung eingeführt       | `GLOSSAR.md`                                                                                         |
| Setup-Schritt oder Abhängigkeit hat sich geändert | `DEV_SETUP.md`                                                                                       |
| Release veröffentlicht                            | `release/v<MAJOR>.<MINOR>.<PATCH>.md` (aus `release/TEMPLATE.md`) + `release/RELEASES.md` (Index) + `current_version` in `CLAUDE.md` |

## Was explizit NICHT hier landet

- **Detail-Änderungen pro Commit** → steht in der Git-History, nicht im `CHANGELOG`.
- **Was ist der Code?** → liest man im Code, nicht in der Architektur-Doku.
- **Tagesgeschäft / To-Dos** → gehört in Issues oder den Season-Prompt, nicht in die Roadmap.

## Pflegerhythmus

- **CLAUDE.md**: selten. Nur wenn sich Projekt-Identität oder Regeln ändern.
- **{{PROJEKT_NAME}}_ARCHITEKTUR.md**: bei größeren Architektur-Entscheidungen.
- **ARCHITEKTUR.md**: mittel. Bei jeder strukturellen Erweiterung (neues Modul, neue Tabelle).
- **FEATURES.md / CHANGELOG.md / roadmap/PHASE\<N\>.md**: oft. Nach jeder abgeschlossenen Season.
- **ENTSCHEIDUNGEN.md**: bei Bedarf. Wenn eine nicht-triviale Variante gewählt wurde.
- **TECH_SCHULDEN.md**: bei Bedarf. Wenn ein bewusster Hack gemacht wurde.
- **SEASON_LOG.md**: einmal pro Season. Am Ende, nach dem letzten Feature.
- **GLOSSAR.md / DEV_SETUP.md**: selten. Nur wenn sich Begriffe oder Setup-Schritte ändern.
- **Regeln (CODING / MARKDOWN)**: selten, nach harten Lernerfahrungen.
- **release/RELEASES.md / release/v\<X.Y.Z\>.md**: bei Bedarf. Eine neue Datei pro Release, Index-Tabelle in `RELEASES.md` aktualisieren. Schema dazu → `release/VERSIONIERUNG.md` (sehr selten geändert).
