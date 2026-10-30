---
name: hiring-report
description: A short status of the company's hiring on Techify. Use when the user asks how their jobs are doing, what expires soon, how many applications came in, what is not invoiced yet, or for a weekly hiring update.
---

# Hiring report

## Steps

1. `get-context` for counts and payment method.
2. `search-jobs` with `status: live`. Note jobs expiring within 14 days.
3. `list-applications` (first page) for recent applications; count per job for the live jobs with `get-job` if the user wants numbers per role.
4. `search-jobs` with `status: draft` for drafts waiting.
5. `billing-overview` for charges not yet invoiced and open invoices.

## Output

- **Live**: number of live jobs, and a list of those expiring soon with the date.
- **Applications**: new since the date the user cares about (default 7 days), per job.
- **Drafts waiting**: count, and the three oldest.
- **Billing**: payment method, amount not yet invoiced, invoices that are sent but not paid.
- **Suggestions**: at most three, each tied to a job, for example "Publish the Data Engineer draft, it has been waiting 10 days". Do not act on them without the user's instruction.
