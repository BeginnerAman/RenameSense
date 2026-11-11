# RenameSense v3.0.0 - Official Windows Desktop Release

RenameSense is an enterprise-grade, high-performance batch file renamer designed for Windows 10 and Windows 11. It combines instant real-time diff previews, strict collision prevention, multi-stage regex rule pipelines, and full undo recovery backed by write-ahead transaction logging.

RenameSense is 100% free proprietary freeware for personal, creative, and commercial use. It runs entirely offline on your local machine with zero data collection and zero cloud telemetry.

---

## What is New in Version 3.0.0

### Real-Time Interactive Diff Engine
- View real-time before-and-after filename previews before any file is renamed.
- Unified Diff and Split View modes let you review exact character insertions, deletions, and replacements.
- Multi-token highlighting provides clear visibility into filename modifications.

### Multi-Stage Sequential Rule Engine
- Chain multiple search-and-replace rules in a deterministic pipeline where each rule processes the output of previous steps.
- Full Regular Expression support with capture groups ($1, $2, etc.).
- Combine token replacements with sequence numbers and system dates in a single batch pass.

### Safe Journal and Multi-Level Undo
- Atomic batch operations backed by write-ahead transaction logs (WAL).
- Instant multi-step undo restores files to their original state even after closing and reopening the application.
- Crash recovery protects your filesystem against unexpected power loss or process interruption.

### Enterprise Safety Invariants
- Pre-execution validation verifies destination path availability and access permissions before renaming starts.
- Automatic collision detection flags naming overlaps, existing target files, and illegal Windows characters.
- Non-destructive case-only renaming on case-insensitive NTFS and ReFS filesystems using two-phase temporary staging.

### Refined User Experience
- Fluent dark and light interface modes designed to match modern Windows 11 aesthetics.
- Keyboard shortcuts for rapid power-user workflows (F2 to scan, Ctrl+Enter to rename, Ctrl+Z to undo).
- Direct system log viewer accessible via Settings for quick diagnostics.

---

## Download Options

RenameSense v3.0.0 is distributed in two official formats:

### Option 1: Windows Setup Installer (Recommended)
- File Name: RenameSense-3.0.0-Setup.exe
- File Size: 74,259,974 bytes (~74.2 MB)
- Features: Automatic per-user installation, Desktop and Start Menu shortcuts, and Windows Explorer right-click shell integration.
- SHA-256 Checksum: `3EB8E830FF188A1F2A7D26BFA27F9562EA9BB9DB053615868DABED716A600137`

### Option 2: Portable Package (No Installation Required)
- File Name: RenameSense-3.0.0-Portable.zip
- File Size: 111,594,747 bytes (~106.4 MB)
- Features: Standalone archive. Extract anywhere (including USB flash drives or portable media) and run RenameSense.exe directly without system installation or administrator rights.
- SHA-256 Checksum: `4D8E0F2E28EEF40E2361455DAE338DB14BE67BC9ADE4E79027C5D690E309D226`

---

## System Requirements
- Operating System: Windows 10 (64-bit) or Windows 11 (64-bit)
- Processor: x86-64 compatible processor
- Memory: 4 GB RAM minimum (8 GB recommended for batches exceeding 50,000 files)
- Storage: 250 MB available disk space for portable extraction (150 MB for installer)
- Network: No internet connection required (100% offline application)

---

## Terms of Use
RenameSense is provided free of charge for personal and commercial use under the RenameSense Freeware End User License Agreement. It is proprietary software: reverse engineering, decompilation, and unauthorized redistribution of modified packages are prohibited. Copyright (c) 2026 Aman Vishwakarma. All rights reserved.
