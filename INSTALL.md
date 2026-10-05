# Installing OLIVE 1.0

- [Linux](#linux)
- [Windows (preview)](#windows-preview)
- [macOS and iPhone](#macos-and-iphone)
- [After installing](#after-installing)

Before you install, check the download against
[SHA256SUMS.txt](https://github.com/ST10473732-DIEGO/get-olive/releases/download/olive-1.0/SHA256SUMS.txt)
([how](README.md#verify-downloads)).

## Linux

OLIVE for Linux is one AppImage for x86_64. It needs no Python, Node or other tools.

```sh
chmod +x OLIVE-1.0.0-linux-x86_64.AppImage
./OLIVE-1.0.0-linux-x86_64.AppImage
```

### FUSE

The AppImage mounts itself with `libfuse.so.2`. Distributions that ship only FUSE 3 need their
`libfuse2` (Debian, Ubuntu) or `fuse2` (Arch, Fedora) package. Without it, run:

```sh
APPIMAGE_EXTRACT_AND_RUN=1 ./OLIVE-1.0.0-linux-x86_64.AppImage
```

### Linux sandbox

OLIVE isolates web content with Chromium's sandbox, which needs **unprivileged user namespaces**.
When they are unavailable, OLIVE shows **"OLIVE could not start safely"** and exits. It never
runs without the sandbox.

**Ubuntu 24.04 and later** allow user namespaces only to programs with an AppArmor profile. An
AppImage mounts at a new path on each start, so give OLIVE a fixed folder first:

```sh
./OLIVE-1.0.0-linux-x86_64.AppImage --appimage-extract      # creates ./squashfs-root
mkdir -p ~/Applications && mv squashfs-root ~/Applications/OLIVE
```

Create `/etc/apparmor.d/olive`, replacing `YOU` with your user name:

```
abi <abi/4.0>,
include <tunables/global>

profile olive /home/YOU/Applications/OLIVE/olive flags=(unconfined) {
  userns,

  include if exists <local/olive>
}
```

Load it, then start OLIVE from that folder:

```sh
sudo apparmor_parser -r /etc/apparmor.d/olive
~/Applications/OLIVE/olive
```

This allows user namespaces for that one program only. These steps have not yet been tested on a
clean Ubuntu machine.

**Other distributions:** user namespaces must be enabled (`sysctl user.max_user_namespaces` must be
greater than 0; older Debian kernels also need `kernel.unprivileged_userns_clone=1`). Hardened
kernels may turn them off on purpose; follow your distribution's documentation.

### Menu entry

The AppImage contains `olive.desktop` (name OLIVE, icon `olive`). AppImage integration tools such
as AppImageLauncher or Gear Lever add it to your application menu.

### Where OLIVE writes on Linux

| | Location |
| --- | --- |
| Profile | An existing `~/.dmdo` or `~/.olive`, otherwise `~/.local/share/olive` |
| Runtimes | `~/.local/share/olive/runtime` |
| Creator models | `~/.local/share/olive/models` |
| Ollama models | `~/.ollama/models` |

`~/.local/share` is `$XDG_DATA_HOME` when you have set it.

## Windows (preview)

The Windows build is a **preview**: it is not code-signed. It was tested by hand on a Windows PC
before release and is launch-tested in release CI.

1. Download `OLIVE-Setup-1.0.0-windows-x86_64.exe` and verify it:

   ```powershell
   Get-FileHash .\OLIVE-Setup-1.0.0-windows-x86_64.exe -Algorithm SHA256
   ```

   Compare the result with the line for this file in `SHA256SUMS.txt`.
2. Run the installer. SmartScreen shows **"Windows protected your PC"** because the file is
   unsigned. If the checksum matched, choose **More info → Run anyway**. Do not turn off
   SmartScreen or Microsoft Defender.
3. OLIVE installs for your user, without administrator rights, into
   `%LOCALAPPDATA%\Programs\OLIVE`, adds a Start menu entry and starts.
4. Install Ollama from [ollama.com/download](https://ollama.com/download). OLIVE 1.0's setup does
   not download Ollama on Windows. It finds the official Ollama install and then downloads the
   models.

| | Location |
| --- | --- |
| Program | `%LOCALAPPDATA%\Programs\OLIVE` |
| Profile | `%USERPROFILE%\.olive` (or an existing `.dmdo`) |
| Runtimes | `%LOCALAPPDATA%\OLIVE\runtime` |

**Uninstall:** Settings → Apps → Installed apps → OLIVE → Uninstall. This removes the program and
its shortcuts only, never your profile, runtimes or models.

## macOS and iPhone

Neither is part of OLIVE 1.0. A macOS build needs Apple signing and notarisation and testing on a
Mac first; the iPhone companion needs App Store distribution.

## After installing

On first start OLIVE opens setup:

1. **Welcome:** your name (optional).
2. **System check:** operating system, processor, memory, GPU and free space per drive.
3. **Package:** OLIVE Core, or OLIVE Creator on Linux with an NVIDIA GPU.
4. **Runtimes and models:** what will be downloaded, from where, and how much space it needs.
   Existing Ollama installs and models are reused.
5. **Verification:** OLIVE checks each feature and asks FAST one short question.
6. **OLIVE Connect** and **Connect World:** optional. You can skip both.

Choose **Set up later** at any time; Settings → Open setup brings it back.
