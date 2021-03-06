# 3.6.7

## Editor

### Bugfixes

* `smoothDownscaling` option now works propertly again for both the editor and stickers

# 3.6.6

## Editor

### Bugfixes

* Fix force crop / force controls

# 3.6.5

## Editor

### Bugfixes

* Fix SVG filters in combination with `<base>` tags

# 3.6.4

## Editor

### Bugfixes

* Fix rotation not being applied when cropping the whole image

# 3.6.2

## Editor

### Bugfixes

* Fix text height calculation in Firefox < 45.0

# 3.6.1

## Editor

### Features

* New frames feature replaces the old border feature
* We got rid of the "apply" button - instead, we introduced "Default" options for all controls
* Only one focus operation is allowed at a time, so we updated the focus controls
* Font list is now scrollable
* Google Fonts are preloaded correctly, making sure the font previews are rendered correctly
* Displaying a warning when font loading fails
* Don't reload fonts every time the text controls are opened

### Bugfixes

* Crop ratios are now grouped correctly
* Fix crop assets preloading
* Fix text height calculation
* Rotating a crop with fixed pixel values does no longer flip the crop

## SDK

### Bugfixes

* Fix crop with pixel values
* Fix export of transparent images, un-premultiply alpha
* Fix gamma rendering in combination with brightness and contrast

# 3.6.0

## Editor

