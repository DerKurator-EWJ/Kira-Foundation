# KIRA FOUNDATION v0.13 – Partielle relationale Analogien

Alle bisherigen v0.12-Module bleiben enthalten. **Neu:** `foundation/partial_generalization.py`.

## Windows-Start

- `START_PARTIAL.bat` – partielle Strukturübereinstimmung und SQLite-Protokoll.
- `START_GENERALIZATION.bat` – unveränderte exakte v0.12-Referenz.
- `TEST_ALL.bat` – gesamte Regressionstestsuite.

## Methode

Für Graphen mit maximal sieben Knoten sucht der Matcher injektive Zuordnungen von Teilmengen der Quell- auf Zielknoten. Gerichtete und typisierte Kanten müssen übereinstimmen, um als Treffer zu gelten. Fehlende und zusätzliche Kanten werden als Abweichungen protokolliert. Priorisiert werden (1) Zahl gemeinsamer Kanten, (2) Anteil gemeinsamer Kanten an der Vereinigung der induzierten Kanten, (3) Zahl zugeordneter Knoten. `min_edges` und `min_precision` legen Mindestanforderungen fest. Bei mehreren gleichwertigen Optima werden **keine** Hypothesen übertragen. Die Suche ist kombinatorisch und bewusst auf kleine Graphen begrenzt.

`partial_transfer` überträgt nur Quellkanten, deren beide Endpunkte eindeutig zugeordnet sind. Eine in der Zielwelt fehlende Kante ist **eine unbestätigte Hypothese**, kein kausaler Nachweis. Bereits vorhandene Kanten sind **beobachtete Analogien**, keine Kausalitätsbelege. Die Beispielgraphen werden manuell vorgegeben. Keine Rohdaten-Graphentdeckung, kein Echtzeitbetrieb, keine semantische Abstraktion.

Persistenz: `data/partial.sqlite` (Tabelle `generalization_runs`).
