# KIRA FOUNDATION v0.16 – Hierarchische Strukturmakros

Enthält v0.1–v0.15 und ergänzt `foundation/hierarchical_structures.py`.

Start: `START_HIERARCHY.bat`. Tests: `TEST_ALL.bat`.

**Neu:** Mehrstufige binäre Makrokomposition aus gerichteten, typisierten Graphkanten.
Jede zusammengesetzte Struktur speichert konkrete Kantenzeugen und Kinder;
`reconstruct()` prüft vollständige verlustfreie Wiederherstellung der **Graphkanten**.
Identische Graphstrukturen mit anderen numerischen Knoten-IDs erhalten gleiche
kanonische Struktur-IDs. SQLite hält Versionen und Makrohäufigkeiten vor.

**Grenzen:** Maximal 12 Kanten pro Graph, höchstens fünf Knoten pro zusammengeführtem
Motiv. Die Kompositionsheuristik ist deterministisch, aber nicht optimal.
Ein Strukturmakro ist keine semantische oder kausale Erkenntnis. Die Graphen
müssen weiterhin von `event_graph` oder anderen Komponenten geliefert werden.
Die Hierarchie komprimiert derzeit keine Daten auf Dateiebene; konkrete
Kantenzeugen bleiben vollständig gespeichert. Getestet wird Graph-Roundtrip,
nicht Rekonstruktion der ursprünglichen Audio-Wellenform.
