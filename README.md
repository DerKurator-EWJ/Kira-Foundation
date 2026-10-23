# KIRA FOUNDATION v0.7 — Windows research runtime

Built on v0.6. Run **START_LIVE.bat**, or `py -3 live_cli.py` from PowerShell. No third-party dependencies.

Commands: `help`, `start`/`resume`, `pause`, `step 100`, `wav C:\Audio\test.wav 100`, `status`, `macros 3`, `history 10`, `stop`.

- **Tick** increments once per ingested frame, not wall-clock time.
- **Incremental online macro counters** are updated per event for widths 2–6, without replaying the whole stream. These are candidate counts, **not** compressed hierarchies; the v0.6 batch compressor remains available separately.
- **Single SQLite transaction per observation** commits token, candidate counts, event log and serialized adaptive audio codebook together. This replaces the v0.6 separate JSON codebook **for live mode**. No guarantees against storage-device failures beyond SQLite's normal transactional guarantees.
- **Pause/resume** gates input processing. This is an interactive, command-driven process, **not** an autonomous background service or live microphone capture.
- Existing v0.1–v0.6 scripts remain available.
- A stored stream has fixed frame size and macro width; mismatched restarts are rejected.
- The runtime always starts paused after a restart. It never invents new input while idle.

Test with `TEST_ALL.bat` or `py -3 -m unittest discover -s tests -v`.

## Research boundaries
This is a bounded n-gram counter and transactional research runtime, not autonomous learning, causal discovery, or a complete Kotlin port. In particular, the existing compression pipeline is still a separate batch operation. Future versions should add atomic checkpoints for compression and tests for performance under large streams.
