# Roadmap Phase 2 – Intelligente Erweiterungen

**Voraussetzung:** Phase 1 abgeschlossen (v0.1 stabil).

**Ziel:** Aus der funktionsfähigen Basis eine ausgereifte Anwendung machen. Externe Dienste anbinden, UI verfeinern, Programm für den täglichen Einsatz komfortabler gestalten.

**Milestone:** `v1.0.0` (Phasen-Milestone-Release, semver-Major-Bump, nach Release-Code-Review). Zwischen-Releases während Phase 2: `v0.1.1`, `v0.1.2`, … — jeweils gezielter Release-Review der Datei-Diffs gegenüber der vorherigen Version. Schema → [release/VERSIONIERUNG.md](../release/VERSIONIERUNG.md)

---

Features haben keine feste Reihenfolge.
**Feature-Blöcke** kennzeichnen Abhängigkeiten – zuerst das obere Feature, dann das untere.

---

## Bereich: UI / Frontend

Features die die Benutzeroberfläche betreffen.

### Feature: <Name>

Kurze Beschreibung.

- *(konkreter Bulletpoint)*

---

## Bereich: Core / Geschäftslogik

Features die die Kernlogik betreffen.

### Feature: <Name>

Kurze Beschreibung.

- *(konkreter Bulletpoint)*

---

## Bereich: Datenbank / Persistenz

Features die Datenspeicherung und -zugriff betreffen.

### Feature: <Name>

Kurze Beschreibung.

- *(konkreter Bulletpoint)*

---

## Bereich: API / Integration

Features die externe Schnittstellen oder Dienste betreffen.

### Feature: <Name>

Kurze Beschreibung.

- *(konkreter Bulletpoint)*

---

## Feature-Block: <Name>

> ⚠️ Diese Features bauen aufeinander auf. Erst Feature 1 umsetzen, dann Feature 2.

### Feature 1: <Name>

- *(konkret)*

### Feature 2: <Name>

**Voraussetzung:** Feature 1

- *(konkret)*

---

## Allgemeine Bugfixes & Performance

Laufend, keine eigene Season nötig. Werden direkt behoben und im [CHANGELOG.md](../CHANGELOG.md) erfasst.
