---
layout: default
title: Migration Guide
nav_order: 6
description: "Updating code for new namespace"
---

# BOOK.IO Lite Namespace Migration Guide

Version 6.0.3 - Updating code to use the new BOOKIO namespace

## Overview

Version 6.0.3 introduces the `$.global.BOOKIO` namespace to organize 57+ utility functions into 9 logical categories. This guide helps you migrate existing code to use the new namespace structure.

### Key Points

- Old global function names still work (backward compatible)
- New namespace approach is recommended for all new code
- Migration can be done gradually
- Performance impact is negligible
- Code organization is significantly improved

---

## Quick Reference: Function Name Mapping

### Finder Functions

| Old Name | New Name |
|----------|----------|
| `findLayerByName()` | `$.global.BOOKIO.finder.layer()` |
| `findLayerWithPossibleNames()` | `$.global.BOOKIO.finder.layerWithNames()` |
| `findCompositionByName()` | `$.global.BOOKIO.finder.composition()` |
| `findFolderByName()` | `$.global.BOOKIO.finder.folder()` |
| `findOrCreateFolder()` | `$.global.BOOKIO.finder.orCreateFolder()` |

### Color Functions

| Old Name | New Name |
|----------|----------|
| `hexToRgb()` | `$.global.BOOKIO.color.hexToRgb()` |
| `rgbToHex()` | `$.global.BOOKIO.color.rgbToHex()` |
| `updateColorDisplay()` | `$.global.BOOKIO.color.updateDisplay()` |
| `applyBGColor()` | `$.global.BOOKIO.color.applyBG()` |
| `applyFontColor()` | `$.global.BOOKIO.color.applyFont()` |

### Layer Functions

| Old Name | New Name |
|----------|----------|
| `setLayerOpacity()` | `$.global.BOOKIO.layer.setOpacity()` |
| `setLayerText()` | `$.global.BOOKIO.layer.setText()` |
| `getSliderValue()` | `$.global.BOOKIO.layer.getSlider()` |
| `setSliderValue()` | `$.global.BOOKIO.layer.setSlider()` |
| `setBookioLogoOpacity()` | `$.global.BOOKIO.layer.setBookioLogo()` |
| `setStuffioLogoOpacity()` | `$.global.BOOKIO.layer.setStuffioLogo()` |
| `setBookTitleText()` | `$.global.BOOKIO.layer.setBookTitle()` |
| `setBookTitleOpacity()` | `$.global.BOOKIO.layer.setBookTitleOpacity()` |

### Layout Functions

| Old Name | New Name |
|----------|----------|
| `setAspectRatioEffect()` | `$.global.BOOKIO.layout.setAspectRatio()` |
| `setBlockingPreCompOpacity()` | `$.global.BOOKIO.layout.setBlockingOpacity()` |
| `setTitleSafePreCompOpacity()` | `$.global.BOOKIO.layout.setTitleSafeOpacity()` |
| `setArrowsYPosition()` | `$.global.BOOKIO.layout.setArrowsY()` |

### Project Functions

| Old Name | New Name |
|----------|----------|
| `getIndex()` | `$.global.BOOKIO.project.getIndex()` |
| `getNextCompNumberInFolder()` | `$.global.BOOKIO.project.getNextCompNumber()` |
| `getNextFolderNumberInFolder()` | `$.global.BOOKIO.project.getNextFolderNumber()` |
| `getImageWidth()` | `$.global.BOOKIO.project.getImageWidth()` |
| `readUint16()` | `$.global.BOOKIO.project.readUint16()` |
| `readUint32()` | `$.global.BOOKIO.project.readUint32()` |

### Render Functions

| Old Name | New Name |
|----------|----------|
| `filterFilesByType()` | `$.global.BOOKIO.render.filterFiles()` |
| `checkIfCompositionNeeded()` | `$.global.BOOKIO.render.checkIfNeeded()` |
| `setupProjectFolders()` | `$.global.BOOKIO.render.setupFolders()` |
| `setupRenderQueue()` | `$.global.BOOKIO.render.setupQueue()` |
| `importSequence()` | `$.global.BOOKIO.render.importSequence()` |
| `calculateMediaScale()` | `$.global.BOOKIO.render.calculateScale()` |
| `addDropShadowEffect()` | `$.global.BOOKIO.render.addDropShadow()` |
| `addMarkersToComp()` | `$.global.BOOKIO.render.addMarkers()` |
| `addMarkersToCaseComp()` | `$.global.BOOKIO.render.addCaseMarkers()` |
| `addMarkersToJacketComp()` | `$.global.BOOKIO.render.addJacketMarkers()` |

