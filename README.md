# JebRaymarch Clouds

Standalone volumetric cloud renderer for Kerbal Space Program. It does not
depend on EVE (Environmental Visual Enhancements) or any other cloud/graphics
mod: it ships its own shader AssetBundle and drives its own raymarching pass
directly on the flight camera.

Works alongside Scatterer if you have it installed (atmosphere/ocean
scattering) — not required, but cloud rendering composites correctly on top
of Scatterer's effects when both are present.

## Features

- Real-time volumetric raymarched clouds, configured per celestial body via
  `GameData/JebedariumClouds/JebRaymarch/clouds.cfg`.
- Multiple independently-configured altitude layers per body (Kerbin has a low
  cumulus deck, a mid layer and a high thin deck) composited far-to-near.
- Coverage and cloud type driven by photographic source textures for organic,
  non-repetitive distribution.
- Self-shadowing, height-based ambient occlusion, a capped silver-lining glow
  toward the sun, and a bounded screen-space godray pass.
- Cloud-cast shadows on terrain and ocean below.
- Wind drift, independent per layer.

## Requirements

- KSP 1.12.x
- No other mod required. Scatterer is optional but supported.

## Installation

Drop the `JebedariumClouds` folder into `GameData/`, so the plugin ends up at
`GameData/JebedariumClouds/Plugins/JebRaymarch/`.

## In-game settings (F8 or the toolbar button)

Press **F8** in Flight, or click the cloud icon in the stock app launcher, to
open the live tuning window. Each slider has a numeric field next to it for
typing exact values. Changes save automatically to
`PluginData/jebraymarch_settings.cfg`.

| Slider | Effect |
|---|---|
| Edge smoothing | Silhouette anti-aliasing strength |
| Cloud density | Global density multiplier (stacks with each layer's own density) |
| Direct sunlight brightness | Strength of direct sunlight lighting |
| Ambient/skylight brightness | Strength of ambient/skylight fill lighting |
| Shadowed-underside darkness | How dark a cloud's shielded underside gets |
| Opacity buildup (extinction) | How quickly a cloud builds up to fully opaque |
| Ground shadow strength | Strength of cloud-cast shadows on terrain/ocean |
| Wind/animation speed | Multiplier on each layer's configured wind drift speed |
| Godray strength | Strength of the sun-directed light-shaft effect |

## Known limitations

This is a real-time raymarched approximation, not a fully physically-based
multi-scattering volumetric renderer. Distant/scaled-space views (the
background view of Kerbin from deep space, and Map View) show a lightweight
flat cloud overlay instead of the full volumetric effect, since individual
raymarch detail is not resolvable at that scale. The Tracking Station and
Space Center do not show clouds. Interaction with mods other than Scatterer is
untested.

## Credits

Created by **8008lover69**.

## License

See `LICENSE.txt`. Redistribution is permitted with attribution to the
original author.
