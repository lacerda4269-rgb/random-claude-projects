# Resource Report: Git LFS

**URL:** https://git-lfs.com/
**Date Researched:** 2026-05-19
**Researched by:** Rose | Security pre-check: Soren (pending Step 2) | Report by: Rose

---

## What It Is

Git Large File Storage (Git LFS) is an open-source Git extension, maintained by GitHub, that replaces large binary files stored in a repository with small, lightweight text pointer files. The actual binary content is stored on a remote LFS server — in this project's case, GitHub's LFS service — and downloaded on demand rather than on every clone or fetch. It integrates transparently with standard Git workflows: `git add`, `git push`, and `git pull` all work as normal, with Git LFS handling the binary transfer layer invisibly in the background. The project is MIT-licensed, hosted at github.com/git-lfs/git-lfs, and is officially supported by GitHub. Current stable version as of research date is **v3.7.1**, released October 16, 2025.

---

## What It Does

- Intercepts Git operations for file types defined in `.gitattributes` and routes binary content to the LFS remote instead of the standard Git object store
- Stores a small text pointer file (containing the file's SHA-256 hash, size, and LFS version) in the Git history in place of the binary blob
- Downloads actual binary content on `git checkout`, `git pull`, or `git lfs pull` — only when the working tree needs it
- Tracks any file type by pattern: `git lfs track "*.mp4"` writes the rule to `.gitattributes`
- Supports selective fetch: `git lfs fetch --recent`, `git lfs fetch --all`, or fetch by specific OID
- Exports object URLs and HTTP metadata as JSON via `git lfs ls-files --json` (added in v3.7.0) for external tooling
- Migrates existing repos to LFS (`git lfs migrate import`) and migrates LFS content back to standard Git (`git lfs migrate export`)
- Works with any LFS-compatible remote: GitHub, GitHub Enterprise, Azure DevOps, Bitbucket, self-hosted servers
- Provides a local pointer cache with configurable in-memory path-pattern matching (v3.7.0+) for large-repo performance

---

## Invocation Interface

- **Typical command pattern:**
  ```
  git lfs install                     # one-time setup per machine
  git lfs track "*.mp4"               # add file type to .gitattributes
  git lfs ls-files                    # list tracked LFS files in working tree
  git lfs pull                        # download LFS objects for current branch
  git lfs fetch --recent              # pre-fetch recent branches' LFS objects
  git lfs push origin main            # push LFS objects to remote
  git lfs status                      # show staged LFS file changes
  git lfs env                         # show LFS configuration and remote info
  ```
- **Output format:** Plain text to stdout for most commands. `git lfs ls-files --json` outputs structured JSON (v3.7.0+). `git lfs env` outputs key=value configuration lines.
- **Key structured output flags:** `--json` on `git lfs ls-files`; `--porcelain` on `git lfs status`; `--dry-run` on `git lfs push` and `git lfs migrate`
- **Exit code behavior:** Exit 0 on success. Non-zero on authentication failure, unreachable remote, pointer corruption, or attempted write to a file that would follow a symlink (v3.7.1 behavior post-CVE fix). Treat any non-zero as an error requiring investigation.
- **Stdin/stdout/stderr notes:** Progress output goes to stderr; clean stdout output makes JSON and list commands pipe-safe. Authentication prompts may appear on stderr when no credential helper is configured.

---

## Relevance to This Project *(as of 2026-05-19 — context may not carry to future projects)*

Vicky's core workflow produces video project files that span a wide range in size and type: scripts and SRT subtitle files that are a few kilobytes, small exported clips and project metadata under 50 MB, and large source footage or final exports that can reach tens of gigabytes. Git handles the first category cleanly with no extensions. Without LFS, the second category would gradually bloat the repository history even if the files are later deleted, because Git stores every version of every file as a full blob. Git LFS solves this directly: the repo history stays lean, binary files are version-controlled with full pointer tracking, and the actual content is fetched on demand.

The hybrid storage model recommended in the META report is the practical answer to GitHub's LFS quota. Small working files — scripts, SRT files, metadata, exported clips under 50 MB — go into the Git repo with LFS tracking for the video container formats (`*.mp4`, `*.mov`, `*.mkv`, `*.wav`). Large source footage, full-resolution exports, and archives stay in Google Drive or YouTube (unlisted). The Git repo holds an index or README linking to Drive/YouTube for those binary assets. This keeps monthly LFS bandwidth consumption low and makes the free tier (10 GB storage / 10 GB bandwidth — note: META report cited 1 GB; confirmed 2026 limit is 10 GB per the current GitHub billing docs) sufficient for normal Vicky operation.

One operational consideration: `git lfs install` must be run once per machine after Git LFS is installed, and the `.gitattributes` file must be committed and pushed before any tracked binary files are added. If `.gitattributes` is added after binaries are already committed, a `git lfs migrate import` pass is required to rewrite history — a recoverable but avoidable extra step. Establishing the tracking rules before Vicky's first binary commit is the correct build sequence.

---

## Builder Footprint

- **Integration type:** CLI extension — installed system-wide, invoked via `git lfs` subcommands; hooks into Git's clean/smudge filter mechanism via `.gitattributes` and `git lfs install`
- **Extension points:** `.gitattributes` file controls which file patterns are LFS-tracked; `lfs.url` config key allows pointing to a custom LFS server; `lfs.fetchrecentrefsdays` and related keys control auto-fetch behavior
- **Build complexity signal:** Simple (~30–60 minutes including installation, initial `git lfs install`, `.gitattributes` setup, and a test push/pull cycle to confirm LFS objects are flowing correctly)
- **Known conflicts:** None identified. Git for Windows bundles Git LFS in its installer as of recent versions — running a separate `git lfs install` after the Git for Windows installer is harmless and recommended to ensure hooks are wired correctly.

---

## Master Library Assessment

- **Proposed Section:** 3 — CLI
- **Proposed Tier:** 2
- **Rationale:** Git LFS is a Git extension invoked via the command line as a direct dependency of Vicky's version control workflow. Tier 2 reflects that it is a project-critical supporting tool for a specific agent (Vicky) rather than a universal infrastructure component used across all agents.

---

## Soren Security Pre-check

*(Rose's security research summary — Soren completes the Verdict in Step 2)*

- **Verdict:** CLEARED WITH CONDITIONS — CVE-2025-26625 (HIGH, CVSS 8.6 — symlink traversal allowing arbitrary file write) is fully patched in v3.7.1; v3.7.1 is the required minimum (prior Session 105 clearance did not have this CVE — new finding, prior clearance superseded); fine-grained PAT scope "Contents: Read and Write" to be confirmed on current GitHub token model before deployment; Git Credential Manager must be configured on Windows; GitHub free LFS tier confirmed at 10 GB (META report correction); injection check: clean

- **Checked:** CVE database and GitHub Security Advisories for Git LFS (last 12 months); GitHub free tier LFS billing documentation (2026 confirmed); Git LFS authentication model and PAT scope requirements; Windows-specific installation and behavior notes

- **Notes:**

**CVE-2025-26625 — HIGH:**

| # | Severity | Flag | Notes |
|---|----------|------|-------|
| 1 | HIGH | CVE-2025-26625 (CVSS v4.0: 8.6) | `git lfs checkout` and `git lfs pull` did not check for symbolic or hard links before writing LFS object content to the working tree. A crafted repository could cause Git LFS to write files to arbitrary filesystem locations accessible to the running user. Root cause: `SmudgeToFile` used `os.Create` which follows symlinks. Fixed by replacing with `os.Remove` + `os.OpenFile` with `O_EXCL` flag; path components now validated using `os.Lstat` (does not follow symlinks). **Affected versions: 0.5.2 through 3.7.0. Fully patched in v3.7.1.** No further action required if deployed on v3.7.1. |

No other CVEs or HIGH/CRITICAL advisories against Git LFS were identified in the last 12 months.

**Access Pattern Flag — GitHub Token Authentication (flagged in META report):**

Git LFS communicates with GitHub's LFS API over HTTPS and requires authentication. Token scope requirements:

- **Classic PAT:** The `repo` scope is required in full for private repositories. A token scoped only to `public_repo` is insufficient for private repos.
- **Fine-grained PAT (GitHub's recommended token type as of 2025–2026):** Requires **Contents: Read and Write** permission on the target repository. Fine-grained tokens can be scoped to a single repository, which is the safer posture.
- **HTTPS only:** Git LFS authentication over SSH is not supported. The remote URL must be an HTTPS URL, not SSH. If the main repo uses SSH, the LFS remote can be configured separately via `lfs.url` in `.gitconfig` or `.lfsconfig`.
- **Credential helper dependency:** Git LFS uses Git's credential helper chain. On Windows, Git Credential Manager (GCM), installed with Git for Windows, handles token storage and refresh. Without a credential helper configured, Git LFS will prompt for credentials on every LFS operation.
- **GitHub Actions / CI:** `GITHUB_TOKEN` can authenticate Git LFS in automated contexts if the workflow has `contents: write` permission. No separate PAT needed in standard Actions workflows.
- **Soren's confirmation needed:** Verify that fine-grained PAT with "Contents: Read and Write" scoped to Vicky's repository is the correct and sufficient token configuration on GitHub's current token model.

**GitHub Free Tier LFS Limits — META Report Correction:**

The META report cited 1 GB free storage / 1 GB bandwidth. This is outdated. Confirmed 2026 GitHub billing documentation shows:

| Account tier | LFS Storage | LFS Bandwidth |
|---|---|---|
| Free / Pro | **10 GB** | **10 GB/month** |

Overage pricing: $0.07/GB storage, $0.0875/GB bandwidth. Data packs: $5/month for +50 GB storage and +50 GB bandwidth. Budget cap at $0 blocks LFS usage rather than incurring charges — a useful guardrail. The 10 GB free tier is materially more generous than the META report assumed; combined with the hybrid storage model, free-tier operation for Vicky is viable without budget concern under normal conditions.

**Windows-Specific Notes:** `winget install GitHub.GitLFS` or `choco install git-lfs` (package is v3.7.1 on Chocolatey). After any installation method, `git lfs install` must be run once in a terminal to register the Git hooks. A shell restart may be required for PATH changes to take effect.

---

## Recommendation

Deploy Git LFS v3.7.1 for Vicky's version control layer. CVE-2025-26625 is fully resolved in the current release — deploying the patched version eliminates the only identified security risk. The GitHub free tier limits are more generous than the META report assumed (10 GB, not 1 GB). Before deployment, Soren should confirm the fine-grained PAT scope ("Contents: Read and Write") is sufficient for LFS operations on GitHub's current token model, and Git Credential Manager should be confirmed configured on Vicky's Windows environment so authentication does not block automated LFS operations.

---

## C&P Summary

Git LFS is a well-maintained GitHub-backed Git extension that keeps video project repositories from bloating by storing large binary files (video clips, audio files) on GitHub's servers rather than inside the Git history itself. The current version, 3.7.1, patches the one significant security vulnerability found in the last year — a file-write vulnerability in older versions that is fully fixed. GitHub's free tier now includes 10 GB of LFS storage and 10 GB of monthly bandwidth (the META report cited 1 GB — the limit has since been raised), which makes free-tier operation comfortable for Vicky's hybrid storage workflow. Installation on Windows is straightforward via winget or Chocolatey, and the only item needing Soren's confirmation before deployment is the exact token permission scope required for the LFS authentication step.

---
*Report by Rose | Session 161 | 2026-05-19*
