# Public data dictionary

The authoritative live record is available from [`https://www.colainsight.com/api/cola`](https://www.colainsight.com/api/cola). The complete reader-facing dictionary is maintained at [COLA Insight](https://www.colainsight.com/data-dictionary).

| Field | Type / unit | Meaning |
|---|---|---|
| `schemaVersion` | string | Version of the public contract. |
| `observedAt` | ISO 8601 UTC | Time the stored snapshot was successfully assembled. |
| `benefitYear` | integer | Calendar year in which the COLA applies. |
| `status` | enum | `forecast`, `computed`, or `official`. |
| `rate.displayed` | percent or null | Value used by public calculators: official, then computed, then forecast. |
| `rate.forecast` | percent or null | Independent estimate while the record is in forecast status. |
| `rate.computed` | percent or null | Formula result after all three required Q3 observations exist. |
| `rate.official` | percent or null | SSA-published benefit-year COLA. |
| `cpiW.seriesId` | string | BLS series `CWUR0000SA0`. |
| `cpiW.baseline` | object | Prior applicable Q3 comparison period and average. |
| `cpiW.observations` | array | July, August, and September inputs; pending values are `null`. |
| `sources` | object | Original publisher, retrieval path, and official-confirmation source. |
| `ssaConfirmed` | boolean | True only after the applicable SSA determination is confirmed. |
| `notes` | string or null | Plain-language context attached to the snapshot. |

## Null and unit rules

- A missing observation is `null`, never zero.
- COLA rates use percentage points.
- CPI-W values use index points, 1982–84 = 100.
- Public timestamps use UTC.
- A changed CPI-W value, rate, status, or retrieval path creates a new historical snapshot.
