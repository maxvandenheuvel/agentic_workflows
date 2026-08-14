---
description: Add the current UTC date to the site's daily updates.
engine: copilot
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  copilot-requests: write
tools:
  edit: true
safe-outputs:
  create-pull-request:
    max: 1
    allowed-files:
      - index.html
---

# New Day

Update the existing Daily Updates navigation in `index.html` for this workflow run.

## Task

1. Determine the workflow run's current date in UTC. Use `date -u`, or the UTC value represented by the workflow run context; do not use the agent machine's local date.
2. Format the date exactly like the existing entry, for example `1st of August`. Use a matching lowercase ID such as `august-1-dialog`.
3. Inspect `index.html` before editing. If the UTC date is already present in the Daily Updates navigation or its matching dialog, make no changes and call `noop` with a brief explanation.
4. Otherwise, add one navigation button to the existing Daily Updates list and one matching accessible `<dialog>` following the existing HTML structure and ID conventions. The button must use `aria-haspopup="dialog"`, `aria-controls` pointing to the new dialog ID, and `data-dialog-trigger`.
5. The dialog must use the existing `daily-update-dialog` classes and pattern, have unique `aria-labelledby` and `aria-describedby` IDs, preserve the existing close control, and clearly confirm that the daily update ran for the formatted UTC date.
6. Preserve every existing daily update and all unrelated HTML. Do not modify `styles.css` or any other file.

## Safe Output

- When `index.html` changes, use the configured `create-pull-request` safe output to create at most one pull request.
- The pull request must contain only `index.html`.
- If no change is needed, use `noop` instead of creating a pull request.