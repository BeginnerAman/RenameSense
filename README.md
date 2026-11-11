# RenameSense

Intelligent, safe, and offline-first batch file renamer for Windows 10 and Windows 11.

[Download Official Installer (v3.0.0)](https://github.com/BeginnerAman/RenameSense/releases/download/v3.0.0/RenameSense-3.0.0-Setup.exe) | [Visit Official Website](https://beginneraman.github.io/RenameSense/) | [View License](LICENSE)

---

## 1. Overview

RenameSense is a modern, high-performance desktop utility engineered to rename thousands of files quickly and safely. It replaces fragile, confusing renamers with a structured, visual workbench built on a zero-data-loss principle.

Every rename operation is logged to an atomic Write-Ahead Log (WAL) transaction journal. If you make a mistake, you can reverse the entire batch with a single click, restoring all original filenames with 100% fidelity.

RenameSense is 100% free proprietary software. All core file scanning, template evaluation, regex matching, and disk renaming execute locally on your machine with zero cloud telemetry.

---

## 2. Key Highlights

### For Everyday Users
* Simple 3-step workflow: Select a folder, preview proposed names in real time, and click Rename.
* Dynamic template tags: Click to insert tokens like `{name}`, `{seq}`, `{date}`, `{parent}`, and `{cleaned}`.
* Safe 1-click undo: Roll back any previous batch operation instantly from the Audit History ledger.
* Real-time preview diff: Inspect changes before writing a single byte to disk, with color-coded additions and deletions.
* Windows Explorer context menu: Right-click any folder or directory in Windows to open it directly in RenameSense.
* Fast dark and light theme: Native Windows 11 Fluent interface with automatic theme switching and zero screen flicker.

### For Power Users and Technologists
* Multi-stage sequential rule pipeline: Chain multiple find-and-replace rules where each step transforms the output of the prior step.
* Full regular expressions: Capture groups (`$1`, `$2`), lookaheads, case sensitivity flags, and live syntax validation.
* Write-Ahead Log (WAL) engine: Durable JSONL transaction journal records atomic rename states for guaranteed recovery.
* Collision and conflict detection: Proactively prevents overwrites, duplicate targets, invalid Win32 characters, and reserved system names.
* Case-only rename resolution: Two-phase intermediate staging (`file.txt` to temp to `FILE.TXT`) handles Windows case-insensitive filesystems cleanly.
* Extended length path support: Transparent Win32 extended path prefixing (`\\?\`) handles paths exceeding the traditional 260-character limit.
* High-volume performance: Virtualized rendering easily handles directories with over 50,000 files at 60 frames per second.

---

## 3. Core Transformation Engines

### Dynamic Template Format
Build structured filenames using dynamic metadata tokens:
* `{name}`: Original filename without extension.
* `{cleaned}`: Output of any preceding sequential Replace rules.
* `{ext}`: Original file extension.
* `{seq}` or `{seq:03d}`: Sequential numbering with custom padding (e.g., 001, 002).
* `{date:YYYY-MM-DD}`: Current date or file modification timestamp.
* `{parent}`: Name of the enclosing parent folder.
* `{artist}`, `{title}`, `{track}`: Embedded ID3 tags for audio files.
* `{camera}`, `{exif_date}`: Embedded EXIF metadata for photos.

### Sequential Replace Pipeline
Chain multiple rules sequentially:
* Rule 1: Extract numeric IDs via regex `DSC_([0-9]+)` to `Photo_$1`.
* Rule 2: Remove unwanted substrings or replace separators.
* Rule 3: Insert live dynamic tokens into replacement strings.

### Case and Separator Formatting
Standardize naming across file collections:
* Case transformations: lowercase, UPPERCASE, Title Case, camelCase, snake_case, kebab-case.
* Separator cleanup: Convert spaces, underscores, dots, or hyphens consistently.
* Cleanup tools: Strip leading and trailing whitespace, remove double spaces, and eliminate punctuation.

### Extension Management
* Batch convert extensions (e.g., `.jpeg` to `.jpg`).
* Enforce lowercase or uppercase extensions across all files.

---

## 4. Safety Architecture and Invariants

RenameSense is built on strict data-safety invariants:
1. Non-Destructive Preview: The preview engine operates entirely in memory. Disk files are untouched until you explicitly click "Rename Selected Files".
2. Atomic Transaction Journal: Renames are recorded to a durable journal before execution. In case of power loss or process interruption, the journal detects incomplete batches on restart.
3. 1-Click Rollback Ledger: Every committed batch can be audited, exported, and reversed. Rollback executes reverse operations atomically.
4. Pre-Flight Collision Shield: Detects name collisions, existing destination files, and invalid filesystem characters before renaming starts.
5. Local and Offline: No file paths, names, or file contents are ever uploaded to any remote server.

---

## 5. Keyboard Shortcuts HUD

| Shortcut | Description |
|---|---|
| Ctrl + O | Open native folder browser dialog |
| F5 / Ctrl + R | Refresh and re-scan active folder |
| F2 | Quick inline edit of focused proposed filename |
| Space | Toggle selection for the currently focused row |
| Ctrl + A | Select all files in the active list |
| Ctrl + Shift + A | Deselect all files in the active list |
| Up / Down Arrow | Navigate between files in the preview table |
| Ctrl + Enter | Commit and execute batch rename |
| Ctrl + Z | Quick undo for the most recently completed batch |
| Ctrl + Shift + T | Toggle between Light and Dark interface themes |
| Escape | Close open modals or clear current search filter |
| ? | Open Keyboard Shortcuts help HUD |

---

## 6. System Requirements

* Operating System: Windows 11 or Windows 10 (64-bit edition).
* Architecture: x64 compatible processor.
* Runtime: Microsoft Edge WebView2 Runtime (pre-installed on Windows 10 and 11).
* Memory: 512 MB RAM minimum (2 GB recommended for 50,000+ file batches).
* Disk Space: 180 MB free disk space.
* Permissions: Standard user account (no administrator rights required for standard installation).

---

## 7. Installation

1. Download the latest installer: [RenameSense-3.0.0-Setup.exe](https://github.com/BeginnerAman/RenameSense/releases/download/v3.0.0/RenameSense-3.0.0-Setup.exe).
2. Run the installer. It installs per-user into your local application directory without triggering UAC administrator prompts.
3. Launch RenameSense from your Start Menu, Desktop shortcut, or by right-clicking any folder in Windows Explorer and choosing "Open with RenameSense".

---

## 8. License and Terms of Use

RenameSense is proprietary freeware created by Aman Vishwakarma.

* You are free to download, install, and use RenameSense for both personal and commercial purposes at zero cost.
* RenameSense is closed source software. Reverse engineering, decompiling, disassembling, modifying, or republishing modified binaries is strictly prohibited.
* For complete legal terms, review the full [LICENSE](LICENSE) agreement.

Copyright (c) 2026 Aman Vishwakarma. All rights reserved.
