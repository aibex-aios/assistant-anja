# Praxis — Arbeitspferde

Quellen: Spec v0.5, 07 *Arbeitspferde* (ganz); 06 *`manifest.yaml`*, *Holen*; 04 *Formate*, *Umlenkung für Tests*; 03 *Ausführungsmodell*. AA-AIbex-AIOS, V0.5, Memos 12, 16, 17, 20–22, 29–33, 36.

## Was ein Arbeitspferd ist

Ein Programm ist genau dann ein Arbeitspferd, wenn es **ausgeführt** wird (K1), auf dem **Rechner** wohnt statt im Projekt (K2) und **vor Ort gebaut** wird (K3). Typisch: eigene Version (K4), meist Fremdsoftware (K5), für Skills gebaut (K6), Daten unter `@Data/` des Pakets, das sie erzeugt (K7). Ein Befehl in `commands/` und ein Skript eines Skills sind keine Arbeitspferde (sie liegen im Paket und brauchen kein setup); `python3` und `git` sind Voraussetzungen des Kernels.

## Regeln

| # | Regel | Beispiel |
|---|---|---|
| W1 | Ein Arbeitspferd ist ein eigenes Paket `type: worker`, Name `worker-<name>`; andere Pakete nutzen es über `depends`. Das Feld `workers:` aus v0.4 gibt es nicht mehr, `aios --fetch` lehnt es ab | `skill-video-analyse` → `depends: worker-yt-dlp` |
| W2 | Ein `worker` ist ein Modul **ohne Elemente**: kein `contents` | — |
| W3 | `worker:` nennt `kind` (`python` oder `script`), `programs` (Programme in `bin/`) und optional `check` (Befehl, Exit 0 = in Ordnung) | `programs: [yt-dlp]`, `check: yt-dlp --version` |
| W4 | `kind: python`: `requirements` nennt eine Datei im Paket mit **allen** Paketen als `paket==version` und mindestens einem `--hash=sha256:…` je Paket; ohne Hashes wird das Paket nicht geholt | `worker/requirements.lock` |
| W5 | Die Datei erzeugt der Maintainer, nicht AIOS: `pip-compile --generate-hashes --strip-extras -o worker/requirements.lock requirements.in` (pip-tools in einem eigenen venv). Sie enthält die Hashes aller Wheels einer Version und gilt damit für macOS und Linux | `requirements.in`: `yt-dlp[default]` |
| W6 | Die **Programmversion steht im Paket fest**; ein neues Programm ist eine neue Paketversion (Patch) | `worker-yt-dlp` 0.1.1 mit neuem `yt-dlp` |
| W7 | `kind: script` nur als Ausweg: `setup` und `remove` als Bash-Skripte; sie legen die Programme in `$AIOS_WORKER_DIR/bin/` ab; der Plan zeigt ihren vollen Inhalt | — |
| W8 | Skills rufen ein Arbeitspferd **über seinen Weiterleiter** auf, nie über den `PATH` des Users: `~/.aios/bin/<programm>` | `~/.aios/bin/yt-dlp -J --skip-download "<URL>"` |
| W9 | Fehlt das Programm (Exit 127 des Weiterleiters), meldet der Skill „Paket nicht vollständig geladen" und nennt höchstens `aios --fetch`; **keine Installationsanweisung im Chat**, nie ein setup aus dem Skill (I10) | — |
| W10 | Arbeitspferde, die einander brauchen, nennen sich in `depends`; der Weiterleiter stellt `~/.aios/bin` vorn in den `PATH`, so finden sie einander | `worker-yt-dlp` → `depends: worker-deno` |
| W11 | Daten eines Arbeitspferds legt das **nutzende** Paket unter seinem `@Data/` ab, nicht unter `@Data/worker-…/` (K7) | Datenbank einer App unter `@Data/app-notizen/` |
| W12 | `requires.aios: ">=0.5,<0.6"`; unter v0.4 gibt es keinen Typ `worker` | — |

## Was AIOS damit tut

- **Installation je Version** unter `/opt/aios/workers/<paket>/v<version>/` (ohne `sudo` unter `~/.aios/workers/`), nach dem setup schreibgeschützt; Versionen liegen nebeneinander.
- **Aktiviert** ist die Version aus `lock.yaml` des nächsten Projekts der Kette; der Weiterleiter wählt sie ab `cwd`.
- **Paket laden** (`aios --fetch`): ein Plan mit setup (bei `python` die Liste `paket==version`), ein Ja, alles oder nichts; registriert wird erst nach erfolgreichem setup.
- **Upgrade** richtet die neue Version ein; **Entfernen** baut eine Version ab, wenn kein Projekt sie mehr nutzt; der **Abgleich** auf einem zweiten Rechner richtet fehlende Versionen ein.
- `aios --worker` zeigt den Stand, `aios --worker <paket> setup` repariert.
- In v0.5 nicht: Dienste (`start`, `stop`), `kind: binary` (z. B. `ffmpeg`).

## Beispiel — `worker-yt-dlp`

```yaml
name: worker-yt-dlp
version: 0.1.0
type: worker
description: yt-dlp zum Laden von Videos und Untertiteln
requires:
  aios: ">=0.5,<0.6"
depends:
  worker-deno: "~=0.1.0"
worker:
  kind: python
  requirements: worker/requirements.lock
  programs: [yt-dlp]
  check: yt-dlp --version
license: Apache-2.0
```

```
worker-yt-dlp/
├── manifest.yaml
├── requirements.in             yt-dlp[default]   (Quelle für pip-compile, nicht ausgewertet)
├── worker/requirements.lock    11 Pakete mit Hashes
└── README.md
```

**Ablauf beim Bauen:** Repo anlegen (`anja-anlegen`), `requirements.in` schreiben, Datei mit `pip-compile` erzeugen, `anja-pruefen` (prüft `==` und Hashes), lokal taggen, Probe mit `aios --fetch worker-yt-dlp --from <repo>` in einem Testprojekt, dann `~/.aios/bin/yt-dlp --version` dort aufrufen. Für Tests ohne Netz gibt es `AIOS_PIP_FIND_LINKS` (Spec 04).

## Grenzen

- Die Lizenz eines Arbeitspferds ist die des Pakets (Manifest, README); die Lizenzen der installierten Programme (z. B. Unlicense bei `yt-dlp`) nennt das README.
- Ob ein Programm wirklich ein Arbeitspferd braucht, entscheidet K1–K3; ein Skript mit der Standardbibliothek von Python bleibt im Skill.