### JSON Functions

| Old Name | New Name |
|----------|----------|
| `loadAEBridge()` | `$.global.BOOKIO.json.load()` |
| `getAEBridgeStatus()` | `$.global.BOOKIO.json.getStatus()` |
| `cacheJSONData()` | `$.global.BOOKIO.json.cache()` |
| `updateJSONBridgeStatus()` | `$.global.BOOKIO.json.updateStatus()` |
| `updateUIFromJSON()` | `$.global.BOOKIO.json.updateUI()` |

### Log Functions

| Old Name | New Name |
|----------|----------|
| `BOOKIO_debug()` | `$.global.BOOKIO.log.debug()` |
| `BOOKIO_info()` | `$.global.BOOKIO.log.info()` |
| `BOOKIO_warning()` | `$.global.BOOKIO.log.warning()` |
| `BOOKIO_error()` | `$.global.BOOKIO.log.error()` |
| `BOOKIO_fatal()` | `$.global.BOOKIO.log.fatal()` |
| `BOOKIO_setLogLevel()` | `$.global.BOOKIO.log.setLevel()` |
| `BOOKIO_setModuleLogLevel()` | `$.global.BOOKIO.log.setModuleLevel()` |
| `BOOKIO_getLogLevel()` | `$.global.BOOKIO.log.getLevel()` |
| `BOOKIO_loadLogConfig()` | `$.global.BOOKIO.log.loadConfig()` |
| `BOOKIO_handleError()` | `$.global.BOOKIO.log.handleError()` |

### Config Functions

| Old Name | New Name |
|----------|----------|
| `initializeConfig()` | `$.global.BOOKIO.config.initialize()` |
| `initializeMediaConfig()` | `$.global.BOOKIO.config.initializeMedia()` |

### Utility Functions

| Old Name | New Name |
|----------|----------|
| `initializeUtils()` | `$.global.BOOKIO.utils.initialize()` |
| `trimString()` | `$.global.BOOKIO.utils.trim()` |

---

## Migration Examples

### Example 1: Finding a Layer

**Before (Old Style):**
```javascript
var comp = app.project.activeItem;
var titleLayer = findLayerByName(comp, "Title");
if (titleLayer) {
    setLayerOpacity(titleLayer, 75);
}
```

**After (New Style):**
```javascript
var comp = app.project.activeItem;
var titleLayer = $.global.BOOKIO.finder.layer(comp, "Title");
if (titleLayer) {
    $.global.BOOKIO.layer.setOpacity(titleLayer, 75);
}
```

### Example 2: Color Operations

**Before (Old Style):**
```javascript
var hexColor = "#FF6B35";
var rgb = hexToRgb(hexColor);
var layer = findLayerByName(comp, "Background");
applyBGColor(layer, hexColor);
```

**After (New Style):**
```javascript
var hexColor = "#FF6B35";
var rgb = $.global.BOOKIO.color.hexToRgb(hexColor);
var layer = $.global.BOOKIO.finder.layer(comp, "Background");
$.global.BOOKIO.color.applyBG(layer, hexColor);
```

### Example 3: Error Handling and Logging

**Before (Old Style):**
```javascript
try {
    var comp = findCompositionByName(app.project, "MyComp");
    if (!comp) {
        BOOKIO_error("Composition not found");
    }
} catch (e) {
    BOOKIO_handleError(e);
}
```

**After (New Style):**
```javascript
try {
    var comp = $.global.BOOKIO.finder.composition(app.project, "MyComp");
    if (!comp) {
        $.global.BOOKIO.log.error("Composition not found");
    }
} catch (e) {
    $.global.BOOKIO.log.handleError(e);
}
```

### Example 4: Project Organization

**Before (Old Style):**
```javascript
var renderFolder = findOrCreateFolder(app.project.rootFolder, "Renders");
var nextNum = getNextCompNumberInFolder(renderFolder);
var newName = "Composition_" + nextNum;
```