:rotating_light: **Please note:** From this version on, you will need an API key to use PhotoEditorSDK
for HTML5. Please [log in to your account](https://www.photoeditorsdk.com) to obtain an API key and
specify it using the `apiKey` option.

### Features

* Implement licensing check and `apiKey` option

### Bugfixes

* Fix filter history / undo
* Fix text height calculation (now uses DOM element measuring when available)
* Fix crop and rotation compensation for sprites
* Fix very small brushes
* Fix splash screen assets being preloaded incorrectly

## Engine

### Bugfixes

* Fix a bug that caused Quads to be disposed incorrectly

## SDK

### Bugfixes

* Fix selective blur feature in combination with other texture units
* Fix selective blur for canvas

# 3.5.3

* Removed React and ReactDOM dependencies from source code, they now need to be installed manually.

# 3.5.2

## Editor

### Features

* Add an optional `Selective Blur` feature that allows users to blur parts of the image using a
  brush. Can be enabled using `editor: { tools: ['selective-blur'] }`.
* Add an optional `Gamma correction` feature under `Adjustments`. Can be enabled using
  `editor: { tools: ['gamma'] }`.
* Due to changes to our feature set, our serialization schema has been updated to version `1.0.1`.
  The new `schema.json` can be found [here](http://static.photoeditorsdk.com/serialization/schema-1.0.1.json).
* Decrease brush step, making large brushes look smoother
* Add output dimensions to crop control
* Allow `dimensions` option for crop ratios, causing the resulting image to be exactly of the given
  dimensions (Needs to be a `PhotoEditorSDK.Math.Vector2`)
* Add a preloader (can be disabled using the `editor.preloader` option)

### Bugfixes

* Fix crop rotation deserialization issues
* Fix `smoothUpscaling` option for intermittent render textures
* Fix knob dragging of linear focus controls

## SDK

### Features

* Add `dimensions` option (of type `PhotoEditorSDK.Math.Vector2) to `CropOperation`
* Add `gamma` option to `AdjustmentsOperation`

### Bugfixes

* Fix SDK disposal (`PhotoEditorSDK#dispose` now correctly disposes all textures and shaders)

## Engine

### Bugfixes

* Only use `highp` shader precision when it's available


# 3.5.1

This version of PhotoEditorSDK for HTML5 contains a *lot* of memory management improvements, fixing
a lot of exporting issues and slowdowns on slower / older devices.

## Editor

### Features

* Implement Google Fonts support
* Add `editor.smoothUpscaling` option (default: `false`)

### Bugfixes

* Fix brush texture dimensions while drawing
* Fix brush size when entering tool after zooming in
* Fix webcam button on photo roll screen
* Fix text cropping
* Fix crop ratio remember function
* Fix rounding issues causing textures to be re-initialized
* Fix text selection bug when zoom is larger than 100%
* FilterOperation was not removed when Original Filter was selected
* Fix a bug that caused brushes to disappear after clicking the canvas on retina devices
* Fix brush thickness after crop
* Don't show drag cursor on canvas if image is not draggable
* Correctly set texture quality on export

## SDK

### Bugfixes

* Correctly set texture quality on export
* Fix GLSL randomness function on Mobile Safari
* Operation: Fix RenderTexture disposal
* WebGLFilterManager: Fix RenderTexture disposal
* Shader: Correctly dispose vertex and fragment shaders
* LookupTableFilter: Fix texture disposal
* Dispose render textures before exporting
* Fix PrimitivesStack (Filter) disposal
* Disable operation cache during export, free memory after rendering operation
* Fix SpriteOperation leaking textures

### Features

* Add `editor.smoothUpscaling` option (default: `false`)

### Improvements

* Re-use path canvases

## Engine

### Features

* Automatically add float precision to shaders, depending on platform

# 3.5.0

Breaking changes are tagged with :rotating_light:

## Editor

### Features

* Editor now uses smaller textures while editing which has a **huge** impact on performance when
  using larger images
* Add `editor.forceControls` option. See [the documentation](https://www.photoeditorsdk.com/documentation/html5/editor/force-controls)   for more info.
* Add an overlay bar for text elements with delete and edit buttons (Edit button only appears on
  mobile browsers)
* Zoom now has new zoom levels, similar to Photoshop
* Sticker controls: Add `fixedRatio` option (default is `true`)
* :rotating_light: Crop controls: Renamed `additionalRatios` to `ratios`

### Improvements

* Add brush opacity back in, now behaving correctly
* Improve brush performance
* Photo roll now looks better on mobile browsers

### Bugfixes

* Stickers and texts are selected on click, not on mousedown
* Fix touch event handling on Android
* Fix a crop display bug in Internet Explorer
* Crop is now correctly repositioned when flipping the image

## SDK

### Features

* :rotating_light: All operations: All position values are now relative (0...1) instead of pixel
  values. :rotating_light:
* Add `textureQuality` option
* Add `export.fileBasename` option
* Add `export.quality` option (only works with image/jpeg mime type)

### Bugfixes

* PhotoEditorSDK no longer tries to `require('gl')` and `require('canvas')`, fixing usage in
  Meteor environments
* Fix transparent images getting a white background when filters are applied (WebGL only)

---

# 3.4.2-1

## Editor

### Bugfixes

* Fix upload and webcam icons in photo roll
* Fix `undefined` value in photo roll search input

---

# 3.4.2

## Editor

### Features

* New crop UI with smooth rotation
* Implemented serialization and deserialization

### Bugfixes

* Switch to home screen before exporting (this applies text objects that are being edited while
  clicking the export button)
* Fix brushes disappearing when cropping
* Fix unnecessary re-rendering of some components

## SDK

### Bugfixes

* Fix `#setSpriteScale`
* Operations no longer listen for other operations to update (e.g. `SpriteOperation` listening for
  `CropOperation` to change, so that sprite positions can be changed accordingly). Instead, the UI
  calls `crop`, `rotate` and `flip` on operations that need to compensate changes of other
  operations.

---

# 3.4.1

## Editor

### Bugfixes

* PhotoRoll: Fix distribution of photos across columns
* PhotoRoll: Implemented nicer scroll bars
* PhotoRoll: Fix icon dimensions on retina screens
* Fix repositioning of text objects when image is flipped
* Error messages disable the editor while they're open
* Re-added sticker options bar (flipping, take to front, remove)
* Switching back to home screen when text has been removed
* Fix texts not being deleted

---

# 3.4.0

Please note that this release changes the names of quite a few API methods and options. Please
refer to our current documentation in case you experience any issues with this release.

## Editor

### Features

* New Photo Roll feature that lets your users pick from a variety of photos
* Implemented new splash screen
* Added `showHeader` option
* Added `showTopBar` option
* Added thickness presets for brushes
* Implemented `ReactUI#export` to manually trigger export
* Implemented `ReactUI#setImage` to change the image that's currently being edited
* Color pickers close automatically when clicking outside of a picker
* New text elements automatically clear their contents when edited for the first time (removing
  the default placeholder)
* Re-structured options hash
* EXIF orientation is now handled by a separate `ExifOrientationOperation` so that it doesn't
  interfere with the `OrientationOperation`
* Make K1, K2, K6 and KDynamic filters available via the UI again
* Developers are now allowed to override single localization strings
* Refactored all controls, allowing controls to have their own top-bar controls

### Bugfixes

* Fixed a retina issue that caused the editor to export images with extremely large dimensions
* Fixed default font selection for text tool
* Fixed file picker not working when selecting the same file twice
* Fixed editor in IE9
* Add sub header for webcam screen back in

## Backend

### Features

* Added Clarity, Exposure, Shadows and Highlights to adjustments
* Added `LUTFilter` which uses the same filter technology we use in iOS and Android
* Brushes are now part of SpriteOperation, allowing other sprites to be layered on top of brushes
* Brushes can now have a hardness (a value between 0 (blurry) to 1 (hard))
* Reworked brush drawing, allowing to draw brush images other than circles
* Added context creation error reporting
* Added WebGL framebuffer error reporting
* Added a `smoothDownscaling` option that will enable mip-mapping in WebGL and a smooth resizing
  algorithm in Canvas2D
* Implemented `setSpriteScale` which allows the developer to export images at a specific scale.
  The sprite scale is incorporated in export while zoom level is not.
* Many refactorings, e.g. introducing `Constants.OPTION_TYPE`, `Constants.UNIFORM_TYPE` and
  `Constants.RENDERER_TYPE` objects for cleaner code.

### Bugfixes

* Fixed memory leaks in all operations
* Fixed textures of images where `width` and `height` properties have been changed
* Fixed retina performance issues
