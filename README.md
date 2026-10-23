# KIRA FOUNDATION v0.15 — Structural Macros

Windows: `START_STRUCTURAL.bat`; all tests: `TEST_ALL.bat`.

New: `foundation/structural_macros.py` discovers connected directed typed motifs of 1–3 edges in graphs derived from observed ID streams. Canonicalization enumerates vertex permutations (max 5 vertices), yielding stable ID-independent motif signatures. BLAKE2b motif IDs and per-stream evidence are stored in `data/structural_macros.sqlite`. Repeated analyses of the same stream are idempotent. The `shared` query returns motifs present in at least two streams, without confusing raw ID equality with structural equality.

Example: `py -3 structural_cli.py`. Optional: `--events path/to/event_graph.sqlite --streams streamA streamB`; use `--live-db path/to/live.sqlite` to import an audio ID stream. Audio import alone does not imply semantics. The CLI's default demo adds events on each run; learned motif evidence itself is deduplicated by stream.

**Limitations:** These are bounded subgraph *templates*, not recursively compressed stored graphs; a motif ID does not yet replace an underlying graph. Presence is counted per stream, not by occurrence frequency within a stream. No causal or semantic inference is performed. Isomorphic motifs may admit multiple node correspondences; a shared motif is not a unique transfer map. The upstream graph extractor retains its <=7-node limit and records observational temporal edges, not causes. Exhaustive canonicalization is deliberately bounded for small research graphs.

All v0.1–v0.14 components remain available. This version links event-graph extraction to reusable, ID-independent motif storage, without claiming general intelligence.
