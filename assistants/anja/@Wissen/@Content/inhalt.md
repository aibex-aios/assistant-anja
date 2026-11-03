# Inhalt der Praxis

Der Leitfaden ist geladen. Die Praxis ist verfügbar: Lies das passende Dokument mit Read, bevor du zu seinem Thema etwas sagst oder tust. Jedes Dokument nennt seine Quellen in der Spec und im Konzept-Repo.

| Datei | Inhalt | Lesen, wenn … |
|---|---|---|
| `@@Praxis/namen-und-arten.md` | Paketnamen, Elementnamen, Titel, verbotene Namen | ein Paket oder Element benannt oder ein Name geprüft wird |
| `@@Praxis/manifest-und-versionen.md` | vollständiges Manifest, `contents`, SemVer, Versionen der Elemente, Standardbereich | ein Manifest geschrieben oder geprüft oder eine Version erhöht wird |
| `@@Praxis/getaggte-staende.md` | Tags, Release-Kandidaten, Cache bei `--from`, Ablauf einer neuen Version | getaggt, korrigiert oder eine neue Version gemacht wird |
| `@@Praxis/inhalt-eines-assistenten.md` | Aufbau, Frontmatter, Rollentext, Wissen und Auflösung eines Assistenten | ein Assistent entworfen oder geprüft wird |
| `@@Praxis/grenzen-und-ehrlichkeit.md` | Grenzen im Rollentext, nicht raten, Quelle nennen | ein Rollentext geschrieben wird oder eine Frage außerhalb des Wissens liegt |
| `@@Praxis/arbeitspferde.md` | Arbeitspferde: Kriterien, Paket `worker-<name>`, Hash-Datei, Installation unter `~/.aios/workers/`, Weiterleiter, Aufruf aus Skills, Beispiel | ein Paket ein Programm braucht (z. B. `yt-dlp`) oder ein `worker` entsteht oder geprüft wird |
| `@@Praxis/daten-einer-app.md` | `@Data/<paket>/`, mitgelieferte Daten, Speichern aus HTML-Teilen | ein Paket Daten speichert (App oder Assistent) |
| `@@Praxis/oberflaechen.md` | `gui.yaml`, Kacheln, HTML-Teile, Ausweg im Chat | eine Oberfläche entworfen oder geprüft wird |
| `@@Praxis/rueckfragen.md` | Plan, Rückfrage, Ausführen; Schritte nach außen; Aufruf von `aios` über den Weiterleiter | ein Skill schreibt, `aios` aufruft oder etwas nach außen wirkt |
| `@@Praxis/abhaengigkeiten.md` | `depends`, Bereiche, Suche in Hubs, Resolver, Paketwechsel bei der Aktivierung | ein Paket ein anderes braucht |
| `@@Praxis/probe-vor-veroeffentlichung.md` | Ablauf der Probe in einem Testprojekt, `--to`, Release-Kandidaten | ein Paket ausprobiert wird |
| `@@Praxis/veroeffentlichen.md` | Checkliste für das Veröffentlichen im Hub, Begleitpakete, Commits vor dem Push | ein Paket veröffentlicht wird |
| `@@Praxis/rueckfluss.md` | `aios --contribute`, Übernahme durch den Maintainer | Beiträge von Usern ankommen oder angenommen werden sollen |
| `@@Praxis/testvorlagen.md` | Test-Hubs, Testversionen, Live-Tests, Headless-Läufe ohne die Regeln des Users | automatische Tests für Pakete oder den Kernel entstehen oder eine Probe ohne den User laufen soll |
| `@@Praxis/entwicklungsprozess.md` | Best Practices P1–P12 hinter deinem Workflow, Maß halten je Paketgröße | der User nach dem Sinn eines Schritts fragt oder du den Umfang des Workflows vorschlägst |
| `@@Praxis/kernel-distribution-tutorial.md` | Kernel, Kernel-Skills und Hüllen, Distributionen, Tutorials | ein Paket dieser Typen entsteht oder geprüft wird |

Lies nur das Dokument, das zur Frage passt. Steht die Antwort weder dort noch in der Spec, sag das, statt zu raten.
