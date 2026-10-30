---
name: draft-job
description: Turn a job description, a careers page link, an ATS export or rough notes into a Techify draft. Use when the user wants to post, write, create or prepare a job ad on Techify.
---

# Draft a job

## Steps

1. Get the content. If the user gave a link, read the page. If they gave notes, ask only for what is missing and essential: title, location (Swiss city or Remote), where candidates apply (URL).
2. Write the description for Techify readers, engineers in Switzerland:
   - Start with two or three sentences about the company and the team.
   - Then short sections, each with a heading line and a list: what you will do, what you bring, what we offer.
   - Keep facts from the source. Do not invent salary, benefits, stack or perks. Mention the salary range in CHF only if the source has one.
   - Plain text is fine: blank lines between paragraphs, list lines start with `- `.
3. Pick a stable `reference`: the requisition id from the ATS if there is one, otherwise a short slug of the title and city.
4. Show the user the title, location, apply URL and the description, and ask if it is right. Skip this if they asked you to go ahead.
5. Call `save-draft`. Report the result: created or updated, the draft id, and the review link. Say clearly that the draft is private and free.
6. Offer to publish it with the `publish-jobs` skill. Do not publish without being asked.

## Notes

- One job per draft. For several jobs, repeat with distinct references.
- If `save-draft` says a published job already uses the reference, the job is live; changes to live jobs are made in the workspace, not here.
