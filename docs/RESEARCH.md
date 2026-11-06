# Research brief — Indic Tokenizer Lab

## 1. Problem framing
Tokenization is a model-interface decision with consequences for context length, compute, language coverage, and text fidelity. For Indian languages, comparisons must account for script and orthographic variation, morphology, code-mixing, transliteration, and noisy real-world text. A single average tokens-per-word number can conceal severe language- or domain-specific failure.

## 2. Research hypotheses (to test, not assume)
- H1: Token fertility and sequence expansion vary substantially by language, script, domain, and tokenizer family.
- H2: Unicode normalization and grapheme handling can change segmentation and round-trip behavior for visually similar strings.
- H3: High fragmentation may increase inference cost for a fixed semantic input, but the effect depends on model architecture, batching, cache behavior, and implementation.
- H4: Tokenizer-only metrics do not reliably predict downstream quality; controlled model-based probes are needed.
- H5: Code-mixed and transliterated text needs separate slices rather than being merged into monolingual language scores.

## 3. Prior-art landscape
This project must build on, not repackage, existing work:
- **SentencePiece**: language-independent subword tokenizer framework and Unigram/BPE implementations.
- **Hugging Face Tokenizers / Transformers**: widely used tokenizer APIs and serialization formats.
- **Indic language resources and benchmarks**: evaluate datasets such as FLORES-200 and AI4Bharat resources only after checking their current cards, terms, and permitted use.
- **Tokenizer research**: review recent work on multilingual tokenization, vocabulary allocation, byte-level approaches, grapheme-aware tokenization, and Indic-specific tokenization before finalizing novelty claims.
- **Evaluation suites**: downstream tasks should use established task definitions where possible; this repository's contribution is controlled tokenizer diagnostics and reproducibility.

A prior-art review should include recent ACL Anthology findings on Indic tokenization, MUTANT-style multilingual tokenization analysis, and grapheme-based tokenizer research. Verify titles, publication versions, and claims directly from the papers before citing them in any publication. The existence of related recent work means “compare tokenizers for Indic languages” alone is not a novelty claim.

## 4. Proposed contribution
The differentiator is a **diagnostic protocol and reproducible evidence pipeline**:
1. A common adapter contract across tokenizer families.
2. A corpus/slice manifest that records provenance and language/script metadata.
3. Unicode and round-trip audits alongside conventional fertility metrics.
4. Paired comparisons on identical samples, with uncertainty intervals.
5. Optional model-controlled experiments to distinguish tokenization effects from model differences.
6. A report format that exposes failures by slice rather than collapsing them into one rank.

## 5. Metrics
| Metric | Definition / use | Caveat |
|---|---|---|
| Token fertility | Tokens per whitespace-delimited word or annotated lexical unit | Word segmentation differs across languages |
| Characters per token | Unicode code points per token | Code points are not grapheme clusters |
| Bytes per token | UTF-8 bytes represented per token | Useful for storage/sequence diagnostics, not quality |
| Sequence expansion | Token count relative to a documented baseline | Baseline must be stated |
| Byte/unknown fallback rate | Share of input represented through fallback paths | Tokenizer-specific APIs differ |
| Round-trip fidelity | Decode(encode(text)) compared with normalized input | Must state normalization policy |
| Boundary stability | Segmentation change under benign orthographic variants | Define variants carefully |
| Token distribution | Frequency, tail, and concentration statistics | Corpus composition strongly affects it |
| Latency / throughput | Encode/decode runtime under fixed conditions | Hardware, batch size, and implementation matter |

Always report sample count and distribution (median, percentiles, tails), not only a mean.

## 6. Dataset and governance plan
Start with small, legally usable, documented samples. Candidate sources include FLORES-200, Common Voice text/transcripts, and AI4Bharat datasets; each source must be checked individually for license, consent, redistribution, and research-use restrictions. Do not assume that a dataset's public availability grants redistribution rights.

Each corpus manifest should record:
- source URL and version or commit;
- license and access date;
- language and script labels, including label confidence;
- domain and collection method;
- filtering, deduplication, and normalization steps;
- sample counts and exclusion reasons;
- whether text may be redistributed or only referenced by ID.

Prefer publishing manifests, scripts, and aggregate results over redistributing source text where terms are unclear.

## 7. Experimental protocol
1. Freeze corpus snapshot and tokenizer revisions.
2. Define language/domain slices before looking at results.
3. Run the same inputs through every tokenizer adapter.
4. Verify decode/encode behavior and normalization.
5. Compute metrics per sample, then aggregate by slice.
6. Bootstrap confidence intervals for paired differences where appropriate.
7. Publish raw machine-readable outputs and environment metadata.
8. Repeat runs to estimate runtime variance.

## 8. Risks and mitigations
- **Metric gaming:** report multiple complementary measures and downstream checks.
- **Corpus bias:** disclose source/domain composition and slice sizes.
- **Normalization destroys distinctions:** retain original input and make transforms explicit.
- **Language-label noise:** track confidence and allow mixed/unknown categories.
- **False novelty:** maintain a paper-by-paper related-work table before public claims.
- **License violations:** do not bundle corpora without explicit redistribution permission.

## 9. Primary references and starting points
- SentencePiece: https://github.com/google/sentencepiece
- Hugging Face Tokenizers: https://github.com/huggingface/tokenizers
- Hugging Face Transformers: https://github.com/huggingface/transformers
- FLORES-200 dataset: https://huggingface.co/datasets/facebook/flores
- ACL Anthology search: https://aclanthology.org/
- AI4Bharat: https://ai4bharat.org/

These are starting points, not endorsements or proof of compatibility. Check current versions, papers, and licenses before using them.
