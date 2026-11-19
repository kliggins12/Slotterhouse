# Refresh and Assumption Workflow

## Refresh Drawings

The manual Refresh Drawings action and any scheduled refresh must call the same ingestion service.

1. Fetch from a verified official Texas Lottery source or a documented trusted export.
2. Record source URL/feed identifier, fetch timestamp, checksum, parser version, and rules version.
3. Parse draw date, session, main numbers, and bonus numbers separately.
4. Validate field count, numeric ranges, duplicates, draw date, session, and applicable rule era.
5. Quarantine invalid rows with explicit reasons; never silently coerce malformed data.
6. Append only new valid draws. Repeated imports must be idempotent.
7. Rebuild affected row masks, Piece Journal entries, and transition counts.
8. Report per game: inserted, duplicate, rejected/quarantined, latest draw, and refresh status.

Prevent overlapping refresh jobs. Retries must be safe. Preserve previously verified records.

Suggested UI states: Idle, Fetching, Validating, Applying, Rebuilding, Complete, Partial, Failed.

## Markov analysis

Use first-order transitions as the baseline. For state i and destination j:

P(j | i) = count(i -> j) / total outgoing transitions from i.

Always show the supporting transition count. If state i has no observed outgoing transitions, show “insufficient evidence”; do not invent a probability. Keep models separate by game, row, and session where session boundaries apply. Sparse storage is required for wide rows.

## Building assumed combinations

For each row, rank next-shape candidates from the latest valid state and show evidence counts. Then assemble full-game candidates under the complete game constraints. Do not simply concatenate independently selected row states if the result violates a game's valid draw structure.

Candidate ranking may use a documented heuristic such as a sum of row log-scores. Because row states are dependent under fixed draw-size constraints, this score is not a calibrated joint probability.

Bonus balls are modeled separately from main-number grids. Rule changes require era-aware validation and configurations.

## Immutable assumption snapshots

Each generated assumption set records:
- target draw and game/session;
- generated-at timestamp;
- data cutoff for each stream;
- source checksums;
- rules, parser, and engine versions;
- row-state rankings, counts, and scores;
- final candidate combinations and constraints applied.

Lock the snapshot before the target draw. Do not rewrite it after results are known.

## Evaluation

After the actual draw is imported, compare it with the locked snapshot. Report main-number matches, bonus-ball matches separately, and historical comparison baselines where available. Keep assumptions distinct from actual outcomes. Do not claim that the method improves the odds of a lottery draw.
