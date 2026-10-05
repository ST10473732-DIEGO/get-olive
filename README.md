# OLIVE 1.0

OLIVE is a private AI assistant that runs on your own computer. Chat, research, documents,
coding tasks, notes, drawings and image generation run locally, with [Ollama](https://ollama.com)
as the model engine. There is no OLIVE account, no hosted AI and no telemetry.

## Download

| Platform | Architecture | Download | Status |
| --- | --- | --- | --- |
| Linux | x86_64 | [OLIVE-1.0.0-linux-x86_64.AppImage](https://github.com/ST10473732-DIEGO/get-olive/releases/download/olive-1.0/OLIVE-1.0.0-linux-x86_64.AppImage) | **Supported.** Tested on CachyOS (KDE Plasma) with an NVIDIA GPU |
| Windows | x86_64 | [OLIVE-Setup-1.0.0-windows-x86_64.exe](https://github.com/ST10473732-DIEGO/get-olive/releases/download/olive-1.0/OLIVE-Setup-1.0.0-windows-x86_64.exe) | **Preview.** Unsigned. Tested by hand on a Windows PC before release and launch-tested in release CI |
| macOS | — | Not available | Not included in OLIVE 1.0 |
| iPhone | — | Not available | Not included in OLIVE 1.0 |

Checksums: [SHA256SUMS.txt](https://github.com/ST10473732-DIEGO/get-olive/releases/download/olive-1.0/SHA256SUMS.txt) ·
Licences: [THIRD_PARTY_NOTICES.txt](https://github.com/ST10473732-DIEGO/get-olive/releases/download/olive-1.0/THIRD_PARTY_NOTICES.txt) ·
All files: [OLIVE 1.0 release](https://github.com/ST10473732-DIEGO/get-olive/releases/tag/olive-1.0)

You only need the installer for your platform. OLIVE downloads models and engines during setup.

## System requirements

| | |
| --- | --- |
| Operating system | Linux x86_64 (glibc), or Windows 10/11 x64 (preview) |
| Disk | About 30 GB free for OLIVE Core, about 50 GB for OLIVE Creator (Linux) |
| Internet | Needed during setup to download models and engines |
| Graphics | An NVIDIA GPU is recommended. REIMAGINE needs one |

OLIVE has been measured on one configuration: an RTX 3080 Ti Laptop GPU (16 GB VRAM) with 64 GB RAM.
The setup's system check reports **Verified** only on Linux with an NVIDIA GPU, and **Not yet
verified** elsewhere. Less memory may work, but has not been measured.

## Install on Linux

```sh
chmod +x OLIVE-1.0.0-linux-x86_64.AppImage
./OLIVE-1.0.0-linux-x86_64.AppImage
```

- If nothing happens and the terminal mentions FUSE, install your distribution's `libfuse2` (or `fuse2`)
  package, or run `APPIMAGE_EXTRACT_AND_RUN=1 ./OLIVE-1.0.0-linux-x86_64.AppImage`.
- OLIVE requires the Chromium sandbox and will not start without it. If you see **"OLIVE could not
  start safely"**, see [Linux sandbox](INSTALL.md#linux-sandbox). Ubuntu 24.04 and later need one
  extra step.

More detail, including desktop menu integration: [INSTALL.md](INSTALL.md#linux).

## Install on Windows (preview)

1. Download `OLIVE-Setup-1.0.0-windows-x86_64.exe` and [check its SHA-256](#verify-downloads).
2. Run it. The installer is not code-signed, so Windows SmartScreen shows **"Windows protected your PC"**.
   If the checksum matches, choose **More info → Run anyway**.
3. OLIVE installs for your user only (no administrator rights) into `%LOCALAPPDATA%\Programs\OLIVE`
   and opens setup.
4. Install [Ollama for Windows](https://ollama.com/download) yourself. OLIVE 1.0's setup does not
   download Ollama on Windows, but it finds an installed Ollama and then downloads OLIVE's models.

## First launch

A new profile opens setup: your name, a system check, then a package.

| Package | What it adds | Download (approx.) |
| --- | --- | --- |
| **OLIVE Core** | Ollama (Linux) and four local models: FAST, NORMAL, NOW and document search | 28 GB |
| **OLIVE Creator** | Core plus REIMAGINE: an image engine and the FLUX.2 [klein] 4B image model (Linux with NVIDIA) | +16 GB |

Setup lists every file before it downloads, checks each one's size and SHA-256 (or Ollama
registry digest), and reuses Ollama and models you already have. You can choose **Set up later**
and open setup again from Settings.

## What you can do

| Mode | What it does | Needs |
| --- | --- | --- |
| FAST | Quick local chat (qwen3:8b) | Core |
| NORMAL | Reasoning and longer answers (gpt-oss:20b) | Core |
| NOW | Live web answers with sources (qwen3.5:9b) | Core, internet |
| DEEP | Answers from your documents, with page citations | Core |
| Agent Workspace | Coding tasks with diffs, test runs and receipts | Core |
| Notes and Draw | Local notes and drawings | — |
| REIMAGINE | Image generation and editing (FLUX.2 [klein] 4B) | Creator, Linux, NVIDIA |

Not in OLIVE 1.0: MAX, UNCENSORED, VIDEO and image-to-video, a bundled AUDIO engine, the macOS app and the
iPhone app.
These appear in the app as **Not available in this build** or **Needs setup**.

## Creator and image generation

REIMAGINE is available on **Linux x86_64 with an NVIDIA GPU** only. Choosing OLIVE Creator in
setup downloads:

- the OLIVE Creator image runtime (ComfyUI 0.35.0 with PyTorch, 1.1 GB, from this repository's
  [Creator runtime release](https://github.com/ST10473732-DIEGO/get-olive/releases/tag/creator-runtime-1.0.0-ecdb6702));
- 20 NVIDIA CUDA and related Python packages (2.5 GB) directly from PyPI, each checked against a
  pinned SHA-256;
- the FLUX.2 [klein] 4B model files (12.5 GB) from Hugging Face.

Installed, the image engine takes about 7 GB and the model about 12.5 GB. On the tested GPU a
1024×1024 image takes about 7 seconds. Windows has no Creator engine in OLIVE 1.0.

## Privacy

Your chats, documents, notes, drawings and images stay on your computer. OLIVE has no account
and sends no telemetry. OLIVE uses the network only for:

- **Setup:** downloads from github.com, the Ollama registry, Hugging Face and PyPI;
- **NOW:** short search queries to public web search services, then the pages it reads;
- **features you set up yourself:** Mail (your IMAP/SMTP or Gmail account), OLIVE Connect and a
  Connect World relay you host.

DEEP never sends your documents to the web.

## Data and models

| | Linux | Windows |
| --- | --- | --- |
| Application | The AppImage file, wherever you keep it | `%LOCALAPPDATA%\Programs\OLIVE` |
| Profile (chats, notes, settings) | `~/.local/share/olive` (or an existing `~/.olive` / `~/.dmdo`) | `%USERPROFILE%\.olive` |
| Runtimes and Creator models | `~/.local/share/olive` | `%LOCALAPPDATA%\OLIVE` |
| Ollama models | `~/.ollama/models` | Ollama's own folder |

OLIVE never writes inside the AppImage or the installed program folder.

## Updating

OLIVE does not update itself. To update, download the new version from this page and install
it over the old one (Windows) or replace the AppImage (Linux). Your profile, runtimes and models
are kept.

## Uninstalling

- **Windows:** Settings → Apps → Installed apps → OLIVE → Uninstall.
- **Linux:** delete the AppImage (and its menu entry, if you added one).

Uninstalling removes the application only. Your profile, runtimes and models stay where they are
(see [Data and models](#data-and-models)). Delete those folders only if you want to remove your
OLIVE data permanently.

## Troubleshooting

| Problem | What to do |
| --- | --- |
| A mode shows **Needs setup** | Open Settings → Open setup and install the package that mode needs |
| A download stops | Choose **Retry** in setup. Downloads resume where they stopped |
| Setup says a model changed upstream | The published model no longer matches OLIVE's pinned digest. Setup refuses it; wait for an OLIVE update |
| Linux: "OLIVE could not start safely" | Enable the Chromium sandbox: [INSTALL.md](INSTALL.md#linux-sandbox) |
| Linux: the AppImage does not start | `chmod +x` the file; install `libfuse2` or use `APPIMAGE_EXTRACT_AND_RUN=1` |
| Windows: SmartScreen warning | Expected for this unsigned preview. Verify the checksum, then **More info → Run anyway** |
| Windows: no AI answers | Install Ollama from ollama.com, then reopen setup |
| REIMAGINE unavailable | Needs Linux, an NVIDIA GPU with a current driver, and the OLIVE Creator package |

## Verify downloads

Compare the file's SHA-256 with [SHA256SUMS.txt](https://github.com/ST10473732-DIEGO/get-olive/releases/download/olive-1.0/SHA256SUMS.txt).

Linux:

```sh
sha256sum -c SHA256SUMS.txt --ignore-missing
```

Windows PowerShell:

```powershell
Get-FileHash .\OLIVE-Setup-1.0.0-windows-x86_64.exe -Algorithm SHA256
```

## What's in OLIVE 1.0

- A desktop app for Linux, with a Windows preview.
- Guided first-run setup that downloads only pinned, checksum-verified components.
- Local chat modes FAST and NORMAL, live web answers (NOW) and document answers with citations (DEEP).
- Agent Workspace for coding tasks with diffs and receipts.
- Local-first Notes and Draw.
- REIMAGINE image generation on Linux with NVIDIA.

## Known limitations

- **Windows** is a preview: unsigned (SmartScreen warns), no Creator engine, and Ollama must be
  installed separately. It was tested by hand on one Windows PC before release and is
  launch-tested in release CI.
- **Linux** has been tested on CachyOS with KDE Plasma. Other distributions should work but are not
  yet verified. Desktop navigation and control need KDE Plasma.
- **macOS** and the **iPhone** app are not part of OLIVE 1.0.
- **Connect World** needs a relay you host yourself; the relay package is not part of these downloads.
- MAX, UNCENSORED, VIDEO and AUDIO are not included.
- No automatic updates.

## Release history

| Date | Milestone |
| --- | --- |
| Before Sept 2026 | Development as DMDO (versions 2.x to 3.5): dependable chat state, bounded actions, research with evidence, a single-window desktop |
| Sept 2026 | Renamed OLIVE. Electron desktop, Studio and coding workspaces, the Design System V2 |
| 19–27 Sept 2026 | OLIVE Connect: pairing, pinned TLS between devices, sync and file transfer |
| 28–30 Sept 2026 | Chat modes, NOW research, REIMAGINE in Chat, Agent Workspace, Notes and Draw |
| 1–2 Oct 2026 | Connect World relay with automatic failover |
| 2–5 Oct 2026 | OLIVE 1.0 release engineering: packaged backend, first-run setup, pinned downloads, Creator image runtime, release builds |

Details: [CHANGELOG.md](CHANGELOG.md) · [Release notes](RELEASE-NOTES-1.0.md)

## Version

OLIVE 1.0 — version 1.0.0

## Source availability

This repository hosts OLIVE's release downloads and documentation. The OLIVE application source
is not published here. OLIVE is proprietary software; the third-party components it uses keep
their own licences ([THIRD_PARTY_NOTICES.txt](https://github.com/ST10473732-DIEGO/get-olive/releases/download/olive-1.0/THIRD_PARTY_NOTICES.txt)).
