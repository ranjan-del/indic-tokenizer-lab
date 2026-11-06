# Indic Tokenizer Lab

**A measurement-first research and engineering toolkit for understanding how tokenization affects Indian-language NLP and LLM systems.**

Indic Tokenizer Lab investigates a practical question: *when a model reads Indian languages, how much information, context budget, compute, and quality are lost or gained because of tokenization choices?* It is not intended to be another tokenizer implementation or a leaderboard of raw token counts. The project will provide reproducible diagnostics, controlled comparisons, and evidence-backed recommendations.

## Why this matters
Indic languages have diverse scripts, orthographic conventions, morphology, code-mixing, and normalization behavior. A tokenizer that looks efficient on English may fragment words in another language, consume more context-window budget, or create uneven representation across languages. Raw fertility alone is insufficient: normalization, byte fallback, vocabulary allocation, script coverage, and downstream task behavior also matter.

## Research questions
1. How do normalization and Unicode handling change token boundaries and round-trip fidelity?
2. How do tokenizers differ in fertility, byte fallback, sequence length, and vocabulary allocation across languages and domains?
3. Do fragmentation differences correlate with latency, memory, or task quality under controlled model conditions?
4. How do code-mixed text, transliteration, spelling variation, and noisy user input affect results?
5. Which diagnostics can identify unfair or fragile language coverage before model training?

## Scope and non-goals
**In scope:** tokenizer adapters, corpus sampling, normalization audits, language/script-aware metrics, reproducible reports, controlled downstream experiments, dataset provenance.

**Not in scope initially:** training a foundation model, claiming a universally best Indic tokenizer, scraping unlicensed corpora, or replacing established tokenizer libraries.

## Core capabilities (planned)
- Adapters for Hugging Face Tokenizers, SentencePiece, and compatible tokenizer APIs.
- Unicode/script audit: NFC/NFKC comparisons, combining marks, grapheme clusters, whitespace and punctuation behavior.
- Metrics: fertility, characters/bytes per token, sequence expansion, unknown/byte-fallback rate, token distribution, round-trip fidelity.
- Slice analysis by language, script, domain, code-mixing, and input quality.
- Reproducible benchmark manifests and machine-readable JSON/CSV outputs.
- Optional downstream probes that isolate tokenizer effects from model/training effects.

## Proposed architecture
See [architecture](docs/ARCHITECTURE.md), [research notes](docs/RESEARCH.md), and [roadmap](docs/ROADMAP.md).

## Quick-start target
The first release will accept a manifest of text samples and tokenizer adapters, run deterministic diagnostics, and export a report. The exact CLI and package API are design targets and may change during implementation.

## Evaluation principles
- Publish dataset source, license, language labels, sampling method, and exclusions.
- Report per-language and per-slice distributions; never hide weak slices behind a single aggregate.
- Separate tokenizer-only measurements from model-dependent outcomes.
- Pin tokenizer revisions, library versions, normalization settings, and random seeds.
- Do not infer language identity from personal or sensitive attributes.

## Current status
<badge>Research / design phase</badge>

No benchmark results are claimed yet. Results must be generated from documented runs before being reported.

## Development
See [CONTRIBUTING.md](CONTRIBUTING.md). Initial milestones and acceptance criteria are in [docs/ROADMAP.md](docs/ROADMAP.md).

## References
See [docs/RESEARCH.md](docs/RESEARCH.md) for primary papers, tools, datasets to evaluate, and a prior-art review checklist.
