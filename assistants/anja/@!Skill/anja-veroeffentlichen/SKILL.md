---
name: anja-veroeffentlichen
version: 0.1.0
description: >
  Veröffentlicht ein geprüftes und erprobtes Paket von AIbex AIOS in einem Hub auf GitHub,
  Schritt für Schritt mit eigener Rückfrage: Repo anlegen, Zweig und Tag pushen, Topic,
  Index, Beschreibung, Probe gegen den Hub, Tag im Konzept-Repo. Verwenden bei
  "Paket veröffentlichen", "in den Hub", "neue Version veröffentlichen", "release".
---

# Paket veröffentlichen

Ein Skill der Assistentin Anja. **Jeder Schritt wirkt nach außen** und braucht eine eigene Rückfrage, auch wenn der User „veröffentliche" gesagt hat. Lies zuerst `@@Praxis/veroeffentlichen.md` und `@@Praxis/getaggte-staende.md`.

**Arbeitsweise:** Arbeite mit absoluten Pfaden und `git -C <repo>`, wechsle nie mit `cd`.

## 1. Voraussetzungen

Prüfe und berichte, bevor du etwas vorschlägst:

- `/anja-pruefen` ohne offene Befunde; Arbeitsbaum committet.
- Probe bestanden (`@@Praxis/probe-vor-veroeffentlichung.md`); fehlt sie, sag das und empfiehl sie.
- Lokaler Tag `v<version>` gleich `version` im Manifest und auf dem letzten Commit; sonst Tag anlegen bzw. nachziehen (nur solange er nicht gepusht ist).
- `gh auth status` angemeldet; Schreibrecht im Ziel-Hub (`gh api orgs/<owner>` bzw. `gh api repos/<owner>/<paket>` mit `permissions.push`).
- Hub, Owner, Sichtbarkeit und Lizenz aus der Regel *AIOS-Pakete — Vorgaben*; fehlt etwas, frage und biete an, die Regel zu ergänzen.

## 2. Plan

Zeige alle Schritte auf einmal als nummerierte Liste mit den Befehlen. Führe sie dann **einzeln** aus, jeden nach eigenem Ja:

| # | Schritt | Befehl |
|---|---|---|
| 1 | Repo anlegen (nur bei der ersten Version) | `gh repo create <owner>/<paket> --public\|--private --source <repo> --remote origin` |
| 2 | Zweig pushen | `git -C <repo> push -u origin main` |
| 3 | Tag pushen; danach ist er endgültig | `git -C <repo> push origin v<version>` |
| 4 | Topic (beim Kernel `aios-core`) | `gh repo edit <owner>/<paket> --add-topic aios-package` |
| 5 | Beschreibung | `gh repo edit <owner>/<paket> --description "<description>"` |
| 6 | Index, falls der Hub `aios-index` hat und das Paket neu ist oder sich `description` geändert hat | Klon von `<owner>/aios-index`, Eintrag in `index.yaml`, Commit, Push |
| 7 | Probe gegen den Hub in einem frischen Testprojekt | `aios --library <paket>`, `aios --fetch <paket> --to <testprojekt>` |
| 8 | Tag im Konzept-Repo auf dem Memo der Veröffentlichung, annotiert mit Verweis auf den Commit im Paket-Repo; pushen | `git -C <konzept> tag -a <paket>-v<version> -m "…"`, `git -C <konzept> push origin <tag>` |

Bei einer **neuen Version** eines schon veröffentlichten Pakets entfallen 1 und 4.

Lehnt der User einen Schritt ab, halte an und sag, welcher Stand jetzt draußen ist. Schlägt ein Schritt fehl, halte ebenfalls an; einen gepushten Tag bewegst du nie (`@@Praxis/getaggte-staende.md`, T4).

## 3. Abschluss

Berichte: Repo-URL, Tag, Topic, Index, Ergebnis der Probe. Schlage ein Memo im Konzeptprojekt vor, das die Veröffentlichung festhält.
