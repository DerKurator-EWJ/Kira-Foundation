# KIRA FOUNDATION v0.8 — Online prediction research

Windows: double-click **START_PREDICTION.bat**. Python 3 required; no extra packages.

The v0.7 live runtime is extended with a **persistent variable-order transition predictor**. It counts next-token transitions for contexts of length 1–3, backs off to shorter contexts when necessary, and reports empirical conditional frequencies. A prediction is scored **before** its observed token is learned (prequential evaluation), avoiding training/test leakage for the current event. Counts, per-event prediction results, audio codebook, and observations are committed in one SQLite transaction.

### Try it

In the console, enter:

```text
start
step 100
status
predict
predictions 10
pause
stop
```

Restart with `START_PREDICTION.bat`; `status` and `predict` show the saved state. The runtime starts paused after each restart. You can also use `wav C:\Audio\test.wav 100` with compatible PCM WAV input.

`predict` shows the conditional distribution for the current token context. `predictions 10` shows previously issued predictions, observed outcomes and whether the most likely token matched. `status` includes cumulative top-1 accuracy **on events for which a prediction was available**. Ties break by numeric token ID.

### Limitations

- This is **statistical next-ID prediction**, not causal understanding, semantic learning, or autonomous cognition.
- There is no live microphone or idle-time processing. The `step` command generates synthetic audio.
- Prediction state is stored in the existing `data/live.sqlite` database; the bundled archive excludes experimental data.
- The predictor currently stores up to three prior IDs as context; it does not yet learn variable-order causal rules or handle concept drift with forgetting.
- Original v0.1–v0.7 tools remain available.

Run all tests: `TEST_ALL.bat` or `py -3 -m unittest discover -s tests -v`.
