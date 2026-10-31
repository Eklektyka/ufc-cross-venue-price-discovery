# UFC Cross-Venue Price Discovery: Kalshi x Polymarket

Replication package for [*Integration Without Leadership: Cross-Venue Price
Discovery in UFC Prediction Markets*](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=7194218)
(SSRN 7194218, 2026).

**Status:** Finished. Exhibits frozen at commit `bb5d695` (2026-07-17, seed=42).

---

## Key Results

All numbers from [`paper/PAPER_BRIEF.md`](paper/PAPER_BRIEF.md), sourced to
individual exhibits.

| Finding | Number | Exhibit |
|---------|--------|---------|
| Panel | 281 fights, 35 cards, May 2025 -- Jul 2026 | [ex1](paper/exhibits/ex1_sample.md) |
| Cross-correlation at k=0 | +0.103 (5-min) / +0.204 (30-min), both significant | [ex2](paper/exhibits/ex2_ccf.md) |
| Jump asymmetry (3c) | K->PM 54.8% vs PM->K 39.5%, diff +15.3 pp [+3.4, +26.1] | [ex3](paper/exhibits/ex3_jump.md) |
| Persistent-minus-transient at +1h | K->PM +4.4c, PM->K +3.4c, both CIs exclude zero | [ex3](paper/exhibits/ex3_jump.md) |
| Gap closure median | Main-event 32 min, undercard 118 min | [ex4](paper/exhibits/ex4_gap.md) |
| Fragmentation ratio | 0.81x (PM depth stable; Kalshi grew ~10x) | [ex6](paper/exhibits/ex6_pm_depth.md) |
| OFI reversal (confirmatory) | -1.13c, t = -6.29, p < 0.001 (sub-fee) | [ex5](paper/exhibits/ex5_ownflow.md) |

## Reproducing the Exhibits

```bash
# Requires Python 3.12, pandas, numpy, scipy
python code/exhibit_freeze.py        # produces paper/exhibits/ex1-ex7
python code/ex5d_diagnostics.py      # bounce diagnostics
python code/ex5e_large_trade.py      # large-trade split (post-hoc)
```

All three scripts are deterministic (seed=42). Runtime for `exhibit_freeze.py`
is approximately 33 seconds. Requires the Polymarket data-api trade pulls and
Kalshi trade parquets (not included; too large for git).

## Repository Structure

| Folder | Contents |
|--------|----------|
| `code/` | Pipeline scripts: crosswalk, panel build, exhibit freeze, diagnostics |
| `paper/exhibits/` | Frozen exhibit outputs (ex1--ex7, ex5d, ex5e) as CSV and markdown |
| `paper/PAPER_BRIEF.md` | Headline numbers reference (single vintage, `bb5d695`) |
| `qa/` | Audit trail: complement fix, crosswalk validation, asymmetry robustness |
| `osf/` | Pre-registration and exploratory log |
| `data/meta/` | UFC crosswalk overrides (CSV) |

## Data Sources

| Source | Venue | Coverage |
|--------|-------|----------|
| Polymarket data-api (taker fills) | PM | May 2025 -- Jul 2026 |
| Kalshi public archive + live collector | Kalshi | May 2025 -- Jul 2026 (Dec 2025 -- Mar 2026 gap unrecoverable) |

## Upstream

This repository contains only the UFC price-discovery paper files. The
original development history lives at
[Eklektyka/Prediction_Markets_Public](https://github.com/Eklektyka/Prediction_Markets_Public),
which was forked from the Diercks/Katz/Wright Fed-rate prediction market
project and used as the starting template for this work.

## License

Code: MIT. Text and figures: CC BY 4.0.

## Citation

> Michal Adamczewski, *Integration Without Leadership: Cross-Venue Price
> Discovery in UFC Prediction Markets* (2026).
>
> https://papers.ssrn.com/sol3/papers.cfm?abstract_id=7194218
