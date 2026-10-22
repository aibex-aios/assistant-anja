# Praxis — Abhängigkeiten

Quellen: Spec v0.4, 06 *`manifest.yaml`*, *Versionen und Bereiche*, *Resolver*, *Holen*, *Ausrollen*, *Vorrang*. AA-AIbex-AIOS, V0.4, Memos 17, 21, 24 (H4), 26 (H5), 27, 74 (B8).

| # | Regel | Beispiel |
|---|---|---|
| B1 | `depends` **sparsam**: nur Pakete, ohne die das Paket nicht läuft. Was nur gut zusammenpasst, bleibt unabhängig und findet sich über die Kette | Astronom und `knowledge-orion` ohne `depends` |
| B2 | Bereiche mit `~=`: ab 1.0 `~=X.Y`, darunter `~=0.Y.Z` | `skill-memo: "~=6.0"` |
| B3 | `aios` gehört nach `requires`, nie nach `depends` | `requires: {aios: ">=0.4,<0.5"}` |
| B4 | Eine Abhängigkeit wird **zuerst im Hub des verlangenden Pakets** gesucht, dann in der Hub-Liste; zusammengehörige Pakete am besten im selben Hub | — |
| B5 | Ein gleichnamiges Paket in mehreren Hubs der Hub-Liste führt zum Abbruch mit Exit 3 und einer Rückfrage; Namen im eigenen Hub eindeutig halten | `skill-memo` in zwei Test-Hubs |
| B6 | Mit `--from <repo>` hat das Paket keinen Hub; seine Abhängigkeiten kommen aus der Hub-Liste. Bei mehreren Treffern die Abhängigkeit vorher mit vollem Namen holen | `aios --fetch aibex-aios/skill-memo`, dann `--from` |
| B7 | Abhängigkeiten werden **ganz** ausgerollt (`only` gilt nur für Pakete aus `packages:`) und immer in dasselbe Projekt geholt wie das verlangende Paket | — |
| B8 | Kein Backtracking: Erfüllt keine Version alle Bereiche, bricht der Resolver mit den Konflikten ab. Enge Bereiche (`==`) in `depends` vermeiden (Ausnahme: Distributionen) | — |
| B9 | Zwei Pakete mit Elementen gleichen Namens im selben Masterspace sind ein Fehler; Elementnamen über Pakete hinweg eindeutig wählen | — |

## Prüfen vor dem Veröffentlichen

- Jede Abhängigkeit gibt es mit passender Version im Ziel-Hub (`aios --library <paket>`).
- Die Probe holt in ein leeres Testprojekt, damit fehlende Abhängigkeiten nicht von Paketen darüber verdeckt werden.
