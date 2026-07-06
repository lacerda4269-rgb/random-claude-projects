# Resource Report: BARKOD Studio — Artistic Barcode Generator

**URL:** https://barkod.studio/
**Date Researched:** 2026-04-18
**Researched by:** Rose | Security pre-check: Soren (pending) | Report by: Rose
**Already in Master Library?** No — Rose Research Round 2 (Session 60)

---

## What It Is
A web-based tool that transforms standard product barcodes into visually stylized SVG artwork — scannable barcodes that look like something other than a barcode.

## What It Does
- Accepts standard barcode numbers in EAN-13, EAN-8, or Code 128 formats
- Applies artistic style templates (Palm, Car, Pizza, Wizard hat, and others) to generate decorative barcode SVGs
- Output remains scannable — artistic styling is applied above a protected scan zone at the bottom
- Users can customize colors and download SVG files or copy the code directly
- Does not sell or register barcode numbers (GTINs) — only generates graphics for numbers the user provides
- Web app — no installation required; browser-based
- No GitHub repo identified; standalone web tool

## Relevance to This Project
None to current project workflows. This is a creative/novelty tool for turning product barcodes into art. Pre-routed to Section 9 (Jay's Shelf) per submission instructions, which is exactly the right call — it is the kind of interesting, weird thing worth knowing about, completely outside our current build.

## Master Library Assessment
- **Proposed Section:** 9 — Jay's Shelf (WTF Shelf)
- **Proposed Tier:** N/A (Shelf items are not tiered)
- **Rationale:** Pre-routed per submission instructions. Confirmed appropriate — this has zero operational relevance to the current project and is exactly the kind of creative discovery that lives on the shelf.

## Soren Security Pre-check
- **Verdict:** CLEARED
- **Date reviewed:** 2026-04-18
- **Re-reviewed:** 2026-06-08 — verdict confirmed. Site remains live; same minimal interaction surface (barcode number in, SVG out); no installation, no credentials, no data risk. No change to clearance.
- **Checked:** Deployment surface, data transmission profile, credential exposure, integration risk, project relevance.
- **Notes:** Web application only — no installation, no executable code, no dependencies to manage, no credentials required. The interaction model is minimal: a barcode number goes in, an SVG comes out. No account creation, no API keys, no sensitive data on our side.
  The only data transmitted to barkod.studio's server is the barcode number entered by the user — a public product identifier by definition. SVG output is downloaded or copied client-side. No data privacy concern for this project.
  Zero integration with any project workflow. This is a web tool accessed through a browser, nothing more. No deployment-time scan required. Cleared for filing on Jay's Shelf.

## Recommendation
File on Jay's Shelf. It is exactly what the shelf is for.

---
*Report by Rose | Session 60 | 2026-04-18*
*Freshness sweep: Rose | Session 229 | 2026-06-08 — site confirmed live at barkod.studio; style library still active (Palm, Car, POOP, Horse, GHOST, Silhouette, Burger, Paw, Angry Shark, Guitar, Cocktail, House, Star, Love, Bottle, Coffee Cup, Wizard Hat, Whale, Dude, Dog, Cat, Banana, and others). No GitHub repo identified — no version or commit metrics applicable. No change to assessment.*

---

## C&P Summary
BARKOD is a website that lets you turn a product barcode number into decorative art. You type in a standard barcode number (like the kind on a cereal box), pick a style theme (Palm tree, Pizza, Wizard hat, and others), and it generates a stylized SVG barcode that still actually scans. The scan zone at the bottom is kept clean for readability; the artistic styling is applied above it. You can download the SVG or copy the code. It does not sell barcode numbers — it only draws them. For this project, there is no operational relevance. It landed on the WTF Shelf for exactly the right reason: it is the kind of genuinely interesting, weird, creative tool that deserves acknowledgment even when it has nothing to do with what we are building.

---

## Report Version Log

| Version | Date | What Changed |
|---------|------|--------------|

