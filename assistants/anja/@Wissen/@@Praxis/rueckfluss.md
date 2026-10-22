# Praxis — Rückfluss

Quellen: Spec v0.4, 06 *Rückfluss*, Invariante P5. AA-AIbex-AIOS, V0.4, Memos 11, 19 (L3, L4), 55, 56, 74, 75, 76. Paket `app-taschenrechner`, Pull Request `aibex-aios/app-taschenrechner#1`.

## Der Weg eines Beitrags

| # | Wer | Schritt |
|---|---|---|
| F1 | User | Daten aus `@Data/<paket>/` als Beitrag senden, mit Plan und Rückfrage: `aios --contribute @Data/<paket>/<datei> --to <paket>` |
| F2 | AIOS | eigener Zweig `contrib/<user>/<datum>-<kurzname>`, Datei nach `contrib/<user>/<datei>`, Pull Request gegen den Standardzweig; ohne Schreibrecht über einen Fork |
| F3 | Maintainer | Pull Request prüfen und mergen; damit liegt der Beitrag in `contrib/`, **noch nicht im Inhalt** |
| F4 | Maintainer | Beitrag in den Inhalt übernehmen (beim Taschenrechner nach `knowledge/@!Funktionstasten/`), Version erhöhen, taggen, veröffentlichen |
| F5 | andere User | bekommen ihn mit `aios --fetch --upgrade <paket>` |

## Regeln

| # | Regel |
|---|---|
| F6 | AIOS pusht nie auf den Standardzweig; jeder Beitrag hat einen eigenen Zweig und Pull Request |
| F7 | Ein Paket, das Beiträge annehmen will, sagt in seinem Skill, welche Datei sich eignet, und bietet den Aufruf mit Plan an (Skill `taschenrechner`, *Zurückspielen*) |
| F8 | Mitgelieferte Daten stehen verborgen im Wissen (`knowledge/@!…/`), damit Beiträge nicht ungefragt in den Kontext aller User kommen |
| F9 | Ein Beitrag, der als eigenes Paket veröffentlicht wird (`type: knowledge`), ist ein Paket, aber kein Modul |

## Zu beachten

- **F3 ist nicht F4.** Beim Taschenrechner ist der Pull Request #1 gemergt, die Übernahme in den Inhalt und die neue Version standen bei v0.4.0 noch aus (V0.4, Memo 76). Erinnere den Maintainer an F4, wenn `contrib/` Dateien enthält, die nicht im Inhalt stehen.
- `aios --contribute` braucht `gh` mit Anmeldung; ohne Zugang meldet es das und legt nichts an.
