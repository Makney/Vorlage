# {{PROJEKT_NAME}} — Architektur-Referenz

**Stand:** {{DATUM}}
**Status:** *(Architektur in Arbeit | Architektur abgeschlossen, MVP ready | …)*
**Name:** {{PROJEKT_NAME}} — *(optionale Etymologie / Bedeutung des Namens)*

---

## 1. Projekt-Identität

*(1–3 Absätze: Was ist die App, für wen, was ist das Alleinstellungsmerkmal?)*

- **Nutzungsmodell:** *(privat / Team / öffentlich)*
- **Aktuelle Projekte/Daten:** *(initiale Größenordnung — wie viele Nutzer / Items / Sessions)*
- **Plattform:** *(Windows 11 / macOS / Linux / Cross-Plattform)*
- **Lebenszyklus:** *(Daily-Driver / gelegentliche Nutzung / einmalige Auswertung)*

### Naming-Konventionen

| Kontext | Schreibweise |
|---|---|
| GitHub Repo | `{{PROJEKT_NAME}}` |
| App-Name in UI | `{{PROJEKT_NAME}}` |
| `package.json` `name` | *(kebab-case, z.B. `projekt-name`)* |
| AppData-Ordner | `{{PROJEKT_NAME}}` |
| App-Bundle-ID (optional) | *(z.B. `de.makney.projektname`)* |

---

## 2. Technischer Stack (final)

| Komponente | Wahl | Hinweise |
|---|---|---|
| Runtime | *(z.B. Electron + TypeScript / Python 3 + PySide6)* | *(Strict-Mode? Version-Pin?)* |
| UI | *(z.B. React 18 + Zustand)* | *(Anzahl Stores, State-Strategie)* |
| Storage | *(z.B. better-sqlite3 / SQLAlchemy)* | *(WAL? Migrations-Strategie?)* |
| *(weitere Bausteine)* | | |
| Build | *(z.B. Electron Forge + Vite / PyInstaller)* | |

**Bewusste Auslassungen:**

- *(Hier explizit auflisten, was NICHT gewählt wurde und warum — z.B. „kein Monaco-Editor weil CodeMirror reicht")*

---

## 3. Prozess-Architektur

*(Welche Prozesse / Threads / Module gibt es, wie kommunizieren sie?)*

- **Haupt-Prozess:** *(Verantwortlichkeit, Abhängigkeiten)*
- **Worker / Hintergrund-Prozess:** *(falls vorhanden)*
- **IPC / RPC / API-Boundary:** *(typed Channels? REST? gRPC? Result-Types?)*

*(Optional: ASCII-Diagramm der Prozess-Topologie)*

---

## 4. Persistenz

*(Schema / Tabellen / Dateiformate)*

- **Speicherort:** *(`%APPDATA%\{{PROJEKT_NAME}}\` / `~/.config/{{PROJEKT_NAME}}/` / …)*
- **Schema-Versionierung:** *(Migrations-Strategie)*
- **Backup-/Export-Strategie:** *(falls relevant)*

### Tabellen / Entitäten

*(Für jede Tabelle: Spalten, Indizes, Fremdschlüssel, kurze Begründung)*

---

## 5. CLAUDE.md-Konvention

*(Falls eine projekt-spezifische Anpassung gegenüber der Vorlage erfolgt — z.B. zusätzliche Frontmatter-Felder, eigene Trigger-Phrasen, abweichende Working Rules. Sonst: „Keine Abweichungen.")*

---

## 6. Komponenten-Architektur

*(UI-Hierarchie / Modul-Aufteilung / Service-Schichten)*

- **Shell:** *(Haupt-Layout, Navigation)*
- **Domänen-Module:** *(je Bounded Context ein Eintrag)*
- **Shared / Utilities:** *(was wird querschnittlich genutzt?)*

---

## 7. App-Lifecycle

*(Start → Hauptbetrieb → Shutdown — was passiert wann?)*

- **Cold Start:** *(Schritte und Dauer-Erwartung)*
- **Reguläre Nutzung:** *(typische Event-Loops, Watchdogs)*
- **Shutdown:** *(Daten persistieren, Locks freigeben)*

---

## 8. Phasen-Plan

Siehe [roadmap/ROADMAP.md](./roadmap/ROADMAP.md) für die Phasen-Übersicht. Hier nur die Architektur-relevanten Eckpunkte:

- **Phase 1 (MVP):** *(welche Architektur-Bausteine MÜSSEN stehen?)*
- **Phase 2:** *(welche Erweiterungen sind vorgesehen?)*
- **Phase 3:** *(welche Langfrist-Themen sind explizit *möglich*, aber nicht geplant?)*

---

## 9. Build-Reihenfolge (Sprints)

*(Empfohlene Reihenfolge, in der die Architektur-Bausteine gebaut werden — wichtig für Phase 1.)*

1. **Sprint 1:** *(Fundament — z.B. „App-Skelett + IPC + DB-Stub")*
2. **Sprint 2:** *(erste echte Domäne)*
3. *…*

---

## 10. Schlüssel-Designprinzipien

*(3–7 Sätze, die das Projekt-Ethos zusammenfassen. Beispiele:)*

- *„Lokal first — keine Cloud-Abhängigkeit, keine Telemetrie."*
- *„Typed Boundaries — IPC, DB, externe APIs sind typisiert."*
- *„Konfiguration ist Code — keine Runtime-Settings, die nicht im Quellcode auffindbar sind."*

---

## 11. Identifizierte Reibungen

*(Bekannte Schwachstellen / Friktion in der gewählten Architektur, die akzeptiert wurden. Verweist ggf. auf `TECH_SCHULDEN.md`.)*

---

## 12. Was bewusst NICHT gebaut wird

*(Negative-Scope-Liste auf Architektur-Ebene — vgl. mit Roadmap-Negative-Liste.)*

---

## 13. Offene Fragen

*(Punkte, die vor dem ersten Implementations-Sprint noch geklärt werden müssen. Diese Sektion sollte schrumpfen, je weiter die Architektur reift.)*
