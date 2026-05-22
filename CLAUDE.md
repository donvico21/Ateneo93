# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Static single-page website for the **ADNU High School Batch '93** alumni community. There is no build system or package manager — `index.html` is the entire site and can be opened directly in a browser.

This workspace is also configured to use GoDaddy's internal GoCode API (an Anthropic API proxy).

## Launching Claude Code

Use the provided startup script to launch Claude Code with the correct GoCode API environment:

```powershell
./start-gocode.ps1
```

This sets the GoCode API token, points `ANTHROPIC_BASE_URL` to the internal GoCode production endpoint (`caas-gocode-prod.caas-prod.prod.onkatana.net`), and launches `claude`.

## API Configuration

| Variable | Purpose |
|---|---|
| `GOCODE_API_TOKEN` | Authentication token for the GoCode proxy |
| `ANTHROPIC_BASE_URL` | GoCode production endpoint (instead of `api.anthropic.com`) |
| `ANTHROPIC_MODEL` | Pinned to `claude-sonnet-4-6` |
| `CLAUDE_CODE_DISABLE_EXPERIMENTAL_BETAS` | Set to `1` — beta features are disabled |

If the GoCode token needs to be rotated, update the `$env:GOCODE_API_TOKEN` value in `start-gocode.ps1`.

## Site Architecture

Everything lives in `index.html` — all CSS (inline `<style>`), HTML sections, and JavaScript (inline `<script>`).

**Navigation model:** The site is a fixed-position SPA. All `<section>` elements are `position: fixed; opacity: 0; pointer-events: none` by default. The active section gets `.active` (opacity 1, pointer-events auto). The `showSection(hash)` function drives all transitions by toggling this class. There is no routing library.

**Sections:** `#home` (hero), `#about`, `#events`, `#officers`, `#gallery`, `#connect` (includes the `<footer>`).

**Design tokens** — CSS custom properties on `:root`:
- Colors: `--navy #0d1b3e`, `--blue #1a3a8f`, `--gold #c9961a`, `--gold-light #f0b429`, `--black #080c14`, `--white #f5f5f0`, `--gray #9aa3b2`
- Fonts: `Cinzel` (headings/display), `Lato` (body)

## Content That Needs Customization

| What | Where in `index.html` |
|---|---|
| Current officers (President, VP, etc.) | `.officers-grid` `.officer-name` elements (~line 997) |
| Previous officer terms and names | `.prev-terms` `.prev-term` blocks (~line 1030) |
| Event dates and details | `.event-card` blocks in `#events` (~line 960) |
| Batch section names in contact form | `<select id="section">` `<option>` values (~line 1152) |
| Social/community links | `.social-link` `href="#"` values in `#connect` (~line 1172) |
| Gallery photos | Replace `<div class="gallery-placeholder">` with `<img>` tags in `.gallery-grid` |

## Deployment

Hosted on GitHub Pages. Push to `main`, then set Pages source to **Deploy from branch → main → / (root)**.
