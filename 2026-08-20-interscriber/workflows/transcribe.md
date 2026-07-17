# Workflow: Transcribe an interview

**Objective:** Turn a recorded interview (audio or video) into a timestamped, speaker-labeled Markdown transcript you can quote from directly.

**Required inputs:**
- The recording file (`.mp4`, `.mov`, `.wav`, `.m4a`, `.mp3`)
- `ffmpeg` installed (`brew install ffmpeg` on macOS)
- Python 3.11+
- Optional: a [Groq API key](https://console.groq.com/keys) if you want cloud speed instead of local/free

**Steps:**
1. Run `./run.sh` (macOS/Linux) or `run.bat` (Windows). First run creates a virtual environment and installs dependencies — that's the slow part, only happens once.
2. In the browser tab that opens, upload your recording.
3. Pick an engine: local Whisper (free, private, runs on your machine) or Groq Cloud (near-instant, ~$0.11/hr as shipped — `tools/transcribe_groq.py` calls Whisper Large-V3; switching the model string to `whisper-large-v3-turbo` drops that to ~$0.04/hr at a slight accuracy tradeoff, untested in this build. Either way, audio is sent to Groq's servers).
4. Click **Start Transcription** and wait. A 1-hour interview takes roughly 15-60 minutes locally, or under a minute on Groq.
5. Download the Markdown transcript, or copy it straight into your notes.

**What's happening under the hood** (if you're adapting this, not just running it): `tools/transcribe_whisper.py` or `tools/transcribe_groq.py` extracts audio via `ffmpeg`, transcribes it word-by-word, and writes a word-level JSON. `tools/pack_transcripts.py` then groups those words into phrase-level lines — breaking on any silence ≥0.5s or a speaker change — and writes the final `takes_packed.md`.

**Expected output:** a Markdown file with lines like `[02:14] Speaker said this exact quote`, ready to paste into a story file.

**Edge cases / things learned:**
- Groq's file-size limit is 25MB, so `transcribe_groq.py` extracts audio as low-bitrate mp3 rather than wav — don't "fix" this back to wav for long interviews, it'll fail on anything over ~40 minutes.
- The raw audio file is deleted after transcription; only the JSON transcript persists. If you need the original recording kept, copy it elsewhere first — this tool doesn't.
