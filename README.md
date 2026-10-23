# KIRA FOUNDATION v0.6 – Durchgängige Audiopipeline (Windows)

Enthält v0.1–v0.5 unverändert und ergänzt `foundation/pipeline.py`, `pipeline_cli.py` und Integrationstests.

## Start
- `START_PIPELINE.bat` führt ein deterministisches Experiment mit 80 synthetischen Audioframes aus.
- `TEST_ALL.bat` führt sämtliche Tests aus.
- PowerShell: `py -3 pipeline_cli.py --wav "C:\Audio\test.wav" --frames 100 --stream audio:aufnahme1`
- WAV: unkomprimiertes Mono, 16-bit PCM. Standardframegröße 1024 Samples.
- `--db` und `--codebook` setzen Speicherorte. `--stream audio:<name>` trennt Ereignisfolgen.
- Bei jedem Start werden neue Frames **angehängt**. Zum Zurücksetzen `data/pipeline.sqlite` und `data/pipeline_codebook.json` löschen (bei geschlossenem Programm).

## Pipeline
PCM -> sechs Zeitbereichsmerkmale -> adaptives Codebuch -> numerische ID -> SQLite-Ereignisstream -> Online-Makrokandidaten -> hierarchischer Routing-Index -> rekursive ID-Kompression -> verlustfreie ID-Rekonstruktion.

`pipeline_cli.py` zeigt Ereigniszahl, eindeutige IDs, Kandidatenzahl, Routing-Probe, Kompressions-Slot-Bilanz und Roundtrip-Prüfung. `analyze()` konsolidiert aus dem **gesamten gespeicherten Stream** erneut; Online-Kandidaten werden aktuell ebenfalls aus dem gespeicherten Stream neu aufgebaut. Das ist noch keine inkrementelle kontinuierliche Makro-Promotion.

## Grenzen
- Die Quantisierung ist **verlustbehaftet**. Nur die ID-Sequenz kann aus der komprimierten Repräsentation verlustfrei wiederhergestellt werden, **nicht** das ursprüngliche Audio.
- Token-Slots sind keine gemessenen Bytes/RAM. Die Datenbank bewahrt Rohereignisse zusätzlich auf.
- Codebook JSON und SQLite werden **nicht atomar gemeinsam** geschrieben. Ein Absturz während der Verarbeitung kann inkonsistente Zustände hinterlassen; für produktiven Dauerbetrieb braucht es Transaktions-/Recovery-Design.
- `AdaptiveAudio` hat aktuell eine lineare Prototypensuche trotz Bucket-Filter; keine gesicherte Kotlin-Parität oder Echtzeit-Performance.
- Keine autonome Hypothesenbildung, keine Sprachbedeutung, kein Ghost. Keine Aussage über FFT-Überlegenheit.
- Die ursprüngliche v0.5 bleibt erhalten.
