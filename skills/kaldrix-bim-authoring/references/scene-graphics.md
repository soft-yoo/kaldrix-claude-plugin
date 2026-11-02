# Presentation scene graphics

The presentation scene dresses a designed building for the client: 3D models (furniture, garden items,
cars, people) and PBR textures on wall and slab surfaces. Scene graphics are visual only: they never
change quantities, the physical `modelVersion`, estimates or offers. Tools need the GRAPHICS company
module and the `graphics.read`, `graphics.write` and `graphics.delete` scopes.
Project underlays are separate from 3D graphics: their tools use `projects.*` scopes and do not need GRAPHICS.

## Assets come only from the company library

Without the GRAPHICS module there is no 3D graphics at all: no library, no textures or models in the scene.

- `list_graphic_library` searches the Kaldrix graphics library — ready textures and models (furniture, devices
  such as heat pumps, boilers or air conditioners, installations, garden, people) with Polish and English names,
  manufacturer and links. Library items are not used directly: `copy_graphic_library_item` copies one into the
  company library (its own files, counted in the company limits) and returns a `READY` company asset. Check
  `copiedAssetIds` first so you do not copy the same item twice.
- `list_graphic_assets` searches the company library (type `TEXTURE` or `MODEL_3D`, text query, status).
  Only `READY` assets can be used in a scene; textures stay `PROCESSING` until the optimizer finishes.
- `get_graphic_asset` shows one asset with its files and how many projects use it.
- Kaldrix never downloads files from the internet. A new asset must come from bytes the user gave you:
  `upload_graphic_asset_file` (Base64, small files) or `request_graphic_asset_file_upload` and the upload address it returns
  (large files), then `create_graphic_asset` with the returned `fileId`s. Uploads go through the same checks as the application: the person's scopes and
  media type allowlist, extension matching the media type, size limits and a check of the real bytes
  (image signature, self-contained GLB 2.0 header). Check `get_graphic_asset_limits` first.
- A texture needs a `BASE_COLOR` map (optional `NORMAL`, `ROUGHNESS`) and `tileMeters` — the real size
  of one repeat. A model needs one `.glb` file (`MODEL`) and may have a `PREVIEW` image.

## Read the scene before writing

`get_project_scene` returns `sceneVersion`, `modelVersion` and, per floor, the placed models and the
walls and slabs that accept a texture (`surfaceElements` with their `surfaces` and current `textures`).
It also returns the project `mapUnderlay` and each floor's `planUnderlay`, including PDF `pageNumber`.
Set `floorId` for large projects. Every scene write needs `expectedSceneVersion` = the `sceneVersion`
you read; each successful write returns the next `sceneVersion` to use.

- `SCENE_VERSION_CONFLICT` — someone (the user in the 3D view or another agent) changed models,
  textures or underlays since your read. Read `get_project_scene` again and re-plan; never retry blindly.
- Geometry edits (walls, rooms, roofs) do not conflict with scene writes: they change `modelVersion`,
  not `sceneVersion`. A texture write may add the optional `expectedModelVersion` to also refuse a write
  after a geometry change.

## Placing models

`place_graphic_model` puts a `MODEL_3D` on a floor:

- `x`, `y` — plan coordinates in metres (the same plan as `get_floor_detail` and `render_floor_svg`);
- `elevation` — height above the floor base, between 0 and the floor height (default 0);
- `rotationDegrees` — rotation around the vertical axis; `scale` — 0.01 to 50 (default 1);
- `idempotencyKey` — reuse it with identical input after an uncertain response; the retry returns the
  first placement and never creates a second one.

`update_placed_model` moves, rotates, scales, renames or swaps the asset of one placement (only the
fields you send change). `remove_placed_model` needs `confirm=true` after the user explicitly asked for
the removal; the GLB stays in the library.

## Textures on surfaces

`set_element_surface_texture` assigns a `TEXTURE` to one surface of a wall (`WALL_LEFT`, `WALL_RIGHT`,
`WALL_EDGES`) or a slab (`SLAB_TOP`, `SLAB_BOTTOM`, `SLAB_EDGES`); without `surface` it covers every
surface of the element. Other textures, the colour and the material of the element stay.
`clear_element_surface_texture` removes a texture after user approval (`graphics.write`, `graphics.delete`, `confirm=true`); the asset stays in the library.

Typical facade: list the floor's `EXTERNAL` walls from `get_project_scene` and set the same texture on
their outer surface. The outer side depends on the wall direction — when unsure, omit `surface` or ask
the user to check the 3D view.

## Texture on a part of a wall side

`set_wall_texture_region` puts a `TEXTURE` on a rectangle of the left or right side of a wall, painted
over the whole-side texture: tiles up to 1.2 m in a bathroom, a brick band on the lower half of a facade,
another finish between two points of the wall.

