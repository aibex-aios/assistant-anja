# Praxis — Oberflächen

Quellen: Spec v0.4, 03 *Oberflächen*. AA-AIbex-AIOS, V0.3, Memo 60 und A10; V0.4, Memos 29, 31, 66 (B4), 67. Pakete `assistent-gaertner`, `app-taschenrechner` 0.4.2.

| # | Regel | Beispiel |
|---|---|---|
| O1 | Eine Oberfläche ist eine **Abkürzung** zu Prompts und Skills, kein eigenes Programm; alles läuft über Claude und die Rückfragen von AIOS | — |
| O2 | Sie ist ein eigener Skill `<name>-gui` mit `SKILL.md`, `version`, `gui.yaml` und optionalen HTML-Teilen | `gaertner-gui` |
| O3 | Ein Assistent hat **eine** Oberfläche (`gui:`, aufgerufen mit `/gui`); eine App ebenso (`contents.gui`, aufgerufen über ihren Skill oder die Kachel *Apps* von `/aios-gui`, nicht über `/gui`) | `/taschenrechner-gui` |
| O4 | 1 bis 12 Kacheln, je mit genau einem von `prompt`, `skill`, `html` | — |
| O5 | Kacheln senden nie einen Text mit `/` am Anfang (die Desktop-App verwirft ihn), sondern „Run the skill /<skill>. …" | Taschenrechner, Kachel *Funktionstasten anzeigen* |
| O6 | Ein HTML-Teil ist ein Fragment ohne `<html>`, `<head>`, `<body>`, mit eingebettetem CSS und JavaScript, ohne Inline-Handler (`onclick`), Skripte auf oberster Ebene, ohne Netz | `rechner.html` |
| O7 | **Jede Aktion braucht einen Ausweg im Chat**, weil `sendPrompt` nicht in jeder Session ankommt: Die Oberfläche zeigt den Satz, den der User tippen kann, und der Skill versteht ihn | „Gespeichert wird im Chat. Kommt dort keine Nachricht an, schreib: Speichere die Funktionstaste A …" |
| O8 | Was erst Claude erledigt, darf in der Oberfläche **nicht erledigt aussehen** | „Belegt: A …" sah gespeichert aus (B4) |
| O9 | In der CLI erscheint dieselbe Beschreibung als Menü; Kacheln mit `html` fehlen dort | — |

## Zu beachten

- Eine Oberfläche ist optional; sie lohnt sich, wenn Anwender ohne Befehlskenntnis wiederkehrende Aufgaben haben.
- In **zwei** Sessions testen: in der eigenen und in einer frischen, weil `sendPrompt` sich je Session unterschiedlich verhielt (V0.4, Memo 66).
