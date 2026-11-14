<p align="center"><img src="assets/icon.png" alt="Cascade Download Manager icon" width="128"></p>

# Cascade Download Manager

**Cascade Download Manager by Blueflame OPC** is a fast, multi-connection download manager for Windows, built for people and for scripts and AI agents. It splits a file into segments, resumes where it left off, checks what it downloaded, and can be driven from the command line.

> **Download:** open [**Releases**](../../releases/latest) and grab `Cascade.DM.<version>.zip` (GitHub shows the spaces in the name as dots).

## Why Cascade DM

- **Fast and resumable** - up to 32 connections per file, pause and resume, a queue with priorities, speed limits and automatic retries.
- **Checks what it downloads** - every finished file gets the Windows "downloaded from the internet" mark and is handed to Windows Defender (or your antivirus). It also looks for disguised programs (a `.exe` named `.pdf`), dangerous file types, risky archives and unsigned installers. Anything serious is **quarantined** instead of landing in your folders, and you decide whether to release or delete it. It is a safety net, not a replacement for your antivirus: it can miss threats or flag harmless files.
- **Built-in browser with tabs** - open sites that create download links on the fly; downloads you click are captured with your login and referrer, so they stay segmented and resumable.
- **Made for scripts and agents** - the `cdm` command-line tool prints plain text or `--json`, uses clear exit codes, and can ask you to approve a download before it starts. Agents are kept away from private network addresses and your own folders by default.
- **Tidy by default** - files sort into `Downloads\CDM\<category>`, with the file name the server provides. Optional checksum verification (SHA-256, MD5, SHA-1).
- **Quiet in the background** - tray icon, start with Windows, clipboard link detection and notifications, all optional.
- **Safe updates** - update from a file inside the app, with a backup first and one-click rollback. Installing an older version is blocked; rollback is the way back.
- **Private by design** - no account, no ads, no telemetry, and nothing is sent to Blueflame. It connects only to the sites you download from or open in its browser. If you turn on encrypted DNS (optional), website name lookups go to the resolver you choose, for example Cloudflare or Google.

## Requirements

- Windows 10 or 11 (64-bit)
- Microsoft Edge WebView2 Runtime (already present on Windows 11 and most Windows 10 installs). Cascade DM uses the copy already on your PC and does not bundle it. It keeps its own separate browser profile inside its data folder, so it never shares cookies, logins or settings with other apps that also use WebView2.

## Install

1. Download `Cascade.DM.<version>.zip` from the latest release.
2. Check it (optional): the release page lists its SHA-256. In PowerShell: `Get-FileHash "Cascade.DM.<version>.zip" -Algorithm SHA256`.
3. Unzip the `Cascade DM` folder anywhere you like (for example `C:\Apps`).
4. Run `cascade-dm.exe`.

The first run may show **"Windows protected your PC"** because Cascade DM is not code-signed yet. Choose *More info* then *Run anyway* only if you downloaded it from this page.

## Update and roll back

- **Update:** in the app, go to *Settings -> About -> Update from file...* and pick the newer zip (the `Cascade.DM.<version>.zip` file you downloaded). Your downloads, settings and saved credentials are kept. You can also run `Update Cascade DM.bat` from the install folder.
- **Roll back:** *Settings -> About* lists the backups made before each update. Pick one to go back.

## Command line

```powershell
cdm get https://example.com/file.zip          # download, then scan the result
cdm get https://example.com/file.zip --json   # machine-readable progress and result
cdm status <job-id> --wait
cdm list --state quarantined
cdm --help
```

A few exit codes: `0` success, `3` network error, `4` blocked by the safety policy, `6` approval rejected, `7` approval timed out, `12` quarantined by the security scan.

## Your data

Downloads go to `Downloads\CDM`. The job history and settings live in `%LOCALAPPDATA%\CascadeDM`. A proxy password, if you set one, is kept in Windows Credential Manager, not in a file. The optional browser extension hands the address, cookies and referrer of a download you start in your browser to Cascade DM on the same PC, so the site accepts the download; they are not sent anywhere else.

## Status

Version **1.0** is the first stable release. Release notes are on each release page.

## Use it responsibly

Cascade DM is a general download tool. You decide what to download, and you are responsible for having the right to download and use it and for following the terms of the sites you use. It is not built to bypass copy protection or DRM, and you must not use it for that.

## License

Cascade Download Manager is free to use under the [End User License Agreement](EULA.txt) (also included in the download as `EULA.txt`). It is proprietary software: the source code is not public and you may not resell or modify it. It includes open-source components, whose licenses are listed in `THIRD-PARTY-NOTICES.txt` inside the download. By installing or using it you agree to the EULA.

---

Cascade Download Manager is made by Blueflame OPC and provided as is, without warranty (see the EULA). Found a bug? Open an [issue](../../issues).

Windows, Windows Defender, Microsoft Edge and WebView2 are trademarks of Microsoft Corporation. Chrome, Firefox, Brave, Cloudflare, Google and other names mentioned belong to their owners. Cascade Download Manager is an independent product and is not affiliated with or endorsed by any of them.
