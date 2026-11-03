# Praxis — Veröffentlichen

Quellen: Spec v0.6.1, 06 *Hubs*, *Index und Suche*, *Paketwechsel bei der Aktivierung*. AA-AIbex-AIOS, Memo 04 (Tags im Konzept-Repo); V0.4, Memos 28, 45, 46, 61, 62, 76; V0.6, Memos 77 (R4), 112, 113 (R9). MAA-Anja-AIOS-Expert, Memo 82 (F33, F34).

Jeder Schritt ist nach außen wirksam und bekommt eine **eigene Rückfrage**.

| # | Schritt | Wie |
|---|---|---|
| V1 | Abnahme auf einem Release-Kandidaten bestanden, Stand committet, Tag `v<x.y.z>` gleich `version` in Manifest und Elementen | `git -C <repo> status`, Manifest lesen |
| V2 | Hub, Owner, Sichtbarkeit aus den Vorgaben des Users; sonst fragen. Öffentlich heißt: `aios --fetch` braucht keine Anmeldung | Regel *AIOS-Pakete — Vorgaben* |
| V3 | **Beim Kernel:** Begleitpakete, die die neue Version braucht (deren `requires.aios` erst zu ihr passt), vor oder mit dem Kernel veröffentlichen; sonst bricht `aios --activate` bei Usern ab oder findet keine passende Version | v0.6.0: Begleitpakete mit `<0.7` (V0.6, Memo 51) |
| V4 | Repo im Hub anlegen, Name gleich dem Paketnamen | `gh repo create <owner>/<paket> --public --source <repo>` |
| V5 | **Vor jedem Push** die Commits zeigen, die hinausgehen, nicht nur zählen; Commits, die nicht aus dieser Session stammen, nennen und fragen | `git -C <repo> log origin/main..main` |
| V6 | Zweig und Tag pushen | `git -C <repo> push -u origin main`, `git -C <repo> push origin v<x.y.z>` |
| V7 | Topic **`aios-package`** setzen (beim Kernel `aios-core`) | `gh repo edit <owner>/<paket> --add-topic aios-package` |
| V8 | Eintrag in `aios-index` des Hubs (`index.yaml`: `name`, `type`, `description`), falls der Hub einen Index hat | Commit und Push in `<owner>/aios-index` |
| V9 | Beschreibung des Repos setzen (ein Satz, wie `description`) | `gh repo edit <owner>/<paket> --description "…"` |
| V10 | Probe gegen den echten Hub in einem frischen Testprojekt | `aios --library <paket>`, `aios --fetch <paket> --to <testprojekt>` |
| V11 | Tag `<paket>-v<version>` im Konzept-Repo auf dem Abnahme-Memo (ohne Abnahme auf dem Memo der Veröffentlichung), mit Verweis auf den Commit im Paket-Repo; pushen (V5 gilt auch hier) | annotierter Tag |
| V12 | Ergebnis als Memo im Konzeptprojekt | — |

## Zu beachten

- Ab dem Push ist der Tag endgültig. Jede spätere Änderung, auch am README, ist eine neue Version: committen, Kandidat taggen, Probe, endgültig taggen, V5, V6, gegebenenfalls V8, V10, V11.
- **Warum V5:** Andere Sessions schreiben im selben Repo mit; beim Push von AIOS v0.6.1 ging ein fremder Commit unbemerkt mit (V0.6, Memo 112).
- Ein Repo im Hub ohne `manifest.yaml` ist kein Paket; `aios --fetch` meldet es als ungültig.
- Ein Hub auf GitHub ist am besten eine Organisation; ein persönlicher Account lässt sich nicht umwandeln (V0.4, Memo 28).
