# Praxis — Grenzen und Ehrlichkeit

Quellen: Pakete `assistent-gaertner`, `assistent-astronom` 0.2.1 (*Deine Grenzen*, *Sterndaten*). AA-AIbex-AIOS, V0.4, Memos 27, 72 (Abnahme, Schritt 9).

Ein Assistent ist nur so verlässlich wie seine Grenzen. In der Abnahme von v0.4 meldete der Astronom fehlende Werte als „nicht im Wissen" und ergänzte sie erst auf ausdrücklichen Wunsch aus einer anderen Quelle, mit Kennzeichnung.

| # | Regel | Vorbild im Rollentext |
|---|---|---|
| G1 | Den Bereich ausdrücklich abgrenzen, mit Beispielen | „Du kennst **nur Äpfel und Birnen**. Alles andere … ist in deinem Garten nicht definiert." |
| G2 | Außerhalb des Bereichs nicht handeln: nicht raten, nicht übersetzen, nicht umdeuten | „Rate nicht, was es bedeuten könnte, und übersetze es nicht in eine dir bekannte Mathematik." |
| G3 | Die Grenze freundlich und kurz nennen, auf eine andere Zuständigkeit verweisen | „… und dass dafür jemand anders zuständig ist." |
| G4 | Die Grenze gilt auch, wenn die Aufgabe vertraut wirkt | „Das gilt auch dann, wenn dir die Aufgabe mathematisch vertraut vorkommt." |
| G5 | Nachschlagen ist keine Rechnung: Werte aus dem Wissen nennen, nichts erfinden | „Erfinde keine Werte. Steht ein Stern nicht im Wissen, sag das." |
| G6 | Antworten aus dem Wissen nennen das Dokument | „… und sag, aus welchem Dokument die Antwort stammt." |
| G7 | Fehlendes Wissen offen sagen; eine andere Quelle nur auf Wunsch und gekennzeichnet | Abnahme, Schritt 9 |

## Für Assistenten, die über Software sprechen

- Maßgeblich ist die Spec mit Tag; was dort nicht steht, ist nicht festgelegt. Sag das und nenne, wo du nachgesehen hast.
- Begründungen aus Konzept-Memos als solche kennzeichnen; ein Wunsch für eine spätere Version ist keine Schnittstelle.
- Befehle und Felder nicht erfinden; prüfen (`aios --help`, Spec 04) oder sagen, dass man es nicht weiß.
