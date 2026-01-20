# BOOK.IO Lite v6.0.3 Quick Reference

Fast lookup guide for common tasks and namespace API

---

## Namespace Quick Access

```javascript
$.global.BOOKIO.finder       // Find compositions, layers, folders
$.global.BOOKIO.color        // Convert and apply colors
$.global.BOOKIO.layer        // Modify layer properties
$.global.BOOKIO.layout       // Control positioning and aspect ratio
$.global.BOOKIO.project      // Manage project organization
$.global.BOOKIO.render       // Set up rendering
$.global.BOOKIO.json         // Load and cache JSON data
$.global.BOOKIO.log          // Log messages and handle errors
$.global.BOOKIO.config       // Initialize configuration
$.global.BOOKIO.utils        // General utilities
$.global.BOOKIO.sanitize     // Input sanitization and validation
```

---

## Finding Things

### Find a Layer
```javascript
var layer = $.global.BOOKIO.finder.layer(comp, "Layer Name");
```

### Find a Composition
```javascript
var comp = $.global.BOOKIO.finder.composition(app.project, "Comp Name");
```

### Find or Create a Folder
```javascript
var folder = $.global.BOOKIO.finder.orCreateFolder(parentFolder, "Folder Name");
```

### Find with Multiple Names
```javascript
var layer = $.global.BOOKIO.finder.layerWithNames(comp,
    ["Title", "Title Layer", "BookTitle"]);
```

---

## Colors

### Convert Hex to RGB
```javascript
var rgb = $.global.BOOKIO.color.hexToRgb("#FF0000");
// Returns [1, 0, 0]
```

### Convert RGB to Hex
```javascript
var hex = $.global.BOOKIO.color.rgbToHex(1, 0, 0);
// Returns "#ff0000"
```

### Apply Background Color
```javascript
$.global.BOOKIO.color.applyBG(layer, "#FFFFFF");
```

### Apply Font Color
```javascript
$.global.BOOKIO.color.applyFont(layer, "#000000");
```

---

## Layer Operations

### Set Opacity
```javascript
$.global.BOOKIO.layer.setOpacity(layer, 75);
```

### Set Text
```javascript
$.global.BOOKIO.layer.setText(textLayer, "Hello World");
```

### Set Slider Value
```javascript
$.global.BOOKIO.layer.setSlider(layer, "Slider", 50);
```

### Get Slider Value
```javascript
var value = $.global.BOOKIO.layer.getSlider(layer, "Slider");
```

---

## Layout

### Set Aspect Ratio
```javascript
$.global.BOOKIO.layout.setAspectRatio(layer, 1.5);
```

### Set Blocking Opacity
```javascript
$.global.BOOKIO.layout.setBlockingOpacity(precompLayer, 50);
```

### Set Title-Safe Opacity
```javascript
$.global.BOOKIO.layout.setTitleSafeOpacity(precompLayer, 25);
```

### Set Arrows Position
```javascript
$.global.BOOKIO.layout.setArrowsY(precompLayer, 540);
```

---

## Logging

### Log Levels
```javascript
$.global.BOOKIO.log.debug("Debug message", "moduleName");
$.global.BOOKIO.log.info("Info message", "moduleName");
$.global.BOOKIO.log.warning("Warning message", "moduleName");
$.global.BOOKIO.log.error("Error message", "moduleName");
$.global.BOOKIO.log.fatal("Fatal message", "moduleName");
```

### Set Log Level
```javascript
$.global.BOOKIO.log.setLevel("DEBUG");
```

### Handle Error
```javascript
try {
    // Code that might fail
} catch (e) {
    $.global.BOOKIO.log.handleError(e);
}
```

---

## Rendering

### Filter Files
```javascript
var pngFiles = $.global.BOOKIO.render.filterFiles(fileArray, ".png");
```

### Calculate Scale
```javascript
var scale = $.global.BOOKIO.render.calculateScale(2400, 1200);
// Returns 50
```

### Setup Render Queue
```javascript
$.global.BOOKIO.render.setupQueue(comp, "/path/to/output/", settings);
```

### Import Sequence
```javascript
$.global.BOOKIO.render.importSequence(folder, "/path/to/sequence/");
```

