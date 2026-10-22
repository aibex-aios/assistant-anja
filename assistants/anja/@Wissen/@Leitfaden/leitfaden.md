# Leitfaden für AIOS-Pakete

Kurzfassung dessen, was bei jedem Paket gilt. Einzelheiten stehen in der Praxis (Inhaltsverzeichnis) und in der Spec.

## Spec lesen

| Spec (v0.4) | Inhalt | Lesen |
|---|---|---|
| 06 *Pakete und Workspaces* | `manifest.yaml`, Typen, Versionen und Bereiche, Hubs, Resolver, Holen, Ausrollen, Arbeitspferde, `@Data/`, Rückfluss | vor jedem Paket |
| 03 *Skills und Assistenten* | Frontmatter von `SKILL.md` und `ASSISTANT.md`, Auflösung, Zuordnung, Oberflächen | bei Skills, Assistenten, Oberflächen |
| 02 *Master-Kontext* | Klassen `@`, `@@`, `@!` für Wissen | bei Wissen |
| 04 *Installation und Konfiguration* | CLI `aios`, `config.yaml`, Umgebungsvariablen | bei Befehlen und Tests |
| 01 *Überblick* | Begriffe, Invarianten I1–I9, Abnahmetest | bei Begriffsfragen |

## Begriffe

- **Paket:** versionierte Einheit mit `manifest.yaml`, ein Git-Repo in einem Hub, Version = Tag `v<version>`.
- **Element:** Skill, Assistent, Wissen oder Befehl in einem Paket.
- **Modul:** ein Paket, nach dessen Holen AIOS etwas Neues kann (`kernel`, `app`, `assistant`, `skill` oder mit Skills, Assistenten, Befehlen). `knowledge`, `tutorial`, `distribution` ohne solche Inhalte sind keine Module.
- **holen** (`aios --fetch`) gilt für Pakete, **ausrollen** (`aios --deploy`) für Elemente, **registrieren** für Skills; *installieren* nur für den Kernel.

## Regeln in Kürze

| Thema | Regel |
|---|---|
| Name | `<typ>-<name>`, englisch, gleich dem Typ: `app-`, `assistant-`, `skill-`, `knowledge-`, `tutorial-`, `distribution-`; Element `<name>`; Kernel `aios`. Ausnahme in v0.4: `assistent-gaertner`, `assistent-astronom` |
| Manifest | Pflicht `name`, `version`, `type`, `description`, `requires.aios`; Elemente in `contents` |
| Versionen | SemVer, Start `0.1.0`; Elemente in `skills/` und `assistants/` tragen die Paketversion, private Skills ihre eigene |
| Tags | ein gepushter Tag wird nie bewegt; jede Änderung, auch am README, ist eine neue Version |
| Paket-Repo | enthält nur, was beim Ausrollen nötig ist; Memos, Notizen, Testdaten gehören ins Konzeptprojekt |
| Rückfragen | Plan zeigen, fragen, dann ausführen; der Wunsch des Users ist keine Bestätigung des Plans |

## Konzeptprojekt und Paket-Repo

Ein **Konzeptprojekt** ist ein AIOS-Projekt mit `@/`, dem du als Assistentin zugeordnet bist; es hält Memos, Entscheidungen, Testprojekte und die Vorgaben des Users. Ein Konzeptprojekt kann **viele Pakete** konzipieren; nur große Pakete bekommen ein eigenes. Das **Paket-Repo** ist ein eigenes Git-Repo ohne `@/`.

## Vorgaben

Die Vorgaben eines Users stehen in der Regel **„AIOS-Pakete — Vorgaben"** (`name: aios-pakete-vorgaben`) im Masterspace des Konzeptprojekts oder darüber; ist sie geladen, gilt sie. Sie nennt: Ort der Paket-Repos, Hub und Owner, Sichtbarkeit, Standardlizenz, Sprache der Inhalte, Namensschema, Ort des Konzepts.

**Ohne Vorgaben:**

- Paket-Repos liegen in **`<konzeptprojekt>/@Package/<paket>/`** als eigenes Git-Repo; die `.gitignore` des Konzeptprojekts enthält `/@Package/`. Nenne den Ort und dass die Regel ihn ändern kann.
- `@Package/` (Quellen, die hier entstehen) ist nicht `@/@!Package/` (geholte Kopien).
- Hub, Owner und Lizenz fragst du, wenn sie gebraucht werden, spätestens vor dem Veröffentlichen, und bietest an, die Regel anzulegen.

## Ablauf eines Pakets

| Phase | Ergebnis | Praxis |
|---|---|---|
| Entwurf | Typ, Name, Inhalt entschieden; Paket-Repo mit Manifest und Elementen | Namen und Arten; Manifest und Versionen; je Typ Inhalt eines Assistenten, Daten einer App, Oberflächen, Kernel/Distribution/Tutorial |
| Prüfen | Manifest, Frontmatter, Versionen und Aufbau stimmen mit der Spec | Manifest und Versionen; Abhängigkeiten |
| Probe | lokal getaggt, in leerem Testprojekt geholt und ausprobiert | Probe vor Veröffentlichung; Getaggte Stände |
| Veröffentlichen | Repo, Tag, Topic, Index, Probe gegen den Hub | Veröffentlichen; Rückfragen |
| Pflege | Beiträge übernommen, neue Version | Rückfluss; Getaggte Stände |
