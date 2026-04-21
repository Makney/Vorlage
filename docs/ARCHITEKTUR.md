# Architektur

Diese Datei beschreibt den **statischen Aufbau** des Projekts: welche Module existieren, wie sie zusammenhängen, wo Daten liegen. Abgrenzung zu anderen Dokus:

- **CLAUDE.md** → Projekt-Steckbrief (1 Absatz), hier ist der Verweis dahin
- **ENTSCHEIDUNGEN.md** → *warum* die Struktur so ist (nicht hier)
- **FEATURES.md / ROADMAP.md** → was davon existiert / wird gebaut (nicht hier)

## Ordnerstruktur

```
{{PROJEKT_NAME}}/
├── <einstiegspunkt>            # z.B. main.py / index.ts / cmd/<name>/main.go
├── <dependency-manifest>       # requirements.txt / package.json / Cargo.toml …
├── <laufzeit-artefakte>        # DB-Datei, Caches — ausgeschlossen über .gitignore
├── .gitignore
│
├── <layer-1>/                  # z.B. database · core · backend
│   ├── <modul>.ext
│   └── …
│
├── <layer-2>/                  # z.B. core · domain · service
│   └── …
│
├── <layer-3>/                  # z.B. ui · frontend · api
│   └── …
│
└── docs/                       # Du bist hier
```

Die Schichten sind bewusst getrennt: *oben* importiert aus *unten*, nie umgekehrt. Das hält Geschäftslogik frei von UI-/Framework-Abhängigkeiten und macht spätere Austausche (anderer UI-Stack, anderer Server) handhabbar.

## Datenfluss beim Start

```
<Einstiegspunkt>
  ├─ <schritt 1 — z.B. DB-Init>
  ├─ <schritt 2 — z.B. Config laden>
  └─ <schritt 3 — z.B. Hauptfenster / Server starten>
       └─ <was auf Ebene 3 passiert>
```

## Datenfluss für <Haupt-Usecase>

Beispiel-Platzhalter — für jeden wichtigen Ablauf (Import / Anfrage / Render-Zyklus …) eine eigene Sequenz dokumentieren:

```
<Auslöser>
  → <Aktion in Layer 1>
  → <Aktion in Layer 2>
  → <Ergebnis zurück in Layer 3>
```

## Datenmodell

Wenn das Projekt eine Persistenzschicht hat: Tabellen / Collections / Schemas mit ihrer Beziehung hier knapp dokumentieren.

### Tabelle / Collection `<name>`

| Feld      | Typ | Bedeutung |
| --------- | --- | --------- |
| id        |     |           |
| …         |     |           |

Beziehungen: `<tabelle_a> (1) ─── (n) <tabelle_b>`.

Was ist **Cache** (wird aus Quelldaten berechnet) vs. **primär** (muss gepflegt werden) — hier sauber markieren, sonst wird es beim ersten „Feld manuell gesetzt, nicht mitgezogen"-Bug schmerzhaft.

## Wichtige Konstrukte / Muster

Hier projektspezifische Patterns dokumentieren, die mehrfach auftauchen und beim Querlesen sonst Stirnrunzeln produzieren. Typische Beispiele:

- **Signal-/Event-Richtung** — wie kommunizieren Komponenten nach außen?
- **Thread-/Async-Modell** — wer darf UI anfassen, wer nicht?
- **Styling-/Theming-Strategie** — zentrale Datei oder Komponenten-lokal?
- **Konfigurations-Lookup** — woher kommen Werte (ENV, Settings-Store, Config-Datei)?

## Konfiguration / Persistenz

| Was                | Wo                                                 |
| ------------------ | -------------------------------------------------- |
| Nutzer-Einstellungen | `<Store>` — z.B. QSettings, OS-Keychain, config.toml |
| Projekt-Daten      | `<Datei/DB>` — z.B. `{{PROJEKT_NAME}}.db`          |
| Generierte Assets  | `<Ordner>` — z.B. `assets/covers/`                 |
| Secrets            | **nie im Repo** — z.B. `.env` (ignoriert)          |

## Versionierung

- Git-Remote: {{REPO_URL}}
- `.gitignore` schließt Laufzeit-Artefakte aus (siehe Datei).
