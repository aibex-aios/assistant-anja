# Praxis — Namen und Arten

Quellen: Spec v0.4, 03 *Registrieren*, *Assistenten*; 06 *`manifest.yaml`*, *Umstellung von v0.3*. AA-AIbex-AIOS, V0.4, Memo 43; V0.5, Memo 05.

| # | Regel | Beispiel |
|---|---|---|
| N1 | Ein Paket heißt `<typ>-<name>`, kleingeschrieben, mit `-`. Die Art im Namen ist **gleich dem `type`** im Manifest, englisch: `app`, `assistant`, `skill`, `knowledge`, `tutorial`, `distribution` | `app-taschenrechner`, `skill-memo`, `knowledge-orion`, `assistant-anja` |
| N2 | Das Element im Paket heißt `<name>`, ohne Art | Paket `skill-memo` → Skill `memo`; Paket `assistant-anja` → Assistent `anja` |
| N3 | Der Kernel heißt `aios`, ohne Art; eine Variante unterscheidet sich durch Hub bzw. Repo | `aibex-aios/aibex-aios` |
| N4 | Der Paketname ist zugleich der Repo-Name im Hub und der Ordnername lokal | `aibex-aios/skill-memo` |
| N5 | Ein Assistent hat einen **Titel** für die Anzeige; Umlaute nur im Titel, der Name bleibt ASCII | `name: gaertner`, `title: Gärtner` |
| N6 | `name` im Frontmatter ist gleich dem Verzeichnisnamen, sonst wird das Element nicht registriert bzw. nicht aufgelöst | `skills/memo/SKILL.md` mit `name: memo` |
| N7 | Weitere Skills einer App oder eines Assistenten tragen den Elementnamen als Präfix | `taschenrechner-gui`, `gaertner-gui` |
| N8 | Verboten: `aios` (außer für den Kernel), `aios-…`, `gui`, `none`, `inherit`; höchstens 64 Zeichen aus Kleinbuchstaben, Ziffern und `-` | — |
| N9 | Maßgeblich für AIOS ist `type:` im Manifest; die Art im Namen ist eine Konvention von AIbex | — |

## Zu beachten

- **Ausnahme in v0.4:** Die Demo-Assistenten heißen noch `assistent-gaertner` und `assistent-astronom` (älteres deutsches Präfix, V0.4, Memo 43). Der Kernel v0.4 bildet bei der Umstellung von v0.3 `assistants: <name>` auf `assistent-<name>` ab. Die Umbenennung ist für v0.5 vorgesehen (V0.5, Memo 05, Wunsch). Neue Pakete heißen immer `assistant-…`.
- **Daten eines Pakets** liegen unter dem Paketnamen, nicht unter dem Elementnamen: `@Data/app-taschenrechner/`.
- **Umstellung von v0.3:** `skills: memo` → `skill-memo`; Einträge `<assistant>/<skill>` haben kein Paket (Spec 06).
