---
# Kickoff-Template hat KEINE Auto- oder Input-Variablen aus TakumiDeck-Sicht.
# Alle {{...}}-Tokens im Body (KURZBESCHREIBUNG, STACK, AGENT_ROLLE, TRIGGER_*, …)
# sind Agent-Anweisungen — der Agent extrahiert die Werte aus dem Brainstorm-
# Input und ersetzt sie zur Laufzeit selbst. TakumiDeck laesst alle Tokens
# literal stehen (leeres `variables:`-Map = kein Token ist Renderer-bekannt).
variables: {}
---

# Projekt-Kickoff-Template

Dieses Template startet einen **Kickoff-Lauf**: aus dem rohen Klon dieser Vorlage und einem Kickoff-Prompt (Ergebnis einer langen Brainstorm-Season in einer anderen Session/Tool) entsteht ein arbeitsbereites Projekt.

**Konzept:** Der Agent, der diesen Prompt empfängt, ist Orchestrator. Er liest den Kickoff-Prompt des Users, extrahiert alle Entscheidungen daraus, ersetzt Platzhalter in der Vorlage, benennt eine Datei um, füllt die Architektur- und Phasen-Skelette mit den Brainstorm-Inhalten — alles **ohne Code zu schreiben**. Erstes Coding passiert erst in der ersten regulären Season (siehe [SEASON_PROMPT.md](./SEASON_PROMPT.md)).

**Voraussetzung:** Der User hat in einer separaten Brainstorm-Session einen **Kickoff-Prompt** erzeugt, der mindestens diese Bausteine enthält:

- Projektname, Kurzbeschreibung, Stack, Zielplattform, Repo-URL
- Agent-Rolle / Seniorität, Kommentar-Sprache
- Architektur-Grundgerüst (Persistenz, Prozesse, Module, App-Lifecycle, Designprinzipien, bewusste Auslassungen)
- Phasen-Plan (welche Phasen existieren, welche Features pro Phase, was bewusst NICHT gebaut wird)
- Trigger-Phrasen (für Doku-Update, Commit, Release-Gates) — falls vorhanden, sonst Defaults vorschlagen
- Default-Claude-Modell — falls vorhanden, sonst Default vorschlagen

Fehlt einer dieser Bausteine: **vor Beginn der Phasen unten nachfragen**, nicht raten.

---

## Vorlage (Inhalt)

