# Praxis — Testvorlagen

Quellen: Spec v0.6.1, 02 *Freigabe*; 04 *Umlenkung für Tests* (`AIOS_HUBS`, `AIOS_GITHUB`); 06 *Hub-Liste*, *Rückfluss* (Tests). AA-AIbex-AIOS, V0.4, Memos 19 (L4), 27, 44, 61, 62 (G1), 68, 71. MAA-Anja-AIOS-Expert, Memos 77, 80 (F28). Code-Repo `aibex-aios`, `tests/hub/`, `tests/live/`.

Testvorlagen braucht, wer **automatische Tests** gegen Pakete schreibt: der Kernel und jedes Paket mit eigenem Code (Befehle, Arbeitspferde). Für ein einfaches Paket genügt die Probe.

| # | Regel | Beispiel |
|---|---|---|
| E1 | Hubs für Tests liegen lokal unter `file://` und werden mit `AIOS_HUBS` eingesetzt; GitHub mit `AIOS_GITHUB` umgelenkt; `gh` durch eine Attrappe im `PATH` ersetzt | `AIOS_HUBS="aibex-aios=file://… aibex-hub=file://…"` |
| E2 | Eine Vorlage einer **echten** Version ist **gleich dem Tag im Repo**; geprüft mit `diff` | `skill-memo` 6.0.0 im Test-Hub = Tag `v6.0.0` |
| E3 | **Testversionen** (eigens für einen Test verändert) bekommen eine **höhere Nummer** als jede echte Version und werden mit jeder neuen echten Version weiter hochgezählt | Taschenrechner: echt 0.4.2, Testversion 0.4.3 |
| E4 | Reine Testpakete tragen das Präfix `test-` und kommen nie in einen echten Hub | `test-…` |
| E5 | Zwei Hubs mit einem gleichnamigen Paket prüfen die Rückfrage bei Mehrdeutigkeit | `skill-memo` in beiden Test-Hubs |
| E6 | Live-Tests mit einem kleinen Modell (haiku) prüfen Hooks, Skills, Assistenten und Oberflächen; sie nehmen die Pakete aus dem Test-Hub | `tests/live/assistants.sh` |
| E7 | **Headless-Läufe ohne die Regeln des Users** zeigen, was der Hook allein freigibt: `claude -p "<prompt>" --output-format stream-json --verbose --permission-mode default --setting-sources project --settings <datei mit nur den Hooks>` im Testprojekt; zum Schreiben von Dateien `--permission-mode acceptEdits`. Abgelehnte Aufrufe stehen im Ergebnis unter `permission_denials`, der Verlauf im Transkript | `MAAP-Probe-Anja-030/probe/run_probe.py` (MAA, Memo 77) |

## Zu beachten

- Nach jeder neuen echten Version die Test-Hubs neu bauen und E2 erneut prüfen.
- Testversionen nie veröffentlichen; ihre höhere Nummer würde sonst bei `--upgrade` gewinnen.
- **Warum E7:** Erlaubt der User global `Bash` (`permissions.allow`), fragt der Host bei keinem Befehl; ob ein Skill auch bei anderen Usern ohne Rückfrage läuft, zeigt erst ein Lauf ohne diese Regel. Ein Lauf je Variante zeigt eine Tendenz, keine Gewissheit.
