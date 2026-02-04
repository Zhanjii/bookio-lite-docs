# BOOK.IO Lite Namespace API Documentation

Version 6.0.3 - Complete reference for the BOOKIO namespace structure

## Table of Contents

1. [Overview](#overview)
2. [Namespace Structure](#namespace-structure)
3. [Core Modules](#core-modules)
4. [API Reference](#api-reference)
5. [Usage Examples](#usage-examples)
6. [Migration Guide](#migration-guide)

---

## Overview

The BOOKIO namespace consolidates 68+ utility functions into 11 logical categories, eliminating global scope pollution while maintaining backward compatibility. All functions are accessible via `$.global.BOOKIO.<namespace>.<function>()`.

### Initialization

The BOOKIO namespace is automatically initialized by loading `00UT_00_bootstrap.jsx` first. This file creates the namespace structure:

```javascript
// Automatically created by bootstrap
$.global.BOOKIO = {
    finder: {},
    color: {},
    layer: {},
    layout: {},
    project: {},
    render: {},
    json: {},
    log: {},
    config: {},
    utils: {},
    sanitize: {}
};
```

---

## Namespace Structure

```
$.global.BOOKIO
├── finder         (5 functions)  - Finding compositions, layers, folders
├── color          (5 functions)  - Color conversion and application
├── layer          (8 functions)  - Layer property manipulation
├── layout         (4 functions)  - Positioning and aspect ratios
├── project        (6 functions)  - Project organization utilities
├── render         (10 functions) - Render queue and export utilities
├── json           (5 functions)  - JSON Bridge operations
├── log            (10 functions) - Logging and error handling
├── config         (2 functions)  - Configuration management
├── utils          (2 functions)  - General utilities
└── sanitize       (11 functions) - Input sanitization and validation
```

---

## Core Modules

### Module Loading Order

The bootstrap file ensures modules are loaded in the correct order:

1. **00UT_00_bootstrap.jsx** - Namespace initialization (must be first)
2. **00UT_03_error_handler.jsx** - Logging (used by other modules)
3. **Core utilities** - Finder, color, layer, layout, project, render
4. **00UT_01_utils.jsx** - General utilities
5. **00UT_04_json_bridge.jsx** - JSON Bridge operations
6. **00UT_05_json_ui_updater.jsx** - JSON UI updates
7. **Configuration** - Config and media config modules
8. **Layer constants** - COMPS, LAYERS, PROPS, etc.

---

## API Reference

### BOOKIO.finder - Finding Compositions, Layers, and Folders

Functions for locating elements in the After Effects project.

#### finder.layer(composition, layerName)

Finds a layer by name in a composition.

**Parameters:**
- `composition` (CompItem) - The composition to search
- `layerName` (string) - Exact name of the layer to find

**Returns:** Layer object or null if not found

**Example:**
```javascript
var comp = app.project.activeItem;
var titleLayer = $.global.BOOKIO.finder.layer(comp, "Title");
if (titleLayer) {
    titleLayer.opacity.setValue(50);
}
```

#### finder.layerWithNames(composition, nameArray)

Finds a layer by checking multiple possible names.

**Parameters:**
- `composition` (CompItem) - The composition to search
- `nameArray` (array) - Array of possible layer names to try

**Returns:** Layer object or null if none found

**Example:**
```javascript
var layer = $.global.BOOKIO.finder.layerWithNames(comp, ["Title", "Title Layer", "BookTitle"]);
```

#### finder.composition(projectOrFolder, compositionName)

Finds a composition by name.

**Parameters:**
- `projectOrFolder` (Project or FolderItem) - Where to search
- `compositionName` (string) - Name of the composition

**Returns:** CompItem or null if not found

**Example:**
```javascript
var comp = $.global.BOOKIO.finder.composition(app.project, "BookCover");
```

#### finder.folder(projectOrFolder, folderName)

Finds a folder by name.

**Parameters:**
- `projectOrFolder` (Project or FolderItem) - Where to search
- `folderName` (string) - Name of the folder

**Returns:** FolderItem or null if not found

#### finder.orCreateFolder(parentFolder, folderName)

Finds a folder, creating it if it doesn't exist.

**Parameters:**
- `parentFolder` (FolderItem) - Parent folder to search/create in
- `folderName` (string) - Name of the folder

**Returns:** FolderItem (existing or newly created)

**Example:**
```javascript
var renderFolder = $.global.BOOKIO.finder.orCreateFolder(
    app.project.rootFolder,
    "Renders"
);
```

---

### BOOKIO.color - Color Conversion and Application

Functions for working with color values in RGB, hex, and After Effects formats.

#### color.hexToRgb(hexColor)

Converts hex color code to RGB array.

**Parameters:**
- `hexColor` (string) - Hex color code (e.g., "#FF0000")

**Returns:** Array of [R, G, B] values (0-1 range)

**Example:**
```javascript
var rgb = $.global.BOOKIO.color.hexToRgb("#FF0000");
// Returns [1, 0, 0]
```

#### color.rgbToHex(r, g, b)

Converts RGB values to hex color code.

**Parameters:**
- `r` (number) - Red value (0-1)
- `g` (number) - Green value (0-1)
- `b` (number) - Blue value (0-1)

**Returns:** String in format "#RRGGBB"

**Example:**
```javascript
var hex = $.global.BOOKIO.color.rgbToHex(1, 0, 0);
// Returns "#ff0000"
```

#### color.updateDisplay(colorControlUI, rgbArray)

Updates a ScriptUI color control with an RGB value.

**Parameters:**
- `colorControlUI` (ScriptUI element) - Color input control
- `rgbArray` (array) - [R, G, B] values (0-1 range)

#### color.applyBG(layer, hexColor)

Applies a background color to a solid layer.

**Parameters:**
- `layer` (Layer) - Solid layer to color
- `hexColor` (string) - Hex color code

**Example:**
```javascript
var bgLayer = $.global.BOOKIO.finder.layer(comp, "Background");
$.global.BOOKIO.color.applyBG(bgLayer, "#FFFFFF");
```

#### color.applyFont(textLayer, hexColor)

Applies a font color to a text layer.

**Parameters:**
- `textLayer` (Layer) - Text layer to color
- `hexColor` (string) - Hex color code

---

### BOOKIO.layer - Layer Property Manipulation

Functions for modifying layer properties and effects.

#### layer.setOpacity(layer, opacityValue)

Sets the opacity of a layer.

**Parameters:**
- `layer` (Layer) - The layer to modify
- `opacityValue` (number) - Opacity value (0-100)

**Example:**
```javascript
$.global.BOOKIO.layer.setOpacity(titleLayer, 75);
```

#### layer.setText(textLayer, textValue)

Sets the text content of a text layer.

**Parameters:**
- `textLayer` (Layer) - The text layer to modify
- `textValue` (string) - New text content

#### layer.getSlider(layer, sliderName)

Gets the current value of a slider effect.

**Parameters:**
- `layer` (Layer) - Layer containing the slider
- `sliderName` (string) - Name of the slider effect

**Returns:** Current slider value

**Example:**
```javascript
var shadowOpacity = $.global.BOOKIO.layer.getSlider(shadowLayer, "Slider");
```

#### layer.setSlider(layer, sliderName, sliderValue)

Sets a slider effect value.

**Parameters:**
- `layer` (Layer) - Layer containing the slider
- `sliderName` (string) - Name of the slider effect
- `sliderValue` (number) - New slider value

**Example:**
```javascript
$.global.BOOKIO.layer.setSlider(shadowLayer, "Slider", 50);
```

#### layer.setBookioLogo(layer, opacityValue)

Sets the opacity of the Bookio logo layer.

**Parameters:**
- `layer` (Layer) - Logo layer
- `opacityValue` (number) - Opacity (0-100)

#### layer.setStuffioLogo(layer, opacityValue)

Sets the opacity of the Stuffio logo layer.

**Parameters:**
- `layer` (Layer) - Logo layer
- `opacityValue` (number) - Opacity (0-100)

#### layer.setBookTitle(layer, titleText)

Sets the book title text.

**Parameters:**
- `layer` (Layer) - Title layer
- `titleText` (string) - Title text

#### layer.setBookTitleOpacity(layer, opacityValue)

Sets the opacity of the book title layer.

**Parameters:**
- `layer` (Layer) - Title layer
- `opacityValue` (number) - Opacity (0-100)

---

### BOOKIO.layout - Positioning and Aspect Ratio

Functions for controlling layout effects and positioning.

#### layout.setAspectRatio(layer, aspectRatioValue)

Sets the aspect ratio on a layer's effect.

**Parameters:**
- `layer` (Layer) - Layer with aspect ratio effect
- `aspectRatioValue` (number) - Aspect ratio value

**Example:**
```javascript
$.global.BOOKIO.layout.setAspectRatio(coverLayer, 1.5);
```

#### layout.setBlockingOpacity(precompLayer, opacityValue)

Sets the opacity of a blocking pre-composition.

**Parameters:**
- `precompLayer` (Layer) - Precomp layer
- `opacityValue` (number) - Opacity (0-100)

#### layout.setTitleSafeOpacity(precompLayer, opacityValue)

Sets the opacity of a title-safe area precomp.

**Parameters:**
- `precompLayer` (Layer) - Precomp layer
- `opacityValue` (number) - Opacity (0-100)

#### layout.setArrowsY(precompLayer, yPosition)

Sets the Y position of arrows/guides.

**Parameters:**
- `precompLayer` (Layer) - Precomp layer
- `yPosition` (number) - Y position value

---

### BOOKIO.project - Project Organization

Functions for managing project structure and metadata.

#### project.getIndex(projectOrFolder, itemName)

Gets the index of an item in a folder.

**Parameters:**
- `projectOrFolder` (Project or FolderItem) - Where to search
- `itemName` (string) - Item name to find

**Returns:** Item index or -1 if not found

#### project.getNextCompNumber(folder)

Gets the next available composition number in a folder.

**Parameters:**
- `folder` (FolderItem) - Folder to check

**Returns:** Next available number

#### project.getNextFolderNumber(parentFolder)

Gets the next available folder number.

**Parameters:**
- `parentFolder` (FolderItem) - Parent folder

**Returns:** Next available number

#### project.getImageWidth(imagePath)

Gets the width of an image file.

**Parameters:**
- `imagePath` (string) - Full path to image file

**Returns:** Image width in pixels

#### project.readUint16(file, offset)

Reads a 16-bit unsigned integer from a file.

**Parameters:**
- `file` (File) - File to read from
- `offset` (number) - Byte offset

**Returns:** 16-bit unsigned integer

#### project.readUint32(file, offset)

Reads a 32-bit unsigned integer from a file.

**Parameters:**
- `file` (File) - File to read from
- `offset` (number) - Byte offset

**Returns:** 32-bit unsigned integer

---

### BOOKIO.render - Rendering and Export

Functions for setting up render operations and managing render queues.

#### render.filterFiles(fileArray, fileType)

Filters an array of files by type extension.

**Parameters:**
- `fileArray` (array) - Array of file paths
- `fileType` (string) - File extension to filter (e.g., ".jpg", ".png")

**Returns:** Filtered array of matching files

**Example:**
```javascript
var pngFiles = $.global.BOOKIO.render.filterFiles(allFiles, ".png");
```

#### render.checkIfNeeded(composition, settingsObject)

Checks if a composition needs to be rendered based on settings.

**Parameters:**
- `composition` (CompItem) - Composition to check
- `settingsObject` (object) - Settings for comparison

**Returns:** Boolean indicating if render is needed

#### render.setupFolders(basePath)

Creates and organizes folder structure for rendering.

**Parameters:**
- `basePath` (string) - Base path for folder creation

**Returns:** Object with folder paths

#### render.setupQueue(composition, outputPath, settings)

Sets up the render queue for a composition.

**Parameters:**
- `composition` (CompItem) - Composition to render
- `outputPath` (string) - Output file path
- `settings` (object) - Render settings

#### render.importSequence(folder, sequencePath)

Imports an image sequence into a folder.

**Parameters:**
- `folder` (FolderItem) - Destination folder
- `sequencePath` (string) - Path to first image in sequence

#### render.calculateScale(imageWidth, targetWidth)

Calculates scale factor for resizing.

**Parameters:**
- `imageWidth` (number) - Original image width
- `targetWidth` (number) - Target width

**Returns:** Scale percentage (0-100)

**Example:**
```javascript
var scale = $.global.BOOKIO.render.calculateScale(2400, 1200);
// Returns 50
```

#### render.addDropShadow(layer, shadowSettings)

Adds a drop shadow effect to a layer.

**Parameters:**
- `layer` (Layer) - Layer to affect
- `shadowSettings` (object) - Shadow configuration

#### render.addMarkers(composition, markerData)

Adds markers to a composition.

**Parameters:**
- `composition` (CompItem) - Target composition
- `markerData` (array) - Marker definitions

#### render.addCaseMarkers(composition, caseData)

Adds case-specific markers to a composition.

**Parameters:**
- `composition` (CompItem) - Target composition
- `caseData` (object) - Case marker data

#### render.addJacketMarkers(composition, jacketData)

Adds jacket-specific markers to a composition.

**Parameters:**
- `composition` (CompItem) - Target composition
- `jacketData` (object) - Jacket marker data

---

### BOOKIO.json - JSON Bridge Operations

Functions for working with JSON data and external bridges.

#### json.load(jsonFilePath)

Loads JSON data from a file.

**Parameters:**
- `jsonFilePath` (string) - Full path to JSON file

**Returns:** Parsed JSON object or null on error

**Example:**
```javascript
var bookData = $.global.BOOKIO.json.load("/path/to/books.json");
if (bookData) {
    $.global.BOOKIO.log.info("Loaded " + bookData.length + " books");
}
```

#### json.getStatus()

Gets the current connection status of the JSON bridge.

**Returns:** Object with status information

**Example:**
```javascript
var status = $.global.BOOKIO.json.getStatus();
if (status.connected) {
    $.global.BOOKIO.log.info("Bridge is connected");
}
```

#### json.cache(jsonData, cacheKey)

Caches JSON data in memory for quick access.

**Parameters:**
- `jsonData` (object) - Data to cache
- `cacheKey` (string) - Cache key identifier

#### json.updateStatus(statusData)

Updates the JSON bridge status.

**Parameters:**
- `statusData` (object) - New status information

#### json.updateUI(jsonData, uiElements)

Updates UI elements with JSON data.

**Parameters:**
- `jsonData` (object) - Data source
- `uiElements` (object) - UI elements to update

---

### BOOKIO.log - Logging and Error Handling

Functions for logging messages and handling errors.

#### log.debug(message, moduleName)

Logs a debug-level message.

**Parameters:**
- `message` (string) - Message to log
- `moduleName` (string, optional) - Module name for context

**Example:**
```javascript
$.global.BOOKIO.log.debug("Starting render process", "renderModule");
```

#### log.info(message, moduleName)

Logs an informational message.

**Parameters:**
- `message` (string) - Message to log
- `moduleName` (string, optional) - Module name

#### log.warning(message, moduleName)

Logs a warning message.

**Parameters:**
- `message` (string) - Message to log
- `moduleName` (string, optional) - Module name

#### log.error(message, moduleName)

Logs an error message.

**Parameters:**
- `message` (string) - Message to log
- `moduleName` (string, optional) - Module name

#### log.fatal(message, moduleName)

Logs a fatal error message.

**Parameters:**
- `message` (string) - Message to log
- `moduleName` (string, optional) - Module name

#### log.setLevel(logLevel)

Sets the global logging level.

**Parameters:**
- `logLevel` (string) - Log level: "DEBUG", "INFO", "WARNING", "ERROR", "FATAL"

**Example:**
```javascript
$.global.BOOKIO.log.setLevel("DEBUG");
```

#### log.setModuleLevel(moduleName, logLevel)

Sets logging level for a specific module.

**Parameters:**
- `moduleName` (string) - Module name
- `logLevel` (string) - Log level

#### log.getLevel()

Gets the current global logging level.

**Returns:** Current log level string

#### log.loadConfig(configObject)

Loads logging configuration from an object.

**Parameters:**
- `configObject` (object) - Configuration object

#### log.handleError(errorObject)

Handles an error with logging and user notification.

**Parameters:**
- `errorObject` (Error or string) - Error to handle

---

### BOOKIO.config - Configuration Management

Functions for initializing and managing configuration.

#### config.initialize()

Initializes the main configuration.

**Returns:** Configuration object

**Example:**
```javascript
var config = $.global.BOOKIO.config.initialize();
```

#### config.initializeMedia()

Initializes media-related configuration.

**Returns:** Media configuration object

---

### BOOKIO.utils - General Utilities

General utility functions used across the project.

#### utils.initialize()

Initializes the utilities module.

**Returns:** Utilities object

#### utils.trim(string)

Removes leading and trailing whitespace from a string.

**Parameters:**
- `string` (string) - String to trim

**Returns:** Trimmed string

**Example:**
```javascript
var clean = $.global.BOOKIO.utils.trim("  Hello World  ");
// Returns "Hello World"
```

---

### BOOKIO.sanitize - Input Sanitization and Validation

Functions for validating and sanitizing user input, file paths, and text.

#### sanitize.normalizePath(path)

Normalizes a path to use forward slashes consistently.

**Parameters:**
- `path` (string) - The path to normalize

**Returns:** String with forward slashes

**Example:**
```javascript
var normalized = $.global.BOOKIO.sanitize.normalizePath("C:\\Users\\Name\\File.txt");
// Returns "C:/Users/Name/File.txt"
```

#### sanitize.validatePath(path)

Checks if a path contains potentially dangerous characters.

**Parameters:**
- `path` (string) - The path to validate

**Returns:** Object with properties:
- `isValid` (boolean) - True if path is safe
- `message` (string) - Error message if invalid
- `sanitized` (string) - Normalized safe path

**Example:**
```javascript
var result = $.global.BOOKIO.sanitize.validatePath(userPath);
if (!result.isValid) {
    $.global.BOOKIO.log.error("Invalid path: " + result.message);
} else {
    var safePath = result.sanitized;
}
```

#### sanitize.isPathWithinBase(path, baseDir)

Checks if a path is within an allowed base directory. Prevents path traversal attacks.

**Parameters:**
- `path` (string) - The path to check
- `baseDir` (string) - The allowed base directory

**Returns:** Boolean indicating if path is within baseDir

**Example:**
```javascript
var isAllowed = $.global.BOOKIO.sanitize.isPathWithinBase(
    "C:/Projects/Book1/cover.jpg",
    "C:/Projects"
);
// Returns true

var isDangerous = $.global.BOOKIO.sanitize.isPathWithinBase(
    "C:/Windows/System32/file.dll",
    "C:/Projects"
);
// Returns false
```

#### sanitize.getRelativePath(fullPath, baseDir)

Extracts the relative path from a base directory.

**Parameters:**
- `fullPath` (string) - The full path
- `baseDir` (string) - The base directory

**Returns:** String containing the relative path, or empty string if not within base

**Example:**
```javascript
var relative = $.global.BOOKIO.sanitize.getRelativePath(
    "C:/Projects/Books/Book1/cover.jpg",
    "C:/Projects/Books"
);
// Returns "Book1/cover.jpg"
```

#### sanitize.pathExists(path)

Checks if a path exists as a file or folder.

**Parameters:**
- `path` (string) - The path to check

**Returns:** Object with properties:
- `exists` (boolean) - True if path exists
- `isFile` (boolean) - True if path is a file
- `isFolder` (boolean) - True if path is a folder

**Example:**
```javascript
var check = $.global.BOOKIO.sanitize.pathExists("C:/Projects/cover.jpg");
if (check.exists && check.isFile) {
    $.global.BOOKIO.log.info("File found");
}
```

#### sanitize.filename(name)

Sanitizes a string for use as a filename.

**Parameters:**
- `name` (string) - The string to sanitize

**Returns:** Safe filename string

**Example:**
```javascript
var safe = $.global.BOOKIO.sanitize.filename("Book/Title: Special*Edition");
// Returns "Book_Title_Special_Edition"
```

#### sanitize.aeName(name)

Sanitizes a string for use as an After Effects layer or composition name.

**Parameters:**
- `name` (string) - The string to sanitize

**Returns:** Safe name string

**Example:**
```javascript
var layerName = $.global.BOOKIO.sanitize.aeName(userInput);
layer.name = layerName;
```

#### sanitize.aeText(text)

Sanitizes text for use in After Effects text layers. Converts "/" to line breaks as per project convention.

**Parameters:**
- `text` (string) - The text to sanitize

**Returns:** Sanitized text with line breaks

**Example:**
```javascript
var safeText = $.global.BOOKIO.sanitize.aeText("First Line/Second Line");
// "/" is converted to line break
textLayer.property("Source Text").setValue(safeText);
```

#### sanitize.hexColor(hex)

Validates and sanitizes a hex color string.

**Parameters:**
- `hex` (string) - The hex color to validate (e.g., "#FF0000" or "F00")

**Returns:** Object with properties:
- `isValid` (boolean) - True if color is valid
- `sanitized` (string) - Normalized hex string (6 characters, uppercase, no #)
- `message` (string) - Error message if invalid

**Example:**
```javascript
var result = $.global.BOOKIO.sanitize.hexColor("#F00");
if (result.isValid) {
    var color = result.sanitized; // Returns "FF0000"
}
```

#### sanitize.number(value, min, max, defaultValue)

Validates and clamps a numeric value within a range.

**Parameters:**
- `value` (any) - The value to validate
- `min` (number) - Minimum allowed value
- `max` (number) - Maximum allowed value
- `defaultValue` (number) - Default value if invalid

**Returns:** Validated and clamped number

**Example:**
```javascript
var opacity = $.global.BOOKIO.sanitize.number(userInput, 0, 100, 100);
layer.opacity.setValue(opacity);
```

#### sanitize.integer(value, min, max, defaultValue)

Validates and clamps an integer value.

**Parameters:**
- `value` (any) - The value to validate
- `min` (number) - Minimum allowed value
- `max` (number) - Maximum allowed value
- `defaultValue` (number) - Default value if invalid

**Returns:** Validated integer

**Example:**
```javascript
var frameNumber = $.global.BOOKIO.sanitize.integer(userInput, 0, 999, 0);
```

---

## Usage Examples

### Example 1: Finding and Modifying a Layer

```javascript
// Find the composition
var comp = $.global.BOOKIO.finder.composition(app.project, "BookCover");
if (!comp) {
    $.global.BOOKIO.log.error("BookCover composition not found");
} else {
    // Find the title layer
    var titleLayer = $.global.BOOKIO.finder.layer(comp, "Title");
    if (titleLayer) {
        // Modify the layer
        $.global.BOOKIO.layer.setText(titleLayer, "My New Title");
        $.global.BOOKIO.layer.setOpacity(titleLayer, 100);
        $.global.BOOKIO.color.applyFont(titleLayer, "#000000");
        $.global.BOOKIO.log.info("Title updated successfully");
    }
}
```

### Example 2: Working with Folders and Organization

```javascript
// Create or find a renders folder
var rendersFolder = $.global.BOOKIO.finder.orCreateFolder(
    app.project.rootFolder,
    "Renders"
);

// Get the next composition number
var nextNum = $.global.BOOKIO.project.getNextCompNumber(rendersFolder);
$.global.BOOKIO.log.info("Next composition number: " + nextNum);
```

### Example 3: Color Operations

```javascript
// Convert colors between formats
var hexColor = "#FF6B35";
var rgbArray = $.global.BOOKIO.color.hexToRgb(hexColor);
$.global.BOOKIO.log.info("RGB: " + rgbArray[0] + ", " + rgbArray[1] + ", " + rgbArray[2]);

// Apply colors to layers
var bgLayer = $.global.BOOKIO.finder.layer(comp, "Background");
$.global.BOOKIO.color.applyBG(bgLayer, hexColor);
```

### Example 4: Logging with Levels

```javascript
// Set logging level
$.global.BOOKIO.log.setLevel("DEBUG");

// Use different log levels
$.global.BOOKIO.log.debug("Detailed debug info", "myModule");
$.global.BOOKIO.log.info("Operation started", "myModule");
$.global.BOOKIO.log.warning("Something might be wrong", "myModule");
$.global.BOOKIO.log.error("An error occurred", "myModule");

// Handle errors automatically
try {
    // Some operation that might fail
} catch (e) {
    $.global.BOOKIO.log.handleError(e);
}
```

### Example 5: JSON Bridge

```javascript
// Load book data
var bookData = $.global.BOOKIO.json.load("/path/to/books.json");

// Check connection status
var status = $.global.BOOKIO.json.getStatus();
$.global.BOOKIO.log.info("Connected: " + status.connected);

// Cache data for quick access
$.global.BOOKIO.json.cache(bookData, "books");
```

### Example 6: Input Sanitization and Validation

```javascript
// Validate and sanitize user path input
var userPath = "C:\\Projects\\Book1\\..\\..\\System32\\file.dll";
var validation = $.global.BOOKIO.sanitize.validatePath(userPath);

if (!validation.isValid) {
    $.global.BOOKIO.log.error("Invalid path: " + validation.message);
    // Output: "Invalid path: Path contains parent directory traversal (..)"
} else {
    var safePath = validation.sanitized;

    // Check if path is within allowed directory
    var baseDir = "C:/Projects";
    if ($.global.BOOKIO.sanitize.isPathWithinBase(safePath, baseDir)) {
        $.global.BOOKIO.log.info("Path is safe to use");
    } else {
        $.global.BOOKIO.log.error("Path is outside allowed directory");
    }
}

// Sanitize filename before creating file
var userInput = "Book/Title: Special*Edition?";
var safeFilename = $.global.BOOKIO.sanitize.filename(userInput);
// Returns: "Book_Title_Special_Edition"

// Sanitize text for AE text layer (converts "/" to line breaks)
var userText = "Line 1/Line 2/Line 3";
var safeText = $.global.BOOKIO.sanitize.aeText(userText);
textLayer.property("Source Text").setValue(safeText);

// Validate hex color
var userColor = "#F00";
var colorResult = $.global.BOOKIO.sanitize.hexColor(userColor);
if (colorResult.isValid) {
    var hexColor = "#" + colorResult.sanitized; // "#FF0000"
    $.global.BOOKIO.color.applyFont(titleLayer, hexColor);
}

// Validate and clamp numeric input
var userOpacity = "150"; // Out of range
var safeOpacity = $.global.BOOKIO.sanitize.number(userOpacity, 0, 100, 100);
// Returns: 100 (clamped to max)
$.global.BOOKIO.layer.setOpacity(layer, safeOpacity);
```

### Example 7: Module Registry and Dependencies

```javascript
// Check if a module is loaded before using it
if (!$.global.BOOKIO.isModuleLoaded("01BC_02_input_output_settings")) {
    $.global.BOOKIO.log.error("Required module not loaded");
} else {
    // Module is loaded and dependencies are valid
    $.global.BOOKIO.log.info("Module is ready to use");
}

// Get information about all registered modules
var modules = $.global.BOOKIO.getModuleRegistry();
for (var moduleName in modules) {
    if (modules.hasOwnProperty(moduleName)) {
        var module = modules[moduleName];
        $.global.BOOKIO.log.info(
            "Module: " + moduleName +
            " v" + module.version +
            " - Valid: " + module.dependenciesValid
        );
    }
}

// Get formatted dependency report
var report = $.global.BOOKIO.getDependencyReport();
$.writeln(report);
// Output:
// === BOOKIO Module Dependency Report ===
//
// Module: 01BC_02_input_output_settings
//   Version: 2.3.0
//   Loaded: 12/15/2025, 10:30:45 AM
//   Dependencies Valid: Yes
```

---

## Migration Guide

### From Old Global Functions to New Namespace

If you have code using the old global functions, migrate it as follows:

#### Old Style

```javascript
// Old global functions (still work but deprecated)
var layer = findLayerByName(comp, "Title");
var rgb = hexToRgb("#FF0000");
setLayerOpacity(layer, 50);
```

#### New Style

```javascript
// New namespace style (recommended)
var layer = $.global.BOOKIO.finder.layer(comp, "Title");
var rgb = $.global.BOOKIO.color.hexToRgb("#FF0000");
$.global.BOOKIO.layer.setOpacity(layer, 50);
```

### Function Name Mapping

Refer to the action plan document (`05b_namespace_restructuring.md`) for a complete table of old function names to new namespace paths.

### Backward Compatibility

All functions remain accessible through their original global names for backward compatibility. However, it is recommended to migrate to the new namespace for better code organization and to avoid future issues.

---

## Constants and Configuration

### Layer Constants

Layer names and constants are available through:

```javascript
$.global.COMPS       // Composition name constants
$.global.LAYERS      // Layer name constants
$.global.PROPS       // Property path constants
$.global.EFFECTS     // Effect name constants
$.global.FOLDERS     // Folder name constants
$.global.FILES       // File name constants
$.global.LAYOUT      // Layout position constants
$.global.COLORS      // Color value constants
$.global.UI          // UI-related constants
```

### Global Variables

Configuration data is available through:

```javascript
$.global.blockchains                // Array of enabled blockchain codes
$.global.stickers                   // Array of sticker patterns
$.global.mediaTypes                 // Array of available media types
$.global.aspectRatios               // Object mapping media types to aspect ratios
$.global.fps                        // Frames per second (30)
$.global.globalVersion              // Version string ("6.0.3")
```

---

## Performance Notes

- Function calls through the namespace have minimal performance overhead
- All functions are optimized for the After Effects environment
- Lazy loading is used where appropriate to minimize startup time
- Caching is implemented for frequently accessed operations

---

## Support and Contributing

For issues, improvements, or questions about the namespace API:

1. Check the existing documentation in the project
2. Review the individual module files for implementation details
3. See CLAUDE.md for ExtendScript JSX coding guidelines
4. Contact the development team

---

**Last Updated:** January 2026
**Version:** 6.0.3
**Maintained By:** BOOK.IO Development Team
