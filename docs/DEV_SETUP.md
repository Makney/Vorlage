# Entwicklungsumgebung

Schritt-für-Schritt-Anleitung für eine frische Entwicklungsumgebung. Ziel: von Null auf laufendes Projekt in möglichst wenigen Schritten.

## Voraussetzungen

| Tool         | Mindestversion | Hinweis                  |
| ------------ | -------------- | ------------------------ |
| `{{TOOL_1}}` | `{{VERSION}}`  | {{INSTALLATIONSHINWEIS}} |
| `{{TOOL_2}}` | `{{VERSION}}`  | {{INSTALLATIONSHINWEIS}} |

## Einrichtung

### 1. Repository klonen

```bash
git clone {{REPO_URL}}
cd {{PROJEKT_NAME}}
```

### 2. Abhängigkeiten installieren

```bash
{{INSTALL_BEFEHL}}
```

### 3. Umgebungsvariablen setzen

`.env.example` nach `.env` kopieren und Werte eintragen:

```bash
cp .env.example .env
```

| Variable    | Pflicht | Beschreibung     |
| ----------- | ------- | ---------------- |
| `{{VAR_1}}` | ja      | {{BESCHREIBUNG}} |
| `{{VAR_2}}` | nein    | {{BESCHREIBUNG}} |

### 4. Projekt starten

```bash
{{START_BEFEHL}}
```

Läuft unter: `{{LOKALE_URL}}`

---

## Häufige Probleme

### {{PROBLEM_TITEL}}

**Symptom:** Was sieht man, wenn das Problem auftritt?

**Ursache:** Warum passiert das?

**Lösung:** Konkrete Befehle oder Schritte zum Beheben.
