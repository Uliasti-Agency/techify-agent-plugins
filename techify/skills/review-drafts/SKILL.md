---
name: review-drafts
description: Go through the drafts that arrived from the company's ATS, job feed or API and decide what to keep, discard or publish. Use when the user asks what is in their drafts, what came in from Greenhouse, Lever, Ashby, Personio or their feed, or wants to clean up drafts.
---

# Review drafts

## Steps

1. If the user wants fresh data, `list-sources`, then `sync-source` for the source they mean (owners and admins only). Report fetched, created and updated.
2. `search-jobs` with `status: draft`. Page through if there are more than 20.
3. For drafts the user wants to look at, `get-job` for the description.
4. Present a compact list: id, title, city, and a one-line note where useful (for example "internship", "not a tech role", "duplicate of 1234", "no apply link").
5. Ask what to do. Typical outcomes:
   - Publish: hand over to the `publish-jobs` skill with the chosen ids.
   - Discard: `discard-draft` without confirm for each, show the list, then with `confirm=true` after the user's yes. Owners and admins only.
   - Keep: nothing to do; drafts cost nothing.

Never discard or publish drafts the user did not explicitly choose.
