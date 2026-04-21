# Markdown-Regeln ({{PROJEKT_NAME}})

Verbindliche Formatierungsregeln für **alle** `.md`-Dateien im Projekt.
Ziel: einheitliches Erscheinungsbild, saubere Git-Diffs, schnelles Parsing durch den Agenten.

Beim Erstellen oder Bearbeiten einer Markdown-Datei: diese Regeln als Checkliste abarbeiten.

---

## 1. Dateinamen

- `SCREAMING_SNAKE_CASE.md` für Doku-Dateien (z.B. `FEATURES.md`, `ROADMAP_PHASE2.md`).
- Ausnahmen: `README.md`, `CLAUDE.md` (Konvention).
- Code-Review-Dateien: `CODE_REVIEW_OFFEN_<BEREICH>.md` – Bereich statt fortlaufender Nummer. Bei Bedarf Unterbereich mit weiterem `_` anhängen.

## 2. Überschriften

- **Nur ATX-Stil** (`#`, `##`, `###`). Kein Setext (Unterstreichung).
- Genau eine Leerzeile **vor** und **nach** jeder Überschrift.
- `#` = Dateititel, **einmal pro Datei** ganz oben.
- Hierarchie nicht überspringen (`##` → `###`, nicht `##` → `####`).

## 3. Listen

- Ungeordnete Listen: **`-`** (Bindestrich). Niemals `*` oder `+`.
- Geordnete Listen: `1.`, `2.`, `3.` …
- Einrückung Sub-Listen: **2 Leerzeichen** (nicht 4, keine Tabs).
- Vor der ersten Listenzeile eine Leerzeile; Listen nicht direkt an eine Überschrift kleben.

## 4. Code

- Fenced Code Blocks mit **Sprach-Tag**: ` ```python `, ` ```sql `, ` ```bash `, ` ```ts `.
- ASCII-Art / Tree-Diagramme: Fence ohne Sprach-Tag ist OK.
- Inline-Code mit Backticks für: Dateinamen, Pfade, Funktionsnamen, Klassen, Variablen, CLI-Kommandos, Spaltennamen.

## 5. Tabellen

- Standard-Pipe-Syntax: `| Spalte | Spalte |`, Trennlinie `| --- | --- |`.
- Links-Alignment (Default) – keine `:---:` / `---:` Varianten verwenden.
- Eine Leerzeile vor und nach der Tabelle.

## 6. Hervorhebungen

- `**bold**` für **Wichtiges**, Feature-Namen, UI-Menüpunkte.
- `*italic*` **sparsam** für Betonung einzelner Begriffe.
- Kein `__bold__`, kein `_italic_` (Unterstrich-Varianten).
- Niemals ganze Absätze fett setzen.

## 7. Emojis (geschlossenes Set)

**Nur diese fünf Emojis sind erlaubt. Keine Erweiterung ohne Absprache.**

| Emoji | Bedeutung                     | Einsatz                      |
| ----- | ----------------------------- | ---------------------------- |
| ✅     | abgeschlossen / aktiv         | FEATURES, ROADMAP, CHANGELOG |
| 🟡    | teilweise / in Entwicklung    | FEATURES, ROADMAP            |
| ⛔     | offen / geplant               | FEATURES, ROADMAP            |
| ⚠️    | Warnung / wichtiger Hinweis   | ROADMAP, CODE_REVIEW         |
| 💡    | Idee / Verbesserungsvorschlag | CODE_REVIEW                  |

- **Kein weiterer Dekor-Emoji-Einsatz** (keine 🚀, 🎉, 📝 etc.).
- Primär in Status-/Roadmap-/Changelog-/Review-Dateien. README, ARCHITEKTUR, ENTSCHEIDUNGEN bleiben emoji-frei, außer zur Status-Markierung.

## 8. Sonderzeichen

- **Pfeil `→`** (U+2192) für Querverweise und Richtungsangaben:
  - `→ docs/FEATURES.md` (Verweis auf Datei)
  - `⛔ → ✅` (Statuswechsel)
- **Em-Dash `—`** (U+2014) als Trenner in Überschriften/CHANGELOG-Einträgen:
  - `## 2026-04-19 — Titel des Eintrags`
- **Kein `->"**, kein `--`, kein `=>`.

## 9. Separatoren

- `---` (drei Bindestriche) als horizontale Trennlinie zwischen großen Abschnitten.
- Je eine Leerzeile davor und danach.
- Sparsam einsetzen – nicht nach jeder Überschrift.

## 10. Links

- Markdown-Syntax: `[Anzeigetext](./docs/DATEI.md)`.
- **Immer relativ** und **mit `./`-Präfix** für interne Dokumente:
  - ✅ `[Features](./docs/FEATURES.md)`
  - ⛔ `[Features](docs/FEATURES.md)`
  - ⛔ `[Features](/docs/FEATURES.md)`
- Externe Links: volle URL `https://…`.
- Zeilen-Referenzen im Code: `[datei.ext:42](./modul/datei.ext)` (ohne Line-Anchor – wird nicht gerendert, aber Konvention halten).

## 11. Frontmatter

- **Keine** YAML-Frontmatter (`---\n...\n---` am Dateianfang).
- Metadaten stehen im Fließtext oder in Tabellen.

## 12. Zeilenlänge

- **Kein Hard-Wrap.** Absätze als eine fließende Zeile schreiben.
- Grund: Git-Diffs bleiben bei Wortänderungen sauber, Renderer bricht selbst um.
- Ausnahme: Listen, Tabellen, Code – da natürlicher Umbruch pro Eintrag.

## 13. CHANGELOG-Format

- Neuer Eintrag **oben** in `docs/CHANGELOG.md`.
- Überschrift: `## YYYY-MM-DD — Titel` (em-dash `—`, keine Binde- oder Spiegelstriche).
- Unterabschnitte wenn nötig als `###`.
- **Keine** „Geänderte Dateien"-Listen (liefert Git-History).

## 14. Blockquotes / Callouts

- Standard-Blockquote `> …` nur für echte Zitate.
- **Kein** GitHub-Callout-Syntax (`> [!NOTE]`, `> [!WARNING]`) – stattdessen ⚠️-Emoji + fetten Text.

## 15. Leerzeilen & Whitespace

- Datei endet mit **genau einer** Leerzeile (Newline am Ende).
- Keine doppelten Leerzeilen zwischen Abschnitten (eine reicht).
- Keine trailing Spaces am Zeilenende.

---

## Schnell-Checkliste vor dem Speichern

1. Dateiname in `SCREAMING_SNAKE_CASE.md`?
2. Nur ein `#`-H1 ganz oben, Hierarchie sauber?
3. Listen mit `-`, 2-Space-Einrückung?
4. Code-Fences mit Sprach-Tag?
5. Nur Emojis aus dem geschlossenen Set (✅ 🟡 ⛔ ⚠️ 💡)?
6. Interne Links mit `./`-Präfix?
7. Keine Frontmatter, kein Hard-Wrap?
8. Em-Dash `—` statt `-` in Datums-Überschriften?
9. Datei endet mit genau einer Newline?
