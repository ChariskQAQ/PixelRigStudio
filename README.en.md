# Pixel Rig Studio

English | [简体中文](README.md)

An offline pixel drawing and animation tool for Windows. Draw frame by frame, bind character parts to 2D bones, pose them, and bake editable pixel frames. Arrange backgrounds, character clips, and props into short pixel films in the scene workspace.

Current release: **v0.5.2 Preview · Windows x64**. **The application interface and bundled detailed guides are in Simplified Chinese.**

**[Download v0.5.2](https://github.com/ChariskQAQ/PixelRigStudio/releases/tag/v0.5.2)** · [Older releases](https://github.com/ChariskQAQ/PixelRigStudio/releases) · [Report an issue](https://github.com/ChariskQAQ/PixelRigStudio/issues)

The project is still being refined. Start with an example and keep backups of important work. Bones help arrange motion, but rotated pixel outlines and joints still need manual inspection and retouching.

## What's new in 0.5.2

Import `.aseprite` / `.ase` files from Home and the File menu, preserving basic pixel layers and groups, layer properties, animation frames, durations, and tag names/ranges. Indexed/grayscale pixels become RGBA and linked Cels become independent editable images. Unsupported rendering features are reported and block inaccurate imports. Save the result as `.pxrig`; the source file is never overwritten.

Repeated workspace labels and permanent tutorial text have been reduced. Editing scope, binding actions, unsaved changes and safety notices remain visible; tool gestures are available on hover. A fixed two-bone arm texture-mapping experiment is also included; see `说明/uv-arm-prototype.zh-CN.md` for its limits.

## Included 0.5.1 improvements

- **A simpler home screen:** removed repeated format notes. Hide each of the three example shortcuts with its × button; this persists across restarts. **Restore Examples** (`恢复示例`) brings them back without deleting any assets.
- **A new icon:** a pixel P and an offset animation frame, using the same dark slate, cyan, and amber as the editor. Updated across window, title-bar, and Windows executable assets.
- **Includes the 0.5.0 redesign:** shared title bars, toolbars, and save-status displays across character, scene, and 3D workspaces.
- **Pixel-puppet examples:** a character animation, binding exercise, scene, and physics example. The character has 12 parts, 13 bones, and a 12-frame walk.
- **Configurable undo:** **Edit → Undo Steps** (`编辑 → 撤销步数…`) supports 20–500 steps, default 80, with a separate 256 MB pixel-history budget.
- **Plugin and code organization updates:** compatibility checks use API and declared app-version ranges. The editors are split into panels, commands, and interaction logic. Project formats are unchanged.

Full notes for this build are bundled as `说明/release-notes-v0.5.2.md`.

## Download and run

1. Download `PixelRigStudio-v0.5.2-Windows-x64.zip` from the release's Assets section.
2. Extract the **entire** archive to a writable folder and run `PixelRigStudio.exe`.
3. Keep all accompanying DLLs, `resources`, `locales`, and other files. Copying only the EXE will not work.
4. Node.js, Blender, an account, and an internet connection are not required. Windows 10 22H2 or Windows 11 is recommended for video encoding.

The main ZIP includes the offline encoder, four examples, Chinese guides, and both optional plugins. Separate plugin ZIPs are for updates. Verify the app archive, plugins and both READMEs using the release's `SHA256SUMS-v0.5.2.txt`.

The executable is not code-signed and there is no automatic updater. This public repository distributes packages and documentation; **the application's source code is not published here**.

## Make a first character animation

1. Open **Binding and Wave Practice** (`绑定与挥手练习`) from the home screen. Save your own copy with `Ctrl+S`.
2. In **Draw Parts** (`绘制部件`), select the unbound left-forearm image in the object tree. Right-click **Bind to Bone** (`绑定到骨骼…`) and choose the left-forearm bone. Dragging an image onto a bone also starts binding.
3. Switch to **Pose** (`摆姿势`), select the forearm, and use `K` to drag its endpoint. Release to record the current pose; `Esc` cancels the drag.
4. Arrange poses on later frames. Choose hold or linear interpolation and play to check timing.
5. Shift-select a frame range, adjust durations, and use **Animation → Bake Animation** (`动画 → 烘焙动画…`).
6. In **Frame Retouching** (`逐帧修整`), draw on the generated pixel layers. Save the `.pxrig` project, then export PNG, a PNG sequence, or a sprite sheet with JSON.

Draw Parts changes the source used by all poses. Frame Retouching changes the baked frame. Rebaking creates a new result and preserves old results and manual edits.

## Workspaces and features

| Area | Features |
| --- | --- |
| Character / sprite | Pencil, eraser, fill, selection, brush presets, palette and color picker; unified layers-and-bones tree; FK, two-bone IK, pose interpolation, onion skinning, baking and retouching |
| Transforms and layout | Current-Cel selection or whole-Cel position, scale, rotation and shear; base bone-length scaling and part stretching; movable, dockable, floating and resizable panels |
| Scene animation | Reuse backgrounds, character clips and props; arrange clips, object keys, camera motion and one reference audio track; export MP4, GIF or transparent PNG sequences |
| Video frame extraction | Sample a local video's time range into scene assets at a chosen rate and pixel size; does not remove backgrounds or generate layered pixel art |
| 3D to sprites | Built-in GLB / FBX; PMX 2.0 / VMD through a plugin; model transforms, camera, motions and supported expressions, then pixel-frame generation |
| Image import | PNG, fixed-grid sprite sheets, and limited layered PSD; complex PSD files can use their saved composite image |

For scenes, open **Scene Film Example** (`打开场景短片示例`) on the home screen and inspect the two characters, background, camera, and audio. Scene assets are embedded, so moving source files does not break playback or export. Retouch a character in its character project, then update the scene asset.

Interpolation changes transforms; it does not draw missing images. IK is a posing tool, without persistent foot locking. Moving an object in a scene does not rerun baked physics.

## Optional plugins

Both ZIPs are included in the app's `可选插件` (Optional Plugins) folder, and are **not installed or enabled by default**.

| Package | Capability |
| --- | --- |
| `pixel-rig-physics-1.2.7.zip` | 2D elastic following, gravity and simple collisions. Bitmaps keep their shape; no soft bodies, cloth or squash-and-stretch. |
| `pixel-rig-pmx-1.2.6.zip` | PMX 2.0, VMD bone motions, IK and basic morphs. MMD physics is disabled; PMX 2.1 is unsupported. |

Open **Plugin Manager** (`插件管理…`) from home or Tools, select **Install Local Plugin** (`安装本地插件…`), choose the ZIP without extracting it, enable it, save and restart. Use the **Physics** (`物理`) or **PMX** sidebar tab. Both can be enabled together.

These API 1 plugins support app version 0.5.2. Existing physics 1.2.6 / PMX 1.2.5 installations also remain compatible. Older plugins capped at app version 0.4.10 require an update: disable, restart, uninstall, install the bundled replacement, enable and restart. Uninstalling preserves project settings and generated pixels.

Plugins execute local code; install only trusted packages. Blender Python add-ons are not compatible. The 2D physics plugin does not add 3D physics to PMX.

## Keyboard shortcuts

| Action | Shortcut |
| --- | --- |
| Pencil / Eraser / Fill / Eyedropper | B / E / G / I |
| Rectangular selection / Move | M / V |
| Bone / Two-bone IK / Binding adjustment | R / K / P |
| Current-frame pixel free transform | Ctrl+T |
| Pan / Zoom | Space + drag / Ctrl + wheel |
| Save / Save As | Ctrl+S / Ctrl+Shift+S |
| Undo / Redo | Ctrl+Z / Ctrl+Shift+Z |
| Previous / Next frame / Play or pause | Left / Right / Enter |
| Cancel drag or uncommitted edit | Esc |

Canvas shortcuts pause while text inputs have focus. Hidden home shortcuts can be restored with `恢复示例`.

## Saving and limitations

- `.pxrig` uses format 3 for ordinary characters, 4 for scenes, and 5 for bone-length characters. Older character formats 1, 2, 3 and 5 can be opened. Keep copies before upgrading; older apps may not open newer formats.
- Saving retains a `.bak` file; changed projects are autosaved to a recovery copy every 60 seconds. Failed or cancelled saves keep the project open.
- Character limits: 512×512 canvas, 500 frames, 150 layers/groups, 256 2D bones. Scene limits: 512×512, 60 seconds, 16 objects, and 6/8/12/24 fps.
- PSD: RGB, 8 bits/channel, up to 512×512 and 150 layers/groups. Masks, complex blending, text and other unsupported content trigger a report rather than silently importing inaccurate layers. Import only; no PSD export.
- MP4 and GIF use a background color; use PNG sequences for transparency. MP4 is not pixel-lossless. Integer output scaling is supported.
- VMD applies only to PMX; there is no cross-skeleton retargeting. 3D output does not reproduce the complete Blender or MMD renderer.
- Some guide screenshots show earlier UI versions; follow current menu names and text. An English README does not add an English application interface.

## Guides and feedback

The extracted app's `说明` (Documentation) folder contains:

- `user-guide.zh-CN.md`: drawing, binding, animation, 3D, saving and export.
- `scene-guide.zh-CN.md`: scenes, cameras, audio, video extraction and film export.
- `plugin-guide.zh-CN.md` and `physics-guide.zh-CN.md`: plugin setup, updates and physics parameters.
- `pixel-brush-guide.zh-CN.md` and `timeline-tracks-update.md`: brushes and track timelines.
- `plugin-api-v1.md`: the limited developer plugin interface.

Please [report issues](https://github.com/ChariskQAQ/PixelRigStudio/issues) with app/plugin versions, reproduction steps, expected behavior and actual results. Screenshots help. Check for private content and sharing rights before uploading projects or models. Thanks for trying the project :)

## Third-party software

License notices for Electron, React, Three.js, Matter.js, Babylon.js, babylon-mmd and other components are in `THIRD-PARTY-NOTICES.txt`. Video encoding uses an LGPL FFmpeg build as a separate process, without libx264. Licenses and build details are under `resources/runtime`; pinned FFmpeg source, build recipes and dependency source locations are under `第三方源码/FFmpeg`.
