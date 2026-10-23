# KIRA FOUNDATION v0.1 — Windows Forschungsprototyp

**Lauffähiger Python-Prototyp**, keine vollständige Portierung der Android-Runtime oder Forge.

## Start
Im entpackten Ordner PowerShell öffnen:

```powershell
py -3 main.py demo
py -3 main.py compare --namespace node --symbol fraggle
py -3 -m unittest discover -s tests -v
```

Alternativ `START_KIRA.bat` und `TEST_KIRA.bat` doppelklicken. Nur Python 3 nötig (keine pip-Abhängigkeiten). Die Datenbank wird unter `data/kira_foundation.sqlite` angelegt.

## Tatsächlich implementiert
- Zwei **getrennte**, quellcodegetreu in Python nachgebildete ID-Konventionen: Runtime `EQXNUM01` und Forge `EQNXID44`, BLAKE2b/8 Byte, Big-Endian-Interpretation, 63-Bit-Maske, 0→1.
- ID-Vergleich ohne stille Umnummerierung.
- Kleiner SQLite-Speicher für kanonische (Subjekt, Prädikat, Objekt)-Tripel, mit scheme-getrennten IDs, Kollisionserkennung und Wiederöffnung.
- Fünf automatische Unit-Tests.
- Originalauszüge aus beiden Projekten unter `reference/` zum Nachprüfen.

## Noch **nicht** implementiert
- Kotlin-Ausführung / bytegenauer Cross-Language-Test gegen JVM; die Python-Ports folgen den gelesenen Algorithmen.
- Migration vorhandener BASE- oder Android-Datenbanken; dafür fehlt noch ein geprüfter Mapping-Vertrag.
- Original-MindCore-Interpreter, Makrocompiler, Forge-Aggregation, adaptive Audio-/Videoquantisierung, ID-Matrix-UI, Ghost-Lernen.
- Nachweis von Geschwindigkeit, Erkenntnisfähigkeit oder Effizienzvorteilen.

## Technische Entscheidung
**Kein** vereinheitlichter Hash-Personalisierungswert wurde erfunden. Beide ID-Räume bleiben versioniert erhalten. Vor einer Migration brauchen wir Inventur aller auf IDs beruhenden Formate und ein explizites Migrationsschema.

Quelle: `Kira_v0_9_8_BasePackage_HotMount(4).zip`, enthaltene Dateien `EquinoxId64.kt` und `canonical_id_space.py`.
