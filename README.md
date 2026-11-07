# tinybrowser WPT results

The published record of the newest WPT run on `tinybrowser-dev/tinybrowser`
`main`, written by `.github/workflows/wpt.yml`. The site at
`https://tinybrowser.ericc.ch/wpt` reads these files.

- `latest.json` — the newest run: totals, per-folder counters, pin, commit
- `index.json` — one entry per run; this is the history chart
- `regressions.json` — failure-list diff against the previous run
- `failures.jsonl.gz` — every failing test and subtest, gzipped JSON lines

This repo is a **snapshot, not a log**: each publish amends the single commit
and force-pushes, so the checkout is always just the current record. A full
run has ~583k failure rows (~4 MB gzipped), and committing a new copy on every
push would grow the repo without bound. The history a reader wants is
`index.json`; git history here would only repeat it.

`latest.json` has no `failures` member for the same reason: the list lives in
the sidecar, which is what the next publish diffs against, and the committed
JSON stays small. The record comes from `python3 tools/wpt/cli.py merge
--summary-out` and is turned into these files by `python3 tools/wpt/cli.py
publish`. The giant merged wptreport is a debug artifact and stays in the
Actions run.

Two runs from different WPT revisions are not comparable, so
`regressions.json` reports `comparable: false` and an empty diff across a pin
bump. New TIMEOUTs are listed separately: they flip with runner load.

Nothing here is edited by hand; the workflow owns the working tree.
