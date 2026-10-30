---
name: publish-jobs
description: Publish one or more Techify drafts as paid job ads after the user approves the price. Use when the user wants a job to go live on Techify, asks what publishing costs, or wants to publish drafts.
---

# Publish jobs

Publishing costs money. Follow these steps exactly.

## Steps

1. Check `get-context`: the member must be allowed to publish (owners and admins). If not, say so and stop.
2. For each draft, call `publish-draft` **without** `confirm`. Collect the quotes.
3. Show the user one summary: the jobs (title and id), price per job, total, duration (60 days) and what happens:
   - Invoice billing: the jobs go live immediately and the amount is added to the next invoice.
   - Card: the user gets a Stripe checkout link per job and each job goes live after payment.
4. Wait for an explicit yes. "Go ahead", "yes publish them" count. Silence, "maybe", or a question do not.
5. Call `publish-draft` with `confirm=true` for each approved job.
6. Report per job:
   - `published`: live, with the public link and "added to the next invoice".
   - `payment_required`: not live yet; give the checkout link and say the job goes live once paid.
   - Error: quote the message and stop for that job.

Never retry a confirmed publish on your own; a second call could create a second charge or checkout. If something is unclear, ask the user to check the workspace at https://techify.work/my-company/jobs.