```text
Projekt-Kickoff — Vorlage → arbeitsbereites Projekt

Du bist der Orchestrator. Du schreibst KEINEN Code in diesem Lauf.
Du übersetzt einen Brainstorm-Output in die Datei-Struktur der Vorlage:
Tokens ersetzen, eine Datei umbenennen, Architektur- und Phasen-Skelette
mit den Brainstorm-Inhalten füllen, Doku-Index säubern. Fertig.

Brainstorm-Input (vom User unten geliefert)
<<<
{HIER FÜGT DER USER DEN KICKOFF-PROMPT AUS DER BRAINSTORM-SESSION EIN>>>
>>>

Pflicht-Lektüre vor dem Start
- README.md                       (Vorlage-Überblick, Platzhalter-Tabelle)
- CLAUDE.md                       (YAML-Frontmatter + Working Rules — beides muss konsistent gefüllt werden)
- docs/README.md                  (Doku-Index — Pflegerhythmus, wer schreibt was)
- docs/MARKDOWN_RULES.md          (gilt für jede .md-Bearbeitung in diesem Lauf)
- docs/COMMANDS.md                (Skelett — Befehlsreferenz, wird in Phase 2 mit projektspezifischen Befehlen gefüllt)
- docs/{{PROJEKT_NAME}}_ARCHITEKTUR.md (Skelett, das gefüllt wird)
- docs/roadmap/ROADMAP.md         (Phasen-Übersicht — Skelett, das gefüllt wird)
- docs/roadmap/PHASE1.md          (Skelett — Skelette aller existierenden Phase-Dateien lesen, bevor du etwas schreibst)

Ablauf, dem du folgst

Phase 1 — Inputs extrahieren und Lücken melden
1. Lies den Brainstorm-Input zwischen <<< und >>> komplett.
2. Extrahiere die folgenden Werte (Pflicht). Wenn ein Wert fehlt: STOPP, frag mich,
   raten ist verboten:
   - PROJEKT_NAME (z.B. "TakumiDeck")
   - KURZBESCHREIBUNG (ein Satz)
   - STACK (kompakt, z.B. "TypeScript · Electron · React · SQLite")
   - ZIELPLATTFORM (z.B. "Windows 11")
   - REPO_URL (Git-Remote-URL)
   - AGENT_ROLLE (z.B. "Senior TypeScript Developer mit Schwerpunkt Electron")
   - KOMMENTAR_SPRACHE (z.B. "Deutsch")
   - CURRENT_PHASE (z.B. "Phase 1 (MVP)")
   - DEFAULT_MODEL (Claude-Modell-ID, z.B. "claude-sonnet-4-6")
3. Extrahiere die Trigger-Phrasen. Wenn der Brainstorm keine vorgibt: schlag
   diese Defaults vor und frag um Bestätigung:
   - DOCS_TRIGGER = "ist korrekt umgesetzt"
   - COMMIT_TRIGGER = "commit"
   - RELEASE_TRIGGER = "release vorbereiten"
   - FIX_TRIGGER = "fix it"
   - RELEASE_ARTIFACTS_TRIGGER = "release artefakte"
   - TAG_PUSH_TRIGGER = "tag und push"
4. Leite aus dem Stack die typischen Projekt-Befehle ab und schlag sie als
   Default-Tabelle vor (Beispiele: Node-npm → "npm install / npm run dev /
   npm run build / npm test / npm run lint"; Python-Poetry → "poetry install /
   poetry run <skript> / pytest / ruff check"; Cargo → "cargo build /
   cargo run / cargo test / cargo clippy"). Wenn der Brainstorm bereits
   konkrete Befehle nennt: die übernehmen. Werte, die mit Stack-Wissen nicht
   eindeutig ableitbar sind: in der Bestätigungs-Tabelle als "*(noch offen)*"
   markieren — nicht raten. Erwartete Tokens:
   - PRIMARY (Entwicklungsplattform, z.B. "Windows 11")
   - PRIMARY_SHELL (Default-Shell, z.B. "PowerShell 7+")
   - INSTALL_BEFEHL, START_BEFEHL, LOKALE_URL
   - BUILD_BEFEHL
   - TEST_ALL_BEFEHL, TEST_ONE_BEFEHL, TEST_WATCH_BEFEHL
   - LINT_BEFEHL, FORMAT_BEFEHL, TYPECHECK_BEFEHL
   - CLEAN_BEFEHL, CLEAN_INSTALL
5. Extrahiere die Architektur-Bausteine (Stack-Detail, Prozesse, Persistenz,
   Module, Lifecycle, Designprinzipien, bewusste Auslassungen, offene Fragen).
   Halte sie kurz strukturiert fest — die landen in Phase 4.
6. Extrahiere den Phasen-Plan (Phase 1/2/3 — welche Features pro Phase, welche
   sind bewusst nicht im Scope). Falls eine Phase nicht gebraucht wird:
   merken, sie wird in Phase 5 gelöscht.
7. Berichte mir das extrahierte Wertepaket als Tabelle/Liste. Frag um Bestätigung,
   BEVOR du etwas schreibst.

Phase 2 — Tokens global ersetzen (nach meinem OK)
8. Ersetze die Tokens in allen .md-Dateien des Repos. Liste der Tokens und ihrer
   Zielwerte siehst du in der Tabelle aus Phase 1 sowie in README.md
   ("Platzhalter-Liste"):
   - {{PROJEKT_NAME}} → <Wert>
   - {{KURZBESCHREIBUNG}} → <Wert>
   - {{STACK}} → <Wert>
   - {{ZIELPLATTFORM}} → <Wert>
   - {{REPO_URL}} → <Wert>
   - {{AGENT_ROLLE}} → <Wert>
   - {{KOMMENTAR_SPRACHE}} → <Wert>
   - {{CURRENT_PHASE}} → <Wert>
   - {{DEFAULT_MODEL}} → <Wert>
   - {{DOCS_TRIGGER}}, {{COMMIT_TRIGGER}}, {{RELEASE_TRIGGER}},
     {{FIX_TRIGGER}}, {{RELEASE_ARTIFACTS_TRIGGER}}, {{TAG_PUSH_TRIGGER}} → <Werte>
   - {{PRIMARY}}, {{PRIMARY_SHELL}} → <Werte aus Phase 1, Punkt 4>
   - {{INSTALL_BEFEHL}}, {{START_BEFEHL}}, {{LOKALE_URL}}, {{BUILD_BEFEHL}},
     {{TEST_ALL_BEFEHL}}, {{TEST_ONE_BEFEHL}}, {{TEST_WATCH_BEFEHL}},
     {{LINT_BEFEHL}}, {{FORMAT_BEFEHL}}, {{TYPECHECK_BEFEHL}},
     {{CLEAN_BEFEHL}}, {{CLEAN_INSTALL}} → <Werte aus Phase 1, Punkt 4>
   - {{DATUM}} → heute (YYYY-MM-DD), nur im Architektur-Skelett
   {{CURRENT_VERSION}} bleibt vorerst "0.0.0-dev" in CLAUDE.md frontmatter — wird
   vom Release-Flow gepflegt, nicht hier.
   Hinweis: docs/COMMANDS.md und docs/DEV_SETUP.md teilen sich die Befehls-Tokens
   ({{INSTALL_BEFEHL}}, {{START_BEFEHL}}, {{LOKALE_URL}}) — derselbe Wert füllt
   beide Dateien.
9. Sonderfall TEMPLATE-Tokens NICHT ersetzen: in den Template-Dateien
   (docs/templates/*.md inkl. dieser Datei) sind {{...}}-Tokens dokumentierter
   Bestandteil der Vorlage (TakumiDeck befüllt sie zur Laufzeit). Diese Dateien
   bleiben unverändert. Ausnahme: docs/templates/SEASON_PROMPT.md,
   BUG_REPORT.md, CODE_REVIEW_START.md, RELEASE_START.md sind reine Templates
   und kommen nicht in den globalen Replace.
10. Sonderfall .claude/rules/*.md — bleibt unverändert (sind Auto-Inject-Regeln,
    keine projekt-spezifischen Inhalte).
11. Liste mir nach dem Replace auf: welche Dateien wurden angefasst, wie viele
    Treffer pro Datei.

Phase 3 — Architektur-Datei umbenennen
12. Benenne die Datei docs/{{PROJEKT_NAME}}_ARCHITEKTUR.md so um, dass der Token
    im Dateinamen durch den realen Projektnamen ersetzt ist (z.B.
    docs/TakumiDeck_ARCHITEKTUR.md).
13. Prüfe alle .md-Dateien auf Verweise auf den alten Dateinamen und korrigiere
    sie. Typische Stellen: CLAUDE.md (frontmatter on_demand_files + Current-Status-
    Block), docs/README.md (Orientierungs-Reihenfolge), README.md.

Phase 4 — Architektur-Skelett befüllen
14. Fülle docs/<PROJEKT_NAME>_ARCHITEKTUR.md mit den Inhalten aus dem Brainstorm.
    Halte dich an die existierende Sektions-Reihenfolge (1. Projekt-Identität …
    13. Offene Fragen). Schreibe nur, was der Brainstorm hergibt — leere Sektionen
    bleiben mit Platzhalter-Hinweis (*(noch offen)*) stehen statt erfundener
    Inhalte.
15. Setze "Stand: <heute>" und "Status: Architektur in Arbeit" am Dateikopf.

Phase 5 — Roadmap-Skelette füllen oder löschen
16. docs/roadmap/ROADMAP.md: Phasen-Übersicht aus dem Brainstorm einsetzen
    (Phase 1/2/3 — Titel + Ein-Satz-Ziel).
17. docs/roadmap/PHASE1.md (und PHASE2.md / PHASE3.md, sofern verwendet):
    Features als ⛔-Liste eintragen, gruppiert wie im Brainstorm. KEINE Features
    auf ✅ setzen — der Kickoff ist Vor-Implementierung.
18. Wenn der Brainstorm nur Phase 1 oder 1+2 vorsieht: die ungenutzten Phasen-
    Dateien LÖSCHEN und alle Verweise (CLAUDE.md on_demand_files, docs/README.md,
    docs/templates/SEASON_PROMPT.md "Welche Roadmap-Datei?"-Tabelle) entsprechend
    kürzen. Frag mich vorher zur Bestätigung.

Phase 6 — Status-Dateien initialisieren
19. docs/FEATURES.md: Feature-Matrix mit allen Phase-1/2/3-Einträgen als ⛔
    (nichts ist gebaut). Schema siehe existierende Tabellen-Struktur.
20. docs/CHANGELOG.md: erster Eintrag oben "## <heute> — Projekt-Kickoff",
    eine Zeile pro großem Architektur-Baustein, der schriftlich festgehalten
    wurde. Kein Code, kein Feature ist fertig — der Eintrag dokumentiert nur
    den Übergang Brainstorm → Repo.
21. docs/ENTSCHEIDUNGEN.md, docs/TECH_SCHULDEN.md, docs/SEASON_LOG.md,
    docs/GLOSSAR.md, docs/DEV_SETUP.md: prüfen, ob die Skelette leer/sauber sind.
    Nicht spekulativ füllen — bleiben bis zur ersten Season leer. Gleiches gilt
    für die zwei unteren Tabellen in docs/COMMANDS.md ("Verifiziert
    funktionierende Befehle" und "Bekannt nicht funktionierende Befehle") — die
    werden im laufenden Betrieb gefüllt, nicht beim Kickoff.

Phase 7 — README anpassen
22. README.md (Root): Falls der User mir nicht ausdrücklich sagt, sie als
    Vorlage-Doku zu behalten — ersetze den Inhalt durch eine projekt-spezifische
    Kurzfassung: <PROJEKT_NAME>, <KURZBESCHREIBUNG>, Stack-Zeile, Verweis auf
    docs/<PROJEKT_NAME>_ARCHITEKTUR.md und docs/roadmap/. Die Platzhalter-Tabelle
    und der "So nutzt du die Vorlage"-Block sind im abgeleiteten Projekt obsolet
    und sollen weg. Frag vor dem Überschreiben einmal nach.

Phase 8 — Git und lokale Overrides
23. Prüfe, ob das Repo bereits auf den finalen Remote zeigt (`git remote -v`).
    Wenn nicht / wenn die Vorlage-Origin noch dranhängt: sag es mir, nimm aber
    KEINE Remote-Änderung selbst vor.
24. CLAUDE.local.md: Skelett bleibt im Vorlage-Repo committed, im abgeleiteten
    Projekt NICHT. Prüfe, ob .gitignore in diesem Repo CLAUDE.local.md
    ausschließt. Falls nicht: Eintrag vorschlagen, nicht selbst hinzufügen
    (`/* CLAUDE.local.md */` — eine Zeile, ich entscheide).
25. KEINE git-Operationen jenseits read-only (status, diff, log) ohne explizites
    Signal. Keinen Initial-Commit setzen — das macht der User mit der konfigurierten
    Commit-Trigger-Phrase (siehe Phase 9).

Phase 9 — Verifikation und Übergabe
26. Suche das ganze Repo nach übrig gebliebenen {{...}}-Tokens, die du laut
    Phase-2-Sonderfällen NICHT bewusst stehen gelassen hast. Wenn welche
    auftauchen: liste sie auf, ich entscheide.
27. Berichte den End-Zustand:
    - geänderte Dateien (gruppiert: umbenannt / inhaltlich gefüllt / Tokens
      ersetzt / gelöscht)
    - offene Fragen aus Phase 4 (Architektur-Sektion 13)
    - empfohlene erste Season (kurzer Vorschlag aus PHASE1.md — der User
      bestätigt vor dem nächsten Schritt)
28. Erinnere mich an die nächsten Aktionen, die NUR ich auslöse:
    - Initial-Commit per Commit-Trigger-Phrase (siehe CLAUDE.md
      workbench.trigger_phrases.commit, gerade gesetzt in Phase 1).
    - Erste Feature-Season per SEASON_PROMPT.md.

Was du NICHT tust
- Keinen Code schreiben (kein src/, kein package.json, keine Migrations).
- Keine Tests anlegen.
- Keine Commits, keine Pushes, keine Tags.
- Keine Inhalte erfinden, die nicht im Brainstorm-Input stehen — bei Lücken
  fragen.
- Keine Tokens in den Template-Dateien (docs/templates/*.md) ersetzen.
- Keine .claude/rules/-Dateien anfassen.
- Keine bewussten Skelett-Bereiche der Vorlage (FEATURES.md, ENTSCHEIDUNGEN.md
  etc.) inhaltlich vor-befüllen.
- Keine Werte in den unteren Tabellen von docs/COMMANDS.md eintragen — die
  füllt der laufende Betrieb.
```

