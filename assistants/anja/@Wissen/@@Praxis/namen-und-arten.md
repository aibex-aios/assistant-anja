# Praxis — Namen und Arten

Quellen: Spec v0.5, 03 *Registrieren*, *Assistenten*; 06 *Pakete* (Paketnamen), *`manifest.yaml`*, *Umstellung von v0.3*, *Umstellung von v0.4*. AA-AIbex-AIOS, V0.4, Memo 43; V0.5, Memos 05, 15, 35.

| # | Regel | Beispiel |
|---|---|---|
| N1 | Ein Paket heißt `<typ>-<name>`, kleingeschrieben, mit `-`. Die Art im Namen ist **gleich dem `type`** im Manifest, englisch: `app`, `assistant`, `skill`, `knowledge`, `tutorial`, `distribution`, `worker` | `app-taschenrechner`, `skill-memo`, `knowledge-orion`, `assistant-anja`, `worker-yt-dlp`, `distribution-rothirsch` |
| N2 | Das Element im Paket heißt `<name>`, ohne Art | Paket `skill-memo` → Skill `memo`; Paket `assistant-anja` → Assistent `anja` |
| N3 | Der Kernel heißt `aios`, ohne Art; eine Variante unterscheidet sich durch Hub bzw. Repo | `aibex-aios/aibex-aios` |
| N4 | Der Paketname ist zugleich der Repo-Name im Hub und der Ordnername lokal | `aibex-aios/skill-memo` |
| N5 | Ein Assistent hat einen **Titel** für die Anzeige; Umlaute nur im Titel, der Name bleibt ASCII | `name: gaertner`, `title: Gärtner` |
| N6 | `name` im Frontmatter ist gleich dem Verzeichnisnamen, sonst wird das Element nicht registriert bzw. nicht aufgelöst | `skills/memo/SKILL.md` mit `name: memo` |
| N7 | Weitere Skills einer App oder eines Assistenten tragen den Elementnamen als Präfix | `taschenrechner-gui`, `gaertner-gui` |
| N8 | Verboten: `aios` (außer für den Kernel), `aios-…`, `gui`, `none`, `inherit`; höchstens 64 Zeichen aus Kleinbuchstaben, Ziffern und `-` | — |
| N9 | Maßgeblich für AIOS ist `type:` im Manifest; die Art im Namen ist eine Konvention von AIbex | — |

## Zu beachten

- **Bis v0.4:** Die Demo-Assistenten hießen `assistent-gaertner` und `assistent-astronom` (älteres deutsches Präfix, V0.4, Memo 43). Ab v0.5 heißen sie `assistant-gaertner` und `assistant-astronom`; die alten Repos bleiben mit Verweis im README, und `aios --activate v0.5.<n>` benennt sie in `packages:` um (Spec 06, *Umstellung von v0.4*). Neue Pakete heißen immer `assistant-…`.
- **Daten eines Pakets** liegen unter dem Paketnamen, nicht unter dem Elementnamen: `@Data/app-taschenrechner/`.
- **Umstellung von v0.3:** `skills: memo` → `skill-memo`; Einträge `<assistant>/<skill>` haben kein Paket (Spec 06).
