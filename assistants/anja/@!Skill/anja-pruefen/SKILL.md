---
name: anja-pruefen
version: 0.1.0
description: >
  Prüft ein Paket-Repo von AIbex AIOS gegen die Spec und die Praxis: Manifest, Namen,
  contents gegen die Ordner, Versionen, Frontmatter von Skills und Assistenten, Wissen,
  Oberflächen, Rückfragen in Skills, Abhängigkeiten, Lizenz, Inhalt ohne Notizen. Schreibt
  nichts. Verwenden bei "Paket prüfen", "prüf das Manifest", "ist das Paket fertig?".
---

# Paket prüfen

Ein Skill der Assistentin Anja. Er **liest nur** und berichtet; Korrekturen schlägt er vor und macht sie erst nach Ja.

**Arbeitsweise:** Arbeite mit absoluten Pfaden und `git -C <repo>`, wechsle nie mit `cd`.

## 1. Was geprüft wird

Das Paket-Repo, das der User nennt, sonst das zuletzt besprochene oder angelegte. Maßstab ist die Spec der AIOS-Version aus `requires.aios` (die letzte freigegebene im Bereich). Lies dazu Spec 06 *`manifest.yaml`* und *Prüfung beim Holen*, bei Assistenten und Skills Spec 03.

## 2. Prüfliste

Lies vor jedem Block die genannte Praxis.

| Block | Prüfe | Praxis |
|---|---|---|
| Manifest | Pflichtfelder; `type` bekannt; `description` ein Satz; `requires.aios` gesetzt; `aios` nicht in `depends` | `manifest-und-versionen.md` |
| Namen | `name` = Repo-Ordner, Muster `<typ>-<name>`, keine verbotenen Namen; `name` im Frontmatter = Verzeichnisname | `namen-und-arten.md` |
| `contents` | jeder Name als Ordner vorhanden; jeder Ordner in `skills/`, `assistants/`, `commands/` genannt; `gui` in `skills`; keine doppelten Elementnamen; private Skills nicht in `contents.skills` | `manifest-und-versionen.md` |
| Versionen | gültiges SemVer überall; Manifest = Elemente in `skills/` und `assistants/`; private Skills mit eigener Version; letzter Tag (`git -C <repo> tag`) kleiner als die Version im Manifest, sonst ist eine neue Version fällig | `manifest-und-versionen.md`, `getaggte-staende.md` |
| Assistent | Frontmatter vollständig; jeder Name in `skills` auflösbar (im Assistentenordner, im Paket oder als `depends`); Rollentext mit Personalität, Handwerk, Grenzen; Wissen mit Klassen und Inhaltsverzeichnis | `inhalt-eines-assistenten.md`, `grenzen-und-ehrlichkeit.md` |
| Skills | jeder schreibende Skill beschreibt Plan → Rückfrage → Ausführen; kein „ohne Rückfrage" beim bloßen Wunsch | `rueckfragen.md` |
| Daten | geschrieben wird nur nach `@Data/<paket>/`, nie ins Paket | `daten-einer-app.md` |
| Oberfläche | `gui.yaml` gültig (1–12 Kacheln, je genau ein Ziel); kein Text mit `/` am Anfang; HTML-Teile ohne Inline-Handler; Ausweg im Chat für jede Aktion | `oberflaechen.md` |
| Abhängigkeiten | nötig, mit `~=`-Bereich, im Ziel-Hub vorhanden (`aios --library <paket>`, nur lesend) | `abhaengigkeiten.md` |
| Lizenz | nach den Vorgaben; bei Apache-2.0 `LICENSE` und `NOTICE` vorhanden | Leitfaden, *Vorgaben* |
| Inhalt | keine Memos, Notizen, Testdaten, `.DS_Store`, Geheimnisse; `README.md` vorhanden; Arbeitsbaum committet (`git -C <repo> status`) | Leitfaden |

## 3. Bericht

Eine Tabelle: Block, Ergebnis (`ok` oder Befund), Fundstelle (Datei, Zeile), Quelle (Spec-Abschnitt oder Praxis). Danach die Vorschläge zur Korrektur, nummeriert. Ändere nichts ohne Ja.

Sag am Ende, was diese Prüfung **nicht** abdeckt: die Wirkung im Projekt. Die zeigt erst die Probe (`@@Praxis/probe-vor-veroeffentlichung.md`): lokal taggen, mit `aios --fetch <paket> --from <repo>` in ein leeres Testprojekt holen, im nächsten Chat ausprobieren.
