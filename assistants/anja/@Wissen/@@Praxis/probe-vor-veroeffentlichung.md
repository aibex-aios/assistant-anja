# Praxis — Probe vor Veröffentlichung

Quellen: Spec v0.4, 03 *Registrieren* (Wirksamkeit); 06 *Holen* (Pflegeprojekte, Prüfung beim Holen). AA-AIbex-AIOS, V0.4, Memos 44, 61, 62, 66.

| # | Schritt | Wie |
|---|---|---|
| P1 | Lokal committen und **lokal taggen**; ohne Tag holt AIOS nichts, auch nicht mit `--from` | `git -C <repo> tag v0.1.0` |
| P2 | Ein **leeres Testprojekt** `P-Probe-<paket>` anlegen (Namensregel von `aios --init`: Präfix vor dem Namen) und das Paket **im Testprojekt selbst** holen | `aios --init <testprojekt>`, dann im Testprojekt `aios --fetch <paket> --from <pfad-zum-repo>` |
| P3 | Meldungen der Prüfung beim Holen beachten: Namen aus `contents`, gültige `version` je Skill, `gui` in `skills`, keine doppelten Elementnamen | Ausgabe von `aios --fetch` |
| P4 | **Neuen Chat** im Testprojekt öffnen; Skills wirken erst ab dem nächsten Chat | — |
| P5 | Kontext prüfen: Assistent aufgelöst, Wissen geladen bzw. im Inhaltsverzeichnis, keine Verdeckung | `/aios-context`, `aios-context --assistant <name>` |
| P6 | Assistent zuordnen und ausprobieren: Prefix, Handwerk, **Grenzen** (eine Aufgabe außerhalb des Bereichs stellen) | `/aios-assistant <Name>` |
| P7 | Oberfläche in der eigenen **und** in einer frischen Session prüfen; jeden Ausweg im Chat einmal benutzen | `/gui` bzw. `/<name>-gui` |
| P8 | **Live-Probe mit einem kleinen Modell** (z. B. haiku): Was ein kleines Modell aus Rollentext und Skill richtig macht, macht ein großes erst recht | — |
| P9 | Korrigieren, lokalen Tag nachziehen, im Testprojekt entfernen, Cache-Eintrag löschen, neu holen (Praxis *Getaggte Stände*, Abschnitt *Zu beachten*) | `aios --fetch --remove <paket>`, dann `aios --fetch <paket> --from <repo>` |

## Zu beachten

- Das Testprojekt ist ein eigenes Projekt mit `@/`, z. B. ein Unterprojekt des Konzeptprojekts; ein Assistent wird dort dem Projekt zugeordnet.
- **Warum im Testprojekt selbst:** `aios --fetch --to <projekt>` registriert die Skills im Projekt der Session, nicht im Ziel (Spec 06 *Holen*, Schritt 7), und `aios --assistant --to` nimmt nur Projekte der Kette nach oben an, kein Unterprojekt (Spec 03 *Wechsel*). Beides ist so spezifiziert; Holen und Zuordnen deshalb im Testprojekt ausführen.
- Befunde der Probe gehören als Memo ins Konzeptprojekt, nicht ins Paket-Repo.
