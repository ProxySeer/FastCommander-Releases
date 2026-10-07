# FastCommander

A fast file **copy, move, mirror-sync, delete and compare** tool for Windows, with Explorer right-click integration.

**Türkçe:** [README.tr.md](README.tr.md)

## Download

**[Download the latest version](../../releases/latest)** (Windows 10/11, 64-bit, about 80 MB)

1. Open the link above and download `FastCommander-...-win-x64.zip`.
2. Unzip it anywhere.
3. Run `FastCommander.UI.exe`. You do **not** need to install .NET; it is included.

> The app is not code-signed yet, so Windows SmartScreen may show a warning the first time. Choose **More info**, then **Run anyway**.

## What it does

- **Copy, Move, Mirror Sync, Delete and Dry-Run Diff** in one window, with a job queue, history, favorite folders and a live progress view showing speed and time remaining.
- **Fast copies.** About 18 times faster than the Windows copy and level with `robocopy /MT:16` on a large folder in the author's tests; see [Speed](#speed) for the numbers.
- **Large files** use a Direct I/O pipeline that avoids filling the Windows file cache, and Cancel stays responsive. On ReFS / Dev Drive volumes it can clone files instantly.
- **Moves within one drive are renames**, so they are instant.
- **Keeps timestamps** and NTFS alternate data streams (such as the "downloaded from the internet" mark) on large files.
- **Overwrite rules:** always, only if newer, only if size or date differ, or never.
- **Safety:** a move deletes the source only after the destination is verified; locked files are skipped without stopping the rest of the folder; delete and sync handle read-only and hidden files.
- **Explorer integration:** Windows 11 modern right-click menu and classic menu entries for copy, move, paste and delete. Turn them on from **Options > General**.
- **Command line:** `FastCommander.UI.exe --cli --copy|-c <src> <dst>`, `--cli --move|-m`, `--cli --sync|-s`, `--cli --delete|-d <target>`.
- English and Turkish interface.

## Speed

Measured on one Windows 11 PC, with source and destination on the same SSD and other apps running. Each tool copied the same data into a fresh empty destination, and the order of the tools was rotated between rounds. Every run was checked to have copied the same number of files and bytes.

**14.3 GB folder, 78,613 files**

| Tool | Time | Speed |
|---|---|---|
| Windows copy (the Explorer copy engine) | 859 s (14 min 19 s), one run | 17 MB/s, 91 files/s |
| `robocopy /MT:16` | 54.2 s and 50.5 s, average 52.4 s | 280 MB/s, 1,500 files/s |
| **FastCommander** | 47.7 s and 44.8 s, average 46.3 s | **317 MB/s, 1,700 files/s** |

FastCommander was about 18 times faster than the Windows copy. It was about 12% faster than `robocopy` and won both rounds, but that gap is small, so treat the two as roughly level.

**8 GB single file** (two runs each)

| Tool | Run 1 | Run 2 | Average |
|---|---|---|---|
| Windows copy | 8.0 s | 19.7 s | 13.9 s |
| `robocopy` | 8.3 s | 17.2 s | 12.8 s |
| **FastCommander** | 4.2 s | 6.7 s | **5.5 s** |

FastCommander was fastest in both rounds, about 2.5 times faster than the other two on average. Single-file timings swing a lot from run to run (the same file took 20 s or more on an earlier, busier day), so treat these as rough.

**Caveats:** one machine, one disk, one folder. "Windows copy" is the Windows shell copy engine run without Explorer's progress window, and I only got one folder run for it (an earlier hand-timed Explorer copy of the same folder took about 400 s, so expect anywhere from 6 to 14 minutes). HDDs, network shares and very different file-size mixes are untested. Your disk, CPU and antivirus will change the numbers.

## Requirements

- Windows 10 or 11, 64-bit.
- The Windows 11 modern right-click menu needs **Developer Mode** turned on (Settings > System > For developers). The app tells you if it is off.

## Known limits

- Copies of files under 256 MB cannot report progress inside a single file or be cancelled mid-file.
- Cancelling a large copy can leave the partly written destination file behind.
- Moves across drives and network shares have not been fully tested.

## Source code

The source code is not public. This repository only hosts the downloads and release notes.
