# Contributing

Contributions should improve reproducibility, correctness, language coverage, or interpretability.

## Before opening an issue
Include the tokenizer/library version, corpus manifest (or a safe synthetic reproduction), normalization policy, expected behavior, and actual behavior. Never attach private or restricted text.

## Pull requests
- Add tests for Unicode and multilingual edge cases.
- Keep normalization explicit; do not silently transform inputs.
- Document metric definitions and limitations.
- Pin or record external versions.
- Do not add datasets unless redistribution rights are clear.
- Avoid claims such as “best tokenizer” without a reproducible protocol and evidence.

## Development status
The API is not stable yet. Open an issue before building a large integration against an unreleased interface.
