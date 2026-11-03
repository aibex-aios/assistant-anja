# assistant-anja

Assistentin *Anja* von AIbex AIOS, Version 0.3.0: Spezialistin für die Entwicklung von AIOS-Paketen aller Typen (App, Assistent, Skill, Wissen, Tutorial, Distribution, Arbeitspferd, Kernel). Sie kennt die Spec von AIOS v0.6, die Gründe dafür und die Praxis aus der Entwicklung und begleitet ein Paket vom ersten Gedanken bis zur Veröffentlichung. Jede Antwort beginnt mit „🙎🏻‍♀️ ".

## Holen

**Voraussetzung:** AIbex AIOS v0.6 ist installiert, und der Vault ist an der Vault-Root mit `aios --activate v0.6.<n>` gebunden (ein AIBOS-Workspace); sonst tut `aios --fetch` nichts. Für AIOS v0.4 und v0.5 gibt es Anja 0.2.x (`aios --fetch "assistant-anja~=0.2.1"`).

```bash
aios --fetch assistant-anja
```

Anja kommt aus dem Hub `aibex-aios`, dem Standard-Hub von AIOS; deshalb braucht der Befehl keine Hub-Angabe. Ausgeschrieben lautet er `aios --fetch aibex-aios/assistant-anja`.

Zuordnen mit `/aios-assistant Anja` in dem Projekt, in dem die Pakete konzipiert werden. Anja und ihre Skills wirken **ab dem nächsten Chat** in diesem Projekt.

## Wie Anja arbeitet

Anja folgt einem Workflow in elf Phasen: Einstieg, Konzept, Bewertung, Konsolidierung in kleinen Fragegruppen, Soll-Bild und Skizze, Spezifikation, Freigabe, Implementierung, Abnahme, Rückblick und Abschluss. Im Konzept führst du oder sie, ganz wie du willst; danach führt sie und fragt immer mit einer Empfehlung. Jeder Übergang braucht dein Ja, alles wird in Memos festgehalten, der Stand in einem Plan (`@Plan/Plan.md`), und gebaut wird erst nach der Freigabe der Spezifikation.

## Voraussetzungen

Anja liest die Spec im Code-Repo `aibex-aios/aibex-aios` (je Version über den Tag) und die Gründe im Konzept-Repo `aibex-aios/AA-AIbex-AIOS`. Beide Repos sind derzeit privat; Anja hilft also vorerst nur Usern mit Zugriff (lokaler Klon oder `gh` mit Anmeldung).

## Vorgaben

Wo Paket-Repos liegen, in welchem Hub veröffentlicht wird und unter welcher Lizenz, legt jeder User selbst fest: in einer Regel *AIOS-Pakete — Vorgaben* (`name: aios-pakete-vorgaben`) im Masterspace des Konzeptprojekts. Dort stehen auch die Orte der Vaults, die Anja vor einer Abnahme durchsucht. Ohne die Regel legt Anja Paket-Repos in `<projekt>/@Package/<paket>/` an und fragt den Rest, wenn er gebraucht wird.

## Lizenz

Apache License 2.0 (`LICENSE`), Rechteinhaber AIbex KG (`NOTICE`). Die Marken „AIbex" und „AIbex AIOS" sind nicht mitlizenziert.
