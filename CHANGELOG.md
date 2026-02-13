---
layout: default
title: Changelog
nav_order: 2
description: "Version history and release notes"
---

# Changelog

All notable changes to BOOK.IO Lite will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [6.0.5] - 2026-02-12

### Fixed
- **Crash Prevention**: Added centralized `getDropdownText()` helper — eliminates 18 crash-prone `.selection.text` patterns across 9 files
- **Infinite Recursion Guard**: Added `processedComps` tracking to `updateFileReferencesInExpressions()` to prevent circular reference loops
- **File I/O Safety**: Added `file.open()` return value checks in error handler, JSON bridge UI, log viewer, and input/output settings
- **CompItem Type Check**: Added `instanceof CompItem` guard in sticker position module

### Improved
- **Undo Support**: Added undo groups to 7 UI callback modules (title positions, sizes, scaling, side text, media type, position L/R)
- **Performance**: Cached `comp.layer(i)` in core finder and 6+ files, single-pass `findBookTitleLayer()`, extracted shared helpers
- **Dead Code Cleanup**: Removed ~400+ lines of dead code (orphaned wrappers, legacy exports, unused functions, startup test block)
- **Constants Migration**: Migrated hardcoded UI strings to `$.global.UI` and file paths to `$.global.FILES` constants
- **Module Registration**: Registered `03EF_04_ds_tag_toggle.jsx` in module loader

### Technical
- Script file renamed from `BOOK.IO_Lite_v6.0.4.jsx` to `BOOK.IO_Lite_v6.0.5.jsx`
- 50 issues fixed across 6 specialized review categories (dead code, crash bugs, performance, logic bugs, undo safety)
- Full review report archived in `action-plans/old/review-*-001.md`

## [6.0.4] - 2026-01-20

### Added
- **Dockable Panel Support**: Script can now be docked alongside native After Effects panels
  - Place in ScriptUI Panels folder and launch from Window menu
  - Backwards compatible with floating palette mode (File > Scripts)
- GitHub Pages documentation site with auto-sync workflow
- Comprehensive CHANGELOG.md for version tracking

### Changed
- Main script wrapped in IIFE to support `thisObj` Panel pattern
- Window creation now detects Panel vs Window mode automatically
- Added `layout.layout(true)` call for proper dockable panel rendering
- Conditional `show()` call - only for Window mode (Panels auto-display)

### Technical
- Script file renamed from `BOOK.IO_Lite_v6.0.2.jsx` to `BOOK.IO_Lite_v6.0.4.jsx`

## [6.0.2] - 2025-12-26

### Added
- **BOOKIO Namespace**: New organized namespace structure (`$.global.BOOKIO`)
- **JSON Bridge**: Dynamic configuration via `ae_bridge.json`
- **Modular Architecture**: 50+ modules organized by functionality
- **Lazy Loading**: Tab content loads on-demand for faster startup
- **Enhanced Logging**: Centralized logging with file output and log viewer UI

### Changed
- Complete refactor from monolithic script to modular structure
- All utility functions moved to namespace categories
- Configuration now loaded from JSON instead of hardcoded values

### Fixed
- Layout refresh for lazy-loaded tab panels
- Various bug fixes and stability improvements

## [6.0.1] - 2025-11-15

### Added
- Initial modular structure implementation
- Bootstrap system for namespace initialization
- Error handler with enhanced logging

### Changed
- Separated UI modules from processing logic
- Improved file organization with numbered prefixes

## [6.0.0] - 2025-10-01

### Added
- Major version release with new architecture
- Support for multiple media types (Book Covers, Socials, Effects, Mint & Print)
- Configurable render settings
- Color correction controls

---

## Version History Summary

| Version | Date | Highlights |
|---------|------|------------|
| 6.0.5 | 2026-02-12 | 50 bug fixes, crash prevention, undo groups, performance |
| 6.0.4 | 2026-01-20 | Dockable panel support, GitHub Pages, CHANGELOG |
| 6.0.2 | 2025-12-26 | BOOKIO namespace, JSON Bridge, modular architecture |
| 6.0.1 | 2025-11-15 | Initial modular structure |
| 6.0.0 | 2025-10-01 | Major architecture overhaul |

---

## Installation

### Dockable Panel (Recommended)
1. Copy `BOOK.io_Lite_Modular` folder to `ScriptUI Panels` folder
2. Restart After Effects
3. Launch from `Window > BOOK.IO_Lite_v6.0.5.jsx`

### Floating Palette
1. Copy `BOOK.io_Lite_Modular` folder to `Scripts` folder
2. Launch from `File > Scripts > BOOK.IO_Lite_v6.0.5.jsx`

---

**Documentation:** [GitHub Pages](https://zhanjii.github.io/bookio-lite-docs/)
**Issues:** [GitHub Issues](https://github.com/zhanjii/BOOK.io_Lite_Modular/issues)
