<p align="center">
  <a href="https://beginneraman.github.io/RenameSense/">
    <img src="assets/logo_wordmark.png" alt="RenameSense Logo" width="380">
  </a>
</p>

<p align="center">
  <b>Enterprise-Grade, Safe, and Offline-First Batch File Renamer for Windows</b>
</p>

<p align="center">
  <a href="https://github.com/BeginnerAman/RenameSense/releases/tag/v3.0.0"><img src="https://img.shields.io/badge/release-v3.0.0-0284c7?style=flat-square" alt="Release"></a>
  <a href="https://beginneraman.github.io/RenameSense/"><img src="https://img.shields.io/badge/website-live-0ea5e9?style=flat-square" alt="Website"></a>
  <img src="https://img.shields.io/badge/platform-Windows%2010%20%7C%2011%20(64--bit)-0369a1?style=flat-square" alt="Platform">
  <img src="https://img.shields.io/badge/license-Freeware%20(Proprietary)-1e293b?style=flat-square" alt="License">
  <img src="https://img.shields.io/badge/offline-100%25%20Local--First-0284c7?style=flat-square" alt="Offline">
  <img src="https://img.shields.io/badge/author-Aman%20Vishwakarma-0ea5e9?style=flat-square" alt="Author">
</p>

<p align="center">
  <a href="https://github.com/BeginnerAman/RenameSense/releases/download/v3.0.0/RenameSense-3.0.0-Setup.exe"><b>Download Setup Installer (74.2 MB)</b></a> | 
  <a href="https://github.com/BeginnerAman/RenameSense/releases/download/v3.0.0/RenameSense-3.0.0-Portable.zip"><b>Download Portable Package (106.4 MB)</b></a> | 
  <a href="https://beginneraman.github.io/RenameSense/"><b>Visit Official Website</b></a> | 
  <a href="LICENSE"><b>License Agreement</b></a>
</p>

---

## 1. Overview

RenameSense is a modern, high-performance Windows desktop application engineered to rename thousands of files quickly, predictably, and safely. It replaces fragile legacy renamers with a structured, visual workbench built on a zero-data-loss principle.

Every rename operation is committed to an atomic Write-Ahead Log (WAL) transaction journal. If you make a mistake, you can reverse the entire batch with a single click, restoring all original filenames with 100% fidelity.

RenameSense is 100% free proprietary software for personal, organizational, and commercial use. All file scanning, template evaluation, regex pattern matching, and filesystem mutations execute strictly on your local machine with zero cloud telemetry.

---

## 2. Key Highlights

### For Everyday Users
* Simple 4-step workflow: Select or drop a folder, configure dynamic tokens, preview live diffs, and rename.
* Dynamic template tags: Click to insert tokens like `{name}`, `{seq}`, `{date}`, `{parent}`, and `{cleaned}`.
* Safe 1-click undo: Roll back any previous batch operation instantly from the persistent Audit History ledger.
* Real-time preview diff: Inspect changes before writing a single byte to disk, with color-coded additions and deletions.
* Windows Explorer context menu: Right-click any folder or directory in Windows to open it directly in RenameSense.
* Fluent dark and light interface: Native Windows 11 aesthetics with seamless theme switching and zero screen flicker.

