# LibZoneBrightness-1.0

How bright is the terrain the player is standing on? A small curated table, keyed by UiMapID, of three
bands: **bright** (sand, snow, pale rock), **normal**, **dark** (forest canopy, swamp, plaguelands).

Addons that draw faint washes and grey text over the world ask for the band and adjust their own palettes.
The library knows terrain; it does not know your colours.

```lua
local ZB = LibStub("LibZoneBrightness-1.0")
local band = ZB:GetBand()                       -- "bright" | "normal" | "dark" for the player's current map
local r, g, b = ZB:Adjust(0.95, 0.95, 0.92, "text")   -- brighter on bright terrain
local a = ZB:AdjustAlpha(0.06)                  -- a wash alpha that becomes a real backing on sand
ZB:RegisterCallback(function(band, uiMapID) MyAddon:Retheme(band) end)
```

`/zonebright bright|normal|dark|clear` overrides the current zone per character (saved in `LibZoneBrightnessDB`).

Vendor it with the BigWigs packager / CurseForge `.pkgmeta`:

```yaml
externals:
  Libs/LibZoneBrightness: https://github.com/WoWAddons-Kuro/LibZoneBrightness
```

Era and Forever share Classic UiMapIDs, so one table serves both. MIT.