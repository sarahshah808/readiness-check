# The Readiness Check

SJ Group International's crisis readiness self-assessment: five situation questions (giving an exposure score and the situations most worth planning for) and twelve readiness questions. One self-contained page (`public/index.html`), no build step, no server, no data collected.

It is embedded on the website at sjgroupinternational.com/readiness-check (Wix, Embed Site element). When it is shown inside another site, or opened with `?embed=1`, it hides its own brand bar, title, intro and footer so the host page's heading isn't repeated. Opened directly, it shows the full version.

## Changing the wording

Everything is in `public/index.html`:

- The five situation questions are in `SIT`. Each option scores 0, 1 or 2 towards the exposure score, and `EXPO_BANDS` holds the four exposure bands.
- The situations shown in the results, with their first-hour steps, are in `SCEN`. The two with the highest score from the situation answers are shown.
- Three audiences: `fam` (private), `fo` (family office) and `org` (organisation). Family offices use their own wording where a question has it (`fo`, `optsFo`, `afo`, `whyFo`), otherwise the organisation wording.
- Advisers ("I advise clients") can copy a link or a short message to send to a client, or answer on a client's behalf. `adv` is true in that case, and the results and PDF say they're for a client.
- Sign-ups record the audience and adviser mode in `source` (for example `readiness-check:adviser-family-office`). The Supabase insert policy only accepts the values listed there, so add any new mode to the policy too.
- The readiness questions, and the next-step advice for each, are in the `Q` list near the bottom. Each question has organisation wording (`org`) and family wording (`fam`), a step title (`t`), and the organisation and family actions (`ao`, `af`).
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
