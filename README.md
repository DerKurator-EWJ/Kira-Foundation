# KIRA FOUNDATION v0.9 – Aktive Exploration (Windows)

Alle Komponenten aus v0.1–v0.8 bleiben vorhanden. Neu: `foundation/exploration.py` und `START_EXPLORATION.bat`.

## Start
Doppelklick `START_EXPLORATION.bat` (Python 3 erforderlich). Alternativ: `py -3 exploration_cli.py`.

Befehle: `observe 3000` (passive Beobachtung), `explore 4000` (Kira waehlt balanciert die naechste Intervention), `report`, `choose`, `history 5`, `do A 1 100`, `exit`.

Die simulierte Welt hat beobachtbare binaere Variablen A, B, Y und einen **verborgenen** gemeinsamen Einfluss Z. A ist mit Y korreliert, verursacht Y aber nicht. Eine gezielte A-Intervention veraendert Y nicht systematisch. B beeinflusst Y kausal. Die Lernkomponente kennt die Weltgleichung nicht, kann aber Beobachtungs- und Interventionsstatistiken getrennt auswerten. Der `report` zeigt Differenzen empirischer Y-Raten (1 minus 0); dies sind **deskriptive Punktschaetzungen**, keine Signifikanztests oder Kausalbeweise. Randomisierte externe Einfluesse und identische Weltregeln sind Annahmen dieses kontrollierten Simulators.

`explore` waehlt deterministisch die bisher am wenigsten untersuchte Kombination aus A/B und 0/1. Dies ist **aktive Versuchsplanung**, aber noch kein autonomer Erkenntnisagent, keine Hypothesengenerierung, keine Uebertragung auf Video/Audio und keine allgemein gueltige Kausalentdeckung. Ein einzelner Lauf mit wenigen Daten kann irrefuehrend sein.

Persistenz: `data/exploration.sqlite`. Sie ist von `data/live.sqlite` getrennt, damit Experimente die produktive Audio-Runtime nicht veraendern. Der Simulator nutzt einen festen Seed; ein Neustart setzt mit dem naechsten Experimentindex fort. Die latente Variable Z wird nicht in der Lern-Datenbank gespeichert.

Tests: `TEST_ALL.bat` oder `py -3 -m unittest discover -s tests -v`.
