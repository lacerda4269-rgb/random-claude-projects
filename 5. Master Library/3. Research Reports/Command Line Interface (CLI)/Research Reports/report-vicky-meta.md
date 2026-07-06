# META Report: Vicky — Videographer Agent Toolset

**Prepared by:** Rose, Research Specialist
**Date:** 2026-05-02
**Status:** Filed — Pending Soren Review
**Report type:** META — Full toolset recommendation for new agent build
**Requested by:** Sage (CEO) — Vicky soul build and SOP foundation
**Routing note:** All Soren-flagged items must clear Soren's pipeline before Vicky uses them in any build.

---

## Who Vicky Is

Vicky is the team's Videographer — a new agent with no soul built yet. Her domain covers the full video production layer: trimming, cutting, and assembling clips; adding AI-generated captions and subtitles; generating short AI video content from text or image prompts; enhancing audio; combining clips into finished deliverables; and managing file size for platform-specific constraints, primarily Discord upload limits. She operates in a Windows environment alongside the rest of the team. She is not a coder-first agent — her tools should be operable via desktop GUI where CLI or API is not practical — but she should be capable of running programmatic workflows when Pete (Python Specialist) builds them for her. This report defines Vicky's full toolset before her soul is written.

---

## Tool Landscape Summary

Vicky's work breaks into four distinct layers, each requiring a different type of tool:

**Layer 1 — Video manipulation (trim, cut, concatenate, compress):** This is a solved problem with mature open-source tooling. FFmpeg is the industry engine underneath almost everything. For Vicky, the question is which interface layer sits on top — raw FFmpeg CLI, MoviePy (Python abstraction), HandBrake (GUI for compression), or a combination.

**Layer 2 — AI video generation (text-to-video, image-to-video):** This is where the landscape is fragmented. No single tool dominates, access tiers vary wildly, and cost is the central constraint. The options split into: web-only free tiers (limited but zero cost), subscription-required paid APIs (Runway, Kling paid, Pika paid), and one genuinely free option via Google (Veo 3.1 via Google Vids — 10 free generations/month for any personal Google account). There is no programmatic API access to any AI video generation tool within the team's current subscription footprint.

**Layer 3 — Auto captions and subtitles:** Solved problem. OpenAI Whisper (open-source, local-running) generates transcription from video audio and outputs SRT files. Combined with FFmpeg to burn or attach subtitles, this is a fully self-contained, free, offline pipeline. Soren flag applies to the Whisper download/install.

**Layer 4 — Version control:** GitHub LFS handles binary video files adequately at small-to-medium scale. Free tier on GitHub provides 1 GB storage/bandwidth. Practical for a video agent producing short clips — will hit limits fast if Vicky stores many full-length source files. Strategy needed.

**What is NOT available within current subscriptions:**
- Runway API (requires separate paid Runway subscription — not included in any current plan)
- OpenAI video generation API (ChatGPT Plus is web UI only, no API)
- Any other paid video generation API

---

## META Picks by Category

---

### Category 1: Core Video Editing and Manipulation

**META Pick: FFmpeg (via ffmpeg-python wrapper or direct CLI)**

**What it is:** FFmpeg is the de facto open-source standard for video processing — trim, cut, split, concatenate, re-encode, compress, extract audio, burn subtitles, convert formats. It runs as a command-line tool on Windows, Mac, and Linux. The `ffmpeg-python` PyPI package provides a clean Python API wrapper. HandBrake is a GUI application that runs FFmpeg under the hood and adds a visual interface for compression work.
- FFmpeg GitHub: https://github.com/FFmpeg/FFmpeg
- ffmpeg-python PyPI: https://pypi.org/project/ffmpeg-python/
- HandBrake: https://handbrake.fr | v1.10.2 (stable, 2026)
- MoviePy v2.2.1: https://pypi.org/project/moviepy/

**Why it's the best pick:** Nothing at this cost level comes close for raw capability. Every major video platform ultimately encodes via FFmpeg-derived tools. It handles every format Vicky will ever encounter. The CLI is scriptable for automation; HandBrake covers the GUI use case for compression without scripting knowledge.

