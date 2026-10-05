# Changelog

OLIVE was developed as DMDO before 1.0. There are no earlier public releases.

## OLIVE 1.0 — 1.0.0

### Added

- Desktop app for Linux x86_64 (AppImage) and, as a preview, Windows x86_64 (per-user installer).
- First-run setup with three steps of trust: every component is pinned by source, size and
  SHA-256 (or Ollama registry digest), engineering-reviewed and approved for the release before
  setup offers it. Downloads are HTTPS-only, resumable and verified; archives are unpacked with
  path and size checks; existing runtimes and models are reused, never replaced.
- Chat modes FAST (qwen3:8b) and NORMAL (gpt-oss:20b) through Ollama.
- NOW: live web research with sources (qwen3.5:9b).
- DEEP: answers from your documents with page citations, with semantic search when the
  qwen3-embedding:0.6b model is installed and keyword search otherwise.
- Agent Workspace: coding tasks with diffs, test runs and receipts.
- OLIVE Notes and OLIVE Draw: local-first notes and drawings, with image import.
- REIMAGINE on Linux with NVIDIA: FLUX.2 [klein] 4B image generation and editing on a reproducible
  ComfyUI 0.35.0 runtime archive. NVIDIA's CUDA packages are downloaded from PyPI, not bundled.
- OLIVE Connect: device pairing with mutual confirmation, pinned TLS 1.3 and per-device permissions.
- Connect World: a relay you host lets paired devices reach each other from any network, with
  automatic Direct ↔ World failover. The relay cannot read your content.
- Mail (IMAP/SMTP or Gmail) and Personal (calendar, tasks, reminders).

### Improved

- An image engine OLIVE started stops after it has been idle, freeing several GB of memory.
- Document search records which embedding model made each vector and re-embeds when it changes.
- The packaged app finds existing Ollama, ComfyUI and model folders by itself.

### Reliability

- Linux: OLIVE refuses to start without the Chromium sandbox and explains how to enable it.
- Connect: failover no longer waits on a network path that vanished silently.
- Connect: database reads tolerate concurrent writes on Windows.
- Remote requests keep room for the prompt inside small context windows.

### Platform support

| Platform | 1.0 |
| --- | --- |
| Linux x86_64 | Supported; tested on CachyOS with KDE Plasma and an NVIDIA GPU |
| Windows x86_64 | Preview; unsigned; tested by hand on a Windows PC before release and launch-tested in release CI |
| macOS | Not included |
| iPhone | Not included |

### Known limitations

- Not included: MAX, UNCENSORED, VIDEO, image-to-video, a bundled AUDIO engine.
- Windows has no Creator engine and needs Ollama installed separately.
- No automatic updates.
