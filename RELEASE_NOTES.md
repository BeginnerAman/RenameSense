# RenameSense v3.0.0 - Official Windows Desktop Release

RenameSense is an enterprise-grade, high-performance batch file renamer designed for Windows 10 and Windows 11. It combines instant real-time diff previews, strict collision prevention, multi-stage regex rule pipelines, AI regex assistance, and full undo recovery backed by write-ahead transaction logging.

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

### AI Regex and Rename Assistant
- Integrated AI assistant powered by Groq (Llama-3.3-70B) and Google Gemini.
- Formulate complex regex patterns using plain English instructions (e.g., "strip bracketed resolution tags", "extract release year into prefix").
- 100% local privacy guarantee: file contents and folder paths are never transmitted or scanned.

### Interactive Presets Manager
- Save, organize, and reload custom renaming configurations with 1 click.
- Create specialized presets for photography, audio albums, video collections, and code assets.

### Live Search and Queue Filtering
- Instant search bar allows filtering by original or proposed filenames.
- Quick status pills (`All`, `Valid`, `Warnings`, `Collisions`) help identify and resolve problematic items instantly in batches exceeding 50,000 files.

### Drag-to-Reorder Sequence Engine
- Drag and drop rows in the file queue to reorder files manually before generating sequence numbering (`{seq}` or `{seq:03d}`).

### Safe Journal and Multi-Level Undo
- Atomic batch operations backed by write-ahead transaction logs (WAL).
- Instant multi-step undo restores files to their original state even after closing and reopening the application.
- Crash recovery protects your filesystem against unexpected power loss or process interruption.

### Enterprise Safety Invariants
- Pre-execution validation verifies destination path availability and access permissions before renaming starts.
- Automatic collision detection flags naming overlaps, existing target files, and illegal Windows characters.
- Non-destructive case-only renaming on case-insensitive NTFS and ReFS filesystems using two-phase temporary staging.
- Extended Win32 path support (`\\?\`) enables safe renaming of deeply nested directories beyond the 260-character limit.

### Refined User Experience
- Fluent dark and light interface modes designed to match modern Windows 11 aesthetics.
- Keyboard shortcuts HUD for rapid power-user workflows (F2 to focus path, F5 to refresh, Ctrl+Enter to rename, Ctrl+Z to undo, Ctrl+F to filter).
- In-app automatic update engine checks official releases directly without needing a browser.
- Live diagnostics viewer with automatic redaction of sensitive tokens and keys.

---

## Download Options

RenameSense v3.0.0 is distributed in two official formats:

### Option 1: Windows Setup Installer (Recommended)
- File Name: RenameSense-3.0.0-Setup.exe
- File Size: 60,908,099 bytes (~58.1 MB)
- Features: Automatic per-user installation, Desktop and Start Menu shortcuts, and Windows Explorer right-click shell integration.
- SHA-256 Checksum: `8B477D19F7D5F1ABA1D45D398842927FCCBAA5C7E58530CE547235A4C4C3D168`

### Option 2: Portable Package (No Installation Required)
- File Name: RenameSense-3.0.0-Portable.zip
- File Size: 83,291,207 bytes (~79.4 MB)
- Features: Standalone archive. Extract anywhere (including USB flash drives or portable media) and run RenameSense.exe directly without system installation or administrator rights.
- SHA-256 Checksum: `AF7C7CCFA93340826A09C331B80E0F8B1FC9FB09247D8C31A4A48B2C37A815AD`

---

## System Requirements
- Operating System: Windows 10 (64-bit) or Windows 11 (64-bit)
- Processor: x86-64 compatible processor
- Memory: 4 GB RAM minimum (8 GB recommended for batches exceeding 50,000 files)
- Storage: 180 MB available disk space for portable extraction (70 MB for installer)
- Network: No internet connection required (100% offline application)

---

## Terms of Use
RenameSense is provided free of charge for personal and commercial use under the RenameSense Freeware End User License Agreement. It is proprietary software: reverse engineering, decompilation, and unauthorized redistribution of modified packages are prohibited. Copyright (c) 2026 Aman Vishwakarma. All rights reserved.
