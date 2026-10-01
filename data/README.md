# Module 3 data pack

This directory is **gitignored** — the pack is ~72 MB of protein embeddings and
is distributed through the course, not through this repo. Only this note is tracked.

## How to populate it

Download the Module 3 data pack from the course site and unzip its contents
directly into this directory (the files sit at `data/`, not in a nested folder).

## Expected contents

`notebooks/module3_part2_real_data.ipynb` checks for these six and refuses to run without them:

| File | What it holds |
|---|---|
| `panel.tsv` | 1201-protein panel with Open Targets tractability labels |
| `panel_emb_main.npy` | ESM-C 300M embeddings, 960-dim, float16 |
| `panel_emb_baseline.npy` | ESM-2 35M embeddings, 480-dim, float16 |
| `manifest.json` | Model provenance, seed, UniProt release |
| `variant_scores_TP53.tsv` | All possible p53 substitutions |
| `anchor_variants.tsv` | Annotated cancer hotspots |

The pack also ships `proteome.tsv`, `proteome_emb_*.npy` (20190 proteins), and
`variant_scores_APOE.tsv` / `variant_scores_TREM2.tsv`, which the Part 2 notebook
does not require.

## Checking it worked

```bash
python -c "from pathlib import Path; print(sorted(p.name for p in Path('data').glob('*')))"
```
