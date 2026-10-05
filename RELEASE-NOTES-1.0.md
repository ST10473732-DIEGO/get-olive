# OLIVE 1.0

The first public release of OLIVE, a private AI assistant that runs on your own computer.

## Highlights

- **Local AI chat.** FAST (qwen3:8b) and NORMAL (gpt-oss:20b) run on your computer through Ollama.
- **Answers with sources.** NOW searches the web and cites what it read. DEEP answers from your
  documents with page citations and never sends them to the web.
- **Agent Workspace.** Coding tasks with diffs, test runs and receipts you can review.
- **Notes and Draw.** Local-first notes and drawings.
- **REIMAGINE** (Linux, NVIDIA). Image generation and editing with FLUX.2 [klein] 4B.
- **Guided setup.** Choose a package; OLIVE downloads only pinned components, checks every file's
  size and SHA-256, and reuses what you already have.

## Downloads

| Platform | File | Status |
| --- | --- | --- |
| Linux x86_64 | `OLIVE-1.0.0-linux-x86_64.AppImage` | Supported |
| Windows x86_64 | `OLIVE-Setup-1.0.0-windows-x86_64.exe` | Preview, unsigned |
| Linux x86_64 | `creator-image-comfyui-0.35.0-linux-x86_64.tar.zst` | Creator image runtime, in its own [release](https://github.com/ST10473732-DIEGO/get-olive/releases/tag/creator-runtime-1.0.0-ecdb6702); setup downloads it for you |

Verify with `SHA256SUMS.txt`. Installation: [INSTALL.md](https://github.com/ST10473732-DIEGO/get-olive/blob/main/INSTALL.md).

## Creator

REIMAGINE needs Linux x86_64 and an NVIDIA GPU. The OLIVE Creator package installs a ComfyUI 0.35.0
image runtime (1.1 GB archive, published at
[creator-runtime-1.0.0-ecdb6702](https://github.com/ST10473732-DIEGO/get-olive/releases/tag/creator-runtime-1.0.0-ecdb6702)),
20 NVIDIA CUDA and related packages straight from PyPI (2.5 GB), and the FLUX.2 [klein] 4B model
from Hugging Face (12.5 GB). Windows has no Creator engine in 1.0.

## Privacy

No account, no hosted AI, no telemetry. OLIVE goes online for setup downloads, for NOW's web
searches, and for features you configure yourself (Mail, Connect World).

## Known limitations

- Windows is a preview: unsigned (SmartScreen warns), no Creator engine, and Ollama must be
  installed separately. It was tested by hand on a Windows PC before release and is launch-tested
  in release CI.
- Linux is tested on CachyOS with KDE Plasma; other distributions are not yet verified. Ubuntu
  24.04+ needs an AppArmor profile for the sandbox ([INSTALL.md](https://github.com/ST10473732-DIEGO/get-olive/blob/main/INSTALL.md#linux-sandbox)).
- Not included: macOS, the iPhone app, MAX, UNCENSORED, VIDEO, a bundled AUDIO engine.
- Connect World needs a relay you host; the relay package is not part of this release.
- No automatic updates.
