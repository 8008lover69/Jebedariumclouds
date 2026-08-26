# Changelog

## v3.0 — Standalone engine

Full rewrite from the obsolete EVE-dependent 3.0.1 build into an original
raymarched shader and plugin with no EVE dependency.

### Rendering

- Fixed clouds disappearing at distance (coverage map was read from too coarse
  a mip level, washing the field to a single value).
- Fixed cube/blocky cloud silhouettes (bad LOD on the 3D noise texture).
- Fixed clouds losing detail at grazing/horizon angles (raymarch step size was
  unbounded over long shell chords).
- Fixed coverage/shadow texture painting across empty sky and space — the root
  cause of many "layers show through each other / through terrain" reports.
- Added an analytic surface-sphere depth fallback so ocean water cannot let
  clouds render through it.
- Fixed cloud noise crawling with the player's movement (sampled raw world
  position instead of a planet-relative offset, so floating-origin recentering
  leaked into the noise field).
- Fixed flat "UFO disc" silhouettes on the thinner upper Kerbin layers (shape
  variation was tied to each layer's noise scale instead of a fixed frequency).
- Reformulated ray/sphere intersection for numerical stability at large
  camera-to-planet distances, eliminating flicker and disappearing clouds from
  orbit.
- Fixed godrays lighting up night-side clouds and bleeding onto the craft (sun
  visibility now checks the planet's bulk, not just screen projection).
- Sorted cloud layers far-to-near each frame so the nearer shell always
  composites on top from any vantage point.
- Made the day/night terminator width look-correct across and along the line.

### Look development

- Replaced procedural coverage/type textures with photographic source textures.
- Added a third (mid-altitude) Kerbin cloud layer.
- Added self-shadowing, height-based ambient occlusion, a Henyey-Greenstein
  phase function with capped silver-lining glow, cloud-cast terrain shadows and
  a screen-space godray pass.
- Gave cloud undersides erosion detail instead of a flat belly.
- Rotated each noise octave's sampling axes to hide the texture's tiling.
- Replaced isotropic post-blur with a directional, edge-aware (FXAA-style)
  blend for silhouette anti-aliasing.
- Tuned wind speed, shape-change speed, cloud scale and density defaults.
- Removed an experimental "random independent clouds" feature.

### Performance

- Distance-based step-count LOD (fewer raymarch/light steps once well above a
  layer's shell).
- Empty-space skipping in the main raymarch (steps grow through consecutive
  clear samples and snap back at the first density).
- Capped light-march/shadow-march step counts and godray sample count.

### UI

- Settings toggle moved to F8 with a stock toolbar button.
- Added a numeric text field next to every slider for exact values.

## v3.0.1 and earlier (discontinued)

Older build that relied on an external cloud framework; superseded by the
standalone engine above.