### Add Drop Shadow
```javascript
$.global.BOOKIO.render.addDropShadow(layer, shadowSettings);
```

### Add Markers
```javascript
$.global.BOOKIO.render.addMarkers(comp, markerData);
```

---

## JSON Operations

### Load JSON
```javascript
var data = $.global.BOOKIO.json.load("/path/to/file.json");
```

### Get Status
```javascript
var status = $.global.BOOKIO.json.getStatus();
if (status.connected) {
    // Bridge is connected
}
```

### Cache Data
```javascript
$.global.BOOKIO.json.cache(jsonData, "cacheKey");
```

### Update UI
```javascript
$.global.BOOKIO.json.updateUI(jsonData, uiElements);
```

---

## Configuration

### Initialize Configuration
```javascript
var config = $.global.BOOKIO.config.initialize();
```

### Initialize Media Config
```javascript
var mediaConfig = $.global.BOOKIO.config.initializeMedia();
```

### Access Configuration
```javascript
var version = $.global.globalVersion;
var fps = $.global.fps;
var mediaTypes = $.global.mediaTypes;
var aspectRatios = $.global.aspectRatios;
```

---

## Input Sanitization

### Validate Path
```javascript
var result = $.global.BOOKIO.sanitize.validatePath(userPath);
if (!result.isValid) {
    $.global.BOOKIO.log.error("Invalid path: " + result.message);
}
```

### Normalize Path
```javascript
var normalized = $.global.BOOKIO.sanitize.normalizePath("C:\\Users\\File.txt");
// Returns "C:/Users/File.txt"
```

### Check Path Within Base
```javascript
var isAllowed = $.global.BOOKIO.sanitize.isPathWithinBase(path, baseDir);
```

### Sanitize Filename
```javascript
var safe = $.global.BOOKIO.sanitize.filename("Book/Title: Special*Edition");
// Returns "Book_Title_Special_Edition"
```

### Sanitize AE Text
```javascript
var safeText = $.global.BOOKIO.sanitize.aeText("Line 1/Line 2");
// "/" converted to line break
```

### Validate Hex Color
```javascript
var result = $.global.BOOKIO.sanitize.hexColor("#F00");
if (result.isValid) {
    var hex = "#" + result.sanitized; // "#FF0000"
}
```

### Validate Number
```javascript
var value = $.global.BOOKIO.sanitize.number(userInput, 0, 100, 50);
```

---

## Module Registry

### Check Module Loaded
```javascript
if ($.global.BOOKIO.isModuleLoaded("module_name")) {
    // Module is ready
}
```

### Get Module Registry
```javascript
var modules = $.global.BOOKIO.getModuleRegistry();
```

### Get Dependency Report
```javascript
var report = $.global.BOOKIO.getDependencyReport();
$.writeln(report);
```

---

## Constants

### Layer Names
```javascript
$.global.COMPS.BOOK_COVER       // Composition name
$.global.LAYERS.TITLE           // Layer name
$.global.PROPS.OPACITY          // Property path
$.global.EFFECTS.DROP_SHADOW    // Effect name
$.global.FOLDERS.RENDERS        // Folder name
$.global.FILES.CONFIG_JSON      // File name
$.global.LAYOUT.CENTER_X        // Position constant
$.global.COLORS.BLACK           // Color value
$.global.UI.PANEL_WIDTH         // UI constant
```

---

## Common Workflows

### Update a Composition

```javascript
var comp = $.global.BOOKIO.finder.composition(app.project, "BookCover");
if (!comp) {
    $.global.BOOKIO.log.error("Composition not found");
} else {
    var titleLayer = $.global.BOOKIO.finder.layer(comp, "Title");
    if (titleLayer) {
        $.global.BOOKIO.layer.setText(titleLayer, "New Title");
        $.global.BOOKIO.layer.setOpacity(titleLayer, 100);
        $.global.BOOKIO.log.info("Title updated");
    }
}
```

### Create Project Structure

```javascript
var rendersFolder = $.global.BOOKIO.finder.orCreateFolder(
    app.project.rootFolder,
    "Renders"
);
var imagesFolder = $.global.BOOKIO.finder.orCreateFolder(
    app.project.rootFolder,
    "Images"
);
var nextNum = $.global.BOOKIO.project.getNextCompNumber(rendersFolder);
$.global.BOOKIO.log.info("Next comp number: " + nextNum);
```

