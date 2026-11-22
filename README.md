# big-cyber-events

A curated dataset of large-scale cyber events — major intrusions, supply-chain
compromises, ransomware incidents, zero-day exploits and critical
infrastructure attacks — in one flat CSV.

Data is **not populated yet**. This repo currently ships the schema and the
empty file; rows land in later commits.

## File

`big-cyber-events.csv` — UTF-8, comma-separated, single header row, RFC 4180
quoting (quote any field containing a comma or quote character).

```
name,cve,link
```

## Fields

| Field  | Type   | Required | Description |
|--------|--------|----------|-------------|
| `name` | string | yes      | Short human-readable event name, e.g. `SolarWinds Orion supply-chain compromise`. Unique. |
| `cve`  | string | no       | CVE identifier(s) for the tracked vulnerability, uppercase `CVE-YYYY-NNNN`. Several CVEs for one event share the field, separated by a space. Empty when no single CVE applies (ransomware campaigns, credential stuffing, OT/physical incidents) — never invented. |
| `link` | URL    | yes      | Absolute `https://` link to the primary public announcement or advisory: vendor bulletin, CISA/CERT notice, incident report, or the researcher's own disclosure writeup. Permalinks over news coverage; no shorteners, no tracking parameters. |

## What counts as "big"

One row per event, not per CVE. An event qualifies on **at least one** of:

- confirmed mass exploitation in the wild;
- national or multi-national impact;
- critical-infrastructure disruption;
- reach through a shared dependency — a library, renderer, appliance or
  managed service whose compromise yields remote code execution across
  thousands of downstream deployments, **counted even before in-the-wild
  exploitation** (the structurally-big class: Log4Shell, ImageTragick,
  CitrixBleed, Upload2Shell).

Events that are merely severe for one organisation do not qualify. Severity
scores are not criteria; reach is.

## Conventions

- Dates, actors, victim counts and impact are deliberately out of scope for
  now — extend the schema rather than smuggling them into `name`.
- Attribution is recorded as stated by the announcing body; the dataset does
  not re-characterise it.
- Where an event carries a root CVE plus per-product CVEs, all identifiers go
  in `cve` and `link` points at the root disclosure.

## Status

- [ ] Populate rows
- [ ] Lightweight validation (header, URL well-formedness, CVE regex)

## License

Data: CC0-1.0.
