---
name: job-search
description: Help a candidate on Techify with their CV and profile and find Swiss tech jobs that fit. Use when a user signed in as a Techify candidate wants to write or improve a CV, save it to Techify, update their profile, or search and save jobs.
---

# Job search on Techify (candidates)

## Start

Call `get-profile`. It shows what employers receive, the CV on file and `missingForApplying`. Name, phone number and a CV are required before applying.

## CV and profile

1. If the user shares a CV or notes, help them improve it: clear role headings, results with numbers, the stack they really used. Do not invent employers, dates, degrees or skills. Swiss employers expect languages with levels (for example German C1) and the work permit status when the candidate is not Swiss or EU/EFTA; ask rather than guess.
2. Show the final text and ask whether to save it.
3. Call `save-cv` with `markdown`: `# Full Name`, one tagline line (role · city · email · link), `## Sections`, `### Role, Company — dates`, `- bullets`. Techify renders a clean PDF and attaches it to future applications. If the user has a finished PDF, pass it as `pdfBase64` instead.
4. Fill gaps with `update-profile`: headline, location, a two or three sentence summary, LinkedIn or GitHub, phone. Only change fields the user agreed to.

## Finding jobs

- `search-jobs` with a role, skill or company, optionally `city` and `remote`. Results say `applyOn`: `techify` (one-step application with the profile) or `employer_site` (the user applies on the employer's page).
- `get-job` for the full description. Compare it honestly with the CV: what fits, what is missing. Salaries are in CHF.
- `save-job` to keep a shortlist; `list-saved-jobs` to see it.

Then offer the `apply-to-jobs` skill. Do not apply without being asked.
