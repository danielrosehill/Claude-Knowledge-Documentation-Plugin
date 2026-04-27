---
name: capture-idea
description: Use when the user wants to turn a voice-note MP3 in the current repository into a transcribed idea/spec with CLAUDE.md and README, then push to GitHub. Triggers on phrases like "capture this idea", "transcribe my voice note", "turn this mp3 into a spec".
---

This repository contains a note file saved as an MP3 (name may vary).

Use the transcription MCP to send the transcription job to Gemini. Request both a verbatim transcript and a cleaned-up transcript.

After receiving the two files, generate a development specification (spec) based on the transcript content. Save the original MP3 and all generated files together in a folder called `Notes` or `Planning`.

Create a `CLAUDE.md` providing basic grounding in the context objectives. Create a short `README.md` summarizing the idea, noting this is a placeholder unless developing immediately.

The README should link to the planning note so anyone interested can pick it up. Link directly to the MP3 and transcripts using relative paths. Include the audio file in the repo.

Then push to GitHub.
