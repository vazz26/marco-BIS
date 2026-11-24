# My MaRCo work log

Runs done with Claude Code on 2026-11-24. The results are in each folder's
`outputs/` folder, which is force-added on this branch (upstream gitignores it).

## Data used

| Dataset | Source | Details |
|---|---|---|
| FRED-QD (quarterly) | St. Louis Fed `current.csv`, downloaded 2026-11-24 | 267 quarters, 1959Q1–2025Q3, 245 series; SHA-256 of raw file: `d9ede94f40c116e8081258417aa82b622b21db8142d284e5eeb7dcb94f8392f7` |
| Kilian `data.txt` | github.com/richryan/jcre-oil (byte-identical to openICPSR 113299) | Fetched automatically by the replication |

The data files themselves are not committed (third-party terms; re-download via
`data/fred_qd/UPDATE.md`). FRED revises its data, so a later download may give
slightly different Sims numbers. Kilian's numbers do not depend on a vintage.

## Runs

| Run | Result | Report |
|---|---|---|
| Sims (1980) six-variable VAR | 8/8 paper targets pass; max eigenvalue 1.074 (mildly explosive, as the replication README expects) | `scripts/replications/sims_1980_var/outputs/report.html` |
| Kilian (2009) oil-market SVAR | 5/5 paper targets pass; oil-specific demand shock → real oil price +5.94% on impact, +8.55% peak | `scripts/replications/kilian_2009_oil_svar/outputs/report.html` |

Disposition for both: **archive only** (canonical replications, results match the paper).

## Paused

- Monetary policy question ("How does monetary policy affect inflation and output?"):
  Stage 1 proposal made (recommended: CEE 1999 on FRED-QD), not yet confirmed.

## Re-running in a new session

```bash
python3.11 -m venv .venv && .venv/bin/pip install -r requirements.txt
# download FRED-QD per data/fred_qd/UPDATE.md, then:
.venv/bin/python scripts/replications/sims_1980_var/replicate.py
.venv/bin/python scripts/replications/kilian_2009_oil_svar/replicate.py
```
