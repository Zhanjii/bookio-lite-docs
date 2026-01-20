---
layout: default
title: BOOK.IO Lite Documentation
---

# BOOK.IO Lite

After Effects automation tool for creating book covers and media assets.

**Current Version:** 6.0.3

## Documentation

- [Changelog](CHANGELOG.md) - Version history and release notes
- [README](README.md) - Installation and getting started
- [Architecture](ARCHITECTURE.md) - System design and module organization
- [Namespace Reference](NAMESPACE.md) - BOOKIO namespace API reference
- [Quick Reference](QUICK_REFERENCE.md) - Common operations cheat sheet
- [Migration Guide](MIGRATION_GUIDE.md) - Updating code for new namespace

## Features

### Book Covers Tab
- Automated book cover creation with customizable settings
- E-book type selection and scaling controls
- Title/Author positioning and sizing
- Shadow and sticker controls
- Color correction plugin toggle

### Socials Tab
- GIF generation for social media
- Book cover banners
- Banner creation tools

### Effects Tab
- Title inversion effects
- Banner controls
- Cover cropping tools

### Mint & Print Tab
- Print-ready output generation
- Case and jacket functions

### System Features
- **Dockable Panel** - Dock alongside native After Effects panels
- **JSON Configuration** - Dynamic settings via ae_bridge.json
- **Lazy Loading** - Fast startup with on-demand tab loading
- **BOOKIO Namespace** - Organized utility functions

## Quick Start

### Dockable Panel Installation (Recommended)
1. Copy `BOOK.io_Lite_Modular` folder to After Effects `ScriptUI Panels` folder:
   - **Windows:** `C:\Program Files\Adobe\Adobe After Effects [version]\Support Files\Scripts\ScriptUI Panels\`
   - **Mac:** `/Applications/Adobe After Effects [version]/Scripts/ScriptUI Panels/`
2. Restart After Effects
3. Launch from `Window > BOOK.IO_Lite_v6.0.3.jsx`
4. Dock the panel anywhere in your workspace

### Floating Palette Installation
1. Copy folder to After Effects `Scripts` folder
2. Launch from `File > Scripts > BOOK.IO_Lite_v6.0.3.jsx`

## Requirements

- Adobe After Effects CS6 or later
- `ae_bridge.json` configuration file (required)

## About

Developed by Zhanji | Contact: nocturnalsession@gmail.com

(c) 2025-2026 Book.io. All rights reserved.
