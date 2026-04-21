# Doku-Index

Diese Datei beantwortet eine einzige Frage: **„Welche Doku-Datei lese / schreibe ich wann?"**

Sie wird nicht automatisch vom Agenten geladen — sie ist für Menschen gedacht, die sich neu ins Projekt einfinden, und für Agenten als gezieltes Nachschlagewerk.

## Orientierungs-Reihenfolge für Neueinsteiger

1. [CLAUDE.md](../CLAUDE.md) — was für ein Projekt ist das, welche Regeln gelten.
2. [ARCHITEKTUR.md](./ARCHITEKTUR.md) — Modul-Aufbau, Datenflüsse.
3. [FEATURES.md](./FEATURES.md) — was ist fertig, was nicht.
4. [CHANGELOG.md](./CHANGELOG.md) — was zuletzt gebaut wurde.

## Wer liest was, wann?

| Situation                                             | Datei                                                                  |
| ----------------------------------------------------- | ---------------------------------------------------------------------- |
| Neue Session / Agent startet                          | `CLAUDE.md` (auto-geladen) + aktueller Season-Prompt                   |
| Aufgabe: Code schreiben / refactorn                   | + `CODING_RULES.md`                                                    |
| Aufgabe: Markdown schreiben / bearbeiten              | + `MARKDOWN_RULES.md`                                                  |
| Überblick: was ist überhaupt drin?                    | `FEATURES.md`                                                          |
| Überblick: was kommt als nächstes?                    | `ROADMAP.md` + aktuelle `ROADMAP_PHASE<N>.md`                          |
| Frage „warum haben wir das damals so gebaut?"         | `ENTSCHEIDUNGEN.md`                                                    |
| Frage „was hat sich diese Woche getan?"               | `CHANGELOG.md` (oberer Eintrag)                                        |
| Neue Season vorbereiten                               | `SEASON_PROMPT_TEMPLATE.md`                                            |
| Code-Review starten                                   | `CODE_REVIEW_TEMPLATE.md` + passende `CODE_REVIEW_OFFEN_<BEREICH>.md`  |

## Wer schreibt was, wann?

| Auslöser                                               | Ziel-Datei(en)                                             |
| ------------------------------------------------------ | ---------------------------------------------------------- |
| Feature wurde implementiert (Nutzer-Signal)            | `CHANGELOG.md` (neuer Abschnitt oben) + `FEATURES.md` (Status) + `ROADMAP_PHASE<N>.md` (Status) |
| Architektur-/Scope-Entscheidung getroffen              | `ENTSCHEIDUNGEN.md` (neuer *Warum*-Eintrag)                |
| Neues Modul / neuer Datenflusses dazugekommen          | `ARCHITEKTUR.md`                                           |
| Neues Feature eingeplant                               | passende `ROADMAP_PHASE<N>.md`                             |
| Neue Phase eröffnet                                    | `ROADMAP.md` (Tabelle) + neue `ROADMAP_PHASE<N>.md` anlegen |
| Code-Review fand bewusst offen gelassene Befunde       | `CODE_REVIEW_OFFEN_<BEREICH>.md` anlegen / erweitern       |
| Neue projektspezifische Coding-Konvention              | `CODING_RULES.md`                                          |

## Was explizit NICHT hier landet

- **Detail-Änderungen pro Commit** → steht in der Git-History, nicht im `CHANGELOG`.
- **Was ist der Code?** → liest man im Code, nicht in der Architektur-Doku.
- **Tagesgeschäft / To-Dos** → gehört in Issues oder den Season-Prompt, nicht in die Roadmap.

## Pflegerhythmus

- **CLAUDE.md**: selten. Nur wenn sich Projekt-Identität oder Regeln ändern.
- **ARCHITEKTUR.md**: mittel. Bei jeder strukturellen Erweiterung (neues Modul, neue Tabelle).
- **FEATURES.md / CHANGELOG.md / ROADMAP_PHASE\<N\>.md**: oft. Nach jeder abgeschlossenen Season.
- **ENTSCHEIDUNGEN.md**: bei Bedarf. Wenn eine nicht-triviale Variante gewählt wurde.
- **Regeln (CODING / MARKDOWN)**: selten, nach harten Lernerfahrungen.
