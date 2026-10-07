# FastCommander

A fast file **copy, move, mirror-sync, delete and compare** tool for Windows, with Explorer right-click integration.

## Download

**[Download the latest version](../../releases/latest)** (Windows 10/11, 64-bit, about 80 MB)

1. Open the link above and download `FastCommander-...-win-x64.zip`.
2. Unzip it anywhere.
3. Run `FastCommander.UI.exe`. You do **not** need to install .NET; it is included.

> The app is not code-signed yet, so Windows SmartScreen may show a warning the first time. Choose **More info**, then **Run anyway**.

## What it does

- **Copy, Move, Mirror Sync, Delete and Dry-Run Diff** in one window, with a job queue, history, favorite folders and a live progress view showing speed and time remaining.
- **Fast folder copies.** In the author's tests a 14 GB folder with about 78,000 files copied roughly three times faster than the first version and level with `robocopy /MT:16`. One PC, one folder: your results will vary with your disk, CPU and antivirus.
- **Large files** use a Direct I/O pipeline that avoids filling the Windows file cache, and Cancel stays responsive. On ReFS / Dev Drive volumes it can clone files instantly.
- **Moves within one drive are renames**, so they are instant.
- **Keeps timestamps** and NTFS alternate data streams (such as the "downloaded from the internet" mark) on large files.
- **Overwrite rules:** always, only if newer, only if size or date differ, or never.
- **Safety:** a move deletes the source only after the destination is verified; locked files are skipped without stopping the rest of the folder; delete and sync handle read-only and hidden files.
- **Explorer integration:** Windows 11 modern right-click menu and classic menu entries for copy, move, paste and delete. Turn them on from **Options > General**.
- **Command line:** `FastCommander.exe --copy|-c <src> <dst>`, `--move|-m`, `--sync|-s`, `--delete|-d <target>`.
- English and Turkish interface.

## Requirements

- Windows 10 or 11, 64-bit.
- The Windows 11 modern right-click menu needs **Developer Mode** turned on (Settings > System > For developers). The app tells you if it is off.

## Known limits

- Copies of files under 256 MB cannot report progress inside a single file or be cancelled mid-file.
- Cancelling a large copy can leave the partly written destination file behind.
- Moves across drives and network shares have not been fully tested.

## Source code

The source code is not public. This repository only hosts the downloads and release notes.