- `fromMeters`..`toMeters` — along the wall axis from its first point (the same measure as an opening
  position), within the wall `lengthMeters` from `get_project_scene`; omit `toMeters` for the wall end.
- `bottomMeters`..`topMeters` — above the wall base, within the wall `heightMeters`; omit `topMeters` to
  reach the wall top (a gable or a knee wall is followed under its slope).
- Each size is at least 0.01 m and a wall takes at most 20 regions. Openings stay uncovered.
- Without `regionId` a new region is added on top (later regions win where they overlap); with the
  `regionId` from `textureRegions` the region changes in place. The result returns `textureRegionId`.

Regions keep their saved limits: after the wall gets shorter or lower the application draws only the part
on the wall, and a region beyond the wall shows nothing until you change or remove it.
`remove_wall_texture_region` removes one region after user approval (`graphics.write`, `graphics.delete`, `confirm=true`); the texture stays in the library. Slabs and roofs take
textures on whole surfaces only.

## Saved camera views

`get_project_scene_viewpoints` (`graphics.read`) returns saved camera views and current scene/model versions.
`save_scene_viewpoint` (`graphics.write`, `graphics.delete` and `confirm=true` after user approval) saves a complete camera view with a stable caller-chosen
UUID. Reuse that UUID and identical data after a lost response; the retry does not create another view or change
the scene version. A project holds up to 30 views, with names of 1 to 80 characters.

Camera `position` and `target` use absolute project world metres: X/Z are the plan and Y is elevation from the
project origin, not height above a floor. They must differ. `fovDegrees` is the vertical field of view (10 to 120).
Save the sunlight study as `sunEnabled`, `sunLatitude` (-90 to 90), `sunDayOfYear` (1 to 366), `sunHour` (0 to 24)
and `sunNorthOffset` (0 to 360 degrees). Restoring these settings does not edit the project orientation.

The saved geometry scope must be restored before applying the camera: `PROJECT` has no building/floor IDs,
`BUILDING` has only an existing `buildingId`, and `FLOOR` has only an existing `floorId`. All referenced geometry
must belong to the project. If a saved scope was removed later, the application explains that the view cannot be
opened instead of applying its camera to another floor.

Every write needs the exact non-negative `expectedSceneVersion`. An outdated different write fails with
`SCENE_VERSION_CONFLICT`; read again before changing it. `remove_scene_viewpoint` needs the person's
`graphics.delete` and `confirm=true` after the user requests removal. Removing an already absent view is safe to retry.
View writes change only `sceneVersion`; physical geometry, quantities, library assets and documents stay unchanged.

These tools save camera metadata. Presentation image rendering to project documents or offers remains planned in KDX-176.

## Floor plan and map underlays

Read `get_project_underlays` with `projects.read` before changing an underlay. It returns only the project
map and floor plan underlays, their document IDs and placement, plus `sceneVersion` and `modelVersion`.
An optional `floorId` restricts the floor list. This read works without GRAPHICS and never exposes 3D assets.
Set `expectedSceneVersion` to the exact non-negative `sceneVersion`; after `SCENE_VERSION_CONFLICT`,
reread and review the placement. Underlay writes do not change physical quantities or `modelVersion`.

- `set_floor_plan_underlay` (`projects.write`, `projects.delete`, `confirm=true`) needs a READY image or PDF document belonging to this
  project, a floor ID, width, height, centre X/Y in plan metres and optional rotation in degrees. For a PDF,
  set `pageNumber` starting at 1 (default 1); the page image must already be ready. For an image the page
  number is ignored. Use the document page tools to prepare a PDF page before attaching it.
- `set_project_map_underlay` (`projects.write`, `projects.delete`, `confirm=true`) needs a READY image document belonging to this project.
  `CUSTOM` requires `centerWorldXMeters` and `centerWorldYMeters` and forbids geographic coordinates.
  `GEOPORTAL`, `GEOPORTAL_CADASTRAL` and `GEOPORTAL_UTILITIES` require `centerLatitude` and
  `centerLongitude`; they may also carry both world-centre values for independent plan placement.
  `groundWidthMeters` and `groundHeightMeters` describe the covered ground. `rotationDeg` rotates the
  image clockwise independently of project north. This tool uses an existing document, never a URL fetch.
- `clear_floor_plan_underlay` and `clear_project_map_underlay` use `projects.delete` and require
  `confirm=true` after the user requested detaching the underlay. They remove the reference and saved
  placement; the document and PDF page images remain. Replacing an underlay also retains the old document.
  Clearing an already empty underlay is a no-op at the current version.
