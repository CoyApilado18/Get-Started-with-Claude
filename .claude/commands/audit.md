---
description: Monthly storage audit of ~/Downloads and ~/Projects — duplicates, large stale files, empty folders — written to storage-audit.md
argument-hint: "[extra folders to scan]"
---

Run a storage audit of `~/Downloads/` and `~/Projects/` (plus any extra folders given here: $ARGUMENTS).

**Don't delete, move, or rename anything during the audit.** This is read-only until I approve specific actions.

## 1. Scan

Walk every folder, skipping `.git` internals, and record each file's path, size, and modified time. For a large tree, run the scan in the background and wait for it to finish.

Find:

1. **Duplicate files.** Group files by name and size, treating `report(1).pdf`, `report (2).pdf`, `report copy.pdf` and `report.pdf` as the same name, and skipping 0-byte files. Then SHA-256 hash each group to confirm the files are byte-identical. Report groups that match on name and size but differ in content separately; those aren't real duplicates.
2. **Files over 50 MB not modified in the last 6 months.** Also list large files just inside the window for reference.
3. **Empty folders.** Say which are leftovers and which are expected, like Helm `charts/` scaffolding or tool runtime dirs.

## 2. Analyze

- **Rank duplicates by space freed** (file size × extra copies), biggest first.
- **Roll up noise.** When thousands of duplicates come from one tool or vendored folder (e.g. a GitHub Actions runner copy, `node_modules`, SDK installs), collapse them into one row and find out what that folder is. Check whether a live service or process uses it (`systemctl`, `pgrep`, symlink targets, config paths) before recommending removal, and flag any credentials or secrets inside it.
- **Spot duplicate folders.** Look for whole folders that duplicate each other, like `css/` vs `css (2)/`, or a Downloads folder that's also a project in `~/Projects` (compare with `diff -rq`).
- **Protect some duplicates.** Never recommend moving `~/Downloads/CLAUDE.md`; it's the working rules file for Downloads. Files shared across separate git repos in `~/Projects` should be kept.
- **Compare with last time.** If `storage-audit.md` already exists, read it first and add a short "Since last audit" section: space change, new large files, and whether earlier recommendations were done.

## 3. Report

Draft the report in the scratchpad, **not** the final location. Include:

- A result table: size of each scanned folder (and before/after, if actions were taken)
- A TL;DR with the headline finding and the total recoverable space
- Duplicates ranked by space freed, with a recommended action per row
- Large stale files
- Empty folders, grouped by type
- Numbered recommendations, with how much space each one recovers

Show me the full report and **wait for approval before saving** to `~/Projects/Claud-Projects/Get-Started-with-Claude/storage-audit.md`.

## 4. Act (only with approval)

- For duplicates in `~/Downloads`, follow `~/Downloads/CLAUDE.md`. Show the exact move plan into `~/Downloads/Duplicates/` (top level, original filenames, no clashes) and wait for an explicit "approve" before moving anything.
- Delete only what I explicitly tell you to delete, and verify the result afterwards (e.g. the live service is still active).
- Once actions are done, update the report with an "Actions taken" section and a before/after table. Show it to me again before saving.
