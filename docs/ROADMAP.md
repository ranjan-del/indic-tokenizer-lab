# Roadmap — Indic Tokenizer Lab

## Phase 0 — Research validation
- [ ] Build a paper matrix covering Indic and multilingual tokenizer diagnostics.
- [ ] Verify dataset licenses and select a small legally usable pilot corpus.
- [ ] Finalize metric definitions and language/script slice taxonomy.
**Exit:** novelty statement is specific; data permissions and benchmark protocol are documented.

## Phase 1 — Minimal reproducible benchmark
- [ ] Define corpus manifest schema.
- [ ] Define tokenizer adapter protocol.
- [ ] Implement two adapters (e.g. Hugging Face fast tokenizer and SentencePiece).
- [ ] Implement fertility, bytes/code points per token, sequence expansion, round-trip checks.
- [ ] Export JSON and CSV with run metadata.
**Exit:** same run can be reproduced from manifest + pinned revisions.

## Phase 2 — Indic diagnostics
- [ ] Add Unicode normalization variants and grapheme-aware diagnostics.
- [ ] Add language, script, domain, and code-mix slices.
- [ ] Add paired comparisons and confidence intervals.
- [ ] Add edge-case fixtures for combining marks, punctuation, numerals, and mixed scripts.
**Exit:** report makes slice-level weaknesses visible.

## Phase 3 — Runtime and downstream probes
- [ ] Add encoding/decoding throughput tests.
- [ ] Add controlled model probes where model and prompt conditions can be held constant.
- [ ] Document limits of causal interpretation.
**Exit:** tokenizer effects are separated from model and infrastructure effects.

## Phase 4 — Research release
- [ ] Publish benchmark card and limitations.
- [ ] Publish reproducibility bundle and example report.
- [ ] Invite external tokenizer/dataset maintainers to review adapter behavior.
**Exit:** results are independently reproducible and no unsupported superiority claims remain.

## Deferred
Training a new tokenizer, proposing a new vocabulary, or training a model is deferred until diagnostics reveal a well-defined gap.
