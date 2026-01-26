---
layout: default
title: Architecture
nav_order: 3
description: "System design and module organization"
---

# BOOK.IO Lite Architecture

Version 6.0.3 - System design, module organization, and dependency structure

## Table of Contents

1. [Overview](#overview)
2. [Module Categories](#module-categories)
3. [Load Order and Dependencies](#load-order-and-dependencies)
4. [Data Flow](#data-flow)
5. [Configuration System](#configuration-system)
6. [UI Architecture](#ui-architecture)
7. [Rendering Pipeline](#rendering-pipeline)
8. [Design Patterns](#design-patterns)

---

## Overview

BOOK.IO Lite v6.0.3 is organized as a modular ExtendScript application for Adobe After Effects. The system separates concerns into distinct modules that operate through a centralized namespace (`$.global.BOOKIO`), eliminating global scope pollution while maintaining clean separation of concerns.

### Key Design Principles

- **Modularity**: Each file has a single responsibility
- **Namespace Organization**: Functions grouped by domain (color, layer, render, etc.)
- **Configuration-Driven**: Behavior controlled through config files rather than hardcoding
- **Error Handling**: Robust logging and error management throughout
- **Extensibility**: New features can be added without modifying core modules

---

## Module Categories

### 1. Bootstrap and Initialization (00UT)

```
ModularScripts/00UT/
├── 00UT_00_bootstrap.jsx           # BOOKIO namespace initialization
├── 00UT_01_utils/                  # Core utility modules
│   ├── 00UT_01_utils.jsx          # General utilities
│   ├── 00UT_01a_finder.jsx        # Composition/layer/folder finding
│   ├── 00UT_01b_color.jsx         # Color conversion and application
│   ├── 00UT_01c_layer_props.jsx   # Layer property manipulation
│   ├── 00UT_01d_layout.jsx        # Layout and positioning
│   ├── 00UT_01e_project_org.jsx   # Project organization
│   ├── 00UT_01f_render_utils.jsx  # Render queue and export
│   └── 00UT_01h_sanitize.jsx      # Input sanitization and validation
├── 00UT_02_info_panel/             # Information and logging UI
│   ├── 00UT_02_info_panel.jsx     # Main info panel
│   ├── 00UT_02a_info_base.jsx     # Base info panel functionality
│   ├── 00UT_02b_log_viewer.jsx    # Log viewing interface
│   ├── 00UT_02c_log_settings.jsx  # Log level controls
│   ├── 00UT_02d_status_indicator.jsx # Status display
│   └── 00UT_02e_json_bridge_ui.jsx # JSON Bridge UI
├── 00UT_03_error_handler.jsx       # Logging system and error handling
├── 00UT_04_json_bridge.jsx         # JSON Bridge operations
└── 00UT_05_json_ui_updater.jsx     # JSON data to UI updates
```

**Responsibility:** Core utilities, error handling, JSON bridge, logging, and input sanitization

**Key Exports to BOOKIO Namespace:**
- `BOOKIO.finder.*` (5 functions)
- `BOOKIO.color.*` (5 functions)
- `BOOKIO.layer.*` (8 functions)
- `BOOKIO.layout.*` (4 functions)
- `BOOKIO.project.*` (6 functions)
- `BOOKIO.render.*` (10 functions)
- `BOOKIO.json.*` (5 functions)
- `BOOKIO.log.*` (10 functions)
- `BOOKIO.utils.*` (2 functions)
- `BOOKIO.sanitize.*` (11 functions)

---

### 2. Configuration and Constants (00CF)

```
ModularScripts/00CF/
├── 00CF_01_config.jsx              # Main application configuration
├── 00CF_02_media_config.jsx        # Media types and aspect ratios
└── 00CF_03_layer_constants.jsx     # Layer name and prop constants
```

**Responsibility:** Centralized configuration and layer constants

**Global Variables Set:**
- `$.global.blockchains` - Enabled blockchain codes
- `$.global.stickers` - Sticker patterns
- `$.global.mediaTypes` - Available media types
- `$.global.aspectRatios` - Aspect ratio mappings
- `$.global.fps` - Frame rate (30)
- `$.global.globalVersion` - Version (6.0.3)

**Constants Namespaces:**
- `$.global.COMPS` - Composition names
- `$.global.LAYERS` - Layer names
- `$.global.PROPS` - Property paths
- `$.global.EFFECTS` - Effect names
- `$.global.FOLDERS` - Folder names
- `$.global.FILES` - File names
- `$.global.LAYOUT` - Layout positions
- `$.global.COLORS` - Color values
- `$.global.UI` - UI constants

---

### 3. Book Covers Tab Controls (01BC)

```
ModularScripts/01BC/
├── 01_E Book Type_container/
│   ├── 01BC_01_scaling_input.jsx
│   ├── 01BC_01_title_author_block.jsx
│   ├── 01BC_01_color_correction.jsx
│   └── 01BC_01_media_type_dropdown.jsx
├── 02_Settings_container/
│   └── 01BC_02_input_output_settings.jsx
├── 03_Side Bar Text_container/
│   └── 01BC_03_side_text_logo.jsx
├── 04_Title Options_container/
│   ├── 01BC_04_position_lr.jsx
│   ├── 01BC_04_text_scaling.jsx
│   ├── 01BC_04_title_colors.jsx
│   ├── 01BC_04_title_positions.jsx
│   └── 01BC_04_title_sizes.jsx
├── 05_Shadow Opacity Stickers_container/
│   ├── 01BC_05_shadow_opacity.jsx
│   ├── 01BC_05_sticker_labels.jsx
│   └── 01BC_05_sticker_position.jsx
└── 06_Start Render_container/
    ├── 01BC_06_render_frames.jsx
    └── 01BC_06_start_button.jsx
```

**Responsibility:** User interface controls for book cover creation

**Dependencies:**
- Finder and layer utilities
- Configuration for media types
- Layout functions for positioning
- Render utilities

---

### 4. Social Media Tab Controls (02SC)

```
ModularScripts/02SC/
├── 02SC_01_gif_settings.jsx        # GIF animation controls
├── 02SC_02_book_cover_banner.jsx   # Book cover banner options
└── 02SC_03_banner_creation.jsx     # Banner generation logic
```

**Responsibility:** UI controls and logic for social media asset creation

**Key Functions:**
- GIF animation configuration
- 3-book cover banner generation
- Banner slicing and export

---

### 5. Effects Tab Controls (03EF)

```
ModularScripts/03EF/
├── 03EF_01_invert_titles.jsx       # Title inversion controls
├── 03EF_02_banner_controls.jsx     # Promotional banner controls
├── 03EF_03_crop_cover.jsx          # Cover cropping tool
└── 03EF_04_ds_tag_toggle.jsx       # DS tag visibility control
```

**Responsibility:** Special effects and advanced controls

**Key Functions:**
- Title color inversion
- Banner creation with text
- Cover cropping to aspect ratios
- DS tag management

---

### 6. Marketing and Print Controls (04MP)

```
ModularScripts/04MP/
├── 04MP_01_print_settings.jsx      # Print configuration
├── 04MP_02_print_button.jsx        # Print action button
├── 04MP_03_case_functions.jsx      # Case/box functionality
├── 04MP_03a_generic_print_handler.jsx # Generic print handler
├── 04MP_04_jacket_functions.jsx    # Jacket/sleeve functionality
└── 04MP_05_expression_utils.jsx    # Expression utilities
```

**Responsibility:** Print and marketing-specific features

**Key Functions:**
- Print settings configuration
- Case/box cover generation
- Jacket/sleeve generation
- Expression evaluation for dynamic content

---

### 7. Main Script

```
BOOK.IO_Lite_v6.0.3.jsx
```

**Responsibility:**
1. Wrap entire script in IIFE for dockable panel support
2. Load bootstrap file first
3. Include all module files
4. Detect running mode (Panel vs Window)
5. Initialize UI (dockable panel or floating palette)
6. Set up event handlers
7. Manage main application flow

**Dockable Panel Support:**
The main script uses the `thisObj` pattern to support both dockable and floating modes:
- When launched from `Window` menu (ScriptUI Panels folder): Runs as dockable panel
- When launched from `File > Scripts`: Runs as floating palette (backward compatible)

```javascript
(function(thisObj) {
    // ... script content ...

    // Panel-aware window creation
    var isPanel = (thisObj instanceof Panel);
    if (isPanel) {
        myWindow = thisObj;  // Use provided Panel object
    } else {
        myWindow = new Window("palette", "BOOK.IO Lite", ...);
    }

    // Force layout for panels
    if (myWindow && myWindow.layout) {
        myWindow.layout.layout(true);
    }

    // Only show() for Window mode (panels are shown automatically)
    if (myWindow instanceof Window) {
        myWindow.show();
    }
})(this);
```

---

## Load Order and Dependencies

### Critical Load Order

The application MUST load files in this exact order to ensure proper initialization:

1. **00UT_00_bootstrap.jsx** (MUST BE FIRST)
   - Creates `$.global.BOOKIO` namespace structure
   - No dependencies

2. **00UT_03_error_handler.jsx**
   - Logging system initialization
   - Used by all other modules
   - Dependencies: None (bootstrap only)

3. **Core Utilities (in order)**
   ```
   00UT_01a_finder.jsx        - Finding elements
   00UT_01b_color.jsx         - Color operations
   00UT_01c_layer_props.jsx   - Layer manipulation
   00UT_01d_layout.jsx        - Layout operations
   00UT_01e_project_org.jsx   - Project organization
   00UT_01f_render_utils.jsx  - Render operations
   00UT_01_utils.jsx          - General utilities
   ```
   - Each depends on logging
   - May depend on finder and color

4. **JSON Bridge**
   ```
   00UT_04_json_bridge.jsx    - JSON loading and caching
   00UT_05_json_ui_updater.jsx - JSON to UI mapping
   ```
   - Depends on logging and utilities

5. **Configuration**
   ```
   00CF_01_config.jsx         - Main configuration
   00CF_02_media_config.jsx   - Media configuration
   00CF_03_layer_constants.jsx - Layer constants
   ```
   - Depends on logging

6. **Info Panel**
   ```
   00UT_02_info_panel.jsx     - Main info panel (includes sub-modules)
   ```
   - Depends on logging and configuration

7. **UI Controls (by container)**
   ```
   01BC/* - Book Covers tab controls
   02SC/* - Socials tab controls
   03EF/* - Effects tab controls
   04MP/* - Marketing/Print controls
   ```
   - Each depends on utilities, configuration, and logging

### Dependency Graph

```
00UT_00_bootstrap (no deps)
    ↓
00UT_03_error_handler (BOOKIO.log)
    ↓
Core Utilities (00UT_01*.jsx)
    ├─→ finder (for finding elements)
    ├─→ color (for color operations)
    ├─→ layer (for layer manipulation)
    ├─→ layout (for positioning)
    ├─→ project (for project organization)
    └─→ render (for rendering)
    ↓
00UT_04_json_bridge (BOOKIO.json)
    ↓
00UT_05_json_ui_updater (BOOKIO.json.updateUI)
    ↓
00CF_01/02/03_config (BOOKIO.config)
    ↓
00UT_02_info_panel (info UI)
    ↓
01BC, 02SC, 03EF, 04MP (UI controls)
    ↓
BOOK.IO_Lite_v6.0.3.jsx (main script)
```

---

## Data Flow

### Configuration → UI → After Effects

```
Configuration Files (00CF)
    ↓
UI Module Initialization (01BC, 02SC, 03EF, 04MP)
    ↓
User Interaction (ScriptUI controls)
    ↓
Event Handlers
    ↓
Utility Functions (BOOKIO.layer.*, BOOKIO.color.*, etc.)
    ↓
After Effects Objects (compositions, layers, effects)
```

### JSON Bridge Flow

```
External JSON File
    ↓
BOOKIO.json.load()
    ↓
BOOKIO.json.cache()
    ↓
BOOKIO.json.updateUI()
    ↓
ScriptUI Update
```

### Rendering Flow

```
User Clicks "START"
    ↓
01BC_06_start_button.jsx
    ↓
Render Configuration
    ↓
BOOKIO.render.setupFolders()
    ↓
BOOKIO.render.importSequence()
    ↓
BOOKIO.render.setupQueue()
    ↓
BOOKIO.render.addMarkers()
    ↓
After Effects Render Queue
```

---

## Configuration System

### Initialization Order

1. **00CF_01_config.jsx** - Loads main configuration
   - FPS setting
   - Version information
   - Blockchain codes
   - Sticker patterns

2. **00CF_02_media_config.jsx** - Loads media configuration
   - Media types (e-book, print, etc.)
   - Aspect ratios per media type
   - Element descriptions
   - Dropdown options

3. **00CF_03_layer_constants.jsx** - Loads all constant mappings
   - Composition names
   - Layer names
   - Property paths
   - Effect names
   - Folder names
   - File names
   - Layout positions
   - Color values
   - UI constants

### Configuration Access

```javascript
// Global variables (direct access)
$.global.fps
$.global.globalVersion
$.global.blockchains[]
$.global.stickers[]
$.global.mediaTypes[]
$.global.aspectRatios{}

// Constants (namespaced)
$.global.COMPS.BOOK_COVER
$.global.LAYERS.TITLE
$.global.PROPS.OPACITY
$.global.EFFECTS.DROP_SHADOW
$.global.FOLDERS.RENDERS
$.global.FILES.CONFIG_JSON
$.global.LAYOUT.CENTER_X
$.global.COLORS.BLACK
$.global.UI.PANEL_WIDTH
```

---

## UI Architecture

### ScriptUI Panel Structure

```
Main Window (tabbed panel)
├── Book Covers Tab (01BC)
│   ├── E-Book Type Section
│   │   ├── Media type dropdown
│   │   ├── Scaling input
│   │   ├── Title/Author block toggle
│   │   └── Color correction
│   ├── Settings Section
│   │   └── Input/Output paths
│   ├── Side Bar Section
│   │   ├── Logo dropdown
│   │   └── Side text input
│   ├── Title Options Section
│   │   ├── Position controls
│   │   ├── Size controls
│   │   ├── Color controls
│   │   ├── Scaling controls
│   │   └── Text scaling
│   ├── Shadow/Stickers Section
│   │   ├── Shadow opacity
│   │   ├── Sticker labels
│   │   └── Sticker position
│   └── Render Controls
│       ├── Render frames
│       └── Start button
├── Socials Tab (02SC)
│   ├── GIF Settings
│   ├── Book Cover Banner
│   └── Banner Creation
├── Effects Tab (03EF)
│   ├── Invert Titles
│   ├── Banner Controls
│   ├── Crop Cover
│   └── DS Tag Toggle
└── Info Panel (00UT_02)
    ├── Status indicator
    ├── Log viewer
    ├── Log settings
    └── JSON Bridge UI
```

### Event Flow

```
User Action (slider, button, etc.)
    ↓
ScriptUI Event Handler
    ↓
Input Validation
    ↓
Utility Function Call (BOOKIO.*)
    ↓
After Effects Update
    ↓
UI Feedback/Status Update
```

---

## Rendering Pipeline

### Complete Render Process

1. **Input Setup** (01BC_02_input_output_settings.jsx)
   - User selects input folder
   - System detects image sequence

2. **Configuration** (01BC_04_title_options.jsx)
   - User sets title text
   - User configures colors
   - User sets positions and sizes

3. **Render Initiation** (01BC_06_start_button.jsx)
   - User clicks START
   - System creates new composition
   - System imports image sequence

4. **Effect Setup** (BOOKIO.render.*)
   - Add drop shadows
   - Apply aspect ratio effects
   - Add markers for sections

5. **Queue Setup** (BOOKIO.render.setupQueue)
   - Configure output path
   - Set render settings
   - Add to render queue

6. **Execution**
   - After Effects processes render queue
   - Files written to output folder
   - Status updated in UI

### Supported Export Formats

- PNG sequence
- JPEG sequence
- MOV video
- MP4 video

---

## Design Patterns

### 1. Module Dependency Declaration Pattern

```javascript
// Declare module dependencies at the top of each module
var MODULE_DEFINITION = {
    name: "module_name",
    version: "1.0.0",
    requires: [
        "BOOKIO.finder.composition",
        "BOOKIO.sanitize.normalizePath",
        "BOOKIO.log.info"
    ],
    optional: [
        "BOOKIO.log.debug"
    ],
    globals: [
        "blockchains",
        "mediaTypes"
    ]
};

// Register module after functions are defined
$.global.BOOKIO.registerModule(MODULE_DEFINITION);
```

### 2. Namespace Organization Pattern

```javascript
// Create namespace if not exists
if (!$.global.BOOKIO) {
    $.global.BOOKIO = {};
}

// Create sub-namespace
if (!$.global.BOOKIO.finder) {
    $.global.BOOKIO.finder = {};
}

// Export functions to namespace
$.global.BOOKIO.finder.layer = function(comp, name) {
    // Implementation
};

// Also export to global for backward compatibility
$.global.findLayerByName = $.global.BOOKIO.finder.layer;
```

### 3. Input Sanitization Pattern

```javascript
// Path validation before use
var pathValidation = $.global.BOOKIO.sanitize.validatePath(userPath);
if (!pathValidation.isValid) {
    $.global.BOOKIO.log.error("Invalid path: " + pathValidation.message);
    return;
}
var safePath = pathValidation.sanitized;

// Ensure path is within allowed directory
if (!$.global.BOOKIO.sanitize.isPathWithinBase(safePath, baseDirectory)) {
    $.global.BOOKIO.log.error("Path is outside allowed directory");
    return;
}

// Sanitize filename before creating files
var safeFilename = $.global.BOOKIO.sanitize.filename(userInput);

// Sanitize text for AE layers
var safeText = $.global.BOOKIO.sanitize.aeText(userText);
```

### 4. Error Handling Pattern

```javascript
try {
    // Operation that might fail
    var result = someOperation();
} catch (error) {
    $.global.BOOKIO.log.error("Operation failed: " + error.toString());
    $.global.BOOKIO.log.handleError(error);
    return null;
}
```

### 5. Configuration Access Pattern

```javascript
// During initialization
$.global.myModule = {
    config: null,
    init: function() {
        this.config = $.global.BOOKIO.config.initialize();
    },
    getMediaType: function() {
        return $.global.mediaTypes[0]; // Uses global config
    }
};
```

### 6. UI Update Pattern

```javascript
// In event handler
var slider = this;
var value = slider.value;

// Update After Effects
var layer = $.global.BOOKIO.finder.layer(comp, "MyLayer");
$.global.BOOKIO.layer.setOpacity(layer, value);

// Log the change
$.global.BOOKIO.log.info("Opacity changed to: " + value);

// Update UI feedback
statusText.text = "Opacity: " + value;
```

### 7. Lazy Initialization Pattern

```javascript
// Module global variable
var infoPanel = null;

// Lazy getter
function getInfoPanel() {
    if (!infoPanel) {
        infoPanel = createInfoPanel(); // Only create when needed
    }
    return infoPanel;
}
```

### 8. Module Registry and Dependency Checking Pattern

```javascript
// Check if module dependencies are loaded
if (!$.global.BOOKIO.isModuleLoaded("required_module")) {
    $.global.BOOKIO.log.error("Required module not loaded");
    return;
}

// Get module registry information
var modules = $.global.BOOKIO.getModuleRegistry();

// Get formatted dependency report
var report = $.global.BOOKIO.getDependencyReport();
$.writeln(report);
```

---

## Performance Considerations

### Optimization Strategies

1. **Namespace Lookup** - O(1) object property access
2. **Caching** - Configuration and compositions cached in memory
3. **Event Debouncing** - Slider updates throttled to avoid excess AE calls
4. **Lazy Loading** - Info panel and certain features created on demand
5. **Batch Operations** - Multiple layer changes wrapped in single undo group

### Memory Management

- Temporary objects cleaned up after use
- Compositions cached only when active
- JSON data cached to avoid repeated file reads
- UI elements created once and reused

---

## Extensibility

### Adding a New Feature

1. **Create module file** in appropriate section (01BC, 02SC, etc.)
2. **Follow naming convention**: `[SECTION]_[CONTAINER]_[NAME].jsx`
3. **Use BOOKIO namespace** for utility function calls
4. **Add configuration** to 00CF files if needed
5. **Update load order** in main script
6. **Add to tab UI** in main script
7. **Document** in this architecture file

### Adding a New Namespace

1. **Create bootstrap entry** in 00UT_00_bootstrap.jsx
2. **Create utility file** that exports to namespace
3. **Update NAMESPACE.md** with API documentation
4. **Update load order** in dependency graph
5. **Add example usage** to NAMESPACE.md

---

## Testing and Validation

### Module Testing

Each module should be tested independently:
- Bootstrap creates namespace correctly
- Each utility function works in isolation
- Configuration loads without errors
- UI controls respond correctly

### Integration Testing

- All modules load in order without errors
- Namespace functions accessible from UI modules
- Configuration properly initialized
- JSON bridge connects successfully
- Rendering pipeline completes without errors

### Validation Checklist

- [ ] No errors in ESTK console
- [ ] BOOKIO namespace created
- [ ] All configuration loaded
- [ ] UI renders correctly
- [ ] File operations work
- [ ] Rendering completes successfully

---

## Troubleshooting

### Common Issues

**Issue:** "BOOKIO is undefined"
- **Cause:** Bootstrap file not loaded first
- **Fix:** Ensure 00UT_00_bootstrap.jsx loads before all other modules

**Issue:** "Function not found in namespace"
- **Cause:** Module not loaded or function not exported
- **Fix:** Check module is included in main script

**Issue:** "Configuration not found"
- **Cause:** Config file not loaded before use
- **Fix:** Ensure 00CF files load before UI modules

**Issue:** "Layer or composition not found"
- **Cause:** After Effects project not open or wrong name
- **Fix:** Verify composition/layer names match constants

---

**Last Updated:** January 2026
**Version:** 6.0.3
**Maintained By:** BOOK.IO Development Team
