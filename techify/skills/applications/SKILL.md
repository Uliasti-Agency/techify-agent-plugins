---
name: applications
description: Read and summarise the applications to the company's Techify jobs. Use when the user asks who applied, for new candidates, for a shortlist, or for the applications to a specific role.
---

# Applications

Applications contain personal data of people who applied. Handle them only for the task the user asked for.

## Steps

1. If the user names a role, find it with `search-jobs` and use its id.
2. `list-applications` with `jobId` (and `name` if they look for a person). Newest first; page through if needed.
3. Summarise: how many, since when, and a table with name, applied date, job, and whether a CV and portfolio link are attached.
4. If the user wants a shortlist, ask for their criteria first. Judge only job-related facts the user can see too (for example the portfolio link they gave). The tool does not return CV contents; do not guess them.

## Rules

- Do not judge or rank by age, gender, origin, nationality, religion, health, family status or photos.
- Do not send candidate data to other tools, files or people unless the user asks for that specific transfer.
- Do not contact candidates. Draft a message for the user if they ask; they send it themselves.
