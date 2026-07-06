# Resource Report: DVC (Data Version Control)

**URL:** https://dvc.org/
**Date Researched:** 2026-05-19
**Researched by:** Rose | Security pre-check: Soren (pending Step 2) | Report by: Rose

---

## What It Is

DVC (Data Version Control) is a free, open-source, platform-agnostic versioning system for large data files, ML models, and experiments. It integrates with Git by storing small metafile pointers (`.dvc` files) in the repository while offloading the actual large files to a configured remote storage backend — Google Drive, S3, Azure Blob, GCS, SSH, and others. For this project, DVC is positioned as a **contingency/optional tool** for Vicky (Videographer agent): it is not being deployed now, but is being cleared in advance so it is ready if Vicky's video library outgrows Git LFS. The existing `report-vicky-git-lfs.md` covers the primary tool; this report covers the fallback. DVC is maintained by lakeFS as of November 2025, following its acquisition from Iterative.ai, and remains 100% open source under the Apache 2.0 license with no planned licensing changes. Current stable version: **v3.67.1** (released March 31, 2026).

---

## What It Does

- Tracks large files and directories in Git via lightweight `.dvc` pointer metafiles, keeping the actual data in remote storage
- Pushes, pulls, and fetches data to/from remote backends (`dvc push`, `dvc pull`, `dvc fetch`)
- Versions datasets, model weights, and large media files alongside code — each Git commit maps to a specific data state
- Supports multiple remote backends: Google Drive, Amazon S3, Azure Blob Storage, Google Cloud Storage, SSH, HDFS, HTTP/HTTPS, and local/network paths
- Provides a pipeline system (`dvc repro`, `dvc.yaml`) to define and reproduce data processing workflows
- Enables experiment tracking and comparison (`dvc exp`) across runs
- Supports cache management with hardlinks, symlinks, or copy modes for local performance optimization
- Provides `dvc status` to detect data drift between local files, cache, and remote
- Outputs `dvc version` for environment diagnostics (Python version, OS, storage type, remotes configured)

---

## Invocation Interface

- **Typical command pattern:**
  ```
  dvc init                                      # initialize DVC in a Git repo
  dvc remote add myremote gdrive://[folder-id]  # configure Google Drive remote
  dvc add videos/raw/clip.mp4                   # track a file
  dvc push                                      # upload to remote
  dvc pull                                      # download from remote
  dvc status                                    # check sync state
  dvc version                                   # print environment info
  ```
- **Output format:** Plain-text progress bars during push/pull; structured YAML for pipeline definitions; `.dvc` metafiles are plain YAML with MD5/SHA256 hashes and size metadata
- **Key structured output flags:**
  - `--json` on select commands for machine-readable output
  - `-v` / `--verbose` for detailed logging
  - `--no-run-cache` on `dvc repro` to force re-execution
  - `dvc remote modify` for per-remote credential and configuration flags
- **Exit code behavior:** Exit 0 on success; non-zero on failure. `dvc status` exits non-zero when local state differs from remote, which is relevant in CI/CD gate logic.
- **Stdin/stdout/stderr notes:** Progress output goes to stderr; pipeline output is captured per stage. Commands are non-interactive after initial OAuth flow is completed and credentials are cached locally.

---

## Relevance to This Project *(as of 2026-05-19 — context may not carry to future projects)*

This tool is a **future-consideration contingency**, not an active deployment. Vicky's current data versioning solution is Git LFS (`report-vicky-git-lfs.md`). DVC + Google Drive remote becomes relevant only if the video library grows beyond Git LFS practical limits — typically when total asset size exceeds GitHub LFS storage quotas, or when the team needs finer-grained data pipeline reproducibility that LFS does not provide.

If that threshold is reached, DVC offers a clean migration path: Git LFS and DVC can coexist temporarily during transition, and DVC's Google Drive backend maps well to the existing Google Workspace environment this project already uses. Vicky would `dvc add` large video files, commit the `.dvc` pointer to Git, and push the actual media to a designated Google Drive folder. Data is then versioned reproducibly alongside the codebase without bloating the Git repository.

The lakeFS acquisition (November 2025) is worth noting for Soren's assessment: DVC is now stewarded by lakeFS under `treeverse/dvc` on GitHub. The project remains Apache 2.0, open roadmap, and actively released. This is a supportive ownership change — lakeFS has strong incentive to keep DVC healthy as a complement to their enterprise product — but it represents a stewardship shift that Soren should factor into the long-term risk rating for any production deployment.

---

## Builder Footprint

- **Integration type:** CLI tool + Python library (`pip install dvc[gdrive]` for Google Drive extras); integrates with Git via hooks and `.dvc` metafiles; no persistent daemon required
- **Extension points:** Remote backends are modular (install `dvc[s3]`, `dvc[gdrive]`, `dvc[azure]`, etc. as pip extras); pipeline stages defined in `dvc.yaml`; pre/post-commit Git hooks for cache checks
- **Build complexity signal:** Moderate (~2–4 hours) — initial setup, remote configuration, OAuth flow, and first successful push/pull cycle on Windows; ongoing usage is straightforward CLI
- **Known conflicts:** Partial overlap with Git LFS (they can coexist but serve different models — LFS is simpler; DVC is more powerful); `dvc add` on a file already tracked by Git LFS requires explicit migration; Windows symlink limitations require admin privileges or hardlink/copy fallback configuration

