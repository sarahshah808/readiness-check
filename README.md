# The Readiness Check

SJ Group International's 12-question crisis readiness self-assessment. One self-contained page (`public/index.html`), no build step, no server, no data collected.

It is embedded on the website at sjgroupinternational.com/readiness-check (Wix, Embed Site element). When it is shown inside another site, or opened with `?embed=1`, it hides its own brand bar, title, intro and footer so the host page's heading isn't repeated. Opened directly, it shows the full version.

## Changing the wording

Everything is in `public/index.html`:

- The questions, and the next-step advice for each, are in the `Q` list near the bottom. Each question has organisation wording (`org`) and family wording (`fam`), a step title (`t`), and the organisation and family actions (`ao`, `af`).
- The four score bands (Early stages, Developing, Prepared, Ready) are in `BANDS`.
- The enquiry button goes to the website contact page with tracking tags, so enquiries from the check show up in analytics.

Commit and push, and Vercel redeploys automatically.

## Hosting

Vercel project, framework "Other", no build command, output folder `public`.

## Keeping results and the optional briefs sign-up

After the score, visitors can save their results as a PDF (the browser's print dialog, with a print layout that shows only the results) or copy them as text. Nothing is sent for either.

Below that is an optional form: "Want the Readiness Briefs for your focus areas?". Only if someone fills it in and presses send, the page posts their email, optional first name, who they answered for, score, band, focus area titles and whether they ticked "occasional insights" to the `readiness_leads` table in the SJ Group Supabase project. Individual answers are never sent.

- The table can be added to through the public key but never read through it (row level security, insert only, limited columns).
- A scheduled task copies new sign-ups each morning into the "Readiness Check sign-ups" database in Notion (Work Hub) and adds a to-do to send the briefs.
- The "occasional insights" box is unticked by default. Only people who ticked it should get anything beyond their briefs.

## Privacy

No accounts, cookies or analytics. Answers never leave the visitor's browser. The only personal data collected is what someone chooses to send through the optional briefs form, described above.
