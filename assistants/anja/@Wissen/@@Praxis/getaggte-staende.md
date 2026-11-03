# Praxis — Getaggte Stände

Quellen: Spec v0.6.1, 01 *Abnahmetest* (Release-Kandidaten); 06 *Pakete*, *Paket finden*, *Holen* (Schritte 3, 4), *Versionen und Bereiche*. AA-AIbex-AIOS, V0.4, Memos 44 (X6), 61, 62 (G2), 68, 70, 71; V0.6, Memos 50 (F62), 77 (R6), 82. MAA-Anja-AIOS-Expert, Memo 78 (F23).

| # | Regel | Beispiel |
|---|---|---|
| T1 | Eine Version ist ein Tag `v<version>` im Repo des Pakets; `version` im Manifest des getaggten Stands muss gleich sein | Tag `v0.2.1`, `version: 0.2.1` |
| T2 | Nur Tags der Form `v<SemVer>` zählen, auch mit Vorabkennung | `v0.3.0-rc1`; `gaertner-v0.1.0` im Code-Repo ist kein Paket-Tag |
| T3 | Geholt wird immer ein getaggter Stand, auch mit `--from <repo>`; was nicht getaggt ist, gibt es für AIOS nicht | Probe eines Entwurfs braucht einen Release-Kandidaten |
| T4 | **Kein Tag wird verschoben**, gelöscht oder überschrieben, auch kein lokaler; jede Änderung ist ein neuer Tag | Taschenrechner 0.4.1 nur für das README |
| T5 | **Probe und Abnahme** laufen auf Release-Kandidaten `v<x.y.z>-rc<n>`; je Befund ein neuer Kandidat `-rc<n+1>`. Ein Kandidat ist ein **eigener Commit**, der `version` in `manifest.yaml` und in den Elementen in `skills/` und `assistants/` auf `<x.y.z>-rc<n>` setzt (private Skills behalten ihre Version); sonst bricht `aios --fetch` ab („tag … has version … in manifest.yaml"). `v<x.y.z>` kommt erst nach der Abnahme, auf einem Commit, der nur diese Versionen auf `<x.y.z>` setzt | AIOS v0.6.1: `rc1`–`rc4`, dann `v0.6.1`; `distribution-rothirsch` `v1.1.0-rc4` mit `version: 1.1.0-rc4` |
| T6 | Einen Kandidaten holt nur ein Bereich, der ihn nennt: `"<paket>==<x.y.z>-rc<n>"`; ohne Bereich wählt AIOS die höchste Release | `aios --fetch "assistant-anja==0.3.0-rc1" --from <repo>` |
| T7 | Ältere Versionen bleiben im Hub; wer sie gebunden hat, behält sie bis `--upgrade` | `app-taschenrechner` 0.1.0 bis 0.5.1 |
| T8 | Ablauf einer neuen Version: Inhalt ändern und committen; Commit mit `version: <x.y.z>-rc1`, Tag `v<x.y.z>-rc1`; Probe und Abnahme (bei Befunden Korrektur, Commit mit `-rc<n+1>`, Tag); nach der Abnahme Commit mit `version: <x.y.z>`, Tag `v<x.y.z>`; Zweig und Tag pushen | Anja 0.3.0 (`rc1` unbrauchbar ohne rc-Version, MAA, Memo 93: B10) |

## Zu beachten

- **Warum T4:** `lock.yaml` hält Tag **und** Commit fest; ein bewegter Tag passt nicht mehr zum Lock, und der Cache anderer User enthält einen anderen Stand als der Hub.
- **Cache:** AIOS legt geholte Stände je Version unter `~/.aios/packages/` ab, bei `--from` getrennt nach Quelle (`_from/<12 Zeichen SHA-256 der Quelle>/<paket>/<version>/`). Hat dieselbe Version einen anderen Commit (andere Quelle oder verschobener Tag), zeigt die Vorschau `other commit`. Mit Release-Kandidaten kommt das nicht vor; ein Cache-Eintrag muss nicht mehr gelöscht werden.
- Der Push eines Tags ist ein Schritt nach außen und braucht eine eigene Rückfrage (Praxis *Rückfragen*).
