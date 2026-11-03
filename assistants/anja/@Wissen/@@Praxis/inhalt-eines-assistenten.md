# Praxis — Inhalt eines Assistenten

Quellen: Spec v0.6.1, 03 *Assistenten*, *Auflösung*; 02 *Klassen*, *Assistent der Session*. AA-AIbex-AIOS, V0.4, Memos 27, 70. Pakete `assistant-gaertner`, `assistant-astronom` 0.3.1.

## Aufbau im Paket

```
assistant-<name>/
├── manifest.yaml                      type: assistant, contents.assistants: [<name>]
├── README.md
└── assistants/<name>/
    ├── ASSISTANT.md                   Frontmatter und Rollentext
    ├── @!Skill/<skill>/SKILL.md       private Skills
    ├── @!Skill/<name>-gui/            Oberfläche (optional)
    └── @Wissen/
        ├── @Grundlagen/…              geladen, wenn der Assistent aktiv ist
        ├── @Content/…                 geladen: Inhaltsverzeichnis mit „Lesen, wenn …"
        └── @@<Thema>/…                verfügbar, gelesen bei Bedarf
```

Vorbilder: `assistant-gaertner` (mit Oberfläche und Wissen), `assistant-astronom` (schlank).

## Frontmatter

| # | Regel |
|---|---|
| A1 | Pflicht: `name` (gleich dem Ordner), `title`, `version`, `description` (eine Zeile) |
| A2 | `skills` nennt jeden Skill, den der Assistent braucht, auch die Oberfläche; `gui` muss in `skills` stehen. Ein nicht gefundener Skill ist ein Fehler |
| A3 | Skills werden zuerst im Assistentenordner gesucht, dann in der Kette; ein geteilter Skill (z. B. `memo`) muss im Projekt verfügbar sein oder als `depends` ins Manifest |
| A4 | `model` ist ein Wunsch, in der Desktop-App nur ein Hinweis; für genaues Arbeiten `opus`, für einfache Rollen `sonnet` |
| A5 | `tools` ist in v0.6 nur dokumentierend |

## Rollentext

Der Rollentext spricht den Assistenten mit **Du** an. Bewährte Gliederung (V0.4, Memo 70):

| Abschnitt | Inhalt |
|---|---|
| Einleitung | wer du bist, Ton, Sprache, Anrede; bei Demo-Assistenten: dient der Veranschaulichung |
| *Deine Personalität* | Antwort-Prefix (z. B. „👩‍🌾 ") und Anrede als Liste |
| *Dein Handwerk* | was der Assistent tut und mit welchem Skill; „halte dich genau an deinen Skill" |
| Fachabschnitt | woher das Wissen kommt, Quelle nennen, was bei Lücken zu sagen ist |
| *Deine Oberfläche* | nur wenn es eine gibt |
| *Deine Grenzen* | Praxis *Grenzen und Ehrlichkeit* |

## Wissen

| # | Regel |
|---|---|
| W1 | Was der Assistent immer braucht, kurz halten und laden; alles Weitere verfügbar, mit Inhaltsverzeichnis, das sagt, **wann** ein Dokument zu lesen ist |
| W2 | Daten, die mehrere Assistenten nutzen können, gehören in ein eigenes Wissenspaket ohne `depends`; der Assistent findet es über die Kette (Astronom und `knowledge-orion`) |
| W3 | Eigene Daten speichert ein Assistent in `@Data/assistant-<name>/` (Praxis *Daten einer App*) |

## Zu beachten

- Ein Assistent ist dem **Projekt** zugeordnet (`assistant:` in `.aios/config.yaml`), nicht dem Chat; zum Ausprobieren ein Unterprojekt anlegen.
- Ein lokaler Assistent gleichen Namens in `@!Assistant/` verdeckt den aus dem Paket; `/aios-context` meldet das. Bei mehreren Kopien entlang der Kette gewinnt die nächste (z. B. das `@!Package/` eines Testprojekts vor dem der Vault-Root).
- Private Skills, die `aios` aufrufen, tragen den Satz zum Aufruf über den Weiterleiter (Praxis *Rückfragen*, R9).
