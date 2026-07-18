# InterScriber

Low-cost, privacy-first transcription for journalists. Drop in an interview recording, get back a clean, timestamped, speaker-labeled Markdown transcript — for pennies on the dollar compared to Otter.ai or Trint, or free if you run it entirely on your own machine.

## Why it matters

- **Time/cost saved:** 10 hours of interview audio costs $0.00 on local Whisper, or ~$0.40-1.11 via Groq Cloud, pay-per-use. Otter.ai Pro is $16.99/mo ($8.33/mo billed annually) with a 20-hour cap; Otter Business is $30/mo per user ($19.99/mo annually) with unlimited minutes; Trint Pro is $79/mo per seat, also unlimited — none of them charge only for what you use. If you transcribe regularly, this pays for itself the first week. (Full comparison table below.)
- **Who it's for:** any reporter who transcribes interviews and is tired of a subscription they don't fully use — no coding required to get the value, with the code open for anyone who wants to modify it.
- **Privacy:** local mode never sends audio anywhere. That matters for source protection and any interview involving sensitive or unpublished material — the recording is deleted from disk right after transcription, and only the transcript persists.

| Service | Cost for 10 hrs | Model |
|---|---|---|
| **InterScriber Local** | **$0.00** | On-device Whisper Small |
| **InterScriber + Groq Turbo** | **~$0.40** | Pay-per-use |
| **InterScriber + Groq** | **~$1.11** | Pay-per-use |
| Rev.ai | ~$1.80 | API, no subscription |
| OpenAI Whisper API | ~$3.60 | Pay-per-use |
| Otter.ai Pro | **$16.99/mo ($8.33/mo billed annually)** | Subscription, 20 hr/mo cap |
| Otter.ai Business | **$30/mo per user ($19.99/mo annually)** | Subscription, unlimited minutes |
| Trint Pro | **$79/mo per seat** | Subscription, unlimited (no pay-per-use tier listed) |

## Get it running without touching a terminal

If a terminal sounds like a foreign language, Claude Cowork can do the installing for you, on your own computer, step by step:

1. Make sure you're on a Claude Pro or Max plan, with the latest [Claude Desktop](https://claude.com/download) app installed.
2. Turn on Computer Use: **Settings > General > Computer use**.
3. Copy this repo's link: `https://github.com/emaduneme/reporters-ai-playbook-builds/tree/main/2026-08-20-interscriber`
4. Open a new [Cowork](https://claude.com/product/cowork) task and paste it in, with a request like: "Clone this repo to my computer, install what it needs, and run it so I can transcribe an interview. Ask for permission wherever you need it."
5. Claude will ask permission before opening apps like Terminal on your behalf. Approve those.
6. This capability is a research preview, so if it stalls partway through, ask it to try again or pick up where it left off.
7. When it's done, InterScriber should be running and open in your browser, ready for you to upload a recording.

Because Cowork is installing the actual code below, not writing its own version, it carries the same choice between local and cloud transcription as any other install — pick local Whisper in the app if source protection matters for that recording.

## Prefer to build your own version? Use Claude Code

You don't need this exact code to get the value — the pattern is what matters. If you'd rather build your own version (different transcription engine, different output format, integrated into your own newsroom's tools), open Claude Code in an empty folder and work through the three prompts in [`prompts/build-from-scratch.md`](prompts/build-from-scratch.md), in order. Claude Code will ask clarifying questions as it goes — that's normal, answer them the way you'd brief a colleague on what you actually need.

## Or install the exact code yourself

For readers who want full control and are comfortable with a terminal: this is the same code either of the paths above would end up building.

**Prerequisites:** Python 3.11+ and ffmpeg (`brew install ffmpeg` on macOS, `sudo apt install ffmpeg` on Linux, or download from ffmpeg.org on Windows).

```bash
# macOS / Linux
./run.sh

# Windows
run.bat
```

The launcher sets up a virtual environment, installs dependencies, and opens the web UI. Full walkthrough in [`workflows/transcribe.md`](workflows/transcribe.md).

To enable Groq Cloud (optional, for near-instant transcription): rename `.env.example` to `.env` and paste in a [Groq API key](https://console.groq.com/keys).

## Files

- `app.py` — the Streamlit web UI, the actual entry point
- `run.sh` / `run.bat` — one-click launchers (env setup + dependency install + app launch)
- `tools/transcribe_whisper.py` — local, free transcription engine
- `tools/transcribe_groq.py` — Groq Cloud transcription engine
- `tools/pack_transcripts.py` — groups word-level JSON into readable, timestamped Markdown
- `workflows/transcribe.md` — the SOP, if you're running this by hand or adapting the pieces
- `prompts/build-from-scratch.md` — the copy-paste prompts for building your own version with Claude Code

## Source

Built by Emmanuel Maduneme with Claude Code and Gemini CLI. This packaged version lives at [reporters-ai-playbook-builds/2026-08-20-interscriber](https://github.com/emaduneme/reporters-ai-playbook-builds/tree/main/2026-08-20-interscriber); the original project, issue tracker, and ongoing updates are at [github.com/emaduneme/interscriber](https://github.com/emaduneme/interscriber).
