# KIRA FOUNDATION v0.4 — Persistente und rekursive Makros

Windows: `START_COMPRESSION.bat` für die Demo, `TEST_ALL.bat` für alle Tests. Python 3.10+, keine Drittanbieterpakete. Enthält die bisherigen Versionen v0.1–v0.3.

## Neu
- `foundation/compression.py`: verlustfreie Wörterbuchkompression über numerische Token-IDs.
- Echte **nichtüberlappende** Ersetzungen statt bloßer Häufigkeitsschätzungen.
- Mehrstufige Makroregeln: spätere Regeln können frühere Makro-IDs referenzieren.
- SQLite-Journal für Ereignisse je Stream, persistente Kandidatenzählung (aus Ereignissen rekonstruierbar), gespeicherte Makroregeln und komprimierte Tokenfolgen.
- Roundtrip-Test: Die Originalfolge muss exakt rekonstruierbar sein.
- `compression_cli.py`: reproduzierbare Demo, Datenbank in `data/kira_research.sqlite`.

## Interpretation der Metriken
Die Einsparung wird in **abstrakten Token-Slots** berechnet: Anzahl kodierter Tokens + Anzahl der Einträge in den Makrodefinitionen einschließlich je eines Headers. Das ist keine Byte-Kompressionsrate und berücksichtigt weder SQLite-Indizes noch Metadaten, Bitbreiten oder Laufzeit-Overhead. Bei ungeeigneten Daten wird keine Regel angelegt.

## Grenzen
Dies ist ein eigenständiger Forschungsprototyp, **kein vollständiger Port** von Runtime `UniversalMacroCompiler` oder Forge `macro_discovery`. Die Online-Kandidaten werden aus persistenten Rohereignissen bei Bedarf neu gezählt; die Kompression läuft batchweise. Noch kein kausales Lernen, keine autonome Hypothesenbildung. Die Rohdaten bleiben aus Gründen der Nachprüfbarkeit gespeichert, deshalb sind die berichteten Token-Slot-Einsparungen **keine** tatsächlichen Gesamtspeichereinsparungen der Datenbank.
