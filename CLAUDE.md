# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a Claude Code workspace for DC Ops SG website testing work, configured to use GoDaddy's internal GoCode API (an Anthropic API proxy).

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
