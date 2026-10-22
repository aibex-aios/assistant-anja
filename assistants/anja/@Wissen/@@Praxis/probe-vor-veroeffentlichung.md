# Praxis — Probe vor Veröffentlichung

Quellen: Spec v0.4, 03 *Registrieren* (Wirksamkeit); 06 *Holen* (Pflegeprojekte, Prüfung beim Holen). AA-AIbex-AIOS, V0.4, Memos 44, 61, 62, 66.

| # | Schritt | Wie |
|---|---|---|
| P1 | Lokal committen und **lokal taggen**; ohne Tag holt AIOS nichts, auch nicht mit `--from` | `git -C <repo> tag v0.1.0` |
| P2 | In ein **leeres Testprojekt** holen, in einem mit AIOS aktivierten Vault | `aios --fetch <paket> --from <pfad-zum-repo> --to <testprojekt>` |
| P3 | Meldungen der Prüfung beim Holen beachten: Namen aus `contents`, gültige `version` je Skill, `gui` in `skills`, keine doppelten Elementnamen | Ausgabe von `aios --fetch` |
| P4 | **Neuen Chat** im Testprojekt öffnen; Skills wirken erst ab dem nächsten Chat | — |
| P5 | Kontext prüfen: Assistent aufgelöst, Wissen geladen bzw. im Inhaltsverzeichnis, keine Verdeckung | `/aios-context`, `aios-context --assistant <name>` |
| P6 | Assistent zuordnen und ausprobieren: Prefix, Handwerk, **Grenzen** (eine Aufgabe außerhalb des Bereichs stellen) | `/aios-assistant <Name>` |
| P7 | Oberfläche in der eigenen **und** in einer frischen Session prüfen; jeden Ausweg im Chat einmal benutzen | `/gui` bzw. `/<name>-gui` |
| P8 | **Live-Probe mit einem kleinen Modell** (z. B. haiku): Was ein kleines Modell aus Rollentext und Skill richtig macht, macht ein großes erst recht | — |
| P9 | Korrigieren, lokalen Tag nachziehen, im Testprojekt neu holen | `aios --fetch --upgrade <paket>` |

## Zu beachten

- Das Testprojekt ist ein eigenes Projekt mit `@/`, z. B. ein Unterprojekt des Konzeptprojekts; ein Assistent wird dort dem Projekt zugeordnet.
- Befunde der Probe gehören als Memo ins Konzeptprojekt, nicht ins Paket-Repo.
