# Praxis — Kernel, Distributionen und Tutorials

Quellen: Spec v0.5, 01 *Begriffe*; 04 *`aios --install distribution-<name>`*; 06 *Pakete*, *`manifest.yaml`*, *Resolver*, *Distributionen*; 03 *Distributionen — `/aios-distribution`*. AA-AIbex-AIOS, Memos 05, 06; V0.4, Memos 04, 07, 46, 61, 62, 75, 76; V0.5, Memo 08.

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

Eine Distribution stellt eine **geprüfte Zusammenstellung** zusammen: optional einen Kernel und Pakete in exakten Versionen (Spec 06, *Distributionen*; V0.5, Memos 25–27, 34).

```yaml
name: distribution-rothirsch
version: 1.0.0
type: distribution
description: Rothirsch — AIOS mit Video-Analyse und der Assistentin Anja
requires:
  aios: ">=0.5,<0.6"
kernel: "==0.5.0"
depends:
  skill-video-analyse: "==0.2.0"
  assistant-anja: "==0.2.0"
```

| # | Regel |
|---|---|
| D1 | Kein `contents`; alles steht in `depends`, Abhängigkeiten der Pakete (z. B. `worker-yt-dlp`) holt der Resolver |
| D2 | **Exakte Versionen** (`==`) in `kernel:` und `depends`; neue Stände sind eine neue Version der Distribution, unabhängig von der Version des Kernels |
| D3 | Name `distribution-<name>`, der Anzeigename steht in `description` |
| D4 | `kernel:` ist optional; ohne ist die Distribution eine reine Sammlung, und `requires.aios` aller Pakete muss zum gebundenen Kernel passen. Höchstens eine Distribution mit `kernel:` je Vault |
| D5 | Installieren und Aktualisieren: `aios --install distribution-<name> [<vault>] [--from <repo>]` — erst der Rechner (Kernel, Arbeitspferde), dann der Vault (binden, holen, registrieren); ein Plan, ein Ja |
| D6 | Im Vault steht die Distribution in `packages:` der Vault-Root, ihre Pakete in `lock.yaml` mit `required_by`; entfernen mit `aios --fetch --remove distribution-<name>`, übersteuern nur mit `only` |
| D7 | Zusammenstellen mit dem AIOS-Skill `/aios-distribution`: vom erprobten Stand eines Projekts aus, Prüfung mit dem Resolver, lokales Repo; er veröffentlicht nicht |
| D8 | Probe: `aios --install distribution-<name> --from <repo> <leerer Vault>` in einem Test- oder Scratchpad-Ordner, nie im Vault des Users; vor der Veröffentlichung der Pakete über einen lokalen Hub (`file://`) |

## Tutorial

| # | Regel |
|---|---|
| U1 | `type: tutorial`; ohne Skills, Assistenten, Befehle ist es kein Modul und wirkt wie Wissen (`knowledge/`) |
| U2 | Name `tutorial-<name>` |
| U3 | Die Tutorials von v0.4 und v0.5 liegen im Kernel (`doc/tutorials/`), nicht als Pakete; es gibt noch kein Beispielpaket |

## Vorlagen

`distribution` und `tutorial` entstehen aus schlanken Vorlagen (nur `manifest.yaml` und `README.md`, beim Tutorial dazu `knowledge/`), bis es Beispielpakete im Hub gibt.