**After (New Style):**
```javascript
var renderFolder = $.global.BOOKIO.finder.orCreateFolder(
    app.project.rootFolder,
    "Renders"
);
var nextNum = $.global.BOOKIO.project.getNextCompNumber(renderFolder);
var newName = "Composition_" + nextNum;
```

### Example 5: Complex Workflow

**Before (Old Style):**
```javascript
function processBookCover() {
    try {
        var comp = findCompositionByName(app.project, "BookCover");
        if (!comp) {
            BOOKIO_error("BookCover composition not found");
            return false;
        }

        var titleLayer = findLayerByName(comp, "Title");
        var authorLayer = findLayerByName(comp, "Author");

        setLayerText(titleLayer, "My Book Title");
        setLayerText(authorLayer, "John Doe");
        applyFontColor(titleLayer, "#000000");
        setLayerOpacity(authorLayer, 100);

        setupRenderQueue(comp, "/path/to/output/", {});
        BOOKIO_info("BookCover composition processed successfully");
        return true;
    } catch (e) {
        BOOKIO_handleError(e);
        return false;
    }
}
```

**After (New Style):**
```javascript
function processBookCover() {
    try {
        var comp = $.global.BOOKIO.finder.composition(app.project, "BookCover");
        if (!comp) {
            $.global.BOOKIO.log.error("BookCover composition not found");
            return false;
        }

        var titleLayer = $.global.BOOKIO.finder.layer(comp, "Title");
        var authorLayer = $.global.BOOKIO.finder.layer(comp, "Author");

        $.global.BOOKIO.layer.setText(titleLayer, "My Book Title");
        $.global.BOOKIO.layer.setText(authorLayer, "John Doe");
        $.global.BOOKIO.color.applyFont(titleLayer, "#000000");
        $.global.BOOKIO.layer.setOpacity(authorLayer, 100);

        $.global.BOOKIO.render.setupQueue(comp, "/path/to/output/", {});
        $.global.BOOKIO.log.info("BookCover composition processed successfully");
        return true;
    } catch (e) {
        $.global.BOOKIO.log.handleError(e);
        return false;
    }
}
```

---

## Migration Strategy

### Phase 1: Learn the New Namespace

1. Read this migration guide
2. Review NAMESPACE.md for complete API
3. Familiarize yourself with the 9 namespaces
4. Understand the function name changes

### Phase 2: Update Critical Paths

Start with the most frequently used functions:

1. **Finder functions** - Used everywhere
   - `findLayerByName()` → `BOOKIO.finder.layer()`
   - `findCompositionByName()` → `BOOKIO.finder.composition()`

2. **Logging functions** - For error handling
   - `BOOKIO_error()` → `BOOKIO.log.error()`
   - `BOOKIO_handleError()` → `BOOKIO.log.handleError()`

3. **Layer operations** - For UI control changes
   - `setLayerOpacity()` → `BOOKIO.layer.setOpacity()`
   - `setLayerText()` → `BOOKIO.layer.setText()`

### Phase 3: Update Supporting Code

Update functions that support critical paths:

1. **Color operations** - For visual updates
2. **Layout functions** - For positioning
3. **Project functions** - For organization

### Phase 4: Update Specialized Features

Migrate remaining functionality:

1. **Render functions** - For export operations
2. **JSON functions** - For data bridge
3. **Config functions** - For initialization

### Phase 5: Cleanup and Documentation

1. Remove old global exports (optional)
2. Update code comments to reference new namespace
3. Document any custom extensions

---

## Backward Compatibility

### Old Functions Still Work

All old global function names remain available for backward compatibility:

```javascript
// Both of these work the same
var layer1 = findLayerByName(comp, "Title");              // OLD
var layer2 = $.global.BOOKIO.finder.layer(comp, "Title"); // NEW
```

### Duration of Support

- **Current Release (6.0.3):** Full backward compatibility
- **Future Releases:** Old functions may show deprecation warnings
- **Eventually:** Old exports may be removed (with advance notice)

### Recommendation

Migrate to the new namespace at your own pace, but plan to complete migration before major version updates.

---

## Common Mistakes to Avoid

### Mistake 1: Forgetting `$.global.BOOKIO` Prefix

```javascript
// WRONG - Function not found
var layer = BOOKIO.finder.layer(comp, "Title");

// RIGHT - Correct namespace prefix
var layer = $.global.BOOKIO.finder.layer(comp, "Title");
```

### Mistake 2: Using Old Function Names with New Namespace

