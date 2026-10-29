# Sports card scanner — catalog data

Catalog data for a personal-use sports card scanning app: photograph a card,
identify it against this catalog, and price it from eBay sold listings.
No paid APIs, no server, no keys — the app fetches these CSV files directly
and does everything else on the phone.

## Files

24 files, 358,788 rows. Mainline Topps flagship Series 1, Series 2, and
Update, plus standalone Topps Holiday (Christmas) sets.

- `2020-topps-series-1-baseball.csv` — 2020 Topps Series 1 Baseball:
  12,119 rows across 137 subsets.
- `2021-topps-series-1-baseball.csv` — 2021 Topps Series 1 Baseball:
  12,645 rows across 144 subsets.
- `2021-topps-update-series-baseball.csv` — 2021 Topps Update Series Baseball:
  9,960 rows across 109 subsets.
- `2021-topps-holiday-baseball.csv` — 2021 Topps Holiday Baseball:
  1,427 rows across 19 subsets.
- `2022-topps-series-1-baseball.csv` — 2022 Topps Series 1 Baseball:
  13,369 rows across 161 subsets.
- `2022-topps-series-2-baseball.csv` — 2022 Topps Series 2 Baseball:
  11,676 rows across 147 subsets.
- `2022-topps-update-series-baseball.csv` — 2022 Topps Update Series Baseball:
  11,650 rows across 133 subsets.
- `2022-topps-holiday-baseball.csv` — 2022 Topps Holiday Baseball:
  1,483 rows across 28 subsets.
- `2023-topps-series-1-baseball.csv` — 2023 Topps Series 1 Baseball:
  12,189 rows across 135 subsets.
- `2023-topps-series-2-baseball.csv` — 2023 Topps Series 2 Baseball:
  13,729 rows across 160 subsets.
- `2023-topps-update-series-baseball.csv` — 2023 Topps Update Series Baseball:
  13,846 rows across 162 subsets.
- `2023-topps-holiday-baseball.csv` — 2023 Topps Holiday Baseball:
  1,856 rows across 28 subsets.
- `2024-topps-series-1-baseball.csv` — 2024 Topps Series 1 Baseball:
  20,043 rows across 164 subsets.
- `2024-topps-series-2-baseball.csv` — 2024 Topps Series 2 Baseball:
  18,297 rows across 204 subsets.
- `2024-topps-update-series-baseball.csv` — 2024 Topps Update Series Baseball:
  18,870 rows across 161 subsets.
- `2024-topps-holiday-baseball.csv` — 2024 Topps Holiday Baseball:
  3,723 rows across 42 subsets.
- `2025-topps-series-1-baseball.csv` — the full 2025 Topps Series 1 Baseball
  checklist: 30,804 rows across 533 subsets (base, rookies, league leaders,
  team cards, every parallel, inserts, autographs, and relics).
- `2025-topps-series-2-baseball.csv` — 2025 Topps Series 2 Baseball:
  29,545 rows across 513 subsets.
- `2025-topps-update-series-baseball.csv` — 2025 Topps Update Series Baseball:
  25,870 rows across 264 subsets.
- `2025-topps-holiday-baseball.csv` — 2025 Topps Holiday Baseball:
  969 rows across 19 subsets.
- `2026-topps-series-1-baseball.csv` — 2026 Topps Series 1 Baseball:
  31,546 rows across 261 subsets.
- `2026-topps-series-2-baseball.csv` — 2026 Topps Series 2 Baseball:
  34,871 rows across 360 subsets.
- `2026-topps-update-series-baseball.csv` — 2026 Topps Update Series Baseball:
  27,661 rows across 533 subsets (Update numbering, e.g. `US4`).
- `2026-topps-holiday-baseball.csv` — 2026 Topps Holiday Baseball:
  640 rows across 12 subsets.

Not yet covered (no free spreadsheet source found): 2020 Series 2, 2020
Update Series, 2021 Series 2, and 2020 Holiday. Easter tin parallels are
not separate files: they ride inside the Series 1 checklists as
`Base Holiday <theme>` subsets.

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

Transcribed from Topps checklist spreadsheets published by ChecklistCenter
(a republication of Topps' official checklists), downloaded October 28, 2026,
and converted to CSV with no rows added, removed, or renamed — only columns
normalized and flags derived from subset names. Note: the flags are only as
good as the source's subset splits — sets that don't split rookies into their
own subset (2026 Series 1 and 2 keep base rookies in `Base`) will show fewer
rookie flags than sets that do (2025 Series 1, 2026 Update).

Six files come from DegreeGrading's published PDF checklists instead
(2020 Series 1, 2021 Series 1, 2021 Update Series, 2021 Holiday,
2022 Series 1, 2026 Holiday), because no free spreadsheet exists for them.
Those PDFs list no team column, so `team` is blank in those files.
The 2026 Holiday PDF lists parallels as "some cards only" without saying
which cards, so that file has no parallel rows; the 2025 Holiday
spreadsheet likewise names base parallels without enumerating them as rows.

## Adding sets

Add one CSV per product under this folder, using the same columns, and the app
picks it up from the same location. The data-source layer is deliberately
swappable: this CSV can later be replaced by a keyed catalog API without
reworking identification or pricing.

## Fetching

The app fetches the raw file over HTTPS, no authentication:

`https://raw.githubusercontent.com/JeremyShanebrook/sports-card-scanner/main/catalog/2025-topps-series-1-baseball.csv`
