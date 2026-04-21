# Feature-Status

Legende:

- ✅ **fertig** – läuft im aktuellen Build
- 🟡 **teilweise** – Grundgerüst steht, es fehlt was Offensichtliches
- ⛔ **offen** – noch nicht angefasst

Nach jedem umgesetzten Feature wird der Eintrag hier auf ✅ gesetzt und in [CHANGELOG.md](./CHANGELOG.md) ein Eintrag angelegt.

Alle offenen Features mit Details → [ROADMAP.md](./ROADMAP.md)

---

## {{BEREICH_1}}

Kurze Einleitung, was dieser Bereich umfasst (1 Satz). Reicht oft ein Stichwort.

| Feature                                   | Status | Bemerkung                                                  |
| ----------------------------------------- | ------ | ---------------------------------------------------------- |
| `<Feature A>`                             | ⛔      |                                                            |
| `<Feature B>`                             | ⛔      |                                                            |
| `<Feature C>`                             | ⛔      |                                                            |

## {{BEREICH_2}}

| Feature                                   | Status | Bemerkung                                                  |
| ----------------------------------------- | ------ | ---------------------------------------------------------- |
| `<Feature>`                               | ⛔      |                                                            |

---

## Hinweise zur Pflege

- **Ein Feature pro Zeile.** Zu grobe Zeilen („UI aufgebaut") verlieren ihre Aussagekraft.
- **Bereich-Gruppen** sollten sich an der `ARCHITEKTUR.md` orientieren (pro Hauptmodul / Domain ein Abschnitt).
- Wenn ein Bereich **leer** ist (noch nichts geplant), trotzdem mit der Überschrift drinlassen — signalisiert, dass der Bereich vorgesehen ist.
- **Fertige Features** werden *nicht* aus der Tabelle entfernt — ✅-Markierung bleibt als Referenz, zusammen mit Datum in der Bemerkung.
