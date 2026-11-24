# speed-maths-data

Live content for the Speed Math app (Bank, SSC & Railway exams).
The app downloads `exam_patterns.json` from this repo at most once a day, so
changes merged here reach every installed app without a release.

## What's in the file
- `exams[]`: per exam: `weights` (topic → relative weight in recent papers;
  **0 or missing = not asked recently**, which removes the topic from exam mixes,
  the daily challenge and sectionals for that exam), `marking`,
  `realQuestions`/`realMinutes` (quant section), `groupOrder`, `sectionals[]`.
- `templates[]`: data-defined, exam-style question types (format documented in
  `lib/engine/template.dart` in the app repo). About a third of a topic's
  questions come from its templates.
- `examDates[]`: upcoming exam dates for the countdown.

## Rules
- Increase `version` on every change, or apps ignore the update.
- Every change must pass `tool/validate_content.sh` in the app repo.
- Never rename or remove topic names; unknown names are ignored by older apps,
  so additions are safe.
- Weightage is estimated from public coaching-site paper analyses, not
  official data. Exam dates stay `"tentative": true` until confirmed on the
  official site, and every date carries a `source`.
- Templates are original questions in the exam's format — never copy real
  paper questions verbatim.

Updated weekly by a scheduled agent (see `AGENT.md`) that opens a pull request
for review; merging the PR publishes it.
