# Pixel Rig Studio

[简体中文](README.md) | English

An offline pixel drawing and animation tool for Windows. Draw frame by frame, bind character parts to 2D bones, pose them, and bake the result into editable pixel frames. The scene workspace lets you arrange backgrounds, character animations, and props into short pixel films.

Current release: **v0.4.10 Preview**, for **Windows x64**. Running the application does not require Node.js, Blender, an account, or an internet connection. Windows 10 22H2 or Windows 11 is recommended for video encoding.

**The application interface and the detailed guides bundled with v0.4.10 are in Simplified Chinese.** This README explains the workflow in English and includes key Chinese interface labels so you can find the controls.

## Download and run

**[Download v0.4.10 for Windows x64](https://github.com/ChariskQAQ/PixelRigStudio/releases/tag/v0.4.10)**

1. Download `PixelRigStudio-v0.4.10-Windows-x64.zip` from the release assets.
2. Extract the entire archive to a writable folder.
3. Run `PixelRigStudio.exe` inside that folder.
4. Keep the DLLs, `resources`, `locales`, and other accompanying files. Copying only the EXE will not work.

The main archive already includes both optional plugins and offline documentation. You do not need to download the plugins again. Separate plugin ZIPs are available on the release page for individual updates. Use `SHA256SUMS-v0.4.10.txt` to verify the main archive and plugin downloads.

This is a preview release and the executable is not code-signed. Start with an example and keep backups of important projects. If Windows displays an unknown-publisher warning, check the download source and checksum first.

This public repository distributes release packages and documentation. **The application's source code is not published here.** Older versions are available under [Releases](https://github.com/ChariskQAQ/PixelRigStudio/releases).

## What's new in 0.4.10

- **Track-based timelines:** character tracks group bone animation and layers/parts; scene objects show clips and transform keys on separate, collapsible rows. Diamonds mark keys; a horizontal span connects a linear key to the next key. Hold keys have no span. Seconds, a blue playhead, character-track zoom, and synchronized label/content scrolling make timing easier to read.
- **Unified object tree:** manage layers, groups, image parts, and bones together, with expansion, context menus, and drag-to-rebind. Layer drawing order is still maintained separately. Bones use a diamond-shaped display.
- **Adjustable workspace:** move, dock, float, and resize panels by their edges. Layouts are remembered locally and can be reset.
- **Current-frame free transform:** Ctrl+T transforms a selection or the whole visible Cel on an ordinary pixel layer. Position, scale, rotation, and shear can be entered precisely; apply is one undo step and Esc cancels. This pixel tool does not edit bound source parts.
- **Base bone-length scaling:** adjust character proportions in source-part mode and optionally stretch attached parts across the animation. Source bitmaps and existing retouched frames remain intact. Rebake to generate pixels at the new proportions; this is not per-frame bone-length animation.
- **Smaller distribution:** keep required runtime assets, Simplified Chinese/Traditional Chinese/English runtime locale files, the offline encoder, licenses, and third-party source materials. The ZIP is about 211.5 MiB; the extracted directory is about 470 MiB. Runtime locale files do not add an English application interface.
- **Updated optional plugins:** physics **1.2.5** and PMX/VMD **1.2.4**, compatible with application versions **0.4.2–0.4.10**, with API 1 unchanged. They are included but not installed or enabled by default. Replace older plugins whose compatibility range excludes this release.

Bone animation still stores whole poses; scene objects still store combined transform keys. The new rows do not introduce independent per-bone or per-property tracks, or automatically draw in-between pixel images.

Video frame extraction, PSD import, FK/IK, adjustable onion skinning, scene audio, film export, and the four stick-figure examples remain available. Validation included 188 core tests, an independently extracted executable, timeline checks at three simulated display scales, plugin restart workflows, and an actual MP4 export with audio. The full 29-group desktop suite and native multi-monitor DPI were not rerun for this release.

## Getting started

The application opens at the project home screen. Create a **Character / Sprite** project (`角色／精灵`) or a **Scene Animation** project (`场景动画`), open an existing `.pxrig` file, import a PSD, or open an example.

Returning to the home screen keeps the active project, undo history, current frame, and view. Choose **Continue Editing** (`继续编辑`) to return. Removing a recent-project entry does not delete its file from disk.

### Animate a character

1. Create a character project or open the built-in stick-figure example. For a guided first attempt, choose the **Binding and Wave Exercise** (`绑定与挥手练习`) on the home screen.
2. Put the head, torso, arms, and other parts on separate layers.
3. Create bones or a humanoid template from the **Bones** menu (`骨骼`). Select a pixel layer and choose **Layer → Bind to Bone** (`图层 → 绑定到骨骼`).
4. Switch to **Pose** mode (`摆姿势`). Use `R` to rotate bones, or select a forearm or lower leg and use `K` to drag the endpoint of a two-bone IK chain.
5. Set key poses and frame durations. Check the rhythm on the timeline; Shift-click selects a continuous frame range.
6. Bake the animation into ordinary pixel layers, then switch to **Frame Retouching** (`逐帧修整`) to clean up outlines and joints.
7. Save a `.pxrig` project or export PNG, a PNG sequence, or a sprite sheet with JSON metadata.

Bone transforms use nearest-neighbor sampling, but arbitrary-angle rotation still changes pixel outlines. **Inspect and retouch generated frames.** Baking again creates a new result group, preserves previous retouches, and hides the previous result group by default.

### Make a short pixel film

1. Create a **Scene Animation** project (`场景动画`) or open the built-in street-corner scene.
2. Import a PNG background, a PNG sequence, extracted video frames, or a selected animation tag or frame range from a character `.pxrig` project.
3. Arrange clip timing, loops, playback speed, position, rotation, scale, and opacity.
4. Animate objects and the camera with keyframes. The camera supports position and zoom.
5. Optionally import one WAV or MP3 reference audio track and adjust its start time, source range, and volume.
6. Export MP4, GIF, or a transparent PNG sequence, with integer output upscaling.

Scenes use baked animation clips. To change a clip's pixels, edit the character project and use **Update Asset** (`更新素材`) to reimport it. Moving an object in the scene does not drive the character's already-baked accessory physics again.

The default scene is 320×180 at 12 fps for 10 seconds. The logical canvas is limited to 512×512, with 6, 8, 12, or 24 fps, up to 60 seconds, and up to 16 objects. MP4 and GIF composite transparency onto a chosen background color; use PNG sequences for transparent output.

### Extract frames from a video

1. In the scene workspace's left **Assets** area (`素材`), click **Video Frame Extraction** (`视频抽帧`) and choose a local video.
2. Set the start and end times, fixed sampling rate, and target pixel size. Review the estimated frame count and resource budget.
3. Click **Extract Frames and Add to Scene** (`抽帧并加入场景`). Once complete, arrange the asset with ordinary objects, clips, and keyframes. Undo, redo, and re-extraction through **Update Asset** (`更新素材`) are supported.

Extraction preserves aspect ratio and uses nearest-neighbor resizing. Input files are limited to 512 MiB; the selected segment is limited to 60 seconds and 500 frames; the longest output edge is limited to 512 pixels. Supported inputs depend on the bundled decoder. Invalid formats or unreadable durations produce an error.

The first-frame reference image does not change with the selected time range. Extraction imports images only. It does not import video audio, remove backgrounds, create layers, or redraw footage as pixel art. Import a WAV or MP3 separately for the reference audio track.

## Optional plugins

Both plugin ZIPs are included in the application folder's **`可选插件`** directory, meaning "Optional Plugins." They are neither installed nor enabled by default.

### Install or update a plugin

1. Open **Plugin Manager** (`插件管理…`) from the home screen or **Tools** menu (`工具`).
2. Click **Install Local Plugin** (`安装本地插件…`) and select the plugin ZIP. **Do not extract it.**
3. Click **Enable** (`启用`), save your project, and restart the application.
4. Open the **Physics** (`物理`) or **PMX** tab at the right edge of the canvas.

Enabling and disabling take effect at the next startup. Collapsing the sidebar does not disable a plugin. To update an older plugin, disable it, restart, uninstall it, install the new ZIP, enable it, and restart again. Both plugins can be enabled together.

Plugin packages are executable local code and are not fully sandboxed. Install only trusted plugins. Uninstalling a plugin preserves project parameters, source assets, and generated pixels.

### 2D physics: `pixel-rig-physics-1.2.5.zip`

Select a bound part, then open the **Physics** (`物理`) sidebar to configure relative mass, gravity, elastic following, damping, physics weight, connections, and simplified collision shapes. Try the ears-and-accessory example from **Tools → Part Simulation Plugin Example** (`工具 → 部件模拟插件示例…`).

Physics keeps each bitmap's shape and changes its position and angle. **It does not provide squash-and-stretch, soft bodies, or cloth.** Simplified circle and rectangle collisions do not guarantee that fast-moving objects will never pass through each other.

### PMX / VMD: `pixel-rig-pmx-1.2.4.zip`

Use the right-hand **PMX** tab to enter the 3D workspace, then open the workspace's PMX sidebar. Import a model and adjust its size, XYZ transforms, VMD animation, supported expressions, materials, camera, and pixel output.

Supported features include PMX 2.0, VMD bone animation and IK, vertex morphs, and limited group morphs. **MMD hair and clothing physics are disabled, and PMX 2.1 is unsupported.** The 2D physics plugin does not add 3D physics to PMX. Blender Python add-ons are not compatible.

GLB and FBX work without a plugin or a Blender installation. VMD applies only to PMX; there is no cross-skeleton motion retargeting. Importing a model does not turn a 2D drawing into a 3D character.

## PSD and PNG import

- PSD import supports RGB, 8 bits per channel, canvases up to 512×512, and up to 150 layers and groups with supported basic layered content.
- Complex blending, masks, text, smart objects, and other unsupported features trigger a compatibility report. When layered import cannot reproduce the content reliably, use the composite image saved inside the PSD if available.
- Import does not modify the PSD. Save the result as `.pxrig`. PSD export, PSB, CMYK, 16-bit or 32-bit documents, and full Photoshop rendering are not supported.
- Ordinary PNG import supports images up to 512×512 and files up to 8 MiB. An image larger than the current canvas is previewed before you choose to enlarge the canvas, crop, or cancel.
- Use **Import Sprite Sheet** (`导入精灵表`) for larger sheets. Split by cell size, spacing, and offset. Input files are limited to 8 MiB, edges to 16,384 pixels, and total image area to 32 million pixels. Imported frames remain subject to project resource and frame limits.

## Saving, recovery, and resource limits

- `Ctrl+S` saves; `Ctrl+Shift+S` saves a copy. Saving keeps the previous file as a `.bak` backup.
- Changed projects are autosaved to a recovery copy every 60 seconds. Recovery options appear on the home screen after restarting.
- If saving is cancelled, fails, or the project changes during a save-and-close operation, the project stays open.
- Ordinary character projects use format 3; scenes use format 4. Characters using bone-length scaling or related part-follow settings use format 5. Character formats 1, 2, 3, and 5 can be opened. The first save after upgrading an older character format defaults to a separate copy. Older application versions cannot open newer formats.
- Character projects support canvases up to 512×512, 500 frames, 150 layers and groups, and 256 2D bones.
- Project ZIP files are limited to 128 MiB. Character part images and all Cels together have a 128 MiB decoded RGBA budget; repeated references are counted separately. Scene shared-pixel resources also have a 128 MiB decoded budget.
- These are resource limits, not performance guarantees at maximum capacity. Start with small examples.

## Keyboard shortcuts

| Action                                       | Shortcut                          |
| -------------------------------------------- | --------------------------------- |
| Pencil / Eraser / Fill / Eyedropper          | B / E / G / I                     |
| Rectangular selection / Move                 | M / V                             |
| Current-frame pixel free transform | Ctrl+T |
| Bone tool / Two-bone IK / Binding adjustment | R / K / P                         |
| Pan / Zoom                                   | Space + drag / Ctrl + mouse wheel |
| Save / Save As                               | Ctrl+S / Ctrl+Shift+S             |
| Undo / Redo                                  | Ctrl+Z / Ctrl+Shift+Z             |
| Previous frame / Next frame / Play or pause  | Left arrow / Right arrow / Enter  |
| Cancel a drag or uncommitted edit            | Esc                               |

Canvas shortcuts are suspended while a text input has focus. See the bundled guides for the full shortcut list and workflow details.

## Detailed guides and feedback

The package's **`说明`** directory, meaning "Documentation," contains the following Chinese-language guides:

- `user-guide.zh-CN.md`: pixel drawing, bones, 3D, saving, and export.
- `scene-guide.zh-CN.md`: scenes, objects, cameras, audio, video frame extraction, and film output.
- `plugin-guide.zh-CN.md`: installation, updates, sidebars, and compatibility.
- `physics-guide.zh-CN.md`: 2D simulation parameters and limitations.
- `pixel-brush-guide.zh-CN.md`: brushes and presets.
- `timeline-tracks-update.md`: the new timeline and screenshots.
- `release-notes-v0.4.10.md`: changes and compatibility.
- `plugin-api-v1.md`: the developer interface.

[Report an issue on GitHub](https://github.com/ChariskQAQ/PixelRigStudio/issues) with your application and plugin versions, steps to reproduce, expected behavior, and actual result. Screenshots help. Back up your project before troubleshooting; do not upload private files or models you do not have permission to share.

## Third-party software

The application uses Electron, React, Three.js, and other components. The physics and PMX plugins use Matter.js, Babylon.js, and babylon-mmd. See `THIRD-PARTY-NOTICES.txt` in the package for license notices.

Video encoding runs an LGPL FFmpeg build as a separate process and does not use libx264. Licenses, origin information, and build options are in `resources/runtime`. Fixed FFmpeg source, build recipes, and an index of dependency source locations are in **`第三方源码/FFmpeg`**, meaning "Third-Party Source / FFmpeg." These materials are not a claim that the upstream binary has been independently reproduced or that the package provides a complete offline rebuild environment.
