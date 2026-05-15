# Roadmap Phase 1 – Minimal lauffähige Version

**Voraussetzung:** keine (Projektstart).

**Ziel:** {{PROJEKT_NAME}} in einen Zustand bringen, in dem der Haupt-Usecase funktioniert — auch wenn Features noch rau sind. Alles Weitere ist Phase 2.

**Milestone:** `v0.1.0` (Phasen-Milestone-Release, semver-Minor-Bump, nach Release-Code-Review). Keine Zwischen-Releases in Phase 1. Schema → [release/VERSIONIERUNG.md](../release/VERSIONIERUNG.md)

---

Features haben keine feste Reihenfolge.
**Feature-Blöcke** kennzeichnen Abhängigkeiten – zuerst das obere Feature, dann das untere.

---

## Bereich: UI / Frontend

Features die die Benutzeroberfläche betreffen.

### Feature: <Name>

Kurze Beschreibung, was das Feature liefert und warum es in Phase 1 muss.

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

## Hinweise zum Phase-1-Scope

- Alles, was nicht zwingend für die Lauffähigkeit gebraucht wird, gehört in [PHASE2.md](./PHASE2.md).
- „Intelligente" Erweiterungen (Online-Anreicherung, Polish, Sortierungen, Themes) → Phase 2.
- Ambitionierte Langfrist-Features (Mehrsprachigkeit, integrierter Reader, Release-Vorbereitung) → [PHASE3.md](./PHASE3.md).

## Allgemeine Bugfixes & Performance

Laufend, keine eigene Season nötig. Werden direkt behoben und im [CHANGELOG.md](../CHANGELOG.md) erfasst.
