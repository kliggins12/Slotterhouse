# Roadmap

## Milestone 1 — data foundation
- [x] Initialize repository and define Slotterhouse as Batchmate's helper add-on.
- [ ] Confirm official source URLs, CSV schemas, game rules, and historical rule eras.
- [ ] Finalize versioned game configuration and draw export schema.
- [ ] Implement canonical draw records, provenance, validation, and idempotent imports.

## Milestone 2 — Piece Journal and engine
- [ ] Implement exact row-shape encoding and decoding.
- [ ] Implement XOR-based position change analysis.
- [ ] Implement chronological Piece Journal storage and filters.
- [ ] Implement sparse first-order transition counts and evidence display.
- [ ] Add deterministic unit and integration tests.

## Milestone 3 — refresh and assumptions
- [ ] Add user-triggered refresh with clear progress and result reporting.
- [ ] Add valid-combination constraints for every supported game and rule era.
- [ ] Generate ranked assumption sets with immutable snapshots.
- [ ] Lock assumptions before target draws and evaluate after actual results arrive.

## Milestone 4 — user interface
- [ ] Build responsive web/PWA views for dashboard, journal, trails, refresh, and assumptions.
- [ ] Add CSV/JSON export.
- [ ] Link Slotterhouse from Batchmate without changing Batchmate's existing page behavior or AdSense.

## Milestone 5 — Android
- [ ] Stabilize API and shared data contracts.
- [ ] Build Android client against the same API and engine outputs.
- [ ] Test on the target Samsung tablet and low-resource devices.

## Release gates

- No unverified source schema or game range is hard-coded as final.
- Invalid data is quarantined, not silently repaired.
- Exact shapes remain position-sensitive.
- Models do not cross prohibited stream/session boundaries.
- Full-game candidates satisfy all current rule constraints.
- Assumptions remain separate from actual results.
- Batchmate's existing AdSense and pipeline are preserved.
