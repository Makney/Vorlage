# Coding-Regeln ({{PROJEKT_NAME}})

Projektspezifische Konventionen. Ergänzung — nicht Ersatz — zu den allgemeinen Regeln in [CLAUDE.md](../CLAUDE.md) (Abschnitt „Coding-Verhalten").

**Hierarchie bei Konflikten:** `CLAUDE.md` > `CODING_RULES.md` > Stack-Standard (z.B. PEP 8 / Prettier / rustfmt).

Diese Datei wird **nur bei Bedarf** gelesen (bei Implementierungs- oder Refactor-Aufgaben), nicht standardmäßig geladen.

---

## 1. Naming

- Module / Funktionen / Variablen: `<stil vom stack: snake_case | camelCase | …>`.
- Klassen / Typen: `<stil: PascalCase | …>`.
- Konstanten: `<stil: UPPER_SNAKE_CASE | …>`.
- Private Symbole: `<konvention: führender Unterstrich | #-Prefix | private-Keyword | …>`.
- Boolean-Namen: Präfix `is_`, `has_`, `should_`.

## 2. Imports / Module

- Block-Reihenfolge: 1) Stdlib · 2) Third-Party · 3) Projekt-lokal (je getrennt durch Leerzeile).
- Innerhalb jedes Blocks alphabetisch.
- **Keine Wildcard-Imports.**
- Ungenutzte Imports entfernen — aber nur, wenn sie durch eigene Änderungen verwaist sind (CLAUDE.md Regel 3).
- Relative Imports nur innerhalb eines Pakets, sonst absolute.

## 3. Type-Hints / Typisierung

- Wenn vom Stack unterstützt: Public-API immer annotiert, interne Helfer nach Bedarf.
- Konsistenz innerhalb einer Funktion: alle Parameter **und** Return-Type, oder gar nicht.
- `Any` / `unknown` / `object` nur wenn unvermeidbar, mit Kommentar warum.

## 4. Docstrings & Kommentare

- Sprache: **{{KOMMENTAR_SPRACHE}}** (aus CLAUDE.md). Gilt für Docstrings und Inline-Kommentare.
- Docstrings nur wo sie echten Mehrwert bringen:
  - Public-Funktionen mit nicht-trivialem Verhalten
  - Komplexe Algorithmen
  - Stack-/Framework-Spezialitäten, die über Standard hinausgehen
- Einfache Getter / Setter / triviale Wrapper brauchen **keinen** Docstring.
- Inline-Kommentare: **warum**, nicht **was**. Redundante Kommentare weglassen.

## 5. Funktions- & Methoden-Design

- Richtwert: ~50 Zeilen pro Funktion. Kein harter Grenzwert — wenn etwas inhaltlich 80 Zeilen braucht, ist das OK. Ab >100 Zeilen: Teilschritte extrahieren prüfen.
- Eine Funktion macht **eine Sache**. Handler, die fünf unabhängige Dinge tun → aufteilen.
- Parameter-Anzahl: Richtwert ≤ 5. Darüber: Datenobjekt erwägen (aber nicht schematisch — siehe CLAUDE.md Regel 2).
- Keine mutablen Defaults (sprachabhängige Falle — prüfen, ob dein Stack das Problem hat).

## 6. Error-Handling

- **Nur für reale Szenarien** (CLAUDE.md Regel 2). Kein spekulatives Try/Catch.
- Fänge so spezifisch wie möglich. Generische Top-Level-Catches nur am Rand der Anwendung (Request-Handler, Worker), dann mit Logging/User-Feedback.
- Niemals stumme `catch (_) {}` / `except: pass`-Blöcke. Wenn wirklich ignoriert werden soll, mit Kommentar warum.
- Ressourcen (Verbindungen, Dateien, Locks) über die idiomatische Auto-Cleanup-Konstruktion des Stacks (`with`, `using`, `defer`, RAII …).

## 7. Persistenz / Datenzugriff

- Bei SQL: Parameter-Binding, **niemals** String-Concatenation (SQL-Injection — auch in Single-User-Projekten als Gewohnheit).
- Transaktionen explizit, wo mehrere Schreibzugriffe zusammengehören.
- Schema-Migrationen idempotent.
- Bei Netz-IO: Timeouts setzen, Retry-Logik nur wo fachlich nötig.

## 8. Framework-/Stack-Spezifisches

Hier Besonderheiten des gewählten Stacks ergänzen — z.B. Qt-Signals/Slots, React-Hook-Regeln, async/await-Konventionen.

- *(Platzhalter — pro Projekt ausfüllen)*

## 9. Dateigröße & Modul-Grenzen

- Richtwert: ≤ 500 Zeilen pro Datei. Darüber: Aufteilung erwägen (aber CLAUDE.md Regel 2 beachten — Aufteilung muss echten Wert haben).
- Eine Datei = eine klar abgegrenzte Verantwortung (siehe `ARCHITEKTUR.md`).
- Keine Zyklen in Imports zwischen Modulen.

## 10. Was NICHT tun

- Keine spekulative Konfigurierbarkeit (CLAUDE.md Regel 2).
- Kein vorgezogenes Abstrahieren: erst wenn der zweite Call-Site existiert, Helper extrahieren.
- Keine Präfix-Kommentare-Blöcke wie `# === SECTION === #` — Code sollte durch Struktur sprechen.
- Keine `TODO:`-Kommentare ohne Kontext. Entweder mit Referenz auf `CODE_REVIEW_OFFEN_<BEREICH>.md` oder gar nicht.
- Keine Performance-Optimierungen ohne Messung.
