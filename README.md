# CloudTorrent for Windows

Compiled releases of CloudTorrent for Windows. This repository holds the installer and its signed release files only;
there is no source code here.

## What it does

CloudTorrent sets up a small download helper on your PC. Torrents you save in the `CloudTorrent\Downloads` folder are
checked when they finish (only real video files pass) and filed under `CloudTorrent\Media`. Anything that doesn't look
like a video is set aside in `CloudTorrent\Held` for you to look at and delete. Torrents you save anywhere else are left
alone.

Everything stays on your PC and your home network. Only qBittorrent's torrent port is open to the internet; nothing
else listens outside this PC.

## What it installs

- **qBittorrent** (the torrent app), from the official package, at a pinned version. Its web interface listens on this
  PC only, and programs, scripts and shortcuts inside torrents are never downloaded.
- **FFmpeg** (to check that downloads are real videos), from the official package, at a pinned version.
- **The CloudTorrent helper**, in your user folder (`%USERPROFILE%\.magnet-relay`). It starts when you sign in and
  checks once a day for a newer signed release.

## System needs

- Windows 10 22H2 or Windows 11, 64-bit
- A drive with at least 50 GB free
- No other qBittorrent set up on this PC (CloudTorrent needs its own)

## Install

1. Download [`ct-setup.exe`](https://github.com/danyeoakl/cloudtorrent-public/releases/latest/download/ct-setup.exe).
2. Run it. The installer isn't code-signed, so Windows may show "Windows protected your PC": choose **More info**, then
   **Run anyway**.
3. When it asks for a friends-and-family code, press Enter to skip. **The code is optional**: without one you get the
   standalone setup described above. Only people who were given a code need one.
4. Approve the one Windows permission prompt (it installs qBittorrent).

Running `ct-setup.exe` again repairs an install, and with a code it switches the PC to the mode the code is for.

## Updates

Once a day the helper reads this repository's latest `manifest.json` and checks its signature. When a newer release is
there, it downloads it, checks every file's SHA-256, installs it and goes back to the previous version if the new one
doesn't start. Updates never ask for permission. A qBittorrent update is installed the next time you run `ct-setup.exe`.

## Release files

| File | What |
|---|---|
| `ct-setup.exe` | The installer and updater |
| `ctd-<version>-win-x64.zip` | The helper |
| `ctd.standalone.json`, `ctd.uploader.json` | Its settings templates |
| `manifest.json`, `manifest.sig` | The file list with sizes and SHA-256, and its ECDSA P-256 signature |

## Uninstall

1. Remove the helper from startup: Settings › Apps › Startup, turn off **CloudTorrent ctd**, then sign out and in.
2. Delete `%USERPROFILE%\.magnet-relay`.
3. Uninstall qBittorrent and FFmpeg from Settings › Apps if you don't use them. Your `CloudTorrent` folder stays until you
   delete it.
