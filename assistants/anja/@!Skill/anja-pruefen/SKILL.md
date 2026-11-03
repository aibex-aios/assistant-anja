---
name: anja-pruefen
version: 0.3.0
description: >
  Prüft ein Paket-Repo von AIbex AIOS gegen die Spec und die Praxis: Manifest, Namen,
  contents gegen die Ordner, Versionen, Frontmatter von Skills und Assistenten, Wissen,
  Oberflächen, Rückfragen in Skills, Abhängigkeiten, Lizenz, Inhalt ohne Notizen. Schreibt
  nichts. Verwenden bei "Paket prüfen", "prüf das Manifest", "ist das Paket fertig?".
---

# Paket prüfen

Ein Skill der Assistentin Anja. Er **liest nur** und berichtet; Korrekturen schlägt er vor und macht sie erst nach Ja.

**Arbeitsweise:** Arbeite mit absoluten Pfaden und `git -C <repo>`, wechsle nie mit `cd`. Rufe `aios` über den Weiterleiter auf: mit dem absoluten Pfad aus dem Block `<aios-kernel-skills>` deines Master-Kontexts, als einzelnen Befehl ohne `cd`, `;`, `&&`, `|` oder Umleitung.

## 1. Was geprüft wird

Das Paket-Repo, das der User nennt, sonst das zuletzt besprochene oder angelegte. Es gibt zwei Maßstäbe, in dieser Reihenfolge:

1. **AIOS:** die Spec der AIOS-Version aus `requires.aios` (der höchste Tag im Bereich) und deine Praxis. Lies dazu Spec 06 *`manifest.yaml`* und *Prüfung beim Holen*, bei Assistenten und Skills Spec 03.
2. **Paket:** die Spezifikation des Pakets im Konzeptprojekt (`@Spec/<paket>/`, sonst `@Spec/`), falls es eine gibt. Prüfe, ob das Paket die dort genannten Elemente, das Verhalten und die Grenzen hat und ob ein Abnahmetest vorliegt. Gibt es keine Spezifikation, sag das und nenne die Phase des Workflows.

## 2. Prüfliste

Lies vor jedem Block die genannte Praxis.

| Block | Prüfe | Praxis |
|---|---|---|
| Manifest | Pflichtfelder; `type` bekannt; `description` ein Satz; `requires.aios` gesetzt und nach M2 (neue Pakete `">=0.6,<0.7"`, bestehende mit Obergrenze `<0.7`); `aios` nicht in `depends`; kein `workers:` | `manifest-und-versionen.md` |
| Arbeitspferd | nur bei `type: worker`: `worker:` mit `kind` (`python`, `script`), mindestens ein Programm in `programs`, `check` empfohlen; kein `contents`; bei `python` die Datei aus `requirements` mit jedem Eintrag `paket==version` und `--hash=sha256:…`; bei `script` `setup` und `remove` vorhanden, Programme nach `$AIOS_WORKER_DIR/bin/`; `requires.aios` mit Obergrenze `<0.7` (neu `">=0.6,<0.7"`) | `arbeitspferde.md` |
| Distribution | nur bei `type: distribution`: `kernel:` (falls vorhanden) und alle `depends` mit `==`; kein `contents` | `kernel-distribution-tutorial.md` |
| Namen | `name` = Repo-Ordner, Muster `<typ>-<name>`, keine verbotenen Namen; `name` im Frontmatter = Verzeichnisname | `namen-und-arten.md` |
| `contents` | jeder Name als Ordner vorhanden; jeder Ordner in `skills/`, `assistants/`, `commands/` genannt; `gui` in `skills`; keine doppelten Elementnamen; private Skills nicht in `contents.skills` | `manifest-und-versionen.md` |
| Versionen | gültiges SemVer überall; Manifest = Elemente in `skills/` und `assistants/`; private Skills mit eigener Version; letzter Tag (`git -C <repo> tag`) kleiner als die Version im Manifest, sonst ist eine neue Version fällig; Tags nur `v<SemVer>`, Kandidaten als `-rc<n>`, kein Tag zeigt auf einen anderen Commit als beim Holen (`other commit`) | `manifest-und-versionen.md`, `getaggte-staende.md` |
| Assistent | Frontmatter vollständig; jeder Name in `skills` auflösbar (im Assistentenordner, im Paket oder als `depends`); Rollentext mit Personalität, Handwerk, Grenzen; Wissen mit Klassen und Inhaltsverzeichnis | `inhalt-eines-assistenten.md`, `grenzen-und-ehrlichkeit.md` |
| Skills | jeder schreibende Skill beschreibt Plan → Rückfrage → Ausführen; kein „ohne Rückfrage" beim bloßen Wunsch. Jeder Skill, der `aios` aufruft, trägt den Satz zum Aufruf über den Weiterleiter (R9); fehlt er, ist das ein Befund. Ein Memo-Skill ohne Rückfrage ist kein Befund, wenn die Spec des Pakets ihn als Grenze nennt (R8); berichte ihn als „Ausnahme laut Paket-Spec" | `rueckfragen.md` |
| Daten | geschrieben wird nur nach `@Data/<paket>/`, nie ins Paket | `daten-einer-app.md` |
| Oberfläche | `gui.yaml` gültig (1–12 Kacheln, je genau ein Ziel); kein Text mit `/` am Anfang; HTML-Teile ohne Inline-Handler; Ausweg im Chat für jede Aktion | `oberflaechen.md` |
| Abhängigkeiten | nötig, mit `~=`-Bereich (bei Distributionen `==`), im Ziel-Hub vorhanden (`aios --library <paket>`, nur lesend); braucht ein Skill ein Programm, steht das `worker`-Paket in `depends` und der Skill ruft `~/.aios/bin/<programm>` statt des `PATH`, ohne Installationsanweisung im Chat | `abhaengigkeiten.md`, `arbeitspferde.md` |
| Lizenz | nach den Vorgaben; bei Apache-2.0 `LICENSE` und `NOTICE` vorhanden | Leitfaden, *Vorgaben* |
| Inhalt | keine Memos, Notizen, Testdaten, `.DS_Store`, Geheimnisse; `README.md` vorhanden; Arbeitsbaum committet (`git -C <repo> status`) | Leitfaden |
| Paket-Spec | Elemente, Verhalten, Grenzen und Lizenz wie in der Spezifikation des Pakets; Abnahmetest vorhanden | Spezifikation des Pakets |

## 3. Bericht

Eine Tabelle: Block, Ergebnis (`ok` oder Befund), Fundstelle (Datei, Zeile), **Maßstab** (AIOS oder Paket-Spec) mit Quelle (Spec-Abschnitt oder Praxis). Danach die Vorschläge zur Korrektur, nummeriert. Ändere nichts ohne Ja.

Sag am Ende, was diese Prüfung **nicht** abdeckt: die Wirkung im Projekt. Die zeigen erst Probe und Abnahme (`@@Praxis/probe-vor-veroeffentlichung.md`): Release-Kandidat taggen, mit `aios --fetch "<paket>==<x.y.z>-rc<n>" --from <repo>` in ein leeres Testprojekt holen (dort oder mit `--to`), im nächsten Chat ausprobieren.
