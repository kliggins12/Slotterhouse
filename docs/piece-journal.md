# Piece Journal

## Purpose

The Piece Journal records each grid-row observation as an individual, chronological piece so a user can trace how an exact shape changes over time.

## Observation identity

Each journal entry includes:
- game and rules/configuration version;
- stream or session;
- draw ID, draw date, and chronological sequence;
- row ID and row label;
- grid width;
- exact left-to-right binary shape;
- integer bitmask representing that exact shape;
- hit count;
- source numbers or source-number references;
- source record ID, checksum, parser version, and ingestion timestamp.

The shape string is canonical and position-sensitive. For a width-four row, 1100, 0110, and 1001 are different shapes even though each contains two hits. Do not merge them by hit count.

## Transitions

For adjacent valid observations in the same stream and row, record:
- previous shape and current shape;
- XOR mask and changed column positions;
- gained positions (0 to 1);
- lost positions (1 to 0);
- retained positions (1 to 1);
- hit-count delta;
- draw interval and calendar-day gap;
- observed transition count and empirical conditional frequency when evidence exists.

Do not create a transition across a missing, invalid, or quarantined draw. Session-specific models must not cross session boundaries. Any combined stream must have an explicitly defined chronological ordering and must remain a separate model.

## Core views

1. **Shape history:** every occurrence of an exact shape, with prior and next shapes.
2. **Position trail:** follow a selected cell/column through time.
3. **Trail explorer:** traverse backward and forward through linked observations.
4. **Recurrence:** first seen, last seen, occurrence count, and gaps between occurrences.
5. **Filters:** game, session, row, date range, exact shape, and hit count.
6. **Export:** CSV and JSON for filtered journal entries and transitions.

## Optional equivalence views

Mirrors, rotations, or shifts may be offered as secondary exploratory groupings. They must never replace exact shape identity or alter the canonical transition history.
