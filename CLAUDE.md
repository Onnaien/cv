# CV repo — instructions

This repo has two parallel CV pages (`index.html` in Norwegian, `en/index.html`
in English) and two static PDFs (`Morten_Undheim_CV_no.pdf`,
`Morten_Undheim_CV_en.pdf`) that are print snapshots of those pages. The PDFs
are **not** generated on the fly — they go stale the moment the HTML changes
unless regenerated.

Whenever content changes (wording, job titles, dates, skills, anything visible
on the page — not pure styling/layout tweaks), do all of the following:

1. **Edit both `index.html` and `en/index.html`.** Translate naturally rather
   than copying Norwegian phrasing — match the tone already used in the
   English version. If wording is ambiguous (e.g. replace vs. append), ask
   rather than guessing — CV accuracy matters. If a change only makes sense
   in one language, say so and confirm before skipping the other file.

2. **Regenerate both PDFs** from the updated HTML using headless Edge (same
   renderer that produces the `@media print` / `@page A4` layout, so output
   matches what "Download as PDF" would produce):

   ```bash
   EDGE="/c/Program Files (x86)/Microsoft/Edge/Application/msedge.exe"
   SCRATCH="<session scratchpad dir>"
   "$EDGE" --headless --disable-gpu \
     --print-to-pdf="$SCRATCH/Morten_Undheim_CV_no.pdf" \
     "file:///C:/git/cv/index.html"
   "$EDGE" --headless --disable-gpu \
     --print-to-pdf="$SCRATCH/Morten_Undheim_CV_en.pdf" \
     "file:///C:/git/cv/en/index.html"
   ```

   Edge refuses to write directly into the repo path (access denied) — render
   into the scratchpad dir first, then copy both files over the repo's
   `Morten_Undheim_CV_no.pdf` / `Morten_Undheim_CV_en.pdf`.

3. **Verify** by reading the regenerated PDFs (the Read tool supports PDF)
   and confirming the edited content shows up correctly on both.

4. **Ask before committing/pushing.** This is a public GitHub Pages site, so
   a push is a public, visible action — don't do it without confirmation,
   even though steps 1–3 can happen freely.