---

## Master Library Assessment

- **Proposed Section:** 3 — CLI
- **Proposed Tier:** 3
- **Rationale:** DVC is a mature, actively maintained CLI tool with a clean Apache 2.0 license and no current CVEs. Tier 3 reflects its contingency status for this project — cleared and ready, but not active in the current build phase.

---

## Soren Security Pre-check

*(Rose's security research summary — Soren completes the Verdict in Step 2)*

- **Verdict:** CLEARED — Provisional (contingency tool — not active deployment); TRCore CVE disambiguation confirmed (CVE-2024-11308/11311/11313/11315 are for an unrelated CCTV product, not this DVC); no CVEs against iterative/dvc or treeverse/dvc; lakeFS acquisition (Nov 2025) reviewed — Apache 2.0 license unchanged, active maintenance confirmed (v3.67.1 released March 2026), no security regression; Google Drive `drive` OAuth scope (full Drive read/write) is broad — service account auth is the safer configuration if adopted; credential token stored in plaintext JSON at local cache path (acceptable for provisional status; must be secured at adoption); follow-up Soren report required at adoption time specifying backend configuration; injection check: clean

- **Checked:** GitHub Advisory Database for GHSA entries against `iterative/dvc` and `treeverse/dvc`; NVD/CVE search for DVC vulnerabilities in the last 12 months; DVC GitHub repository security overview; Google Drive OAuth scope and credential storage model (official DVC documentation); PyPI package integrity and release history; Apache 2.0 license confirmation

- **Notes:**

**CVE / Advisory Status — Clean (with one important disambiguation):**

No CVEs or GitHub Security Advisories were found against `iterative/dvc` or `treeverse/dvc` in the last 12 months. Four CVEs (CVE-2024-11308, CVE-2024-11311, CVE-2024-11313, CVE-2024-11315) appeared in search results for "DVC" — these belong to a completely separate product called "DVC from TRCore" (a Taiwan-based CCTV/DVR management system) and are entirely unrelated to this tool. Soren should confirm this disambiguation holds on their own scan.

**Google Drive Authentication Model — Soren should review:**

DVC uses Google's OAuth 2.0 flow for Google Drive access. Key details:

- **Required OAuth scopes:** `https://www.googleapis.com/auth/drive` (full read/write access) and `https://www.googleapis.com/auth/drive.appdata` (configuration folder in Drive)
- The `drive` scope grants broad access to the entire Google Drive — this is the widest available scope; a narrower scope is not currently supported by DVC for standard user auth
- **Credential storage:** Stored locally in a JSON file at `$CACHE_HOME/pydrive2fs/{gdrive_client_id}/default.json` — plaintext token storage on disk. Alternatively, credentials can be passed via the `GDRIVE_CREDENTIALS_DATA` environment variable (JSON string)
- **Service account authentication:** Supported and is the recommended approach for CI/CD and shared environments — avoids interactive OAuth and limits scope when configured correctly. Client ID and client secret are safe to share (they only generate the auth URL); the credential token file should be protected.
- **Soren's specific review target:** Assess the broad `drive` scope (full Google Drive read/write) against the project's data access risk tolerance. Service account auth is the safer long-term configuration if this tool is ever activated.

**Stewardship note:** Ownership transferred from Iterative.ai to lakeFS (treeverse) in November 2025. The project is actively maintained (v3.67.1 released March 31, 2026), open roadmap, Apache 2.0 unchanged. No regression in security posture identified.

**License:** Apache 2.0 — confirmed. No copyleft restrictions. Commercial and internal use permitted without obligation.

**Windows-specific notes:** Symlinks need admin rights (opt-in via Windows Developer Mode or admin prompt); path length limit (260 chars) addressed via opt-in registry fix; hardlink limits on NTFS (1024 per file) are a cache management edge case. All documented and manageable.

---

## Recommendation

Clear for the Master Library as a Tier 3, Section 3 contingency resource for Vicky. No active CVEs against the correct product, Apache 2.0 license, and active maintenance under lakeFS ownership. Soren should confirm the TRCore CVE disambiguation on independent scan and assess the broad Google Drive OAuth scope (`drive`) against the project's data access risk tolerance — service account auth is the safer long-term configuration if this tool is ever activated.

---

## C&P Summary

DVC is a free, open-source command-line tool that lets you version-control large files — like videos — alongside your code in Git, by storing the actual files on a remote backend like Google Drive and keeping only small pointer files in Git. It is being cleared here as a backup option for Vicky: if the current solution (Git LFS) eventually hits storage limits, DVC plus a Google Drive remote is a proven upgrade path. DVC has no known security vulnerabilities, is actively maintained by lakeFS (who acquired it in late 2025), and is licensed under Apache 2.0. The main item for Soren's review is the Google Drive authentication model, which by default requests broad access to the entire Google Drive — the tool works, but that scope deserves a second look before any live deployment.

---
*Report by Rose | Session 161 | 2026-05-19*
