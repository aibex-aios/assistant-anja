# Praxis — Manifest und Versionen

Quellen: Spec v0.4, 03 *Format eines Skills*, *Versionen*, *Assistenten*; 06 *`manifest.yaml`*, *Prüfung beim Holen*, *Versionen und Bereiche*. AA-AIbex-AIOS, V0.4, Memos 19 (L5), 44 (X1), 70. Pakete im Hub `aibex-aios`.

## Manifest

```yaml
name: app-taschenrechner
version: 0.4.2
type: app
description: Programmierbarer RPN-Taschenrechner nach dem Vorbild des HP-15C mit lernenden Funktionstasten (Demo-App von AIbex AIOS)
requires:
  aios: ">=0.4,<0.5"
depends:
  skill-memo: "~=6.0"
contents:
  skills: [taschenrechner, taschenrechner-gui]
  knowledge: true
  gui: taschenrechner-gui
license: MIT
```

| # | Regel |
|---|---|
| M1 | Pflicht: `name`, `version`, `type`, `description` (ein Satz), `requires.aios` |
| M2 | `requires.aios: ">=0.4,<0.5"` für Pakete, die für v0.4 gebaut sind; Vorabkennungen des Kernels zählen nicht (`0.4.0-rc1` gilt als `0.4.0`) |
| M3 | `contents` nennt jedes Element; jeder Name muss als Ordner vorhanden sein, sonst holt `aios --fetch` das Paket nicht. `gui` muss in `skills` stehen; Elementnamen dürfen sich nicht wiederholen |
| M4 | Ein Assistent steht unter `contents.assistants`; seine privaten Skills (`assistants/<name>/@!Skill/`) stehen **nicht** in `contents.skills` |
| M5 | `depends` nur für Pakete, ohne die das Paket nicht läuft; `aios` gehört nach `requires` (Praxis *Abhängigkeiten*) |
| M6 | `license` setzen, wenn Daten Dritter enthalten sind (`knowledge-orion`: CC-BY-4.0); sonst nach den Vorgaben des Users |
| M7 | `contents.hooks` ist in v0.4 ohne Wirkung; `aios --fetch` meldet ihn |

## Versionen

| # | Regel | Beispiel |
|---|---|---|
| V1 | SemVer `MAJOR.MINOR.PATCH`; ein neues Paket beginnt mit `0.1.0` | `knowledge-orion` 0.1.0 |
| V2 | Jedes `SKILL.md` und `ASSISTANT.md` braucht eine gültige `version`, sonst wird das Element nicht registriert bzw. aufgelöst | — |
| V3 | Die Elemente in `skills/` und `assistants/` tragen die **Version des Pakets** (Konvention von AIbex; die Spec verlangt es nicht) | `assistent-gaertner` 0.2.1 → `ASSISTANT.md` 0.2.1 |
| V4 | **Private Skills** eines Assistenten behalten ihre eigene Version und steigen nur bei eigener Änderung | `gaertner-gui` 0.1.0 in `assistent-gaertner` 0.2.1 |
| V5 | Vor 1.0 darf jede Minor-Version brechen: Korrektur = Patch, neue Funktion oder Bruch = Minor | Taschenrechner 0.3.2 → 0.4.0 (Funktionstasten statt Kacheln) |
| V6 | Ohne Bereich geholt gilt unter 1.0 `~=0.Y.Z` (nur Patches derselben Minor-Version), ab 1.0 `~=X.Y` | `app-taschenrechner` 0.1.0 → `>=0.1.0,<0.2.0` |
| V7 | Jede Änderung am Inhalt, auch ein Satz im Rollentext, ist eine neue Version | Astronom 0.1.0 → 0.2.0 für einen Satz (V0.4, Memo 27) |
