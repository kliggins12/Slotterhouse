# Slotterhouse

Slotterhouse is a helper add-on for **Batchmate**. Batchmate remains the primary website and application; Slotterhouse provides complementary drawing-history analysis, exact-position shape tracking, Markov transition analysis, and constrained assumption building.

## Relationship to Batchmate

- Batchmate remains the primary application and source of its existing lottery data and analytics.
- Slotterhouse is maintained as a separate add-on so its development does not require replacing Batchmate's pipeline or page.
- Integration should begin with a link from Batchmate to Slotterhouse and a documented, versioned data exchange contract.
- Existing Batchmate Google AdSense scripts, publisher identifiers, ad slots, containers, and placements must be preserved. Slotterhouse work must not remove or rewrite them.

## Core capabilities

1. Import and validate official Texas Lottery drawing history.
2. Record each grid-row observation in a chronological Piece Journal.
3. Track exact binary shapes and position changes between consecutive observations.
4. Build sparse, evidence-counted Markov transition models without crossing invalid records or session boundaries.
5. Generate constrained candidate combinations while keeping assumptions separate from actual results.
6. Refresh source data on demand and report new, duplicate, and rejected records.

## Design principles

- Preserve source provenance, checksums, parser versions, and game-rule versions.
- Keep historical records immutable; imports must be idempotent.
- Do not fabricate transition probabilities when evidence is absent.
- Enforce each game's valid number counts, ranges, and bonus-ball separation.
- Label generated combinations as analytical assumptions, not predictions or improved odds.

## Project status

This repository is being initialized. The first implementation milestone is the data contract, game configurations, Piece Journal, and tested shape/transition engine. Web and Android clients follow after the data and engine interfaces are stable.
