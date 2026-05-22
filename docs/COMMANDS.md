# Befehlsreferenz ({{PROJEKT_NAME}})

Verifizierte Shell-Befehle für dieses Projekt. Claude liest diese Datei in jeder Session.

**Zweck:** Reibungsverluste durch falsche Shell-Syntax (PowerShell vs. bash) und unbekannte Projekt-Befehle vermeiden. Wenn ein Befehl hier nicht steht oder fehlschlägt, erst fragen — nicht raten.

## Shell-Umgebung

| Plattform     | Shell                | Anmerkung                                                |
| ------------- | -------------------- | -------------------------------------------------------- |
| `{{PRIMARY}}` | `{{PRIMARY_SHELL}}`  | Standard-Shell für diese Vorlage                         |
| Fallback      | `bash` (Git-Bash/WSL) | Für POSIX-Skripte, wenn PowerShell-Idiom umständlich ist |

Anpassen, falls in diesem Projekt eine andere Plattform/Shell gilt.

---

## PowerShell-Stolperfallen

Häufige Fehler, wenn bash-Idiome unreflektiert auf PowerShell übertragen werden. Linke Spalte → falsch, rechte → korrekt.

### Variablen

| ⛔ bash-Stil           | ✅ PowerShell                  |
| ---------------------- | ------------------------------ |
| `$VAR`                 | `$env:VAR` (Env-Var lesen)     |
| `export VAR=value`     | `$env:VAR = "value"`           |
| `VAR=value command`    | Vorher `$env:VAR = "value"; …` |

### Umleitung & Null-Senken

| ⛔ bash-Stil           | ✅ PowerShell                                |
| ---------------------- | -------------------------------------------- |
| `command > /dev/null`  | `command > $null` oder `command \| Out-Null` |
| `command 2>&1`         | `command 2>&1` (identisch)                   |
| `command &`            | Background: `Start-Job { command }`          |

### Vergleichsoperatoren

| ⛔ bash/C-Stil  | ✅ PowerShell        |
| -------------- | -------------------- |
| `==`, `!=`     | `-eq`, `-ne`         |
| `<`, `>`       | `-lt`, `-gt`         |
| `<=`, `>=`     | `-le`, `-ge`         |
| `=~` (Regex)   | `-match`             |
| `-z`, `-n`     | `[string]::IsNullOrEmpty($x)` |

### Pfad & Datei

| ⛔ POSIX                  | ✅ PowerShell                |
| ------------------------ | ---------------------------- |
| `~/file`                 | `$HOME/file` oder `~\file`  |
| Pfad-Separator `/`       | `/` funktioniert, idiomatisch `\` |
| `which cmd`              | `Get-Command cmd`            |

### Zeilenfortsetzung

- ⛔ Backslash `\` am Zeilenende (bash) — wird in PowerShell als Literal interpretiert.
- ✅ Backtick `` ` `` am Zeilenende.

### Heredoc / Mehrzeilen-Strings an native Tools

- ⛔ `<<EOF … EOF` (bash) funktioniert nicht.
- ✅ Single-quoted Here-String, schließendes `'@` **muss in Spalte 0** stehen, sonst Parse-Fehler.

```powershell
git commit -m @'
Erste Zeile.
Zweite Zeile mit $literal-Dollarzeichen.
'@
```

### Destruktive Cmdlets fragen interaktiv

- `Remove-Item`, `Stop-Process`, `Clear-Content` fragen ggf. nach Bestätigung.
- Bei Skript-Nutzung: `-Confirm:$false` ergänzen. `-Force` für Read-only/Hidden-Items.

### Argumente mit `-` oder `@` an native Exes

- Stop-Parsing-Token verwenden, damit PowerShell die Folgeargumente nicht eigeninterpretiert:

```powershell
git log --% --format=%H
```

### Pipeline ist Objekt-basiert

- ⛔ `command | grep foo` — `grep` ist auf Windows oft nicht installiert.
- ✅ `command | Select-String foo` oder `command | Where-Object { $_ -match "foo" }`.

---

## Projektspezifische Befehle

Beim Kickoff füllen. Wenn ein Befehl nicht verifiziert ist: leer lassen, nicht raten.

### Installation & Setup

```powershell
{{INSTALL_BEFEHL}}
```

### Entwicklung starten

```powershell
{{START_BEFEHL}}
```

Läuft unter: `{{LOKALE_URL}}`

### Build (Produktion)

```powershell
{{BUILD_BEFEHL}}
```

### Tests

| Zweck               | Befehl                  |
| ------------------- | ----------------------- |
| Alle Tests          | `{{TEST_ALL_BEFEHL}}`   |
| Gezielter Testlauf  | `{{TEST_ONE_BEFEHL}}`   |
| Watch-Modus         | `{{TEST_WATCH_BEFEHL}}` |

### Lint & Format

| Zweck         | Befehl                  |
| ------------- | ----------------------- |
| Lint-Check    | `{{LINT_BEFEHL}}`       |
| Auto-Format   | `{{FORMAT_BEFEHL}}`     |
| Type-Check    | `{{TYPECHECK_BEFEHL}}`  |

### Aufräumen

| Zweck              | Befehl                |
| ------------------ | --------------------- |
| Build-Artefakte    | `{{CLEAN_BEFEHL}}`    |
| Dependencies neu   | `{{CLEAN_INSTALL}}`   |

---

## Verifiziert funktionierende Befehle

Hier landen Befehle, die im laufenden Betrieb erfolgreich getestet wurden. Eintragen, sobald ein neuer Befehl reproduzierbar klappt.

| Befehl | Was es tut | Zuletzt verifiziert |
| ------ | ---------- | ------------------- |
|        |            |                     |

---

## Bekannt nicht funktionierende Befehle

Befehle, die in diesem Projekt nicht klappen — inkl. Grund. Verhindert, dass Claude sie erneut versucht.

| Befehl | Symptom | Grund / Alternative |
| ------ | ------- | ------------------- |
|        |         |                     |
