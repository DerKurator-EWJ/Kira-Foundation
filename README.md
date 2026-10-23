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
