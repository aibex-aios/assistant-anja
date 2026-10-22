# Praxis — Getaggte Stände

Quellen: Spec v0.4, 06 *Pakete*, *Paket finden*, *Holen*. AA-AIbex-AIOS, V0.4, Memos 44 (X6), 61, 62 (G2), 68, 70, 71.

| # | Regel | Beispiel |
|---|---|---|
| T1 | Eine Version ist ein Tag `v<version>` im Repo des Pakets; `version` im Manifest des getaggten Stands muss gleich sein | Tag `v0.2.1`, `version: 0.2.1` |
| T2 | Nur Tags der Form `v<SemVer>` zählen | `gaertner-v0.1.0` im Code-Repo ist kein Paket-Tag |
| T3 | Geholt wird immer ein getaggter Stand, auch mit `--from <repo>`; was nicht getaggt ist, gibt es für AIOS nicht | Probe eines Entwurfs braucht einen lokalen Tag |
| T4 | Ein **gepushter** Tag wird nie bewegt, gelöscht oder überschrieben; jede Änderung ist eine neue Version, auch nur am README | Taschenrechner 0.4.1 nur für das README |
| T5 | Ein **lokaler**, nicht gepushter Tag darf nachgezogen werden, solange niemand ihn geholt hat | `v0.4.0` des Kernels bis zur Abnahme lokal nachgezogen |
| T6 | Ältere Versionen bleiben im Hub; wer sie gebunden hat, behält sie bis `--upgrade` | `app-taschenrechner` 0.1.0 bis 0.4.2 |
| T7 | Ablauf einer neuen Version: Inhalt ändern, `version` in Manifest und Elementen erhöhen, committen, taggen, Zweig und Tag pushen | Demo-Assistenten 0.2.1; `v0.2.0` bleibt |

## Zu beachten

- **Warum T4:** `lock.yaml` hält Tag **und** Commit fest; ein bewegter Tag passt nicht mehr zum Lock, und der Cache anderer User enthält einen anderen Stand als der Hub.
- **Nachgezogener Tag und Cache:** AIOS v0.4.0 legt geholte Stände je Version in einen Cache unter `~/.aios/packages/` (bei `--from` unter `_from/<paket>/<version>/`) und nimmt ihn wieder, auch wenn der lokale Tag inzwischen auf einen anderen Commit zeigt; `--upgrade` und der Abgleich sehen keine Änderung. Nach dem Nachziehen also im Testprojekt `aios --fetch --remove <paket>`, den Cache-Eintrag dieser Version löschen und neu holen; danach `commit` in `lock.yaml` prüfen.
- Der Push eines Tags ist ein Schritt nach außen und braucht eine eigene Rückfrage (Praxis *Rückfragen*).
