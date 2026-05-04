# results/

Run outputs for [kSTEP](https://github.com/kstep-dev/kstep). Submodule of the parent repo. Tracked artifacts (jsonl outputs, plots) document each scheduler bug; per-run logs and coverage are gitignored.

## Layout

```
results/
├── latest → <run>/         symlink to the most recent run (gitignored)
├── repro_<bug>/            reproduction outputs from `./reproduce.py <bug>`
│   ├── buggy/
│   │   └── kstep.jsonl     ✓ jsonl trace from the buggy kernel
│   ├── fixed/
│   │   └── kstep.jsonl     ✓ jsonl trace from the fixed kernel
│   ├── plot.png            ✓ figure rendered from the jsonl traces
│   └── plot.pdf            ✓ same plot, vector form
├── fuzz_<bug>/             pre-recorded fuzz runs that discovered each bug
│   ├── corpus/             seed corpus from the run
│   └── error/              crash artifacts grouped by error category
└── tmp_<timestamp>/        ad-hoc local outputs from `./run.py` and `./fuzz.py` (gitignored)
```

✓ tracked in git; everything else is per-run output and gitignored (`*.cov`, `*.log`, `*.signal`, `tmp_*`, `latest`).

## Contents

- `repro_<bug>/` directories are populated by `./reproduce.py <bug>` in the parent repo. Each `kstep.jsonl` is the per-tick scheduler state trace; `plot.png`/`plot.pdf` are produced by the `scripts/plot_*.py` helpers.
- `fuzz_<bug>/` directories are archives of fuzz runs that originally discovered the corresponding bug — used as starting seeds for replay-based fuzzing.
