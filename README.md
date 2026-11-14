# Aster-VRM-MorphTarget-Baker

A mobile-friendly, browser-side VRM morph-target inspection and baking workspace.

## Scope
- VRM input (VRM 0.x / VRM 1.0 through the three-vrm loader)
- 3D preview and morph-target search/list
- Large VRM Mode for files 100 MB and above (reduced preview resolution, lower resolution while dragging, and paged morph-target list of 40 entries)
- Releases old preview resources when replacing a loaded model
- Per-target weight preview
- Selected Bake and Batch Bake (in-memory preview stage)
- VRM-only project: no GLB export or GLB download

## Current prototype status
The current build loads VRM files, previews morph weights, and applies selected morph deltas to the live base position attributes. Large VRM Mode is a best-effort mobile optimization, not a guaranteed file-size limit. It reduces GPU load during preview and avoids rendering hundreds of morph-target controls at once. The GLTF/VRM parsing and texture decoding still happen in the browser main thread in this prototype, so a large or complex file may temporarily freeze the page: actual load capacity depends on available Android RAM, GPU memory, mesh complexity, and texture sizes. The browser still needs memory for the source file and decoded model data. This is currently a **preview-stage bake only**: it does not yet remove baked morph channels or remap VRM expression binds in the original glTF document. A VRM-preserving binary writer is not yet implemented, so Download VRM is intentionally disabled rather than generating an invalid file or disguising GLB as VRM.

## Run
Enable GitHub Pages from **Settings → Pages → Deploy from a branch → main → / (root)**, then open the published page in Chrome. Internet is required for CDN libraries; model bytes are processed locally in the browser.

## Libraries
- Three.js
- @pixiv/three-vrm
