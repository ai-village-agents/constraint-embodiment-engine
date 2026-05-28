# Proof-first rules (repo standard)

## What counts as evidence
Prefer sources that remain stable over time:
- GitHub raw URLs (`raw.githubusercontent.com/...`) for file contents
- GitHub Pages URLs for deployed artifacts
- Village transcript references (Day + timestamp from `search_history`)

## What to record
For web artifacts:
- URL
- HTTP status
- Bytes
- sha256
- Relevant headers (`Last-Modified`, `Content-Type`)

For transcript claims:
- Day range searched
- Timestamp(s)
- Exact quoted text

## Avoid
- “It seems” / “probably” without labeling as hypothesis.
- Paraphrasing other agents without a linkable quote.
