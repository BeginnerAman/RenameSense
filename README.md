<p align="center">
  <a href="https://beginneraman.github.io/RenameSense/">
    <img src="assets/app_icon.png" alt="RenameSense Logo" width="128" height="128" style="border-radius: 24px;">
  </a>
</p>

<h1 align="center">RenameSense</h1>

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
  <a href="https://github.com/BeginnerAman/RenameSense/releases/download/v3.0.0/RenameSense-3.0.0-Setup.exe"><b>Download Setup Installer (58.1 MB)</b></a> | 
  <a href="https://github.com/BeginnerAman/RenameSense/releases/download/v3.0.0/RenameSense-3.0.0-Portable.zip"><b>Download Portable Package (79.4 MB)</b></a> | 
  <a href="https://beginneraman.github.io/RenameSense/"><b>Visit Official Website</b></a> | 
  <a href="LICENSE"><b>License Agreement</b></a>
</p>

---

## Table of Contents
1. [Overview](#1-overview)
2. [Key Architecture & Features](#2-key-architecture--features)
3. [Multi-Stage Sequential Regex Engine](#3-multi-stage-sequential-regex-engine)
   * [How the Sequential Pipeline Works](#how-the-sequential-pipeline-works)
   * [Practical Regex Examples with Before & After](#practical-regex-examples-with-before--after)
4. [AI Regex & Pattern Assistant](#4-ai-regex--pattern-assistant)
   * [Dual Provider & Local Fallback Architecture](#dual-provider--local-fallback-architecture)
   * [Security & Secret Redaction Framework](#security--secret-redaction-framework)
5. [Dynamic Template Engine & Tokens Reference](#5-dynamic-template-engine--tokens-reference)
   * [Core Filesystem Tokens](#core-filesystem-tokens)
   * [Audio, EXIF & Document Tokens](#audio-exif--document-tokens)
   * [Seamless Template Chaining](#seamless-template-chaining)
6. [Safety Engine & Atomic WAL Transactions](#6-safety-engine--atomic-wal-transactions)
   * [Two-Phase Write-Ahead Logging (WAL)](#two-phase-write-ahead-logging-wal)
   * [Guaranteed 1-Click Rollback](#guaranteed-1-click-rollback)
   * [Collision Detection & Case Staging](#collision-detection--case-staging)
7. [Productivity & Workflow Features](#7-productivity--workflow-features)
8. [Keyboard Shortcuts Reference](#8-keyboard-shortcuts-reference)
9. [System Requirements](#9-system-requirements)
10. [Official Downloads & Checksums](#10-official-downloads--checksums)
11. [License & Terms of Use](#11-license--terms-of-use)

---

## 1. Overview

RenameSense is a modern, high-performance Windows desktop application engineered to rename thousands of files quickly, predictably, and safely. It replaces fragile, legacy renaming utilities with a structured visual workbench designed around a strict zero-data-loss principle.

Every batch operation is executed through a transactional Write-Ahead Log (WAL) engine. Before a single file on disk is modified, intent records are committed to persistent storage. If an unexpected condition occurs (such as an in-use file lock or sudden power failure), or if you simply change your mind, the entire batch can be reversed with a single click, restoring original filenames with 100% fidelity.

RenameSense is 100% free proprietary desktop software for personal, organizational, and commercial use. All directory scanning, metadata extraction, regular expression processing, and filesystem operations execute locally on your machine with zero cloud telemetry.

---

## 2. Key Architecture & Features

### Core Design Principles
* **Local & Offline-First**: Zero required internet connectivity. Zero analytics packets. Zero file content tracking.
* **Non-Destructive Workflows**: Real-time virtualized preview diffs show proposed names, collisions, and character modifications before any disk operation occurs.
* **Deterministic Execution**: Predictable transformation pipelines ensure that renames happen in exact user-defined sequences.
* **High-Throughput Performance**: Virtualized table architecture handles 50,000+ files with sub-10ms UI latency.

---

## 3. Multi-Stage Sequential Regex Engine

RenameSense features an industrial-grade Regular Expression (Regex) engine built directly into its core processing pipeline. It allows you to transform filenames with surgical precision using standard regular expressions, capture groups, lookaheads, and dynamic sequence tokens.

### How the Sequential Pipeline Works

In RenameSense, find-and-replace rules operate as a **multi-stage sequential pipeline**:
1. **Rule 1** executes on the original filename stem.
2. The output of Rule 1 is immediately fed as the input to **Rule 2**.
3. The output of Rule 2 is fed to **Rule 3**, and so on.
4. Each rule can independently toggle regular expressions (`use_regex`), case sensitivity (`match_case`), and capture group replacements.

```
Original Filename
       │
       ▼
┌──────────────┐
│  Rule #1     │ ──► Regex extraction or cleanup
└──────────────┘
       │
       ▼ (Intermediary Stem)
┌──────────────┐
│  Rule #2     │ ──► Separator standardization
└──────────────┘
       │
       ▼ (Cleaned Stem)
┌──────────────┐
│  Rule #3     │ ──► Dynamic token insertion ({seq:03d}, {date})
└──────────────┘
       │
       ▼
Final Proposed Filename + Original Extension
```

### Capture Groups and Backreferences
RenameSense fully supports standard capture groups:
* Parentheses `(...)` define capture groups in your search pattern.
* In the replacement string, reference captured groups using `$1`, `$2`, `$3` (or standard `\1`, `\2`).
* Unescaped `$1`, `$2` tokens are automatically translated into safe, high-performance regex replacement backreferences.

---

### Practical Regex Examples with Before & After

Below are real-world renaming scenarios showing how to solve complex file organization tasks with RenameSense.

#### Example A: Standardizing Messy Media & TV Episodes
Downloaded TV episodes often contain erratic release tags, codecs, audio formats, and dots instead of spaces.

* **Target Goal**: Extract the show title, season, and episode numbers, replace dots with spaces, and eliminate junk release metadata.
* **Sample Original Filename**: `Silicon.Valley.S03E04.1080p.WEBRip.x264-[YTS.AM].mkv`

| Step | Rule Mode | Search Pattern | Replace String | Intermediary Output |
|---|---|---|---|---|
| Rule 1 | Regex (Match Case: Off) | `^([a-zA-Z\.\s]+)\.S(\d{2})E(\d{2})\..*$` | `$1 - S$2E$3` | `Silicon.Valley - S03E04` |
| Rule 2 | Literal / Simple Replace | `.` | ` ` (Single space) | `Silicon Valley - S03E04` |

* **Final Result**: `Silicon Valley - S03E04.mkv`

---

#### Example B: Digital Camera Photo Organization
Digital cameras and smartphones generate filenames with timestamps and arbitrary prefixes (`IMG_20261112_143022_HDR.jpg`).

* **Target Goal**: Parse the year, month, and day from the filename, append a descriptive project tag, and insert zero-padded sequential numbers (`001`, `002`).
* **Sample Original Filename**: `IMG_20261112_143022_HDR.jpg`

| Step | Rule Mode | Search Pattern | Replace String | Resulting Output |
|---|---|---|---|---|
| Rule 1 | Regex (Match Case: Off) | `^IMG_(\d{4})(\d{2})(\d{2})_\d{6}.*$` | `$1-$2-$3_Trip_{seq:03d}` | `2026-11-12_Trip_001.jpg` |

* **Final Batch Results**:
  * `IMG_20261112_143022_HDR.jpg` -> `2026-11-12_Trip_001.jpg`
  * `IMG_20261112_143045_BURST.jpg` -> `2026-11-12_Trip_002.jpg`
  * `IMG_20261112_150210.jpg` -> `2026-11-12_Trip_003.jpg`

---

#### Example C: Corporate Invoices and Contracts Cleanup
Business documents often accumulate redundant version suffixes (`_FINAL`, `_v2`, `_Signed`) that make chronological sorting difficult.

* **Sample Original Filename**: `Invoice_#489201-Acme Corp_Signed_FINAL_v2.pdf`

| Step | Rule Mode | Search Pattern | Replace String | Intermediary Output |
|---|---|---|---|---|
| Rule 1 | Regex | `_(?:v\d+|Signed|FINAL)+` | *(Empty)* | `Invoice_#489201-Acme Corp` |
| Rule 2 | Regex | `^Invoice_#(\d+)-(.*)$` | `INV-$1 - $2 - {date:YYYYMMDD}` | `INV-489201 - Acme Corp - 20261112` |

* **Final Result**: `INV-489201 - Acme Corp - 20261112.pdf`

---

#### Example D: Music Tracks & Audio Library Cleanup
Audio tracks downloaded from multiple sources often have leading track numbers, artist prefixes, or bracketed year tags.

* **Sample Original Filename**: `04. The Beatles - Eleanor Rigby (2015 Stereo Mix) [FLAC].flac`

| Step | Rule Mode | Search Pattern | Replace String | Intermediary Output |
|---|---|---|---|---|
| Rule 1 | Regex | `\s*\[[^\]]*\]` | *(Empty - strips brackets)* | `04. The Beatles - Eleanor Rigby (2015 Stereo Mix)` |
| Rule 2 | Regex | `\s*\([^)]*Mix\)` | *(Empty - strips mix tags)* | `04. The Beatles - Eleanor Rigby` |
| Rule 3 | Regex | `^\d+[\.\s-]+\s*` | `{seq:02d} - ` | `01 - The Beatles - Eleanor Rigby` |

* **Final Result**: `01 - The Beatles - Eleanor Rigby.flac`

---

## 4. AI Regex & Pattern Assistant

RenameSense includes a built-in AI Assistant designed to help users generate complex regular expressions and renaming templates using plain English.

```
       User Prompt: "Extract release year inside parenthesis into prefix"
                                 │
                                 ▼
                     ┌───────────────────────┐
                     │  AI Orchestrator      │
                     └───────────────────────┘
                                 │
         ┌───────────────────────┼───────────────────────┐
         ▼                       ▼                       ▼
  ┌─────────────┐         ┌─────────────┐         ┌─────────────┐
  │  Groq API   │         │ Gemini API  │         │ Local Rule  │
  │ (Llama-3.3) │         │ (Flash 2.5) │         │ Synthesizer │
  └─────────────┘         └─────────────┘         └─────────────┘
         │                       │                       │
         └───────────────────────┼───────────────────────┘
                                 ▼
               Verified JSON Configuration Output:
       Search: ^(.*)\s*\((\d{4})\)(.*)$   Replace: $2_$1$3
```

### Dual Provider & Local Fallback Architecture

1. **Groq Cloud Inference**:
   * Model: `llama-3.3-70b-versatile`
   * Characteristics: Extremely fast sub-500ms response time. Perfect for real-time prompt generation.
2. **Google Gemini Inference**:
   * Models: `gemini-2.5-flash`, `gemini-1.5-flash`
   * Characteristics: Deep reasoning for multi-step pattern extraction and token formatting.
3. **Local Offline Rule Synthesizer (No Internet Required)**:
   * If you are working in an air-gapped environment or have no API key configured, RenameSense automatically engages its **deterministic rule synthesizer**.
   * It recognizes natural language intents locally, including:
     * "Replace spaces with underscores"
     * "Remove numbers from filenames"
     * "Add date prefix"
     * "Convert to lowercase / uppercase / kebab-case"
     * "Strip brackets and parentheses"

### Security & Secret Redaction Framework
* **Zero File Content Telemetry**: When communicating with AI providers, RenameSense strictly transmits your textual prompt. File paths, folder trees, document text, and image metadata are **never transmitted**.
* **Automatic Secret Scrubbing**: RenameSense includes a specialized diagnostic sanitizer. Any API key strings (e.g., `gsk_...`, `AIza...`, Bearer tokens) are automatically intercepted and redacted into `[REDACTED_API_KEY]` across all memory logs and disk journals.
* **Local In-Memory Key Management**: API keys are saved exclusively in your local machine configuration and never synchronized to any remote server.

---

## 5. Dynamic Template Engine & Tokens Reference

The RenameSense Template Engine provides safe, non-evaluating metadata substitution. Tokens can be combined with static text and format specifiers.

### Core Filesystem Tokens

| Token | Description | Format Specifier | Example Output |
|---|---|---|---|
| `{name}` | Original filename without extension | None | `Document_Draft` |
| `{cleaned}` | Resulting stem after sequential regex rules | None | `Cleaned_Document` |
| `{proposed}` | Synonym for `{cleaned}` | None | `Cleaned_Document` |
| `{ext}` | Original file extension without dot | None | `pdf` |
| `{.ext}` | Original file extension with leading dot | None | `.pdf` |
| `{parent}` | Name of the immediate parent folder | None | `Project_Alpha` |
| `{seq}` | Sequential counter (1-based index) | None | `1`, `2`, `3` |
| `{seq:02d}` | 2-digit zero-padded sequence | `:02d` | `01`, `02`, `03` |
| `{seq:03d}` | 3-digit zero-padded sequence | `:03d` | `001`, `002`, `003` |
| `{seq:04d}` | 4-digit zero-padded sequence | `:04d` | `0001`, `0002` |
| `{date}` | File modification timestamp (ISO) | None | `2026-11-12` |
| `{date:YYYY-MM-DD}` | Custom year, month, day formatting | `:YYYY-MM-DD` | `2026-11-12` |
| `{date:YYYYMMDD}` | Compact timestamp format | `:YYYYMMDD` | `20261112` |
| `{date:DD-MM-YYYY}` | European date formatting | `:DD-MM-YYYY` | `12-11-2026` |

### Audio, EXIF & Document Tokens

| Token | Category | Description | Fallback Default |
|---|---|---|---|
| `{camera}` / `{model}` | Photo EXIF | Camera model tag | `Unknown_Model` |
| `{make}` | Photo EXIF | Camera manufacturer tag | `Unknown_Make` |
| `{exif_date}` | Photo EXIF | Embedded DateTimeOriginal | `1970-01-01` |
| `{artist}` | Audio ID3 | Track artist name | `Unknown_Artist` |
| `{title}` | Audio ID3 | Track title name | `Untitled` |
| `{album}` | Audio ID3 | Album title | `Unknown_Album` |
| `{track}` | Audio ID3 | Track number (zero-padded) | `00` |
| `{genre}` | Audio ID3 | Musical genre tag | `Unknown_Genre` |
| `{author}` | PDF Meta | Document author name | `Unknown_Author` |
| `{pdf_title}` | PDF Meta | Internal document title | `Untitled` |
| `{subject}` | PDF Meta | Document subject tag | `Unknown_Subject` |

### Seamless Template Chaining
You can combine regex rules with templates using the `{cleaned}` token:
1. Run a Regex Replace rule to strip unneeded prefixes: `DSC_(\d+)` -> `$1`.
2. Apply a Template: `{parent}_{cleaned}_{date:YYYYMMDD}.{ext}`.
3. The template dynamically reads the sanitized result of step 1 and compiles the final filename.

---

## 6. Safety Engine & Atomic WAL Transactions

Batch file renaming is an inherently high-risk filesystem operation. A minor regex typo can corrupt thousands of file relationships in seconds. RenameSense prevents this through a multi-tier safety architecture.

### Two-Phase Write-Ahead Logging (WAL)
Every batch rename executes as a strict two-phase atomic transaction:
* **Phase 1 (Intent Logging)**: Before modifying any file on disk, a unique transaction record (`UUID`) is written to `%LOCALAPPDATA%\RenameSense\history\transactions.jsonl`. This record captures the absolute source path, original filename, target filename, timestamp, and SHA checksum.
* **Phase 2 (Atomic Execution)**: The engine executes renames sequentially. If an error occurs midway (e.g., an antivirus lock, read-only permission, or disk exhaustion), execution halts immediately and rolls back all changes made up to that point.

### Guaranteed 1-Click Rollback
Because transactions are committed to persistent durable storage, rollbacks work even if:
* The RenameSense desktop application was closed or restarted.
* The computer was rebooted.
* Days or weeks have passed since the rename took place.
To reverse an operation, navigate to **Audit History** and click **Undo Batch**. Original filenames are restored with 100% precision.

### Collision Detection & Case Staging
Before executing a batch, the validation engine checks for:
1. **Target Collisions**: Two different source files generating the same proposed filename.
2. **Existing Disk Overwrites**: A proposed filename matching an existing file on disk that is not part of the current rename queue.
3. **Invalid Characters**: Detects characters forbidden by Windows NTFS/ReFS: `< > : " / \ | ? *` and ASCII control characters `0x00-0x1F`.
4. **Reserved Win32 Device Names**: Blocks reserved filenames such as `CON`, `PRN`, `AUX`, `NUL`, `COM1` through `COM9`, and `LPT1` through `LPT9`.
5. **Deterministic Case Staging**: On Windows filesystems, renaming `readme.txt` to `README.TXT` will often fail or be ignored because NTFS is case-preserving but case-insensitive. RenameSense executes case-only renames through a temporary intermediate UUID staging phase (`readme.txt` -> `.rs_tmp_8f2a...` -> `README.TXT`), guaranteeing clean case updates without data loss.

---

## 7. Productivity & Workflow Features

* **Interactive Presets Manager**: Save frequently used rules (e.g., "Photo Archive 3-Digit", "Episode Standardizer", "Invoice Normalizer") to your local preset library. Load them with a single click.
* **Live Search & Status Filters**: Instantly isolate files in large batches using real-time search and status pills (`All`, `Valid`, `Changed`, `Collisions`, `Warnings`).
* **Drag-to-Reorder Queue**: Manually reorder files in the virtualized grid using drag-and-drop. The sequence token `{seq}` dynamically recalculates to match your custom ordering.
* **Directory Boundary Sandbox**: Every path operation is verified by `validate_file_in_boundary` to prevent directory traversal (`../`) attacks outside the selected target folder.
* **Diagnostics & Audit Log**: Inspect live application logs in real-time with automatic secret scrubbing and full export capability.

---

## 8. Keyboard Shortcuts Reference

| Shortcut | Action | Description |
|---|---|---|
| `F2` | Focus Path Input | Jump cursor to the active folder path input bar |
| `F5` | Refresh Queue | Re-scan current directory and recalculate previews |
| `Enter` | Scan Folder | Trigger directory scan when focused on path input |
| `Ctrl + Enter` | Execute Batch | Apply renames to all validated files |
| `Ctrl + Z` | Undo Last Batch | Roll back the most recent batch operation via WAL |
| `Ctrl + F` | Focus Filter | Jump to live queue search bar |
| `Ctrl + O` | Add Files | Open file selection dialog |
| `Ctrl + Shift + O` | Add Folder | Open folder selection dialog |
| `Ctrl + D` | Toggle Theme | Switch between Dark and Light Fluent UI modes |
| `Ctrl + ?` | Shortcuts Modal | View complete keyboard shortcuts guide |
| `Esc` | Close Modal | Dismiss open dialogs or overlays |

---

## 9. System Requirements

* **Operating System**: Windows 10 (64-bit) or Windows 11 (64-bit).
* **Architecture**: x86-64 compatible processor.
* **Runtime**: Microsoft Edge WebView2 Runtime (pre-installed on Windows 10 and 11).
* **Memory**: 4 GB RAM minimum (8 GB recommended for 50,000+ file batches).
* **Disk Space**: 180 MB free disk space for portable package (70 MB for setup installer).
* **Privileges**: Standard user account (no administrative UAC elevation required).

---

## 10. Official Downloads & Checksums

RenameSense is distributed in two official binary formats:

### Windows Setup Installer (Recommended)
* **File**: [RenameSense-3.0.0-Setup.exe](https://github.com/BeginnerAman/RenameSense/releases/download/v3.0.0/RenameSense-3.0.0-Setup.exe)
* **Size**: 60,908,099 bytes (~58.1 MB)
* **Features**: Per-user installation without UAC prompts, Start Menu and Desktop shortcuts, and Windows File Explorer context menu integration.
* **SHA-256 Checksum**: `8B477D19F7D5F1ABA1D45D398842927FCCBAA5C7E58530CE547235A4C4C3D168`

### Portable Standalone Package (Zero Installation)
* **File**: [RenameSense-3.0.0-Portable.zip](https://github.com/BeginnerAman/RenameSense/releases/download/v3.0.0/RenameSense-3.0.0-Portable.zip)
* **Size**: 83,291,207 bytes (~79.4 MB)
* **Features**: Standalone archive. Extract to any directory or USB drive and run `RenameSense.exe` directly without installation or registry modification.
* **SHA-256 Checksum**: `AF7C7CCFA93340826A09C331B80E0F8B1FC9FB09247D8C31A4A48B2C37A815AD`

---

## 11. License & Terms of Use

RenameSense is proprietary freeware created and maintained by **Aman Vishwakarma**.

* **Free for All**: Free to download and use for personal, academic, organizational, and commercial purposes at zero cost.
* **Proprietary & Closed-Source**: Reverse engineering, decompiling, disassembling, modifying, or republishing modified binaries is strictly prohibited.
* For complete terms, see the official [LICENSE](LICENSE) document.

Copyright (c) 2026 Aman Vishwakarma. All rights reserved.
