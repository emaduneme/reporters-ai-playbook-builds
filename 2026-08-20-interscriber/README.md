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

Claude Cowork is the easiest entry point if you've never touched a terminal and don't want to start now — it's a paid-plan feature (Pro/Max/Team/Enterprise) in the Claude desktop app, web, or mobile that reads and writes your local files without you running any commands yourself. Worth knowing before you try it: Cowork executes code in an isolated environment on Anthropic's servers, not literally on your laptop, so it can't just "run our Streamlit app" the way Claude Code can — instead, describe the outcome and let it build its own path there. A prompt to paste into a Cowork task:

> "I have an interview recording at [file path]. Transcribe it into a timestamped, speaker-labeled Markdown transcript I can quote from. Use the Groq API for transcription (I'll give you a key from console.groq.com/keys) — group the words into phrase-level lines, breaking whenever there's a silence of half a second or more or the speaker changes. Give me back a finished Markdown file."

Two honest tradeoffs versus the local route: Cowork's transcription happens via a cloud API call (Groq), not fully on-device, so it doesn't carry the same "audio never leaves your machine" privacy guarantee as InterScriber's local Whisper mode — and it requires a paid Claude plan. If source protection is the priority, use one of the local options below instead.

## Prefer to build your own version? Use Claude Code

You don't need this exact code to get the value — the pattern is what matters. If you'd rather build your own version (different transcription engine, different output format, integrated into your own newsroom's tools), open Claude Code in an empty folder and try:

1. "Build a local tool that transcribes an audio file with OpenAI Whisper, outputs word-level timestamps as JSON, then groups the words into phrase-level lines broken on silence or speaker change."
2. "Wrap that in a Streamlit web UI: file upload, an engine choice (local vs. a cloud API), a progress bar, and a download button for the final transcript."
3. "Add a second engine option using the Groq API (`whisper-large-v3`) for near-instant cloud transcription, and let me switch between them."

Claude Code will ask clarifying questions as it goes — that's normal, answer them the way you'd brief a colleague on what you actually need.

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

## Source

Built by Emmanuel Maduneme with Claude Code and Gemini CLI. This packaged version lives at [reporters-ai-playbook-builds/2026-08-20-interscriber](https://github.com/emaduneme/reporters-ai-playbook-builds/tree/main/2026-08-20-interscriber); the original project, issue tracker, and ongoing updates are at [github.com/emaduneme/interscriber](https://github.com/emaduneme/interscriber).
