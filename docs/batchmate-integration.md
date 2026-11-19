# Batchmate Integration Contract

## Relationship

Batchmate is the primary website and application. Slotterhouse is a helper add-on. Keep the two deployable independently.

## Non-negotiable preservation rule

Do not remove, rewrite, relocate, or alter Batchmate's existing Google AdSense loader, publisher ID, ad slot IDs, ad containers, or placements. Do not replace the Batchmate HTML page or its existing data pipeline as part of Slotterhouse work.

## Integration stages

### Stage 1 — link only

Add a clearly labeled link from Batchmate to the separately deployed Slotterhouse page. This is the preferred first integration because it does not couple the applications or risk the Batchmate page.

### Stage 2 — read-only export

If Batchmate exposes data for Slotterhouse, use a versioned JSON export with:
- schema version;
- game identifier and rules version;
- draw identifier, date, and session where applicable;
- main numbers and bonus numbers in separate fields;
- source provenance and update timestamp.

The Slotterhouse adapter validates the export before ingestion. Unknown schema versions are rejected with a clear error. Slotterhouse does not modify Batchmate's files or generated JSON.

### Stage 3 — optional API

Only after the export contract is stable, consider a read-only API. Authentication, rate limits, caching, and ownership must be specified before deployment.

## Existing Batchmate pipeline

Batchmate currently has its own static page and scheduled refresh pipeline. Slotterhouse must not replace or duplicate that pipeline blindly. Confirm actual CSV headers, date layouts, filenames, game rules, and historical rule eras before implementing any shared adapter.

## Acceptance checks

- Batchmate page still loads.
- All AdSense script tags, publisher identifiers, ad slots, and placements are unchanged.
- Existing Batchmate data files and refresh workflow remain operational.
- Slotterhouse can be deployed and tested independently.
