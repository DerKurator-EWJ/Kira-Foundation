# KIRA FOUNDATION v0.18 — Partielle Makro-Wiederverwendung

Neu: `foundation/partial_macro_routing.py`, `START_PARTIAL_ROUTING.bat`.

Bekannte kleine Relationsgraphen werden als Vorlagen gespeichert. Bei neuen Graphen sucht die Runtime nach exakten, gerichteten, typisierten Teilgraph-Einbettungen. Nicht überlappende bekannte Kanten werden wiederverwendet; unbekannte Kanten bleiben als neue Bestandteile erhalten. Die vollständige Kantenmenge wird überprüfbar rekonstruiert. SQLite hält Vorlagen und Läufe über Neustarts.

**Grenzen:** höchstens 12 Kanten pro Zielgraph, höchstens 7 Zielknoten und 5 Vorlagenknoten; höchstens 20.000 getestete Abbildungen pro Vorlage. Greedy-Auswahl, nicht global optimal. Der Benchmark vergleicht unterschiedliche Arbeitsumfänge (Hierarchieaufbau versus Teilplan), daher ist er kein Nachweis einer Beschleunigung. Kein semantisches oder kausales Verständnis.

Start: `START_PARTIAL_ROUTING.bat`; Tests: `TEST_ALL.bat`.

---

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


## v0.17 – Structural Macro Routing

`START_ROUTING.bat` / `py -3 routing_cli.py`: Persistenter, ID-unabhaengiger
Template-Index fuer **exakt isomorphe** kleine Relationsgraphen.
Ein schneller, notwendiger Struktur-Fingerprint (Grad/Labels) filtert
Kandidaten; die anschliessende Isomorphiepruefung verhindert Fehlzuordnungen.
Bei Treffer werden gespeicherte Hierarchien auf die konkreten IDs umgebunden
und durch `reconstruct()` validiert. Bei Fehlschlag wird die Hierarchie neu
gebildet. Datenbank: `data/macro_router.sqlite`.

**Grenzen:** Keine partielle Wiederverwendung unbekannter Graphen;
maximal fuenf Knoten fuer Template-Matches und zwoelf Kanten fuer
Hierarchiebildung. Kein genereller Geschwindigkeitsvorteil nachgewiesen;
Isomorphiepruefung kann fuer kleine Graphen teurer sein als Neubau.
Statistik `cache_hits` misst Wiederverwendung, nicht Laufzeit oder RAM.
