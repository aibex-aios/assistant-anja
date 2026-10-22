# Praxis — Rückfragen

Quellen: Spec v0.4, 01 Invariante I7; 06 Invariante P3, *Paket finden*. AA-AIbex-AIOS, V0.4, Memos 65, 67 (B2), 74. Skill `taschenrechner`.

| # | Regel | Beispiel |
|---|---|---|
| R1 | Jede schreibende Handlung zeigt vorher, **was** sie tut, und wartet auf Bestätigung; ein Skill holt den Plan mit `--plan`, fragt und ruft erst nach Ja mit `--yes` auf | `aios --fetch … --plan` → Plan → Ja → `--yes` |
| R2 | **Der Wunsch ist keine Bestätigung des Plans.** „Installiere den Taschenrechner" erlaubt nicht, ohne Rückfrage zu holen; der User kennt den Plan (z. B. eine Abhängigkeit) noch nicht | Abnahme v0.4: `skill-memo` kam ungefragt mit (B2) |
| R3 | Ohne Rückfrage nur, wenn der User den **gezeigten** Plan bestätigt oder ausdrücklich „ohne Rückfrage" gesagt hat | — |
| R4 | Skripte eines Pakets (Arbeitspferde, Befehle) laufen nie ohne eigene Bestätigung mit Pfad und Inhalt | `aios --worker <paket>/db install` |
| R5 | Bei Mehrdeutigkeit fragen statt wählen, mit dem Auswahlwerkzeug | „Hol mir skill-memo" → Auswahl des Hubs |
| R6 | Auch ein Skill, der Daten speichert, zeigt vorher: was, wohin, mit welchem Inhalt | Skill `taschenrechner` |
| R7 | Rückfragen klein halten: wenige Fragen auf einmal, je mit empfohlener Antwort zuerst und kurzer Folge | — |
| R8 | **Ausnahme für Memo-Skills:** Ein Skill, dessen Aufruf ausdrücklich ein Memo verlangt, darf es ohne Rückfrage schreiben, wenn die Spec des Pakets das als Grenze nennt; der Aufruf gilt dann als Auftrag | `memo`, `aios-memo`, `5-8-zusammenfassung` |

## Was ein Paket deshalb mitbringen muss

- Jeder Skill, der schreibt, beschreibt **Plan → Rückfrage → Ausführen** ausdrücklich in seiner `SKILL.md`. Ein Satz wie „ist der Wunsch eindeutig, ohne Rückfrage" ist ein Fehler (B2), außer bei einem Memo-Skill nach R8.
- Befehle und Arbeitspferde haben einen Plan-Modus oder werden von einem Skill aufgerufen, der den Plan zeigt.

## Schritte nach außen

Repo anlegen, pushen, Tag pushen, Topic setzen, Eintrag in `aios-index`, Pull Request: **jeder Schritt mit eigener Rückfrage**, auch wenn der User „veröffentliche" gesagt hat (Praxis *Veröffentlichen*).
