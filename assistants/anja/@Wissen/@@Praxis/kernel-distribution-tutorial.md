# Praxis — Kernel, Distributionen und Tutorials

Quellen: Spec v0.4, 01 *Begriffe*; 04 (Installation); 06 *Pakete*, *`manifest.yaml`*, *Resolver*. AA-AIbex-AIOS, Memos 05, 06; V0.4, Memos 04, 07, 46, 61, 62, 75, 76; V0.5, Memo 08.

## Kernel

| # | Regel |
|---|---|
| K1 | Name `aios`, `type: kernel`; eine Variante unterscheidet sich durch Hub bzw. Repo, nicht durch den Namen |
| K2 | Wird mit `aios --install` installiert, nicht geholt |
| K3 | Topic `aios-core`, nicht `aios-package`, und kein Eintrag in `aios-index`; so listet `aios --library` ihn nicht |
| K4 | Code-Repo mit Code, Tests, Spec, Doku; Konzept und Gründe in einem eigenen Konzept-Repo (bei AIbex `aibex-aios/aibex-aios` und `aibex-aios/AA-AIbex-AIOS`) |
| K5 | Release: `VERSION` und `manifest.yaml`, Specs von *Entwurf* auf *Spec*, Tests und Live-Tests grün, Tag zuerst **lokal**; Abnahme auf dem Arbeitsrechner nach dem Abnahmetest der Spec, bis dahin wird der lokale Tag nachgezogen; danach Tag pushen und gleichnamigen Tag im Konzept-Repo auf dem Abnahme-Memo |
| K6 | Vorlage für einen neuen Kernel: das Code-Repo `aibex-aios/aibex-aios` |

## Distribution

Eine Distribution **listet nur andere Pakete mit Versionen auf**; sie ist kein Modul.

```yaml
name: distribution-demo
version: 0.1.0
type: distribution
description: Demo-Ausstattung von AIOS mit Taschenrechner und Astronom
requires:
  aios: ">=0.4,<0.5"
depends:
  app-taschenrechner: "~=0.4.2"
  assistent-astronom: "~=0.2.1"
  knowledge-orion: "~=0.1.0"
```

| # | Regel |
|---|---|
| D1 | Kein `contents`; alles steht in `depends`. Der Resolver holt die Pakete in dasselbe Projekt und rollt sie ganz aus |
| D2 | Bereiche dürfen enger sein als sonst (`==`), weil eine Distribution eine geprüfte Zusammenstellung festlegt (Konvention von AIbex) |
| D3 | Name `distribution-<name>` |

**Lücke in Spec v0.4:** Sie sagt nicht ausdrücklich, wie eine Distribution in `packages:` und `lock.yaml` erscheint und was `--remove` mit ihren Paketen tut (nach den allgemeinen Regeln: entfernt, wenn kein anderes Paket sie verlangt). Sag das, wenn danach gefragt wird (V0.5, Memo 08, Wunsch).

## Tutorial

| # | Regel |
|---|---|
| U1 | `type: tutorial`; ohne Skills, Assistenten, Befehle ist es kein Modul und wirkt wie Wissen (`knowledge/`) |
| U2 | Name `tutorial-<name>` |
| U3 | Die Tutorials von v0.4 liegen im Kernel (`doc/tutorials/`), nicht als Pakete; es gibt noch kein Beispielpaket |

## Vorlagen

`distribution` und `tutorial` entstehen aus schlanken Vorlagen (nur `manifest.yaml` und `README.md`, beim Tutorial dazu `knowledge/`), bis es Beispielpakete im Hub gibt.
