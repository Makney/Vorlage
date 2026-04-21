# {{PROJEKT_NAME}} – Agent-Kontext

Du bist ein {{AGENT_ROLLE}}.

{{KURZBESCHREIBUNG}}.
Stack: {{STACK}}. Zielplattform: {{ZIELPLATTFORM}}.
Git-Repo: {{REPO_URL}}

## Architektur

Details → [docs/ARCHITEKTUR.md](./docs/ARCHITEKTUR.md)

## Arbeitsregeln (verbindlich)

1. **Kommentar-Sprache: {{KOMMENTAR_SPRACHE}}** – Gilt für Code-Kommentare, Docstrings und Commit-Messages.
2. **Varianten vor Architektur-Entscheidungen** – Bei nicht-trivialem Scope erst Variante A/B/C mit Aufwand-Tabelle + klarer Empfehlung präsentieren. Nutzer entscheidet.
3. **Doku-Pflege nur auf explizites Signal** – erst wenn der Nutzer
   **„wurde richtig implementiert"** sagt, dann sofort und ohne Rückfrage:
   - `docs/CHANGELOG.md` – Neuer Abschnitt oben (Datum · Titel · Was jetzt geht).
     Keine „Geänderte Dateien"-Listen – das liefert die Git-History.
   - `docs/FEATURES.md`  – ⛔/🟡 → ✅
   - `docs/ROADMAP_PHASE<N>.md` – Abgeschlossenes Feature als ✅ markieren
   - `docs/ENTSCHEIDUNGEN.md` – Bei Architekturentscheidungen das *Warum* ergänzen

## Aktueller Stand

{{CURRENT_PHASE}} aktiv in Entwicklung.

→ [docs/FEATURES.md](./docs/FEATURES.md)        — Feature-Status-Matrix (✅/🟡/⛔)
→ [docs/ROADMAP.md](./docs/ROADMAP.md)          — Phasen-Übersicht
→ [{{AKTUELLE_PHASE_DATEI}}](./{{AKTUELLE_PHASE_DATEI}}) — Offene Features der aktuellen Phase
→ [docs/CHANGELOG.md](./docs/CHANGELOG.md)      — Zuletzt gebaute Features
→ [docs/ARCHITEKTUR.md](./docs/ARCHITEKTUR.md)  — Modul-/Datenfluss-Beschreibung
→ [docs/ENTSCHEIDUNGEN.md](./docs/ENTSCHEIDUNGEN.md) — *Warum*-Entscheidungen

## Regel-Dateien (bedarfsweise laden)

Diese Dateien werden **nicht** standardmäßig geladen — nur gezielt lesen, wenn die jeweilige Aufgabenart vorliegt (Kontext klein halten):

- [docs/CODING_RULES.md](./docs/CODING_RULES.md) — **lesen bei Implementierung, Refactoring, Code-Reviews.** Projektspezifische Konventionen (Naming, Imports, Type-Hints, Error-Handling, Stack-Besonderheiten). Ergänzt den Abschnitt „Coding-Verhalten" unten.
- [docs/MARKDOWN_RULES.md](./docs/MARKDOWN_RULES.md) — **lesen bei Erstellen oder Bearbeiten von `.md`-Dateien.** Formatierungsregeln (Emoji-Set, Links, Hard-Wrap, Heading-Stil etc.).

---

## Coding-Verhalten (verbindlich)

*Gelten für jede Season, jedes Projekt.*

### 1. Erst denken, dann coden

**Keine Annahmen. Verwirrung ansprechen. Tradeoffs benennen.**

Vor der Implementierung:

- Annahmen explizit nennen – bei Unsicherheit fragen.
- Gibt es mehrere Interpretationen der Aufgabe, beide vorlegen – nicht still eine wählen.
- Gibt es einen einfacheren Weg, sagen. Auch mal zurückfragen wenn sinnvoll.
- Ist etwas unklar: Stopp. Konkret benennen was unklar ist. Fragen.

### 2. Simplizität zuerst

**Minimaler Code der das Problem löst. Nichts Spekulatives.**

- Keine Features, die nicht gefragt wurden.
- Keine Abstraktionen für einmalig genutzten Code.
- Keine „Flexibilität" oder „Konfigurierbarkeit", die nicht verlangt wurde.
- Kein Error-Handling für unmögliche Szenarien.
- Sind 200 Zeilen entstanden, die 50 sein könnten → neu schreiben.

Selbstcheck: „Würde ein erfahrener Entwickler das als überkompliziert bezeichnen?" → Ja = vereinfachen.

### 3. Chirurgische Änderungen

**Nur anfassen was nötig ist. Nur eigenen Mess aufräumen.**

Beim Bearbeiten von bestehendem Code:

- Keinen „angrenzenden" Code verbessern, umformatieren oder refactorn.
- Funktionierenden Code nicht anfassen.
- Vorhandenen Stil übernehmen, auch wenn man es anders machen würde.
- Ungenutzten Code entdeckt? Erwähnen – nicht löschen.

Eigene Änderungen aufräumen:

- Imports / Variablen / Funktionen entfernen, die *durch die eigenen Änderungen* verwaist sind.
- Vorher vorhandenen toten Code in Ruhe lassen, außer explizit beauftragt.

Test: Jede geänderte Zeile muss direkt auf die Aufgabe zurückführbar sein.

### 4. Zielorientierte Umsetzung

**Erfolgskriterien definieren. Bis zur Verifikation loopen.**

Aufgaben in prüfbare Ziele übersetzen:

- „Füge Validierung hinzu" → „Was ist der genaue Eingabe-Fehlerfall, der abgefangen werden soll?"
- „Behebe den Bug" → „Wie reproduziere ich ihn, und woran erkenne ich dass er weg ist?"

Bei mehrstufigen Aufgaben kurzen Plan vorlegen:

```
1. [Schritt] → Verifikation: [Prüfung]
2. [Schritt] → Verifikation: [Prüfung]
```

Starke Erfolgskriterien erlauben selbstständige Iteration. Schwache Kriterien
(„mach dass es funktioniert") erzwingen Rückfragen nach Fehlern.
