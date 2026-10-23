# KIRA FOUNDATION v0.2 — ID Language

Windows: `START_LANGUAGE.bat` starten. Tests: `TEST_LANGUAGE.bat`.

PowerShell:
```powershell
py -3 language_cli.py examples\fabric.eqx
py -3 language_cli.py examples\tree.eqx
py -3 language_cli.py examples\forest.eqx
py -3 -m unittest discover -s tests -v
```

Die v0.1-Dateien `main.py`, `START_KIRA.bat`, `TEST_KIRA.bat` bleiben erhalten. Python-Standardbibliothek genügt.

## Implementierung

`foundation/language.py` ist ein Python-Port der drei Interpreter-Modi aus `reference/runtime/EquinoxMindCore.kt`:
- `FABRIC`: `WORK`/`RUN`, neun Operationen (`RELATE`, `SPLIT`, `MIRROR`, `UNIFY`, `DISSONATE`, `HOLD`, `WAKE`, `SEAL`, `EMIT`), numerische runtime-IDs und tickbasierte Ausführung.
- `TREE`: `THESIS`, `ANTITHESIS`, `MIRROR`, `SEAL`, `WAKE`, `EXTINCT`; strukturelle Tripel.
- `FOREST`: `BEGIN_TREE`, `RELATE`, `EXTERNAL`, `REFINE`, `RUN`, `SETTLE`, `SETTLE_ALL`, `SEAL_FOREST`.

`language_cli.py` schreibt erzeugte numerische Tripel in die vorhandene SQLite-Tabelle `triples` (ID-Schema `runtime`). Sie sind nicht automatisch symbolisch rückauflösbar, weil abgeleitete IDs keine Identitätszuordnung haben. `--no-save` vermeidet Änderungen an der DB.

## Grenzen

Die Original-Implementierung ist ein **regelbasierter Interpreter**, kein selbstlernender Ghost. Die Portierung übernimmt die definierten Befehlswirkungen, nicht die Android-Oberfläche. Eine vollständige Kotlin↔Python-Ausgabevalidierung über dieselben Testvektoren steht noch aus. Speziell die Stringbildung für MIRROR bei mehreren Tripeln sollte vor Produktiveinsatz gegen Kotlin gegengeprüft werden. Die Quelldatei liegt unverändert unter `reference/runtime/`.
