# Weekly content update — instructions for the scheduled agent

Goal: keep `exam_patterns.json` current and exam-relevant for Bank (IBPS/SBI/
RRB), SSC (CGL/CHSL/MTS/CPO) and Railway (RRB NTPC/Group D/ALP) aspirants,
with **no outdated question formats**. Open a pull request; never merge it.

## 1. Set up
- Clone `pipansarkar/speed-maths-data` (this repo) and `pipansarkar/speed-maths`
  (the app) side by side.
- Make sure Flutter (stable) is on PATH; if not, install it
  (`git clone https://github.com/flutter/flutter.git -b stable --depth 1`) and
  run `flutter pub get` in the app repo.

## 2. Research (last 14 days, plus anything still upcoming)
- Official: ibps.in, sbi.bank.in (careers), ssc.gov.in, rrbcdg.gov.in and
  regional RRB sites — notifications, calendars, exam-date notices.
- Paper analyses of shifts held recently: PracticeMock, Oliveboard, Adda247 /
  Bankersadda, PW, TIME, Careers360, Testbook.
- Note for each finding: exam, date, what changed, source URL.

## 3. Edit `exam_patterns.json`
- **examDates**: add newly announced dates; update changed ones; delete
  entries more than 7 days in the past. `"tentative": false` only when the
  official site confirms. Every entry needs a `source`.
- **weights**: change only when two or more independent analyses agree. Set a
  topic to `0` for an exam if it has not appeared in that exam's papers in the
  last 12 months (it then disappears from that exam's mixes, daily challenge
  and sectionals). Restore it if it reappears.
- **templates**: add templates for question formats newly seen in recent
  shifts (original wording, exam-style, Indian number formatting via
  `{var:inr}`); delete templates for formats not seen in 12 months. Keep each
  template's `exams` and `levels` accurate. Prefer formats the built-in
  generators don't already cover.
- **sectionals**: keep compositions in line with the latest weightage.
- Bump `version` by 1 and set `updated` to today's date.
- Add a `CHANGELOG.md` entry listing every change with its source.

## 4. Validate (must pass)
```
cd speed-maths && tool/validate_content.sh ../speed-maths-data/exam_patterns.json
```
Fix and re-run until green. Also sanity-read 3 instances of every new
template (the test output or a quick script) and confirm the answers by hand.

## 5. Publish for review
- If nothing changed, stop — no PR, no empty commits.
- Otherwise create branch `weekly/<yyyy-mm-dd>`, commit, push, and open a PR
  to `main` titled `Weekly content update <yyyy-mm-dd>` with: summary of
  changes, sources, and the validation result. Do not merge.
