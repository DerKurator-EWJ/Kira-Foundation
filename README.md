# KIRA FOUNDATION v0.19 – Integrierte partielle Makro-Wiederverwendung

Die Windows-Forschungsruntime v0.1–v0.18 bleibt erhalten. Neu ist `foundation/integrated_routing.py`.

## Start

Doppelklick auf `START_INTEGRATED.bat`; alle Tests über `TEST_ALL.bat`.

## Funktionsweise

Bekannte Teilgraphen werden per geprüfter Einbettung in neue Graphen gefunden. Statt sie nur im Plan zu markieren, erscheinen sie als **konkrete wiederverwendete Makro-Blätter** in der neuen Hierarchie. Noch nicht abgedeckte Kanten werden als neue Blätter aufgenommen. Anschließend werden zusammenhängende Blätter deterministisch verbunden. Jede Kante ist exakt einmal vertreten, und `reconstruct()` prüft die vollständige Rekonstruktion.

`IntegratedRouter` speichert Vorlagen und konkrete Hierarchien in SQLite. Die Vorlage muss derzeit höchstens fünf Knoten besitzen, der Zielgraph höchstens sieben Knoten und zwölf Kanten. Die Suche ist kombinatorisch und kann teuer werden.

## Fairer Benchmark

`benchmark_equal_workload()` misst **für beide Verfahren die vollständige Graphrekonstruktion** einschließlich Hierarchieerstellung bzw. Wiederverwendung. Beide müssen dieselbe ursprüngliche Kantenmenge zurückgeben. Die Hierarchien selbst dürfen sich im Aufbau unterscheiden. Die Messung verwendet kleine Python-Beispiele, keine optimierte Engine. Weniger neu erzeugte Makro-Knoten bedeutet nicht zwangsläufig weniger Laufzeit; der Einbettungssuchaufwand kann dominieren.

## Grenzen

Die Makro-Blätter sind geprüfte Strukturverweise mit konkretem Kantenzeugen, keine vollständige wiederverwendete verschachtelte Baumstruktur. Diese Repräsentation spart in diesem Prototyp keinen nachgewiesenen RAM oder Dateispeicher. Es findet keine semantische oder kausale Generalisierung statt. Der Kompositionsalgorithmus ist nicht optimal und ist auf kleine Graphen begrenzt.


## v0.20 — Epistemic Regulation Core (experimentell)

`START_EPISTEMIC.bat` demonstriert die Konsolidierung einer Hypothese A→B und ihre Revision zu A→C nach einem Regimewechsel. `foundation/epistemic_regulation.py` speichert Beobachtungen, Modelle und Revisionshistorie in SQLite; begrenzt Untersuchungen mit einem zurücksetzbaren Budget und liefert funktionale Zustandslabels. **Keine echten Emotionen, keine Sprachgenerierung, kein allgemeines Inquiry-System.** Der einfache Mehrheitsmechanismus (Fenster 12, Schwelle 65 %) ist eine kontrollierte Baseline, keine allgemeine Kausalitätsprüfung. Tests: `TEST_ALL.bat`.
