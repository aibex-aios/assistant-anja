# Praxis — Kernel, Distributionen und Tutorials

Quellen: Spec v0.6.1, 01 *Begriffe*, *Abnahmetest*; 03 *Kernel-Skills im Vault*, *Distributionen — `/aios-distribution`*; 04 *Installationen*, *`aios --install distribution-<name>`*; 06 *Pakete*, *`manifest.yaml`*, *Versionen und Bereiche*, *Resolver*, *Distributionen*. AA-AIbex-AIOS, Memos 05, 06; V0.4, Memos 04, 07, 46, 61, 62, 75, 76; V0.5, Memo 08; V0.6, Memos 82, 83.

## Kernel

| # | Regel |
|---|---|
| K1 | Name `aios`, `type: kernel`; eine Variante unterscheidet sich durch Hub bzw. Repo, nicht durch den Namen |
| K2 | Wird mit `aios --install` installiert, nicht geholt; Standard ist `~/.aios/versions/v<version>/`, mit `--system` `/opt/aios/v<version>/`. Gebunden wird ein Vault an der Vault-Root mit `aios --activate` |
| K2a | Die Kernel-Skills `aios-*` und der Alias `gui` werden im A/W als dünne Hüllen an der Vault-Root und in jedem Projekt registriert und stehen im Block `<aios-kernel-skills>` des Master-Kontexts; global registriert AIOS seit v0.6 nichts |
| K3 | Topic `aios-core`, nicht `aios-package`, und kein Eintrag in `aios-index`; so listet `aios --library` ihn nicht |
| K4 | Code-Repo mit Code, Tests, Spec, Doku; Konzept und Gründe in einem eigenen Konzept-Repo (bei AIbex `aibex-aios/aibex-aios` und `aibex-aios/AA-AIbex-AIOS`) |
| K5 | Release: `VERSION` und `manifest.yaml`, Specs von *Entwurf* auf *Spec*, Tests und Live-Tests grün; Abnahme auf dem Arbeitsrechner nach dem Abnahmetest der Spec auf Release-Kandidaten `v<x.y.z>-rc<n>` (je Befund ein neuer, Distributionen mit derselben Nummer); vorher ein voller Bestandslauf (Workflow, Phase 8); danach `v<x.y.z>` taggen, Begleitpakete vorher oder mit veröffentlichen, Tag pushen und gleichnamigen Tag im Konzept-Repo auf dem Abnahme-Memo |
| K6 | Vorlage für einen neuen Kernel: das Code-Repo `aibex-aios/aibex-aios` |

## Distribution

Eine Distribution stellt eine **geprüfte Zusammenstellung** zusammen: optional einen Kernel und Pakete in exakten Versionen (Spec 06, *Distributionen*; V0.5, Memos 25–27, 34).

```yaml
name: distribution-rothirsch
version: 1.1.0
type: distribution
description: "Rothirsch — AIOS mit Video-Analyse und der Assistentin Anja"
license: Apache-2.0
requires:
  aios: ">=0.6,<0.7"
kernel: "==0.6.1"
depends:
  skill-video-analyse: "==0.2.1"
  assistant-anja: "==0.2.1"
```

| # | Regel |
|---|---|
| D1 | Kein `contents`; alles steht in `depends`, Abhängigkeiten der Pakete (z. B. `worker-yt-dlp`) holt der Resolver |
| D2 | **Exakte Versionen** (`==`) in `kernel:` und `depends`; neue Stände sind eine neue Version der Distribution, unabhängig von der Version des Kernels |
| D3 | Name `distribution-<name>`, der Anzeigename steht in `description` |
| D4 | `kernel:` ist optional; ohne ist die Distribution eine reine Sammlung, und `requires.aios` aller Pakete muss zum gebundenen Kernel passen. Höchstens eine Distribution mit `kernel:` je Vault |
| D5 | Installieren und Aktualisieren: `aios --install distribution-<name> [<vault>] [--from <repo>]` — erst der Rechner (Kernel, Arbeitspferde), dann der Vault (binden, holen, registrieren); ein Plan, ein Ja |
| D6 | Im Vault steht die Distribution in `packages:` der Vault-Root, ihre Pakete in `lock.yaml` mit `required_by`; entfernen mit `aios --fetch --remove distribution-<name>`, übersteuern nur mit `only` |
| D7 | Zusammenstellen mit dem Kernel-Skill `/aios-distribution`: vom erprobten Stand eines Projekts aus, Prüfung mit dem Resolver, lokales Repo; er veröffentlicht nicht |
| D8 | Probe: `aios --install "distribution-<name>==<x.y.z>-rc<n>" <leerer Vault> --from <repo>` in einem Test- oder Scratchpad-Ordner, nie im Vault des Users; vor der Veröffentlichung der Pakete über einen lokalen Hub (`file://`) |
| D9 | **Vorabversionen:** `==` nimmt eine Vorabversion nur an, wenn es sie nennt. Zur Abnahme eines Kandidaten des Kernels gibt es Testversionen der Distribution mit Vorabversion (`1.1.0-rc1` mit `kernel: "==0.6.1-rc1"`), nur lokal getaggt; die endgültige Version nennt den endgültigen Kernel |
| D10 | Gepflegt werden die Distributionen des Hubs `aibex-aios` in eigenen Projekten des Vaults `§AIOS` (`D-Distribution/DC-Capricorn`, `D-Distribution/DR-Rothirsch`) |

## Tutorial

| # | Regel |
|---|---|
| U1 | `type: tutorial`; ohne Skills, Assistenten, Befehle ist es kein Modul und wirkt wie Wissen (`knowledge/`) |
| U2 | Name `tutorial-<name>` |
| U3 | Die Tutorials liegen im Kernel (`doc/tutorials/`, installiert unter `~/.aios/versions/v<version>/doc/tutorials/`), nicht als Pakete; es gibt noch kein Beispielpaket |

## Vorlagen

`distribution` und `tutorial` entstehen aus schlanken Vorlagen (nur `manifest.yaml` und `README.md`, beim Tutorial dazu `knowledge/`), bis es Beispielpakete im Hub gibt.
