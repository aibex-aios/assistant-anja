# Praxis — Probe vor Veröffentlichung

Quellen: Spec v0.6.1, 03 *Registrieren* (Wirksamkeit), *Wechsel*; 05 *Namensregel*; 06 *Holen* (Pflegeprojekte, Prüfung beim Holen, Schritt 8), *Versionen und Bereiche*. AA-AIbex-AIOS, V0.4, Memos 44, 61, 62, 66. MAA-Anja-AIOS-Expert, Memos 76, 77, 78 (F22, F23).

| # | Schritt | Wie |
|---|---|---|
| P1 | Lokal committen, `version` im **Manifest** auf `<x.y.z>-rc<n>` setzen (Elemente bleiben `<x.y.z>`), committen und den **Release-Kandidaten** taggen; ohne Tag holt AIOS nichts, auch nicht mit `--from`, und Tag und `version` im Manifest müssen gleich sein (Praxis *Getaggte Stände*, T5) | `version: 0.1.0-rc1`, `git -C <repo> tag v0.1.0-rc1` |
| P2 | Ein **leeres Testprojekt** `<Präfix>P-Probe-<Name>` anlegen, z. B. `MSFP-Probe-Skill-5-8-Zusammenfassung` unter `MSF-Fünf-Acht-Zusammenfassung`, und den Kandidaten holen: im Testprojekt oder mit `--to <testprojekt>` | `aios --init <testprojekt>`, dann `aios --fetch "<paket>==0.1.0-rc1" --from <pfad-zum-repo> --to <testprojekt>` |
| P3 | Meldungen der Prüfung beim Holen beachten: Namen aus `contents`, gültige `version` je Skill, `gui` in `skills`, keine doppelten Elementnamen | Ausgabe von `aios --fetch` |
| P4 | **Neuen Chat** im Testprojekt öffnen; Skills wirken erst ab dem nächsten Chat | — |
| P5 | Kontext prüfen: Assistent aufgelöst **in der erwarteten Version** (`version=` in `AIOS-ASSISTANT-LOAD`), Wissen geladen bzw. im Inhaltsverzeichnis, keine Verdeckung. Eine verworfene Kopie (ungültige Version, falscher Name) wird still von der nächsten gültigen verdeckt; `/aios-context` nennt das Problem | `/aios-context`, `aios --context --assistant <name> --load <testprojekt>` |
| P6 | Assistent zuordnen und ausprobieren: Prefix, Handwerk, **Grenzen** (eine Aufgabe außerhalb des Bereichs stellen); Skills als **ganzen Prompt** aufrufen | `/aios-assistant <Name>` im Testprojekt; `/<skill> …` |
| P7 | Oberfläche in der eigenen **und** in einer frischen Session prüfen; jeden Ausweg im Chat einmal benutzen | `/gui` bzw. `/<name>-gui` |
| P8 | **Live-Probe** mit einem kleinen Modell (z. B. haiku) oder als Headless-Lauf ohne die Regeln des Users (Praxis *Testvorlagen*) | `claude -p` im Testprojekt |
| P9 | Korrigieren, `version` im Manifest auf `-rc<n+1>`, committen, neuen Kandidaten taggen, im Testprojekt neu holen (Praxis *Getaggte Stände*) | `aios --fetch "<paket>==0.1.0-rc2" --from <repo> --to <testprojekt>` |

## Zu beachten

- Das Testprojekt ist ein eigenes Projekt mit `@/`, z. B. ein Unterprojekt des Konzeptprojekts; ein Assistent wird dort dem Projekt zugeordnet.
- **Name des Testprojekts:** Als Unterprojekt gilt für es die Namensregel von `aios --init` (Spec 05 *Namensregel*): Präfix des Konzeptprojekts plus ein Großbuchstabe (`P` für Probe), jeder Namensteil mit großem Anfangsbuchstaben. `P-Probe-skill-…` lehnt `aios --init` ab. `aios --init <testprojekt> --plan` zeigt einen Verstoß, bevor etwas angelegt wird.
- **`--to`:** `aios --fetch … --to <projekt>` registriert seit v0.6 im Ziel, auch mehrere Ebenen unter dem Projekt der Session (Spec 06 *Holen*, Schritt 8). `aios --assistant --to` nimmt dagegen nur Projekte der Kette nach oben an, kein Unterprojekt (Spec 03 *Wechsel*); einen Assistenten ordnest du deshalb im Testprojekt selbst zu. Erbt das Testprojekt den Assistenten, gewinnt beim Auflösen die Kopie im `@!Package/` des Testprojekts (die nächste).
- **Skills als ganzer Prompt:** Tippt der User `/<skill> …` als ganzen Prompt, lädt der Host den Skill direkt. Ruft die KI einen Skill aus einem Paket selbst über das Skill-Werkzeug auf, fragt der Host, weil der Hook nur Kernel-Skills freigibt (Spec 02 *Freigabe*, S2); ohne Fenster scheitert der Aufruf (MAA, Memo 77).
- Befunde der Probe gehören als Memo ins Konzeptprojekt, nicht ins Paket-Repo.
