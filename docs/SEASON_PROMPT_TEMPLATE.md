# Season-Prompt-Template

Dieses Template an den Anfang jedes neuen Season-Prompts kopieren und ausfüllen. [CLAUDE.md](../CLAUDE.md) wird vom Agenten automatisch geladen – Architektur, Regeln und Coding-Prinzipien müssen hier **nicht** wiederholt werden.

---

## Vorlage (kopieren, Platzhalter ersetzen)

```
# Season [NUMMER]: [FEATURE-NAME]

## Einstieg: Diese Dateien zuerst lesen
1. `docs/CHANGELOG.md`       — Was wurde zuletzt gebaut? (oberster Eintrag reicht)
2. `docs/FEATURES.md`        — Aktueller Feature-Status
3. `docs/ROADMAP_PHASE<N>.md` — Offene Features der aktuellen Phase

## Deine Aufgabe
[HIER: Konkrete Beschreibung was in dieser Season implementiert werden soll]

## Hinweise für diese Season (optional)
[HIER: Spezifische Constraints, bekannte Fallstricke, Vorab-Entscheidungen]
```

---

## Welche Roadmap-Datei angeben?

| Aufgabe gehört zu     | Datei                              |
| --------------------- | ---------------------------------- |
| Minimal-Lauffähigkeit | `docs/ROADMAP_PHASE1.md`           |
| Intelligente Erweiterungen / v1.0 | `docs/ROADMAP_PHASE2.md`   |
| Langfristige Features | `docs/ROADMAP_PHASE3.md`           |
| Unklar / übergreifend | `docs/ROADMAP.md` (Übersicht)      |

---

## Warum so kurz?

`CLAUDE.md` wird automatisch geladen und enthält bereits:

- Projekt-Steckbrief + Verweis auf Architektur-Doku
- Alle Arbeitsregeln
- Coding-Prinzipien (erst denken, Simplizität, chirurgische Änderungen, Zielorientierung)

Das Template kommuniziert nur noch das **Was** (Aufgabe) und das **Wann nicht** (Scope-Abgrenzung via Hinweise). Alles andere ist bereits im Kontext.

## Was gehört in „Hinweise" und was nicht?

**Gehört rein:**

- Vorab-Entscheidungen (z.B. „keine neue Abhängigkeit hinzufügen").
- Scope-Abgrenzung zu nahen Features („Feature X ist NICHT Teil dieser Season").
- Bekannte Fallstricke aus ähnlichen Seasons („Re-Scan-Regressionen sind leise und teuer").

**Gehört NICHT rein:**

- Architektur-Wiederholung (steht in `ARCHITEKTUR.md`).
- Regel-Wiederholung (steht in `CLAUDE.md` + `CODING_RULES.md`).
- Detaillierte Umsetzungs-Schritte (erzwingt einen Tunnelblick; lieber Ziele beschreiben und dem Agenten die Wahl lassen).
