# DOB Reference Library

Common Projekts' primary-source NYC code reference, built for answering DOB objections fast and for grounding future plan questions. Every PDF is fetched directly from nyc.gov or zr.planning.nyc.gov, never from code-summary sites, and verified to contain the sections cited.

This repo is one of three synchronized layers:

1. **This repo**: the portable copy, clonable from any Claude session (cloud or desktop).
2. **iCloud working copy**: `COMMON_PROJEKTS/DOB Reference Library/` on the CP laptop. Same files. This is the folder drawings teams browse.
3. **Supabase `dob_reference` table** (project stxmwoprgduoxrhveqsb): one row per code section with citation, summary, objection history (job, date, examiner, objection, resolution), PDF filename, and source URL. Queryable from any session.

`_INDEX.md` is the wiki index: one entry per document with its key sections, which objection brought it into the library, and the source URL, plus an objection cross-reference table.

## Conventions

- Primary source only (nyc.gov, DCP). Note the code year or edition on every entry; CC chapters are marked 2014CC or 2022CC in the file name, NYCECC is 2025.
- When a new objection cites a section: fetch the chapter PDF if missing, add or update the `_INDEX.md` entry, and log the objection into `dob_reference.objection_history`.
- Keep all three layers in sync. A file added here should land in the iCloud folder and get a row (or row update) in Supabase.
- No em dashes in library text.

## Standing rule: nyc.gov fills the gaps (David, 2026-11-05)

1. Check this library first.
2. If the chapter or section is not here, use the official nyc.gov publication directly (DOB code PDFs; zr.planning.nyc.gov for zoning). That is a primary source and is good enough to cite. Never a third-party code site, never recollection.
3. Then fill the gap: add the chapter PDF here, add its `_INDEX.md` entry, add `dob_reference` rows for the sections used, and flip its line in `CATALOG_2022_Construction_Codes.md` to IN LIBRARY.
4. Keep going until every chapter in the catalog is in. `CATALOG_2022_Construction_Codes.md` is the progress tracker.

Edition rule: filings made on or after 11.07.2022 use the 2022 Construction Codes; the 2014 files here are kept for older jobs. Energy is the 2025 NYCECC.

2022 URL pattern (verified 2026-11-05): `https://www.nyc.gov/assets/buildings/codes-pdf/cons_codes_2022/<file>`, file names as listed in the catalog. Library file names follow `<code>_Ch<nn>_<Title>_2022CC.pdf`.

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
