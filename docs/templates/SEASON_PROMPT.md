---
variables:
  PROJEKT_NAME:            { auto: project.name }
  NEXT_SEASON_NR:          { auto: project.next_season_number }
  CURRENT_PHASE_FILE:      { auto: claude_md.workbench.current_phase_file }
  DATUM:                   { auto: today }
  LETZTE_SEASON_NAME:      { auto: db.last_completed_feature_session }
  TECH_SCHULDEN_RELEVANT:  { auto: docs.tech_schulden_top_n }
  LETZTE_ENTSCHEIDUNGEN:   { auto: docs.entscheidungen_top_n }
  FEATURE_NAME:            { input: text,     label: "Feature",            required: true }
  AUFGABE:                 { input: textarea, label: "Aufgabe",            required: true }
  HINWEISE:                { input: textarea, label: "Hinweise (optional)" }
---

# Season-Prompt-Template

Dieses Template wird beim Erstellen einer neuen Season-Session verwendet. TakumiDeck (App) liest es, befüllt die `{{...}}`-Variablen automatisch + via Formular und sendet das Ergebnis ans aktive PTY via Bracketed Paste.

**Auto-Variablen** (von TakumiDeck befüllt):

- `{{PROJEKT_NAME}}` — aus CLAUDE.md (`workbench.project_name`)
- `{{NEXT_SEASON_NR}}` — aus SQLite (next_season_number)
- `{{CURRENT_PHASE_FILE}}` — aus CLAUDE.md (`workbench.current_phase_file`)
- `{{DATUM}}` — heute (`YYYY-MM-DD`)

**Optionale Auto-Variablen** (opt-in pro Template):

- `{{LETZTE_SEASON_NAME}}` — letzte completed Feature-Session
- `{{TECH_SCHULDEN_RELEVANT}}` — Top-3 offene Einträge aus `docs/TECH_SCHULDEN.md`
- `{{LETZTE_ENTSCHEIDUNGEN}}` — Top-3 aus `docs/ENTSCHEIDUNGEN.md`

**User-Variablen** (im Formular einzugeben):

- `{{FEATURE_NAME}}` — Pflicht
- `{{AUFGABE}}` — Pflicht
- `{{HINWEISE}}` — Optional

---

## Vorlage (Inhalt)

```text
Season {{NEXT_SEASON_NR}}: {{FEATURE_NAME}}
Einstieg: Diese Dateien zuerst lesen

docs/CHANGELOG.md              — Was wurde zuletzt gebaut? (oberster Eintrag reicht)
docs/FEATURES.md               — Aktueller Feature-Status
{{CURRENT_PHASE_FILE}}         — Offene Features der aktuellen Phase
/memory prüfen                 — Veraltete Auto-Memory-Einträge können CLAUDE.md-Regeln überschreiben

Deine Aufgabe
{{AUFGABE}}

Hinweise für diese Season (optional)
{{HINWEISE}}
```

---

## Welche Roadmap-Datei ist die richtige?

`{{CURRENT_PHASE_FILE}}` wird automatisch aus der CLAUDE.md gelesen. Falls manuell zu setzen:

| Aufgabe gehört zu                 | Datei                              |
| --------------------------------- | ---------------------------------- |
| MVP / Lauffähigkeit               | `docs/roadmap/PHASE1.md`           |
| Komfort / v1.0                    | `docs/roadmap/PHASE2.md`           |
| Power-Features / langfristig      | `docs/roadmap/PHASE3.md`           |
| Unklar / übergreifend             | `docs/roadmap/ROADMAP.md` (Übersicht) |

---

## Warum so kurz?

`CLAUDE.md` wird automatisch geladen und enthält bereits:

- Projekt-Steckbrief + Verweis auf Architektur-Doku
- Alle Working Rules (inkl. Trigger-Phrasen)
- Coding-Prinzipien und Doku-Update-Regeln

Das Template kommuniziert nur noch das **Was** (Aufgabe) und das **Wann nicht** (Scope-Abgrenzung via Hinweise). Alles andere ist bereits im Kontext.

## Was gehört in „Hinweise" und was nicht?

**Gehört rein:**

- Vorab-Entscheidungen (z.B. „keine neue Abhängigkeit hinzufügen")
- Scope-Abgrenzung zu nahen Features („Feature X ist NICHT Teil dieser Season")
- Bekannte Fallstricke aus ähnlichen Seasons
- Empfohlene Lese-Reihenfolge bei verschachtelten Features

**Gehört NICHT rein:**

- Architektur-Wiederholung (steht in `ARCHITEKTUR.md` / `{{PROJEKT_NAME}}_ARCHITEKTUR.md`)
- Regel-Wiederholung (steht in `CLAUDE.md` + `CODING_RULES.md`)
- Detaillierte Umsetzungs-Schritte (erzwingt Tunnelblick; lieber Ziele beschreiben und dem Agenten die Wahl lassen)