```javascript
// WRONG - Function doesn't exist
var layer = $.global.BOOKIO.findLayerByName(comp, "Title");

// RIGHT - New function name
var layer = $.global.BOOKIO.finder.layer(comp, "Title");
```

### Mistake 3: Missing Error Handling

```javascript
// WRONG - No error check
var layer = $.global.BOOKIO.finder.layer(comp, "Title");
$.global.BOOKIO.layer.setOpacity(layer, 50); // layer might be null

// RIGHT - Check for null
var layer = $.global.BOOKIO.finder.layer(comp, "Title");
if (layer) {
    $.global.BOOKIO.layer.setOpacity(layer, 50);
} else {
    $.global.BOOKIO.log.error("Title layer not found");
}
```

### Mistake 4: Wrong Namespace for Related Functions

```javascript
// WRONG - Using wrong namespace
var layer = $.global.BOOKIO.layer.layer(comp, "Title");

// RIGHT - Use finder for finding, layer for modifying
var layer = $.global.BOOKIO.finder.layer(comp, "Title");
$.global.BOOKIO.layer.setOpacity(layer, 50);
```

### Mistake 5: Assuming Properties Match

```javascript
// WRONG - Properties changed slightly
setSliderValue(layer, "Slider", 50);  // Old function
$.global.BOOKIO.layer.setSlider(layer, "Slider", 50); // New function - different parameter order

// RIGHT - Check NAMESPACE.md for exact signatures
$.global.BOOKIO.layer.setSlider(layer, "Slider", 50);
```

---

## Testing Your Migration

### Checklist for Each Updated File

- [ ] All old function calls replaced or removed
- [ ] All new BOOKIO.* calls use correct syntax
- [ ] Error handling in place for all utility calls
- [ ] No undefined function errors in ESTK console
- [ ] All UI controls function correctly
- [ ] Rendering pipeline works end-to-end
- [ ] No performance degradation

### Quick Validation Script

```javascript
// Add this to your file to verify namespace is available
if ($.global.BOOKIO && $.global.BOOKIO.log) {
    $.global.BOOKIO.log.info("BOOKIO namespace is properly initialized");
} else {
    alert("ERROR: BOOKIO namespace not found. Check load order.");
}
```

---

## Frequently Asked Questions

### Q: Do I have to migrate immediately?

**A:** No, old functions still work. However, plan to migrate before the next major version release.

### Q: Will the old functions be faster than the new namespace?

**A:** No, both approaches have identical performance. The namespace just provides better organization.

### Q: Can I mix old and new function calls?

**A:** Yes, you can use both in the same file during migration. However, it's cleaner to migrate completely.

### Q: What if I create a custom utility function?

**A:** Add it to an existing BOOKIO namespace (if it fits) or create a new namespace for your extensions.

### Q: How do I handle errors with the new namespace?

**A:** Use `$.global.BOOKIO.log.*()` functions for all logging and error handling.

### Q: Are there any functions that didn't migrate?

**A:** All 57+ utility functions were migrated. If you can't find one, check the complete function mapping tables above.

---

## Getting Help

### Resources

- **NAMESPACE.md** - Complete API reference with examples
- **ARCHITECTURE.md** - System design and module organization
- **CLAUDE.md** - ExtendScript JSX coding guidelines
- **Individual Module Files** - Source code documentation

### Common Issues

| Issue | Solution |
|-------|----------|
| "BOOKIO is undefined" | Ensure bootstrap loads first |
| "Function not found" | Check NAMESPACE.md for correct name |
| "Layer returns null" | Verify layer name matches composition |
| "Permission denied" | Check file paths and permissions |

---

## Summary

The new BOOKIO namespace provides:

1. **Better Organization** - 57+ functions organized into 9 categories
2. **Reduced Global Pollution** - Single namespace instead of 90+ global variables
3. **Improved Maintainability** - Related functions grouped together
4. **Backward Compatibility** - Old functions still work during transition
5. **Clear Documentation** - Complete API in NAMESPACE.md

### Next Steps

1. Review the complete mapping above
2. Start with most-used functions (finder, log)
3. Test thoroughly after each change
4. Reference NAMESPACE.md for exact function signatures
5. Refer to ARCHITECTURE.md for system design understanding

---

**Last Updated:** January 2026
**Version:** 6.0.3
**Guide Version:** 1.0
