# KIRA FOUNDATION v0.10 – Hypothesenspeicher (Windows)

Alle Module aus v0.1 bis v0.9 sind enthalten. Neu: `foundation/hypotheses.py`, `hypothesis_cli.py`, `START_HYPOTHESES.bat`.

## Start
Doppelklick `START_HYPOTHESES.bat` oder `py -3 hypothesis_cli.py`.

In der Konsole:
```
observe 3000
hypotheses
explore 4000
review
history 10
choose
exit
```

`hypotheses` bewertet die zwei **vordefinierten** Kandidaten `do(A=1) vs do(A=0)` und `do(B=1) vs do(B=0)` anhand der Interventionen. `review` schreibt eine unveraenderliche Bewertung in die SQLite-Historie, `history` liest sie. `explore` priorisiert offene Hypothesen, balanciert ansonsten die Versuchsarme. `observe` erzeugt nur passive Daten; passive Beobachtungen werden **nicht** zur Interventions-Effektschaetzung herangezogen.

Die Effektgroesse ist die Differenz der empirischen Y=1-Raten. Der konservative Bereich wird aus zwei Wilson-Score-Intervallen gebildet (Differenz der Intervallgrenzen). Dieser Bereich ist keine exakte 95%-Konfidenzgrenze fuer die Differenz; die Einzelintervalle verwenden z=1.96. Die Klassifikation `SUPPORTED_POSITIVE_EFFECT` bedeutet, dass die untere Differenzgrenze ueber +0.10 liegt; `SUPPORTED_NEGLIGIBLE_EFFECT` bedeutet, dass der gesamte Bereich in [-0.10,+0.10] liegt. Andernfalls bleibt die Hypothese offen. Unter 30 Versuchen je Arm bleibt sie ebenfalls offen. Die Entscheidungen haengen von diesen frei gewaehlten Schwellenwerten und dem kontrollierten Simulator ab.

**Grenzen:** Die Hypothesen werden nicht frei erfunden; A und B sind vorgegeben. Das ist ein Evidenz- und Revisionsmechanismus, kein autonomer wissenschaftlicher Theoriegenerator. Die gespeicherte Bewertung ist ein Snapshot, keine automatisch fortgeschriebene Wahrheit. Keine Integration in die Audio-Runtime. `data/hypotheses.sqlite` ist eine separate Experimentdatenbank. Python 3 und Standardbibliothek genuegen.

Tests: `TEST_ALL.bat` oder `py -3 -m unittest discover -s tests -v`.


## v0.11 – Datengetriebene Hypothesenkandidaten

`START_DISCOVERY.bat` startet das neue Labor. Befehle: `observe 3000`, `scan`, `candidates`, `choose`, `explore 4000`, `review`, `history 10`. Persistenz in `data/discovery.sqlite`.

Die Kandidaten werden **erst nach einer Beobachtungsanalyse** angelegt, nicht im Voraus. Die aktuelle ToyWorld besitzt nur die beobachteten binären Eingangsvariablen A und B sowie Y. Der Kandidatenscanner verwendet eine Mindeststichprobe und einen Assoziationsschwellenwert; er kann schwache oder nichtlineare Beziehungen übersehen. Eine beobachtete Assoziation ist keine Kausalität; Interventionen werden separat bewertet. Dies ist weder frei formulierte Hypothesenerfindung noch ein allgemein gültiger Kausalitätsbeweis. Das Labor bleibt vom Audio-Pfad getrennt.


## v0.12 – Strukturelle Generalisierung (ID-invariant)

Start: `START_GENERALIZATION.bat` oder `py -3 generalization_cli.py`.

Neu: `foundation/generalization.py` mit gerichteten, relationstypisierten Graphen,
ID-unabhaengiger Zuordnung, Pruefung eindeutiger Abbildungen und Transfer von
**unverifizierten** Hypothesen. Die Demo benutzt zwei Welten mit unterschiedlichen
IDs, aber identischer Struktur. Historie: `data/generalization.sqlite`.

**Wissenschaftliche Grenze:** Graphen und Relationen sind in dieser Version
explizit eingegeben; sie werden nicht aus Audio oder Rohbeobachtungen entdeckt.
Die Abbildung ist exakte Graphisomorphie fuer kleine Graphen (maximal sieben Knoten),
keine allgemeine Analogie- oder Kausalitaetsentdeckung. Bei mehreren gueltigen
Abbildungen wird ein Transfer verweigert. Ein uebertragener Kandidat ist keine
bestaetigte Wirkung und muss in der Zielwelt experimentell geprueft werden.
Die bestehenden Module bleiben separat nutzbar.
