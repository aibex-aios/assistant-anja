# Praxis — Entwicklungsprozess

Quellen: AA-AIbex-AIOS, Memos zu V0.1–V0.4 (Entwicklung von AIOS, rückblickend betrachtet); V0.6, Memos 01–04 (Workflows). Dein Workflow setzt diese Best Practices um; hier steht, **warum**. Lies dieses Dokument, wenn der User nach dem Sinn eines Schritts fragt oder wenn du den Umfang des Workflows für ein Paket vorschlägst.

Ob jede dieser Anpassungen bei der Entwicklung von AIOS bewusst geplant war, lässt sich nicht sicher sagen. Rückblickend beschreiben sie einen sehr effizienten Prozess: v0.4 brauchte für deutlich mehr Umfang weniger Zeit als v0.1, und die Abnahme fand die Fehler vor dem Release.

## Best Practices

| # | Best Practice | So wendest du sie an | in AIOS sichtbar |
|---|---|---|---|
| P1 | **Klein releasen, groß denken.** Die Vision darf weit reichen; ein Release nimmt nur, was sich in einem Zug abschließen lässt. Alles andere wird als Wunsch für eine spätere Version festgehalten, nicht verworfen | in der Bewertung die Tabelle *gehört zu diesem Release / später*; Späteres als Memo mit Status *Wunsch* | v0.2 bewusst klein; Wünsche in Ordnern für v0.5, v0.6, v0.99 |
| P2 | **Kennzeichnen, wer spricht.** Wunsch des Users, Analyse der KI und Entscheidung stehen als verschiedene Memos mit eigenem Status da | Status *Wunsch*/*Notiz* für Ideen, *Analyse*/*Zusammenfassung* für deine Berichte, *Entscheidung* nur für Antworten des Users; Autor „<Assistent>, im Auftrag von <User>" | ab v0.3 Paare *Wunsch → Entscheidung* |
| P3 | **Erst verdichten, dann spezifizieren.** Die Spec entsteht aus einem geprüften **Soll-Bild**, das nur den gültigen Stand enthält | Phase 4: Soll-Bild als Abschlussprotokoll; die Spec wird daraus erzeugt | v0.4, Memo 13 *Soll-Bild* |
| P4 | **Keine stillen Entscheidungen.** Was du selbst festlegst, steht nummeriert im Bericht und wird bestätigt | Abschnitt *Festlegungen zur Bestätigung*; eine Buchstabenreihe je Schritt | ab v0.2 „beim Erzeugen festgelegt"; Regel *Weiter*, *Offenlegen* |
| P5 | **Tore in kurzen Abständen.** Plan erst als Entwurf, dann freigegeben; jeder Schritt endet mit Bericht und Freigabe des nächsten | bei größeren Paketen ein Implementierungsplan mit Schritten | v0.1 zwölf Schritte ohne Tor; ab v0.3 je Schritt freigegeben |
| P6 | **Annahmen früh prüfen.** Was vom Host abhängt, wird mit einer kleinen Probe geprüft, bevor darauf gebaut wird | Probe im Scratchpad oder Testprojekt, Ergebnis als Memo; Live-Probe mit einem kleinen Modell | v0.3 Proben O3, O4; v0.4 Live-Tests mit haiku |
| P7 | **Die Abnahme vorher festlegen.** Der Abnahmetest steht in der Spec, bevor implementiert wird; die Abnahme ist eine eigene Phase mit nummerierten Befunden und Korrekturen vor dem Release | Abnahmetest in Skizze und Spec; Phase 8 mit Befunden B1…; veröffentlicht wird erst danach | v0.4: Abnahmetest in Spec 01, Befunde B1–B8 |
| P8 | **Was sich bewährt, wird Regel.** Wiederkehrendes wird ausdrücklich: als Regel, als Wissen eines Assistenten, als Skill | im Rückblick vorschlagen | Regel *Weiter* mitten in v0.3; dieser Workflow |
| P9 | **Erst schauen, wie andere es lösen.** Vorbild suchen und festhalten, was übernommen, verändert oder anders gemacht wird | im Konzept nach einem Vorbild fragen; bei Paketen zuerst der Hub | v0.4: Analyse von Zephyr |
| P10 | **Konzept und Ergebnis versioniert ablegen.** Zu jeder veröffentlichten Version gibt es den passenden Stand des Konzepts | Memos im Konzeptprojekt; Tag `<paket>-v<version>` im Konzept-Repo | Versionsordner, Tags in Konzept- und Code-Repo |
| P11 | **Rückkopplung zulassen, aber festhalten.** Zeigt die Umsetzung eine Lücke oder eine bessere Idee, geht es zurück ins Konzept, nie still in den Code | Memo und Fragegruppe, Spec nachführen | v0.4: Taschenrechner während der Umsetzung neu entworfen |
| P12 | **Am Ende zurückblicken.** Was lief gut, was würde die Methode verbessern? | Phase 9 *Rückblick* | diese Best Practices selbst |

## Maß halten

Nicht jedes Paket braucht alles. Schlage den Umfang vor; der User entscheidet.

| Paket | genügt | lohnt sich zusätzlich |
|---|---|---|
| klein: eine Datei Wissen, ein einfacher Skill ohne Code | P1–P4, P10, P11; Phasen zusammengelegt (verkürzte Form) | — |
| mittel: Assistent, Skill mit mehreren Teilen | wie oben, Phasen einzeln | P6, P7 mit kurzer Abnahme, P9 |
| groß: App, Assistent mit Oberfläche, Paket mit Code, Kernel | alle | P5 mit Implementierungsplan, P7 mit Abnahmetest in der Spec |
