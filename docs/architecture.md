# Architecture

## Product boundary

Batchmate is the primary website/application. Slotterhouse is a separately maintained helper add-on. Slotterhouse must not replace Batchmate's draw ingestion, analytics, page, or deployment workflow.

The initial integration is deliberately loose:
1. Batchmate links to the Slotterhouse experience.
2. Batchmate may later publish a versioned, read-only draw export.
3. Slotterhouse consumes that export through a validated adapter.
4. Slotterhouse never writes into Batchmate's source data or pipeline.

All changes to Batchmate must be separately reviewed. Preserve every existing AdSense loader, publisher identifier, ad slot, container, and placement.

## Logical components

- **Source adapters:** retrieve official Texas Lottery history and/or consume a versioned Batchmate export.
- **Validation and ingestion:** parse, validate, deduplicate, quarantine invalid records, and preserve provenance.
- **Canonical draw store:** immutable actual drawing records with game-rule and source versions.
- **Grid encoder:** maps each valid draw to exact row bitmasks.
- **Piece Journal:** chronological row observations and their provenance.
- **Transition engine:** sparse, evidence-counted first-order Markov transitions.
- **Assumption engine:** ranks row-state candidates and assembles only globally valid game combinations.
- **Evaluation service:** compares locked assumptions with later actual results.
- **API:** exposes refresh, journal, transition, assumption, and evaluation operations.
- **Clients:** responsive web/PWA first; Android client after shared contracts stabilize.

## Deployment direction

Keep the analytical engine independent of the UI. Use Python for ingestion and analysis, with a small API boundary. SQLite is suitable for local and lightweight deployments; a server database can be introduced if multi-user hosting requires it. The web client should consume documented API contracts rather than duplicate lottery logic.

## Data integrity

Every imported draw records its source, source URL or feed identifier, fetched-at timestamp, source checksum, parser version, rules/configuration version, and validation result. Imports are idempotent. Actual draw records are immutable; corrections are represented as audited source revisions rather than silent overwrites.

## Statistical limitations

A transition frequency is an empirical historical frequency, not a guarantee of future behavior. If no outgoing transition exists for a state, report insufficient evidence. Row states within a draw are constrained and dependent; multiplying row-level scores does not create a calibrated joint probability. Candidate rankings must be labeled heuristic, not odds improvement or a prediction.
