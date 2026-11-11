# Aletto sales report site

Live: https://jaketub16.github.io/aletto-sales-daily/  (repo: jaketub16/aletto-sales-daily, GitHub Pages from `main` root)

Build (from the box, GHL read-only data only):
1. Run the normal scorecard + funnel (--v2) + brief scripts for the period.
2. Daily: `python3 prep_daily.py --label YYYY-MM-DD --scorecard /workspace/scorecard/daily-<covered day> --funnel /workspace/scorecard/funnel-daily-<run day> --brief /workspace/daily-brief-<run day> --curated curated/daily-<run day>.json --out data/daily-<run day>`
   `curated/*.json` holds the hand-checked items from the brief (to-fix lists, pricing flags, aging next steps, kickoff list, caveats), already shortened to first name + last initial.
3. `python3 build.py --period daily|weekly|monthly|quarterly|yearly --label <label> --data data/<dir>`
   -> site/<label>/ (daily) or site/<period>/<label>/ ; updates site/reports.json + site/index.html.
4. `cd site && git add -A && git commit -m "report <label>" && git push`
5. Verify: `./shoot.sh https://jaketub16.github.io/aletto-sales-daily/<path>/ shots/<run>` (cache-busted, desktop + mobile, `?only=<section>` or `?only=rep-<Name>` isolates a section).

Privacy: the site is public. Never put prospect full names, companies, emails, phones, recording links or per-prospect deal values in report.json. prep_daily.py shortens names; run the privacy scan before pushing.
