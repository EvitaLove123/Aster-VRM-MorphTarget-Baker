# Aster-VRM-MorphTarget-Baker

Android-first, browser-side VRM morph-target inspection and vertex-sculpting prototype.

## Current features
- VRM input: VRM 0.x / VRM 1.0 via `@pixiv/three-vrm`
- 3D preview with touch rotation and zoom
- Existing morph-target search, weight sliders, selection, and preview bake
- Create a new morph target by sculpting mesh vertices directly in the 3D preview
- Brush radius and strength controls
- Sculpted deltas are stored as a new relative position morph target on the touched mesh
- Browser-side processing; model bytes are not uploaded
- No GLB export and no GLB disguised as VRM

## Important limitations
This is an early creator prototype. Newly sculpted morph targets exist in the loaded model's in-memory Three.js scene only. **VRM binary export is not implemented yet**, so the Download VRM button remains disabled. Reloading or closing the page discards newly created targets. The current sculpt brush pushes vertices along the hit surface normal; it is not yet a full Blender-style brush system and does not include symmetry, smoothing, masking, or undo for individual sculpt strokes.

The existing Bake buttons are preview-stage operations. They do not yet remove baked morph channels or remap VRM expression binds in the original GLB/VRM document. Do not use this prototype as a production VRM exporter.

Large VRM files can still exceed available Android RAM. Parsing and texture decoding happen in the browser main thread; practical capacity depends on available memory, GPU, mesh complexity, and texture sizes.

## Run with GitHub Pages
1. Open repository Settings → Pages.
2. Choose Deploy from a branch.
3. Select `main` and `/(root)`.
4. Open the published page in Chrome on Android.

Internet is required for CDN libraries. The VRM file itself is processed locally in the browser.

## Libraries
- Three.js
- `@pixiv/three-vrm`


## Normal / Form B State Switcher
- Normal ON and Form B ON preset buttons
- Transition slider interpolates morph weights between the two presets
- Assign selected morph targets to Normal or Form B using the current slider weights
- Per-mesh visibility presets for each form (for example, hide legs in Form B and hide tail in Normal)
- State assignments are session-only in this prototype; they are not saved into the VRM file
- Mesh visibility changes switch at the midpoint of the transition; visibility itself cannot be smoothly interpolated
- A real alternate-form transformation requires the VRM to contain a tail mesh and suitable morph targets, or the user to create them with the sculpting tool. The switcher does not generate a tail mesh automatically


## Generic Two-Form Setup
- Added an **Auto-detect body meshes** helper.
- It checks mesh names for common leg terms (leg, thigh, calf, foot, shoe, etc.) and tail/fin terms (tail, fin, fluke, alternate-form).
- Recognized leg meshes are set visible in Normal and hidden in Form B; recognized tail/fin meshes are set hidden in Normal and visible in Form B.
- Unmatched meshes remain unchanged; ambiguous names are skipped. Review the per-mesh visibility list after auto-mapping.
- This helper only configures visibility. The VRM must already contain the tail/fin mesh; it does not create new geometry or export a modified VRM.
