---
name: techify
description: Start here for anything about Techify, for companies and for candidates. Explains what Techify is, which MCP tool does what, and the rules for drafts, publishing, applying and personal data. Use when the user mentions Techify, posting or publishing a tech job in Switzerland, job drafts, their ATS sync, applications, job ad invoices, or looking for and applying to tech jobs in Switzerland on Techify.
---

# Techify

Techify (https://techify.work) is a job board for tech jobs in Switzerland. Companies have a workspace with a team (owners, admins, recruiters), jobs, drafts, connected job sources (Greenhouse, Lever, Ashby, Personio, RSS feeds, the Techify API) and billing. A job ad costs CHF 95 and is live for 60 days. Companies pay by card in Stripe Checkout, or on invoice once Techify approved them for it.

You reach it through the `techify` MCP server. Which tools you get depends on the account the user signed in with:

- **Company account**: you act as one member of one company workspace, with that member's role. Tools start with `get-context`. Everything below this list is about this case.
- **Candidate account**: you act for one job seeker. Tools start with `get-profile`. Follow the `job-search` and `apply-to-jobs` skills.

Every tool call is logged.

## Before the first task in a session

1. Call `get-context` (company) or `get-profile` (candidate); the tool list tells you which one exists. Keep the result in mind; do not call it again unless the session is long.
2. If it fails with an authentication error, follow the `setup` skill.

## Which tool for which task

| Task | Tool | Notes |
| --- | --- | --- |
| Overview, permissions, price | `get-context` | Call first. |
| Find jobs by status or title | `search-jobs` | `status`: live, inactive, draft, all. |
| Full details of one job | `get-job` | Description as text, salary, tags, dates, application count. |
| Write a new draft or update one | `save-draft` | Free and private. Same `reference` updates the draft. |
| Publish a draft | `publish-draft` | Two steps: quote without `confirm`, publish with `confirm=true`. Owners and admins only. |
| Remove a draft | `discard-draft` | Needs `confirm=true`. Owners and admins only. |
| Pause or resume a live job | `set-job-visibility` | The paid period keeps running while paused. |
| Applications | `list-applications` | Personal data. See rules. |
| Connected ATS and feeds | `list-sources`, `sync-source` | Sync creates or updates drafts only. |
| Payment method, open charges, invoices | `billing-overview` | |
| Team members | `list-team` | |
| Compare with the market | `search-market` | Live jobs of all companies on Techify. |

Skills for companies: `draft-job`, `review-drafts`, `publish-jobs`, `applications`, `hiring-report`. Skills for candidates: `job-search`, `apply-to-jobs`.

Freelance projects are coming to Techify. Candidates can already mark themselves open to projects (`update-profile`, `openTo`); there are no project listings yet, so do not promise any.

## Rules

- **Money needs a yes.** Publishing costs CHF 95 per job. Always call `publish-draft` without `confirm` first, show the user the price and what will happen, and call it with `confirm=true` only after an explicit yes for that job. One yes can cover a list of jobs if you showed the list and the total.
- **Card payments are not done by you.** When `publish-draft` returns `payment_required`, give the user the checkout link and say the job goes live after they pay. Never say it is live.
- **Never claim success you did not get.** A job is live only if `publish-draft` returned `published`. A draft is saved only if `save-draft` returned `created` or `updated`.
- **Drafts are private.** Say so when you create one; the user can review it at the link in the result.
- **Candidate data is personal data.** Use applications only for the hiring task the user asked for. Do not copy CVs, emails or phone numbers into other tools, files or messages unless the user asks for that specific transfer. Never judge candidates by age, gender, origin, religion, health or other protected traits.
- **Respect the role.** If `get-context` says the member cannot publish or discard, say so and suggest asking an owner or admin. Do not look for workarounds.
- **No deletes of live jobs, no billing changes, no invitations.** Those are not available to you; point the user to the workspace at https://techify.work/my-company.
- Write in the user's language. Swiss German users write ss, not ß. Salaries on Techify are in CHF.
- Summarise results; do not dump raw JSON. Mention job titles and ids so the user can find them.