---

## Ist das nicht das, was die "So nutzt du die Vorlage"-Anleitung im README schon sagt?

Die README beschreibt das aus Sicht eines Menschen, der die Vorlage manuell ausfüllt. Dieses Template ist die Anweisung an einen Agent, dasselbe Ergebnis aus einem unstrukturierten Brainstorm-Output zu erzeugen — mit klaren Stopp-Punkten, festgelegter Reihenfolge und expliziter Liste, was er NICHT tun darf. Der entscheidende Mehrwert ist Phase 1 (extrahieren + bestätigen) und Phase 9 (nichts übersehen).

## Warum kein Sub-Agent-Pattern wie bei Code-Review / Release?

Kickoff ist sequentiell: jeder Schritt baut auf der Bestätigung des Vorgängers auf. Parallelität bringt hier nichts — der User muss in Phase 1 das Wertepaket freigeben, sonst läuft der Rest schief. Außerdem ist der Kontext für den Haupt-Agent klein genug, dass keine Isolation nötig ist.

## Wann kein Kickoff?

- **Vorlage wird in einem bereits laufenden Projekt nachgepflegt** (z.B. nachträglich CLAUDE.md auf das Vorlage-Schema bringen) — dann ist es eine normale Feature-Season, kein Kickoff. Vorgehen über [SEASON_PROMPT.md](./SEASON_PROMPT.md).
- **Brainstorm liegt noch nicht vor** — kein Kickoff. Erst Brainstorm in der separaten Session zu Ende führen, dann zurück hierher.
- **Repo enthält schon Code** — kein Kickoff. Code-Existenz ist ein Bruch mit Phase 2 (globaler Token-Replace) und Phase 7 (README überschreiben). Stattdessen den Brainstorm-Output in eine Architektur-Refactoring-Season umlenken.
