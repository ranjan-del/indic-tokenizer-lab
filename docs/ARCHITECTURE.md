# Architecture — Indic Tokenizer Lab

## Design goals
- Add tokenizer implementations without changing benchmark logic.
- Make every result traceable to exact inputs, tokenizer revisions, and configuration.
- Preserve original text while making normalization an explicit experimental variable.
- Support offline/reproducible execution where dependencies permit.

## Pipeline
```text
Corpus manifest
   -> loader + provenance validation
   -> text integrity / language-slice validation
   -> normalization variants (explicit, opt-in)
   -> tokenizer adapter registry
   -> encode / decode / timing
   -> per-sample metric records
   -> slice aggregation + uncertainty
   -> JSON / CSV / Markdown report
```

## Proposed modules
- `datasets/`: manifest schema, loaders, provenance metadata; no implicit corpus downloads.
- `normalization/`: Unicode normalization and transformation policies.
- `adapters/`: tokenizer interface and implementations.
- `metrics/`: fertility, sequence expansion, fallback, round-trip, boundary stability.
- `runner/`: deterministic orchestration, batching, seeds, environment capture.
- `reports/`: JSON schema, CSV export, Markdown summaries and plots.
- `probes/`: optional downstream/model-based experiments, kept separate from tokenizer-only metrics.
- `tests/`: Unicode edge cases, adapter conformance, deterministic fixtures.

## Adapter contract (initial proposal)
An adapter should expose:
- stable tokenizer identifier and immutable revision;
- encode(text, settings) returning token IDs and optional offsets;
- decode(ids, settings);
- vocabulary size and special-token metadata when available;
- fallback/unknown-token diagnostics when supported;
- dependency/version metadata.

Adapters must not silently normalize text. The runner owns the normalization policy and records it.

## Data model
Every run should include:
- run ID, timestamp, git revision, environment;
- corpus manifest hash and sample identifiers;
- tokenizer name, revision, configuration hash;
- normalization policy;
- metric definitions and version;
- per-sample outputs and aggregated slice summaries.

Avoid storing raw text by default in public result artifacts. Support private/local raw-input retention for debugging where permitted.

## Reliability and performance
- Stream large corpora rather than loading everything into memory.
- Batch encoding where adapters support it, while preserving per-sample attribution.
- Separate cold-start and steady-state timing.
- Record hardware/software environment; never compare timings across unlike environments as if directly equivalent.
- Fail loudly on unsupported adapter features rather than silently substituting metrics.

## Security and privacy
Treat input corpora as untrusted. Avoid logging raw user text by default. Document retention behavior and never upload private corpora automatically.
