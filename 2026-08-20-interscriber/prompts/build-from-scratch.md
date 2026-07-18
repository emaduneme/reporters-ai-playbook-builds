# Build your own transcription tool with Claude Code

Copy these three prompts into Claude Code, in order, in an empty folder. You don't need to know how to code — answer its follow-up questions the way you'd brief a colleague on what you actually need, not the way you'd write a spec document.

**Prompt 1:**
```
Build a local tool that transcribes an audio file with OpenAI Whisper, outputs word-level timestamps as JSON, then groups the words into phrase-level lines broken on silence or speaker change.
```

**Prompt 2:**
```
Wrap that in a Streamlit web UI: file upload, an engine choice between local and a cloud API, a progress bar, and a download button for the final transcript.
```

**Prompt 3:**
```
Add a second engine option using the Groq API for near-instant cloud transcription, and let me switch between them.
```

That's the same pattern InterScriber itself is built from — the code in [`../tools/`](../tools/) is one working implementation of it, not the only one. Change the engine, the output format, or the UI to fit your own newsroom's tools.
