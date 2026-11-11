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

## Download and Installation

1. Download RenameSense-3.0.0-Setup.exe from the Assets section below.
2. Run the installer and follow the on-screen setup instructions.
3. Launch RenameSense from your Start Menu or Desktop shortcut.

### System Requirements
- Operating System: Windows 10 (64-bit) or Windows 11 (64-bit)
- Processor: x86-64 compatible processor
- Memory: 4 GB RAM minimum (8 GB recommended for batches exceeding 50,000 files)
- Storage: 150 MB available disk space
- Network: No internet connection required (100% offline application)

---

## File Verification and Checksum

- File Name: RenameSense-3.0.0-Setup.exe
- File Size: 74,259,974 bytes (~74.2 MB)
- Architecture: x86-64 (Windows 64-bit)
- SHA-256 Checksum: `3EB8E830FF188A1F2A7D26BFA27F9562EA9BB9DB053615868DABED716A600137`

---

## Terms of Use
RenameSense is provided free of charge for personal and commercial use under the RenameSense Freeware End User License Agreement. It is proprietary software: reverse engineering, decompilation, and unauthorized redistribution of modified packages are prohibited. Copyright (c) 2026 Aman Vishwakarma. All rights reserved.
