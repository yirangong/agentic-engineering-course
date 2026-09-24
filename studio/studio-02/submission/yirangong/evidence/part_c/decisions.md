# Decisions

- 2026-09-24 — Storage format: Store notes as JSON Lines (JSONL), one JSON object per note, because it is append-friendly while remaining easy to inspect and parse.
- 2026-09-24 — Command name: Use `note`, because it is short, memorable, and clearly communicates the tool’s purpose.
- 2026-09-24 — Date format: Record each note’s date in ISO 8601 format (`YYYY-MM-DD`), because it is unambiguous and sorts chronologically.
- 2026-09-24 — Fibonacci implementation: Start the sequence at 0 and generate it iteratively, because this produces the conventional first 20 terms with simple constant-space logic.