**Where MoviePy fits:** MoviePy (v2.2.1) is a Python abstraction layer over FFmpeg. It is easier to read and write in Python scripts — good for prototyping and building automation with Pete. Important limitation: MoviePy is significantly slower than direct FFmpeg calls for the same tasks. A subclip operation that takes milliseconds with raw `ffmpeg -c copy` takes 20+ seconds in MoviePy due to frame-by-frame import/export overhead. Use MoviePy for rapid scripting and compositing; use direct FFmpeg calls or ffmpeg-python for any performance-sensitive operations (batch compression, splitting, large file work).

**Where HandBrake fits:** HandBrake is Vicky's GUI option when she needs visual control over compression settings without scripting — especially for Discord size optimization. It exposes constant-quality encoding, resolution control, codec selection (H.264/H.265), and point-to-point range encoding (trim without a script).

**How Vicky uses it:**
- Trim/cut: `ffmpeg -ss [start] -to [end] -i input.mp4 -c copy output.mp4` (stream copy — no re-encode, near-instant)
- Compress for Discord: HandBrake GUI with H.265 codec, 720p, 30fps, target bitrate adjusted to size limit — OR ffmpeg with `-b:v [target_bitrate]` to hit a specific file size
- Split into segments: `ffmpeg -i input.mp4 -f segment -segment_time [seconds] -c copy output_%03d.mp4`
- Concatenate clips: FFmpeg concat demuxer via text file list
- Extract audio: `ffmpeg -i input.mp4 -vn -acodec copy audio.aac`
- Burn subtitles: `ffmpeg -i input.mp4 -vf subtitles=subs.srt output.mp4`

**Cost:** Free. FFmpeg is LGPL/GPL open-source. HandBrake is GPL open-source. ffmpeg-python is MIT license. No subscription required.

**Soren flag:** YES — deployable installs required. Flag details in Soren Flags section.

---

### Category 2: Auto Captions and Subtitles

**META Pick: OpenAI Whisper (local, open-source) + FFmpeg subtitle burn**

**What it is:** Whisper is OpenAI's open-source automatic speech recognition model. It runs entirely locally — no API key, no internet connection, no ongoing cost. It accepts a video or audio file, transcribes the speech, and outputs an SRT subtitle file. That SRT is then used by FFmpeg to either burn captions into the video (hardcoded) or attach as a subtitle track (softcoded).
- Whisper GitHub: https://github.com/openai/whisper
- faster-whisper (optimized variant): https://github.com/SYSTRAN/faster-whisper
- auto-subtitle (CLI wrapper): https://github.com/m1guelpf/auto-subtitle

**Why it's the best pick:** No cost, no API dependency, runs offline, handles multiple languages, produces SRT files that are the universal subtitle standard. The faster-whisper variant runs significantly faster than base Whisper and produces the same output. A 2-minute video transcribes in under 30 seconds on typical hardware.

**How Vicky uses it:**
1. Run Whisper on the video: `auto-subtitle input.mp4 --model medium` → produces `input.srt`
2. Review/edit SRT in any text editor if corrections needed
3. Burn with FFmpeg: `ffmpeg -i input.mp4 -vf subtitles=input.srt output_captioned.mp4`

**Cost:** Free. MIT license.

**Soren flag:** YES — deployable install. Flag details in Soren Flags section.

---

### Category 3: AI Video Generation

**META Pick (Web-Only, Free): Google Vids / Veo 3.1 — primary free path**
**META Pick (Web-Only, One-Time Credits): Runway ML Free Plan — secondary**
**META Pick (Web-Only, Best Daily Free Volume): Kling AI Free Tier — tertiary for volume**

**What it is:**

