# KIRA FOUNDATION v0.22 – Spuren und Zusammenhänge

Kira erhält einen **gemeinsamen Wahrnehmungskern**. Die neuen Werkzeuge heißen `Spur`, `MerkmalsMass`, `Zusammenhang`, `Band`, `Blicktiefe` und `Wahrnehmung` (Python-Klassennamen ohne Umlaute). Sie verarbeiten Merkmalsvektoren und Nachbarschaften unabhängig von Bild, Ton oder Text. Siehe `BEGRIFFE.md`.

## Start unter Windows

- `START_WAHRNEHMUNG.bat`: Demonstration mit drei Quellen und denselben Kernwerkzeugen.
- `START_INQUIRY.bat`: bisherige Fragenverwaltung.
- `TEST_ALL.bat`: sämtliche bisherigen und neuen Tests.

## Tatsächlicher Umfang

- Deterministische Kennungen für quantisierte Messwerte.
- Verbindung von Spuren bei **expliziter Nachbarschaft** und Merkmalsnähe.
- Priorisierte Auswahl von Verarbeitungsschritten unter einem festen Budget.
- Drei Beispiele mit identischem Kern und verschiedenen Herkunftsangaben.
- Vorherige Module und Startdateien bleiben erhalten.

**Noch nicht enthalten:** automatische Bild-/Audio-/Text-Merkmalsextraktion aus Rohdaten, zeitlich beständige Objektidentität, Sprachverständnis, Anschluss der neuen Bänder an das Langzeitgedächtnis und automatische Staunen-Fragen. Die Bild-/Ton-/Textbeispiele verwenden bewusst kleine vorgegebene Merkmalsvektoren. Die Kotlin-Referenzen liegen weiterhin unter `reference/`. Der Kern ist eine getestete Schnittstelle, noch keine vollständige audiovisuelle Integration.


## v0.23 – Wiedererkennung

`START_WIEDERERKENNUNG.bat` demonstriert die Wiedererkennung ähnlicher Beobachtungen über mehrere Schritte. `foundation/wiedererkennung.py` arbeitet mit allgemeinen Merkmalsvektoren und optionaler Lage. Auch Audio- oder Textadapter können die Schnittstelle nutzen. Es handelt sich um einen einfachen Zuordner mit Schwellwerten, nicht um eine erlernte Identität, Bewegungsprognose oder echte Videoanalyse. `baender_als_sichten` verbindet den neuen Zuordner mit den Bändern aus v0.22. Zustände lassen sich als JSON sichern und laden.
