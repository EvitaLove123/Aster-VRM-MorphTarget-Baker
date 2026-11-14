# Aster-VRM-MorphTarget-Baker

A mobile-friendly, browser-side VRM morph-target inspection and baking workspace.

## Scope
- VRM input (VRM 0.x / VRM 1.0 through the three-vrm loader)
- 3D preview and morph-target search/list
- Per-target weight preview
- Selected Bake and Batch Bake (in-memory preview stage)
- VRM-only project: no GLB export or GLB download

## Current prototype status
The current build loads VRM files, previews morph weights, and applies selected morph deltas to the live base position attributes. This is currently a **preview-stage bake only**: it does not yet remove baked morph channels or remap VRM expression binds in the original glTF document. A VRM-preserving binary writer is not yet implemented, so Download VRM is intentionally disabled rather than generating an invalid file or disguising GLB as VRM.

## Run
Enable GitHub Pages from **Settings → Pages → Deploy from a branch → main → / (root)**, then open the published page in Chrome. Internet is required for CDN libraries; model bytes are processed locally in the browser.

## Libraries
- Three.js
- @pixiv/three-vrm
