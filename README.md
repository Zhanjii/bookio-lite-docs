# BOOK.IO Lite

A comprehensive Adobe After Effects automation tool for creating professional book covers, social media assets, and special effects.

## Overview

BOOK.IO Lite is a modular ExtendScript plugin for Adobe After Effects that simplifies and automates the creation of book covers and related media assets. The plugin features a user-friendly tabbed interface with dedicated tools for book covers, social media content, and special effects.

## Features

### Book Covers Tab
- Create book covers with configurable layouts and styles
- Control title, author, and copy text positioning
- Adjust shadow effects and opacity
- Manage sticker placement and labels
- Configure color schemes for text and backgrounds
- Toggle between title-only and title+author block modes
- Render single frames or sequences

### Socials Tab
- Create animated GIFs from image sequences
- Generate 3-book cover banners for marketing materials
- Build custom banner assets with automated slicing tools

### Effects Tab
- Invert title elements with customizable colors
- Add promotional banners with text controls
- Crop covers to different aspect ratios
- Toggle DS tags visibility

## Installation

BOOK.IO Lite supports two installation methods: as a dockable panel (recommended) or as a floating script.

### Option A: Dockable Panel Installation (Recommended)

This allows the script to dock alongside native After Effects panels like Timeline, Project, and Effects.

1. **Download**: Clone or download this repository
2. **Copy to ScriptUI Panels folder**:
   - **Windows**: `C:\Program Files\Adobe\Adobe After Effects [version]\Support Files\Scripts\ScriptUI Panels\`
   - **Mac**: `/Applications/Adobe After Effects [version]/Scripts/ScriptUI Panels/`
3. **Restart After Effects**
4. **Launch**: Go to `Window > BOOK.IO_Lite_v6.0.3.jsx`
5. **Dock**: Drag the panel to dock it alongside other panels

**Tip for Developers**: Create a symbolic link instead of copying to keep the script synchronized:
- **Windows (Run as Admin)**: `mklink /D "[AE ScriptUI Panels path]\BOOK.io_Lite_Modular" "[your development path]"`
- **Mac**: `ln -s "[your development path]" "[AE ScriptUI Panels path]/BOOK.io_Lite_Modular"`

### Option B: Floating Palette Installation

1. **Download**: Clone or download this repository
2. **Copy to Scripts folder**:
   - **Windows**: `C:\Program Files\Adobe\Adobe After Effects [version]\Support Files\Scripts\`
   - **Mac**: `/Applications/Adobe After Effects [version]/Scripts/`
3. **Launch**: In After Effects, go to `File > Scripts > BOOK.IO_Lite_v6.0.3.jsx`

## Requirements

- Adobe After Effects CC 2018 or newer
- Basic understanding of After Effects composition structure

## Usage

### Getting Started

1. Launch the script:
   - **Dockable panel**: Go to `Window > BOOK.IO_Lite_v6.0.3.jsx`
   - **Floating palette**: Go to `File > Scripts > BOOK.IO_Lite_v6.0.3.jsx`
2. Use the tabbed interface to access different functionality groups
3. Configure your project settings in the INPUT/OUTPUT panel
4. Make creative adjustments using the provided controls
5. Click the START button to generate your assets

### Creating a Basic Book Cover

1. Set the input path to your image sequence folder
2. Select your desired E-Book Type
3. Configure title positions and sizes
4. Adjust shadow and color settings
5. Click START to create your book cover

### Rendering Options

- Use the START button to create a new composition with your settings
- Use the RENDER SINGLE FRAMES button to export specific frames
- Configure output paths for your renders in the Settings panel

## Project Structure

The script follows a modular architecture for maintainability:

```
BOOK.IO_Lite_v6.0.3.jsx        # Main script file
ModularScripts/                # Folder containing all modules
├── 00UT/                     # Utility functions and helpers
│   ├── 00UT_00_bootstrap.jsx  # BOOKIO namespace initialization
│   ├── 00UT_01_utils/         # Core utility modules
│   ├── 00UT_02_info_panel/    # Information and logging UI
│   ├── 00UT_03_error_handler  # Logging system
│   ├── 00UT_04_json_bridge    # JSON data bridge
│   └── 00UT_05_json_ui_updater# JSON UI updates
├── 00CF/                     # Configuration settings
│   ├── 00CF_01_config.jsx    # Main configuration
│   ├── 00CF_02_media_config  # Media type configuration
│   └── 00CF_03_layer_constants# Layer name constants
├── 01BC/                     # Book Covers tab modules
├── 02SC/                     # Socials tab modules
├── 03EF/                     # Effects tab modules
└── 04MP/                     # Marketing/Print modules
UI_assets/                     # Images for the user interface
```

## Namespace Structure

Since version 6.0.3, BOOK.IO Lite uses a organized namespace structure to avoid global scope pollution:

```javascript
$.global.BOOKIO
├── finder          // Finding compositions, layers, folders
├── color           // Color conversion and application
├── layer           // Layer property manipulation
├── layout          // Positioning and aspect ratios
├── project         // Project organization utilities
├── render          // Render queue and export utilities
├── json            // JSON Bridge operations
├── log             // Logging and error handling
├── config          // Configuration management
└── utils           // General utility functions
```

See NAMESPACE.md for complete API documentation and usage examples.

## File Naming Convention

Modular scripts follow this naming pattern:
```
[section_code]_[container_number]_[function_name].jsx
```

### Section Codes:
- **00UT**: Utility functions (bootstrap, utils, error handling, JSON bridge)
- **00CF**: Configuration (project settings, layer constants, media config)
- **01BC**: Book Covers tab (all book cover controls)
- **02SC**: Socials tab (GIF, banner creation)
- **03EF**: Effects tab (title inversion, banners, cropping)
- **04MP**: Marketing/Print (case and jacket functions)

## Developer Notes

- The script uses the ExtendScript JSX format compatible with Adobe After Effects (ES3 syntax)
- All functions are exported to both `$.global` (for backward compatibility) and `$.global.BOOKIO` namespace
- Bootstrap file (`00UT_00_bootstrap.jsx`) must be loaded first to initialize the namespace
- Most UI controls trigger corresponding updates in After Effects compositions
- Error handling is implemented throughout for production reliability
- All code follows ExtendScript JSX guidelines in CLAUDE.md

## Contributing

Contributions to improve BOOK.IO Lite are welcome. Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Make your changes following the established naming conventions
4. Commit your changes (`git commit -m 'Add some amazing feature'`)
5. Push to the branch (`git push origin feature/amazing-feature`)
6. Open a Pull Request

Please refer to CLAUDE.md for ExtendScript JSX coding guidelines.

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Support

For support, please contact the author at nocturnalsession@gmail.com or open an issue on GitHub.

## Acknowledgements

- Developed by Zhanji (nocturnalsession@gmail.com)
- Version 6.0.3
- Special thanks to BOOK.IO for their support and guidance