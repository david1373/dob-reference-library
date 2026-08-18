# DOB Reference Library

Common Projekts' primary-source NYC code reference, built for answering DOB objections fast and for grounding future plan questions. Every PDF is fetched directly from nyc.gov or zr.planning.nyc.gov, never from code-summary sites, and verified to contain the sections cited.

This repo is one of three synchronized layers:

1. **This repo**: the portable copy, clonable from any Claude session (cloud or desktop).
2. **iCloud working copy**: `COMMON_PROJEKTS/DOB Reference Library/` on the CP laptop. Same files. This is the folder drawings teams browse.
3. **Supabase `dob_reference` table** (project stxmwoprgduoxrhveqsb): one row per code section with citation, summary, objection history (job, date, examiner, objection, resolution), PDF filename, and source URL. Queryable from any session.

`_INDEX.md` is the wiki index: one entry per document with its key sections, which objection brought it into the library, and the source URL, plus an objection cross-reference table.

## Conventions

- Primary source only (nyc.gov, DCP). Note the code year or edition on every entry; the CC chapters here are the 2014 code (the Powers job's code year), NYCECC is 2025.
- When a new objection cites a section: fetch the chapter PDF if missing, add or update the `_INDEX.md` entry, and log the objection into `dob_reference.objection_history`.
- Keep all three layers in sync. A file added here should land in the iCloud folder and get a row (or row update) in Supabase.
- No em dashes in library text.

## Sync notes

- Do NOT clone this repo inside the iCloud folder. iCloud sync corrupts `.git` directories. Clone somewhere like `~/Repos/` and copy files to or from the iCloud folder.
- Fetching from nyc.gov by script requires a browser User-Agent header; plain requests return 403.
- 2014 CC chapter URL pattern: `nyc.gov/assets/buildings/codes-pdf/cons_codes_2014/2014CC_<code>_Chapter_<n>_<Title>.pdf` (naming is inconsistent between chapters).
- ZR chapter PDFs: each zr.planning.nyc.gov chapter page links `/sites/default/files/article/<article-id>/chapters/Chapter%20<n>.pdf` (Art I=32, Art II=39, Art V=42).

## First push

From the unzipped repo directory, after creating an empty private repo on GitHub:

```
git remote add origin git@github.com:<your-account>/dob-reference-library.git
git push -u origin main
```
