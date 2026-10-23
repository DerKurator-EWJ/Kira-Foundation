# KIRA FOUNDATION v0.5 — Audioquantisierung (Windows)

Enthält die Module aus v0.1–v0.4 sowie `foundation/audio.py`.

## Start
- `START_AUDIO.bat` startet einen reproduzierbaren synthetischen Audiotest und eine FFT-Referenz.
- `TEST_ALL.bat` führt sämtliche automatischen Tests aus.
- Eigene WAV-Datei: `py -3 audio_cli.py --wav "C:\Pfad\aufnahme.wav" --frames 100 --benchmark`
- WAV muss **mono, unkomprimiertes 16-bit PCM** sein. Frames standardmäßig 1024 Samples.
- Der gelernte Codebook-Zustand liegt in `data/audio_codebook.json`; zum Reset diese Datei löschen.

## Ursprung und Port-Status
Die 6 Zeitbereichsmerkmale, Lag-Korrelation, adaptive Prototypen, Radii, ID-Zuweisung und PLAY-Modus sind an `reference/runtime/AdaptiveAudioQuantizer.kt` aus Kira v0.9.8 angelehnt. Das Kotlin-Original ist unverändert beigefügt. Der Python-Port ist eine **experimentelle Übertragung**, keine geprüfte bitgenaue Parität mit Android. Die Kandidatensuche bildet die lokalen Buckets ab, aber nicht den Kotlin-Index als Datenstruktur; für Performancevergleiche ist das relevant.

## FFT-Vergleich und Grenzen
`fft_magnitudes` ist eine reine Python-Radix-2-FFT als **mathematische Referenz**. Sie berechnet ein volles Magnitudenspektrum. Der adaptive Konverter liefert dagegen 6 Zeitbereichsmerkmale und eine gelernte ID. **Das sind nicht dieselben Aufgaben.** Laufzeiten dürfen nicht als Beleg verwendet werden, dass eine Methode generell schneller ist. Für eine faire Bewertung fehlen aufgabenidentische Erkennungsziele, standardisierte Datensätze, optimierte FFT-Implementierung (z. B. NumPy), Qualität/Fehlerraten und RAM-Messungen für beide vollständigen Pipelines. Der ID-Stream ist verlustbehaftet; die früheren verlustfreien Kompressionstests beziehen sich auf ID-Sequenzen, nicht auf Rekonstruktion der ursprünglichen Audiodaten.

## Weitere Grenzen
Kein Echtzeit-Mikrofon, kein visuelles Quantisieren, kein Ghost-Lernen, keine Kotlin-Gegenprüfung. Das bestehende v0.4-Projekt wird nicht überschrieben.
