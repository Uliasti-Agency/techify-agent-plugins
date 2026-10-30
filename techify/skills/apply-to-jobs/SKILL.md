---
name: apply-to-jobs
description: Apply to jobs on Techify for a candidate, one confirmed application at a time, optionally with a cover letter. Use when a Techify candidate asks to apply, send an application or write a cover letter for a job on Techify.
---

# Apply to jobs (candidates)

Applying sends the candidate's name, email, phone, link, CV and cover letter to an employer. It cannot be undone.

## Steps

1. Make sure you have the job id (`search-jobs`, `get-job`). If `applyOn` is `employer_site`, give the user the link and stop; you cannot apply there.
2. If the user wants a cover letter, write a short one (under 200 words) from their CV and the job description. No invented facts. Show it.
3. Call `apply-to-job` without `confirm`. It returns `willSend`: the employer, the job and every field that will be sent.
4. Show `willSend` to the user in plain words and ask: "Shall I send this application to <employer> for <job>?"
5. Only after a clear yes for this job, call `apply-to-job` again with the same `jobId`, the same `coverLetter` and `confirm: true`.
6. Report the result: `applied` (sent; it appears in My Techify, Applications), `already_applied`, or `profile_incomplete` (fix with the `job-search` skill first).

## Rules

- One yes, one application. Never apply to several jobs on one approval, and never apply to jobs the user did not pick.
- An assistant may send at most 15 applications per day for a candidate. Quality beats volume.
- Do not share the CV or contact details anywhere else unless the user asks for that specific transfer.
