# KIRA FOUNDATION v0.25 – Staunen und Wortbrücke

## Neu
- `foundation/staunen_bruecke.py`: verbindet **Bestand** mit der persistenten Fragenverwaltung. Offene Teil-Ganzes-Beziehungen erzeugen Fragen; vorläufig geklärte Befunde schließen sie. Neue Befunde aktualisieren die Begründung.
- `begriffe.json`: maschinenlesbares deutsch-englisches Begriffsregister für die spätere Entwicklung.
- `foundation/wortbruecke.py`: Nachschlagen von deutschen Namen und technischen Kennungen.
- `START_STAUNEN.bat`: vorführbarer Ablauf.
- Zehn zusätzliche Tests. Bestehende Dateien und Startprogramme bleiben erhalten.

## Start
`START_STAUNEN.bat` für den Versuch, `TEST_ALL.bat` für alle Tests.

## Grenzen
Die Beobachtungen werden im Versuch vorgegeben; es gibt noch keine selbstständige Bild- oder Sprachinterpretation. Die Fragen sind aus Vorlagen erzeugt, nicht frei formuliert. Ein geschlossener Befund ist vorläufig. Die Wortbrücke ist ein Terminologieregister, **kein** Übersetzer, der natürliches Englisch in ausführbaren Code verwandelt. Das wäre ein eigenes, abgesichertes Entwicklungswerkzeug mit Parser, Typprüfung und Tests.
