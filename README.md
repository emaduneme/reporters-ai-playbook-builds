# Reporter's AI Playbook — Builds

Working tools for journalists, published alongside The Reporter's AI Playbook newsletter. Every "Build" issue ships one of these: a small, real, install-it-tonight tool, not just a prompt to copy.

Each folder is self-contained and follows the same shape:

```
<build-name>/
├── README.md       # what it does, why it matters, how to install it, how to recreate it with Claude Code or Claude Cowork
├── workflows/      # the SOP — follow it in order, or adapt it
└── tools/          # the scripts the SOP calls
```

That `workflows/` + `tools/` split isn't incidental — it's the same pattern (Workflows / Agents / Tools) the newsletter itself runs on to research, draft, fact-check, and ship each issue. Nothing here is a toy demo of that system; it's the actual system, repackaged so you can run it.

## Builds

- [`2026-08-20-interscriber/`](2026-08-20-interscriber/) — free, privacy-first interview transcription. Local Whisper (free, on-device) or Groq Cloud (near-instant, pennies per hour). An alternative to paying for Otter.ai or Trint.

## Using these

Each build's own README has full install steps. If you'd rather not run someone else's code, every README also includes plain-language prompts for recreating the tool yourself with Claude Code (or Claude Cowork, if you don't want to touch a terminal at all).

## About

Built by [Emmanuel Maduneme](https://github.com/emaduneme) — journalism professor, former broadcast journalist, and the person writing the newsletter these come from. Questions, requests, or a tool you wish existed: open an issue here, or reply to any newsletter issue.