### For Power Users and Technologists
* Multi-stage sequential rule pipeline: Chain multiple find-and-replace rules where each step transforms the output of the prior step.
* Full regular expressions: Capture groups (`$1`, `$2`), lookaheads, case sensitivity flags, and live syntax validation.
* Write-Ahead Log (WAL) engine: Durable JSONL transaction journal records atomic rename states for guaranteed recovery.
* Collision and conflict detection: Proactively prevents overwrites, duplicate targets, invalid Win32 characters, and reserved system names.
* Case-only rename resolution: Two-phase intermediate staging (`file.txt` to temporary UUID to `FILE.TXT`) handles Windows case-insensitive filesystems cleanly.
* Extended length path support: Transparent Win32 extended path prefixing (`\\?\`) handles deep directory paths exceeding the traditional 260-character limit.
* High-volume performance: Virtualized table rendering smoothly handles directories with over 50,000 files at 60 frames per second.

---

## 3. Core Transformation Engines

### Dynamic Template Format
Build structured filenames using dynamic metadata tokens:
* `{name}`: Original filename without extension.
* `{cleaned}`: Output of preceding sequential Replace rules.
* `{ext}`: Original file extension.
* `{seq}` or `{seq:03d}`: Sequential numbering with custom zero-padding (e.g., 001, 002).
* `{date:YYYY-MM-DD}`: Current date or file modification timestamp.
* `{parent}`: Name of the enclosing parent folder.
* `{artist}`, `{title}`, `{track}`: Embedded ID3 tags for audio files.
* `{camera}`, `{exif_date}`: Embedded EXIF metadata for photos.

### Sequential Replace Pipeline
Chain multiple rules sequentially:
* Rule 1: Extract numeric IDs via regex `DSC_([0-9]+)` to `Photo_$1`.
* Rule 2: Remove unwanted substrings or replace separators.
* Rule 3: Insert dynamic tokens into replacement strings.

### Case and Separator Formatting
Standardize naming across file collections:
* Transformations: lowercase, UPPERCASE, Title Case, camelCase, snake_case, and kebab-case.
* Separator cleanup: Convert underscores, hyphens, and periods cleanly.
* Extension normalization: Unify extensions across mixed collections (e.g., `.JPEG` to `.jpg`).

---

## 4. Safety Architecture and Invariants

* Zero silent overwrites: RenameSense rejects destination overwrite conflicts before any file is touched.
* Staged case changes: Case-only renames on NTFS and ReFS filesystems use deterministic two-phase staging to eliminate file collision.
* Transactional rollbacks: All batch operations are written to `%LOCALAPPDATA%\RenameSense\history\transactions.jsonl` prior to disk execution.
* Reserved name protection: Automatically flags illegal characters (`<`, `>`, `:`, `"`, `/`, `\`, `|`, `?`, `*`) and Windows reserved device names (`CON`, `PRN`, `AUX`, `NUL`, `COM1-9`, `LPT1-9`).

---

## 5. Keyboard Shortcuts

| Shortcut | Action | Description |
|---|---|---|
| `F2` | Focus Path Input | Jump cursor to the folder path input bar |
| `Enter` | Scan Folder | Trigger directory scan when focused on path input |
| `Ctrl + Enter` | Execute Batch | Apply renames to all selected files |
| `Ctrl + Z` | Undo Last Batch | Roll back the most recent batch operation |
| `Ctrl + D` | Toggle Theme | Switch between Dark and Light Fluent UI modes |
| `Ctrl + ?` | Shortcuts Modal | View complete keyboard shortcuts guide |
| `Esc` | Close Modal | Dismiss open dialogs or overlays |

---

## 6. System Requirements

* Operating System: Windows 10 (64-bit) or Windows 11 (64-bit).
* Architecture: x86-64 compatible processor.
* Runtime: Microsoft Edge WebView2 Runtime (pre-installed on Windows 10 and Windows 11).
* Memory: 4 GB RAM minimum (8 GB recommended for 50,000+ file batches).
* Disk Space: 250 MB free disk space for portable extraction (150 MB for installer).
* Permissions: Standard user account (no administrator rights required).

---

## 7. Official Downloads

RenameSense is distributed in two official formats:

### Windows Setup Installer (Recommended)
* File: [RenameSense-3.0.0-Setup.exe](https://github.com/BeginnerAman/RenameSense/releases/download/v3.0.0/RenameSense-3.0.0-Setup.exe)
* Size: 74,259,974 bytes (~74.2 MB)
* Features: Installs per-user without UAC administrator prompts, creates Desktop and Start Menu shortcuts, and integrates into the Windows Explorer right-click context menu.
* SHA-256 Checksum: `3EB8E830FF188A1F2A7D26BFA27F9562EA9BB9DB053615868DABED716A600137`

### Portable Package (No Installation Required)
* File: [RenameSense-3.0.0-Portable.zip](https://github.com/BeginnerAman/RenameSense/releases/download/v3.0.0/RenameSense-3.0.0-Portable.zip)
* Size: 111,594,747 bytes (~106.4 MB)
* Features: Standalone ZIP archive. Extract anywhere (including USB flash drives or external drives) and launch `RenameSense.exe` directly without installation.
* SHA-256 Checksum: `4D8E0F2E28EEF40E2361455DAE338DB14BE67BC9ADE4E79027C5D690E309D226`

---

## 8. License and Terms of Use

RenameSense is proprietary freeware created by Aman Vishwakarma.

* You are free to download, install, and use RenameSense for both personal and commercial purposes at zero cost.
* RenameSense is closed source software. Reverse engineering, decompiling, disassembling, modifying, or republishing modified binaries is strictly prohibited.
* For complete legal terms, review the full [LICENSE](LICENSE) agreement.

Copyright (c) 2026 Aman Vishwakarma. All rights reserved.
