# Praxis — Daten einer App

Quellen: Spec v0.4, 06 *Daten von Apps*, *Arbeitspferde*, *Demo-App Taschenrechner*, Invarianten P1, P3, P6; 03 *Beschreibung einer Oberfläche*. AA-AIbex-AIOS, V0.4, Memos 43, 49–56, 67; V0.5, Memo 07. Paket `app-taschenrechner` 0.4.2.

| # | Regel | Beispiel |
|---|---|---|
| D1 | Daten, die ein Paket im Projekt erzeugt, liegen in **`<projekt>/@Data/<paket>/`**, benannt nach dem Paket | `@Data/app-taschenrechner/funktionstasten.yaml` |
| D2 | **Nie ins Paket schreiben:** `@!Package/<paket>/` gehört `aios --fetch` und wird bei Abgleich und Update ersetzt | — |
| D3 | Das Paket legt `@Data/<paket>/` beim ersten Schreiben selbst an | Skill `taschenrechner` |
| D4 | `@Data/` bleibt bei Update und `--remove` stehen; nur das Paket selbst ändert ihn | — |
| D5 | `@Data/` ist versioniert und nicht im Kontext; das Paket liest seine Daten selbst | — |
| D6 | Mitgelieferte Daten gehören **verborgen** ins Wissen des Pakets (`knowledge/@!…/`); die App bietet sie an und übernimmt sie auf Wunsch nach `@Data/` | `knowledge/@!Funktionstasten/quadrat.yaml` |
| D7 | Ein HTML-Teil kann keine Dateien schreiben: Er sendet mit `sendPrompt` eine Nachricht, ein Skill zeigt, was gespeichert wird, und schreibt nach Ja | Rechner → „Speichere die Funktionstaste A …" |
| D8 | Gespeicherte Daten kommen beim Öffnen über `{{aios-data <datei>}}` in den HTML-Teil (`null`, wenn die Datei fehlt) | `{{aios-data funktionstasten.yaml}}` |
| D9 | Ein Datenformat wählen, das ein Mensch auch im Chat tippen kann; der Skill versteht die getippte Form | Tasten durch Leerzeichen, `x`/`*` für `×` |
| D10 | Arbeitspferde bekommen `AIOS_DATA` = `@Data/<paket>/`; ihre Skripte laufen nur nach eigener Bestätigung | `aios --worker <paket>/db install` |

## Assistenten

Spec v0.4 nennt `@Data/` nur für Apps. Als Konvention von AIbex gilt D1–D5 auch für Assistenten: `@Data/assistant-<name>/` (V0.5, Memo 07, Wunsch an die Spec). Vorgaben des Users gehören trotzdem in eine Regel im Masterspace, nicht nach `@Data/`.
