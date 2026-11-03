# Praxis — Daten einer App

Quellen: Spec v0.6.1, 06 *Daten der Pakete*; 07 *Definition* (K7); *Demo-App Taschenrechner*, Invarianten P1, P3, P6; 03 *Beschreibung einer Oberfläche*. AA-AIbex-AIOS, V0.4, Memos 43, 49–56, 67; V0.5, Memo 07. Paket `app-taschenrechner` 0.5.1.

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
| D10 | Ein Arbeitspferd (`worker-…`) hat keine eigenen Daten im Projekt; das **nutzende** Paket legt sie unter seinem `@Data/` ab (Spec 07, K7) | Datenbank einer App unter `@Data/app-notizen/` |

## Assistenten

`@Data/` gilt für jedes Paket, dessen Elemente schreiben, also auch für Assistenten: `@Data/assistant-<name>/` (Spec 06, *Daten der Pakete*; V0.5, Memo 07). Vorgaben des Users gehören trotzdem in eine Regel im Masterspace, nicht nach `@Data/`.
