# Storage Audit — ~/Downloads and ~/Projects

_Scanned 2026-09-23 · 29,246 files · `.git` internals excluded · cleanup done the same day with approval_

## Result

| Area | Before | After |
|---|---|---|
| `~/Downloads` | 3.4 GB | **162 MB** (includes 6 MB waiting for review in `Duplicates/`) |
| `~/Projects` | 526 MB | 526 MB (unchanged, on purpose) |

**Recovered: ~3.2 GB.** Almost all of it came from deleting a stale copy of the GitHub Actions self-hosted runner that was sitting in `~/Downloads`.

## Actions taken

| Action | Space | Notes |
|---|---|---|
| Deleted `~/Downloads/actions-runner/` | ~3.3 GB | A stale copy (versions 2.335.1/2.336.0) of the live runner. First confirmed that the service runs only from `~/actions-runner/` (currently version 2.337.0), has its own credentials from a newer Aug 30 registration, and doesn't reference `~/Downloads`. The service was still `active` after the deletion. |
| Moved 5 duplicates into `~/Downloads/Duplicates/` | 6.0 MB | Filenames unchanged, as the `~/Downloads` CLAUDE.md requires. Nothing was deleted. See the table below. |
| Kept `~/Downloads/CLAUDE.md` | — | Identical to this repo's `CLAUDE.md`, but the Downloads copy is the working rules file. The one in this repo is documentation. |

## 1. Duplicate files (same name + same size)

Files were grouped by name and size (with `(1)`/`copy` suffixes ignored), then SHA-256 hashed to confirm.

- 4,056 name+size groups; **3,625 confirmed byte-identical**, worth **~801 MB**.
- ~775 MB of that was inside the runner copy, and deleting it removed all of those.
- About 430 more groups matched on name and size but had different contents (runner DLLs from different versions). They weren't true duplicates.

### Ranked by space freed (biggest first)

"Space freed" = file size × the number of extra copies, assuming you keep one copy.

| # | Space freed | Size each | Copies | Duplicate | Status |
|---|---|---|---|---|---|
| 1 | **199.8 MB** | 99.9 MB | 3 | Runner `node20_alpine/bin/node` (in `externals.2.335.1`, `externals.2.336.0`, `_work/_update`) | ✅ Deleted with the runner copy |
| 2 | **188.7 MB** | 94.3 MB | 3 | Runner `node20/bin/node` (same three folders) | ✅ Deleted with the runner copy |
| 3 | **125.4 MB** | 125.4 MB | 2 | Runner `node24_alpine/bin/node` | ✅ Deleted with the runner copy |
| 4 | **117.9 MB** | 117.9 MB | 2 | Runner `node24/bin/node` | ✅ Deleted with the runner copy |
| 5 | 143 MB total | ≤ 8 MB | 2–3 | ~3,600 smaller runner files (DLLs, `node_modules`) | ✅ Deleted with the runner copy |
| 6 | 6.5 MB | ≤ 1.7 MB | 2 | ~50 docs, screenshots and manifests shared between `Projects/Automation/GitHub-Actions-Basic-CI-CD-Pipeline/` and `Projects/k8s-projects/ecommerce-app/` | Kept (separate git repos) |
| 7 | 4.6 MB | 4.6 MB | 2 | `~/Downloads/ecommerce-app/` ≈ `~/Projects/k8s-projects/old-learning-app-ecommerce/` | 📦 Moved to `Duplicates/` |
| 8 | 312 KB | 312 KB | 3 | `~/Downloads/Images/cka.png` (also `CKA.png` in two project `docs/images/`) | 📦 Moved to `Duplicates/` |
| 9 | 309 KB | 309 KB | 3 | `~/Downloads/Images/CKAD.png` (also in two project `docs/images/`) | 📦 Moved to `Duplicates/` |
| 10 | 203 KB | 203 KB | 2 | `~/Downloads/css (2)/` = `~/Downloads/css/` | 📦 Moved to `Duplicates/` |
| 11 | 3 KB | 3 KB | 2 | `~/Downloads/Kubernetes-Configs/db-mariadb-deployment.yaml` = `Projects/k8s-projects/k8s-Helm/ecomwebapp/templates/db-mariadb-deployment.yaml` | 📦 Moved to `Duplicates/` |
| 12 | 1 KB | 1 KB | 2 | `~/Downloads/CLAUDE.md` = this repo's `CLAUDE.md` | Kept (working rules file) |

## 2. Files over 50 MB not modified in 6 months (before 2026-03-25)

Only **3 files (283 MB)** qualified, all the same 94.3 MB Node 20 binary inside the runner copy (modified 2026-03-23). ✅ All three were deleted with it. Nothing in `~/Projects` qualified.

Still present, just inside the 6-month window:
- `~/Downloads/Installers/google-chrome-stable_current_amd64.deb`: 119 MB, 2026-04-07

## 3. Empty folders (16 found, 13 remaining)

| Type | Folders | Recommendation |
|---|---|---|
| Truly empty leftovers | `~/Downloads/ecom-stack/`, `~/Downloads/charts/` | Safe to remove |
| Helm chart scaffolding (`charts/` subdirs made by `helm create`) | 6 in `~/Projects/k8s-projects/` (`old-learning-app-ecommerce/` ×4, `helm-tutorial/`, `k8s-Helm/`) | Keep — Helm expects them |
| Inside `~/Downloads/Duplicates/ecommerce-app/` | 4 Helm `charts/` folders and the empty `helm/ecom-stack/` | Go away when `Duplicates/` is reviewed and deleted |
| Runner runtime dirs | 3 folders | ✅ Gone with the runner copy |

Empty folders take essentially no space; removing them is just tidying.

## Remaining recommendations

1. **Review `~/Downloads/Duplicates/` (6.0 MB) and delete it** once you've confirmed the Projects copies are the ones you want to keep.
2. **Delete the Chrome `.deb` installer (119 MB)** if Chrome is already installed. It would bring `~/Downloads` down to about 43 MB.
3. **Remove the 2 empty folders** `~/Downloads/ecom-stack/` and `~/Downloads/charts/`.
4. **Trim the live `~/actions-runner/` (2.3 GB, outside this audit's scope): ~890 MB is recoverable.** The runner now runs 2.337.0 (its `bin`/`externals` symlinks point there), but the previous version is still on disk: `externals.2.336.0/` (595 MB), `bin.2.336.0/` (80 MB), and the `actions-runner-linux-x64-2.336.0.tar.gz` installer (216 MB). Leave the `2.337.0` folders and `_work/` alone.
5. **Check GitHub → repo Settings → Actions → Runners.** `kubeadm-node-runner` should show as Idle or Active. If a stale offline entry from the old May registration is still listed, remove it there.
6. **Leave the `~/Projects` duplicates alone.** They're shared docs and assets across separate git repos (~6.5 MB).
