# COLA Insight Data

Open data, calculation notes, charts, and an embeddable widget for tracking the **2027 Social Security cost-of-living adjustment (COLA)**.

**Live project:** [COLA Insight](https://www.colainsight.com/)  
**Current forecast and CPI-W tracker:** [2027 Social Security COLA forecast](https://www.colainsight.com/2027-social-security-cola-forecast)  
**Public asset library:** [Data, charts, downloads, and widget](https://www.colainsight.com/data)

**Public MCP server:** [Connect an AI assistant](https://www.colainsight.com/mcp-server)

**Official Registry:** [`io.github.ge3m0r/cola-insight`](https://registry.modelcontextprotocol.io/v0/servers/io.github.ge3m0r%2Fcola-insight/versions/1.0.1)

COLA Insight is an independent educational project. It is not affiliated with, endorsed by, or operated by the Social Security Administration (SSA), Bureau of Labor Statistics (BLS), Centers for Medicare & Medicaid Services (CMS), or the U.S. government.

## What is in this repository

This repository publishes the parts of COLA Insight that are most useful for independent verification and reuse:

- preserved 2027 COLA forecast and calculation snapshots;
- a complete benefit-impact table from $100 through $5,000;
- the public JSON data contract and an example record;
- calculation methodology and status definitions;
- publication-ready SVG charts;
- a copy-and-paste version of the live COLA widget;
- public MCP distribution metadata and connection documentation.

The production website, Cloudflare Worker deployment, D1 configuration, scheduled refresh system, rate limiting, analytics, and editorial/SEO application source are intentionally maintained separately.

## Current public endpoints

| Asset | Permanent URL |
|---|---|
| Current JSON record | [colainsight.com/api/cola](https://www.colainsight.com/api/cola) |
| Snapshot history CSV | [2027 COLA history CSV](https://www.colainsight.com/data/2027-cola-history.csv) |
| Benefit amount CSV | [2027 benefit amounts CSV](https://www.colainsight.com/data/2027-cola-benefit-amounts.csv) |
| Preserved revision timeline | [2027 COLA forecast history](https://www.colainsight.com/2027-cola-forecast-history) |
| CPI-W chart | [2027 COLA CPI-W chart](https://www.colainsight.com/2027-cola-cpi-w-chart) |
| Benefit increase chart | [2027 COLA increase chart](https://www.colainsight.com/2027-cola-benefit-increase-chart) |
| Embeddable tracker | [Free 2027 COLA widget](https://www.colainsight.com/2027-cola-widget) |
| Interactive calculator | [2027 COLA calculator](https://www.colainsight.com/2027-cola-calculator) |
| MCP documentation | [Connect to COLA Insight MCP](https://www.colainsight.com/mcp-server) |
| MCP endpoint | [`https://www.colainsight.com/mcp`](https://www.colainsight.com/mcp) |
| Official MCP Registry | [`io.github.ge3m0r/cola-insight`](https://registry.modelcontextprotocol.io/v0/servers/io.github.ge3m0r%2Fcola-insight/versions/1.0.1) |

The files in this repository are publishable snapshots. The permanent URLs above are the authoritative, automatically updated versions.

## Data status matters

Every record uses exactly one status:

- `forecast` — an independent estimate while one or more required Q3 CPI-W observations are unavailable;
- `computed` — all three observations are available and the statutory formula can be reproduced, but SSA confirmation is still pending;
- `official` — SSA has published the benefit-year COLA.

Do not describe a `forecast` or `computed` record as an official SSA announcement.

See [`methodology/status-definitions.md`](methodology/status-definitions.md) and [`schema/data-dictionary.md`](schema/data-dictionary.md) before reusing the data.

## Quick examples

Fetch the current record:

```js
const response = await fetch("https://www.colainsight.com/api/cola");
const record = await response.json();

console.log(record.status, record.rate.displayed);
```

Embed the live tracker:

```html
<iframe
  src="https://www.colainsight.com/embed/2027-cola"
  title="2027 Social Security COLA tracker by COLA Insight"
  width="100%"
  height="430"
  style="border:0;max-width:720px"
  loading="lazy"
></iframe>
```

Connect an MCP-compatible assistant using the remote Streamable HTTP endpoint:

```text
https://www.colainsight.com/mcp
```

The MCP server is public, read-only, and requires no API key. It provides four tools for the current COLA record, educational benefit calculations, preserved snapshot history, and primary sources. See [`mcp/README.md`](mcp/README.md) for the tool list, example configuration, privacy guidance, and versioning policy.

## Primary sources

- [BLS Public Data API](https://www.bls.gov/developers/) — CPI-W series `CWUR0000SA0`
- [SSA latest COLA determination](https://www.ssa.gov/OACT/COLA/latestCOLA.html)
- [CMS Medicare premiums and deductibles](https://www.cms.gov/newsroom/fact-sheets/2026-medicare-parts-b-premiums-deductibles)
- [FRED CPI-W series](https://fred.stlouisfed.org/series/CWUR0000SA0) — retrieval fallback and cross-check

The source used to retrieve each stored observation is included with the record. A fallback changes the retrieval path, not the underlying BLS series.

## Citation

Suggested citation:

> COLA Insight Editorial Team. “COLA Insight Data: 2027 Social Security COLA Data, Charts, and Tools.” 2026. https://www.colainsight.com/data

For machine-readable citation metadata, see [`CITATION.cff`](CITATION.cff). Questions and corrections can be sent to [support@colainsight.com](mailto:support@colainsight.com).

## Licensing

- Example code and widget snippets: [MIT License](LICENSE)
- Original documentation, charts, and explanatory content: [CC BY 4.0](CONTENT-LICENSE.md)
- Government facts and source data may have their own public-domain or agency terms; attribution to the responsible agency should be preserved.
- The COLA Insight name and logo are not granted for reuse as a product identity. See [`TRADEMARKS.md`](TRADEMARKS.md).

Attribution is appreciated and helps readers verify freshness, but no specific keyword-rich anchor text is required.
