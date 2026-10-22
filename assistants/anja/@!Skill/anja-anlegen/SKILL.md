---
name: anja-anlegen
version: 0.1.0
description: >
  Legt ein neues Paket-Repo für AIbex AIOS an, für jeden Typ (app, assistant, skill, knowledge,
  tutorial, distribution, kernel): Typ und Name klären, Ort nach den Vorgaben des Users,
  Vorlage aus einem bestehenden Paket, Manifest, Lizenz, lokaler Commit. Verwenden bei
  "neues Paket", "Paket anlegen", "Modul anlegen", "Repo für … anlegen".
---

# Paket anlegen

Ein Skill der Assistentin Anja. Er legt ein Paket-Repo **lokal** an; nichts geht nach außen.

**Arbeitsweise:** Arbeite mit absoluten Pfaden und `git -C <repo>`, wechsle nie mit `cd`.

## 1. Klären

Frage, was noch offen ist, in einem kleinen Fragepaket mit Empfehlung:

| Punkt | Hilfe |
|---|---|
| Typ | `app`, `assistant`, `skill`, `knowledge`, `tutorial`, `distribution`, `kernel`; Begriffe im Leitfaden |
| Name | `<typ>-<name>`, Element `<name>`, beim Assistenten ein Titel; lies `@@Praxis/namen-und-arten.md` |
| Zweck | ein Satz für `description` |
| AIOS-Version | Standard: die letzte freigegebene Spec, `requires.aios: ">=0.4,<0.5"` |

## 2. Ort und Vorgaben

- Ist die Regel *AIOS-Pakete — Vorgaben* (`name: aios-pakete-vorgaben`) geladen, gilt ihr Ort, ihre Lizenz und ihr Namensschema. Eine andere geladene Regel, die den Ort von Paket-Repos nennt, gilt ebenso.
- Sonst gilt der Default: `<konzeptprojekt>/@Package/<paket>/`, und die `.gitignore` des Konzeptprojekts bekommt `/@Package/`. Sag das und dass die Regel den Ort ändern kann.
- Gibt es den Zielordner schon, brich ab und sag es.

## 3. Vorlage

Nimm ein bestehendes Paket desselben Typs als Vorlage, getaggter Stand, ohne `.git`:

| Typ | Vorlage |
|---|---|
| `assistant` | `assistent-gaertner` (mit Oberfläche und Wissen) oder `assistent-astronom` (schlank) |
| `skill` | `skill-memo` |
| `knowledge` | `knowledge-orion` |
| `app` | `app-taschenrechner` |
| `kernel` | `aibex-aios` |
| `distribution`, `tutorial` | keine; nur `manifest.yaml` und `README.md`, beim Tutorial dazu `knowledge/` (`@@Praxis/kernel-distribution-tutorial.md`) |

Woher: ein lokaler Klon (z. B. `~/git/<owner>/<repo>`, nach den Vorgaben), sonst ein flacher Klon des Tags in ein temporäres Verzeichnis: `git clone --depth 1 --branch v<version> https://github.com/aibex-aios/<repo> <tmp>`.

Übernimm nur den **Aufbau**: Ordner, Frontmatter-Felder, Abschnitte des Rollentexts, `gui.yaml`-Gerüst. Leere die Inhalte und ersetze Namen, Titel, Beschreibung. Übernimm nie `contrib/`, Daten oder Wissen der Vorlage.

## 4. Plan zeigen und fragen

Zeige vor dem Schreiben: Zielordner, Dateien mit Kurzinhalt, `manifest.yaml` vollständig, Lizenzdateien, Eintrag in `.gitignore` (falls Default). Schreibe erst nach Ja (`@@Praxis/rueckfragen.md`).

## 5. Anlegen

1. Ordner anlegen, `git init -b main`.
2. `manifest.yaml` nach `@@Praxis/manifest-und-versionen.md`: `version: 0.1.0`, `contents` passend zu den Ordnern; Elemente in `skills/` und `assistants/` mit `version: 0.1.0`.
3. Lizenz nach den Vorgaben. Bei Apache-2.0: `license: Apache-2.0`, `LICENSE` als unveränderte Kopie (z. B. aus `@!Package/assistant-anja/LICENSE`), `NOTICE` mit Paketname, Copyright-Zeile und, falls vorgegeben, dem Satz zu den Marken. Ohne Vorgabe: Lizenz offen lassen und vor dem Veröffentlichen fragen.
4. `README.md`: Zweck, `aios --fetch <paket>`, Aufruf bzw. Zuordnung, Lizenz.
5. Beim Default: `/@Package/` in die `.gitignore` des Konzeptprojekts eintragen und dort nur diese Zeile committen.
6. Im Paket-Repo committen: „<paket> 0.1.0: angelegt aus <vorlage>". **Kein Tag**; getaggt wird erst zur Probe.

## 6. Melden

Nenne Ort, Dateien und den nächsten Schritt: Inhalte schreiben, dann `/anja-pruefen`.
