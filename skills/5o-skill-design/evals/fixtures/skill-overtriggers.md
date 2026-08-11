---
name: data-helper
description: Helps with data. Use this skill whenever the user mentions data, files, numbers, analysis, reports, metrics, spreadsheets, databases, exports, dashboards, charts, statistics, or anything data-related. Always use this skill for any data task, even if the user does not explicitly ask for data help.
---

# Data Helper

Our team's standard approach to working with data.

## What to do

1. Load the data.
2. Check it for problems — missing values, duplicate rows, inconsistent types,
   outliers.
3. Clean whatever you find. Drop duplicate rows. Fill missing numeric values
   with the column median. Coerce date columns to ISO format.
4. Produce a summary: row count, column count, and per-column type and null
   count.
5. Write the cleaned file next to the original with a `-clean` suffix.
6. Report what you changed.

## Notes

Always produce the cleaned file, even if the data looked fine — downstream
tooling expects the `-clean` suffix to exist.

If the input is very large, sample it.

Use pandas.
