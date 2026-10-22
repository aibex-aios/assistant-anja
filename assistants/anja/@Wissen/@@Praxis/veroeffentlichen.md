# Praxis — Veröffentlichen

Quellen: Spec v0.4, 06 *Hubs*, *Index und Suche*. AA-AIbex-AIOS, Memo 04 (Tags im Konzept-Repo); V0.4, Memos 28, 45, 46, 61, 62, 76.

Jeder Schritt ist nach außen wirksam und bekommt eine **eigene Rückfrage**.

| # | Schritt | Wie |
|---|---|---|
| V1 | Probe bestanden, Stand committet, `version` in Manifest und Elementen gleich dem Tag | `git -C <repo> status`, Manifest lesen |
| V2 | Hub, Owner, Sichtbarkeit aus den Vorgaben des Users; sonst fragen. Öffentlich heißt: `aios --fetch` braucht keine Anmeldung | Regel *AIOS-Pakete — Vorgaben* |
| V3 | Repo im Hub anlegen, Name gleich dem Paketnamen | `gh repo create <owner>/<paket> --public --source <repo>` |
| V4 | Zweig und Tag pushen | `git -C <repo> push -u origin main`, `git -C <repo> push origin v<x.y.z>` |
| V5 | Topic **`aios-package`** setzen (beim Kernel `aios-core`) | `gh repo edit <owner>/<paket> --add-topic aios-package` |
| V6 | Eintrag in `aios-index` des Hubs (`index.yaml`: `name`, `type`, `description`), falls der Hub einen Index hat | Commit und Push in `<owner>/aios-index` |
| V7 | Beschreibung des Repos setzen (ein Satz, wie `description`) | `gh repo edit <owner>/<paket> --description "…"` |
| V8 | Probe gegen den echten Hub in einem frischen Testprojekt | `aios --library <paket>`, `aios --fetch <paket>` |
| V9 | Tag im Konzept-Repo auf dem Memo der Veröffentlichung, mit Verweis auf den Commit im Paket-Repo; pushen | annotierter Tag |
| V10 | Ergebnis als Memo im Konzeptprojekt | — |

## Zu beachten

- Ab dem Push ist der Tag endgültig. Jede spätere Änderung, auch am README, ist eine neue Version: committen, taggen, V4, gegebenenfalls V6, V8, V9.
- Ein Repo im Hub ohne `manifest.yaml` ist kein Paket; `aios --fetch` meldet es als ungültig.
- Ein Hub auf GitHub ist am besten eine Organisation; ein persönlicher Account lässt sich nicht umwandeln (V0.4, Memo 28).
