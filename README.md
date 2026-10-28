# Sports card scanner — catalog data

Catalog data for a personal-use sports card scanning app: photograph a card,
identify it against this catalog, and price it from eBay sold listings.
No paid APIs, no server, no keys — the app fetches these CSV files directly
and does everything else on the phone.

## Files

- `2025-topps-series-1-baseball.csv` — the full 2025 Topps Series 1 Baseball
  checklist: 30,804 rows across 533 subsets (base, rookies, league leaders,
  team cards, every parallel, inserts, autographs, and relics).

## Columns

| Column | Meaning |
| --- | --- |
| year | Release year |
| manufacturer | Card manufacturer (Topps) |
| product | Full product name |
| subset | Subset / parallel name as listed on the checklist (e.g. `Base`, `Base Gold`, `Base Rookie`, `1990 Topps Baseball Autographs Gold`) |
| card_number | Card number within the subset, as printed (numeric or alphanumeric, e.g. `1`, `90A-AA`) |
| player | Player / subject name |
| team | Team as listed |
| print_run | Serial-numbered print run where the card is numbered (e.g. `2025`, `99`, `1`); empty when unnumbered |
| is_rookie | 1 if the row is a rookie card |
| is_autograph | 1 if the row is an autograph card |
| is_relic | 1 if the row is a memorabilia / patch card |

## Source

Transcribed from the 2025 Topps Series 1 Baseball checklist spreadsheet
published by ChecklistCenter (a republication of Topps' official checklist),
downloaded October 28, 2026, and converted to CSV with no rows added, removed,
or renamed — only columns normalized and flags derived from subset names.

## Adding sets

Add one CSV per product under this folder, using the same columns, and the app
picks it up from the same location. The data-source layer is deliberately
swappable: this CSV can later be replaced by a keyed catalog API without
reworking identification or pricing.

## Fetching

The app fetches the raw file over HTTPS, no authentication:

`https://raw.githubusercontent.com/JeremyShanebrook/sports-card-scanner/main/catalog/2025-topps-series-1-baseball.csv`
