# KIRA FOUNDATION v0.3 — Makro-Forschung

Windows: `START_MACROS.bat` (Demo) oder `TEST_ALL.bat` (Tests). Python 3.10+, keine externen Pakete. Die Funktionen aus v0.1 und v0.2 bleiben enthalten.

## Neu
- `foundation/macros.py`: **experimentelle** Online-Erkennung wiederkehrender ID-Teilsequenzen, nach Modalitaet und Quellstufe getrennt.
- Laengen- und Zwei-Token-Ankerindex fuer die laengste bekannte Endsequenz.
- Vollsuche als Korrektheitsreferenz und Vergleich der Anzahl exakter Signatur-Lookups.
- Stabile IDs fuer Makrokandidaten und deterministische Tests.

## Herkunft / Grenzen
Die Routing-Idee orientiert sich an `reference/runtime/HierarchicalRouteIndex.kt`; die Kandidatenmetriken an `reference/forge/macro_discovery.py`. **Dies ist kein vollstaendiger Port** von `MemoryModel.kt`, `UniversalMacroCompiler.kt` oder der Forge-Discovery: weder Kandidaten-Promotion, nichtueberlappende Einsparungsrechnung, Persistenz der Kandidaten noch mehrstufige Kompression sind bereits integriert. Die ausgegebenen Einsparungen sind optimistische Schaetzungen, keine gemessenen Speichergewinne. Die Demo zeigt Lookup-Zahlen, keine validierten Laufzeit-Speedups. Noch keine autonome Erkenntnisbildung.

## Nächster Schritt
Persistente Online-Kandidaten und Promotion mit echten nichtueberlappenden Kompressionsmessungen; anschliessend Laufzeit- und Speichermessungen mit identischen Datensaetzen.
