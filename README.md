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

## Privacy

No accounts, cookies, analytics or personal data. Answers never leave the visitor's browser.
