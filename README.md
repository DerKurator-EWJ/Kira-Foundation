# KIRA FOUNDATION v0.14 – Ereignisstrom → Relationsgraph

Alle Module der v0.13 bleiben erhalten. Neu: `foundation/event_graph.py`, `graph_cli.py`, `START_GRAPHS.bat`.

## Start (Windows)

- `START_GRAPHS.bat`: zwei synthetische ID-Ereignisströme aufnehmen, beobachtete zeitliche Relationen als Graphen ableiten und mit dem partiellen Matcher vergleichen.
- `TEST_ALL.bat`: Regressionstests ausführen.
- Vorhandene v0.7+ Live-Daten importieren: `py -3 graph_cli.py --live-db "C:\Pfad\zu\live.sqlite"`.

## Wissenschaftliche Einschränkungen

Die abgeleiteten Kanten `PRECEDES` bedeuten ausschließlich **beobachtete unmittelbare zeitliche Nachbarschaft**, nicht Ursache, Einfluss oder Semantik. Die Kanten enthalten Zählwerte und die explizite Kennzeichnung `causal: false`. `min_count=2` filtert zufällige Einzelereignisse. Nur die sieben häufigsten IDs werden für den Graphen verwendet; andere IDs sind im Rohstrom weiterhin gespeichert. Die Graphen werden mit dem vorhandenen v0.13-Matcher verglichen. Bei Mehrdeutigkeit darf kein Hypothesentransfer als gesichert ausgegeben werden.

Die Graph-Pipeline ist eine eigenständige Forschungsanwendung mit SQLite-Speicher; Live-Runtime-Daten lassen sich per Import einlesen. Es gibt noch **keine** automatisierte Audio→Graph-Hintergrundverarbeitung, keine kausale Entdeckung, keine robuste semantische Interpretation und keinen Skalierungsnachweis. Bei Import in eine bereits anders verwendete Ziel-Stream-ID können Tick-Kollisionen entstehen; daher separate Datenbank oder Ziel-Stream verwenden.
