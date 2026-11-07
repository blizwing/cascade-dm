# Cascade Download Manager

**Cascade Download Manager by Blueflame OPC** is a fast, multi-connection download manager for Windows, built for people and for scripts and AI agents. It splits a file into segments, resumes where it left off, checks what it downloaded, and can be driven from the command line.

> **Download:** open [**Releases**](../../releases/latest) and grab `Cascade DM <version>.zip`.

## Why Cascade DM

- **Fast and resumable** - up to 32 connections per file, pause and resume, a queue with priorities, speed limits and automatic retries.
- **Checks what it downloads** - every finished file gets the Windows "downloaded from the internet" mark and is handed to Windows Defender (or your antivirus). It also looks for disguised programs (a `.exe` named `.pdf`), dangerous file types, risky archives and unsigned installers. Anything serious is **quarantined** instead of landing in your folders, and you decide whether to release or delete it. It is a safety net, not a replacement for your antivirus.
- **Built-in browser with tabs** - open sites that create download links on the fly; downloads you click are captured with your login and referrer, so they stay segmented and resumable.
- **Made for scripts and agents** - the `cdm` command-line tool prints plain text or `--json`, uses clear exit codes, and can ask you to approve a download before it starts. Agents are kept away from private network addresses and your own folders by default.
- **Tidy by default** - files sort into `Downloads\CDM\<category>`, with the file name the server provides. Optional checksum verification (SHA-256, MD5, SHA-1).
- **Quiet in the background** - tray icon, start with Windows, clipboard link detection and notifications, all optional.
- **Safe updates** - update from a file inside the app, with a backup first and one-click rollback. Installing an older version is blocked; rollback is the way back.
- **Private by design** - no account, no ads, no telemetry. It only connects to the addresses you ask it to download from.

## Requirements

- Windows 10 or 11 (64-bit)
- Microsoft Edge WebView2 Runtime (already present on Windows 11 and most Windows 10 installs)

## Install

1. Download `Cascade DM <version>.zip` from the latest release.
2. Check it (optional): the release page lists its SHA-256. In PowerShell: `Get-FileHash "Cascade DM <version>.zip" -Algorithm SHA256`.
3. Unzip the `Cascade DM` folder anywhere you like (for example `C:\Apps`).
4. Run `cascade-dm.exe`.

The first run may show **"Windows protected your PC"** because this early build is not code-signed. Choose *More info* then *Run anyway* only if you downloaded it from this page.

## Update and roll back

- **Update:** in the app, go to *Settings -> About -> Update from file...* and pick the newer zip. Your downloads, settings and saved credentials are kept. You can also run `Update Cascade DM.bat` from the install folder.
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

Downloads go to `Downloads\CDM`. The job history and settings live in `%LOCALAPPDATA%\CascadeDM`. A proxy password, if you set one, is kept in Windows Credential Manager, not in a file.

## Status

Early releases (`0.1.x`). Expect rough edges and quick changes. Release notes are on each release page.

---

Cascade Download Manager is a personal project by Blueflame OPC, provided as is, without warranty. The source code is not public.