### Apply Colors

```javascript
var layer = $.global.BOOKIO.finder.layer(comp, "Title");
if (layer) {
    $.global.BOOKIO.color.applyFont(layer, "#FFFFFF");

    var bgLayer = $.global.BOOKIO.finder.layer(comp, "Background");
    $.global.BOOKIO.color.applyBG(bgLayer, "#000000");
}
```

### Setup Rendering

```javascript
var comp = $.global.BOOKIO.finder.composition(app.project, "BookCover");
if (comp) {
    $.global.BOOKIO.render.setupFolders("/path/to/output");
    $.global.BOOKIO.render.importSequence(comp, "/path/to/images/");
    $.global.BOOKIO.render.setupQueue(comp, "/path/to/output/", {});
    $.global.BOOKIO.log.info("Render queue ready");
}
```

### Error Handling

```javascript
try {
    $.global.BOOKIO.log.setLevel("DEBUG");
    var comp = $.global.BOOKIO.finder.composition(app.project, "Test");

    if (!comp) {
        throw new Error("Composition not found");
    }

    $.global.BOOKIO.log.info("Process completed successfully");

} catch (error) {
    $.global.BOOKIO.log.error("Process failed: " + error.message);
    $.global.BOOKIO.log.handleError(error);
}
```

---

## Key Files

| File | Purpose |
|------|---------|
| `00UT_00_bootstrap.jsx` | Namespace initialization |
| `00UT_03_error_handler.jsx` | Logging system |
| `00UT_01a_finder.jsx` | Finding elements |
| `00UT_01b_color.jsx` | Color operations |
| `00UT_01c_layer_props.jsx` | Layer manipulation |
| `00UT_01d_layout.jsx` | Layout controls |
| `00UT_01e_project_org.jsx` | Project organization |
| `00UT_01f_render_utils.jsx` | Render operations |
| `00UT_04_json_bridge.jsx` | JSON data handling |
| `00CF_01_config.jsx` | Main configuration |
| `00CF_02_media_config.jsx` | Media configuration |
| `00CF_03_layer_constants.jsx` | Layer constants |

---

## Troubleshooting

### "BOOKIO is undefined"
```javascript
// Solution: Bootstrap must load first
// Check: 00UT_00_bootstrap.jsx is included before other modules
```

### "Function not found"
```javascript
// Solution: Check function name in NAMESPACE.md
// Example: findLayerByName → $.global.BOOKIO.finder.layer
```

### "Layer is null"
```javascript
// Solution: Check layer name spelling
// Verify: Layer exists in composition
var layer = $.global.BOOKIO.finder.layer(comp, "ExactName");
if (!layer) {
    $.global.BOOKIO.log.error("Layer not found");
}
```

### "Color not applied"
```javascript
// Solution: Verify color format
// Use hex: "#RRGGBB" or "#RGB"
$.global.BOOKIO.color.applyFont(layer, "#000000"); // Correct
```

---

## Tips and Best Practices

1. **Always check for null** before using found layers
   ```javascript
   var layer = $.global.BOOKIO.finder.layer(comp, "Name");
   if (layer) { /* use layer */ }
   ```

2. **Use logging for debugging**
   ```javascript
   $.global.BOOKIO.log.debug("Current value: " + value);
   ```

3. **Wrap error-prone code in try/catch**
   ```javascript
   try { /* code */ } catch(e) { $.global.BOOKIO.log.handleError(e); }
   ```

4. **Access configuration before use**
   ```javascript
   var config = $.global.BOOKIO.config.initialize();
   ```

5. **Use constants for consistency**
   ```javascript
   var comp = $.global.BOOKIO.finder.composition(app.project, $.global.COMPS.BOOK_COVER);
   ```

---

## Related Documentation

- **NAMESPACE.md** - Complete API reference
- **ARCHITECTURE.md** - System design and modules
- **MIGRATION_GUIDE.md** - Updating from old function names
- **CLAUDE.md** - ExtendScript JSX coding guidelines

---

**Version:** 6.0.3
**Last Updated:** January 2026