**Google Vids / Veo 3.1:**
As of April 2, 2026, every personal Google account gets 10 free AI video generations per month via Google Vids (https://vids.new) using Google's Veo 3.1 model. No credit card. No trial. Permanently free. Output: 720p, up to 8 seconds per clip. Text-to-video and image-to-video both supported. The operator has a free Google account — this is immediately accessible.

**Runway ML Free Plan:**
Runway (https://runwayml.com) offers a free-forever plan with 125 one-time credits that do not expire and do not refresh. Access to Gen-4 Turbo model. All free-tier outputs carry a Runway watermark. At 5 credits/second for Gen-4 Turbo, 125 credits = 25 seconds of AI video total. Limited but zero-cost. Web interface only.

**Kling AI Free Tier:**
Kling (https://klingai.com) offers 66 free credits daily, refreshed every day. Can generate 3–6 short clips per day on the free tier. Outputs at lower resolution (360p–540p) with watermarks on the free tier. Web UI only — no API without a paid plan.

**Why this configuration is the right call:** There is no AI video generation API available within the current subscription footprint. The honest recommendation is to use web-based free tiers for AI generation. Google Vids is the cleanest: best model quality available for free, 10 solid generations/month, and tied to a Google account the operator already has.

**The honest ceiling:** Vicky cannot do high-volume AI video generation without a paid subscription. Google Vids gives 10/month. Runway gives 125 one-time credits total. Kling gives 66 daily credits but at low resolution with watermarks. If this project eventually requires significant AI video generation volume, a paid Runway subscription ($15–28/month) or Kling paid plan ($6.99–$36/month) is the path.

**Cost:**
- Google Vids/Veo 3.1: Free with existing Google account. No new cost.
- Runway free plan: Free. 125 one-time credits.
- Kling free tier: Free. 66 daily credits.

**Soren flag:** These are web-UI tools only — no deployable install. No Soren flag for the tools themselves.

---

### Category 4: LLM Access Beyond Claude

**Finding: No practical path to additional LLM API access within current subscriptions.**

The $100/month Claude Code subscription provides Claude API access via `ANTHROPIC_API_KEY`. The $20/month ChatGPT Plus subscription is a web UI consumer product — no API key, no programmatic access. The $20/month Cursor subscription is an IDE — no LLM API offered. No other subscriptions are active.

**What this means for Vicky specifically:** Vicky does not need LLM API access for her core video work. FFmpeg, Whisper, and HandBrake are all offline/local. AI video generation is handled via web UIs. If Vicky ever needs to integrate AI text generation into a video pipeline (e.g., generate a script for a voiceover), she uses Claude via the existing API.

**Bottom line:** Claude is Vicky's only LLM. That is sufficient for her core use cases.

---

### Category 5: Google Tools for Video and Storage

**Finding: Google Drive and YouTube are the practical tools. Google Vids is the AI generation access point.**

**Google Drive (Free 15 GB):**
The operator's free Google account includes 15 GB of Google Drive storage. Drive supports direct sharing links, is accessible from any browser, and accepts video uploads in all major formats. This is Vicky's best backup and sharing layer for video assets that exceed GitHub LFS capacity. Sharing a Drive link in Discord bypasses the 10MB upload limit entirely.

**YouTube (Free, Unlimited hosting):**
YouTube is a free, unlimited video hosting platform tied to the operator's Google account. Vicky can upload videos as unlisted to keep them private, share the link in Discord for playback without file transfer, and maintain a library of published content. Zero storage cost. Best long-term storage solution for finished video work.

**Google Vids / Veo 3.1:**
Already covered in Category 3. Access point is https://vids.new.

**Google Photos:** Not relevant. Lacks production video editing capability.

**Google Meet Recording:** Not available on free personal accounts. Requires Workspace Business Standard or higher. Not applicable.

**Cost:** All free under existing Google account. No new cost.

**Soren flag:** None. All accessed via web browser.

---

### Category 6: GitHub Version Control for Video

**META Pick: GitHub + Git LFS for project metadata; Google Drive or YouTube as primary binary storage**

**What it is:** Git LFS is a Git extension that replaces large binary files with lightweight pointer files in the repository while storing actual binaries on a remote server. GitHub provides 1 GB free LFS storage and 1 GB free LFS bandwidth per month on free accounts. Overage: $0.07/GB storage, $0.0875/GB bandwidth.

**The honest assessment:** Git LFS works for video in theory and strains in practice. 1 GB free storage fills fast — one 10-minute 1080p video can exceed that limit alone. The practical limit: use LFS for small clips (under 50 MB each), SRT files, scripts, and metadata — not for large source files.

**Recommended hybrid workflow for Vicky:**
1. Git repository tracks: project structure, scripts, SRT files, metadata, settings, small exported clips (<50MB)
2. `.gitattributes` LFS tracking for: `*.mp4`, `*.mov`, `*.mkv`, `*.wav` — small working files only
3. Large source files, final exports, and archives live in Google Drive or YouTube (unlisted)
4. README or index file in the repo links to Drive/YouTube for binary assets
5. Result: repo stays lean, version history intact for everything meaningful, large binaries accessible via link

**Alternative if scale grows — DVC:** DVC (Data Version Control) integrates with Git and supports backing storage on Google Drive, S3, or local disk — better performance than LFS for large binary management. If Vicky's video library grows significantly, DVC + Google Drive backend is the stronger long-term option.

**Cost:** Git LFS 1 GB free — zero cost within that limit. DVC is MIT open-source.

**Soren flag:** YES — Git LFS is a CLI extension (deployable). DVC is deployable if adopted.

---

## Adversarial Pass — AI Video Editing META Pick (FFmpeg)

**Named adversarial pass — conducted on FFmpeg as Vicky's core editing engine.**

**Challenge 1: Is FFmpeg actually appropriate for a non-coder agent?**
Partially sustained. FFmpeg's CLI is steep. Raw command syntax is complex and unforgiving. This is a real concern for Vicky if she operates without Pete's scripting support. The mitigation: HandBrake covers the GUI use case for compression, and a pre-built script library (Pete's domain) covers the automation use case. Vicky does not need to write FFmpeg commands from scratch — she needs to understand what they do. Verdict: appropriate with the right scaffolding. Not a blocker.

**Challenge 2: Is MoviePy a better primary tool for an agent-driven pipeline?**
No. MoviePy's performance gap is real and documented — 20+ seconds vs. milliseconds for equivalent operations. MoviePy is the right choice for scripting readability and compositing tasks; ffmpeg-python or direct subprocess calls are right when performance matters. The two-tool split is the correct architecture, not a compromise.

**Challenge 3: FFmpeg's licensing complexity (GPL/LGPL, codec patents).**
Real issue for commercial software distribution — not relevant here. The team is building internal tools. FFmpeg usage for internal video processing does not trigger GPL redistribution requirements. H.264/H.265 patent concerns apply to distribution of encoded content at commercial scale — not to a small agent pipeline producing videos for internal use or Discord. Not a blocker.

**Challenge 4: Is there a better all-in-one tool that handles editing AND AI generation?**
Not at zero cost. Adobe Premiere Pro (Firefly integrations) and DaVinci Resolve Studio have deeper AI integration but require paid subscriptions. The free DaVinci Resolve (not Studio) is worth noting — professional color grading, Magic Mask AI tracking, runs on Windows, free. Does not include AI video generation. For Vicky's use case, FFmpeg + HandBrake (editing) plus Google Vids (AI generation) covers the same ground at zero cost. DaVinci Resolve free tier is flagged to Sage as optional for future scope expansion.

**Adversarial pass verdict:** FFmpeg as core engine, HandBrake as GUI companion, MoviePy for scripting convenience — this holds. No better zero-cost option exists for Vicky's manipulation layer.

---

## Cost Summary

| Tool | Purpose | Cost | Access Path | Soren Flag |
|---|---|---|---|---|
| FFmpeg | Core video manipulation engine | Free (LGPL/GPL) | Download + install | YES |
| ffmpeg-python | Python wrapper for FFmpeg | Free (MIT) | pip install | YES |
| MoviePy v2.2.1 | Python scripting layer | Free (MIT) | pip install | YES |
| HandBrake v1.10.2 | GUI compression tool | Free (GPL) | Download + install | YES |
| OpenAI Whisper | Auto captioning / transcription | Free (MIT) | pip install | YES |
| faster-whisper | Faster Whisper variant | Free (MIT) | pip install | YES |
| auto-subtitle | CLI wrapper for Whisper + FFmpeg | Free (MIT) | pip install | YES |
| Google Vids / Veo 3.1 | AI video generation (10 clips/month) | Free — existing Google account | Web UI (vids.new) | No |
| Runway ML free plan | AI video generation (125 one-time credits, watermarked) | Free | Web UI — new signup required | No |
| Kling AI free tier | AI video generation (66 credits/day, low-res, watermarked) | Free | Web UI — new signup required | No |
| Google Drive | Large video file storage and sharing | Free (15 GB) | Web — existing account | No |
| YouTube (unlisted) | Finished video hosting and Discord sharing | Free | Web — existing account | No |
| Git LFS | Video file version control (small clips) | Free to 1 GB; $0.07/GB overage | CLI extension — install | YES |
| DVC | Advanced video asset versioning (optional) | Free (MIT) | pip / package install | YES (if adopted) |

**Total new monthly cost: $0.00**

---

## Soren Flags

All items below are deployable. Every item routes to Soren for security clearance before deployment.

**FLAG 1 — HIGH: FFmpeg**
- Source: https://ffmpeg.org/download.html (Windows builds: https://www.gyan.dev/ffmpeg/builds/)
- Type: Binary download + PATH configuration
- Notes: Complex GPL/LGPL license with codec-level variations (libx264, libx265, libfdk_aac trigger GPL). Soren should assess which build variant is appropriate. gyan.dev is the community-standard Windows build source — Soren verifies build integrity.

**FLAG 2 — MEDIUM: HandBrake v1.10.2**
- Source: https://handbrake.fr/downloads.php
- Type: Desktop application installer (Windows .exe)
- Notes: GPL license, 20+ year project. Low risk profile. Standard Soren clearance.

**FLAG 3 — MEDIUM: ffmpeg-python**
- Source: https://pypi.org/project/ffmpeg-python/ | GitHub: https://github.com/kkroening/ffmpeg-python
- Type: pip install (Python package)
- Notes: MIT license. Thin wrapper around FFmpeg. Clearance is linked to FFmpeg clearance — if FFmpeg clears, this clears.

**FLAG 4 — MEDIUM: MoviePy v2.2.1**
- Source: https://pypi.org/project/moviepy/ | GitHub: https://github.com/Zulko/moviepy
- Type: pip install (Python package)
- Notes: MIT license, active project. Depends on FFmpeg being installed. 77 open GitHub issues including a TextClip performance regression as of Feb 2026 — noted, not a blocker.

**FLAG 5 — HIGH: OpenAI Whisper**
- Source: https://github.com/openai/whisper | PyPI: `pip install openai-whisper`
- Type: pip install (Python package) + model download on first run
- Notes: MIT license. Runs entirely locally — no data sent to OpenAI servers. Model files download from OpenAI's CDN on first run (hundreds of MB depending on model size: tiny/base/small/medium/large). Soren should assess: (a) model download source integrity, (b) acceptable local model storage path.

**FLAG 6 — MEDIUM: faster-whisper**
- Source: https://github.com/SYSTRAN/faster-whisper | PyPI: `pip install faster-whisper`
- Type: pip install (Python package)
- Notes: MIT license. Uses CTranslate2 backend for 4–8x speed improvement over base Whisper. Same local-only behavior — no external data transmission. Soren to verify CTranslate2 dependency chain.

**FLAG 7 — LOW: auto-subtitle (CLI wrapper)**
- Source: https://github.com/m1guelpf/auto-subtitle
- Type: pip install (Python package)
- Notes: MIT license, lightweight CLI wrapper. Depends on Whisper and FFmpeg. Clearance follows those two.

**FLAG 8 — LOW: Git LFS**
- Source: https://git-lfs.com/
- Type: Binary install (Git extension)
- Notes: MIT license, GitHub-maintained. Low risk. Standard team tooling pattern.

**FLAG 9 — LOW (if adopted): DVC**
- Source: https://dvc.org/ | PyPI: `pip install dvc`
- Type: pip install (Python package)
- Notes: Apache 2.0 license. Only relevant if Vicky's video library outgrows Git LFS.

---

## Recommendation

Vicky's core toolkit is lean, fully functional, and costs nothing new.

**The manipulation layer** (trimming, cutting, splitting, compressing, captioning) is fully solved: FFmpeg for engine power, HandBrake for GUI compression, MoviePy for Python scripting with Pete, and Whisper for auto captions. This stack handles everything on Vicky's job description that involves working with existing video.

**The AI generation layer** is web-UI-only within the current subscription footprint. Google Vids (Veo 3.1 — 10 free clips/month) is the primary path — zero cost, best quality, no watermark concern, tied to the operator's existing Google account. Runway (125 one-time credits) and Kling (66 daily credits, lower quality) are supplementary. This is the honest ceiling for now. If AI video generation becomes a significant use case, a paid Runway subscription ($15–28/month) or Kling paid plan ($6.99–$36/month) is the right next step — not a workaround.

**The storage and version control layer** is hybrid by design: GitHub + LFS for scripts, SRT files, metadata, and small clips; Google Drive for large source files; YouTube unlisted for finished output and Discord sharing.

**What Vicky needs before she can build:** All Soren-flagged tools (FFmpeg, HandBrake, Whisper, faster-whisper, ffmpeg-python, MoviePy, Git LFS, auto-subtitle — 8 items, 9 flags total with optional DVC) must clear Soren's pipeline before deployment. AI generation web UIs require no Soren clearance.

**Optional addition for Sage's consideration:** DaVinci Resolve (free desktop version) — professional color grading, Magic Mask AI tracking, no subscription required. Not part of Vicky's initial kit but worth noting if her scope expands into professional post-production.

---

## C&P Summary

Vicky is the team's Videographer, handling video editing, AI generation, captioning, and Discord file management. Her core toolkit costs nothing new. For video manipulation — trimming, cutting, compressing, splitting, and burning captions — the stack is FFmpeg (the industry engine, free and open-source), HandBrake (GUI companion for compression, also free), MoviePy (Python scripting layer for Pete-built automations), and OpenAI Whisper (local auto-captioning from speech, no API key required, runs entirely offline). For AI video generation, Vicky uses web UIs only: Google Vids (Veo 3.1 model, 10 free clips per month, available on the operator's existing free Google account), Runway ML (125 one-time free credits, watermarked), and Kling AI (66 daily free credits, lower resolution). There is no AI video generation API accessible within current subscriptions — Claude API is the only confirmed programmatic LLM access. For storage, Google Drive (15 GB free) handles large video archives and Discord sharing via link, YouTube unlisted handles finished video hosting, and GitHub with Git LFS handles project metadata, scripts, subtitle files, and small clips. Every downloadable tool (FFmpeg, HandBrake, Whisper, MoviePy, Git LFS and variants) requires Soren clearance before deployment — nine flags total, none expected to block.

---

## Sources

- FFmpeg official: https://ffmpeg.org/ | GitHub: https://github.com/FFmpeg/FFmpeg
- ffmpeg-python PyPI: https://pypi.org/project/ffmpeg-python/
- MoviePy PyPI: https://pypi.org/project/moviepy/ | GitHub: https://github.com/Zulko/moviepy
- MoviePy performance issue: https://github.com/Zulko/moviepy/issues/2165
- HandBrake: https://handbrake.fr
- OpenAI Whisper GitHub: https://github.com/openai/whisper
- faster-whisper GitHub: https://github.com/SYSTRAN/faster-whisper
- auto-subtitle GitHub: https://github.com/m1guelpf/auto-subtitle
- Google Vids / Veo 3.1 free announcement: https://www.ghacks.net/2026/04/07/google-opens-veo-3-1-ai-video-generation-to-all-users-with-free-monthly-access/
- Runway ML pricing 2026: https://runwayml.com/pricing
- Kling AI free tier 2026: https://klingai.com
- GitHub LFS official: https://git-lfs.com/
- GitHub LFS billing docs: https://docs.github.com/billing/managing-billing-for-git-large-file-storage/about-billing-for-git-large-file-storage
- DVC: https://dvc.org/
- Discord file size limits 2026: https://fast.io/resources/discord-file-size-limit/
- LiteLLM report (LLM access context): report-litellm.md (this project, Session 105)

---

*Report by Rose | Session 105 | 2026-05-02*
